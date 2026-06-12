---
name: isp-tech-specs
description: 'Produce grounded technical specifications — file-level change list, component hierarchy, API contracts, state management approach, and migration plan — derived from the implementation checklist and the actual codebase. Runs five independent specification passes and scores each spec item by convergence. Only specs that re-emerge consistently are included in the verified spec document. Use after isp-checklist to produce implementable technical guidance. Trigger on: "write the technical spec", "what files need to change", "define the API contract", "component hierarchy", "state management plan", or as the eighth step in the isp-feature-analysis workflow.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# ISP Technical Specs

This skill produces technical specifications grounded in the actual repository across five independent passes. Spec items that re-emerge consistently are high-confidence; items that vary between passes indicate architectural ambiguity that needs resolution before implementation. Specs are derived from the checklist and the real codebase — not invented patterns.

**Receives from:** `isp-checklist` (CL items and complexity tiers), `isp-gap-analysis` (GAP register)
**Feeds into:** `isp-effort-estimate`, `isp-deliverable`

---

## Feature context load

Before reading the repository or generating any specs, check for existing feature context.

1. Ask the user: "What is the feature name or slug? I'll check for existing PRD and analysis context."
   - If the user provides a PRD filename, derive the slug: lowercase, hyphens for spaces.
2. Check `team-memory/features/<feature-slug>/` for existing context files:
   - **`prd-context.md`** — load: problem statement, user roles, scope (in/out), Must requirements, open questions, impacted areas, upstream dependencies.
   - **`checklist-context.md`** — load: CL items, complexity tiers, items flagged for review.
   - Any other phase context files present — load and note their phase.
3. Apply loaded context:
   - Do not ask about scope, roles, or requirements already captured in `prd-context.md`.
   - Use the PRD's open questions to flag `⚠ architectural decision needed` items in the spec.
   - Use PRD's impacted areas to ensure the file-level change list covers all affected components.
4. If no context files exist: proceed without them; note that upstream context is missing and the user may want to run `isp-prd-builder` first.

---

## Spec domains

| Domain | What to specify |
|--------|----------------|
| File-level changes | New files, modified files, deleted files with proposed paths |
| Component hierarchy | Component tree, parent/child relationships, props contracts |
| API contracts | Request/response shapes, HTTP methods, auth, error codes |
| State management | State slices, context providers, derived state — must match repo conventions |
| Utilities and hooks | Reusable helpers, custom hooks, design-system additions |
| Migration plan | Backwards-compatibility, data migration, feature-flag phasing |
| Risks and mitigations | Technical unknowns, dependencies, breaking-change risks |

---

## Workflow

### Pass 0 — Initial spec generation

Read the actual repository before writing any specs. Inspect:
- Directory structure and naming conventions
- Existing component patterns and props contracts
- State management approach (Redux, Zustand, Context, etc.)
- Data fetching patterns (REST, GraphQL, SWR, React Query, etc.)
- Styling approach (CSS modules, Tailwind, styled-components, etc.)
- Routing conventions

Then, for each confirmed CL item, derive the corresponding spec. Assign IDs:
- `SPEC-F-01`, ... — file-level changes
- `SPEC-C-01`, ... — component hierarchy
- `SPEC-A-01`, ... — API contracts
- `SPEC-S-01`, ... — state management
- `SPEC-M-01`, ... — migration
- `SPEC-R-01`, ... — risks

Store as **Draft 0**. Do not present yet.

### Passes 1–4 — Independent re-inspections

For each of the four additional passes:

1. Re-read the repository and checklist from scratch without referencing Draft 0.
2. Re-derive all spec items independently.
3. Compare each item to the current draft:
   - Matches existing SPEC item → **confirmed**.
   - New spec item → **emerging**.
   - Draft item absent or different → **challenged** — record both versions.
4. Apply critique questions to each confirmed item:
   - Does this spec item follow the repo's existing conventions, or introduce a new pattern?
   - Is the proposed file path consistent with how similar files are organized today?
   - Does the API contract match what the backend already exposes, or does it require a new endpoint?
   - Is the state management approach consistent with how similar state is managed in the repo?
   - Does this spec item introduce a breaking change? If so, is the migration plan adequate?
5. Update the **convergence tally**.

### Convergence tally

| SPEC-ID | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Confidence |
|---------|--------|--------|--------|--------|-------|------------|
| SPEC-F-01 | ✓ | ✓ | ✓ | ✓ | 5/5 | High |
| SPEC-A-03 | ✓ | ✗ | ✓ | ✗ | 3/5 | Medium |
| SPEC-S-02 | ✗ | ✗ | ✓ | ✗ | 2/5 | Low |

For spec items where passes **disagree on the approach** (not just presence), record both approaches and flag as `⚠ architectural decision needed`.

**Confidence thresholds:**

| Score | Confidence | Action |
|-------|------------|--------|
| 5/5 | **High** | Include in verified spec document |
| 4/5 | **High** | Include; note the one miss |
| 3/5 | **Medium** | Include with `⚠ verify approach` flag |
| 2/5 | **Low** | Appendix — architectural alternative |
| 1/5 | **Noise** | Discard |

---

## Final output

### File-level change list

| File path | Change type | Linked CL | Notes |
|-----------|------------|-----------|-------|
| `src/components/Feature/index.tsx` | New | CL-01 | |
| `src/pages/FeaturePage.tsx` | Modify | CL-03 | |

### Component hierarchy

```
<FeaturePage>
  ├── <FeatureHeader props: { title, subtitle } />
  ├── <FeatureBody>
  │     ├── <ItemCard props: { id, title, status, onClick } />  [CL-01]
  │     └── <EmptyState props: { message } />  [CL-04]
  └── <FeatureFooter />
```

### API contracts

| SPEC-ID | Endpoint | Method | Request | Response | Auth | Linked CL |
|---------|----------|--------|---------|----------|------|-----------|

### State management

| SPEC-ID | State slice / context | Shape | Mutations | Linked CL |
|---------|-----------------------|-------|-----------|-----------|

### Migration plan

| SPEC-ID | Change | Migration approach | Breaking? | Rollback plan |
|---------|--------|--------------------|-----------|---------------|

### Risks and mitigations

| SPEC-ID | Risk | Likelihood | Impact | Mitigation | Score |
|---------|------|------------|--------|------------|-------|

### Architectural decision appendix (score 2/5)

Spec items where passes proposed different approaches. These need a team decision before implementation. Present both options with trade-offs.

---

## Feature context save

After producing the verified spec document, save a context summary for downstream skills (test cases, effort estimation).

Write to `team-memory/features/<feature-slug>/tech-specs-context.md`:

```markdown
---
feature: <feature-slug>
skill: isp-tech-specs
date: <today>
output_file: <feature>_tech_specs.md
---

## Architecture decisions
[Bullet per decision: what was chosen and why — pattern, library, approach]

## New files
[SPEC-F items with Change=New — path + one-line purpose]

## Modified files
[SPEC-F items with Change=Modify — path + what changes]

## API contracts
[SPEC-A items — METHOD /endpoint — brief description of what it does]

## Breaking changes
[SPEC-M items flagged Breaking=Yes — what breaks and what the migration requires]

## Risks flagged
[SPEC-R items with High likelihood or High impact — risk + mitigation]

## Architectural decisions still open
[Items flagged ⚠ architectural decision needed — both options and the trade-off]
```

Then confirm: `Tech spec context saved → team-memory/features/<feature-slug>/tech-specs-context.md`

---

## Operating principles

- **Read the repo first.** Never invent file paths, component names, or API patterns. Derive everything from what already exists.
- **No new libraries without explicit PRD justification.** If the PRD does not require a new dependency, do not add one.
- **Convention over invention.** If the repo uses a pattern, follow it — even if a "better" pattern exists.
- **Architectural conflicts are escalation items.** When passes disagree on approach, do not pick one arbitrarily — surface both and let the team decide.
- **Every spec item links to a CL item.** Specs without a checklist trace are scope additions — flag them.
