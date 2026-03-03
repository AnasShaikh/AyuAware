# AyuAware — Session Log: March 3, 2026

---

## Session Overview

First technical deep-dive session. Set up the GitHub repo, analyzed documentation coverage across all major app screens, and identified gaps that need resolution before development begins.

---

## Changes Made

1. **GitHub repo created** at https://github.com/AnasShaikh/AyuAware — pushed all existing documentation (41 files)
2. **README.md added** — project overview, tech stack, structure
3. **team-exchange-figma-feedback-2026-03-03.md** — saved Figma prototype review email exchange between Anas, Shiv, Nikhel, and Armand
4. **prakriti-dosha-questionnaire.md** — saved 18-question Prakriti quiz with scoring logic from Shiv's email

---

## Research & Analysis

### Health Pillars — DB Field Mapping

Analyzed all 7 health pillar screens against the database schema in the Final Technical PRD.

| Pillar | Primary DB Source | Score Formula | Build-Ready? |
|--------|------------------|---------------|-------------|
| **Prakriti** | `user_constitution` (vata/pitta/kapha_percentage) | Undefined — "alignment" score needs definition | Mostly |
| **Vikriti** | `user_current_state` (imbalance deltas) | Needs imbalance-to-percentage conversion | Mostly |
| **Agni** | `user_current_state.agni_state` (enum) | Needs enum-to-percentage mapping | Yes |
| **Ojas** | `user_current_state.ojas_level` (1-10) | Straightforward: level × 10 | Yes |
| **Manas** | No DB fields exist | No tangible parameter — needs full design | No |
| **Nidra** | `daily_checkins.sleep_quality` + wearable sleep data | No aggregation formula defined | Partial |
| **Prana** | `daily_checkins.energy_level` + wearable HRV/activity | PRD says "qualitative" — most vague | No |

### Exposure Screens — Doc Coverage

| Screen | Data Source | Build-Ready? |
|--------|-----------|-------------|
| **Weather/AQI** | External API (OpenWeatherMap) | Yes — dosha scoring formulas fully defined |
| **Light/Circadian** | External API + calculation | Yes — UV, Brahma Muhurta formula defined |
| **Lunar Influence** | Astronomical calculation + Claude AI | Yes — 8 phases mapped to dosha effects |
| **Astrology** | Unclear API + Claude AI | Partial — data model exists but no API chosen |
| **Weather Protocol** | Claude AI generates it | Yes — prompt + response structure defined |
| **Shop/Products** | `shop_products` DB table | Yes — schema exists, needs product catalog seeded |

### Profile Section — Doc Coverage

Profile is ~90% ready. Core sections (constitution, settings, preferences, wearables, privacy, subscription) all map to existing DB tables.

**Gaps identified:**
- No `vikriti_history` table for constitutional timeline graph
- No `practitioners` table for practitioner connection feature
- No gamification/leveling system defined for "Level 3 Apprentice" badge

---

## Key Decisions (from team email exchange)

1. **Wearable is mandatory** at onboarding — no "no data" fallback screens needed
2. **Spike** is the wearable data aggregator (replaces direct HealthKit/Oura/WHOOP integration from PRD)
3. **Prakriti quiz starts at 18 questions** (not 60 as PRD states), expanding to 50 later
4. **Scoring logic confirmed**: Option A = Vata, B = Pitta, C = Kapha. Bi-doshic if second highest within 15-20% of first
5. **Astrology inputs**: DOB, place of birth, sex (minimum) — prompt design TBD
6. **Login screens** need to be added to Figma
7. **Figma flow arrows** update incoming from design team

---

## Open Items / Unresolved

| Item | Status | Owner |
|------|--------|-------|
| Manas calculation formula | Undefined | Team — needs collaborative design |
| Prana calculation formula | Undefined | Team — needs collaborative design |
| Prakriti "alignment" score definition | Undefined | Team |
| Nidra score weighting (check-in vs wearable) | Partially resolved — wearable mandatory | Team |
| Vedic astrology API selection | TBD | Shiv researching |
| Astrology prompt design | TBD | Shiv/Nikhel |
| "Complete Full Assessment" button — screen missing in Figma | Unanswered | Nikhel |
| Product catalog seeding for Shop | Not started | Team |
| Vikriti history table schema | Not in PRD | Dev |
| Practitioner tables schema | Not in PRD | Dev |
| Spike integration (replacing direct wearable APIs) | New requirement — not in PRD | Dev |

---

## Next Steps

- **Thursday, March 5 call** — development strategy discussion (Anas, Shiv, Nikhel, Armand)
- Finalize Manas & Prana formulas
- Receive updated Figma with flow arrows
- Receive 18 Prakriti questions (confirmed in questionnaire doc)
- Begin MVP development planning post-call
