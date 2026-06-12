---
name: project-planning
description: 'Plan construction projects from pre-construction through handover. Use when the user mentions "construction schedule", "project plan", "work breakdown structure", "WBS", "Gantt chart", "construction programme", "project milestones", "pre-construction planning", "project kickoff", "scope of works", or "project timeline". Also trigger when identifying project risks, sequencing trades, or planning a construction tender. For day-to-day site operations, see site-inspection. For safety planning, see safety-compliance.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: construction
---

# Construction Project Planning Skill

A structured framework for planning construction projects that deliver on time, on budget, and to specification. Great project planning eliminates surprises by anticipating constraints, sequencing work correctly, and building buffers where they matter — before ground is broken.

## Core Principle

**Plan the work, then work the plan — but plan for what can go wrong.** Every day of planning saves three days of rework. The best construction plans are not rigid schedules; they are decision frameworks that guide the team when reality deviates from the plan (and it always does).

## Scoring

**Goal: 10/10.** When reviewing or building a project plan, rate 0–10 based on completeness of scope, realism of timeline, identification of critical path, risk mitigation, and stakeholder alignment. A 10/10 means the team can execute the project from this plan without ambiguity.

## Planning Framework

### 1. Project Definition & Scope

**Core concept:** Establish a clear, agreed scope of works before any scheduling begins.

**Why it matters:** Scope creep is the #1 cause of budget blowouts and delays. A clear scope is the contract between the team and the client.

**Scope document must-haves:**
- Description of all works included (what we are building)
- Explicit exclusions (what we are NOT doing)
- Contract type (lump sum, cost-plus, schedule of rates)
- Client-supplied items and client responsibilities
- Design status — what is confirmed vs. still in development
- Regulatory requirements (permits, inspections, council approvals)

**Scope creep prevention:**
- All scope changes go through a formal variation process
- No verbal instructions to proceed on additional work without written sign-off
- Hold weekly scope review with client to surface emerging changes early

### 2. Work Breakdown Structure (WBS)

**Core concept:** Decompose the total scope into a hierarchical list of all work packages required to complete the project.

**Why it matters:** You cannot schedule or cost what you haven't defined. The WBS is the backbone of the schedule and budget.

**WBS structure (example — commercial fit-out):**

```
1.0 Pre-Construction
  1.1 Design finalization
  1.2 Permits and approvals
  1.3 Procurement (long-lead items)
2.0 Strip-out & Demolition
  2.1 Asbestos survey and removal
  2.2 Strip-out of existing fit-out
  2.3 Structural demolition
3.0 Structure & Civil
  3.1 Concrete works
  3.2 Steel works
4.0 Services (MEP)
  4.1 Mechanical (HVAC)
  4.2 Electrical
  4.3 Plumbing & hydraulics
  4.4 Fire services
5.0 Finishes
  5.1 Partitions and ceilings
  5.2 Flooring
  5.3 Painting
  5.4 Joinery
6.0 Commissioning & Handover
  6.1 Services commissioning
  6.2 Defects inspection
  6.3 Practical completion
  6.4 As-built documentation
```

### 3. Programme (Schedule)

**Core concept:** A realistic, sequenced schedule that shows every work package, its duration, and its dependencies.

**Why it matters:** A programme without dependencies is a wish list, not a schedule.

**Programme development steps:**
1. List all activities from the WBS
2. Estimate duration for each activity (with input from trades)
3. Define dependencies (what must finish before this can start)
4. Identify the critical path — the longest sequence of dependent activities
5. Apply resources to confirm durations are achievable
6. Add float to non-critical activities and contingency to critical path

**Programme types by project phase:**

| Type | Detail Level | Use Case |
|------|-------------|----------|
| Master Programme | Level 1–2 (milestones) | Client reporting, contract baseline |
| Construction Programme | Level 3 (work packages by week) | Day-to-day team execution |
| 3-Week Lookahead | Level 4 (tasks by day) | Trade coordination, material delivery |

**Critical path rule:** Any delay on a critical path activity delays the whole project. Protect the critical path above everything else.

See: [references/programme-template.md](references/programme-template.md)

### 4. Resource & Procurement Planning

**Core concept:** Ensure the right people, materials, and equipment are available when the programme requires them.

**Why it matters:** The most common cause of schedule delays is a resource that was assumed to be available but wasn't.

**Key practices:**
- Identify long-lead procurement items early (structural steel, specialist equipment, imported materials) — order these before construction starts
- Confirm subcontractor availability against the programme before awarding contracts
- Build a material delivery schedule tied to the programme
- Resource-load the programme to identify over-allocation of trades
- Maintain a preferred subcontractor list with capacity and lead times

### 5. Risk Register

**Core concept:** Identify, assess, and plan responses to the project's top risks before they become problems.

**Why it matters:** Every project has risks. Teams that identify risks early have options; teams that find risks late have crises.

**Risk register structure:**

| Risk | Likelihood (1–5) | Impact (1–5) | Score | Owner | Mitigation | Contingency |
|------|-----------------|-------------|-------|-------|-----------|------------|
| Design not complete at construction start | 4 | 5 | 20 | PM | Freeze design by [date] | Prioritize confirmed areas first |
| Key subcontractor unavailable | 3 | 4 | 12 | PM | Secure backup sub | Re-sequence programme |
| Adverse weather | 2 | 3 | 6 | Site Manager | Buffer in programme | Covered work areas |
| Latent conditions (unknown site conditions) | 3 | 4 | 12 | PM | Pre-start site investigation | Provisional sum in contract |

**Risk score threshold:**
- 15–25: Critical — active mitigation required
- 8–14: High — monitor weekly
- 1–7: Low — monitor monthly

### 6. Stakeholder & Communication Plan

**Core concept:** Define who needs what information, when, and how.

**Why it matters:** Poor communication is cited in over 60% of construction disputes.

**Communication plan:**

| Stakeholder | Information Needed | Frequency | Format | Owner |
|------------|-------------------|-----------|--------|-------|
| Client | Progress, cost, issues | Weekly | Progress report + meeting | PM |
| Head contractor | Programme, RFIs, variations | Daily | Site meetings + written | PM |
| Subcontractors | 3-week lookahead, site instructions | Weekly | Coordination meeting | Site Manager |
| Design team | RFIs, design clarifications | As needed | Formal RFI register | PM |
| Authority / Inspector | Inspection hold points | Per programme | Formal notice | Site Manager |

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Starting construction before design is complete | Constant rework as design changes | Design freeze milestone before construction programme is locked |
| Programme without dependencies | Can't see critical path or float | Build the programme in scheduling software with logic links |
| No risk register | Surprises become crises | Complete a risk register at the end of pre-construction |
| Long-lead items ordered late | Delays critical path | Identify and order long-lead items in pre-construction |
| Communication plan is verbal | Stakeholders get different information | Write the communication plan; make it part of the contract |

## Quick Diagnostic

| Question | If No | Action |
|----------|-------|--------|
| Is the scope of works fully documented and signed off? | Scope creep risk | Complete scope document before mobilising |
| Is the programme logic-linked with a visible critical path? | Schedule is unreliable | Rebuild the programme in scheduling software |
| Are long-lead items identified and ordered? | Critical path delay risk | Audit procurement status against the programme |
| Is there a risk register with mitigations? | No early warning system | Complete risk register in the next planning session |

## Reference Files

- [references/programme-template.md](references/programme-template.md) — Master programme template (Excel/MS Project format)
