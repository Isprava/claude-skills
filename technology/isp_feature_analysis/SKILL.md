---
name: isp_feature_analysis
description: Run a structured, interactive gap analysis between a Product Requirements Document (PRD), Figma designs, the current production UI, and a target code repository — then produce a complete implementation plan (checklist, test cases, technical specs) as a single Markdown deliverable. Use this skill whenever the user mentions analyzing a PRD against Figma, comparing designs to current state, planning a redesign or feature rollout, building an implementation checklist from a spec, defining test cases for a redesign, or scoping work in a repo from product/design inputs — even if they don't explicitly say "gap analysis". Trigger on phrases like "analyze the PRD", "gaps between PRD and Figma", "implementation plan from this spec", "redesign analysis", "checklist for this feature", or any combination of PRD + Figma + repo references in one request.
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
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

### Phase 9 — Final deliverable

Combine everything into one Markdown file at `./<output_filename>` (or `/mnt/user-data/outputs/<output_filename>` if running in a sandboxed environment).

Structure:
1. Document metadata (author, date, version, status, inputs used)
2. Table of contents
3. Executive summary (5–8 bullets max)
4. Phase 2 — PRD requirements table
5. Phase 3 — Figma inventory
6. Phase 4 — Current state analysis
7. Phase 5 — Gap analysis + Open questions
8. Phase 6 — Implementation checklist
9. Phase 7 — Test cases
10. Phase 8 — Technical specs
11. Appendix — Assumptions made

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

- After Phase 1, briefly confirm: "Here's what I've got. Should I proceed through phases 2–9 and present the final doc, or pause after each phase for review?"
- During analysis phases, surface the **most important 2–3 findings** in chat, even though the full output goes in the file.
- If something in the PRD or Figma seems wrong (internal contradiction, missing critical state, accessibility miss), flag it conversationally — don't bury it in the table.

---

## Reference files

- `references/output_template.md` — the exact structure of the final deliverable. Read this before writing Phase 9.
- `references/severity_rubric.md` — how to assign Blocker / High / Medium / Low. Read this if unsure during Phase 5.
- `references/test_taxonomy.md` — the test types and what each should cover. Read this during Phase 7.

These are optional reads — pull them in when relevant. They keep SKILL.md focused.
