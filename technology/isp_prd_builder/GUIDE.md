# isp_prd_builder — User Guide

**Version:** 1.0.0 | **Department:** Technology | **Output:** `<feature>_prd.md`

> Transforms a single-line idea into a complete, 16-section Product Requirements Document through structured dialogue.

---

## What it does

`isp_prd_builder` takes a one-sentence idea and builds a production-ready PRD by asking you targeted questions across five conversation rounds. It infers as much as possible from your input before asking — so you're never answering obvious questions. After gathering everything it needs, it drafts the full PRD, runs a 5-pass completeness review, and writes the final document to a file.

---

## How to use it

### Step 1 — Invoke the skill

Type your idea as a single line. You don't need a structured prompt. Examples:

```
write a PRD for a guest check-in status tracker
```
```
create a spec for bulk property export in admin
```
```
I want to build a WhatsApp notification when a booking is confirmed
```
```
draft requirements for letting guests upload their own ID documents
```

**Trigger phrases:** "write a PRD for", "create a spec for", "I want to build", "draft requirements for", "turn this idea into a PRD"

---

### Step 2 — Round 0: Idea intake (skill reads, you confirm)

The skill reads your idea and extracts what it can — surface (web/mobile/API), user type, action type, domain. It states its inferences and asks **only what it cannot figure out** — at most 3 questions.

**Example exchange:**

> **Skill:** Got it — this sounds like a new feature for guests on the web app in the notifications area. A few quick questions before I start:
> 1. Should this notification also go to the property manager, or only the guest?
> 2. Is there an existing notification system this plugs into, or is this greenfield?

> **You:** Both guest and property manager. We already have email notifications — this adds WhatsApp on top.

---

### Step 3 — Round 1: Problem context

The skill asks about the *why* — what problem this solves, what happens today without it, and whether there's a business goal or deadline driving it.

**What you'll be asked (only gaps):**
- What problem does this solve? What happens today without this?
- What triggers this feature? (user action, system event, scheduled job)
- Is there a metric this feature is expected to move?
- Is there a deadline or dependency driving the timing?

**Tip:** If your idea already names the problem, the skill confirms your framing instead of asking again.

---

### Step 4 — Round 2: Users and roles

The skill maps every actor who interacts with or is affected by this feature.

**What you'll be asked (only gaps):**
- Who are the primary users?
- Are there secondary users (people who receive output or are impacted)?
- Are there role-based permission differences?
- Does behaviour differ by user segment (e.g. free vs. paid)?

At the end of this round the skill reads back a one-line summary per role — confirm or correct before moving on.

---

### Step 5 — Round 3: Existing functionality and what changes

The skill establishes current state so the PRD clearly separates "what exists today" from "what is new."

**What you'll be asked (only gaps):**
- What does the current system do in this area?
- What parts of current behaviour are kept, modified, or removed?
- Could this change break other features that depend on the current behaviour?

At the end of this round the skill shows a **Today vs. After** two-column table. Confirm it is accurate before Round 4.

---

### Step 6 — Round 4: Scope and edge cases

The skill draws a hard boundary around what this PRD covers.

**What you'll be asked (only gaps):**
- What is the minimum viable version? What must be true to launch?
- What is explicitly out of scope for now?
- What are the important edge cases? (no data, network failure, special account types)
- Are there platforms or environments this does NOT need to support?
- Are there regulatory or compliance constraints?

At the end of this round the skill presents **In Scope / Out of Scope** lists. Confirm or add items before Round 5.

---

### Step 7 — Round 5: Acceptance criteria and dependencies

The skill defines what "done" looks like and maps everything the feature touches.

**What you'll be asked (only gaps):**
- How do we know this works? (specific, measurable conditions — not "it should work")
- What does this feature depend on upstream?
- What will this feature affect downstream?
- Which teams need to be involved or notified?
- Are there analytics events or tracking requirements?
- Are there performance, availability, or load targets?

**Note:** If you give a vague criterion like "it should be fast", the skill will ask once for a specific target (e.g. "delivered within 5 seconds of booking confirmation"). It will not loop on this.

---

### Step 8 — PRD generation and 5-pass review (automatic)

After Round 5 is complete you don't need to do anything. The skill:

1. Drafts the full 16-section PRD from all gathered information.
2. Runs five independent completeness passes internally:

| Pass | What it checks |
|------|---------------|
| Coverage | All 16 sections present and populated |
| Traceability | Every acceptance criterion links to a requirement; every requirement links to a story or goal |
| Specificity | All acceptance criteria are binary pass/fail; all NFRs have numeric targets |
| Scope integrity | Requirements and In-Scope list are consistent with each other |
| Consistency | User roles, actors, impacted areas, and dependencies all agree across sections |

Any check scoring below 3/5 is treated as a document defect and fixed before delivery.

---

### Step 9 — Receive the PRD

The skill writes the file and shows a delivery summary:

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

It then asks: *"Does this PRD reflect what you had in mind? Would you like to adjust any section, add detail, or resolve any open questions now?"*

---

## PRD structure — 16 sections

| # | Section | What it contains |
|---|---------|-----------------|
| 1 | Overview | One paragraph: what, why, who |
| 2 | Problem Statement | Problem, impact, root cause, success definition |
| 3 | Goals and Non-Goals | Measurable outcomes; explicit deferrals |
| 4 | User Roles | Role table: who, what they need, expected outcome |
| 5 | Existing Functionality | What the system does today in this area |
| 6 | Proposed Changes | What changes, what stays, what is removed |
| 7 | Functional Requirements | REQ-XX table with Must / Should / Could priority |
| 8 | Non-Functional Requirements | NFR-XX table with measurable targets |
| 9 | User Stories | As a [role], I want [action] so that [outcome] |
| 10 | Acceptance Criteria | Given / When / Then, binary pass/fail, linked to REQs |
| 11 | Scope | In Scope and Out of Scope lists |
| 12 | Impacted Areas | Systems, features, teams affected when this ships |
| 13 | Dependencies | Upstream (blockers) and Downstream (notifications) |
| 14 | Analytics & Tracking | Events, properties, owners |
| 15 | Open Questions | Unresolved items with owner and due date |
| 16 | Appendix | Assumptions and alternatives considered |

---

## Interaction rules (what to expect)

| Rule | What it means for you |
|------|----------------------|
| Max 3 questions per round | You'll never be hit with a wall of questions |
| Infer before asking | The skill states what it believes to be true; you confirm or correct |
| Never repeats a question | If you answered something in Round 1, it won't come up again in Round 3 |
| Acknowledges before moving on | After each round, the skill confirms what it understood — catch misunderstandings early |
| Accepts "I don't know" | TBD answers are logged as open questions; the skill moves on without looping |
| No PRD until Round 5 is done | The document is only drafted after all five rounds are complete |

---

## Common pitfalls to avoid

| Pitfall | Why it matters | What to do instead |
|---------|---------------|-------------------|
| Giving a vague idea with no context | More inference gaps = more questions | Add one sentence of context: who it's for and what problem it solves |
| Saying "it should just work" for acceptance criteria | Creates untestable requirements | Give a specific condition: "user receives WhatsApp within 30 seconds of booking" |
| Skipping the Today vs. After confirmation in Round 3 | PRD may describe a greenfield feature when it's really a modification | Review the two-column table carefully before confirming |
| Leaving all open questions as TBD | Blocks dev team decisions at implementation time | Resolve as many as you can during Round 5 or immediately after delivery |

---

## Example session (abbreviated)

```
You:      write a PRD for sending WhatsApp notifications when a booking is confirmed

Skill:    Got it — new notification for guests (and possibly property managers) 
          in the booking confirmation flow. Two quick questions:
          1. Should the notification go to the guest only, or also the property manager?
          2. Is there an existing notification system this adds on to, or is this new?

You:      Both. We already have email — this adds WhatsApp.

Skill:    [Round 1] I'm reading the problem as: guests currently only get email 
          confirmations, which has lower open rates than messaging apps. Is that right?

You:      Yes. We want to hit guests where they actually read messages.

...       [Rounds 2–5 continue]

Skill:    PRD ready
          ─────────────────────────────────────────
          File               : whatsapp_booking_confirmation_prd.md
          Sections           : 16 / 16
          Requirements       : 12 (Must: 8 | Should: 3 | Could: 1)
          Acceptance criteria: 9 (all measurable)
          Open questions     : 2
          
          Top decisions needed before development:
          1. Which WhatsApp Business API provider — Twilio or 360dialog?
          2. Should failed WhatsApp delivery fall back to SMS or email only?
          
          Does this PRD reflect what you had in mind?
```
