---
name: isp_effort_estimate
description: 'Produce three-mode effort estimates (Unsupervised AI, Supervised AI, Manual) for a feature implementation, derived from the implementation checklist and technical specs. Runs five independent estimation passes with slightly varied assumption sets to produce a converged estimate range and confidence rating. Use after isp_checklist and isp_tech_specs to produce effort estimates. Trigger on: "how long will this take", "estimate the effort", "sprint planning", "sizing", "effort estimate", or as the ninth step in the isp_feature_analysis workflow.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP Effort Estimates

This skill produces three-mode effort estimates across five independent estimation passes. Each pass uses slightly varied assumption sets to simulate different estimators. The converged output is a range with an explicit confidence rating — not a single point estimate that implies false precision.

**Receives from:** `isp_checklist` (CL items and complexity tiers), `isp_tech_specs` (file count, API contracts, risks), `isp_gap_analysis` (open question count)
**Feeds into:** `isp_deliverable`

---

## Inputs required before estimating

| Signal | Source |
|--------|--------|
| Checklist items classified by complexity tier (T1–T5) | `isp_checklist` |
| Count of new vs modified vs deleted files | `isp_tech_specs` |
| Presence of API contracts, data-model changes, or migrations | `isp_tech_specs` |
| Number of test cases by type | `isp_test_cases` |
| Count of open questions still unresolved | `isp_gap_analysis` |
| Repo familiarity signal (consistent conventions vs. messy/undocumented) | `isp_tech_specs` |

## Complexity tiers

| Tier | Description | Examples |
|------|-------------|---------|
| `T1 Trivial` | Scaffolding, copy change, config tweak | Color token, page title, route constant |
| `T2 Simple` | Single-file component or utility | Stateless component, format helper, unit test |
| `T3 Medium` | Multi-file change, moderate state or API | New page with existing API, form with validation |
| `T4 Complex` | New API contract, complex state, cross-cutting | New endpoint + frontend integration, auth change |
| `T5 Exploratory` | High ambiguity, novel architecture | First use of new pattern, ambiguous PRD, perf work |

---

## Workflow

### Pass 0 — Baseline estimate

Classify every CL item into T1–T5. Count: `n_T1`, `n_T2`, `n_T3`, `n_T4`, `n_T5`.

Compute all three modes using the formulas below. Store as **Estimate 0**.

#### Mode 1 — Fully Unsupervised AI

```
Raw hours = (n_T1 × 0.08) + (n_T2 × 0.33) + (n_T3 × 1.0)
           + (n_T4 × 3.25) + (n_T5 × 6.5)
Parallel factor  = 0.40
Ambiguity buffer = open_questions × 0.5 hr
Total AI hours   = (Raw hours × Parallel factor) + Ambiguity buffer
```

#### Mode 2 — Supervised AI

```
AI hours      = Raw hours (no parallelism — gated by reviews)
Review hours  = (n_T2 × 0.17) + (n_T3 × 0.5) + (n_T4 × 2.0) + (n_T5 × 3.0)
Rework hours  = (n_T4 × 0.375) + (n_T5 × 1.2)
Total hours   = AI hours + Review hours + Rework hours
Calendar days = Total hours ÷ 6
```

#### Mode 3 — Fully Manual

```
Dev hours    = (n_T1 × 0.25) + (n_T2 × 1.0) + (n_T3 × 3.0)
             + (n_T4 × 8.0) + (n_T5 × 16.0)
Review hours = (n_T1 × 0.08) + (n_T2 × 0.33) + (n_T3 × 0.75)
             + (n_T4 × 1.5) + (n_T5 × 3.0)
QA hours     = Dev hours × 0.25
Scope buffer = (Dev hours + Review hours + QA hours) × 0.20
Total hours  = Dev hours + Review hours + QA hours + Scope buffer
Calendar days = Total hours ÷ 5
```

### Passes 1–4 — Re-estimation with varied assumptions

Each pass re-classifies the checklist items with a slightly different assumption set:

| Pass | Assumption variation |
|------|---------------------|
| Pass 1 | T4 items carry 40 % rework risk (vs. 30 % baseline); T5 carry 70 % |
| Pass 2 | Parallel factor for Mode 1 = 0.35 (less parallelism); reviewer bottleneck = 5 hr/day |
| Pass 3 | Junior engineer multiplier applied (1.5×) for Mode 3 |
| Pass 4 | +15 % scope buffer on all modes (more unknown unknowns) |

For each pass:
1. Re-classify CL items into T1–T5 from scratch.
2. Compute all three modes using the pass's assumption variation.
3. Compare totals to the current estimate draft:
   - Within 15 % of previous pass → **converged**.
   - 15–30 % difference → **within range**.
   - Over 30 % difference → **challenged** — re-examine classification.
4. Apply critique questions:
   - Did I classify any T3 item that should be T4 given the repo complexity?
   - Are there hidden T5 items (novel patterns, ambiguous PRDs) I've been underweighting?
   - Does the ambiguity buffer reflect all unresolved open questions from `isp_gap_analysis`?
   - Is the parallel factor realistic given the actual dependency chain in the checklist?
   - Am I accounting for integration testing time in Mode 3?
5. Update the **convergence tally**.

### Convergence tally

| Mode | Pass 0 | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Range | Converged? |
|------|--------|--------|--------|--------|--------|-------|------------|
| Mode 1 (AI) | X hr | X hr | X hr | X hr | X hr | X–Y hr | Yes / No |
| Mode 2 (Supervised) | X hr | X hr | X hr | X hr | X hr | X–Y hr | Yes / No |
| Mode 3 (Manual) | X days | X days | X days | X days | X days | X–Y days | Yes / No |

Converged = all passes within 20 % of each other. If not converged, identify which CL items are driving variance and re-examine their tier classification.

---

## Final output

### Estimate summary table

| Mode | Total effort | Calendar time | AI cost signal | Human cost signal | Risk level |
|------|-------------|---------------|---------------|-------------------|------------|
| 1 — Unsupervised AI | X–Y hr | X–Y hr wall-clock | High | None | High (T4/T5 errors undetected) |
| 2 — Supervised AI | X–Y hr total | X–Y days | Medium | Low (review only) | Medium |
| 3 — Manual | X–Y hr | X–Y days | None | High | Low |

### Confidence rating

| Confidence | Condition |
|------------|-----------|
| **High (±15 %)** | All requirements measurable, no T5 items, repo well-understood, passes converged |
| **Medium (±30 %)** | ≤ 3 open questions, ≤ 2 T5 items, some repo ambiguity, passes within range |
| **Low (±50 %+)** | Many unresolved gaps, T5 items dominate, no repo access, passes diverged |

State explicitly: `"Estimate confidence: Medium (±30 %) — 2 T5 items and 4 open questions remain unresolved."`

If `n_T5 > 2`, prepend: `"Recommend a discovery spike of 1–2 days before committing to these estimates."`

### Tier breakdown

| Tier | Count | Mode 1 contribution | Mode 3 contribution |
|------|-------|---------------------|---------------------|
| T1 | N | X hr | X hr |
| T2 | N | X hr | X hr |
| T3 | N | X hr | X hr |
| T4 | N | X hr | X hr |
| T5 | N | X hr | X hr |

---

## Operating principles

- **Range over point.** Present min–max, not a single number. False precision erodes trust.
- **T5 items are high-risk.** Flag each one explicitly — they are the most likely source of estimate failure.
- **Do not estimate unresolved open questions.** Items blocked on open questions from `isp_gap_analysis` are excluded from estimates. Add a note: "N items not estimated — blocked on unresolved open questions."
- **Convergence is the signal.** If passes diverge significantly, the root cause is classification uncertainty — fix the tier assignments, not the formula.
