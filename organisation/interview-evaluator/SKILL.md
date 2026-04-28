---
name: interview-evaluator
description: >
  Generates a complete, structured interview evaluation framework for any role, candidate, and set of evaluation dimensions.
  Use this skill whenever a user shares a job description and a resume and wants to run a structured interview, or wants to know
  how to evaluate a candidate, or asks for an interview plan, interview questions, a scorecard, evaluation criteria, or a hiring framework.
  Also triggers when a user says things like "help me interview this person", "how should I evaluate this candidate",
  "create an interview process for this role", "I have a round 2 interview to conduct", or shares a JD + resume and asks what to look for.
  Always use this skill — do not attempt to improvise an interview framework without it.
---

# Interview Evaluator Skill

Generates a complete interview evaluation system: timed blocks, per-block questions, what-to-listen-for, green flags, red flags, nudge tips, and a live interactive scorecard — all calibrated to a specific JD, resume, and set of evaluation dimensions.

## What this skill produces

Two outputs, always both:
1. A **written pre-brief** (in your response text) — your honest read of the candidate against the role before the interview starts
2. An **interactive HTML widget** — the run sheet with a live block timer, per-block questions, flags, nudge tips, and a weighted scorecard

---

## Step 1 — Extract inputs

Before generating anything, identify these five things from the conversation. If any are missing, ask for them explicitly.

| Input | What to extract | What to do if missing |
|---|---|---|
| **JD / Role description** | Role title, core responsibilities, team context, what "good execution" looks like in this role | Ask: "Can you paste the job description or describe the role in a few sentences?" |
| **Resume** | Candidate name, education, tools/skills, projects, work experience, gaps or flags | Ask: "Can you share the candidate's resume?" |
| **Evaluation dimensions** | 3–6 named dimensions the hiring manager cares about, with weights (or derive them from the JD if not given) | Derive from JD — see Step 2 |
| **Interview duration** | Total time in minutes | Default to 45 min if not specified |
| **Hiring manager context** | What the HM will own vs delegate, what they'll define vs what the candidate executes | Extract from their description of the role; ask if unclear |

---

## Step 2 — Derive evaluation dimensions (if not given)

If the hiring manager has not named the dimensions explicitly, derive 4–6 from the JD and role context using this logic:

- **Execution-heavy roles** (coordinators, analysts, ops): Weight execution orientation highest (25–30%), tech/tool fluency second
- **Research-heavy roles** (strategy, consulting, policy): Weight research quality and synthesis highest, learning agility second
- **Technical roles** (engineering, data): Weight tech depth highest, problem decomposition second
- **Customer-facing roles** (sales, CS, BD): Weight communication and stakeholder instinct highest
- **Generalist / ambiguous roles**: Weight learning agility and first-principles thinking highest

Always include one dimension that probes the known gap from the resume — something the candidate has not demonstrated yet that the role requires.

Name each dimension clearly. Assign weights that sum to 100%.

---

## Step 3 — Write the pre-brief (response text, before the widget)

Write 4 paragraphs in your response text. This is the hiring manager's honest read of the candidate before they walk in.

**Paragraph 1 — Resume read for this role**
What does this resume actually say about fit for this specific role? Not generic strengths — specifically what in their background maps to what the role requires, and what is conspicuously absent.

**Paragraph 2 — The key unknown**
The one thing the resume cannot tell you — the dimension where the entire bet is on the interview. Name it. Explain why the resume leaves it open.

**Paragraph 3 — The specific risk**
What is the downside scenario if you hire this person and they do not work out? What early signal would you have missed? This sharpens what to probe for.

**Paragraph 4 — The bet**
If you hire this person, what are you actually betting on? Name it explicitly — it clarifies the interview's job.

---

## Step 4 — Design the interview blocks

Structure the full interview into 4–6 timed blocks. Every interview must include:

| Block type | Purpose | Typical duration |
|---|---|---|
| Opening | Rapport + first signal | 4–6 min |
| Dimension probes (2–4 blocks) | One block per key dimension | 7–12 min each |
| Live task simulation | Cold task, observed process | 10–15 min |
| Close + candidate questions | Signal from what they ask | 4–6 min |

**Allocation rules:**
- Live task simulation always gets the most time of any single block (min 10 min, max 15 min)
- Opening and close are always the two shortest blocks
- Blocks must sum exactly to the interview duration
- Never put the live task first — always after at least one warm-up block

**For each block, define:**
1. Block title and time allocation (e.g., "Min 1–6, 6 min")
2. The dimension(s) it evaluates and weight
3. Goal of the block (1–2 sentences — what you are trying to find out)
4. The key insight (1 sentence — what this block tells you that no prepared answer can fake)
5. 2–3 questions with exact wording
6. For each question: what to listen for (specific signals, not generic advice)
7. 3–4 green flags
8. 3–4 red flags
9. A "if they stall" nudge — what to say to push without giving the answer away

---

## Step 5 — Write the live task simulation

This is the most important block. It must always be a cold, real task — not a hypothetical opinion question.

**Task design rules:**
- Task must be something the candidate could genuinely be asked to do in week 1–2 of the role
- Must have an observable output format (a document, comparison, recommendation, or plan)
- Must be completable in 48 hours with public information
- Task should expose how they structure ambiguity, not whether they know the answer

**Three probes always required inside the task block:**
1. Task drop — give the task verbatim, then stop talking. Watch the first 30 seconds.
2. Source probe — "Where specifically would you start? Not Google — what is the first thing you would actually open?"
3. Output probe — "What does the thing you hand me actually look like? Describe the document."

**Watch at task drop:**
- Does the candidate ask a clarifying question before answering? (strong signal)
- Do they define the output format themselves before being asked? (strong signal)
- Do they describe a process or jump straight to content? (process = execution instinct)

---

## Step 6 — Generate the interactive widget

After writing the pre-brief in response text, call `show_widget` with a fully self-contained HTML widget.

### Required widget components

**Timeline bar** — A proportional colored bar across the top. Each segment is clickable and navigates to that block.

Color assignment by block type (not sequential):
- Opening block: `#888780` (gray)
- Dimension probe blocks: assign from `#534AB7` (purple), `#0F6E56` (teal), `#D85A30` (coral), `#BA7517` (amber) in that order
- Live task block: `#993C1D` (deep red — always most visually prominent)
- Close block: `#888780` (gray)

**Block navigation** — Pill buttons below the timeline, one per block, active block highlighted.

**Live block timer** — MM:SS counting up from 0. Start / Pause / Reset. Turns red when block time is exceeded. Resets on block switch.

**Per-block card** — shows:
- Block title + time range badge + dimension badge
- Goal (2 sentences max)
- Key insight (bolded)
- Questions with what-to-listen-for
- Green flags panel + Red flags panel (side by side grid)
- Nudge tip box with purple left-border accent (only if block has a tip)

**Summary / Scorecard tab** (always the last tab):
- One row per dimension: name, weight percentage, score
- 5-button rating per dimension (1–5), fills amber when selected
- Weighted score auto-calculates as candidate rates each dimension
- Verdict auto-generates:
  - Score >= 4.0: "Strong hire signal. Proceed to offer stage."
  - Score >= 3.0: "Lean hire — check which dimensions pulled the score down."
  - Score < 3.0: "Pass. Candidate does not meet the bar for this role."
- Automatic disqualifiers section at the bottom (2–3 role-specific hard stops)

### Widget data structure (JS)

```js
const blocks = [
  {
    id: 0,
    title: "Block title",
    minutes: 6,
    color: "#888780",
    dim: "Dimension name · weight%",
    dimColor: "#F1EFE8",
    dimText: "#444441",
    goal: "What you are trying to find out in this block.",
    insight: "What this block reveals that a prepared answer cannot fake.",
    questions: [
      {
        n: "Q label",
        q: "Exact question wording in quotes.",
        listen: "What to listen for. Use <span>Strong:</span> and <span>Weak:</span> inline."
      }
    ],
    green: ["Green flag 1", "Green flag 2", "Green flag 3"],
    red: ["Red flag 1", "Red flag 2", "Red flag 3"],
    tip: "If they stall, say this..." // omit key if no tip needed
  }
];

const weights = [0.25, 0.25, 0.25, 0.15, 0.10]; // must sum to 1.0, one per scored dimension
```

### Widget implementation rules
- All CSS must use `var(--color-*)` and `var(--border-radius-*)` tokens — dark mode mandatory
- No hardcoded colors on text or backgrounds except timeline segment fills
- No external dependencies
- Timer: `setInterval` counting up, red when `timerSeconds >= blocks[current].minutes * 60`
- Scorecard: `scores[]` array, rated[] boolean array, weighted sum on each rating click
- Summary tab is always index 5 (or last index) — not scored by the timer

See `references/widget-template.md` for the base HTML/JS scaffolding.

---

## Step 7 — Automatic disqualifiers

At the bottom of the Summary tab, list 2–3 automatic disqualifiers specific to this role. These are answers or behaviours that — regardless of overall score — should stop the hire. Derive from:

- The single most critical dimension (if they fail this, nothing else matters)
- The key gap from the resume (if the gap turns out to be a wall, not a bridge)
- The live task simulation (no structured output + no process = automatic pass for execution roles)

---

## Output checklist — verify before finishing

- [ ] Pre-brief written in response text (4 paragraphs, not inside widget)
- [ ] Widget has proportional timeline bar, clickable segments
- [ ] Widget has live block timer, turns red on overrun, resets on tab switch
- [ ] Every block has: goal, key insight, at least 2 questions, what-to-listen-for, green flags, red flags
- [ ] Live task block has all three probes: task drop, source probe, output probe
- [ ] Summary tab has weighted scorecard with auto-verdict and disqualifiers
- [ ] Automatic disqualifiers are role-specific, not generic
- [ ] Block times sum exactly to interview duration
- [ ] Widget is fully self-contained HTML

---

## Common mistakes to avoid

- Do not write generic questions. Every question must be calibrated to the specific resume. If the candidate has SQL experience, the tech probe uses their SQL context, not a generic database question.
- Do not make the live task a hypothetical. "What would you do if..." is not a live task. A live task is: "Here is the task. Walk me through exactly how you would do it starting now."
- Do not assign equal weights to all dimensions. Weights must reflect what actually matters in this role.
- Do not make green/red flags generic. "Good communication" is not a green flag. "Asks a clarifying question before answering the task drop" is a green flag.
- Do not bury the live task. It always gets the most time. It never goes last. It never goes first.
- Do not skip the pre-brief. The widget is the run sheet. The pre-brief is the judgment that makes the run sheet mean something.
