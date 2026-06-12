---
name: isp-prd-builder
description: 'Build a comprehensive Product Requirements Document from a single line of idea or requirement through structured interactive dialogue. Asks targeted questions across five conversation rounds — problem context, user roles, existing vs. new behaviour, scope, and acceptance criteria — then generates a full PRD covering existing functionality, proposed changes, user roles, acceptance criteria, scope, out of scope, impacted areas, and dependencies. Runs a 5-pass completeness review before producing the final document. Use when the user has an idea, feature request, or single-sentence requirement and wants a production-ready PRD. Trigger on: "write a PRD for", "create a spec for", "I want to build", "draft requirements for", "turn this idea into a PRD", or any single-line description of a feature or product change.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP PRD Builder

This skill transforms a single line of idea or requirement into a comprehensive, production-ready PRD through five rounds of targeted dialogue. It asks only what it cannot already infer, adapts follow-up questions to previous answers, and never asks the same thing twice. The final document is reviewed across five completeness passes before being presented.

**Output:** `<feature>_prd.md`

---

## How this skill works

1. User provides a single line — an idea, feature request, or rough requirement.
2. Skill runs five conversation rounds, each focused on a different dimension of the PRD.
3. After all rounds, skill drafts the full PRD.
4. PRD is reviewed in five completeness passes.
5. Final document is written to a file and presented.

This is an **interactive** skill. Wait for user responses between rounds. Do not batch all questions into one message.

---

## Round 0 — Idea intake and first read

Read the user's input carefully before asking anything.

Extract whatever can be inferred directly:
- Surface (web, mobile, API, internal tool, etc.)
- Probable user type (end customer, internal team, admin, etc.)
- Action type (new feature, modification to existing, removal, integration)
- Domain (booking, payments, notifications, content, auth, etc.)

Then ask **only the questions that cannot be inferred**. Never ask more than **three questions per round**. If you can infer something with reasonable confidence, state your inference and ask the user to confirm or correct — do not ask an open question.

Example opener:
> "Got it — this sounds like a new feature for [inferred user type] in the [inferred domain] area. A few quick questions before I start:
> 1. [Most critical missing piece]
> 2. [Second most critical]"

---

## Round 1 — Problem context

Goal: Understand *why* this is being built and what problem it solves.

Ask (only what is not already clear):
- What problem does this solve for the user? What happens today without this feature?
- What is the trigger or entry point for this feature? (e.g., user action, system event, scheduled job)
- Is there a business goal or metric this feature is expected to move? (e.g., conversion rate, support ticket reduction, time savings)
- Is there a deadline, launch date, or dependency that is driving the timing?

**Inference rule:** If the idea already names the problem (e.g., "users can't export their data"), skip the "what problem does this solve" question and confirm instead: "I'm reading the problem as X — is that right?"

After receiving answers: acknowledge what you've understood, state any inferences you've made, and transition to Round 2.

---

## Round 2 — Users and roles

Goal: Identify every actor who interacts with or is affected by this feature.

Ask (only what is not already clear):
- Who are the primary users of this feature? (e.g., guests, property managers, ops team, admins)
- Are there secondary users — people who receive output from this feature or are affected by it?
- Are there any role-based permission differences? (e.g., admin can do X but regular user cannot)
- Does this feature behave differently for different user segments? (e.g., free vs. paid, new vs. returning)

For each identified role, capture: **who they are**, **what they need to do**, and **what outcome they expect**.

After receiving answers: confirm the role list back to the user in one line per role before moving on.

---

## Round 3 — Existing functionality and what changes

Goal: Establish the current state so the PRD clearly separates "what exists today" from "what is new or different."

Ask (only what is not already clear):
- What does the current system do in this area today? (Even if the answer is "nothing" — confirm that.)
- What parts of the current behaviour should be **kept unchanged**?
- What parts of the current behaviour are being **replaced or modified**?
- Are there any current behaviours that are **intentionally being removed**?
- If this is a new area with no existing functionality, confirm: "Is there truly nothing in the current system related to this, or is there something adjacent I should account for?"

**Regression awareness:** If the user describes existing behaviour that is being modified, ask: "Are there other features or flows that depend on this existing behaviour that could break?"

After receiving answers: write a two-column summary — "Today" vs. "After this feature" — and ask the user to confirm it is accurate before Round 4.

---

## Round 4 — Scope, out of scope, and edge cases

Goal: Draw a hard boundary around what this PRD covers and what it explicitly does not.

Ask (only what is not already clear):
- What is the minimum viable version of this feature? What must be true for it to launch?
- Are there related things that would be *nice to have* but are explicitly out of scope for now?
- What are the important edge cases? (e.g., what happens if the user has no data, if a network call fails, if the user has a special account type)
- Are there any platforms, devices, or environments this feature does NOT need to support?
- Are there any regulatory, legal, or compliance constraints? (e.g., GDPR, data retention, financial regulations)

After receiving answers: present the scope boundary as two lists — "In scope" and "Out of scope" — and ask the user to confirm or add to them.

---

## Round 5 — Acceptance criteria, dependencies, and impacted areas

Goal: Define what "done" looks like and what else in the system is touched.

Ask (only what is not already clear):
- How do we know this feature is working correctly? What are the specific, measurable conditions that must be true? (Push for specifics: numbers, states, user actions — not "it should work".)
- Which other features, systems, or services does this depend on? (Upstream dependencies — things that must exist or be changed first.)
- Which other features, systems, or services will be affected when this ships? (Downstream impacts — things that may break or change behaviour.)
- Which teams or stakeholders need to be aware of or involved in this? (e.g., backend, design, data, legal, customer support)
- Are there any analytics or tracking requirements? (Events to fire, metrics to report)
- Are there any non-functional requirements? (Performance targets, availability SLAs, load expectations)

After receiving answers: confirm the dependency list and impacted areas before moving to PRD generation.

---

## PRD generation

Using all information gathered in rounds 0–5, generate the full PRD. Structure:

---

```markdown
# [Feature Name] — Product Requirements Document

**Author:** [from context or "TBD"]
**Date:** [today]
**Version:** 0.1 — Draft
**Status:** In Review
**Feature area:** [domain]

---

## 1. Overview

One paragraph describing what this feature is, why it exists, and who it is for.

---

## 2. Problem Statement

**Problem:** [What exists today that is broken, missing, or suboptimal]
**Impact:** [Who is affected and how — quantified where possible]
**Root cause:** [Why this problem exists]
**Success looks like:** [What will be true when this is solved]

---

## 3. Goals and Non-Goals

### Goals
- [Measurable outcome 1]
- [Measurable outcome 2]

### Non-Goals
- [What this feature explicitly does not aim to achieve]
- [What is deferred to a future version]

---

## 4. User Roles

| Role | Description | What they need | Expected outcome |
|------|-------------|---------------|-----------------|
| [Role 1] | ... | ... | ... |
| [Role 2] | ... | ... | ... |

---

## 5. Existing Functionality

Description of what the system does today in this area.

| Area | Current behaviour |
|------|------------------|
| [Component / flow] | [What it does today] |

*If no existing functionality: "This is a new capability with no current equivalent in the system."*

---

## 6. Proposed Changes

### What changes
| Area | Current behaviour | New behaviour |
|------|------------------|---------------|
| [Component / flow] | [Today] | [After this feature] |

### What stays the same
- [Existing behaviour 1 that is explicitly preserved]
- [Existing behaviour 2 that is explicitly preserved]

### What is removed
- [Existing behaviour that is intentionally removed, if any]

---

## 7. Functional Requirements

Numbered list. Each requirement is stated as: **[REQ-XX]** [Actor] [action] [outcome] [condition].

| REQ-ID | Requirement | Priority | Notes |
|--------|-------------|----------|-------|
| REQ-01 | [Actor] shall [action] so that [outcome] | Must / Should / Could | |

Priority scale: **Must** (launch blocker) / **Should** (strongly desired) / **Could** (nice to have)

---

## 8. Non-Functional Requirements

| NFR-ID | Category | Requirement | Measurement |
|--------|----------|-------------|-------------|
| NFR-01 | Performance | [e.g., page loads within 2 s at P95] | P95 load time ≤ 2000 ms |
| NFR-02 | Availability | ... | ... |
| NFR-03 | Security | ... | ... |

---

## 9. User Stories

Format: "As a [role], I want to [action] so that [outcome]."

| Story ID | Role | Action | Outcome | Linked REQ |
|----------|------|--------|---------|------------|

---

## 10. Acceptance Criteria

Each criterion is specific, measurable, and binary (pass / fail).

| AC-ID | Criterion | Linked REQ | Verification method |
|-------|-----------|------------|---------------------|
| AC-01 | Given [context], when [action], then [outcome] | REQ-01 | Manual test / automated test |

---

## 11. Scope

### In Scope
- [Explicit item 1]
- [Explicit item 2]

### Out of Scope
- [Explicit exclusion 1 — reason]
- [Explicit exclusion 2 — reason]

---

## 12. Impacted Areas

Systems, features, and teams that will be affected when this ships.

| Area | Type of impact | Severity | Owner | Action required |
|------|---------------|----------|-------|----------------|
| [System / feature / team] | Breaking / Behaviour change / Data change / UI change | High / Medium / Low | [Team] | [What needs to happen] |

---

## 13. Dependencies

### Upstream (must exist or be completed before this ships)
| Dependency | Type | Owner | Status | Blocker? |
|------------|------|-------|--------|----------|

### Downstream (will be affected when this ships)
| Dependency | Type | Owner | Notification needed? |
|------------|------|-------|----------------------|

---

## 14. Analytics and Tracking

| Event name | Trigger | Properties | Owner |
|------------|---------|------------|-------|

*If none: "No new tracking events required."*

---

## 15. Open Questions

| # | Question | Owner | Due date | Resolution |
|---|----------|-------|----------|------------|

---

## 16. Appendix

### Assumptions
- [ASSUMPTION] [Statement assumed to be true, not confirmed]

### Alternatives considered
- [Alternative approach 1] — rejected because [reason]
```

---

## 5-pass completeness review

After generating the draft PRD, run five independent completeness passes before presenting it. In each pass, check:

1. **Coverage:** Are all 16 sections present and populated? Any section that is empty (other than legitimately N/A) is a gap.
2. **Traceability:** Does every Acceptance Criterion link to at least one REQ? Does every REQ trace to a user story or goal?
3. **Specificity:** Are all acceptance criteria binary pass/fail? Are NFRs measurable (numbers, not adjectives like "fast" or "reliable")?
4. **Scope integrity:** Is there anything described in the requirements that is not listed in the In-Scope section, or vice versa?
5. **Consistency:** Do the user roles in section 4 match the actors in the requirements and user stories? Do the impacted areas in section 12 align with the dependencies in section 13?

**Convergence tally:**

| Check | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Pass 5 | Score | Status |
|-------|--------|--------|--------|--------|--------|-------|--------|
| All sections present | | | | | | /5 | |
| Full traceability | | | | | | /5 | |
| All criteria measurable | | | | | | /5 | |
| Scope integrity | | | | | | /5 | |
| Internal consistency | | | | | | /5 | |

Any check that scores below 3/5 is a **document defect** — fix it before presenting the file.

---

## Final output

Write the PRD to `./<feature>_prd.md`. Then confirm to the user:

```
PRD ready
──────────────────────────────────────────────────
File            : <feature>_prd.md
Sections        : 16 / 16
Requirements    : N (Must: X | Should: X | Could: X)
Acceptance criteria: N (all measurable)
Open questions  : N

Top decisions needed before development can begin:
1. [Most critical open question]
2. [Second most critical]
```

Ask: "Does this PRD reflect what you had in mind? Would you like to adjust any section, add detail, or resolve any of the open questions now?"

---

## Feature context save

After confirming the PRD with the user, save a compact context file so downstream skills (tech specs, test cases) can pick up this work without re-briefing.

**Derive the feature slug** from the PRD filename: lowercase, hyphens for spaces.
`whatsapp_booking_confirmation_prd.md` → `whatsapp-booking-confirmation`

Write to `team-memory/features/<feature-slug>/prd-context.md`:

```markdown
---
feature: <feature-slug>
skill: isp-prd-builder
date: <today>
output_file: <feature>_prd.md
---

## Problem statement
[One sentence from Section 2 — the core problem this feature solves]

## User roles
[Bullet per role: **Role name** — one-line description of what they need]

## In scope
[Bullet list from Section 11 — In Scope]

## Out of scope
[Bullet list from Section 11 — Out of Scope]

## Must requirements
[REQ-ID — one-line description, for all Must-priority items from Section 7]

## Key acceptance criteria
[AC-ID — criterion, for all P1 items from Section 10]

## Open questions
[All unresolved items from Section 15 — question, owner, impact of leaving unresolved]

## Impacted areas
[High-severity rows from Section 12 — area, type of impact, owner]

## Upstream dependencies
[Blocking items from Section 13 — what must exist before this ships]
```

Then confirm: `Feature context saved → team-memory/features/<feature-slug>/prd-context.md`

---

## Interaction rules

- **Ask at most 3 questions per round.** More than three questions in one message causes decision fatigue.
- **Infer before asking.** State what you've inferred and ask for confirmation. Do not ask open questions about things you can reasonably deduce.
- **Never ask the same thing twice.** If an earlier answer already covered something, reference that answer instead of re-asking.
- **Acknowledge before moving on.** After each round, briefly confirm what you've understood before asking the next set of questions. This catches misunderstandings early.
- **Accept partial answers.** If the user says "I don't know" or "TBD", note it as an open question and move on. Do not loop on unanswered questions.
- **Push for specificity on acceptance criteria.** If the user says "it should be fast" or "it should work correctly", ask: "Can you give me a specific target? For example, loads in under 2 seconds, or handles 500 concurrent users?" Do this exactly once per vague criterion.
- **Do not start writing the PRD until Round 5 is complete.** Premature drafting leads to documents that miss key context gathered in later rounds.

---

## Common mistakes

| Mistake | Why it fails | Fix |
|---------|-------------|-----|
| Asking all questions in one message | Overwhelms the user; answers are shallow | Maximum 3 questions per round |
| Writing the PRD before Round 5 | Misses dependencies, impacted areas, acceptance criteria | Always complete all 5 rounds first |
| Accepting vague acceptance criteria | Creates untestable requirements | Push for measurable conditions exactly once |
| Skipping "existing functionality" | PRD looks like a greenfield feature when it's actually a modification | Always establish current state in Round 3 |
| Treating "out of scope" as optional | Scope creep starts in the PRD | Out-of-scope items are as important as in-scope items |
| Leaving open questions unanswered | Blocks implementation decisions | Flag all TBDs clearly; note the owner and impact of leaving them unresolved |
