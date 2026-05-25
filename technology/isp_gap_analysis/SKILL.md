---
name: isp_gap_analysis
description: 'Three-way gap analysis comparing PRD requirements, Figma design, and current production state across five independent passes. Each finding is scored by convergence — only gaps that re-emerge consistently are reported as high-confidence. Use after isp_prd_analysis, isp_figma_analysis, and isp_current_state to produce the verified gap register that drives the implementation checklist. Trigger on: "find the gaps", "what is missing", "compare PRD to design", "what does not match", or as the fifth step in the isp_feature_analysis workflow.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP Gap Analysis

This skill compares PRD requirements, Figma design, and the current production state in a three-way comparison run across five independent passes. Only findings that survive self-critique and re-emerge consistently are reported as high-confidence gaps. The output drives all downstream phases: checklist, test cases, and technical specs.

**Receives from:** `isp_prd_analysis` (REQ register), `isp_figma_analysis` (design inventory), `isp_current_state` (classification table)
**Feeds into:** `isp_checklist`, `isp_test_cases`, `isp_tech_specs`

---

## Gap types

| Gap Type | Meaning |
|----------|---------|
| `Missing-in-PRD` | Present in Figma or current state; no PRD requirement backs it |
| `Missing-in-Figma` | Required by PRD; not shown in any Figma frame |
| `Missing-in-Current` | Required by PRD or shown in Figma; not in today's codebase |
| `Conflict` | PRD and Figma contradict each other on the same element |
| `Ambiguous` | Requirement exists but is too vague to compare against design or code |
| `Out-of-Scope` | Explicitly excluded in the PRD but present in Figma or current state |
| `Regression-Risk` | Existing behaviour not accounted for in the new design |

## Severity levels

| Severity | Meaning |
|----------|---------|
| `Blocker` | Core user flow broken or undefined; must resolve before build |
| `High` | Important feature missing or misaligned; workaround is poor |
| `Medium` | Secondary behaviour differs; UX degraded but not broken |
| `Low` | Cosmetic, copy, or edge-case difference |

---

## Workflow

### Pass 0 — Initial three-way comparison

Using the verified outputs from `isp_prd_analysis`, `isp_figma_analysis`, and `isp_current_state`, scan for discrepancies. For each finding:

| GAP-ID | Requirement / Element | PRD | Figma | Current | Gap Type | Severity | Owner | Notes |
|--------|-----------------------|-----|-------|---------|----------|----------|-------|-------|

- **Owner:** `Product` (PRD needs clarification), `Design` (Figma needs update), `Engineering` (code needs change), `QA` (test coverage gap)

Assign IDs: `GAP-01`, `GAP-02`, ... Store as **Draft 0**. Do not present yet.

### Passes 1–4 — Independent re-comparisons

For each of the four additional passes:

1. Re-read the PRD requirement register, Figma inventory, and current-state table from scratch.
2. Generate a fresh gap list independently.
3. Compare each finding to the current draft:
   - Matches an existing GAP → **confirmed**.
   - New gap found → **emerging**.
   - Draft GAP absent → **challenged**.
4. Apply critique questions to each confirmed finding:
   - Could this gap be intentional — a product decision not yet documented?
   - Does another section of the PRD or a different Figma frame resolve this?
   - Is this gap in the PRD (ambiguous requirement) or in the implementation (wrong code/design)?
   - Would the PM who wrote this PRD recognize it as a gap?
   - Would the engineer who built this recognize it as a discrepancy?
5. Update the **convergence tally**.

### Convergence tally

| GAP-ID | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Confidence |
|--------|--------|--------|--------|--------|-------|------------|
| GAP-01 | ✓ | ✓ | ✓ | ✓ | 5/5 | High |
| GAP-04 | ✓ | ✗ | ✓ | ✓ | 4/5 | High |
| GAP-07 | ✓ | ✗ | ✓ | ✗ | 3/5 | Medium |
| GAP-11 | ✗ | ✗ | ✓ | ✗ | 2/5 | Low |

**Confidence thresholds:**

| Score | Confidence | Action |
|-------|------------|--------|
| 5/5 | **High** | Include in main gap table |
| 4/5 | **High** | Include; note the one miss |
| 3/5 | **Medium** | Include with `⚠ needs verification` flag |
| 2/5 | **Low** | Appendix — "potential gap, verify manually" |
| 1/5 | **Noise** | Discard |

---

## Final output

### Verified gap table (confidence ≥ 3/5)

| GAP-ID | Requirement / Element | PRD | Figma | Current | Gap Type | Severity | Score | Owner | Notes |
|--------|-----------------------|-----|-------|---------|----------|----------|-------|-------|-------|

### Open questions

One bullet per ambiguity, phrased as a direct question to the right owner:
- `[Product]` GAP-03: The PRD says "contextual CTA" but does not define the trigger. What is the trigger condition?
- `[Design]` GAP-07: Mobile frame is missing — is the layout the same as tablet or unique?

### Low-confidence appendix (score 2/5)

Gaps seen in some passes but not consistently. Include for human review; do not carry into implementation phases as confirmed.

### Summary

```
Gap analysis summary
────────────────────
Passes completed    : 5
Total findings      : N
  High confidence   : N (Blocker: X | High: X | Medium: X | Low: X)
  Medium confidence : N (⚠ needs human verification)
  Discarded (noise) : N

Open questions      : N (Product: X | Design: X | Engineering: X)
```

---

## Operating principles

- **Every gap needs an owner.** Unowned gaps do not get resolved.
- **Separate "PRD is ambiguous" from "code/design is wrong".** Different root cause, different owner, different fix.
- **Do not invent gaps.** Every finding must point to a specific REQ-ID, FIG-ID, or CS-ID from the upstream phase outputs.
- **Convergence over volume.** Ten high-confidence gaps are more useful than forty uncertain ones.
