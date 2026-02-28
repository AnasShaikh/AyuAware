# AyuAware — Final Technical PRD
### Source of Truth Document for Development

**Version:** 1.0
**Date:** February 2026
**Phase:** Phase 1 Deliverable — Technical Scoping & Architecture Design
**Status:** Final

---

> This document is the single source of truth for AyuAware development. It consolidates all Phase 1 deliverables: technical architecture design, user and backend flow charting, database schema, technology stack recommendation, and implementation specifications. All development decisions should reference this document first.

---

## Table of Contents

1. [Product Overview](#1-product-overview)
2. [Technology Stack Recommendation](#2-technology-stack-recommendation)
3. [System Architecture](#3-system-architecture)
4. [Data Architecture & Database Schema](#4-data-architecture--database-schema)
5. [Feature Priority Tiers & MVP Scope](#5-feature-priority-tiers--mvp-scope)
6. [User Flows & Backend Flows](#6-user-flows--backend-flows)
7. [API Contracts](#7-api-contracts)
8. [AI Integration Design (Claude API)](#8-ai-integration-design-claude-api)
9. [Module Technical Specifications](#9-module-technical-specifications)
10. [External Integrations](#10-external-integrations)
11. [Security & Compliance](#11-security--compliance)
12. [Infrastructure & Deployment](#12-infrastructure--deployment)

---

## 1. Product Overview

### 1.1 What is AyuAware?

AyuAware is an AI-powered Ayurvedic Digital Health Companion. It combines classical Ayurvedic principles with modern health data and large language model AI to deliver a personalized, continuously learning health guidance system.

The core product is the **Digital Twin** — a persistent AI model of each user built from their constitutional type (Prakriti), current health state (Vikriti), and continuously updated health data streams. The Digital Twin converses naturally, generates personalized wellness protocols, and proactively alerts users to imbalances before symptoms manifest.

### 1.2 Core Value Proposition

| Traditional Ayurveda | AyuAware Digital Twin |
|---|---|
| One-time practitioner visit | Persistent, always-available AI companion |
| Subjective pulse/tongue diagnosis | Multi-modal data (wearables, labs, images, logs) |
| Generic dosha advice | Personalized to individual constitution + current state |
| Static protocol | Dynamically adjusted based on adherence and new data |
| Expensive and inaccessible | Scalable, freemium model |

### 1.3 Platform

- **Primary:** iOS mobile app (React Native)
- **Backend:** RESTful API (Node.js/NestJS)
- **AI:** Claude API (Anthropic)
- **Cloud:** AWS (HIPAA-eligible infrastructure)
- **Android:** Enabled by React Native architecture, planned post-MVP

### 1.4 User Tiers

| Plan | Price | Key Limits |
|---|---|---|
| Free | $0 | 20 AI messages/month, manual data only, 1 protocol |
| Personal | $9.99/mo | Unlimited messages, wearable integration, 10 image scans/month |
| Premium | $24.99/mo | Lab results upload (3/month), genetic data, 3 active protocols |
| Practitioner | $99/mo | Manage up to 20 client accounts, HIPAA messaging |
| Enterprise | Custom | Unlimited accounts, white-labeling, dedicated support |

### 1.5 Ayurvedic Conceptual Foundation

Understanding these core concepts is necessary to understand the data architecture and AI design:

| Concept | Description | Technical Role |
|---|---|---|
| **Prakriti** | Birth constitution — immutable Vata/Pitta/Kapha percentages | Static user record, set at onboarding |
| **Vikriti** | Current dosha imbalance state | Dynamic record, updated by all data streams |
| **Agni** | Digestive fire — Sama (balanced), Vishama (irregular), Tikshna (sharp), Manda (slow) | Field on Vikriti; informed by digestion logs and wearables |
| **Ama** | Accumulated toxins from poor digestion — None/Low/Moderate/High | Field on Vikriti; informed by tongue scans, check-ins |
| **Ojas** | Vital essence/immunity (1–10 scale) | Field on Vikriti; informed by HRV, sleep, stress data |
| **Doshas** | Vata (Air+Space), Pitta (Fire+Water), Kapha (Water+Earth) | Core classification system throughout |

---

## 2. Technology Stack Recommendation

### 2.1 Recommended Stack

| Layer | Technology | Version | Rationale |
|---|---|---|---|
| **Mobile** | React Native | 0.73+ | iOS-first with zero-cost Android path. TypeScript throughout. Expo managed workflow for faster iteration. Large ecosystem, strong HealthKit support via `react-native-health`. |
| **Backend Language** | Node.js + TypeScript | Node 20 LTS | Same language as mobile (shared types/validation schemas). NestJS framework provides structured, enterprise-grade architecture with dependency injection, guards, and decorators. |
| **Backend Framework** | NestJS | 10.x | Modular architecture maps cleanly to AyuAware's 13 modules. Built-in support for WebSockets, queues, guards for auth/subscription checks. |
| **Primary Database** | PostgreSQL | 15+ (AWS RDS) | Relational integrity for user data, protocols, and relationships. JSONB columns for flexible Ayurvedic metadata. HIPAA-eligible on AWS RDS. Full-text search via `pg_trgm`. |
| **Time-Series Extension** | TimescaleDB | Latest | Extension on the same PostgreSQL instance. Wearable data and check-in data are time-series by nature — TimescaleDB provides hypertables with automatic partitioning and 10–100x faster time-range queries at scale. |
| **Cache / Sessions** | Redis | 7.x (AWS ElastiCache) | JWT token blacklist, rate limiting, AI response caching for common queries, session storage. Sub-millisecond access. |
| **File Storage** | AWS S3 + KMS | — | Images (tongue, meal, skin scans), lab result PDFs, genetic data files. Server-side encryption with AWS KMS. Presigned URLs for secure client upload/download. |
| **AI Model** | Claude Sonnet (primary), Claude Haiku (fallback) | claude-sonnet-4-5 / claude-haiku-3 | Claude Sonnet handles all core Digital Twin conversations, protocol generation, and image analysis. Haiku fallback for simple FAQ-type queries during high load. Both via Anthropic API. |
| **Real-time / Streaming** | WebSockets (Socket.io) | 4.x | Chat response streaming from Claude API to client. Also used for real-time sync notifications when wearable data arrives. |
| **Authentication** | JWT + OAuth 2.0 | — | JWT (7-day access, 30-day refresh). Apple Sign-In (required for iOS App Store). Google OAuth. Email/password with bcrypt hashing. |
| **Payments (Global)** | Stripe (USD/EUR) + Razorpay (INR) | Latest SDKs | Stripe handles all non-India subscriptions. Razorpay handles India-based users (INR, UPI, local cards). User locale detected at signup determines gateway routing. Both use webhook-driven plan change events. |
| **Push Notifications** | APNs (via Expo Notifications) | — | Morning summary delivery, prediction alerts, protocol reminders. |
| **Background Jobs** | BullMQ (Redis-backed) | 5.x | Wearable sync jobs (hourly), morning summary generation (daily), prediction alert analysis (every 6 hours), lab OCR processing (async). |
| **Search** | PostgreSQL FTS (`pg_trgm`) | — | Conversation history search, protocol library search. Sufficient for MVP; Elasticsearch can replace if needed at scale. |
| **Monitoring** | Sentry + CloudWatch | — | Sentry for application error tracking (mobile + backend). CloudWatch for infra metrics, alarms, and log aggregation. |
| **MVP Deployment** | Railway.app or Fly.io | — | **For 1-2 developer teams at MVP:** managed deployment removes DevOps burden. Railway Postgres + Upstash Redis replaces RDS + ElastiCache. Migrate to ECS Fargate when team grows or MRR justifies dedicated DevOps. |
| **CI/CD** | GitHub Actions → deploy target | — | MVP: GitHub Actions → Railway/Fly.io deploy. Production: GitHub Actions → AWS ECR → ECS blue/green. |

### 2.2 Ayurvedic Intelligence Layer

The Ayurvedic Intelligence Layer is not a separate service — it is implemented through a combination of:

1. **Claude API** — provides all Ayurvedic reasoning, herb/food knowledge, and personalization from its training data
2. **AI Response Cache** — PostgreSQL `herbs` and `foods` tables cache Claude's generated responses for consistency and speed; populated incrementally as users query (not pre-seeded)
3. **Business Logic Layer** — NestJS services that assemble user context, run scoring algorithms, and format data for Claude

> **Important caveat:** AyuAware's Ayurvedic knowledge is AI-generated from Claude's training data, not from a manually curated and practitioner-validated database. This is acceptable for MVP but should be flagged to users ("AI-generated guidance — consult a practitioner for clinical decisions"). A curated, practitioner-validated knowledge base is a Phase 2 quality milestone.

```
User Input
    ↓
Context Assembly Service (NestJS)
  - Prakriti + Vikriti
  - Recent check-ins (7 days)
  - Active protocol summary
  - Relevant conversation history
  - Current season/date
    ↓
Claude API (Sonnet) with Tool Definitions
  - Herb/food knowledge: generated from Claude's training data
  - Herb safety: cross-referenced against user's medications (from DB)
  - Cached responses optionally stored in herbs/foods tables
    ↓
Structured Response → WebSocket Stream → Mobile Client
```

### 2.3 Why Not [Alternative]

| Alternative | Why Rejected |
|---|---|
| Flutter | Dart ecosystem is smaller; React Native has better HealthKit libraries and larger talent pool |
| Python/FastAPI backend | Would require context switching between Python backend and TypeScript mobile; Node.js enables shared type definitions |
| MongoDB | Lack of relational integrity is a problem for health data with complex relationships; PostgreSQL's JSONB covers document storage needs |
| Firebase | Not HIPAA-eligible out of the box; limited support for complex queries; vendor lock-in risk |
| OpenAI GPT-4 | Claude's 200k context window is essential for maintaining long health conversation histories; superior instruction-following for structured protocol generation |
| Separate TimescaleDB instance | Running as extension on the same RDS instance avoids operational overhead for MVP; migrate to dedicated instance at scale |

---

## 3. System Architecture

### 3.1 High-Level Architecture

```
┌─────────────────────────────────────────────────────┐
│                   iOS App (React Native)             │
│  Chat UI │ Insights │ Protocols │ Today │ Profile    │
└──────────────────────┬──────────────────────────────┘
                       │ REST / WebSocket
                       ▼
┌─────────────────────────────────────────────────────┐
│              AWS Application Load Balancer           │
└──────────────────────┬──────────────────────────────┘
                       │
          ┌────────────┴────────────┐
          ▼                         ▼
┌─────────────────┐       ┌─────────────────────┐
│  NestJS API     │       │  Background Workers  │
│  (ECS Fargate)  │       │  (ECS Fargate)       │
│                 │       │  - Wearable sync     │
│  REST Modules:  │       │  - Morning summary   │
│  Auth           │       │  - Prediction scan   │
│  User           │       │  - Lab OCR           │
│  Assessment     │       │  (BullMQ / Redis)    │
│  Chat           │       └──────────┬──────────┘
│  Health         │                  │
│  Protocols      │       ┌──────────▼──────────┐
│  Insights       │       │   Anthropic API      │
│  Notifications  │◄─────►│   (Claude Sonnet)    │
└────────┬────────┘       └─────────────────────┘
         │
    ┌────┴──────────────────────────┐
    │                               │
    ▼                               ▼
┌──────────────┐           ┌──────────────────┐
│  PostgreSQL  │           │  Redis           │
│  + TimescaleDB│          │  (ElastiCache)   │
│  (AWS RDS)   │           │  Sessions/Cache  │
└──────────────┘           └──────────────────┘
         │
    ┌────┴──────────────────────────┐
    │                               │
    ▼                               ▼
┌──────────────┐           ┌──────────────────┐
│  AWS S3      │           │  Apple HealthKit  │
│  Images/PDFs │           │  (iOS native)    │
└──────────────┘           └──────────────────┘
```

### 3.2 Component Responsibilities

| Component | Responsibility |
|---|---|
| **iOS App** | UI rendering, HealthKit integration, camera/file access, push notification handling, WebSocket client |
| **NestJS API** | Business logic, auth, context assembly, Claude API calls, data persistence |
| **Background Workers** | Async tasks: wearable sync, morning summary generation, prediction analysis, OCR processing |
| **PostgreSQL + TimescaleDB** | All persistent data — user profiles, health data, protocols, conversations |
| **Redis** | Token blacklist, rate limit counters, BullMQ job queue, AI response cache (60s TTL for FAQ-type responses) |
| **S3** | Binary storage — scan images, lab PDFs, genetic data files, exported reports |
| **Claude API** | Core AI reasoning — chat, protocol generation, image analysis, morning summaries, predictions |
| **Apple HealthKit** | Native iOS data source — sleep, HRV, heart rate, steps, active energy |
| **Stripe** | Subscription lifecycle, payment processing, webhook events |
| **APNs** | Push notification delivery for morning summaries and alerts |

### 3.3 NestJS Module Structure

```
src/
├── modules/
│   ├── auth/           # Registration, login, OAuth, JWT
│   ├── users/          # Profile, preferences, constitution
│   ├── assessment/     # Prakriti quiz, Vikriti check
│   ├── chat/           # Conversations, messages, streaming
│   ├── health/         # Check-ins, scans, lab uploads
│   ├── wearables/      # HealthKit sync, device management
│   ├── protocols/      # Protocol CRUD, activation, tracking
│   ├── insights/       # Dashboard aggregates
│   ├── notifications/  # Morning summary, prediction alerts
│   ├── twin/           # Digital Twin profile, preferences
│   ├── shop/           # Product catalog, orders
│   ├── learn/          # Content, lessons, progress
│   └── projects/       # Long-term health goals
├── shared/
│   ├── ai/             # Claude API client, context assembly
│   ├── knowledge/      # Ayurvedic DB queries (herbs, foods)
│   ├── queue/          # BullMQ job definitions
│   └── guards/         # Auth guard, subscription tier guard
└── main.ts
```

---

## 4. Data Architecture & Database Schema

### 4.1 Data Categories

| Category | Nature | Storage | Update Cadence |
|---|---|---|---|
| **Prakriti (Constitution)** | Static | PostgreSQL | Once (onboarding), re-assessable |
| **Vikriti (Current State)** | Dynamic summary | PostgreSQL | On every data ingestion event |
| **Daily Check-Ins** | Time-series | TimescaleDB hypertable | User-triggered, typically daily |
| **Wearable Data** | Time-series | TimescaleDB hypertable | Hourly background sync |
| **Lab Results** | One-time documents | PostgreSQL + S3 | On user upload |
| **Scan Analyses** | Event-based | PostgreSQL + S3 | User-triggered |
| **Genetic Profiles** | One-time document | PostgreSQL + S3 | On user upload |
| **Protocols** | Structured documents | PostgreSQL (JSONB) | On creation/modification |
| **Conversations/Messages** | Append-only log | PostgreSQL | On every message |
| **Manual Logs** | Event-based | PostgreSQL | User-triggered |
| **Knowledge Base** | Static reference | PostgreSQL | Seeded, admin-updated |

### 4.2 Full Database Schema

#### Users & Authentication

```sql
-- Core user account
CREATE TABLE users (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email           VARCHAR(255) UNIQUE NOT NULL,
  email_verified  BOOLEAN DEFAULT FALSE,
  password_hash   VARCHAR(255),               -- NULL for OAuth-only users
  full_name       VARCHAR(255) NOT NULL,
  date_of_birth   DATE,
  gender          VARCHAR(50),                -- 'male','female','non-binary','prefer_not_to_say'
  timezone        VARCHAR(100) DEFAULT 'UTC',
  locale          VARCHAR(10)  DEFAULT 'en',
  avatar_url      TEXT,
  subscription_tier VARCHAR(20) DEFAULT 'free', -- free, personal, premium, practitioner, enterprise
  subscription_status VARCHAR(20) DEFAULT 'active',
  stripe_customer_id  VARCHAR(100),
  created_at      TIMESTAMPTZ DEFAULT NOW(),
  updated_at      TIMESTAMPTZ DEFAULT NOW(),
  last_active_at  TIMESTAMPTZ,
  deleted_at      TIMESTAMPTZ                 -- soft delete
);

-- OAuth provider links
CREATE TABLE user_oauth_providers (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id       UUID REFERENCES users(id) ON DELETE CASCADE,
  provider      VARCHAR(50) NOT NULL,         -- 'google', 'apple'
  provider_uid  VARCHAR(255) NOT NULL,
  email         VARCHAR(255),
  created_at    TIMESTAMPTZ DEFAULT NOW(),
  UNIQUE(provider, provider_uid)
);

-- Refresh tokens
CREATE TABLE refresh_tokens (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id     UUID REFERENCES users(id) ON DELETE CASCADE,
  token_hash  VARCHAR(255) UNIQUE NOT NULL,
  device_info JSONB,                          -- device name, OS version
  expires_at  TIMESTAMPTZ NOT NULL,
  revoked_at  TIMESTAMPTZ,
  created_at  TIMESTAMPTZ DEFAULT NOW()
);
```

#### Constitution & Current State

```sql
-- Prakriti (static birth constitution — set at onboarding)
CREATE TABLE user_constitution (
  id                  UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id             UUID UNIQUE REFERENCES users(id) ON DELETE CASCADE,
  vata_percentage     SMALLINT NOT NULL CHECK (vata_percentage BETWEEN 0 AND 100),
  pitta_percentage    SMALLINT NOT NULL CHECK (pitta_percentage BETWEEN 0 AND 100),
  kapha_percentage    SMALLINT NOT NULL CHECK (kapha_percentage BETWEEN 0 AND 100),
  dominant_type       VARCHAR(50),             -- 'vata', 'pitta-vata', 'tridoshic', etc.
  assessment_responses JSONB NOT NULL,         -- raw 60-question responses
  scoring_breakdown   JSONB,                   -- per-section scores
  assessed_at         TIMESTAMPTZ DEFAULT NOW(),
  reassessed_at       TIMESTAMPTZ              -- if user retakes
);

-- Vikriti (dynamic current state — updated continuously)
CREATE TABLE user_current_state (
  id                  UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id             UUID UNIQUE REFERENCES users(id) ON DELETE CASCADE,
  -- Current dosha imbalance deltas from Prakriti baseline
  vata_imbalance      SMALLINT DEFAULT 0,      -- -10 to +10, positive = excess
  pitta_imbalance     SMALLINT DEFAULT 0,
  kapha_imbalance     SMALLINT DEFAULT 0,
  -- Ayurvedic state indicators
  agni_state          VARCHAR(20) DEFAULT 'sama', -- sama, vishama, tikshna, manda
  ama_level           VARCHAR(20) DEFAULT 'none',  -- none, low, moderate, high
  ojas_level          SMALLINT   DEFAULT 7,         -- 1-10
  -- Active symptoms (array of symptom codes)
  active_symptoms     TEXT[],
  -- Source of last update
  last_updated_by     VARCHAR(50),             -- 'checkin', 'wearable', 'scan', 'lab', 'manual'
  updated_at          TIMESTAMPTZ DEFAULT NOW()
);

-- User health profile (conditions, medications, dietary preferences)
CREATE TABLE user_health_profile (
  id                    UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id               UUID UNIQUE REFERENCES users(id) ON DELETE CASCADE,
  -- Encrypted sensitive fields
  medical_conditions    TEXT,                  -- AES-256 encrypted JSONB string
  current_medications   TEXT,                  -- AES-256 encrypted JSONB string
  allergies             TEXT[],
  family_history        TEXT,                  -- AES-256 encrypted
  -- Dietary & lifestyle
  dietary_restrictions  TEXT[],                -- 'vegan', 'gluten-free', etc.
  dietary_preferences   TEXT[],
  exercise_preferences  TEXT[],
  health_goals          TEXT[],
  pregnancy_status      VARCHAR(20),           -- 'not_pregnant', 'pregnant', 'nursing'
  -- Lifestyle context
  wake_time             TIME,
  sleep_time            TIME,
  stress_level_baseline SMALLINT,             -- 1-10
  updated_at            TIMESTAMPTZ DEFAULT NOW()
);

-- Digital Twin personality preferences
CREATE TABLE user_twin_preferences (
  id                    UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id               UUID UNIQUE REFERENCES users(id) ON DELETE CASCADE,
  twin_name             VARCHAR(100) DEFAULT 'Ayur',
  communication_style   VARCHAR(30) DEFAULT 'supportive_friend', -- supportive_friend, wise_teacher, clinical_guide
  verbosity_level       VARCHAR(20) DEFAULT 'balanced',          -- concise, balanced, detailed
  sanskrit_usage        VARCHAR(20) DEFAULT 'moderate',          -- none, moderate, frequent
  voice_enabled         BOOLEAN DEFAULT FALSE,
  voice_id              VARCHAR(100),
  morning_summary_time  TIME DEFAULT '07:00',
  morning_summary_enabled BOOLEAN DEFAULT TRUE,
  notification_preferences JSONB DEFAULT '{}',
  data_access_permissions  JSONB DEFAULT '{"wearables":true,"checkins":true,"scans":true,"labs":false,"genetics":false}',
  updated_at            TIMESTAMPTZ DEFAULT NOW()
);
```

#### Health Data Streams

```sql
-- Daily check-ins (TimescaleDB hypertable)
CREATE TABLE daily_checkins (
  id              UUID          DEFAULT gen_random_uuid(),
  user_id         UUID          NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  checked_in_at   TIMESTAMPTZ   NOT NULL DEFAULT NOW(),
  energy_level    SMALLINT      CHECK (energy_level BETWEEN 1 AND 10),
  sleep_quality   SMALLINT      CHECK (sleep_quality BETWEEN 1 AND 10),
  digestion_state VARCHAR(20),  -- good, variable, sluggish, burning
  mood            VARCHAR(20),  -- calm, anxious, irritable, heavy, mixed
  symptoms        TEXT[],
  notes           TEXT,
  PRIMARY KEY (id, checked_in_at)
);
SELECT create_hypertable('daily_checkins', 'checked_in_at');

-- Wearable data points (TimescaleDB hypertable)
CREATE TABLE wearable_data_points (
  id              UUID          DEFAULT gen_random_uuid(),
  user_id         UUID          NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  device_type     VARCHAR(50)   NOT NULL, -- apple_health, oura, whoop, fitbit, garmin
  data_type       VARCHAR(50)   NOT NULL, -- sleep, activity, heart_rate, hrv, temperature
  recorded_at     TIMESTAMPTZ   NOT NULL,
  raw_values      JSONB         NOT NULL, -- device-specific metric object
  -- Pre-computed Ayurvedic interpretation
  dosha_signal    VARCHAR(20),            -- vata, pitta, kapha, balanced
  interpretation  TEXT,
  synced_at       TIMESTAMPTZ   DEFAULT NOW(),
  PRIMARY KEY (id, recorded_at)
);
SELECT create_hypertable('wearable_data_points', 'recorded_at');

-- Connected wearable devices
CREATE TABLE user_wearable_devices (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID REFERENCES users(id) ON DELETE CASCADE,
  device_type     VARCHAR(50) NOT NULL,
  access_token    TEXT,                   -- encrypted OAuth token
  refresh_token   TEXT,                   -- encrypted
  token_expires_at TIMESTAMPTZ,
  last_synced_at  TIMESTAMPTZ,
  sync_status     VARCHAR(20) DEFAULT 'active', -- active, paused, error
  created_at      TIMESTAMPTZ DEFAULT NOW()
);

-- Lab results
CREATE TABLE lab_results (
  id                    UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id               UUID REFERENCES users(id) ON DELETE CASCADE,
  test_date             DATE NOT NULL,
  lab_name              VARCHAR(255),
  file_url              TEXT,                   -- S3 URL (encrypted)
  -- Extracted and interpreted data
  biomarkers            JSONB,                  -- array of {name, value, unit, ref_min, ref_max, status, ayurvedic_interpretation, dhatu_affected}
  overall_pattern       TEXT,
  root_cause_analysis   TEXT,
  action_plan           TEXT[],
  medical_flags         TEXT[],                 -- critical values flagged
  -- AI processing metadata
  ocr_status            VARCHAR(20) DEFAULT 'pending', -- pending, processing, complete, failed
  processed_at          TIMESTAMPTZ,
  uploaded_at           TIMESTAMPTZ DEFAULT NOW()
);

-- Visual diagnostic scans (tongue, meal, skin, product)
CREATE TABLE scan_analyses (
  id                UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id           UUID REFERENCES users(id) ON DELETE CASCADE,
  scan_type         VARCHAR(30) NOT NULL,       -- tongue, meal, skin, product
  image_url         TEXT NOT NULL,              -- S3 URL (encrypted)
  -- Analysis results (structure varies by scan_type, stored as JSONB)
  analysis          JSONB NOT NULL,
  -- Common derived fields
  dosha_indicators  TEXT[],
  ama_signal        VARCHAR(20),                -- for tongue scans
  agni_signal       VARCHAR(20),                -- for tongue/meal scans
  recommendations   TEXT[],
  scanned_at        TIMESTAMPTZ DEFAULT NOW()
);

-- Manual health logs (meals, symptoms, mood, meditation, etc.)
CREATE TABLE manual_logs (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id     UUID REFERENCES users(id) ON DELETE CASCADE,
  log_type    VARCHAR(30) NOT NULL,             -- meal, symptom, mood, meditation, menstrual, supplement
  data        JSONB NOT NULL,                   -- flexible structure per log_type
  notes       TEXT,
  logged_at   TIMESTAMPTZ DEFAULT NOW()
);

-- Genetic profiles (V2 feature — schema defined now for migration planning)
CREATE TABLE genetic_profiles (
  id                        UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id                   UUID UNIQUE REFERENCES users(id) ON DELETE CASCADE,
  source                    VARCHAR(50),        -- 23andme, ancestry, other
  file_url                  TEXT,               -- S3 URL (encrypted at rest)
  variants                  TEXT,               -- AES-256 encrypted JSONB
  constitutional_validation TEXT,
  risk_themes               TEXT[],
  protective_factors        TEXT[],
  processed_at              TIMESTAMPTZ,
  uploaded_at               TIMESTAMPTZ DEFAULT NOW()
);
```

#### Protocols

```sql
-- Wellness protocols (AI-generated)
CREATE TABLE protocols (
  id                  UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id             UUID REFERENCES users(id) ON DELETE CASCADE,
  name                VARCHAR(255) NOT NULL,
  description         TEXT,
  -- Targeting
  primary_imbalance   VARCHAR(100),
  secondary_imbalances TEXT[],
  target_doshas       TEXT[],
  -- Structure
  duration_days       INTEGER NOT NULL,
  phases              JSONB NOT NULL,           -- array of Phase objects
  recommendations     JSONB NOT NULL,           -- array of Recommendation objects
  success_metrics     JSONB,
  checkin_schedule    JSONB,
  adjustment_triggers TEXT[],
  -- State
  status              VARCHAR(20) DEFAULT 'draft', -- draft, active, paused, completed, archived
  current_phase_index SMALLINT DEFAULT 0,
  activated_at        TIMESTAMPTZ,
  completed_at        TIMESTAMPTZ,
  -- Tracking
  adherence_percentage SMALLINT DEFAULT 0,
  -- Metadata
  version             SMALLINT DEFAULT 1,
  source              VARCHAR(30) DEFAULT 'ai_generated', -- ai_generated, library, practitioner
  created_at          TIMESTAMPTZ DEFAULT NOW(),
  updated_at          TIMESTAMPTZ DEFAULT NOW()
);

-- Protocol version history (immutable audit trail)
CREATE TABLE protocol_versions (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  protocol_id   UUID REFERENCES protocols(id) ON DELETE CASCADE,
  version       SMALLINT NOT NULL,
  snapshot      JSONB NOT NULL,                 -- full protocol state at this version
  change_reason TEXT,
  changed_by    VARCHAR(30),                    -- user, ai, practitioner
  created_at    TIMESTAMPTZ DEFAULT NOW()
);

-- Daily protocol tracking
CREATE TABLE protocol_tracking (
  id                UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  protocol_id       UUID REFERENCES protocols(id) ON DELETE CASCADE,
  user_id           UUID REFERENCES users(id) ON DELETE CASCADE,
  tracked_date      DATE NOT NULL,
  completed_items   TEXT[],                     -- recommendation IDs completed
  skipped_items     TEXT[],
  notes             TEXT,
  symptom_changes   TEXT[],
  energy_rating     SMALLINT,
  overall_feeling   VARCHAR(20),
  UNIQUE(protocol_id, tracked_date)
);
```

#### Conversations & Messages

```sql
-- Conversation sessions
CREATE TABLE conversations (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID REFERENCES users(id) ON DELETE CASCADE,
  title           VARCHAR(255),                 -- auto-generated from first message
  conversation_type VARCHAR(30) DEFAULT 'chat', -- chat, morning_summary, onboarding, checkin
  -- Context snapshot at conversation start (for AI reconstruction)
  context_snapshot JSONB,
  is_favorited    BOOLEAN DEFAULT FALSE,
  created_at      TIMESTAMPTZ DEFAULT NOW(),
  last_message_at TIMESTAMPTZ DEFAULT NOW()
);

-- Individual messages
CREATE TABLE messages (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  conversation_id UUID REFERENCES conversations(id) ON DELETE CASCADE,
  user_id         UUID REFERENCES users(id) ON DELETE CASCADE,
  sender          VARCHAR(10) NOT NULL,          -- 'user', 'twin'
  message_type    VARCHAR(30) DEFAULT 'text',    -- text, summary_card, protocol_card, visualization, quick_action
  content         TEXT NOT NULL,
  structured_data JSONB,                         -- for non-text message types
  attachments     JSONB,                         -- [{type, url, analysis_id}]
  -- AI metadata
  model_used      VARCHAR(50),
  tokens_used     INTEGER,
  tools_called    TEXT[],
  created_at      TIMESTAMPTZ DEFAULT NOW()
);

CREATE INDEX idx_messages_conversation ON messages(conversation_id, created_at DESC);
CREATE INDEX idx_conversations_user ON conversations(user_id, last_message_at DESC);
```

#### Notifications & Alerts

```sql
-- Prediction alerts and morning summaries
CREATE TABLE notifications (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID REFERENCES users(id) ON DELETE CASCADE,
  notification_type VARCHAR(30) NOT NULL,        -- prediction_alert, morning_summary, protocol_reminder, system
  title           VARCHAR(255) NOT NULL,
  body            TEXT NOT NULL,
  data            JSONB,                         -- deep-link data, alert details
  status          VARCHAR(20) DEFAULT 'pending', -- pending, sent, read, dismissed
  apns_message_id VARCHAR(255),
  scheduled_for   TIMESTAMPTZ,
  sent_at         TIMESTAMPTZ,
  read_at         TIMESTAMPTZ,
  created_at      TIMESTAMPTZ DEFAULT NOW()
);
```

#### Ayurvedic Knowledge Base

```sql
-- Herb knowledge cache (AI-generated responses, not pre-seeded)
-- Populated incrementally as users query herbs; source of truth is Claude's training knowledge.
-- Do NOT treat as a complete or authoritative database at MVP.
-- Phase 2: replace with practitioner-validated dataset.
CREATE TABLE herbs (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name_common     VARCHAR(255) NOT NULL UNIQUE,
  name_sanskrit   VARCHAR(255),
  name_latin      VARCHAR(255),
  rasa            TEXT[],                        -- tastes
  virya           VARCHAR(20),                   -- heating, cooling
  vipaka          VARCHAR(20),                   -- post-digestive effect
  prabhav         TEXT,                          -- specific action
  dosha_effect    JSONB,                         -- {vata, pitta, kapha}: -1/0/+1
  primary_actions TEXT[],
  indications     TEXT[],
  contraindications TEXT[],
  drug_interactions TEXT[],
  pregnancy_safety VARCHAR(20),                  -- safe, caution, avoid
  standard_dosage TEXT,
  preparation_methods TEXT[],
  ai_generated    BOOLEAN DEFAULT TRUE,          -- flag: true until practitioner-reviewed
  last_updated    TIMESTAMPTZ DEFAULT NOW()
);

-- Food knowledge cache (AI-generated responses, not pre-seeded)
-- Same pattern as herbs: populated on demand, not a pre-built reference DB.
CREATE TABLE foods (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name            VARCHAR(255) NOT NULL UNIQUE,
  category        VARCHAR(100),
  six_tastes      JSONB,                         -- taste percentages
  dosha_effect    JSONB,                         -- {vata, pitta, kapha} effect scores
  agni_effect     VARCHAR(20),                   -- strengthens, weakens, neutral
  ama_potential   VARCHAR(20),                   -- low, moderate, high
  best_season     TEXT[],
  combining_rules JSONB,                         -- incompatible combinations
  qualities       TEXT[],                        -- heavy, light, dry, oily, etc.
  ai_generated    BOOLEAN DEFAULT TRUE,
  last_updated    TIMESTAMPTZ DEFAULT NOW()
);
```

#### Subscription & Usage Tracking

```sql
CREATE TABLE subscriptions (
  id                    UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id               UUID REFERENCES users(id) ON DELETE CASCADE,
  stripe_subscription_id VARCHAR(100) UNIQUE,
  plan                  VARCHAR(30) NOT NULL,
  status                VARCHAR(30) NOT NULL,     -- active, past_due, canceled, trialing
  current_period_start  TIMESTAMPTZ,
  current_period_end    TIMESTAMPTZ,
  cancel_at_period_end  BOOLEAN DEFAULT FALSE,
  created_at            TIMESTAMPTZ DEFAULT NOW(),
  updated_at            TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE usage_counters (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id       UUID REFERENCES users(id) ON DELETE CASCADE,
  period_start  DATE NOT NULL,                   -- start of billing month
  ai_messages   INTEGER DEFAULT 0,
  image_scans   INTEGER DEFAULT 0,
  lab_uploads   INTEGER DEFAULT 0,
  UNIQUE(user_id, period_start)
);
```

### 4.3 Key Database Indexes

```sql
-- Performance indexes
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_subscription ON users(subscription_tier, subscription_status);
CREATE INDEX idx_wearable_user_type_time ON wearable_data_points(user_id, data_type, recorded_at DESC);
CREATE INDEX idx_checkins_user_time ON daily_checkins(user_id, checked_in_at DESC);
CREATE INDEX idx_protocols_user_status ON protocols(user_id, status);
CREATE INDEX idx_scan_user_type ON scan_analyses(user_id, scan_type, scanned_at DESC);
CREATE INDEX idx_messages_search ON messages USING gin(to_tsvector('english', content));
CREATE INDEX idx_conversations_user_type ON conversations(user_id, conversation_type, last_message_at DESC);
```

---

## 5. Feature Priority Tiers & MVP Scope

### 5.1 Tier 1 — Non-Negotiable MVP (v1.0)

The app cannot function without these. Required for launch.

| # | Feature | Reason It's Non-Negotiable |
|---|---|---|
| 1 | **Onboarding + Prakriti Assessment** | Without constitution, no personalization is possible |
| 2 | **Digital Twin Chat** | The core product surface; primary user interaction |
| 3 | **Daily Check-In** | Primary mechanism for updating Vikriti |
| 4 | **Protocol Engine** (1 active protocol) | Core health guidance deliverable |
| 5 | **Insights Dashboard** (Health tab) | Shows users their dosha state and trends |
| 6 | **Authentication** (email + Apple Sign-In) | Required for iOS App Store; user identity foundation |
| 7 | **Profile + Subscription** | Plan gating; user data management |

### 5.2 Tier 2 — High-Value Features (v1.5)

Strong retention drivers. Prioritize immediately after v1.0 is stable.

| # | Feature | Value |
|---|---|---|
| 8 | **Apple HealthKit Integration** | Enriches Vikriti automatically; reduces manual effort |
| 9 | **Morning Summary** | Daily re-engagement hook; key retention feature |
| 10 | **Tongue + Meal Scans** | Differentiating AI feature; visual engagement |
| 11 | **Today Section** | Daily protocol action checklist; adherence driver |
| 12 | **History Tab** | Conversation archive; builds trust over time |
| 13 | **Prediction Alerts** | Proactive health guidance; delight feature |

### 5.3 Tier 3 — Growth Features (v2.0+)

Enable premium monetization and practitioner ecosystem.

| # | Feature | Tier Gate |
|---|---|---|
| 14 | Lab Results Upload | Premium |
| 15 | Nutrition Tab (detailed logging) | Personal+ |
| 16 | Supplements Tab | Personal+ |
| 17 | Lifestyle Tab (full Dinacharya) | Personal+ |
| 18 | Projects (multi-protocol goals) | Premium |
| 19 | Learn (gamified education) | Free (limited) |
| 20 | Shop (product marketplace) | All tiers |
| 21 | Practitioner Plan features | Practitioner |
| 22 | Genetic Data Analysis | Premium |
| 23 | Exposure Tab | Premium |
| 24 | Google Fit / Oura / WHOOP integration | Personal+ |

### 5.4 MVP Subscription Gates

| Feature | Free | Personal | Premium |
|---|---|---|---|
| AI messages/month | 20 | Unlimited | Unlimited |
| Active protocols | 1 | 1 | 3 |
| Image scans/month | 0 | 10 | Unlimited |
| Apple HealthKit | ✗ | ✓ | ✓ |
| Morning summary | ✗ | ✓ | ✓ |
| Lab uploads/month | 0 | 0 | 3 |
| Conversation history | 30 days | 1 year | Full |

---

## 6. User Flows & Backend Flows

> Each flow is described as: **User action → Frontend event → API call → Backend processing → Response**

### 6.1 Onboarding Flow

**User experience:** Welcome → Goals → 60-question assessment → Constitution results → Twin personalization → HealthKit connect (optional) → Deep-dive chat → First protocol → Enter app

```
STEP 1: App launch, user taps "Get Started"
  → Frontend: navigate to /onboarding/welcome
  → No API call

STEP 2: User selects health goal(s)
  → Frontend: store selections locally

STEP 3: User completes 60-question Prakriti assessment
  → Displayed as 5 sections, ~12 questions each
  → Answers stored locally until submission

STEP 4: User submits assessment
  API: POST /api/auth/register
    Body: { email, password, fullName }
    Response: { userId, accessToken }

  API: POST /api/assessment/prakriti
    Body: { responses: [...60 answers], health_goals: [...] }
    Backend:
      1. Run Prakriti scoring algorithm (weighted multi-category scoring)
         - Physical section weight: 35%
         - Mental/emotional section weight: 30%
         - Digestive/lifestyle section weight: 35%
      2. Calculate vata/pitta/kapha percentages (must sum to 100)
      3. Determine dominant type (single, dual, tridoshic)
      4. INSERT into user_constitution
      5. INSERT into user_current_state (defaults: imbalance=0, agni=sama, ama=none, ojas=7)
      6. INSERT into user_health_profile (with health goals)
    Response: { prakriti, percentages, dominantType, description, characteristics }

STEP 5: User personalizes Digital Twin
  API: POST /api/twin/preferences
    Body: { twinName, communicationStyle, verbosityLevel, sanskritUsage }
    Backend: INSERT/UPDATE user_twin_preferences
    Response: { success }

STEP 6: HealthKit authorization (optional, iOS only)
  → Frontend: request HealthKit permissions via native API
  → If granted:
    API: POST /api/wearables/connect
      Body: { deviceType: 'apple_health', permissionsGranted: [...] }
      Backend:
        1. INSERT into user_wearable_devices
        2. Enqueue wearable_initial_sync job (BullMQ)
        3. Job runs: read last 30 days of HealthKit data, INSERT into wearable_data_points
      Response: { connected, syncStatus: 'pending' }

STEP 7: Deep-dive onboarding chat
  → Regular chat flow (see 6.3), conversation_type = 'onboarding'
  → Twin asks about current symptoms, lifestyle, specific concerns
  → Twin updates user_health_profile based on conversation

STEP 8: First protocol generation
  API: POST /api/protocols/generate
    Body: { primaryConcern, duration: 21, fromOnboarding: true }
    Backend:
      1. Assemble full user context (Prakriti + Vikriti + health goals + preferences)
      2. Call Claude API with protocol generation prompt + context
      3. Parse structured protocol response
      4. INSERT into protocols (status: 'draft')
    Response: { protocol } (draft, not yet active)

  → User reviews protocol, taps Accept
  API: POST /api/protocols/:id/activate
    Backend:
      1. UPDATE protocols SET status='active', activated_at=NOW()
      2. Schedule daily protocol reminder notifications
    Response: { success }

STEP 9: Onboarding complete → redirect to Today tab
```

**Prakriti Scoring Algorithm:**

```
For each question response (0–3 scale: 0=not like me, 3=very much like me):
  - Vata responses accumulate vata_score
  - Pitta responses accumulate pitta_score
  - Kapha responses accumulate kapha_score

Section weights applied:
  physical_build     → 0.35 weight
  physiological      → 0.30 weight
  mental_emotional   → 0.25 weight
  lifestyle_prefs    → 0.10 weight

Final percentages:
  total = vata_weighted + pitta_weighted + kapha_weighted
  vata_pct   = round((vata_weighted / total) * 100)
  pitta_pct  = round((pitta_weighted / total) * 100)
  kapha_pct  = 100 - vata_pct - pitta_pct  (ensures sum = 100)

Dominant type classification:
  if max_dosha > 60%         → single-dominant (e.g., 'vata')
  if max_dosha 40–60%        → dual-dominant (e.g., 'vata-pitta')
  if all three 28–38%        → tridoshic
```

---

### 6.2 Daily Check-In Flow

**User experience:** Tap check-in → 5 quick questions → AI insight returned

```
USER: Taps "Check In" button (Today section or chat quick action)

FRONTEND:
  → Display 5-question modal:
    1. Energy level (1–10 slider)
    2. Sleep quality (1–10 slider)
    3. Digestion state (4-option selector: Good/Variable/Sluggish/Burning)
    4. Mood (5-option selector: Calm/Anxious/Irritable/Heavy/Mixed)
    5. Active symptoms (multi-select from symptom list + free text)

USER: Submits answers

API: POST /api/health/checkin
  Body: { energyLevel, sleepQuality, digestionState, mood, symptoms, notes }
  Backend:
    1. INSERT into daily_checkins (TimescaleDB)
    2. Vikriti update logic:
       - Map digestion_state → agni_state update
         (good→sama, variable→vishama, burning→tikshna, sluggish→manda)
       - Analyze symptom patterns vs. Prakriti baseline
       - Calculate delta dosha imbalances from symptoms
       - UPDATE user_current_state (vikriti fields, last_updated_by='checkin')
    3. Async: enqueue ai_checkin_analysis job
       - Job: call Claude with checkin data + last 7 days context
       - Generate 2-3 sentence pattern insight + 1 actionable tip
       - INSERT response as message in daily checkin conversation
    4. Check for alert triggers:
       - 3+ consecutive days of concerning patterns → generate prediction_alert
  Response: { checkinId, insight (immediate lightweight), tip }

FRONTEND:
  → Show insight card with tip
  → Update Today section dosha status indicators
```

---

### 6.3 Chat / One-Off Query Flow

**User experience:** User types message → streaming response appears → saved to history

```
USER: Sends message in chat interface

FRONTEND:
  → WebSocket: emit 'chat:message'
    Payload: { conversationId (or null for new), content, attachments? }

BACKEND (WebSocket handler):
  1. Auth & rate limit check:
     - Verify JWT
     - Check usage_counters.ai_messages against plan limit
     - If at limit → emit 'chat:error' { code: 'USAGE_LIMIT', upgradeUrl }

  2. Context assembly (ContextAssemblyService):
     a. Fetch user_constitution (Prakriti)
     b. Fetch user_current_state (Vikriti)
     c. Fetch active protocols (summary: name, phase, today's recommendations)
     d. Fetch last 7 daily_checkins
     e. Fetch last 20 messages from this conversation (or empty if new)
     f. Fetch user_twin_preferences (communication style, name)
     g. Fetch user_health_profile (conditions, medications, goals)
     h. Add current date, season, time of day
     i. Calculate total token estimate; if >90k tokens, trim oldest messages

  3. Build Claude API request:
     - System prompt: base Master Prompt + dynamic context block (see Section 8)
     - Messages: conversation history + new user message
     - Tools: 10 tool definitions (see Section 8)
     - Stream: true

  4. Call Claude API (streaming)

  5. For each chunk received:
     → emit 'chat:chunk' to client WebSocket

  6. When stream complete:
     a. INSERT conversation (if new)
     b. INSERT user message into messages
     c. INSERT twin response into messages (with model_used, tokens_used, tools_called)
     d. UPDATE conversations.last_message_at
     e. INCREMENT usage_counters.ai_messages

  7. emit 'chat:complete' with message metadata

FRONTEND:
  → Stream chunks render in real-time as text appears
  → On complete: persist message locally, update history
```

**Protocol Modification via Chat:**

If Claude's response includes a tool call to `modify_protocol` or `create_protocol`:
```
1. Tool call intercepted by backend
2. Call relevant NestJS service method
3. Service returns updated data to Claude as tool result
4. Claude generates response confirming the change
5. Frontend shows protocol card in chat with "View Protocol" CTA
```

---

### 6.4 New Data Ingestion Flows

#### 6.4.1 Wearable Sync (Apple HealthKit)

```
BACKGROUND WORKER (runs every hour via BullMQ):
  Job: wearable_sync
  Input: { userId, deviceType: 'apple_health', lastSyncAt }

  1. iOS app (when active) OR background fetch:
     - HealthKit query: sleep, HRV, heart rate, steps, active energy
     - Since: lastSyncAt
     - Batch: up to 1000 data points

  2. API: POST /api/wearables/sync
     Body: { deviceType, dataPoints: [...] }
     Backend:
       a. Validate and normalize data points
       b. BATCH INSERT into wearable_data_points (TimescaleDB)
       c. For each significant event, compute Ayurvedic interpretation:
          - Sleep: fragmented (>3 awakenings) → vata_signal
          - Sleep: waking 10pm–2am → pitta_signal
          - HRV low (<30ms) + low energy → vata depletion → ojas concern
          - HRV high + good sleep → ojas strength
       d. Vikriti update logic:
          - Average last 3 nights sleep + HRV trends
          - UPDATE user_current_state if signals are consistent
       e. Alert trigger check:
          - HRV declining >20% over 3 days → potential imbalance alert
       f. UPDATE user_wearable_devices.last_synced_at
```

#### 6.4.2 Lab Results Upload

```
USER: Uploads lab PDF in Health section

FRONTEND:
  → Request presigned S3 URL
  API: POST /api/health/lab/presigned-url
    Response: { uploadUrl, fileKey }
  → Upload PDF directly to S3 via presigned URL
  → Confirm upload complete

API: POST /api/health/lab/confirm
  Body: { fileKey, testDate, labName }
  Backend:
    1. INSERT into lab_results (status: 'pending', file_url set)
    2. Enqueue lab_ocr_processing job (BullMQ)

BACKGROUND WORKER: lab_ocr_processing
  1. Download PDF from S3
  2. Call Claude API with vision: extract all biomarker names, values, units, reference ranges
  3. For each biomarker extracted:
     - Look up in knowledge base → map to dhatu (tissue layer) + dosha
     - Flag if outside reference range (medical_flag if critically abnormal)
  4. Generate synthesis:
     - Overall pattern analysis (cross-biomarker)
     - Root cause analysis (Ayurvedic lens)
     - Action plan recommendations
     - Protocol suggestions
  5. UPDATE lab_results with extracted data + interpretations
  6. Send push notification: "Your lab results are ready"
  7. Trigger Vikriti reassessment based on lab findings
```

#### 6.4.3 Image Scan Flow (Tongue / Meal / Skin)

```
USER: Taps scan button, takes/selects photo

FRONTEND:
  → Get presigned S3 upload URL
  API: POST /api/health/scan/presigned-url
    Body: { scanType: 'tongue' }
    Response: { uploadUrl, fileKey }
  → Upload image to S3
  → Confirm upload, show loading state

API: POST /api/health/scan/analyze
  Body: { fileKey, scanType }
  Backend:
    1. INSERT scan_analyses (status: pending)
    2. Increment usage_counters.image_scans; check plan limit
    3. Build scan-specific prompt for Claude Vision
    4. Call Claude API (claude-sonnet vision):
       - Tongue: assess coating (color, thickness, location), tongue color, texture, shape, teeth marks
       - Meal: identify ingredients, estimate six-taste breakdown, assess dosha impact
       - Skin: assess type, identify issues, correlate to dosha
    5. Parse structured response into scan_analyses.analysis (JSONB)
    6. Extract dosha_indicators, ama_signal, agni_signal
    7. Generate personalized recommendations based on Prakriti + scan findings
    8. UPDATE scan_analyses with full analysis
    9. Update Vikriti if scan indicates significant change (e.g., heavy ama coating)
  Response: { analysis, recommendations, comparison_to_last? }
```

---

### 6.5 Protocol Creation Flow

```
TRIGGER: User requests protocol in chat, taps "New Protocol", or onboarding completion

API: POST /api/protocols/generate
  Body: { primaryConcern, duration?, intensity?, constraints? }
  Backend:
    1. Assemble protocol generation context:
       - Prakriti + Vikriti (full)
       - Active symptoms
       - Existing active protocols (to avoid conflicts)
       - Lifestyle constraints from user_health_profile
       - Current season
       - Past protocol outcomes (if any)

    2. Call Claude API with protocol_generation system prompt:
       - Must generate: name, description, 3 phases, 5 recommendation categories
       - Each recommendation: action, frequency, timing, rationale, tips, contraindications
       - Define success metrics and check-in schedule

    3. Herb safety check (for all herbs in recommendations):
       - Query herbs table for contraindications
       - Cross-check against user_health_profile.current_medications
       - Cross-check against user_health_profile.medical_conditions
       - Remove or flag unsafe recommendations

    4. INSERT into protocols (status: 'draft')
    5. INSERT into protocol_versions (version 1 snapshot)

  Response: { protocol } (returned to chat as protocol_card message type)

→ User reviews in chat or Protocol detail screen
→ User taps "Start Protocol"

API: POST /api/protocols/:id/activate
  Backend:
    1. UPDATE protocols SET status='active', activated_at=NOW()
    2. Deactivate any conflicting active protocols (if on Free/Personal plan: max 1)
    3. Schedule daily protocol_reminder notifications via APNs
  Response: { success, activeProtocol }
```

---

### 6.6 Protocol Modification Flow

**Triggers:** AI recommendation in chat, poor adherence detected, new lab/wearable data, user request, seasonal change

```
TRIGGER TYPE 1: Via chat conversation
  → User says "This diet recommendation is too hard for me"
  → Claude calls modify_protocol tool
  → Tool handler:
    API: PUT /api/protocols/:id/modify
      Body: { modifications: [{recommendationId, change, reason}] }
      Backend:
        1. Snapshot current protocol → INSERT protocol_versions
        2. Apply modifications to protocols.recommendations (JSONB update)
        3. Increment protocols.version
      Response: { updatedProtocol }
  → Claude confirms change in chat

TRIGGER TYPE 2: Poor adherence detected (background worker)
  Background job runs nightly:
  - Query protocol_tracking for last 7 days adherence per active protocol
  - If adherence_percentage < 40% for 5+ days:
    → Enqueue protocol_review job
    → Job: call Claude with context → generate adjustment suggestions
    → INSERT notification (type: 'protocol_review_suggestion')
    → User opens app → sees suggestion card → can accept/decline

TRIGGER TYPE 3: New significant health data
  - After lab result processing or significant wearable trend detected
  - ProtocolService.reviewActiveProtocols(userId, trigger: 'new_data')
  - Assess if current protocol recommendations are still appropriate
  - If significant mismatch → generate modification suggestion
```

---

### 6.7 Morning Summary Flow

```
BACKGROUND WORKER: morning_summary_generator
  Schedule: Daily at user's morning_summary_time (default 7:00 AM user timezone)

  1. Fetch overnight data:
     - wearable_data_points from last 8 hours (sleep session)
     - Latest user_current_state (Vikriti)
     - Active protocol today's recommendations
     - Any active prediction_alerts

  2. Compute overnight Ayurvedic interpretation:
     - Sleep quality assessment (duration, efficiency, stages)
     - HRV trend (recovering/declining)
     - Map to dosha forecast

  3. Call Claude API with morning_summary prompt:
     - Personalized greeting (uses twin name)
     - Sleep interpretation in Ayurvedic terms
     - Dosha forecast for today
     - Top 3 recommended actions (from active protocol + current state)
     - Encouraging closing note

  4. INSERT as conversation (type: 'morning_summary') + message

  5. Send push notification via APNs:
     { title: "Good morning! Your daily summary is ready", body: [first line of summary] }

  6. User taps notification → opens Today section → sees Morning Summary Card
```

---

### 6.8 Prediction Alert Flow

```
BACKGROUND WORKER: prediction_scanner
  Schedule: Every 6 hours

  1. For each user with Personal+ plan and active wearable/checkin data:
     a. Fetch last 7 days of daily_checkins + wearable_data_points
     b. Calculate trend vectors (improving/declining/stable) for:
        - Energy, sleep quality, digestion, mood (from check-ins)
        - HRV, sleep efficiency, resting HR (from wearables)
     c. Compare to user's baseline (last 30-day averages)
     d. If any metric declining >2 standard deviations over 3+ days:
        → Flag as potential imbalance

  2. For flagged users:
     Call Claude API with prediction_alert prompt:
     - Identify specific imbalance pattern
     - Map to Ayurvedic interpretation (e.g., "Vata aggravation building")
     - Generate 3–5 specific preventive recommendations
     - Estimate timeline ("may manifest as symptoms in 3–5 days if unaddressed")

  3. INSERT into notifications (type: 'prediction_alert')
  4. Send push notification
  5. Alert also surfaces in chat as proactive twin message on next app open
```

---

## 7. API Contracts

> All endpoints are prefixed with `/api/v1`. All requests require `Authorization: Bearer <access_token>` except auth endpoints. All responses follow the envelope: `{ success: boolean, data: any, error?: { code, message } }`.

### 7.1 Authentication

```
POST   /auth/register
Body:  { email, password, fullName }
Resp:  { userId, message: "Verification email sent" }

POST   /auth/verify-email
Body:  { token }
Resp:  { success }

POST   /auth/login
Body:  { email, password, rememberMe? }
Resp:  { accessToken, refreshToken, user: { id, email, fullName, subscriptionTier, onboardingComplete } }

POST   /auth/refresh
Body:  { refreshToken }
Resp:  { accessToken, refreshToken }

POST   /auth/logout
Body:  { refreshToken }
Resp:  { success }

POST   /auth/oauth/apple
Body:  { identityToken, authorizationCode, fullName? }
Resp:  { accessToken, refreshToken, user, isNewUser }

POST   /auth/oauth/google
Body:  { idToken }
Resp:  { accessToken, refreshToken, user, isNewUser }

POST   /auth/forgot-password
Body:  { email }
Resp:  { message: "Reset email sent if account exists" }

POST   /auth/reset-password
Body:  { token, newPassword }
Resp:  { success }
```

### 7.2 Assessment (Prakriti & Vikriti)

```
POST   /assessment/prakriti
Body:  { responses: [{ questionId, value: 0-3 }], healthGoals: string[] }
Resp:  { prakriti: { vata, pitta, kapha, dominantType, description, characteristics } }

GET    /assessment/prakriti
Resp:  { prakriti, assessedAt, canRetake: boolean }

POST   /assessment/vikriti
Body:  { symptoms: string[], lifestyle: { stress, sleep, diet, exercise } }
Resp:  { vikriti: { imbalances, agniState, amaLevel, ojasLevel }, recommendations: string[] }

GET    /assessment/vikriti
Resp:  { vikriti, lastUpdatedBy, updatedAt }
```

### 7.3 User Profile & Twin

```
GET    /users/me
Resp:  { user, constitution, currentState, healthProfile, twinPreferences }

PUT    /users/profile
Body:  { fullName?, dateOfBirth?, gender?, timezone?, avatarUrl? }
Resp:  { user }

GET    /users/health-profile
Resp:  { healthProfile }

PUT    /users/health-profile
Body:  { medicalConditions?, currentMedications?, allergies?, dietaryRestrictions?,
         dietaryPreferences?, healthGoals?, pregnancyStatus?, wakeTime?, sleepTime? }
Resp:  { healthProfile }

GET    /twin/preferences
Resp:  { twinPreferences }

PUT    /twin/preferences
Body:  { twinName?, communicationStyle?, verbosityLevel?, sanskritUsage?,
         voiceEnabled?, morningTimeSummaryTime?, notificationPreferences?,
         dataAccessPermissions? }
Resp:  { twinPreferences }
```

### 7.4 Chat

```
GET    /chat/conversations
Query: { page?, limit?, type?, search? }
Resp:  { conversations: [{ id, title, lastMessage, lastMessageAt, type }], total }

GET    /chat/conversations/:conversationId
Resp:  { conversation, messages: [{ id, sender, messageType, content, structuredData, createdAt }] }

DELETE /chat/conversations/:conversationId
Resp:  { success }

PUT    /chat/conversations/:conversationId/favorite
Body:  { isFavorited: boolean }
Resp:  { success }

-- WebSocket events (via Socket.io namespace /chat) --
EMIT   chat:send      { conversationId?, content, attachments?: [{ type, fileKey }] }
ON     chat:chunk     { chunk: string }
ON     chat:complete  { messageId, conversationId, tokensUsed }
ON     chat:error     { code, message, upgradeUrl? }
```

### 7.5 Health Data

```
POST   /health/checkin
Body:  { energyLevel: 1-10, sleepQuality: 1-10, digestionState, mood, symptoms?: string[], notes? }
Resp:  { checkinId, insight: string, tip: string }

GET    /health/checkins
Query: { startDate?, endDate?, limit? }
Resp:  { checkins: [...], trends: { energy, sleep, digestion, mood } }

GET    /health/scans
Query: { scanType?, startDate?, endDate? }
Resp:  { scans: [{ id, scanType, thumbnailUrl, summary, scannedAt }] }

GET    /health/scans/:scanId
Resp:  { scan: { id, scanType, imageUrl, analysis, recommendations, scannedAt } }

POST   /health/scan/presigned-url
Body:  { scanType: 'tongue'|'meal'|'skin'|'product' }
Resp:  { uploadUrl, fileKey, expiresIn: 300 }

POST   /health/scan/analyze
Body:  { fileKey, scanType }
Resp:  { scanId, analysis, recommendations, doshaIndicators, amaSignal?, agniSignal? }

GET    /health/lab-results
Resp:  { labResults: [{ id, testDate, labName, status, summary }] }

GET    /health/lab-results/:labId
Resp:  { labResult: { id, biomarkers, overallPattern, rootCauseAnalysis, actionPlan, medicalFlags } }

POST   /health/lab/presigned-url
Resp:  { uploadUrl, fileKey, expiresIn: 300 }

POST   /health/lab/confirm
Body:  { fileKey, testDate, labName? }
Resp:  { labResultId, status: 'processing', estimatedReadyIn: '2-5 minutes' }

POST   /health/manual-log
Body:  { logType: 'meal'|'symptom'|'mood'|'meditation'|'menstrual'|'supplement',
         data: object, notes?, loggedAt? }
Resp:  { logId }

GET    /health/manual-logs
Query: { logType?, startDate?, endDate? }
Resp:  { logs: [...] }
```

### 7.6 Wearables

```
GET    /wearables/devices
Resp:  { devices: [{ deviceType, syncStatus, lastSyncedAt }] }

POST   /wearables/connect
Body:  { deviceType: 'apple_health'|'oura'|'whoop'|'fitbit'|'garmin',
         accessToken?, permissionsGranted?: string[] }
Resp:  { connected, syncStatus: 'pending' }

DELETE /wearables/disconnect/:deviceType
Resp:  { success }

POST   /wearables/sync
Body:  { deviceType, dataPoints: [{ dataType, recordedAt, rawValues }] }
Resp:  { synced: number, skipped: number }

GET    /wearables/summary
Query: { startDate, endDate, deviceType? }
Resp:  { summary: { sleep: {...}, activity: {...}, heart: {...}, ayurvedic: { interpretation, doshaSignals } } }
```

### 7.7 Protocols

```
POST   /protocols/generate
Body:  { primaryConcern: string, duration?: number, intensity?: 'gentle'|'moderate'|'intensive',
         constraints?: string[] }
Resp:  { protocol: { id, name, description, duration, phases, recommendations,
                     successMetrics, checkinSchedule } }

GET    /protocols
Query: { status?: 'active'|'completed'|'archived', page?, limit? }
Resp:  { protocols: [...], total }

GET    /protocols/:protocolId
Resp:  { protocol, currentPhase, todayRecommendations, adherencePercentage }

POST   /protocols/:protocolId/activate
Resp:  { success, activeProtocol }

POST   /protocols/:protocolId/pause
Body:  { reason? }
Resp:  { success }

PUT    /protocols/:protocolId/modify
Body:  { modifications: [{ recommendationId, change: string, reason: string }],
         changeReason: string }
Resp:  { updatedProtocol, version }

POST   /protocols/:protocolId/track
Body:  { trackedDate: date, completedItems: string[], skippedItems?: string[],
         notes?, symptomChanges?: string[], energyRating?: 1-10, overallFeeling? }
Resp:  { trackingId, adherencePercentage, streak }

GET    /protocols/:protocolId/progress
Resp:  { adherenceHistory: [...], symptomTrends: {...}, milestones: [...] }

GET    /protocols/library
Query: { concern?, dosha?, duration?, intensity?, page?, limit? }
Resp:  { protocols: [{ id, name, description, targetImbalances, duration, rating, usageCount }] }
```

### 7.8 Insights

```
GET    /insights/health
Query: { period?: '7d'|'30d'|'90d' }
Resp:  { doshaBalance: { vata, pitta, kapha, trend },
         agniState, amaLevel, ojasLevel,
         checkInTrends: { energy, sleep, digestion, mood },
         symptomFrequency: [{ symptom, count, trend }] }

GET    /insights/wearables
Query: { period?, dataType? }
Resp:  { sleepAnalysis: {...}, hrvTrends: {...}, activityTrends: {...},
         ayurvedicInterpretation: string }

GET    /insights/nutrition
Query: { period? }
Resp:  { sixTasteBalance: {...}, doshaImpact: {...}, mealTimingScore, hydrationAvg }

GET    /insights/supplements
Resp:  { currentSupplements: [...], effectivenessRatings: [...], interactions: [...] }
```

### 7.9 Notifications

```
GET    /notifications
Query: { status?: 'unread'|'all', page?, limit? }
Resp:  { notifications: [{ id, type, title, body, status, createdAt }] }

PUT    /notifications/:notificationId/read
Resp:  { success }

DELETE /notifications/:notificationId
Resp:  { success }

GET    /notifications/morning-summary/latest
Resp:  { summary: { content, generatedAt, sleepInsight, doshaForecast, topActions } }

POST   /notifications/device-token
Body:  { deviceToken: string, platform: 'ios' }
Resp:  { success }
```

### 7.10 Subscriptions

```
GET    /subscriptions/current
Resp:  { plan, status, currentPeriodEnd, cancelAtPeriodEnd, usage: { aiMessages, imageScans, labUploads } }

POST   /subscriptions/checkout
Body:  { plan: 'personal'|'premium'|'practitioner', successUrl, cancelUrl }
Resp:  { checkoutUrl }

POST   /subscriptions/portal
Resp:  { portalUrl }

POST   /subscriptions/webhook
-- Stripe webhook handler (no auth required, verified by Stripe signature)
```

### 7.11 Privacy & Data

```
GET    /privacy/settings
Resp:  { dataAccessPermissions, integrationConsents, aiTrainingConsent }

PUT    /privacy/settings
Body:  { dataAccessPermissions?, aiTrainingConsent? }
Resp:  { settings }

POST   /privacy/export
Body:  { format: 'json'|'pdf'|'csv', dataTypes: string[], dateRange? }
Resp:  { exportId, estimatedReadyIn }

GET    /privacy/export/:exportId
Resp:  { status, downloadUrl? }

DELETE /privacy/data
Body:  { dataTypes: string[], confirmation: 'DELETE_MY_DATA' }
Resp:  { scheduled, recoveryWindowDays: 30 }

DELETE /privacy/account
Body:  { confirmation: 'DELETE_MY_ACCOUNT', password }
Resp:  { scheduled, recoveryWindowDays: 30 }

GET    /privacy/audit-log
Query: { page?, limit? }
Resp:  { logs: [{ action, resource, timestamp, ipAddress }] }
```

---

## 8. AI Integration Design (Claude API)

### 8.1 Overview

The Digital Twin is powered by Claude Sonnet via the Anthropic API. Every chat interaction, protocol generation, image analysis, morning summary, and prediction alert passes through the `AiService` in the NestJS backend. The mobile app never calls the Anthropic API directly — all AI calls are mediated by the backend.

```
Mobile App → NestJS AiService → Anthropic API
                    ↑
             Context Assembly
             Tool Execution
             Safety Checks
```

### 8.2 System Prompt Strategy

The system prompt is assembled dynamically per request by the `ContextAssemblyService`. It has two parts:

**Part 1 — Static Base Prompt** (from Master Prompt, ~15k tokens)
Loaded once at server startup, cached in Redis. Contains:
- Identity and role definition
- Communication style and tone
- Foundational Ayurvedic knowledge (doshas, Agni, Ama, Ojas, six tastes, seasonal routines)
- Herb and food knowledge base
- Safety and medical boundary rules
- Response quality guidelines

**Part 2 — Dynamic User Context Block** (assembled per request, ~2–8k tokens)
Injected immediately after the base prompt. Contains:
```
## CURRENT USER CONTEXT

### User Identity
- Name: {fullName}
- Twin Name: {twinName}
- Communication Style: {communicationStyle}
- Verbosity: {verbosityLevel}
- Sanskrit Usage: {sanskritUsage}

### Constitution (Prakriti) — Immutable
- Vata: {vata}% | Pitta: {pitta}% | Kapha: {kapha}%
- Dominant Type: {dominantType}
- Constitutional Summary: {description}

### Current State (Vikriti) — As of {updatedAt}
- Vata Imbalance: {vataImbalance} (scale: -10 to +10)
- Pitta Imbalance: {pitaImbalance}
- Kapha Imbalance: {kaphaImbalance}
- Agni State: {agniState}
- Ama Level: {amaLevel}
- Ojas Level: {ojasLevel}/10
- Active Symptoms: {symptoms}

### Health Profile
- Conditions: {medicalConditions}
- Medications: {currentMedications}
- Allergies: {allergies}
- Dietary Restrictions: {dietaryRestrictions}
- Health Goals: {healthGoals}
- Pregnancy Status: {pregnancyStatus}

### Active Protocol
- Name: {protocolName}
- Phase: {currentPhase} of {totalPhases}
- Today's Recommendations: {todayItems}
- Adherence (last 7 days): {adherencePercentage}%

### Recent Check-Ins (last 7 days)
{checkinSummaryTable}

### Wearable Trends (if available)
- Sleep (7-day avg): {sleepAvg}h, quality {sleepQualityAvg}/10
- HRV (7-day avg): {hrvAvg}ms, trend: {hrvTrend}
- Activity: {activitySummary}

### Context
- Current Date: {date}
- Season: {season}
- User Timezone: {timezone}
- Time of Day: {timeOfDay}
```

### 8.3 Context Window Management

| Priority | Content | Max Tokens |
|---|---|---|
| 1 (always kept) | System prompt (base + user context) | ~20k |
| 2 (always kept) | Most recent 5 messages | ~3k |
| 3 (trim last) | Older conversation history | up to 70k |
| 4 (always kept) | Current user message | ~2k |
| **Total budget** | | **~100k tokens** |

**Trimming strategy:** When assembled context approaches 95k tokens, remove oldest messages first (beyond the most recent 5) until budget is met. The user context block is never trimmed — it always reflects current state.

### 8.4 Claude API Tool Definitions

The Digital Twin has access to 10 tools. Tools allow Claude to fetch live data and take actions without requiring the data to be pre-loaded in the context.

```typescript
const tools: Tool[] = [

  {
    name: "get_user_health_summary",
    description: "Get the user's current health state including recent check-ins, wearable data trends, and active protocol status. Call this when the user asks about their current health, energy, or progress.",
    input_schema: {
      type: "object",
      properties: {
        include_wearables: { type: "boolean", default: true },
        days_back: { type: "number", default: 7 }
      }
    }
  },

  {
    name: "get_active_protocols",
    description: "Retrieve the user's current active wellness protocols including today's recommendations and phase details.",
    input_schema: { type: "object", properties: {} }
  },

  {
    name: "create_protocol",
    description: "Generate and save a new wellness protocol for the user. Use when the user requests a protocol for a specific health concern.",
    input_schema: {
      type: "object",
      required: ["primaryConcern", "duration"],
      properties: {
        primaryConcern: { type: "string" },
        duration: { type: "number", description: "Total days, e.g. 7, 21, 90" },
        intensity: { type: "string", enum: ["gentle", "moderate", "intensive"], default: "moderate" },
        constraints: { type: "array", items: { type: "string" } }
      }
    }
  },

  {
    name: "modify_protocol",
    description: "Adjust an existing active protocol. Use when the user wants to change a recommendation, skip an item, or adjust the protocol based on feedback.",
    input_schema: {
      type: "object",
      required: ["protocolId", "modifications", "changeReason"],
      properties: {
        protocolId: { type: "string" },
        modifications: {
          type: "array",
          items: {
            type: "object",
            properties: {
              recommendationId: { type: "string" },
              change: { type: "string" },
              reason: { type: "string" }
            }
          }
        },
        changeReason: { type: "string" }
      }
    }
  },

  {
    name: "log_checkin",
    description: "Log a daily check-in for the user. Use when the user reports their current energy, sleep, digestion, or mood during conversation.",
    input_schema: {
      type: "object",
      properties: {
        energyLevel: { type: "number", minimum: 1, maximum: 10 },
        sleepQuality: { type: "number", minimum: 1, maximum: 10 },
        digestionState: { type: "string", enum: ["good", "variable", "sluggish", "burning"] },
        mood: { type: "string", enum: ["calm", "anxious", "irritable", "heavy", "mixed"] },
        symptoms: { type: "array", items: { type: "string" } }
      }
    }
  },

  {
    name: "check_herb_safety",
    // NOTE: Herb property knowledge comes from Claude's training data, NOT a pre-built DB.
    // This tool retrieves the user's medications + conditions from DB and asks Claude to reason
    // about safety. Claude caches the herb info to herbs table after generating it.
    description: "Check if a specific herb is safe for this user. Retrieves user's current medications and health conditions from their profile, then generates a safety assessment using Ayurvedic herb knowledge. Always call this before recommending any herb. Result is cached to herbs table.",
    input_schema: {
      type: "object",
      required: ["herbName"],
      properties: {
        herbName: { type: "string" },
        intendedUse: { type: "string" }
      }
    }
  },

  {
    name: "lookup_herb",
    // NOTE: Checks herbs cache table first (ai_generated=true rows are acceptable for MVP).
    // If not cached, Claude generates the response and the tool handler caches it.
    description: "Get detailed Ayurvedic properties of a herb — rasa, virya, vipaka, dosha effects, dosage, and contraindications. Checks cache first; generates and caches if not found.",
    input_schema: {
      type: "object",
      required: ["herbName"],
      properties: {
        herbName: { type: "string" }
      }
    }
  },

  {
    name: "lookup_food",
    // Same cache pattern as lookup_herb.
    description: "Get Ayurvedic properties of a food — six tastes, dosha effects, agni impact, and food combining rules. Checks cache first; generates and caches if not found.",
    input_schema: {
      type: "object",
      required: ["foodName"],
      properties: {
        foodName: { type: "string" }
      }
    }
  },

  {
    name: "log_manual_entry",
    description: "Log a manual health entry on behalf of the user (meal, symptom, supplement, meditation session) when the user mentions it during conversation.",
    input_schema: {
      type: "object",
      required: ["logType", "data"],
      properties: {
        logType: { type: "string", enum: ["meal", "symptom", "supplement", "meditation", "menstrual"] },
        data: { type: "object" },
        notes: { type: "string" }
      }
    }
  },

  {
    name: "detect_emergency",
    description: "ALWAYS call this tool first if the user's message contains any potential emergency keywords (chest pain, difficulty breathing, suicidal thoughts, severe bleeding, stroke symptoms, loss of consciousness, severe allergic reaction, high fever with confusion, severe abdominal pain). This tool logs the event and returns the emergency response template.",
    input_schema: {
      type: "object",
      required: ["emergencyType", "userMessage"],
      properties: {
        emergencyType: { type: "string" },
        userMessage: { type: "string" }
      }
    }
  }

];
```

### 8.5 Tool Execution Flow

```
Claude API stream begins
  ↓
Claude emits tool_use block
  ↓
NestJS intercepts stream, pauses forwarding to client
  ↓
ToolExecutorService.execute(toolName, toolInput, userId)
  ↓
Tool handler calls relevant NestJS service
  (e.g., create_protocol → ProtocolService.generate())
  ↓
Tool result returned to Claude as tool_result block
  ↓
Claude continues generating response
  ↓
Stream resumes forwarding to client
```

Tools that take significant time (e.g., `create_protocol`) emit a `chat:tool_progress` WebSocket event to show the client a loading state.

### 8.6 Streaming Implementation

```typescript
// NestJS AiService.streamChat()
async streamChat(userId: string, conversationId: string, content: string, socket: Socket) {
  const context = await this.contextService.assemble(userId);
  const history = await this.messageRepo.getRecent(conversationId, 20);

  const stream = await this.anthropic.messages.stream({
    model: 'claude-sonnet-4-5',
    max_tokens: 2048,
    system: context.systemPrompt,
    messages: [...history, { role: 'user', content }],
    tools: AYUAWARE_TOOLS,
  });

  for await (const event of stream) {
    if (event.type === 'content_block_delta' && event.delta.type === 'text_delta') {
      socket.emit('chat:chunk', { chunk: event.delta.text });
    }
    if (event.type === 'content_block_start' && event.content_block.type === 'tool_use') {
      const result = await this.toolExecutor.execute(event.content_block, userId);
      // feed result back to stream continuation
    }
  }

  const finalMessage = await stream.finalMessage();
  await this.saveMessage(conversationId, userId, content, finalMessage);
  socket.emit('chat:complete', { messageId, tokensUsed: finalMessage.usage });
}
```

### 8.7 Model Selection & Fallback

| Use Case | Model | Max Tokens | Notes |
|---|---|---|---|
| Chat conversation | claude-sonnet-4-5 | 2048 | Primary model |
| Protocol generation | claude-sonnet-4-5 | 4096 | More complex output |
| Image analysis (scan) | claude-sonnet-4-5 | 1024 | Vision-enabled |
| Morning summary | claude-sonnet-4-5 | 1024 | Scheduled job |
| Prediction alert | claude-sonnet-4-5 | 512 | Background job |
| Simple FAQ (cached miss) | claude-haiku-3 | 512 | High-load fallback |

**Fallback logic:**
```
If Claude Sonnet API latency > 5s OR error rate > 5%:
  → Route simple conversational queries to Claude Haiku
  → Queue complex tasks (protocol generation) in BullMQ
  → Return to user: "Your request is being processed..."
  → Notify via push when complete
```

### 8.8 Rate Limiting & Usage Tracking

```
Per request:
  1. Check Redis key: rate_limit:{userId}:{minute} → max 10 req/min
  2. Check PostgreSQL: usage_counters.ai_messages for current billing period
     - Free:     20/month
     - Personal: unlimited
     - Premium:  unlimited
  3. If at limit: return 429 with { code: 'USAGE_LIMIT', plan, upgradeUrl }

After each successful response:
  → INCREMENT usage_counters.ai_messages WHERE user_id = ? AND period_start = ?
  → UPDATE Redis token count
```

---

## 9. Module Technical Specifications

> Each module covers: **Data Model**, **API Endpoints**, **Business Logic**, **AI Touchpoints**. Tier 1 modules are fully specified. Tier 2 and 3 modules include sufficient detail for initial development planning.

---

### 9.1 Onboarding Module [TIER 1]

**Purpose:** Guide new users from signup through Prakriti assessment, Digital Twin setup, and first protocol activation.

**Tables used:** `users`, `user_constitution`, `user_current_state`, `user_health_profile`, `user_twin_preferences`, `protocols`

**Key business logic:**
- Assessment responses stored raw in `user_constitution.assessment_responses` (for auditability / re-scoring)
- Scoring algorithm runs server-side (never on device) — see Section 6.1 for algorithm
- Prakriti percentages must always sum to exactly 100 (rounding applied to kapha last)
- `onboarding_complete` flag set on `users` table only after protocol is activated
- If user abandons mid-onboarding, resume from last completed step (step tracked in Redis)
- Users can retake assessment after 90 days (controlled by `can_retake` logic comparing `assessed_at`)

**AI touchpoints:**
- Step 6 (deep-dive chat): `conversation_type = 'onboarding'` conversation; Twin asks targeted questions to populate `user_health_profile`
- Step 7 (protocol generation): `create_protocol` tool called within onboarding conversation context

---

### 9.2 Chat / Digital Twin Module [TIER 1]

**Purpose:** Core product surface — the AI conversation interface where users interact with their Digital Twin.

**Tables used:** `conversations`, `messages`, `usage_counters`

**Key business logic:**
- New conversation created automatically on first message if no `conversationId` provided
- Conversation title auto-generated from first user message (truncated to 60 chars) using lightweight Claude Haiku call
- Message types rendered differently on client:
  - `text` → standard chat bubble
  - `protocol_card` → tappable card with protocol summary + "View Protocol" CTA
  - `summary_card` → structured card (morning summary, check-in result)
  - `visualization` → embedded chart component
  - `quick_action` → horizontally scrolling action buttons
- Conversation list sorted by `last_message_at DESC`
- Soft delete: conversations marked `deleted_at`, purged after 30 days (Free) / 1 year (Personal+)

**Context assembly rules:**
1. Always include: Prakriti, Vikriti, active protocol summary, twin preferences
2. Include: last 7 check-ins, last 7 days wearable summary (if connected)
3. Conditionally include: last 20 messages from this conversation (trim if over budget)
4. Exclude from context (fetched via tools on demand): herb details, food details, historical scans

---

### 9.3 Daily Check-In Module [TIER 1]

**Purpose:** Primary Vikriti update mechanism. Quick 5-question form that updates the user's current state and surfaces an AI insight.

**Tables used:** `daily_checkins` (TimescaleDB), `user_current_state`

**Key business logic:**
- Only one check-in per day (per `user_id + DATE(checked_in_at)` uniqueness)
- If user checks in twice: second check-in overwrites first within the same calendar day
- Vikriti update rules from check-in input:

| Check-In Field | Value | Vikriti Update |
|---|---|---|
| `digestionState` | `burning` | `agni_state = 'tikshna'`, `pitta_imbalance += 1` |
| `digestionState` | `sluggish` | `agni_state = 'manda'`, `kapha_imbalance += 1` |
| `digestionState` | `variable` | `agni_state = 'vishama'`, `vata_imbalance += 1` |
| `digestionState` | `good` | `agni_state = 'sama'` |
| `mood` | `anxious` or `scattered` | `vata_imbalance += 1` |
| `mood` | `irritable` | `pitta_imbalance += 1` |
| `mood` | `heavy` | `kapha_imbalance += 1` |
| `energyLevel` | ≤3 | `ojas_level -= 1` (min 1) |
| `energyLevel` | ≥8 | `ojas_level += 0.5` (max 10) |

- After update, check for prediction alert conditions (3+ consecutive days with same signal)
- AI insight generated async via BullMQ `checkin_insight` job (1–3 sentence response using Haiku for speed)

---

### 9.4 Protocol Engine Module [TIER 1]

**Purpose:** Create, manage, track, and modify AI-generated wellness protocols.

**Tables used:** `protocols`, `protocol_versions`, `protocol_tracking`

**Protocol data structure (JSONB fields):**

```typescript
// phases JSONB structure
phases: [{
  name: 'Foundation' | 'Building' | 'Maintenance',
  durationDays: number,
  focusAreas: string[],
  intensity: 'gentle' | 'moderate' | 'intensive'
}]

// recommendations JSONB structure
recommendations: [{
  id: string,           // UUID for modification targeting
  category: 'dietary' | 'lifestyle' | 'herbs' | 'practices' | 'environmental',
  phase: number,        // 0 = all phases, 1 = Foundation only, etc.
  action: string,
  frequency: string,    // 'daily', '3x weekly', 'with each meal'
  timing: string,       // 'morning', 'before bed', 'with meals'
  rationale: string,
  tips: string[],
  contraindications: string[],
  alternatives: string[]
}]

// successMetrics JSONB structure
successMetrics: [{
  metric: string,
  baseline: any,
  target: any,
  measurementMethod: string,
  checkByDay: number
}]
```

**Key business logic:**
- Free plan: max 1 active protocol. Activating a new one auto-pauses the existing one
- Herb safety check runs synchronously during protocol generation before saving draft
- Protocol version snapshot taken before every modification (immutable audit trail)
- Adherence calculated nightly: `(completed_items_count / total_items_count) * 100` across last 7 days
- Protocol phases auto-advance based on `activated_at + phase.durationDays`

---

### 9.5 Insights / Health Dashboard Module [TIER 1]

**Purpose:** Visual dashboard showing the user's dosha balance, Agni, Ama, Ojas, and health trends over time.

**Tables used:** `user_current_state`, `daily_checkins`, `wearable_data_points`, `scan_analyses`

**Health Tab — Data Aggregation Queries:**

```sql
-- Dosha trend over 30 days (using check-in mood/digestion signals)
SELECT
  DATE(checked_in_at) as date,
  AVG(CASE WHEN 'anxious' = ANY(symptoms) OR mood = 'anxious' THEN 1 ELSE 0 END) as vata_signal,
  AVG(CASE WHEN mood = 'irritable' OR digestion_state = 'burning' THEN 1 ELSE 0 END) as pitta_signal,
  AVG(CASE WHEN mood = 'heavy' OR digestion_state = 'sluggish' THEN 1 ELSE 0 END) as kapha_signal
FROM daily_checkins
WHERE user_id = $1 AND checked_in_at > NOW() - INTERVAL '30 days'
GROUP BY date ORDER BY date;

-- Energy and sleep 7-day moving average
SELECT
  time_bucket('1 day', checked_in_at) as day,
  AVG(energy_level) as avg_energy,
  AVG(sleep_quality) as avg_sleep
FROM daily_checkins
WHERE user_id = $1 AND checked_in_at > NOW() - INTERVAL '30 days'
GROUP BY day ORDER BY day;
```

**Rendered indicators:**
- **Dosha Balance**: Three-segment gauge (Vata/Pitta/Kapha) showing current Vikriti vs Prakriti baseline
- **Agni State**: Icon with label (Sama=green, Vishama=amber, Tikshna=red-warm, Manda=blue-slow)
- **Ama Level**: Horizontal bar (None→Low→Moderate→High)
- **Ojas Meter**: 1–10 circular dial
- **Trend charts**: 7d/30d/90d switchable line charts for energy, sleep, digestion, mood

---

### 9.6 Today Section Module [TIER 2]

**Purpose:** Daily dashboard showing morning summary, active protocol checklist, and quick stats.

**Tables used:** `notifications`, `protocols`, `protocol_tracking`, `user_current_state`

**Components:**
- **Morning Summary Card**: Pull latest `notifications` where `type = 'morning_summary'` and `DATE(created_at) = TODAY`
- **Current Status Snapshot**: Read `user_current_state` — show Agni, Ama, Ojas, dominant imbalance
- **Today's Actions**: Query active protocol's today recommendations; join with `protocol_tracking` for today to show completion state
- **Quick Stats**: Last check-in data; wearable last-night summary

**Today's Actions completion:**
```
PATCH /api/v1/protocols/:id/track/item
Body: { date, recommendationId, completed: boolean }
→ Upsert into protocol_tracking.completed_items array
→ Recalculate adherence_percentage
```

---

### 9.7 Apple HealthKit Integration Module [TIER 2]

**Purpose:** Automatically sync Apple Health data to enrich Vikriti without manual entry.

**iOS native implementation (React Native):**
```typescript
// Using react-native-health library
const permissions = {
  permissions: {
    read: [
      AppleHealthKit.Constants.Permissions.SleepAnalysis,
      AppleHealthKit.Constants.Permissions.HeartRateVariabilitySDNN,
      AppleHealthKit.Constants.Permissions.HeartRate,
      AppleHealthKit.Constants.Permissions.StepCount,
      AppleHealthKit.Constants.Permissions.ActiveEnergyBurned,
      AppleHealthKit.Constants.Permissions.BodyTemperature,
      AppleHealthKit.Constants.Permissions.RespiratoryRate,
    ]
  }
};
```

**Sync strategy:**
- **Foreground sync**: When app opens, sync last 24 hours
- **Background fetch**: iOS Background App Refresh, sync last 1 hour
- **Initial sync**: On first connect, sync last 30 days
- Data sent to `POST /api/v1/wearables/sync` in batches of 200 data points

**Ayurvedic interpretation rules for sleep data:**

| Metric | Value | Signal |
|---|---|---|
| Sleep duration | <6 hours | Vata aggravation, Ojas depletion |
| Sleep duration | >9 hours | Kapha excess |
| Sleep onset latency | >30 min | Vata imbalance |
| Awakenings count | >3/night | Vata imbalance |
| Waking time | 10pm–2am | Pitta imbalance |
| HRV 7-day avg | <30ms | Ojas low, Vata/Pitta stress |
| HRV declining | >20% over 3 days | Prediction alert trigger |
| Resting HR | Elevated >10% from baseline | Pitta aggravation |

---

### 9.8 Scan Analysis Module [TIER 2]

**Purpose:** AI-powered image analysis for tongue, meals, skin, and product labels using Claude Vision.

**Tables used:** `scan_analyses`, `usage_counters`

**Scan type specifications:**

**Tongue Scan — Analysis Output Schema:**
```typescript
{
  coating: {
    presence: 'none' | 'thin' | 'moderate' | 'thick',
    color: 'white' | 'yellow' | 'brown' | 'grey',
    location: ('front' | 'middle' | 'back' | 'sides')[]
  },
  tongueColor: 'pale' | 'normal-pink' | 'red' | 'dark-red' | 'purple',
  texture: 'dry' | 'moist' | 'swollen',
  shape: {
    teethMarks: boolean,
    cracks: ('midline' | 'transverse' | 'geographic')[],
    size: 'small' | 'normal' | 'swollen'
  },
  amaLevel: 'none' | 'low' | 'moderate' | 'high',
  agniState: 'sama' | 'vishama' | 'tikshna' | 'manda',
  doshaIndicators: string[],
  organCorrelations: string[],
  recommendations: string[]
}
```

**Meal Scan — Analysis Output Schema:**
```typescript
{
  ingredientsIdentified: { name: string, confidence: number }[],
  sixTastes: { sweet: %, sour: %, salty: %, pungent: %, bitter: %, astringent: % },
  doshaImpact: { vata: -5..+5, pitta: -5..+5, kapha: -5..+5 },
  foodCombining: { compatible: boolean, issues: string[] },
  constitutionalSuitability: 'excellent' | 'good' | 'moderate' | 'poor',
  agniImpact: 'strengthens' | 'neutral' | 'weakens',
  preparationQuality: string,
  improvements: string[]
}
```

**Image quality validation:**
- Minimum resolution: 400×400px
- If quality insufficient: return `{ error: 'IMAGE_QUALITY', message, retakeGuide }`
- Max file size: 10MB (enforced at presigned URL generation)

---

### 9.9 Morning Summary Module [TIER 2]

**Purpose:** Daily AI-generated personalized health briefing delivered via push notification.

**Trigger:** BullMQ cron job, per-user at `user_twin_preferences.morning_summary_time` in user's timezone

**Generation prompt inputs:**
1. Last night's sleep data (HealthKit or last check-in)
2. Current Vikriti state
3. Active protocol — today's phase and recommendations
4. Active prediction alerts (if any)
5. Current season + day of week
6. User's twin name and communication style preference

**Output structure stored in notification.data:**
```typescript
{
  greeting: string,            // personalized opening
  sleepInsight: string,        // interpretation of last night
  doshaForecast: string,       // what to watch for today
  topActions: string[],        // 3 specific actions (from protocol + current state)
  encouragement: string        // closing motivational note
}
```

---

### 9.10 Lab Results Module [TIER 3]

**Purpose:** Upload and AI-interpret blood work and other lab reports. Premium feature.

**Tables used:** `lab_results`
**Plan gate:** Premium only (3 uploads/month)

**OCR + Interpretation pipeline:**
1. PDF uploaded to S3 via presigned URL
2. BullMQ job: `lab_ocr_processing`
3. Call Claude Vision with PDF page images: extract all biomarkers as structured JSON
4. For each biomarker:
   - Look up in internal knowledge map (biomarker → dhatu + dosha)
   - Flag if outside reference range
   - Generate Ayurvedic interpretation
5. Synthesize cross-biomarker patterns
6. Generate protocol recommendations based on findings
7. Any critically abnormal values → `medical_flags` + push notification with "consult doctor" message

**Biomarker → Ayurvedic Mapping Examples:**
| Biomarker | Low | High | Dhatu | Dosha Signal |
|---|---|---|---|---|
| Hemoglobin | Rakta (blood) dhatu deficiency | — | Rakta | Pitta/Vata |
| Ferritin | Rakta dhatu depletion, Ojas low | — | Rakta | Vata |
| TSH | Hypothyroid → Kapha excess | Hyperthyroid → Vata/Pitta | Meda | Kapha/Vata |
| Cortisol AM | Adrenal fatigue, Ojas depletion | Chronic stress, Pitta aggrav | — | Vata/Pitta |
| Vitamin D | Asthi (bone) dhatu weakness | — | Asthi | Vata/Kapha |
| CRP | — | Inflammation, Ama high, Pitta excess | — | Pitta |

---

### 9.11 History Module [TIER 2]

**Purpose:** Searchable archive of all past conversations, organized by date and type.

**Tables used:** `conversations`, `messages`

**Search implementation:**
```sql
-- Full-text conversation search
SELECT c.id, c.title, c.last_message_at,
       ts_headline('english', m.content, query) as snippet
FROM conversations c
JOIN messages m ON m.conversation_id = c.id
  AND m.sender = 'twin'
  AND to_tsvector('english', m.content) @@ plainto_tsquery($2)
WHERE c.user_id = $1
ORDER BY ts_rank(to_tsvector('english', m.content), plainto_tsquery($2)) DESC
LIMIT 20;
```

**Retention policy:**
- Free: 30 days
- Personal: 1 year
- Premium+: Unlimited
- Soft delete at `conversations.deleted_at`; hard delete via nightly cleanup job

---

### 9.12 Projects Module [TIER 3]

**Purpose:** Long-term health goals combining multiple sequential protocols with milestone tracking.

**Tables used:** `projects` (new table), `project_protocols`, `project_milestones`

```sql
CREATE TABLE projects (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id       UUID REFERENCES users(id) ON DELETE CASCADE,
  title         VARCHAR(255) NOT NULL,
  description   TEXT,
  health_goal   TEXT,
  start_date    DATE,
  target_end_date DATE,
  status        VARCHAR(20) DEFAULT 'active',
  milestones    JSONB,
  created_at    TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE project_protocols (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id  UUID REFERENCES projects(id) ON DELETE CASCADE,
  protocol_id UUID REFERENCES protocols(id),
  sequence    SMALLINT,   -- order within project
  status      VARCHAR(20) DEFAULT 'pending'  -- pending, active, completed
);
```

---

### 9.13 Learn Module [TIER 3]

**Purpose:** Gamified Ayurvedic education with lessons, badges, and learning streaks.

**Tables used:** `learn_lessons`, `learn_paths`, `user_learn_progress`

```sql
CREATE TABLE learn_lessons (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  path_id     UUID,
  title       VARCHAR(255),
  content     JSONB,  -- { introduction, core, interactive, application, summary }
  dosha_focus TEXT[], -- which doshas this lesson is most relevant to
  difficulty  VARCHAR(20),
  duration_minutes SMALLINT,
  order_in_path SMALLINT
);

CREATE TABLE user_learn_progress (
  id            UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id       UUID REFERENCES users(id) ON DELETE CASCADE,
  lesson_id     UUID REFERENCES learn_lessons(id),
  status        VARCHAR(20),  -- 'in_progress', 'completed'
  score         SMALLINT,
  completed_at  TIMESTAMPTZ,
  streak_days   SMALLINT DEFAULT 0
);
```

**Paths (seeded content):** Foundations, Your Constitution, Daily Rhythms, Seasonal Living, Food as Medicine, Herbal Wisdom, Mind-Body Practices, Advanced Topics

**Free tier:** First 2 lessons of each path; rest gated behind Personal+

---

### 9.14 Shop Module [TIER 3]

**Purpose:** Curated marketplace for Ayurvedic products with constitutional recommendations.

**Tables used:** `shop_products`, `shop_orders`

```sql
CREATE TABLE shop_products (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name            VARCHAR(255),
  category        VARCHAR(100),  -- herbs, teas, self_care, kitchen, books, tools
  description     TEXT,
  price_usd       DECIMAL(10,2),
  image_url       TEXT,
  affiliate_url   TEXT,          -- external product URL
  dosha_benefits  JSONB,         -- { vata: boolean, pitta: boolean, kapha: boolean }
  constitutional_suitability JSONB,
  ayurvedic_analysis TEXT,
  is_featured     BOOLEAN DEFAULT FALSE,
  is_active       BOOLEAN DEFAULT TRUE
);
```

**Product recommendations:** When user views Shop, query products filtered by `dosha_benefits` matching user's current Vikriti dominant imbalance.

---

### 9.15 Profile Module [TIER 1]

**Purpose:** User account settings, health profile, subscription management, and privacy controls.

**Tables used:** All user tables, `subscriptions`, `usage_counters`

**Key sections:**
- **Personal Info**: Name, email, DOB, gender, timezone, avatar — `PUT /users/profile`
- **Constitution**: View Prakriti results, retake after 90 days
- **Health Info**: Medical conditions, medications, allergies — `PUT /users/health-profile`
- **Dietary & Lifestyle**: Restrictions, preferences, goals — part of `user_health_profile`
- **Subscription**: Current plan, usage meters, upgrade CTA — `GET /subscriptions/current`
- **Notifications**: Toggle morning summary, prediction alerts, protocol reminders — `PUT /twin/preferences`
- **Privacy**: Data access permissions per integration, export data, delete account — `/privacy/*`
- **Achievements**: Badges earned from Learn module, streak counters

---

## 10. External Integrations

### 10.1 Apple HealthKit (iOS)

- **Library:** `react-native-health`
- **Auth:** iOS permission dialog (no OAuth — device-local)
- **Data flow:** iOS app reads HealthKit → batches to `POST /wearables/sync`
- **Permissions requested:** SleepAnalysis, HeartRateVariabilitySDNN, HeartRate, StepCount, ActiveEnergyBurned, BodyTemperature
- **Background sync:** iOS Background App Refresh (max ~30s execution window)

### 10.2 Apple Sign-In

- **Required by:** App Store guidelines (must offer if using any third-party OAuth)
- **Library:** `@invertase/react-native-apple-authentication`
- **Flow:** Apple identity token → `POST /auth/oauth/apple` → validated via Apple's public keys → user created/matched
- **Email relay:** Apple may provide relay email — stored as-is, not used for direct sending

### 10.3 Google Sign-In

- **Library:** `@react-native-google-signin/google-signin`
- **Flow:** Google ID token → `POST /auth/oauth/google` → validated via Google tokeninfo endpoint

### 10.4 Stripe

- **SDK:** `stripe` (Node.js) on backend; `@stripe/stripe-react-native` on mobile (for Apple Pay support later)
- **Subscription flow:**
  1. `POST /subscriptions/checkout` → create Stripe Checkout Session → return URL
  2. User completes payment in webview/browser
  3. Stripe webhook `customer.subscription.created` → update `users.subscription_tier` + insert `subscriptions` row
- **Webhooks:** `customer.subscription.updated`, `customer.subscription.deleted`, `invoice.payment_failed`
- **Webhook verification:** Stripe signature verification (never process without valid signature)

### 10.5 APNs (Apple Push Notifications)

- **Library:** `@aws-sdk/client-sns` or direct APNs via `apn` npm package
- **Token storage:** Device push token saved via `POST /notifications/device-token`
- **Notification types:** Morning summary (rich notification with summary preview), prediction alerts, protocol reminders
- **Delivery:** Backend sends via APNs HTTP/2 API

### 10.6 Razorpay (India / INR payments)

AyuAware targets a global market from launch. Indian users pay in INR via Razorpay; all other users via Stripe. Currency routing happens at signup based on detected locale.

- **SDK:** `razorpay` (Node.js) on backend; `react-native-razorpay` on mobile
- **Supported methods:** UPI, cards (Visa/MC/RuPay), net banking, wallets
- **Subscription flow:**
  1. `POST /subscriptions/checkout` with `{ currency: 'INR' }` → create Razorpay Subscription → return checkout token
  2. Mobile renders Razorpay checkout sheet (native SDK)
  3. Razorpay webhook `subscription.charged` → update `users.subscription_tier`
- **Webhooks:** `subscription.charged`, `subscription.cancelled`, `payment.failed`
- **Currency routing logic:**
  ```typescript
  // At signup / plan upgrade
  const gateway = user.locale === 'IN' ? 'razorpay' : 'stripe';
  const currency = user.locale === 'IN' ? 'INR' : 'USD';
  ```
- **DB change needed:** Add `inr_price_monthly` and `inr_price_yearly` fields to plan configuration; add `payment_gateway` enum (`stripe` | `razorpay`) to `subscriptions` table.

**INR pricing (indicative):**

| Plan | USD | INR (approx) |
|---|---|---|
| Personal | $9.99/mo | ₹849/mo |
| Premium | $24.99/mo | ₹2,099/mo |
| Practitioner | $99/mo | ₹8,299/mo |

### 10.7 Future Integrations (V2)

| Integration | API | Auth | Data |
|---|---|---|---|
| Oura Ring | Oura API v2 | OAuth 2.0 | Sleep, HRV, readiness |
| WHOOP | WHOOP API | OAuth 2.0 | Recovery, strain, sleep |
| Fitbit | Fitbit Web API | OAuth 2.0 | Sleep, activity, heart rate |
| Garmin | Garmin Health API | OAuth 2.0 | Activity, sleep, stress |
| Epic MyChart | FHIR R4 | Smart on FHIR | Lab results, medications |

---

## 11. Security & Compliance

### 11.1 Authentication Security

| Control | Implementation |
|---|---|
| Password hashing | bcrypt, cost factor 12 |
| Password policy | 8+ chars, upper, lower, number, special char; checked against HaveIBeenPwned API |
| Access token | JWT, RS256, 7-day expiry |
| Refresh token | Opaque token (hashed in DB), 30-day expiry, rotated on use |
| Token revocation | Refresh token blacklist in Redis; access token short-lived (no revocation needed) |
| CSRF protection | SameSite=Strict cookies + custom header check for state-changing ops |
| Session limits | Max 5 concurrent active refresh tokens per user |

### 11.2 Encryption

| Data | Encryption |
|---|---|
| Data in transit | TLS 1.3 (minimum), perfect forward secrecy |
| Data at rest (RDS) | AWS RDS encryption via KMS |
| Data at rest (S3) | SSE-KMS (Server-Side Encryption with KMS) |
| Sensitive fields | AES-256 field-level: `medical_conditions`, `current_medications`, genetic data, wearable OAuth tokens |
| Backups | Encrypted with separate KMS key |

### 11.3 Compliance by Jurisdiction

AyuAware launches globally. Three regulatory frameworks apply from day one:

**HIPAA (United States)**

| Requirement | Implementation |
|---|---|
| Business Associate Agreements | BAAs signed with: AWS, Anthropic, Stripe, Sentry |
| Access controls | Role-based: user, admin, support. No employee accesses PHI without audit log |
| Audit logging | All PHI access logged to `audit_logs` table: user, action, resource, timestamp, IP |
| Audit log retention | 7 years |
| Breach notification | Incident response plan; 60-day notification to affected users and HHS |
| Data minimization | Collect only what is necessary for core functionality |

**GDPR (European Union / UK)**

| Requirement | Implementation |
|---|---|
| Lawful basis | Explicit informed consent at signup |
| Data subject rights | Access, rectification, erasure, portability, objection — all via `/privacy/*` endpoints |
| Data Protection Officer | Designated DPO required when processing health data at scale |
| Cross-border transfers | Standard Contractual Clauses (SCCs) for data transfers outside EU |
| Breach notification | 72-hour notification to supervisory authority |

**DPDP Act (India — Digital Personal Data Protection Act 2023)**

| Requirement | Implementation |
|---|---|
| Explicit consent | Granular consent obtained at signup and at each data collection point |
| Data localisation | Indian user data stored in AWS `ap-south-1` (Mumbai) region. Requires separate RDS instance or read replica in India for DPDP compliance. |
| Grievance officer | Designated grievance officer with contact details in app and privacy policy; 30-day response obligation |
| Breach notification | Notify Data Protection Board and affected users promptly (specific timeline TBD by rules) |
| Right to erasure | `DELETE /privacy/account` → 30-day soft delete → permanent purge |
| Data fiduciary obligations | AyuAware is a "Significant Data Fiduciary" if processing sensitive personal data at scale — triggers additional audit requirements |

> **⚠️ Architecture implication:** DPDP data localisation requires Indian users' personal health data to reside in India (`ap-south-1`). For MVP with a 1-2 person team, a pragmatic approach is to route Indian users to a separate managed database (Railway's India region or AWS RDS ap-south-1) with a feature flag. Full multi-region replication is a Phase 2 infrastructure task.

### 11.4 Authorization Model

```
Guards applied per route in NestJS:

@UseGuards(JwtAuthGuard)                    → All authenticated routes
@UseGuards(JwtAuthGuard, SubscriptionGuard) → Plan-gated features
@UseGuards(JwtAuthGuard, ResourceOwnerGuard)→ Resource-specific access

SubscriptionGuard checks:
  users.subscription_tier IN (required_tiers)
  → 403 if insufficient tier, with { upgradeUrl } in response

ResourceOwnerGuard:
  Checks resource.user_id = req.user.id
  → 403 if accessing another user's data
  (Practitioners have explicit sharing grants — checked separately)
```

### 11.5 Input Validation & Security

- All input validated using `class-validator` decorators on NestJS DTOs
- File uploads: MIME type validation + AWS Lambda virus scan trigger on S3 upload
- SQL injection: Parameterized queries only (TypeORM / node-postgres with `$1` parameters)
- XSS: All user content sanitized with `DOMPurify` equivalent before storage
- Rate limiting: `@nestjs/throttler` — 100 req/min general, 10 req/min for AI endpoints
- API key protection: Anthropic API key, Stripe secret key stored in AWS Secrets Manager

### 11.6 Data Retention & User Rights

| Right | Implementation |
|---|---|
| Access | `GET /privacy/audit-log` + data export within 30 days |
| Rectification | `PUT /users/profile` + `PUT /users/health-profile` |
| Erasure | `DELETE /privacy/account` → 30-day soft delete → permanent purge |
| Portability | `POST /privacy/export` → JSON, PDF, or CSV within 7 days |
| Restriction | `PUT /privacy/settings` — granular permissions per data type |
| Objection to AI training | `PUT /privacy/settings { aiTrainingConsent: false }` — excluded from model fine-tuning |

---

## 12. Infrastructure & Deployment

> **Two-phase infrastructure plan.** Phase 1 (MVP, 1-2 devs) uses managed platforms to eliminate DevOps overhead. Phase 2 (production scale) migrates to full AWS for SLA, compliance, and cost efficiency at volume. Both phases use the same NestJS codebase — only deployment targets change.

### 12.0 Phase Comparison

| Concern | Phase 1 MVP (1-2 devs) | Phase 2 Production |
|---|---|---|
| **API hosting** | Railway.app or Fly.io | AWS ECS Fargate (auto-scaling) |
| **Database** | Railway PostgreSQL (managed) | AWS RDS PostgreSQL + Multi-AZ |
| **Redis** | Upstash (serverless, pay-per-use) | AWS ElastiCache |
| **File storage** | AWS S3 (keep from day 1) | AWS S3 (same) |
| **CDN / DNS** | Cloudflare (free tier) | AWS CloudFront + Route 53 |
| **Secrets** | Railway env vars / Doppler | AWS Secrets Manager |
| **Monitoring** | Sentry + Railway logs | Sentry + CloudWatch |
| **Est. infra cost** | ~$50–150/month at <1k users | ~$500–1,500/month at scale |
| **DevOps burden** | Near-zero | Requires dedicated attention |
| **Migration trigger** | When MAU > 5,000 or HIPAA audit required | — |

### 12.1 AWS Services (Phase 2 Production Target)

| Service | Purpose | Config |
|---|---|---|
| **ECS Fargate** | API containers (auto-scaling) | Min 2 tasks, max 20; scale on CPU >60% |
| **ECS Fargate** | Background worker containers | Min 1 task, max 10 |
| **RDS PostgreSQL** | Primary database | Multi-AZ, db.t3.medium (MVP), automated backups 7 days |
| **ElastiCache Redis** | Cache + job queue | cache.t3.micro cluster (MVP) |
| **S3** | File storage | Versioning enabled, lifecycle rules: move to Glacier after 1 year |
| **KMS** | Encryption key management | Separate keys for DB, S3, field-level encryption |
| **CloudFront** | CDN for static assets | iOS app API gateway, image serving |
| **ALB** | Load balancing + SSL termination | ACM certificate, HTTPS only |
| **ECR** | Docker image registry | Image scanning enabled |
| **Secrets Manager** | API keys + secrets | Anthropic key, Stripe key, JWT private key |
| **CloudWatch** | Logs + metrics + alarms | Log retention: 90 days; alarms on error rate, latency |
| **SNS / SES** | Push notifications + transactional email | APNs via SNS for iOS |

### 12.2 Environments

| Environment | Phase 1 (MVP) | Phase 2 (Production) |
|---|---|---|
| `development` | Docker Compose (Postgres + Redis local) | Same |
| `staging` | Railway/Fly.io staging env | Single ECS task, shared RDS non-prod |
| `production` | Railway/Fly.io production | AWS ECS Fargate, multi-AZ |

### 12.3 CI/CD Pipeline (GitHub Actions)

**Phase 1 (Railway/Fly.io):**
```
Push to feature/* → run tests + lint + type check
Merge to develop  → deploy to staging (Railway/Fly CLI)
Merge to main     → deploy to production + notify Slack
```

**Phase 2 (AWS ECS):**
```
Push to feature/* branch:
  → Run tests (unit + integration)
  → Run ESLint + TypeScript type check
  → Build Docker image (not deployed)

Merge to develop:
  → Build Docker image → push to ECR
  → Deploy to staging (ECS update-service --force-new-deployment)
  → Run smoke tests against staging

Merge to main:
  → Deploy to production (blue/green via ECS)
  → Run smoke tests against production
  → Notify team on Slack
```

### 12.4 Performance Targets & SLAs

| Metric | Target | Alert Threshold |
|---|---|---|
| API p50 response time | <200ms | >500ms for 5 min |
| API p95 response time | <500ms | >1s for 5 min |
| AI chat first token | <1.5s | >3s for 5 min |
| AI chat full response | <8s | >15s for 5 min |
| Image scan analysis | <10s | >20s |
| Protocol generation | <15s | >30s |
| Wearable sync | <5s per batch | >30s |
| App availability | 99.9% | <99.5% over 1 hour |
| Background job queue depth | <100 pending | >500 pending |

### 12.5 Disaster Recovery

- **RTO (Recovery Time Objective):** 1 hour
- **RPO (Recovery Point Objective):** 1 hour (RDS automated backups every hour)
- **Multi-AZ RDS:** Automatic failover within ~60 seconds on primary failure
- **S3:** Cross-region replication enabled for images and documents
- **Database backups:** Daily snapshots retained 7 days; weekly snapshots retained 4 weeks

### 12.6 Background Job Queues (BullMQ)

| Queue | Jobs | Concurrency | Retry |
|---|---|---|---|
| `wearable-sync` | Hourly per-user sync | 50 | 3x with backoff |
| `morning-summary` | Daily per-user at set time | 20 | 2x |
| `checkin-insight` | After each check-in | 30 | 3x |
| `prediction-scan` | Every 6h, all active users | 10 | 2x |
| `lab-ocr` | On lab upload | 5 | 3x |
| `protocol-adherence` | Nightly adherence check | 10 | 2x |

---

## 13. Unit Economics & Cost Analysis

> ⚠️ **Cost modeling has not been done yet. This section flags the key cost drivers and provides estimates to inform pricing and context window decisions before development begins.**

### 13.1 Claude API Cost Structure (as of Feb 2026)

| Model | Input tokens | Output tokens |
|---|---|---|
| claude-sonnet-4-5 | $3.00 / 1M tokens | $15.00 / 1M tokens |
| claude-haiku-3 | $0.25 / 1M tokens | $1.25 / 1M tokens |

### 13.2 Per-Message Cost by Context Window Size

The context window is the single largest cost lever. Each chat message includes: system prompt + user context block + conversation history + user message.

| Tier | Strategy | Approx tokens/message | Sonnet cost/msg |
|---|---|---|---|
| Free | Base profile only + last 5 msgs | ~5,000 input | ~$0.015 |
| Personal | Profile + check-ins (7d) + last 10 msgs | ~30,000 input | ~$0.090 |
| Premium | Full context: profile + wearables + last 20 msgs | ~80,000 input | ~$0.240 |

> The PRD currently specifies a 100k token budget for all tiers. **This is only viable for Premium.** Free and Personal tier must use reduced context windows or route to Haiku.

### 13.3 Monthly API Cost Per Active User

Assumes: average 2 AI messages/day for active users, 200 output tokens/response.

| User Type | Msgs/month | Model | Context | API cost/user/month |
|---|---|---|---|---|
| Free (casual) | 20 (plan limit) | Haiku | 5k tokens | ~$0.05 |
| Personal (moderate) | 60 | Sonnet (Personal context) | 30k tokens | ~$5.60 |
| Premium (heavy) | 150 | Sonnet (full context) | 80k tokens | ~$36.60 |
| Premium (light) | 30 | Sonnet (full context) | 80k tokens | ~$7.30 |

### 13.4 Break-Even Analysis

| Plan | Revenue/user/month | Max API cost/user (breakeven at 50% margin) | Max msgs at breakeven |
|---|---|---|---|
| Personal ($9.99) | $9.99 | $5.00 | ~55 msgs/month (Sonnet, 30k context) |
| Premium ($24.99) | $24.99 | $12.50 | ~50 msgs/month (Sonnet, 80k context) |

**Key finding:** At the currently specified 100k context window, a moderately active Premium user (~100 msgs/month) costs ~$24 in API fees alone — essentially the entire subscription price. **Context window strategy must be tiered by plan.**

### 13.5 Recommended Context Window Strategy (Revised)

| Tier | System prompt | User context block | Conversation history | Max total |
|---|---|---|---|---|
| Free | 15k (base prompt only) | 2k (Prakriti + Vikriti only) | Last 5 messages (~2k) | ~19k |
| Personal | 15k | 5k (profile + 7-day check-ins) | Last 10 messages (~5k) | ~25k |
| Premium | 15k | 8k (full context + wearables) | Last 20 messages (~10k) | ~33k |

This keeps Personal API cost at ~$1.50/user/month and Premium at ~$5/user/month for typical usage — healthy unit economics.

### 13.6 Other Infrastructure Cost Estimates (Phase 1 MVP)

| Service | Monthly cost (Phase 1) | Monthly cost (Phase 2 / 10k users) |
|---|---|---|
| Railway/Fly.io API | $20 | — (migrated to ECS) |
| AWS ECS Fargate | — | ~$200–400 |
| Database | $20 (Railway Postgres) | ~$150 (RDS Multi-AZ) |
| Redis | $0–10 (Upstash free tier) | ~$30 (ElastiCache) |
| AWS S3 | $5–15 | ~$30–50 |
| Anthropic API | Variable (see above) | Variable |
| Sentry | $26 (Team plan) | $26 |
| **Total (excl. AI)** | **~$80–100/month** | **~$450–650/month** |

### 13.7 Action Items Before Development

- [ ] **Decide context window per tier** (use §13.5 recommendation as starting point)
- [ ] **Implement Haiku routing for Free tier** — all Free tier chat uses claude-haiku-3
- [ ] **Add `tokens_used` tracking** to `messages` table and `usage_counters` — enables real cost monitoring
- [ ] **Set a monthly API budget alert** in Anthropic console from day one
- [ ] **Model cost at 1,000 Personal subscribers** before pricing decisions are finalised


---

## Appendix A: Error Codes

| Code | HTTP | Meaning |
|---|---|---|
| `INVALID_CREDENTIALS` | 401 | Wrong email or password |
| `EMAIL_NOT_VERIFIED` | 403 | Account exists but email not verified |
| `TOKEN_EXPIRED` | 401 | Access token expired; refresh needed |
| `INSUFFICIENT_PLAN` | 403 | Feature requires higher subscription tier |
| `USAGE_LIMIT` | 429 | Monthly usage limit reached for this feature |
| `RATE_LIMITED` | 429 | Too many requests; try again in {retryAfter} seconds |
| `IMAGE_QUALITY` | 422 | Uploaded image too low quality for analysis |
| `FILE_TOO_LARGE` | 413 | File exceeds maximum allowed size |
| `SCAN_LIMIT` | 403 | Monthly image scan limit reached |
| `RESOURCE_NOT_FOUND` | 404 | Requested resource does not exist |
| `PROTOCOL_CONFLICT` | 409 | Cannot activate; would exceed plan's active protocol limit |
| `ASSESSMENT_LOCKED` | 403 | Cannot retake Prakriti assessment yet (min 90 days) |
| `EMERGENCY_DETECTED` | 200 | AI detected emergency; standard response overridden |
| `AI_UNAVAILABLE` | 503 | Claude API unreachable; fallback or queue active |
| `SYNC_IN_PROGRESS` | 409 | Wearable sync already running for this device |

---

## Appendix B: Ayurvedic Concept Quick Reference

| Concept | Sanskrit | Meaning | Technical Role |
|---|---|---|---|
| Constitution | Prakriti | Immutable birth nature | Static DB record; basis for all personalization |
| Current State | Vikriti | Present imbalance | Dynamic DB record; updated by all data streams |
| Digestive Fire | Agni | Metabolic capacity | `agni_state` enum field on `user_current_state` |
| Toxins | Ama | Undigested residue | `ama_level` enum field; informed by tongue scans |
| Vital Essence | Ojas | Immunity + vitality | `ojas_level` 1–10 field; informed by HRV + sleep |
| Life Force | Prana | Vital energy | Qualitative; reflected in energy_level check-in |
| Air Element | Vata | Movement + nervous system | `vata_percentage` in constitution; `vata_imbalance` in state |
| Fire Element | Pitta | Transformation + metabolism | `pitta_percentage`; `pitta_imbalance` |
| Earth Element | Kapha | Structure + immunity | `kapha_percentage`; `kapha_imbalance` |
| Daily Routine | Dinacharya | Structured day rhythm | Lifestyle module; protocol recommendations |
| Seasonal Routine | Ritucharya | Seasonal adjustments | Context injected into AI per current season |
| Six Tastes | Shadrasas | Sweet/Sour/Salty/Pungent/Bitter/Astringent | Meal scan analysis; food database |
| Tissue Layers | Dhatus | 7 body tissues | Used in lab result interpretation (biomarker mapping) |
| Wellness Protocol | Chikitsa | Treatment/care plan | `protocols` table |

---

*Document Version: 1.0 | Phase 1 Deliverable | February 2026*
*Prepared as part of AyuAware Phase 1: Technical Scoping, Architecture Design & PRD Finalisation*
