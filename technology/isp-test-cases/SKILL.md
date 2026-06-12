---
name: isp-test-cases
description: 'Generate comprehensive test cases covering unit, integration, E2E, visual regression, responsive, accessibility, and edge cases — derived from the verified gap register and implementation checklist. Runs five independent generation passes and scores each test case by convergence. Only test cases that re-emerge consistently are included in the verified test suite. Use after isp-gap-analysis and isp-checklist to produce the test plan. Trigger on: "write test cases", "what should we test", "test coverage", "define the test suite", or as the seventh step in the isp-feature-analysis workflow.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP Test Cases

This skill generates test cases from the verified gap register and checklist across five independent passes. Test cases that re-emerge consistently across passes are high-confidence coverage items. Cases that only appear once are either edge cases worth keeping or noise — convergence scoring separates the two. Every test case links back to at least one requirement or checklist item.

**Receives from:** `isp-gap-analysis` (verified gap table), `isp-checklist` (CL items and linked GAP-IDs), `isp-prd-analysis` (REQ register)
**Feeds into:** `isp-deliverable`

---

## Feature context load

Before generating any test cases, check for existing feature context accumulated by upstream skills.

1. Ask the user: "What is the feature name or slug? I'll load context from the PRD and tech spec phases."
   - Derive the slug from any filename the user provides.
2. Check `team-memory/features/<feature-slug>/` for existing context files:
   - **`prd-context.md`** — load: user roles, Must requirements, acceptance criteria, scope, open questions, impacted areas. Use the REQ register here if no separate `isp-prd-analysis` output is provided.
   - **`tech-specs-context.md`** — load: API contracts (each needs integration tests), breaking changes (each needs a regression test), risks (each needs an edge case test), new files (each needs unit tests).
   - **`checklist-context.md`** — load: CL items and complexity tiers to ensure test coverage matches implementation scope.
3. Apply loaded context:
   - For every Must requirement in `prd-context.md` — ensure at least one test case links to it.
   - For every breaking change in `tech-specs-context.md` — ensure at least one regression test exists.
   - For every High-risk item in `tech-specs-context.md` — ensure at least one edge case test exists.
   - For every API contract in `tech-specs-context.md` — ensure at least one integration test exists.
   - Do not ask about scope, roles, or requirements already captured in loaded context.
4. If no context files exist: proceed with what the user provides directly; note that upstream context is missing.

---

## Test types to cover

| Type | What to test |
|------|-------------|
| `Unit` | Individual functions, components, utilities in isolation |
| `Integration` | Component interactions, API calls, state flows |
| `E2E` | Full user flows from entry to outcome |
| `Visual regression` | Component renders match design at all breakpoints |
| `Responsive` | Layout at each Figma breakpoint (375 px, 768 px, 1440 px, etc.) |
| `Accessibility` | Keyboard navigation, focus order, ARIA labels, screen reader flow, contrast ratios |
| `Edge case` | Empty state, error state, slow network, very long content, missing images, RTL |

---

## Workflow

### Pass 0 — Initial generation

Using the REQ register, gap table, and checklist, generate test cases. Assign IDs:
- `TC-U-01`, `TC-U-02`, ... — unit tests
- `TC-I-01`, ... — integration tests
- `TC-E-01`, ... — E2E tests
- `TC-V-01`, ... — visual regression
- `TC-R-01`, ... — responsive
- `TC-A-01`, ... — accessibility
- `TC-X-01`, ... — edge cases

For each test case:

| TC-ID | Title | Preconditions | Steps | Expected result | Type | Priority | Linked REQ / CL |
|-------|-------|---------------|-------|-----------------|------|----------|-----------------|

- **Priority:** `P1 Must` / `P2 Should` / `P3 Nice-to-have`
- **Linked REQ / CL:** Every test case links to at least one `REQ-XX` or `CL-XX`

Store as **Draft 0**. Do not present yet.

### Passes 1–4 — Independent re-generations

For each of the four additional passes:

1. Re-read the REQ register, gap table, and checklist from scratch without referencing Draft 0.
2. Independently generate the full test suite.
3. Compare each test case to the current draft:
   - Matches an existing TC → **confirmed**.
   - New test case → **emerging** (possible coverage gap caught by this pass).
   - Draft TC absent → **challenged**.
4. Apply critique questions to each confirmed test case:
   - Does this test case verify a user-visible outcome, or just internal implementation?
   - Is the expected result specific and binary (pass/fail), or vague?
   - Is this test case linked to a confirmed REQ or CL item, or derived from an open question?
   - Would this test case catch the regression scenario flagged in `isp-current-state`?
   - Is this covered by a higher-priority test type (e.g., is a unit test redundant if an E2E covers it)?
5. Update the **convergence tally**.

### Convergence tally

| TC-ID | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Confidence |
|-------|--------|--------|--------|--------|-------|------------|
| TC-E-01 | ✓ | ✓ | ✓ | ✓ | 5/5 | High |
| TC-A-03 | ✓ | ✗ | ✓ | ✗ | 3/5 | Medium |
| TC-X-07 | ✗ | ✗ | ✓ | ✗ | 2/5 | Low |

**Confidence thresholds:**

| Score | Confidence | Action |
|-------|------------|--------|
| 5/5 | **High** | Include in verified test suite |
| 4/5 | **High** | Include; note the one miss |
| 3/5 | **Medium** | Include with `⚠ review coverage` flag |
| 2/5 | **Low** | Appendix — edge case candidate |
| 1/5 | **Noise** | Discard |

---

## Final output

### Verified test suite (confidence ≥ 3/5)

| TC-ID | Title | Preconditions | Steps | Expected result | Type | Priority | Score | Linked REQ / CL |
|-------|-------|---------------|-------|-----------------|------|----------|-------|-----------------|

### Coverage matrix

Verify that every confirmed REQ-ID and high-confidence CL-ID has at least one linked test case:

| REQ-ID / CL-ID | Test cases linked | Coverage status |
|----------------|------------------|-----------------|
| REQ-01 | TC-E-01, TC-U-03 | Covered |
| REQ-05 | — | ⚠ Not covered |

Any uncovered REQ or CL item is a coverage gap — add a test case or flag for the team to decide if coverage is needed.

### Test suite summary

```
Total test cases    : N
  Unit              : N (P1: X | P2: X | P3: X)
  Integration       : N
  E2E               : N
  Visual regression : N
  Responsive        : N (per breakpoint: 375px: X | 768px: X | 1440px: X)
  Accessibility     : N
  Edge cases        : N

Medium-confidence (⚠ review coverage): N
Uncovered requirements: N (see coverage matrix)
```

### Edge case appendix (score 2/5)

Test cases seen in some passes — may represent valuable edge case coverage. Include for team review.

---

## Feature context save

After producing the verified test suite, save a context summary for downstream skills (deliverable, retrospectives).

Write to `team-memory/features/<feature-slug>/test-cases-context.md`:

```markdown
---
feature: <feature-slug>
skill: isp-test-cases
date: <today>
output_file: <feature>_test_cases.md
---

## Coverage summary
Total: N | Unit: N | Integration: N | E2E: N | Visual: N | Responsive: N | A11y: N | Edge: N

## Uncovered requirements
[REQ-IDs with no linked test case — with note on whether the team decided to skip or left unresolved]

## Regression risks covered
[TC items explicitly covering components flagged Regression-Risk in upstream context]

## High-priority edge cases
[TC-X items with P1 Must priority — title + expected result]

## Accessibility gaps
[Any accessibility requirement with no corresponding TC-A item]

## Open questions inherited from upstream
[Questions from prd-context.md or tech-specs-context.md that affected test design — and how they were handled]
```

Then confirm: `Test case context saved → team-memory/features/<feature-slug>/test-cases-context.md`

---

## Operating principles

- **Every TC links to a REQ or CL.** Tests without a traceability link are unverifiable against requirements. Add the link or discard the test.
- **Expected results are binary.** "The page loads correctly" is not a valid expected result. "The page renders within 2 s on a 3G connection and displays all product cards" is.
- **Accessibility is not optional.** Every feature must have at least one keyboard-navigation test and one screen-reader/ARIA test.
- **Visual regression per breakpoint.** A visual test that only runs at one viewport is not visual regression testing.
- **Regression-Risk items get priority.** Any component flagged Regression-Risk in `isp-current-state` must have at least one E2E or integration test covering its existing behaviour.
