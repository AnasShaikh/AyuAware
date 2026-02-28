# AyuAware — Backend Architecture Overview

---

## The Two-Layer Data Model

Every feature in AyuAware is built on two data layers per user.

| Layer | Name | Nature | When Set | Table |
|---|---|---|---|---|
| **1** | Prakriti (Constitution) | Static — who the user fundamentally is | Once, at onboarding | `user_constitution` |
| **2** | Vikriti (Current State) | Dynamic — how the user is right now | Continuously, via all data streams | `user_current_state` |

**Prakriti** is the immutable baseline: Vata %, Pitta %, Kapha % captured from a 60-question assessment. It never changes (users may re-assess after 90 days). Every AI call includes Prakriti in context.

**Vikriti** is a live snapshot of imbalance: `vata_imbalance`, `pitta_imbalance`, `kapha_imbalance` (each −10 to +10 from Prakriti baseline), plus `agni_state`, `ama_level`, `ojas_level`. Every data stream feeds into Vikriti.

---

## Health Data Streams

Multi-modal inputs that continuously update Vikriti.

| Stream | Source | Cadence | What it updates |
|---|---|---|---|
| **Wearable data** | Apple HealthKit (MVP), Oura, WHOOP (V2) | Hourly background sync | Sleep patterns → Vata/Pitta/Kapha signals; HRV → Ojas level |
| **Daily check-in** | User submits 5 answers in-app | User-triggered, ideally daily | Direct Vikriti: digestion → Agni state; mood → dosha imbalance delta |
| **Visual diagnostics** | Camera scan: tongue, meal, skin, product | User-triggered | Tongue coating → Ama level; meal scan → six-taste balance |
| **Lab results** | PDF upload | Occasional | Biomarkers → dhatu/dosha interpretation; flags for protocol adjustment |
| **Manual logs** | In-app: meals, symptoms, meditation, cycle | User-triggered | Symptom tracking; lifestyle patterns |
| **Genetic data** | 23andMe/Ancestry raw data | One-time upload (V2) | Constitutional validation; predisposition flags |

---

## Types of User Interactions

### 1. Onboarding
First-time setup. Captures Prakriti, personalises the Digital Twin, and generates the user's first protocol. Happens once.

### 2. Daily Check-In
Quick 5-question form (energy, sleep, digestion, mood, symptoms). The primary mechanism for updating Vikriti when no wearable is connected.

### 3. One-Off Query
Any ad-hoc message the user sends to the Digital Twin — health questions, scan analysis requests, "how am I doing?", etc. Can also trigger a protocol change.

### 4. Data Ingestion (background)
Wearable sync, lab upload, image scan. May happen without the user actively chatting. Can trigger Vikriti updates, prediction alerts, or protocol modification suggestions.

---

## Types of Backend Workflows

### A. Data Store
Pure write: receive incoming data → interpret through Ayurvedic lens → update Vikriti → check for alert triggers. No AI conversation involved.

### B. Protocol Creation
AI generates a structured wellness plan from the user's current Prakriti + Vikriti + goals. User reviews and activates.

### C. Protocol Modification
An existing active protocol is adjusted. Can be triggered by a chat conversation, poor adherence, new data, or a seasonal change.

---

## Backend Flows

---

### Onboarding Flow

**Goal:** Capture Prakriti and store it as the user's permanent constitutional baseline.

```
1. User registers (email / Apple Sign-In / Google)
   → INSERT users row, set onboarding_complete = false

2. User completes 60-question Prakriti assessment
   → Scoring algorithm runs server-side
   → INSERT user_constitution { vata_pct, pitta_pct, kapha_pct, responses }
   → INSERT user_current_state { all imbalances = 0, agni = sama, ama = none, ojas = 7 }

3. User names their Digital Twin, sets communication style
   → INSERT user_twin_preferences

4. (Optional) Apple HealthKit authorization
   → INSERT user_wearable_devices
   → Enqueue wearable_initial_sync job (reads last 30 days of HealthKit data)

5. Onboarding deep-dive conversation
   → Standard chat flow, conversation_type = 'onboarding'
   → Twin asks about symptoms, lifestyle, goals
   → Responses update user_health_profile (conditions, medications, goals)

6. First protocol generation
   → POST /protocols/generate (triggered at end of onboarding chat)
   → AI assembles: Prakriti + Vikriti + health goals
   → INSERT protocols { status: 'draft' }
   → User reviews → taps Accept
   → UPDATE protocols { status: 'active', activated_at: now }
   → SET users.onboarding_complete = true
```

---

### Daily Check-In Flow

**Goal:** Update Vikriti from user-reported symptoms and give an immediate AI insight.

```
1. User submits 5 answers:
   energy_level (1–10), sleep_quality (1–10),
   digestion_state, mood, symptoms[]

2. INSERT daily_checkins (TimescaleDB hypertable)

3. Vikriti update rules applied synchronously:
   digestion = burning   → agni = tikshna, pitta_imbalance += 1
   digestion = sluggish  → agni = manda,   kapha_imbalance += 1
   digestion = variable  → agni = vishama,  vata_imbalance += 1
   mood = anxious        → vata_imbalance += 1
   mood = irritable      → pitta_imbalance += 1
   mood = heavy          → kapha_imbalance += 1
   energy ≤ 3            → ojas_level -= 1

4. UPDATE user_current_state { new deltas, last_updated_by = 'checkin' }

5. Enqueue checkin_insight job (async)
   → Claude Haiku generates 2–3 sentence pattern observation + 1 tip
   → INSERT message into daily check-in conversation

6. Check alert triggers:
   If same dosha signal 3+ consecutive days → enqueue prediction_alert job
```

---

### One-Off Query Flow

**Goal:** User sends a message → Digital Twin responds with full personalised context.

```
1. User sends message (WebSocket emit: chat:send)

2. Auth check + usage limit check (Free: 20 msgs/month cap)

3. Context assembly:
   a. Prakriti (user_constitution)
   b. Vikriti (user_current_state)
   c. Active protocol summary + today's recommendations
   d. Last 7 daily_checkins
   e. Recent wearable summary (if connected)
   f. Last N messages from this conversation (N by tier: Free=5, Personal=10, Premium=20)
   g. user_health_profile (conditions, medications, goals)
   h. Current date, season, time of day

4. Claude API call (Sonnet, streaming)
   → System prompt = base Master Prompt + dynamic context block
   → Tools available for Claude to call during response

5. If Claude calls a tool mid-stream:
   → Tool handler executes (e.g., check_herb_safety queries user medications from DB)
   → Result returned to Claude as tool_result
   → Stream continues

6. Stream chunks forwarded to client via WebSocket (chat:chunk events)

7. On stream complete:
   → INSERT conversation (if new), INSERT user message, INSERT twin response
   → INCREMENT usage_counters.ai_messages
   → emit chat:complete

--- If Claude calls create_protocol or modify_protocol tool:
   → See Protocol Creation / Modification flows below
```

---

### Data Ingestion Flow — Wearable Sync

**Goal:** Translate raw device metrics into Ayurvedic signals and update Vikriti.

```
1. iOS app reads HealthKit data since last_synced_at
   → POST /wearables/sync { deviceType, dataPoints[] }

2. BATCH INSERT wearable_data_points (TimescaleDB)

3. Interpret each significant data point:
   Sleep < 6h or > 3 awakenings    → vata_signal
   Sleep waking 10pm–2am           → pitta_signal
   Sleep > 9h, hard to wake        → kapha_signal
   HRV 7-day avg < 30ms            → ojas concern flag
   HRV declining > 20% over 3 days → prediction_alert trigger

4. If signals consistent over 3+ days:
   → UPDATE user_current_state (dosha imbalance deltas)

5. UPDATE user_wearable_devices.last_synced_at

6. Check prediction alert threshold → enqueue if triggered
```

---

### Data Ingestion Flow — Lab Upload

**Goal:** Extract biomarkers from a lab PDF, interpret them through an Ayurvedic lens, and surface insights.

```
1. User uploads PDF → S3 via presigned URL
   → POST /health/lab/confirm { fileKey, testDate }
   → INSERT lab_results { status: 'pending' }
   → Enqueue lab_ocr_processing job

2. Background job:
   a. Download PDF from S3
   b. Claude Vision: extract all biomarker names, values, units, reference ranges
   c. For each biomarker:
      → Map to dhatu (tissue layer) + dosha correlation
      → Flag if outside reference range
   d. Synthesize cross-biomarker patterns
   e. Generate: overall_pattern, root_cause_analysis, action_plan
   f. UPDATE lab_results { biomarkers, interpretations, status: 'complete' }
   g. Push notification: "Your lab results are ready"

3. Vikriti reassessment:
   → Significant abnormalities update user_current_state
   → If new data conflicts with active protocol recommendations
     → Enqueue protocol_review suggestion
```

---

### Protocol Creation Flow

**Goal:** Generate a structured, phased wellness plan personalised to the user's current state.

**Triggers:** End of onboarding, user chat request, direct "New Protocol" action.

```
1. POST /protocols/generate { primaryConcern, duration?, intensity? }

2. Assemble context:
   Prakriti + Vikriti + active symptoms + health goals
   + lifestyle constraints (from user_health_profile)
   + current season
   + existing active protocols (to avoid conflicts)

3. Claude API call with protocol_generation prompt:
   → Returns structured protocol: name, 3 phases, recommendations per category
     (Dietary / Lifestyle / Herbs / Practices / Environmental)
   → Each recommendation includes: action, frequency, timing, rationale, tips

4. Herb safety check (for every herb in recommendations):
   → Cross-reference user's current_medications
   → Cross-reference user's medical_conditions
   → Remove or flag unsafe recommendations

5. INSERT protocols { status: 'draft' }
   INSERT protocol_versions { version: 1, snapshot }

6. Return protocol object to client as protocol_card message type

7. User reviews and taps Accept:
   → POST /protocols/:id/activate
   → UPDATE protocols { status: 'active', activated_at: now }
   → If plan limit reached (Free = 1): pause existing active protocol
   → Schedule daily protocol reminder notifications
```

---

### Protocol Modification Flow

**Goal:** Adjust an active protocol in response to new information or user feedback.

**Triggers (any of these):**

| Trigger | Source | Mechanism |
|---|---|---|
| User says "this is too hard" in chat | One-off conversation | Claude calls `modify_protocol` tool |
| New lab result changes health picture | Lab ingestion flow | ProtocolService.reviewActiveProtocols() |
| Adherence < 40% for 5+ days | Nightly background job | Protocol review suggestion notification |
| Seasonal change | Scheduled job (quarterly) | AI generates seasonal adjustment |

```
For ALL triggers:

1. Snapshot current protocol state:
   INSERT protocol_versions { version: N, snapshot: full_protocol_json }

2. Apply modification:
   UPDATE protocols.recommendations (JSONB patch)
   UPDATE protocols.version += 1

3. Return updated protocol to user:
   → Chat: Twin confirms change in conversation
   → Notification: "Your protocol has been updated"

--- For conversation-triggered modification (most common):

Claude mid-conversation calls modify_protocol tool:
  Input: { protocolId, modifications[], changeReason }
  → ToolExecutorService routes to ProtocolService.modify()
  → Above steps 1-2 execute
  → Tool result returned to Claude
  → Claude confirms change in natural language in chat
```

---

## How Flows Connect

```
ONBOARDING
  └─→ Prakriti stored (permanent)
  └─→ Vikriti initialized (zeros)
  └─→ First Protocol created

DAILY CHECK-IN / WEARABLE SYNC / LAB UPLOAD
  └─→ Vikriti updated
  └─→ May trigger: Prediction Alert
  └─→ May trigger: Protocol Modification suggestion

ONE-OFF QUERY
  └─→ Reads: Prakriti + Vikriti + active protocol
  └─→ May trigger: Protocol Creation (via tool)
  └─→ May trigger: Protocol Modification (via tool)
  └─→ May trigger: Check-In logging (via tool, if user reports symptoms mid-chat)

PROTOCOL ACTIVE
  └─→ Generates daily recommendations (Today section)
  └─→ Tracked via protocol_tracking (adherence)
  └─→ Modified by: conversation, new data, adherence alerts, season
```
