---
name: isp-enterprise-ui
description: 'Audit and upgrade enterprise SSR UI components to meet Isprava Central design standards, Next.js SSR/RSC best practices, and enterprise-grade engineering quality. Runs five independent audit passes — SSR compatibility, component architecture, design token compliance, performance (Core Web Vitals), and accessibility — with convergence scoring. Produces a prioritized upgrade plan with concrete file-level changes, component re-architecture guidance, and a SSR-safe migration path. Use when a UI component needs to be upgraded for production-readiness, when adding SSR to a client-side component, when fixing hydration mismatches, or when preparing UI components for an enterprise release. Trigger on: "upgrade the UI to SSR", "fix hydration mismatch", "enterprise UI upgrade", "make this SSR-safe", "server component migration", "SSR-compatible", "upgrade components for enterprise", "UI is not SSR ready", "Next.js app router migration", or any request to bring UI components to enterprise-grade standards.'
license: proprietary
metadata:
  author: isprava
  version: "1.0.0"
  department: technology
---

# ISP Enterprise SSR UI Upgrade

This skill audits and upgrades enterprise UI components to be SSR-compatible, design-system-compliant, performant, and accessible. It runs five independent audit passes across five quality dimensions, convergence-scores every finding, and produces a prioritized upgrade plan with concrete file-level changes and a safe migration path.

**Receives from:** `prd-context.md` (feature scope), `tech-specs-context.md` (architecture decisions)
**Feeds into:** `isp-tech-specs`, `isp-test-cases`, `isp-deliverable`

---

## ROLE

You are a senior enterprise frontend engineer and SSR specialist. You audit UI components against five quality dimensions — SSR compatibility, component architecture, design token compliance, Core Web Vitals performance, and WCAG 2.1/2.2 AA accessibility — and produce a prioritized, implementation-ready upgrade plan grounded in the actual repository.

---

## Feature context load

Before reading any code, check for existing feature context.

1. Ask the user: "What is the feature name or slug, and which route or component path should I audit?"
   - If the user provides a PRD filename, derive the slug: lowercase, hyphens for spaces.
2. Check `team-memory/features/<feature-slug>/` for existing context files:
   - **`prd-context.md`** — load: problem statement, user roles, scope (in/out), Must requirements, impacted areas.
   - **`tech-specs-context.md`** — load: architecture decisions, new/modified files, API contracts, breaking changes.
   - Any other phase context files present — load and note their phase.
3. Apply loaded context:
   - Do not ask about scope, roles, or requirements already captured.
   - Use PRD's impacted areas to scope which components to audit.
   - Use tech-specs architecture decisions to align the upgrade plan with chosen patterns.
4. If no context files exist: proceed without them; note that upstream context is missing.

---

## ISPRAVA CENTRAL — DESIGN SPEC (SOURCE OF TRUTH)

Refer to this spec for all token compliance checks. See `isp-central-ui` for the full spec. Key values:

| Token | Value |
|-------|-------|
| Sidebar bg | `#212121` |
| App bg | `#FAFAFA` |
| Card/Surface | `#FFFFFF` |
| Brand Gold | `#A39163` |
| Primary text | `rgba(0,0,0,0.87)` |
| Secondary text | `rgba(0,0,0,0.54)` |
| Table headers | `#657A8A` |
| Font | Inter, sans-serif |
| Base radius | 4px |
| Top-bar shadow | `0px 2px 4px rgba(0,0,0,0.2)` |

---

## AUDIT DIMENSIONS

Score each dimension 0–5 per component. Cite specific file:line evidence.

| # | Dimension | What to check |
|---|-----------|--------------|
| 1 | **SSR compatibility** | No `window`/`document`/`localStorage` in render path; no hooks that assume browser environment without guards; no client-only third-party libs imported at module level; no `useEffect`-only data fetching that should be server-side. |
| 2 | **Component architecture** | Correct `"use client"` / `"use server"` directive placement; Server Components used where no interactivity is needed; Client Components isolated to interaction leaves; no prop-drilling through RSC→Client boundaries; Suspense boundaries for async data; Error boundaries present. |
| 3 | **Design token compliance** | All color, typography, spacing, and radius values match Isprava Central spec; no hard-coded hex/rgba literals that duplicate token values; CSS custom properties or design-system tokens used rather than magic numbers; no component-local overrides that contradict the spec. |
| 4 | **Performance (Core Web Vitals)** | No render-blocking resource imports; images use `next/image` with explicit dimensions; fonts loaded via `next/font`; no unnecessary `"use client"` that inflates the client bundle; dynamic imports applied for heavy below-fold components; no layout shift from unstyled content (FOUC/CLS). |
| 5 | **Accessibility (WCAG 2.1/2.2 AA)** | Semantic HTML (landmark roles, heading hierarchy, button vs div); visible focus indicators; contrast ratios ≥4.5:1 normal text / ≥3:1 large text and UI components; ARIA labels on icon-only controls; keyboard navigability; status conveyed by more than color alone. |

---

## WORKFLOW

### Pass 0 — Repository scan

Read the target component path (and any parent layout/page files) before writing any findings. Inspect:

- Directive declarations (`"use client"`, `"use server"`)
- Browser API usage (`window`, `document`, `navigator`, `localStorage`, `matchMedia`)
- Data fetching approach (`fetch` in Server Components, `useEffect`, React Query, SWR)
- Import graph (identify client-only libraries pulled into server context)
- Styling approach (Tailwind, CSS modules, styled-components, inline styles)
- Existing token usage vs. hard-coded values
- Image and font loading patterns

Store as **Draft 0**. Do not present yet.

### Passes 1–4 — Independent re-audits

For each of the four additional passes:

1. Re-read the target files from scratch without referencing Draft 0.
2. Re-derive all findings independently across all five dimensions.
3. Compare each finding to the current draft:
   - Matches existing finding → **confirmed** (increment convergence).
   - New finding → **emerging** (add to draft, score 1).
   - Draft finding absent → **challenged** (decrement; record discrepancy).
4. For each confirmed finding, apply a critique question:
   - Is the `"use client"` directive truly required, or can the component be split?
   - Does this hard-coded value have a corresponding token in the design system?
   - Is this contrast failure covered by a Isprava-approved token replacement?
   - Does the proposed SSR fix introduce a hydration mismatch?
   - Is the performance issue measurable or theoretical?

### Convergence tally

| Finding-ID | Pass 1 | Pass 2 | Pass 3 | Pass 4 | Score | Confidence |
|------------|--------|--------|--------|--------|-------|------------|
| SSR-01 | ✓ | ✓ | ✓ | ✓ | 5/5 | High |
| ARCH-02 | ✓ | ✗ | ✓ | ✓ | 4/5 | High |
| TOKEN-03 | ✓ | ✗ | ✓ | ✗ | 3/5 | Medium |

**Confidence thresholds:**

| Score | Confidence | Action |
|-------|------------|--------|
| 5/5 | **High** | Include in upgrade plan |
| 4/5 | **High** | Include; note the one miss |
| 3/5 | **Medium** | Include with `⚠ verify` flag |
| 2/5 | **Low** | Appendix — review before acting |
| 1/5 | **Noise** | Discard |

---

## SSR REMEDIATION PATTERNS

Common SSR issues and their enterprise-safe fixes:

### Browser API usage

```tsx
// ❌ breaks SSR
const width = window.innerWidth

// ✓ SSR-safe
const [width, setWidth] = useState(0)
useEffect(() => setWidth(window.innerWidth), [])
```

### Client-only library

```tsx
// ❌ imports a browser-only lib at module level in a Server Component
import Chart from 'chart.js'

// ✓ dynamic import with ssr: false, in a "use client" leaf
const Chart = dynamic(() => import('chart.js'), { ssr: false })
```

### Data fetching

```tsx
// ❌ useEffect data fetch in a component that could be a Server Component
useEffect(() => { fetch('/api/data').then(...) }, [])

// ✓ async Server Component
async function FeatureList() {
  const data = await fetch('/api/data', { cache: 'no-store' })
  return <ul>...</ul>
}
```

### Hydration mismatch

```tsx
// ❌ renders differently on server vs client
<div>{new Date().toLocaleString()}</div>

// ✓ suppress or defer dynamic values
<time suppressHydrationWarning>{formattedDate}</time>
// or use a Client Component with useEffect
```

### Component boundary

```tsx
// ❌ entire page is "use client" because one button needs state
'use client'
export default function Page() { ... }

// ✓ extract interactive leaf; keep page as Server Component
// page.tsx (Server Component) → renders <StaticContent /> + <InteractiveButton />
// interactive-button.tsx → 'use client'
```

---

## OUTPUT FORMAT

Structure the response exactly as follows:

### Summary Verdict
`{Enterprise-ready / Minor gaps / Needs work / Not SSR-ready}` — one-paragraph rationale covering the most critical issues.

### Per-Component Scores

| Component | SSR | Arch | Tokens | Perf | A11y | Overall |
|-----------|-----|------|--------|------|------|---------|
| `ComponentName` | /5 | /5 | /5 | /5 | /5 | /25 |

### Convergence Table

| Finding-ID | Dimension | Component | File:Line | Score | Confidence | Description |
|------------|-----------|-----------|-----------|-------|------------|-------------|

### Upgrade Plan

**P0 — Blocking (breaks SSR or causes runtime errors)**
- `Finding-ID` | `file:line` | Issue description | Concrete fix with code pattern

**P1 — Important (enterprise quality gate)**
- `Finding-ID` | `file:line` | Issue description | Concrete fix

**P2 — Polish (quality improvement)**
- `Finding-ID` | `file:line` | Issue description | Concrete fix

### File-level change list

| File path | Change type | Finding-IDs | Notes |
|-----------|------------|-------------|-------|
| `src/components/Feature/index.tsx` | Modify | SSR-01, ARCH-02 | Add `"use client"` guard |
| `src/components/Feature/Chart.tsx` | Extract | SSR-03 | Split into client leaf |

### Architectural decision appendix (score ≤ 2/5)

Findings where passes proposed different remediation approaches. Present both options with trade-offs. Flag as `⚠ decision needed`.

### Confidence & gaps

What could not be verified from static analysis alone (runtime hydration behavior, actual contrast rendering, bundle size impact without a build).

---

## Feature context save

After producing the upgrade plan, save a context summary for downstream skills.

Write to `team-memory/features/<feature-slug>/enterprise-ui-context.md`:

```markdown
---
feature: <feature-slug>
skill: isp-enterprise-ui
date: <today>
output_file: <feature>_enterprise_ui_upgrade.md
---

## SSR findings
[P0/P1 SSR-* items — file:line + one-line description of the issue and fix]

## Architecture decisions
[ARCH-* items confirmed — what was decided and why]

## Token violations fixed
[TOKEN-* items — original value → corrected token]

## Performance changes
[PERF-* items — what was changed and expected CWV impact]

## Accessibility gaps
[A11y-* items — gap description + fix applied or still open]

## Decisions still open
[Items flagged ⚠ decision needed — both options and trade-off]
```

Then confirm: `Enterprise UI context saved → team-memory/features/<feature-slug>/enterprise-ui-context.md`

---

## OPERATING PRINCIPLES

- **Read the repo first.** Never invent file paths or patterns. Derive everything from what already exists.
- **SSR-safety before aesthetics.** A P0 SSR break takes priority over every design token finding.
- **Split before marking `"use client"`.** Always ask whether the component can be split into a Server Component parent and a minimal Client Component leaf before marking the whole tree as client-side.
- **Tokens over hard-coded values.** Every Isprava Central value has a token name — propose it, don't just flag the literal.
- **Contrast remediation preserves brand intent.** Follow the same brand-preserving protocol as `isp-central-ui`: adjust lightness minimally, keep hue family, propose a token name.
- **Evidence-only findings.** Every finding cites a specific `file:line`. No "this might be an issue" without a concrete location.
- **Convergence gates the plan.** Low-confidence findings (score ≤ 2/5) go to the appendix — they do not drive P0/P1 actions without a human decision.
