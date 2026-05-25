---
name: isp_prd_analysis
description: 'Extract and classify every requirement from a PRD through five independent reading passes, scoring each requirement by how consistently it is identified across passes. High-confidence requirements (≥3/5) form the verified requirement register; ambiguities that appear consistently become confirmed open questions. Use when starting a feature analysis, auditing a PRD for completeness, or building a requirement baseline before gap analysis. Trigger on: "extract requirements from this PRD", "what does the PRD say", "analyze the spec", "build a requirement list", or as the second step after isp_intake.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP PRD Analysis

This skill reads a PRD five times independently and cross-checks every extracted requirement across passes. Requirements that appear consistently are high-confidence; ambiguity flags that re-emerge across passes are confirmed open questions. Single-pass requirement extraction has high miss and false-positive rates — this skill eliminates both.

**Receives from:** `isp_intake` (confirmed inputs block)
**Feeds into:** `isp_figma_analysis`, `isp_gap_analysis`, `isp_checklist`, `isp_test_cases`

---

## Requirement categories

Classify every extracted requirement into one of:

| Category | What it covers |
|----------|---------------|
| `Functional` | What the system does |
| `Non-functional` | Performance, scale, security, reliability |
| `UI/UX` | Visual design, layout, interaction patterns |
| `Content` | Copy, microcopy, localization, empty states |
| `Analytics` | Tracking events, properties, triggers |
| `SEO` | Metadata, structured data, URL patterns |
| `Accessibility` | WCAG level, specific a11y requirements |
| `Out-of-scope` | Explicitly excluded in the PRD |

---

## Workflow

### Pass 0 — First read

Read the full PRD. Extract every requirement. For each, record:

| REQ ID | Category | Summary | Acceptance criteria | Ambiguity flag |
|--------|----------|---------|---------------------|----------------|

- `REQ-01`, `REQ-02`, ... — sequential IDs
- **Ambiguity flag**: mark if vague, unmeasurable, or contradicted elsewhere in the PRD
- Anything without a measurable acceptance criterion is automatically flagged as ambiguous

Store as **Draft 0**. Do not present yet.

### Passes 1–4 — Independent re-reads

For each of the four additional passes:

1. Re-read the PRD from scratch without referencing the previous draft.
2. Extract all requirements fresh.
3. Compare each extracted item to the current draft:
   - Matches existing REQ → **confirmed** for this pass.
   - New item found → **emerging**.
   - Draft REQ absent → **challenged**.
4. Apply critique questions to each confirmed requirement:
   - Is this truly a requirement, or a design suggestion / implementation detail?
   - Is the acceptance criterion measurable (time, count, boolean) or vague?
   - Does this requirement conflict with any other REQ in the draft?
   - Is this explicitly stated in the PRD, or am I inferring it?
   - Would removing this REQ change what gets built?
5. Update the **convergence tally**.

### Convergence tally

| REQ ID | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Confidence |
|--------|--------|--------|--------|--------|-------|------------|
| REQ-01 | ✓ | ✓ | ✓ | ✓ | 5/5 | High |
| REQ-04 | ✓ | ✗ | ✓ | ✗ | 3/5 | Medium |
| REQ-09 | ✗ | ✗ | ✓ | ✗ | 2/5 | Low |

**Confidence thresholds:**

| Score | Confidence | Action |
|-------|------------|--------|
| 5/5 | **High** | Include in verified requirement register |
| 4/5 | **High** | Include; note the one miss |
| 3/5 | **Medium** | Include with `⚠ needs clarification` flag |
| 2/5 | **Low** | Move to appendix as "candidate requirement" |
| 1/5 | **Noise** | Discard |

---

## Final output

### Verified requirement register (confidence ≥ 3/5)

| REQ ID | Category | Summary | Acceptance criteria | Score | Ambiguity flag |
|--------|----------|---------|---------------------|-------|----------------|

### Confirmed open questions (ambiguity score ≥ 3/5)

One bullet per question, phrased as a direct question to the right owner:
- `[Product]` Is "fast load" defined as a P95 target? If so, what is the threshold?
- `[Design]` The PRD mentions "contextual CTAs" but does not specify trigger conditions. What are they?

### Candidate requirements appendix (score 2/5)

Requirements that appeared in some passes but not consistently. Keep for human review — do not carry into downstream phases as confirmed.

### Discarded items (score 1/5)

Items that appeared once and did not re-emerge. Listed briefly for transparency.

---

## Operating principles

- **Requirements only.** Do not extract implementation suggestions, design opinions, or engineering notes — only statements about what the system must do or be.
- **No inference.** If a requirement is not in the PRD, do not add it. Tag any inference explicitly as `[ASSUMPTION]`.
- **Measurable or flagged.** Every requirement either has a measurable acceptance criterion or carries an ambiguity flag. No middle ground.
- **IDs are stable.** Once a REQ ID is assigned in Draft 0, keep it across all passes and in the final output.
