---
name: isprava-context
description: Ongoing platform decisions, architecture constraints, and active initiatives the whole team should know before starting any technical session
metadata:
  type: project
  updated: 2026-05-25
---

# Isprava Platform Context

Shared context about the Isprava platform that Claude should apply when helping with any technical work.

**Why:** Prevents repeated onboarding, avoids suggestions that conflict with known constraints.
**How to apply:** Read this before planning any feature, PRD, or gap analysis in the Isprava codebase.

---

## Platform overview

Isprava is a luxury villa rental and property management company. The platform serves three primary actors:
- **Guests** — book and stay at Isprava properties
- **Property Managers** — manage individual properties, availability, and guest experience
- **Ops / Admin team** — internal team that manages the platform, bookings, and operations

---

## Active constraints

| Constraint | Detail | Impact on suggestions |
|------------|--------|----------------------|
| *(Add constraints here)* | | |

---

## Active initiatives

| Initiative | Status | Owner | Notes |
|------------|--------|-------|-------|
| *(Add active projects here)* | | | |

---

## Architecture decisions

| Decision | Rationale | Date |
|----------|-----------|------|
| *(Add architectural decisions here)* | | |

---

## Known integrations

| System | Purpose | Notes |
|--------|---------|-------|
| WhatsApp Business API | Guest and property manager notifications | Being added on top of existing email notifications |
| *(Add other integrations)* | | |

---

## How to update this file

Add a row to the relevant table. Include the date for time-sensitive entries (active initiatives, constraints). Commit with message: `docs(team-memory): update isprava-context — [what changed]`
