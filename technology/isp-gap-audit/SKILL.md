---
name: isp-gap-audit
description: 'Deep gap and ambiguity audit between a PRD, a Figma design, and the actual codebase. Inputs are repository name/path, PRD path, and Figma path. Produces a confidence-ranked finding list by running five independent analysis passes and checking which gaps appear consistently across all passes. Use when the user says "find gaps", "what is ambiguous in this PRD", "does the code match the PRD", "does Figma match the spec", "audit the PRD against code", "verify implementation against requirements", or any request that pairs a PRD with code OR Figma and asks for discrepancies, ambiguities, or missing pieces — even without the word "gap". Distinct from isp-feature-analysis: this skill produces no implementation plan — only a high-confidence gap and ambiguity register.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# PRD Gap & Ambiguity Audit

This skill runs a focused, iterative audit across two comparison axes — **PRD ↔ Code** and **PRD ↔ Figma** — and stress-tests every finding through five independent passes. Only findings that survive self-critique and re-emerge across passes are reported as high-confidence. The output is a ranked gap register, not an implementation plan.

Use this skill when you need to know **what is wrong or unclear**, not yet how to fix it.

---

## When to use this skill vs `isp-feature-analysis`

| Question | Use this skill | Use `isp-feature-analysis` |
|----------|---------------|--------------------------|
| "What gaps exist between PRD and code?" | Yes | No |
| "Are there ambiguities in the PRD?" | Yes | No |
| "Does Figma match what the PRD says?" | Yes | No |
| "Build me an implementation checklist" | No | Yes |
| "What are the test cases for this feature?" | No | Yes |
| "I need a full deliverable doc" | No | Yes |

---

## Inputs

| Input | Required? | Notes |
|-------|-----------|-------|
| Repository name or local path | Yes | Used to read actual code |
| PRD path (`.md`, `.pdf`, `.docx`, Notion/Confluence link) | Yes | Primary source of truth for requirements |
| Figma path, link, or exported frames | Yes | Design source of truth |

If any input is missing, ask for it before starting. Do not substitute or assume.

---

## Workflow

Run all phases in order. Do not skip. The five-pass loop in Phase 4 is the core of this skill — do not collapse it into a single pass.

---

### Phase 1 — Intake

1. Read the PRD in full before asking any questions.
2. Inspect the repository: directory structure, key feature files, component tree.
3. Inspect the Figma: enumerate screens, states, and components visible in the provided frames or link.
4. Echo back a **Confirmed Inputs** summary:
   - Repository: `<name>` at `<path>`
   - PRD: `<filename>` — `<N>` requirements extracted on first read
   - Figma: `<N>` screens / frames identified
5. Ask: "Should I proceed with the full 5-pass audit, or do you want to review inputs first?"

---

### Phase 2 — Axis A: PRD ↔ Code (Pass 0 — first read)

Walk every requirement in the PRD. For each one, check whether the codebase implements it, partially implements it, or does not implement it. Also flag any code behavior that has no backing requirement (undocumented behavior = potential ambiguity in the PRD).

Produce an initial finding list using this format:

| ID | Requirement (from PRD) | Code Status | Gap Type | Severity | Notes |
|----|------------------------|-------------|----------|----------|-------|
| A-01 | ... | Missing / Partial / Present / Undocumented | `Gap` / `Ambiguity` / `Conflict` / `Undocumented` | Blocker / High / Medium / Low | ... |

**Gap types:**
- `Gap` — requirement exists in PRD but not implemented in code
- `Ambiguity` — requirement is vague, unmeasurable, or contradicted elsewhere in the PRD
- `Conflict` — PRD says X, code does Y in a way that may be intentional
- `Undocumented` — code behavior exists with no PRD backing (may be intentional or stale)

**Severity rubric:**
- `Blocker` — core user flow broken or undefined
- `High` — important feature missing or misaligned, workaround exists but is poor
- `Medium` — secondary behavior differs; user experience degraded but not broken
- `Low` — cosmetic, copy, or edge case difference

Store this as **Draft A** (not the final output yet).

---

### Phase 3 — Axis B: PRD ↔ Figma (Pass 0 — first read)

Walk every requirement in the PRD. For each one, check whether the Figma design accounts for it. Also enumerate everything visible in Figma that has no PRD requirement behind it.

Produce an initial finding list:

| ID | Requirement (from PRD) | Figma Status | Gap Type | Severity | Notes |
|----|------------------------|--------------|----------|----------|-------|
| B-01 | ... | Missing / Partial / Present / Extra | `Gap` / `Ambiguity` / `Conflict` / `Extra` | Blocker / High / Medium / Low | ... |

**Extra** = Figma shows something the PRD never mentions (design drift, undocumented decision, or rogue addition).

Store this as **Draft B**.

---

### Phase 4 — Five-Pass Critique Loop

This is the core mechanism. Run five independent passes. In each pass:

1. **Re-read** the PRD, code, and Figma independently — do not reference your previous draft.
2. **Generate** a fresh finding list for both axes from scratch.
3. **Compare** each new finding against Draft A / Draft B:
   - Does this finding appear in the draft? Mark it as **confirmed**.
   - Is this a new finding? Add it as **emerging**.
   - Is a previous finding absent this pass? Mark it as **challenged**.
4. **Critique** each confirmed finding: ask "Could this actually be intentional, documented elsewhere, or a misread?" If yes, downgrade severity or reclassify.
5. After each pass, update a **convergence tally**.

#### Convergence tally format

| Finding ID | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Pass 5 | Score | Confidence |
|------------|--------|--------|--------|--------|--------|-------|------------|
| A-01 | ✓ | ✓ | ✓ | ✓ | ✓ | 5/5 | High |
| A-03 | ✓ | ✗ | ✓ | ✗ | ✓ | 3/5 | Medium |
| B-02 | ✓ | ✓ | ✗ | ✗ | ✗ | 2/5 | Low |

**Confidence thresholds:**

| Score | Confidence | Meaning |
|-------|------------|---------|
| 5/5 | **High** | Finding is real and consistent. Report it. |
| 4/5 | **High** | Near-certain. Report it with a note on the one miss. |
| 3/5 | **Medium** | Possible gap. Report it with a flag — needs human verification. |
| 2/5 | **Low** | Inconsistent finding. Include in an appendix as "potential noise". |
| 1/5 | **Noise** | Appeared once, not reproducible. Discard. |

#### Critique questions for each pass

Ask these for every finding before scoring it:
1. Could this be intentional (a product decision not documented in the PRD)?
2. Is there a different section of the PRD or codebase that resolves this?
3. Is this finding about the PRD being ambiguous, or about the implementation being wrong? (Separate these clearly.)
4. If I were the product manager who wrote this PRD, would I recognize this as a gap?
5. If I were the engineer who wrote this code, would I recognize this as a discrepancy?

---

### Phase 5 — Final Gap Register

Present only findings with confidence **Medium or above** (score ≥ 3/5). Organize by axis, then by severity.

#### Axis A: PRD ↔ Code

| ID | Requirement | Gap Type | Severity | Score | What's Missing or Wrong | Owner |
|----|-------------|----------|----------|-------|--------------------------|-------|
| A-01 | ... | Gap | High | 5/5 | ... | Engineering |
| ... | | | | | | |

#### Axis B: PRD ↔ Figma

| ID | Requirement | Gap Type | Severity | Score | What's Missing or Wrong | Owner |
|----|-------------|----------|----------|-------|--------------------------|-------|
| B-01 | ... | Ambiguity | Blocker | 5/5 | ... | Product |
| ... | | | | | | |

#### Ambiguity register

Collect every PRD statement that is vague, unmeasurable, or internally contradicted, regardless of which axis surfaced it:

| Amb-ID | PRD Statement | Why It's Ambiguous | What Needs Clarification | Score |
|--------|--------------|-------------------|--------------------------|-------|
| Amb-01 | "The page should load quickly" | No performance target defined | Define P95 load time in ms | 5/5 |

#### Discarded findings (noise)

List any findings that scored 1/5 or 2/5 in a collapsed appendix. Keep these brief — they are signals, not conclusions.

---

### Phase 6 — Summary

Close with a short summary block:

```
Audit summary
─────────────
Axes analyzed       : PRD ↔ Code | PRD ↔ Figma
Passes completed    : 5
Total findings      : N
  High confidence   : N (Blocker: X | High: X | Medium: X | Low: X)
  Medium confidence : N (needs human verification)
  Discarded (noise) : N

Top 3 findings:
1. [A-XX] <one-line description> — Severity: Blocker | Confidence: 5/5
2. [B-XX] <one-line description> — Severity: High | Confidence: 5/5
3. [Amb-XX] <one-line description> — Severity: High | Confidence: 4/5

Recommended next step: resolve Amb-01 with the product owner before any
implementation begins — three high-confidence findings depend on its
clarification.
```

---

## Operating principles

- **Re-read each pass independently.** Do not reference previous pass outputs when generating findings — look at the source material directly. Cross-reference only when building the tally.
- **Separate "PRD is ambiguous" from "code is wrong".** These require different owners and different fixes.
- **Never invent a finding.** If you cannot point to a specific PRD line, code file + line, or Figma frame, it is not a finding.
- **Mark assumptions explicitly.** If you infer intent, tag it `[ASSUMPTION]`. Inferences are hypotheses, not findings.
- **Owner assignment is mandatory.** Every finding must name an owner: `Product` (PRD needs clarification), `Design` (Figma needs update), or `Engineering` (code needs change). Unowned findings drift.
- **High confidence does not mean high severity.** A 5/5 Low finding is a real but minor issue. A 3/5 Blocker is a potential showstopper that needs human eyes.

---

## Common mistakes

| Mistake | Why it fails | Fix |
|---------|-------------|-----|
| Running one pass and calling it done | Single-pass findings have high false-positive rates — misreads, ambiguous phrasing, and scope mismatches are common | Always run all 5 passes |
| Reporting noise findings as findings | Wastes stakeholder attention and erodes trust in the audit | Discard 1/5 findings; clearly flag 2/5 |
| Conflating "ambiguous PRD" with "wrong implementation" | Different problem, different fix, different owner | Always classify gap type and owner separately |
| Including implementation suggestions | This skill produces a gap register, not a plan | Remove any "should be implemented as..." language from findings |
| Skipping the critique questions in Phase 4 | Without active challenge, confirmation bias inflates scores | Ask all 5 critique questions for every finding, every pass |

---

## Quick diagnostic

| Question | If No | Action |
|----------|-------|--------|
| Did I read the full PRD before Phase 2? | Risk of missed requirements | Read the full PRD — do not skim |
| Did each of the 5 passes re-read source material independently? | Confirmation bias inflates scores | Re-run passes that referenced earlier output |
| Does every finding have a PRD line number or code location? | Finding is ungrounded | Add the reference or discard |
| Does every finding have an owner? | Gap will go unresolved | Assign Product / Design / Engineering |
| Are "ambiguous PRD" and "wrong code" findings in separate rows? | Root causes mixed up | Split into two rows with different owners |
