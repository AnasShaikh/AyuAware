# AyuAware — Team Exchange: Figma Prototype Feedback

**Date:** February 27 – March 3, 2026
**Participants:** Anas Shaikh, Shiv Khanna, Nikhel K Mahajan, Armand
**Subject:** Figma Prototype Review & Clarifications

---

## Figma Prototype Link

https://www.figma.com/design/ZcQkSKWkfzN9mMkCh30bvJ/AyuAware--Copy-?node-id=343-293&p=f&t=dAUSEMsz0FTM1Cla-0

---

## Questions Raised (Anas) & Responses (Shiv)

### 1. Login form missing (Email login + success screen)
**Response:** Yes, let's add these.

### 2. Screen flow — sequential arrangement, arrows & labels needed
**Response:** Yes, screens are sequentially arranged to the right. Updated Figma with arrows to clearly define the flow will be sent.

### 3. Where are all 50 Prakriti questions?
**Response:** 18 questions exist at the moment, will expand to 50 later. The 18 questions will be sent separately by email.

### 4. Onboarding leads to Today screen — will we have enough data?
**Response:**
- All users **MUST connect a wearable device** during onboarding.
- AyuAware is wearable-agnostic — uses **Spike** as a data aggregator for biometric data.
- We have access to **30–90 days of historic wearable data** when the user connects their device.
- That provides sufficient longitudinal data for an insightful Today screen on first load.

### 5. "Complete Full Assessment" button — screen not found
**Response:** Shiv hasn't seen this either. Nikhel to provide insight.

### 6. No clear formula for Manas and Prana calculations
**Response:** Still needs to be worked on. (Previously discussed on WhatsApp — not yet finalized.)

### 7. Nidra without wearable — fallback screen needed
**Response:** All users MUST connect wearable devices — that is the only way to provide regular insights and solutions based on biometric data. *(No separate fallback screen needed.)*

### 8. Astrology reports — what input data is needed?
**Response:**
- Usually: **date of birth, place of birth, sex**. May be other factors.
- Will study further and get back.
- Will need to build a sophisticated prompt that includes all relevant input parameters to create personalized Ayurvedic NSL outputs based on astro movements.

---

## Key Decisions / Takeaways

- **Wearable is mandatory** at onboarding — eliminates "no data" fallback screens
- **Spike** is the wearable data aggregator (not direct HealthKit/Oura/WHOOP integration)
- **Manas & Prana formulas** — still undefined, needs collaborative design
- **Astrology inputs** — DOB, place of birth, sex (minimum) — needs further research
- **Prakriti quiz** — starting with 18 questions, expanding to 50 later
- **Login screens** — need to be added to Figma
- **Flow arrows** — Figma update incoming for clearer navigation

---

## Next Steps

- **Call scheduled:** Thursday, March 5, 2026 (time TBD via WhatsApp)
- Agenda: Development strategy discussion
- Anas may have additional Qs after further review of the Figma
