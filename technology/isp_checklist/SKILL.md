---
name: isp_checklist
description: 'Generate a developer-actionable implementation checklist from the verified gap register, covering components, APIs, state, routing, accessibility, analytics, and more. Runs five independent generation passes and scores each checklist item by convergence — only items that appear consistently are included in the final checklist. Use after isp_gap_analysis to produce the atomic task list that drives implementation. Trigger on: "build the checklist", "what needs to be built", "implementation tasks", "what do I need to do", or as the sixth step in the isp_feature_analysis workflow.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP Implementation Checklist

This skill generates a developer-actionable checklist from the verified gap register across five independent passes. Items that re-emerge consistently across passes are high-confidence work items. Items that only appear in some passes either represent optional work or were mis-derived from the gaps — convergence scoring separates the two.

**Receives from:** `isp_gap_analysis` (verified gap table and open questions)
**Feeds into:** `isp_test_cases`, `isp_tech_specs`, `isp_effort_estimate`

---

## Checklist domains

Generate items across all applicable domains:

| Domain | What to cover |
|--------|--------------|
| Components / modules | New components, modified components, file paths if repo is known |
| API / backend | New endpoints, modified contracts, request/response shapes |
| State management | New state slices, context providers, derived state |
| Routing | New routes, redirects, guards, breadcrumbs |
| Responsive breakpoints | Per-breakpoint layout tasks |
| Accessibility | Specific WCAG checks — keyboard nav, focus management, ARIA labels, contrast |
| Analytics | Event names, properties, trigger conditions |
| SEO / metadata | Title, description, structured data, canonical |
| Feature flags / rollout | Flag names, rollout stages, kill-switch conditions |
| Documentation | README updates, storybook, API docs |

Every item uses `- [ ]` syntax. Items must be atomic — small enough that a single PR could close several of them.

---

## Workflow

### Pass 0 — Initial generation

Read the verified gap table from `isp_gap_analysis`. For each confirmed gap (High and Medium confidence), derive one or more actionable checklist items. Assign IDs:
- `CL-01`, `CL-02`, ... — sequential across all domains

Every item must trace back to at least one `GAP-ID`.

| CL-ID | Domain | Task | Linked GAP | Complexity tier |
|-------|--------|------|------------|----------------|

**Complexity tiers:**
- `T1 Trivial` — config tweak, copy change, token update
- `T2 Simple` — single-file component, format utility
- `T3 Medium` — multi-file change, moderate state or API
- `T4 Complex` — new API contract, cross-cutting change
- `T5 Exploratory` — high ambiguity, novel pattern

Store as **Draft 0**. Do not present yet.

### Passes 1–4 — Independent re-generations

For each of the four additional passes:

1. Re-read the gap register from scratch without referencing Draft 0.
2. Independently derive the full checklist.
3. Compare each item to the current draft:
   - Matches existing CL item → **confirmed**.
   - New item derived → **emerging**.
   - Draft item absent → **challenged**.
4. Apply critique questions to each confirmed item:
   - Is this item atomic enough for one PR, or should it be split?
   - Does it trace directly to a GAP-ID, or am I adding scope?
   - Is the complexity tier accurate given what the repo already has?
   - Is this truly required by a confirmed gap, or by an open question (unresolved)?
   - Would removing this item leave a gap unaddressed?
5. Update the **convergence tally**.

### Convergence tally

| CL-ID | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Confidence |
|-------|--------|--------|--------|--------|-------|------------|
| CL-01 | ✓ | ✓ | ✓ | ✓ | 5/5 | High |
| CL-06 | ✓ | ✗ | ✓ | ✗ | 3/5 | Medium |
| CL-12 | ✗ | ✗ | ✓ | ✗ | 2/5 | Low |

**Confidence thresholds:**

| Score | Confidence | Action |
|-------|------------|--------|
| 5/5 | **High** | Include in final checklist |
| 4/5 | **High** | Include; note the one miss |
| 3/5 | **Medium** | Include with `⚠ verify scope` flag |
| 2/5 | **Low** | Appendix — possible scope addition |
| 1/5 | **Noise** | Discard |

---

## Final output

### Verified implementation checklist (confidence ≥ 3/5)

Organized by domain:

```
## Components
- [ ] [CL-01] [T2] Create <ComponentName> — linked to GAP-02
- [ ] [CL-02] [T3] Modify <ComponentName> to support <state> — linked to GAP-05

## API / Backend
- [ ] [CL-08] [T4] Add POST /endpoint with schema <X> — linked to GAP-09

## Accessibility
- [ ] [CL-15] [T1] Add aria-label to <element> — linked to GAP-11

...
```

### Checklist summary

```
Total items     : N
  T1 Trivial    : N
  T2 Simple     : N
  T3 Medium     : N
  T4 Complex    : N
  T5 Exploratory: N

Medium-confidence items (⚠ verify scope): N
```

### Optional-scope appendix (score 2/5)

Items that appeared in some passes — may represent scope that should be discussed before committing.

---

## Operating principles

- **Trace everything.** Every CL item links to at least one GAP-ID. Items without a link are scope additions — flag them explicitly.
- **Atomic items only.** If implementing an item requires touching more than three files and involves a non-trivial design decision, split it.
- **Open questions block items.** If a checklist item depends on an unresolved open question from `isp_gap_analysis`, flag it as blocked: `⚠ blocked on [Product] question re: GAP-03`.
- **No implementation detail yet.** This is a task list, not technical specs. File paths and API contracts belong in `isp_tech_specs`.
