# AyuAware

**AI-Powered Ayurvedic Digital Health Companion**

AyuAware combines 5,000 years of Ayurvedic wisdom with modern AI to deliver personalized, continuously learning health guidance. At its core is the **Digital Twin** — a persistent AI model of each user built from their constitutional type (Prakriti), current health state (Vikriti), and real-time health data streams.

## What It Does

- **Prakriti Assessment** — 60-question onboarding to determine your Ayurvedic constitution (Vata/Pitta/Kapha)
- **Live Health Tracking** — Wearables, daily check-ins, visual diagnostics (tongue/meal/skin scans), lab uploads, and manual logs continuously update your health profile
- **Personalized Protocols** — AI-generated wellness plans (diet, herbs, lifestyle, yoga) dynamically adjusted based on adherence and new data
- **Proactive Alerts** — Detects imbalances before symptoms manifest
- **Ayurvedic Education** — Contextual learning content tied to your constitution and current state
- **Supplement Shop** — Curated Ayurvedic products matched to your profile

## Tech Stack

| Layer | Technology |
|---|---|
| Mobile | React Native (iOS first, Android post-MVP) |
| Backend | Node.js / NestJS — RESTful API |
| AI | Claude API (Anthropic) |
| Database | PostgreSQL + pgvector |
| Cloud | AWS (HIPAA-eligible) |
| Health Data | Apple HealthKit (MVP), Oura & WHOOP (V2) |

## Project Structure

```
docs/
  tech_prds/          # Technical PRDs per module (Onboarding, Nutrition, Health, etc.)
  uiux_prds/          # UI/UX PRDs per module
  netlify/            # Interactive HTML documentation
  AyuAware - Final Technical PRD.md          # Source of truth for development
  AyuAware - Backend Architecture Overview.md # Two-layer data model & backend flows
  AyuAware - Product Requirements Document.md # Complete product specification
```

## Status

**Phase 1 Complete** — Technical scoping, architecture design, database schema, and PRD finalization.

Currently in pre-development. All documentation and specifications are finalized and ready for MVP implementation.

## License

Proprietary. All rights reserved.
