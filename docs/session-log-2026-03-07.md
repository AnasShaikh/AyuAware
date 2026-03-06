# AyuAware Session Log — 2026-03-07

## Context
Continuation of Anas's PRD refinement thread after Amy feedback, focused on closing the remaining intelligence-layer gap for Armand review readiness.

## Live PRD Sources
- Human PRD: http://89.117.52.159/ayu-mvp-prd.html
- Bot PRD: http://89.117.52.159/ayu-mvp-prd-bot.html
- Aliases synced: `/TEAM_COLLAB_HUB.html`, `/TEAM_COLLAB_HUB_BOT.html`

## Decisions Confirmed by Anas
- Canonical context keys (always included):
  - user profile
  - prakriti
  - latest vikriti
  - active protocol
  - recent check-ins
  - wearables snapshot
  - recent chat summary
  - environment exposure
- Check-in lookback: last 7 days.
- Conflict rule: manual user input wins.
- Missing context behavior:
  - continue partial + reduced confidence (for secondary context)
  - block and ask user (for required core context)
- Confidence thresholds: accepted as proposed.
- Screen-specific mandatory additions and fallback copy: generated and finalized from engineering context.

## Implemented in Live PRD
- Added **Base Context Assembly Contract (Canonical)** section under **Flows → Intelligence Prompt Architecture** in both human and bot pages.
- Added explicit subsections:
  - Conflict Resolution & Precedence
  - Missing Context Behavior
  - Confidence Thresholds
  - Screen-Specific Mandatory Additions (MVP)
  - User-Facing Safety Fallback Copy (v1)
- Verified NSL wording remains expanded:
  - `NSL (Nutrition, Supplements, Lifestyle)`.
- Verified roadmap state remains:
  - `330 Hours`
  - `$500 AI credits` marked as **Request**
  - rounded weeks column.
- Fixed bot-page structural mismatch:
  - `<details>` open/close count now balanced (4/4) for better crawler reliability.

## Amy Feedback Closure Status
- NSL definition: closed.
- Intelligence-layer contract clarity: closed with canonical context and behavior rules.
- Flow-hosting resilience: recommendation only (not blocker).

## Ready-to-Check Prompt
Use this to verify memory continuity in agent chat:

"Summarize AyuAware today: what Amy flagged, what was fixed, what remains before Armand review, with links to human and bot PRD."

