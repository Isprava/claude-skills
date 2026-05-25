---
name: isp_deliverable
description: 'Assemble all phase outputs into a single, standalone Markdown deliverable and run five completeness passes to verify every section is present, every cross-reference is intact, and no phase output was lost in assembly. Use as the final step after all isp_ analysis phases are complete. Trigger on: "produce the final document", "assemble the deliverable", "create the output file", "write the analysis doc", or as the tenth and final step in the isp_feature_analysis workflow.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP Final Deliverable

This skill assembles all phase outputs into one standalone Markdown file and verifies its completeness across five independent passes. Passes check for missing sections, broken cross-references (e.g., a TC-ID that references a REQ-ID that was removed), and inconsistencies between sections. The output is a document that can be handed to any engineer, designer, or product manager cold.

**Receives from:** All preceding isp_ skills (intake through effort estimates)
**Output:** `<feature>_analysis.md` (or the filename confirmed in `isp_intake`)

---

## Required document structure

| Section | Source phase | Required? |
|---------|-------------|-----------|
| Document metadata | `isp_intake` | Yes |
| Table of contents | Auto-generated | Yes |
| Executive summary (5–8 bullets) + estimate summary table | All phases | Yes |
| PRD requirements table | `isp_prd_analysis` | Yes |
| Figma inventory | `isp_figma_analysis` | Yes |
| Current-state analysis | `isp_current_state` | If phase was run |
| Gap analysis + open questions | `isp_gap_analysis` | Yes |
| Implementation checklist | `isp_checklist` | Yes |
| Test cases | `isp_test_cases` | Yes |
| Technical specs | `isp_tech_specs` | Yes |
| Effort estimates (all three modes + confidence) | `isp_effort_estimate` | Yes |
| Appendix — Assumptions | All phases | Yes |

---

## Workflow

### Pass 0 — Initial assembly

Assemble the document section by section. For each section, pull from the corresponding phase's final output (verified items only — do not include low-confidence appendices in the main body unless explicitly flagged). Assign the output filename confirmed during intake.

### Passes 1–4 — Completeness verification

For each of the four additional passes, re-read the assembled document independently and verify:

1. **Section presence:** Are all required sections present?
2. **Cross-reference integrity:** Do all IDs resolve correctly?
   - Every `TC-XX` links to a `REQ-XX` or `CL-XX` that exists in the document.
   - Every `CL-XX` links to a `GAP-XX` that exists in the document.
   - Every `SPEC-XX` links to a `CL-XX` that exists in the document.
3. **Confidence consistency:** Are items in the main body all ≥ 3/5 confidence? Are low-confidence items only in appendices?
4. **Open questions accounted for:** Is there an open questions section? Does it reflect the current state of unresolved questions from `isp_gap_analysis`?
5. **Executive summary accuracy:** Do the 5–8 bullets accurately reflect the document content, especially the top findings?

Apply critique questions:
- Is the executive summary something a PM could act on cold, without reading the rest?
- Are there contradictions between sections (e.g., a REQ claimed as implemented in specs but flagged as a gap)?
- Is every assumption tagged `[ASSUMPTION]` and listed in the appendix?
- Is there any phase output that is referenced in one section but missing from its dedicated section?
- Could an engineer start implementation from this document without needing to ask any clarifying questions about scope?

Update the **completeness tally**.

### Completeness tally

| Check | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Status |
|-------|--------|--------|--------|--------|-------|--------|
| All required sections present | ✓ | ✓ | ✓ | ✓ | 5/5 | Pass |
| All TC-IDs resolve | ✓ | ✗ | ✓ | ✓ | 4/5 | Pass (minor fix) |
| No contradictions between sections | ✓ | ✓ | ✗ | ✓ | 4/5 | Pass |
| Executive summary accurate | ✓ | ✓ | ✓ | ✓ | 5/5 | Pass |

Any check scoring below 3/5 is a **document defect** — fix before presenting the file to the user.

---

## Document structure

```markdown
# <Feature Name> — Analysis & Implementation Plan

**Author:** <from intake>
**Date:** <today>
**Version:** 1.0
**Status:** Draft | Ready for Review
**Inputs:** PRD: <path> | Figma: <link> | Repo: <path>

---

## Table of Contents
1. Executive Summary
2. PRD Requirements
3. Figma Inventory
4. Current-State Analysis
5. Gap Analysis & Open Questions
6. Implementation Checklist
7. Test Cases
8. Technical Specs
9. Effort Estimates
10. Appendix — Assumptions

---

## 1. Executive Summary

- <Finding 1>
- <Finding 2>
- ...

[Estimate summary table from isp_effort_estimate]

---

## 2. PRD Requirements
[Verified requirement register from isp_prd_analysis]

---

## 3. Figma Inventory
[Verified design inventory from isp_figma_analysis]

---

## 4. Current-State Analysis
[Verified current-state table from isp_current_state]
*Skipped — no current-state references provided.*

---

## 5. Gap Analysis & Open Questions
[Verified gap table and open questions from isp_gap_analysis]

---

## 6. Implementation Checklist
[Verified checklist from isp_checklist]

---

## 7. Test Cases
[Verified test suite and coverage matrix from isp_test_cases]

---

## 8. Technical Specs
[Verified specs from isp_tech_specs]

---

## 9. Effort Estimates
[All three modes, tier breakdown, and confidence rating from isp_effort_estimate]

---

## 10. Appendix — Assumptions
[All [ASSUMPTION] tags collected from all phases]
```

---

## Final output

Write the assembled document to `./<output_filename>` (or `/mnt/user-data/outputs/<output_filename>` in sandboxed environments). Then present to the user with:

```
Deliverable ready
─────────────────
File            : <output_filename>
Sections        : N / N required
Cross-references: All resolved (or: N broken — fixed)
Document defects: None (or: N found and corrected)

Top findings:
1. <GAP-XX or REQ-XX> — <one-line summary>
2. ...
3. ...
```

---

## Operating principles

- **Assemble from verified outputs only.** Never add new analysis in this phase. If something is missing from a phase output, surface it as a document defect and ask the user whether to re-run that phase or proceed with a gap.
- **Every assumption in the appendix.** Scan all sections for `[ASSUMPTION]` tags and collect them.
- **Cross-references must resolve.** A broken ID reference (e.g., `TC-04` linking to `REQ-99` which does not exist) is a document defect, not a cosmetic issue.
- **The executive summary is for cold readers.** It must be understandable without reading the rest of the document — include the estimate, the top 3 gaps, and the biggest open question.
