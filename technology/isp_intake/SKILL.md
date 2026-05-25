---
name: isp_intake
description: 'Intake and validate all inputs for an ISP feature analysis session — repository path, PRD path, Figma path, feature name, and output filename. Runs five independent validation passes to surface missing, contradictory, or ambiguous inputs before any analysis begins. Use as the first step before isp_prd_analysis, isp_figma_analysis, or the full isp_feature_analysis workflow. Trigger when the user provides a PRD, Figma link, or repo path and wants to begin a feature analysis, gap audit, or implementation plan.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP Intake & Input Validation

This skill gathers and validates every input needed for a feature analysis session before any analysis begins. It runs five independent validation passes to surface missing fields, contradictions, and ambiguities in the inputs themselves — not the content. A clean intake prevents compounding errors across all downstream phases.

**Feeds into:** `isp_prd_analysis`, `isp_figma_analysis`, `isp_current_state`, `isp_gap_analysis`

---

## Inputs required

| Field | Required? | Fallback if missing |
|-------|-----------|---------------------|
| Project / repo name | Yes | Ask |
| Feature / page name | Yes | Ask |
| PRD location (path, URL, or paste) | Strongly preferred | Ask; note "no PRD — Figma is source of truth" |
| Figma link(s) or exported frames | Strongly preferred | Ask; note "no Figma — PRD is source of truth" |
| Current-state references (screenshots, URLs) | Optional | Flag as skipped; downstream Phase 4 will be skipped |
| Repo path / branch | Strongly preferred | Ask; specs will be framework-agnostic if absent |
| Output filename | No | Default to `<feature>_analysis.md` |

Read any files or links provided **before** asking questions — many answers are already in the PRD or Figma description.

---

## Workflow

### Pass 0 — First read

Scan all provided inputs. For each field in the table above, mark it as:
- `Present` — value is clearly provided
- `Absent` — not provided at all
- `Ambiguous` — provided but unclear (e.g., "the main repo" with no path, "the latest Figma" with no link)
- `Conflicted` — two inputs contradict each other (e.g., PRD says feature is mobile-only but repo is desktop-only app)

Record this as **Draft 0**. Do not present to the user yet.

### Passes 1–4 — Independent re-validation

For each of the four additional passes:

1. Re-scan all provided inputs independently without referencing Draft 0.
2. Re-classify each field.
3. Compare to current draft:
   - Field status matches → **confirmed**.
   - New issue found → **emerging**.
   - Previous issue absent → **challenged**.
4. Ask these critique questions for each flagged field:
   - Is the absence actually a problem, or can it be inferred from other inputs?
   - Is the ambiguity in the input itself, or in my interpretation?
   - Could the conflict be resolved by reading more carefully?
   - Would a downstream skill be blocked or just degraded without this input?
5. Update the **convergence tally**.

### Convergence tally

| Field | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Confidence |
|-------|--------|--------|--------|--------|-------|------------|
| PRD location | ✓ | ✓ | ✓ | ✓ | 5/5 | High |
| Figma link | ✗ | ✓ | ✗ | ✗ | 2/5 | Low |

**Confidence thresholds:**

| Score | Confidence | Action |
|-------|------------|--------|
| 5/5 | **High** | Issue is real — ask the user to resolve before proceeding |
| 4/5 | **High** | Issue is real — ask the user |
| 3/5 | **Medium** | Likely issue — flag it, offer to proceed with a placeholder |
| 2/5 | **Low** | Possibly a misread — note it, do not block |
| 1/5 | **Noise** | Discard |

---

## Final confirmed-inputs block

Present only High and Medium confidence issues to the user. Format:

```
Confirmed inputs
────────────────
Project         : <name>
Feature         : <name>
PRD             : <path or "not provided">
Figma           : <link or "not provided">
Current state   : <reference or "skipped">
Repo            : <path/branch or "not provided">
Output file     : <filename>

Issues requiring resolution (High confidence):
• [FIELD] — <what's wrong and what's needed>

Flags (Medium confidence — can proceed with placeholder):
• [FIELD] — <what's unclear and assumed value>
```

Ask: "Are these inputs correct? Should I proceed to PRD analysis, or do you want to resolve any issues first?"

---

## Operating principles

- **Read before asking.** Never ask for something already provided.
- **Distinguish blocking from degrading.** A missing repo path means specs will be generic — that is not a blocker for PRD analysis. A missing PRD and a missing Figma simultaneously is a blocker.
- **One question at a time.** If multiple fields are missing, ask for the most critical one first.
- **Do not begin analysis.** This skill only validates inputs. No requirement extraction, no gap finding.
