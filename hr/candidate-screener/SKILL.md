---
name: candidate-screener
description: >
  Screens and scores a batch of candidate resumes (5–20) against a Job Description, using user-defined must-have and nice-to-have criteria. Outputs a ranked scorecard table + a detailed per-candidate drill-down. Use this skill whenever a user uploads or pastes a JD plus one or more resumes and wants to evaluate, rank, compare, or shortlist candidates. Triggers on phrases like "evaluate these resumes", "score these candidates", "who's the best fit for this role", "rank my applicants", "screen resumes against this JD", or whenever a JD and multiple resumes appear together. Always use this skill — do not attempt to improvise a scoring framework without it.
---

# Candidate Screener Skill

Screens a batch of resumes against a JD, scores each candidate on user-defined criteria, and produces a ranked summary table + drill-down cards — so the hiring team can shortlist in minutes.

---

## Step 1 — Gather Inputs

Identify these inputs before proceeding. If anything is missing, ask explicitly.

| Input | What to extract | If missing |
|---|---|---|
| **Job Description** | Role title, responsibilities, required qualifications, preferred qualifications, team/culture context | Ask user to upload or paste the JD |
| **Resumes** | All uploaded resume files; extract: name, education, total YOE, tools/skills, relevant experience, career trajectory, gaps | Ask for uploads |
| **Must-Have criteria** | Non-negotiable requirements. Failing any = automatic disqualify | Ask: "What are the absolute must-haves for this role?" |
| **Nice-to-Have criteria** | Differentiating factors that raise or lower a score | Ask: "What nice-to-haves would make a candidate stand out?" |
| **Weights** | How important is each scored dimension? | Derive from JD if not given — see Step 2 |

**Reading uploaded files**: Use the `file-reading` skill to extract text from uploaded PDFs/DOCX resumes. Process all resumes before scoring any.

---

## Step 2 — Confirm Criteria With the User

Before scoring, present the criteria you will use and get confirmation.

Format the criteria check like this in your response:

```
📋 Scoring Criteria — please confirm or adjust before I score:

MUST-HAVES (any fail = disqualified):
• [list each must-have]

NICE-TO-HAVES (scored dimensions):
• [Dimension name] — [weight]% — [what counts as evidence]
• ...

Total weight: 100%
```

Wait for user confirmation or edits before proceeding to scoring.

---

## Step 3 — Derive Scoring Dimensions

If the user has not specified dimensions, derive 4–6 from the JD using this logic:

| Role type | Top-weighted dimension |
|---|---|
| Technical (eng, data, ML) | Technical skill depth (30%) |
| Execution / Ops | Relevant experience & ownership (30%) |
| Research / Strategy | Analytical thinking & domain knowledge (30%) |
| Customer-facing | Communication & stakeholder skills (30%) |
| Generalist | Breadth of experience & learning agility (25%) |

Always include:
- **Relevant Experience** (years + domain match)
- **Technical / Tool Fit** (skills match to JD requirements)
- **Career Trajectory** (growth signals, scope expansion)
- One dimension for the most common gap across resumes seen

Weights must sum to 100%.

---

## Step 4 — Score Each Candidate

For every candidate, score each dimension **1–5**:

| Score | Meaning |
|---|---|
| 5 | Exceeds requirement — clear evidence in resume |
| 4 | Meets requirement fully — solid evidence |
| 3 | Partial match — some evidence, some gaps |
| 2 | Weak match — minimal evidence |
| 1 | No evidence or actively contradicts requirement |

**Disqualification check**: Before scoring, check every must-have. If any must-have fails → mark candidate as `DISQUALIFIED` and skip dimension scoring.

**Weighted score**: `Σ (dimension_score × dimension_weight)` → produces a 1–5 composite score.

**Shortlist verdict** based on composite:
- ≥ 4.0 → 🟢 **Strong — Advance to interview**
- 3.0–3.9 → 🟡 **Consider — Review carefully**
- < 3.0 → 🔴 **Pass**
- Any must-have fail → ⛔ **Disqualified**

---

## Step 5 — Output Format

Always produce **both** outputs in sequence:

### Output A: Ranked Summary Table

Present as a markdown table, sorted by composite score descending:

```
| Rank | Candidate | [Dim1] | [Dim2] | [Dim3] | [Dim4] | Composite | Verdict |
|------|-----------|--------|--------|--------|--------|-----------|---------|
| 1    | Name      | 4/5    | 5/5    | 3/5    | 4/5    | 4.1       | 🟢 Advance |
...
```

Below the table, add a one-line **cohort observation** — what pattern stands out across all candidates (e.g., "Strong on technical depth, weak on leadership signals across the board").

### Output B: Per-Candidate Drill-Down

For each candidate (in rank order), write a structured card:

```
──────────────────────────────────────────
👤 [Candidate Name] · Rank #N · Composite: X.X/5 · [Verdict]
──────────────────────────────────────────

MUST-HAVES
✅ [requirement]: [evidence from resume]
❌ [requirement]: [why it fails] ← if disqualified

DIMENSION SCORES
[Dim 1] — [score]/5
  Evidence: [1–2 sentences of specific evidence]
  Gap: [what's missing, if any]

[Dim 2] — [score]/5
  Evidence: ...
  Gap: ...

(repeat for each dimension)

STRENGTHS (top 2)
• [strength with evidence]
• [strength with evidence]

CONCERNS (top 2)
• [concern with evidence]
• [concern with evidence]

RECOMMENDED INTERVIEW FOCUS
If advancing: [the 1–2 things to probe in the interview]
```

---

## Step 6 — Shortlist Summary

After all drill-downs, write a **shortlist recommendation**:

```
SHORTLIST RECOMMENDATION

Advance immediately (🟢): [names]
Worth a closer look (🟡): [names + one-line reason per]
Pass (🔴 / ⛔): [names, one-line reason per]

Hiring manager note: [1 paragraph honest read of the cohort — 
what the pool tells you about candidate availability for this role, 
whether the bar needs adjusting, and what to probe in interviews]
```

---

## Rules

- **Never average scores without weights.** Always use the weighted composite.
- **Never skip the must-have check.** A disqualified candidate must be marked before scoring.
- **Be specific in evidence.** "Has Python experience" is not evidence. "Led a 3-person team rebuilding the data pipeline in Python at Company X" is evidence.
- **Never invent resume content.** If you cannot find evidence for a dimension, score it 1–2 and note "no evidence found."
- **Score consistently.** Calibrate across the batch — a 4 means the same thing for candidate 1 and candidate 12.
- **Always confirm criteria before scoring** (Step 2). Do not proceed without user confirmation.

---

## File Reading Reference

When resumes are uploaded as PDFs or DOCX files, read the `file-reading` SKILL.md at `/mnt/skills/public/file-reading/SKILL.md` to determine the correct extraction method before processing.

---

## Quick Reference: Scoring Rubric Card

| Score | Technical/Tool Fit | Relevant Experience | Career Trajectory |
|---|---|---|---|
| 5 | Exact stack match + advanced usage | 5+ yrs direct domain | Consistent promotion + scope growth |
| 4 | Most tools match + some advanced | 3–5 yrs direct | Clear progression |
| 3 | Partial match, transferable skills | 1–3 yrs or adjacent domain | Some growth, some lateral |
| 2 | 1–2 tools match, mostly learning | <1 yr or tangential | Flat or unclear |
| 1 | No relevant tools | No relevant experience | No signals |
