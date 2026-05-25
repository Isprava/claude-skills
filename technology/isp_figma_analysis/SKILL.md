---
name: isp_figma_analysis
description: 'Enumerate every component, state, breakpoint, and interaction visible in Figma designs through five independent inspection passes. Components and states that appear consistently across passes form the high-confidence design inventory used in gap analysis. Use when cataloguing a Figma design for feature analysis, auditing design coverage, or building a component inventory before comparing against a PRD or codebase. Trigger on: "analyze the Figma", "what does the design show", "catalog the components", "inspect the Figma frames", or as the third step after isp_prd_analysis.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP Figma Analysis

This skill inspects Figma designs five times independently and cross-checks every catalogued component, state, and interaction across passes. Design elements that appear consistently are high-confidence inventory items. Single-pass Figma inspection misses states, breakpoints, and edge-case frames — five passes ensure full coverage.

**Receives from:** `isp_intake` (confirmed inputs block)
**Feeds into:** `isp_gap_analysis`

---

## What to catalogue

For each Figma frame or screen, enumerate:

| Dimension | What to record |
|-----------|---------------|
| **Components** | Every distinct UI element (button, card, modal, nav, form, etc.) |
| **States** | All variants per component: default, hover, active, loading, error, empty, disabled, focused |
| **Breakpoints** | Exact viewport widths shown (e.g., 375 px mobile, 768 px tablet, 1440 px desktop) |
| **Typography** | Font styles, sizes, weights — flag any deviations from the existing design system |
| **Spacing & color tokens** | Note design-system token usage vs. hard-coded values |
| **Interactions** | Animations, transitions, gestures, scroll behavior |
| **Edge cases** | Long text truncation, missing images, empty lists, RTL, overflow |
| **Extra elements** | Anything visible in Figma with no apparent PRD requirement behind it |

---

## Workflow

### Pass 0 — First inspection

Inspect all provided Figma frames or images. Record every element using the catalogue dimensions above. Assign a short ID:
- `FIG-C-01`, `FIG-C-02`, ... — components
- `FIG-S-01`, `FIG-S-02`, ... — states
- `FIG-B-01`, `FIG-B-02`, ... — breakpoints
- `FIG-X-01`, `FIG-X-02`, ... — extra / undocumented elements

Store as **Draft 0**. Do not present yet.

### Passes 1–4 — Independent re-inspections

For each of the four additional passes:

1. Re-inspect all Figma frames from scratch without referencing the previous draft.
2. Re-catalogue all visible elements.
3. Compare each catalogued item to the current draft:
   - Matches existing item → **confirmed** for this pass.
   - New item found → **emerging**.
   - Draft item absent → **challenged**.
4. Apply critique questions to each confirmed item:
   - Is this a distinct component, or a variant of an already-listed one?
   - Are all visible states catalogued, or did I miss any (e.g., no error state shown)?
   - Is this element tied to a PRD requirement, or is it a design addition?
   - Is the breakpoint shown a real target width, or a Figma canvas artifact?
   - Could this "extra" element be in scope but not yet in the PRD?
5. Update the **convergence tally**.

### Convergence tally

| Item ID | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Confidence |
|---------|--------|--------|--------|--------|-------|------------|
| FIG-C-01 | ✓ | ✓ | ✓ | ✓ | 5/5 | High |
| FIG-S-04 | ✓ | ✗ | ✓ | ✗ | 3/5 | Medium |
| FIG-X-02 | ✗ | ✗ | ✓ | ✗ | 2/5 | Low |

**Confidence thresholds:**

| Score | Confidence | Action |
|-------|------------|--------|
| 5/5 | **High** | Include in verified design inventory |
| 4/5 | **High** | Include; note the one miss |
| 3/5 | **Medium** | Include with `⚠ needs design review` flag |
| 2/5 | **Low** | Appendix — "possible element, verify with designer" |
| 1/5 | **Noise** | Discard |

---

## Final output

### Verified design inventory (confidence ≥ 3/5)

#### Components and states

| ID | Component | States catalogued | Breakpoints | Score | Notes |
|----|-----------|------------------|-------------|-------|-------|

#### Breakpoints

| ID | Width | Layout description | Score |
|----|----|---|---|

#### Interactions and animations

| ID | Trigger | Behavior | Target component | Score |
|----|---------|----------|-----------------|-------|

#### Extra elements (no PRD backing)

| ID | Element | Frame | Possible intent | Score |
|----|---------|-------|----------------|-------|

These extra elements become gap candidates in `isp_gap_analysis` — they may represent undocumented decisions or design drift.

### Low-confidence appendix (score 2/5)

Elements seen in some passes but not consistently. Flag for designer verification before gap analysis.

---

## If Figma is not directly accessible

If the Figma link cannot be opened:
1. Ask the user to paste relevant frames as images or screenshots.
2. Proceed with what is available; mark all items as `[PARTIAL — frame not viewed directly]`.
3. Flag the entire inventory as Medium confidence regardless of pass scores.
4. Recommend a follow-up session with direct Figma access.

---

## Operating principles

- **Only catalogue what is visible.** Do not infer states that are not shown in the frames.
- **Separate components from states.** A loading button is a state of the button component, not a separate component.
- **Flag design system deviations immediately.** A hard-coded color or font in a Figma frame that differs from the design system is a gap candidate, not just a visual note.
- **Extra elements are not mistakes.** Flag them neutrally — they may be intentional product decisions that need PRD coverage.
