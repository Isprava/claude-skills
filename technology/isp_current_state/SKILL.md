---
name: isp_current_state
description: 'Analyse the current production UI by classifying every existing component as Keep, Modify, Replace, Remove, or New across five independent inspection passes. Classifications that converge across passes are high-confidence. Use to understand what already exists before gap analysis or implementation planning. Trigger on: "what exists today", "analyse the current UI", "current state review", "what do we keep vs replace", or as the fourth step after isp_figma_analysis. Skip if no current-state references are provided.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP Current-State Analysis

This skill classifies every component in the current production UI against the incoming Figma design across five independent inspection passes. Classifications that converge across passes are high-confidence; components where passes disagree signal ambiguity about what to keep or replace. Skip this skill if no current-state references (screenshots, live URL, or description) are available.

**Receives from:** `isp_intake`, `isp_figma_analysis`
**Feeds into:** `isp_gap_analysis`

---

## Classification labels

| Label | Meaning |
|-------|---------|
| `Keep` | Component exists today and carries forward unchanged |
| `Modify` | Component exists but needs changes (styling, behaviour, copy) |
| `Replace` | Component is replaced entirely by a new Figma component |
| `Remove` | Component exists today but is not in the new design |
| `New` | Component does not exist today; must be built from scratch |

---

## Regression risk flag

Any component classified `Remove` or `Modify` that has behaviour not shown in the new Figma design should carry a **Regression-Risk** flag. These are candidates for unintentional breakage.

---

## Workflow

### Pass 0 — First inspection

Inspect all provided current-state references (screenshots, live page description, or URL). For each visible component, assign a classification and ID:
- `CS-01`, `CS-02`, ... — current-state component IDs

| ID | Component | Current behaviour | Classification | Regression risk | Notes |
|----|-----------|------------------|---------------|-----------------|-------|

Store as **Draft 0**. Do not present yet.

### Passes 1–4 — Independent re-inspections

For each of the four additional passes:

1. Re-inspect current-state references from scratch without referencing the previous draft.
2. Re-classify all visible components.
3. Compare each classification to the current draft:
   - Classification matches → **confirmed** for this pass.
   - Classification differs → **challenged** — record both classifications.
   - New component spotted → **emerging**.
4. Apply critique questions to each confirmed classification:
   - Is the classification driven by the Figma design or my assumption about intent?
   - Could "Modify" actually be a full "Replace" in disguise (completely different UX)?
   - Does the current component have behaviour (state, API call, animation) not shown in the new design?
   - Is this component intentionally removed, or just not shown in the frames provided?
   - Could a "Remove" be a false negative — maybe it's on a frame I haven't seen?
5. Update the **convergence tally**.

### Convergence tally

| ID | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Confidence |
|----|--------|--------|--------|--------|-------|------------|
| CS-01 (Header) | Keep | Keep | Keep | Keep | 5/5 | High |
| CS-04 (Sidebar) | Modify | Replace | Modify | Modify | 3/5 | Medium |
| CS-07 (Footer) | Remove | Remove | Keep | Remove | 3/5 | Medium |

For classification conflicts, record the **majority classification** and flag it as `⚠ conflicted`.

**Confidence thresholds:**

| Score | Confidence | Action |
|-------|------------|--------|
| 5/5 | **High** | Include in verified current-state table |
| 4/5 | **High** | Include; note the one-pass conflict |
| 3/5 | **Medium** | Include with `⚠ verify classification` flag |
| 2/5 | **Low** | Appendix — needs human confirmation |
| 1/5 | **Noise** | Discard |

---

## Final output

### Verified current-state table (confidence ≥ 3/5)

| ID | Component | Classification | Score | Regression risk | Notes |
|----|-----------|---------------|-------|-----------------|-------|

**Summary counts:**
```
Keep    : N
Modify  : N
Replace : N
Remove  : N
New     : N (from Figma, not yet in production)

Regression-risk components: N — review before implementation
```

### Classification conflicts (score 3–4/5 with disagreement)

List components where passes disagreed on Keep vs. Modify vs. Replace. These need a product or design decision before implementation begins.

### Low-confidence appendix (score 2/5)

Components seen inconsistently across passes. Flag for manual inspection of the live UI.

---

## Operating principles

- **Base classification on the Figma design, not assumptions.** If the Figma does not show a component, classify it as `Remove` and flag as Regression-Risk — do not assume it was intentionally kept.
- **Regression-Risk is not optional.** Every `Remove` and `Modify` must be evaluated for hidden behaviour before carrying into gap analysis.
- **Conflict is information.** When passes disagree on a classification, that disagreement is itself a finding — it means the scope decision is ambiguous.
- **Skip gracefully.** If no current-state references exist, output a one-line note: "No current-state references provided — Phase 4 skipped. Recommend reviewing before implementation." Do not fabricate a current state.
