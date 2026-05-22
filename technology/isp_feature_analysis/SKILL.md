---
name: isp_feature_analysis
description: Run a structured, interactive gap analysis between a Product Requirements Document (PRD), Figma designs, the current production UI, and a target code repository — then produce a complete implementation plan (checklist, test cases, technical specs) as a single Markdown deliverable. Use this skill whenever the user mentions analyzing a PRD against Figma, comparing designs to current state, planning a redesign or feature rollout, building an implementation checklist from a spec, defining test cases for a redesign, or scoping work in a repo from product/design inputs — even if they don't explicitly say "gap analysis". Trigger on phrases like "analyze the PRD", "gaps between PRD and Figma", "implementation plan from this spec", "redesign analysis", "checklist for this feature", or any combination of PRD + Figma + repo references in one request.
license: proprietary
metadata:
  author: your-org
  version: "1.1.0"
  department: technology
---

# PRD ↔ Figma Gap Analysis & Implementation Planning

This skill guides Claude through a rigorous, interactive analysis when a user provides product/design inputs (PRD, Figma, current-state screenshots) and wants a complete implementation plan grounded in a real codebase.

The output is a single, standalone Markdown file containing: gap analysis, open questions, an implementation checklist, test cases, and technical specs.

---

## When to use this skill

Trigger on requests that combine **two or more** of these:
- A PRD or spec document (`.md`, `.docx`, `.pdf`, Confluence/Notion link)
- Figma links or design references
- Screenshots / references of the current live page
- A code repository to ground implementation in

Example user phrasings: "analyze gaps between PRD and Figma", "plan the implementation for this redesign", "make a checklist from this spec", "compare current vs new design and tell me what to build".

If the user provides only one input (e.g., just a PRD with no design, or just Figma with no repo), still proceed — but flag the missing dimension as the **first gap** and ask whether to continue with placeholders or pause.

---

## Workflow (run in order — do not skip phases)

This is an **interactive** skill. After each phase, share the output with the user and confirm before moving on. If the user says "just do the whole thing", batch phases 2–7 and present the final deliverable, but still run Phase 1 (intake) interactively.

### Phase 1 — Intake & confirmation

Gather and confirm these inputs before doing any analysis:

| Input | Required? | How to handle if missing |
|---|---|---|
| Project / repo name | Yes | Ask |
| Feature / page name | Yes | Ask |
| PRD location | Strongly preferred | Ask, or proceed with "no PRD — Figma is source of truth" |
| Figma link(s) | Strongly preferred | Ask, or proceed with "no Figma — PRD is source of truth" |
| Current-state references | Optional | Skip Phase 4 if absent |
| Repo path / branch | Strongly preferred | Ask, or produce framework-agnostic specs |
| Output filename | No | Default to `<feature>_analysis.md` |

Read whatever files have been provided **before** asking clarifying questions — many answers will already be in the PRD. For `.docx` files use the docx skill; for `.pdf` use pdf-reading; for images use image viewing directly.

End Phase 1 by echoing back a short "Confirmed inputs" block and asking the user to confirm before proceeding.

### Phase 2 — PRD analysis

Extract every requirement from the PRD and classify each into:
- **Functional** (what it does)
- **Non-functional** (perf, scale, security)
- **UI/UX** (visual + interaction)
- **Content** (copy, microcopy, localization)
- **Analytics / tracking** (events, properties)
- **SEO / metadata**
- **Accessibility** (WCAG level, specific a11y requirements)
- **Out of scope** (explicitly excluded)

For each requirement, capture:
- A short ID (e.g., `REQ-01`)
- One-line summary
- Acceptance criteria (if stated)
- **Ambiguity flag** if vague, unmeasurable, or contradicted elsewhere

Output as a table. Anything not measurable becomes an open question for Phase 5.

### Phase 3 — Figma analysis

Enumerate everything visible in the new design:
- Components and their states (default, hover, loading, error, empty, disabled)
- Breakpoints covered (mobile, tablet, desktop — and which sizes specifically)
- Typography, spacing, color tokens — note any deviations from the existing design system
- Interactions (animations, transitions, gestures)
- Edge cases the design accounts for (long text, missing images, etc.)

If you cannot access the Figma directly, ask the user to paste relevant frames as images or to describe sections — then proceed with what's available and mark the rest as "needs design review".

### Phase 4 — Current-state analysis

For each provided current-state reference (desktop, responsive, etc.):
- Describe what exists today
- Classify each component as: **Keep**, **Modify**, **Replace**, **Remove**, **New**
- Note any current behavior that may be intentional but is missing from the new design (potential regressions)

Skip this phase if no current-state references were provided, but flag it as a recommended follow-up.

### Phase 5 — Gap analysis (three-way comparison)

This is the core deliverable. Produce a table:

| # | Requirement / Element | PRD | Figma | Current | Gap Type | Severity | Owner | Notes |
|---|----------------------|-----|-------|---------|----------|----------|-------|-------|

- **Gap Type:** `Missing-in-PRD`, `Missing-in-Figma`, `Missing-in-Current`, `Conflict`, `Ambiguous`, `Out-of-Scope`, `Regression-Risk`
- **Severity:** `Blocker` / `High` / `Medium` / `Low`
- **Owner:** `Product`, `Design`, `Engineering`, `QA` — who needs to resolve it

Follow the table with an **Open Questions** section — one bullet per ambiguity, phrased as a direct question to the right owner.

### Phase 6 — Implementation checklist

A developer-actionable, atomic checklist. Organize by:
- Components / modules (with proposed file paths if a repo was provided)
- API / backend changes
- State management
- Routing
- Responsive breakpoints
- Accessibility (specific WCAG checks, not just "be accessible")
- Analytics events (name, properties, trigger)
- SEO / metadata
- Feature flags / rollout
- Documentation updates

Every item uses `- [ ]` syntax. Items should be small enough that a single PR could close several of them.

### Phase 7 — Test cases

Use this table format:

| TC ID | Title | Preconditions | Steps | Expected Result | Type | Priority | Linked Req |
|-------|-------|---------------|-------|-----------------|------|----------|------------|

Cover all of: unit, integration, E2E, visual regression, responsive (per breakpoint), accessibility (keyboard nav, screen reader, contrast), and edge cases (slow network, empty states, error states, very long content, RTL if applicable). Every TC must link back to at least one `REQ-XX` or checklist item.

### Phase 8 — Technical specs

Grounded in the actual repo (read it before writing these — don't invent patterns):
- File-level change list: new files, modified files, deletions, with proposed paths
- Component hierarchy and props contracts
- Data fetching strategy and API contracts (request / response shapes)
- State management approach **consistent with existing repo conventions**
- Reusable utilities, hooks, or design-system additions
- Migration / backward-compatibility plan
- Risks and mitigations
- Effort estimate per spec item: `S` / `M` / `L` / `XL`

If no repo was provided, produce framework-agnostic specs and note this explicitly.

### Phase 9 — Effort Estimates

Produce three independent estimates for the full implementation scope derived from Phase 6 (checklist) and Phase 8 (technical specs). Do not invent numbers — base every figure on the actual checklist items and complexity signals found in the repo and PRD.

---

#### Estimation inputs (collect before computing)

| Signal | Where to find it |
|--------|-----------------|
| Number of checklist items, classified by complexity tier (see below) | Phase 6 |
| Number of new vs modified vs deleted files | Phase 8 file-level change list |
| Presence of API contracts, data-model changes, or migrations | Phase 8 |
| Number of test cases, broken down by type | Phase 7 |
| Ambiguity count (open questions still unresolved) | Phase 5 |
| Repo familiarity signals (consistent conventions vs messy/undocumented) | Phase 8 inspection |

#### Complexity tiers for checklist items

| Tier | Description | Examples |
|------|-------------|---------|
| **T1 — Trivial** | Pure scaffolding, copy/text change, config tweak | Update page title, add a color token, add a route constant |
| **T2 — Simple** | Single-file component or utility, well-defined I/O | New stateless UI component, a format helper, a unit test file |
| **T3 — Medium** | Multi-file change, moderate state or API integration | New page with existing API, form with validation, responsive layout |
| **T4 — Complex** | New API contract, complex state, cross-cutting change | New backend endpoint + frontend integration, auth change, migration |
| **T5 — Exploratory** | Unknown unknowns, high ambiguity, novel architecture | First use of a new pattern, ambiguous PRD requirements, performance work |

Classify every checklist item into a tier. Count totals: `n_T1`, `n_T2`, `n_T3`, `n_T4`, `n_T5`.

---

#### Mode 1 — Fully Unsupervised AI

Claude Code (or equivalent agentic AI) executes all work end-to-end with no human review loops until final delivery.

**Assumptions:**
- AI handles T1–T3 items reliably; T4 items carry a 30 % rework risk; T5 items carry a 60 % rework risk.
- No waiting time for human feedback between tasks.
- Parallelism factor: AI can run ~3 independent tracks simultaneously.

**Per-item base durations (wall-clock, including generation + self-review):**

| Tier | Base time |
|------|-----------|
| T1 | 5 min |
| T2 | 20 min |
| T3 | 60 min |
| T4 | 2.5 hr (+ 45 min expected rework) |
| T5 | 4 hr (+ 2.5 hr expected rework) |

**Formula:**
```
Raw hours = (n_T1 × 0.08) + (n_T2 × 0.33) + (n_T3 × 1.0)
           + (n_T4 × 3.25) + (n_T5 × 6.5)
Parallel factor = 0.40   # 3 tracks → ~40 % of sequential time
Ambiguity buffer = open_questions × 0.5 hr
Total AI hours = (Raw hours × Parallel factor) + Ambiguity buffer
```

Present as: **X hours** (best case) → **Y hours** (worst case, +50 % on T4/T5 rework).

Highlight any T5 items as **high-risk** — they may cause the AI to stall or produce incorrect output that is hard to detect without domain knowledge.

---

#### Mode 2 — Supervised AI (AI executes, humans review)

AI produces each increment; a human engineer reviews, approves, and merges before the next increment starts.

**Assumptions:**
- Human review adds 20–40 min per PR (or per logical batch of checklist items).
- Estimate one review cycle per T3 item and two per T4/T5 item.
- Human can catch AI errors in T4/T5; rework risk drops to 15 % for T4, 30 % for T5.
- One reviewer, part-time (≤ 2 hr/day dedicated to reviews).

**Per-item base durations (AI time + review overhead):**

| Tier | AI time | Review overhead | Effective total |
|------|---------|-----------------|----------------|
| T1 | 5 min | 0 min (batch) | 5 min |
| T2 | 20 min | 10 min (batch) | 30 min |
| T3 | 60 min | 30 min | 90 min |
| T4 | 2.5 hr | 60 min × 2 | 4.5 hr |
| T5 | 4 hr | 90 min × 2 | 7 hr |

**Formula:**
```
AI hours      = same Raw hours as Mode 1 (no parallelism discount — gated by reviews)
Review hours  = (n_T2 × 0.17) + (n_T3 × 0.5) + (n_T4 × 2.0) + (n_T5 × 3.0)
Rework hours  = (n_T4 × 0.375) + (n_T5 × 1.2)   # reduced rework rates
Total hours   = AI hours + Review hours + Rework hours
Calendar days = Total hours ÷ 6   # assuming reviewer bottleneck caps throughput at ~6 hr/day
```

Present as: **X hours total** across AI + human | **Y calendar days** at standard throughput.

---

#### Mode 3 — Fully Manual (human engineers only)

Experienced engineers do all implementation, code review, and QA manually. No AI assistance.

**Assumptions:**
- Senior engineer unless flagged otherwise; junior adds 1.5× multiplier.
- Effective coding hours per day: 5 hr (meetings, slack, context-switching).
- Code review: 1 round per PR; 30 min/PR for reviewer, 20 min/PR for author to address.
- QA cycle: 1 round at the end; duration = 25 % of dev time.
- Scope buffer: +20 % for unknown unknowns in a real codebase.

**Per-item base durations (senior engineer):**

| Tier | Dev time | Review overhead |
|------|----------|-----------------|
| T1 | 15 min | 5 min |
| T2 | 1 hr | 20 min |
| T3 | 3 hr | 45 min |
| T4 | 8 hr | 90 min |
| T5 | 16 hr | 3 hr |

**Formula:**
```
Dev hours    = (n_T1 × 0.25) + (n_T2 × 1.0) + (n_T3 × 3.0)
             + (n_T4 × 8.0) + (n_T5 × 16.0)
Review hours = (n_T1 × 0.08) + (n_T2 × 0.33) + (n_T3 × 0.75)
             + (n_T4 × 1.5) + (n_T5 × 3.0)
QA hours     = Dev hours × 0.25
Scope buffer = (Dev hours + Review hours + QA hours) × 0.20
Total hours  = Dev hours + Review hours + QA hours + Scope buffer
Calendar days = Total hours ÷ 5   # 5 effective hours/day
```

If `n_T5 > 2`, add an explicit **discovery spike** of 1–2 days before estimation can be trusted.

Present as: **X dev-days** (senior engineer, solo) | **Y calendar days** (if parallelized across 2 engineers).

---

#### Estimate summary table

Present this as the first thing in Phase 9 output, before the detailed breakdowns:

| Mode | Total effort | Calendar time | AI cost signal | Human cost signal | Risk level |
|------|-------------|---------------|---------------|-------------------|------------|
| 1 — Unsupervised AI | X hr | X hr wall-clock | High (many tokens) | None | High (T4/T5 undetected errors) |
| 2 — Supervised AI | X hr | X days | Medium | Low (review only) | Medium |
| 3 — Manual | X hr | X days | None | High | Low |

#### Confidence rating

After computing, assign an overall confidence level and explain it:

| Confidence | Condition |
|------------|-----------|
| **High (±15 %)** | All requirements measurable, no T5 items, repo well-understood |
| **Medium (±30 %)** | ≤ 3 open questions, ≤ 2 T5 items, some repo ambiguity |
| **Low (±50 %+)** | Many unresolved gaps, T5 items dominate, no repo access |

State the confidence level explicitly: `"Estimate confidence: Medium (±30 %) — 2 T5 items and 4 open questions remain unresolved."`

---

### Phase 10 — Final deliverable

Combine everything into one Markdown file at `./<output_filename>` (or `/mnt/user-data/outputs/<output_filename>` if running in a sandboxed environment).

Structure:
1. Document metadata (author, date, version, status, inputs used)
2. Table of contents
3. Executive summary (5–8 bullets max) — include the estimate summary table here
4. Phase 2 — PRD requirements table
5. Phase 3 — Figma inventory
6. Phase 4 — Current state analysis
7. Phase 5 — Gap analysis + Open questions
8. Phase 6 — Implementation checklist
9. Phase 7 — Test cases
10. Phase 8 — Technical specs
11. Phase 9 — Effort estimates (all three modes + confidence rating)
12. Appendix — Assumptions made

Then present the file to the user.

---

## Operating principles

- **Read before asking.** If a PRD was provided, read it before asking questions about it.
- **Mark assumptions explicitly.** Anything not in the PRD or Figma that you infer must be tagged **[ASSUMPTION]** inline and listed in the appendix.
- **Respect repo conventions.** Inspect the repo's existing patterns (state, styling, routing, data fetching) before recommending changes. Do not introduce new libraries or patterns unless the PRD requires them.
- **Be specific.** "Improve accessibility" is not a test case. "Tab order on the booking widget matches visual order; focus ring is visible on all interactive elements (WCAG 2.4.7)" is.
- **Trace everything.** Every test case ties to a requirement. Every spec item ties to a checklist item. Every gap has an owner.
- **Don't pad.** If a phase has nothing to report, say so in one line. Length is not the metric.

---

## Interaction style

- After Phase 1, briefly confirm: "Here's what I've got. Should I proceed through phases 2–10 and present the final doc, or pause after each phase for review?"
- During analysis phases, surface the **most important 2–3 findings** in chat, even though the full output goes in the file.
- If something in the PRD or Figma seems wrong (internal contradiction, missing critical state, accessibility miss), flag it conversationally — don't bury it in the table.

---

## Reference files

- `references/output_template.md` — the exact structure of the final deliverable. Read this before writing Phase 10.
- `references/severity_rubric.md` — how to assign Blocker / High / Medium / Low. Read this if unsure during Phase 5.
- `references/test_taxonomy.md` — the test types and what each should cover. Read this during Phase 7.

These are optional reads — pull them in when relevant. They keep SKILL.md focused.
