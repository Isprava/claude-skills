---
name: isp_central_ui
description: 'Audit a UI screenshot and its source implementation against the Isprava Central design language and enterprise-grade standards (Microsoft Fluent 2 and Salesforce Lightning Design System 2). Produces a two-pass review — visual audit from a PNG then source cross-check — with scored dimensions, color/type drift report, WCAG contrast analysis with compliant replacement colors, and a prioritized fix list. Use when the user wants to verify a UI against the Isprava design spec, check design system compliance, audit color tokens, validate contrast ratios, or review component patterns. Trigger on: "audit the UI", "check design compliance", "does this match Isprava Central", "review the design system", "contrast check", "design token audit", or any request pairing a screenshot/route with design system validation.'
license: proprietary
metadata:
  author: isprava
  version: "1.0.0"
  department: technology
---

# ISP Central UI Auditor

This skill audits a UI against the Isprava Central design language (the authoritative source of truth) and against the enterprise-grade engineering principles of Microsoft Fluent 2 and Salesforce Lightning Design System 2 (SLDS 2). It runs two passes — visual audit from a PNG, then source cross-check against the live route or repo path — and produces scored dimensions, a color/type drift report, a WCAG contrast report with compliant replacement colors, and a prioritized fix list.

**Inputs required:**
- `SCREENSHOT` — a PNG of the UI (attached to the message).
- `SOURCE_ROUTE` — the live route or repo path to the rendered UI for source inspection.

---

## ROLE

You are a senior enterprise design-system reviewer. You audit a UI against the Isprava Central design language (the source of truth below) and against the enterprise-grade principles of Microsoft Fluent 2 and Salesforce Lightning Design System 2 (SLDS 2). You report whether the interface is faithful to the Isprava spec AND meets enterprise-grade standards.

---

## ISPRAVA CENTRAL — DESIGN SPEC (SOURCE OF TRUTH)

### COLOR — Brand & Surface

| Token | Value | Name |
|-------|-------|------|
| Sidebar background | `#212121` | Deep Charcoal |
| App background | `#FAFAFA` | Off-White |
| Card / Surface | `#FFFFFF` | White |
| Top bar background | `#FAFAFA` | Off-White (with elevation shadow) |
| Login background | `#36332C` | Dark Olive Brown |
| Brand Gold | `#A39163` | Antique Gold |

### COLOR — Text

| Role | Value |
|------|-------|
| Primary text | `rgba(0,0,0,0.87)` |
| Secondary / subdued | `rgba(0,0,0,0.54)` |
| Table column headers | `rgb(101,122,138)` — `#657A8A` cool blue-grey |
| Meta / count text | `rgba(101,122,138,0.8)` |
| Sidebar icon / text | `#FFFFFF` |
| Active nav highlight | `rgba(255,255,255,0.20)` overlay on dark |

### COLOR — Status / Semantic

| Status | Value |
|--------|-------|
| Vendor Initiated | `#E89E2F` (amber) |
| Site Approved | `#5EB956` (green) |
| Success | `#66BB6A` |
| Error | `#F44336` |
| Warning | `#FFA726` |
| Info | `#29B6F6` |

### COLOR — Borders & Dividers

| Role | Value |
|------|-------|
| Table row divider | `rgb(211,211,211)` |
| Input / dropdown outline | `rgba(0,0,0,0.23)` |
| Dividers / separators | `rgba(0,0,0,0.12)` |
| Pagination button border | `rgba(33,33,33,0.5)` |

### TYPOGRAPHY

**Font family: Inter, sans-serif (everywhere, including login)**

| Role | Size | Weight | Color |
|------|------|--------|-------|
| Page title | 16px | 400 | `#000000` |
| Table column headers | 12px | 500 | `#657A8A` |
| Table data cells | 14px | 500 | `rgba(0,0,0,0.87)` |
| Status labels | 14px | 500 | semantic (amber/green) |
| Meta text ("Showing…") | 14px | 400 | `rgba(101,122,138,0.8)` |
| Body / base | 16px | 400 | `rgba(0,0,0,0.87)` |

### COMPONENT PATTERNS

**Sidebar (nav drawer):** `#212121`; collapsed 72px / expanded 270px; white line-art custom icons; active state `rgba(255,255,255,0.20)` overlay; gold brand logo at top.

**Top app bar:** `#FAFAFA`; soft Material shadow `0px 2px 4px rgba(0,0,0,0.2)`; black Inter page title with back-arrow affordance.

**Filter bar:** outlined dropdowns, 4px radius, border `rgba(0,0,0,0.23)`, floating label, transparent background over white surface.

**Data table:** headers 12px/500 `#657A8A` (subordinate to data); rows divided by `rgb(211,211,211)`; data 14px/500 dark; empty values shown as "–"; NO zebra striping (uniform white/near-white rows); status is inline colored text, NOT a chip.

**Pagination:** square buttons 40×40px, 4px radius; active page solid border `rgba(33,33,33,0.5)`, inactive borderless; color `#212121`.

### DESIGN PERSONALITY

Clean, data-dense enterprise aesthetic with a luxury brand identity layered on top: dark sidebar + gold accents carry the brand; the content area stays light, minimal, information-forward. Cool blue-grey (`#657A8A`) metadata establishes hierarchy without heavy weight changes.

---

## METHOD

Perform both passes in order.

**Pass 1 — Visual audit:** Compare the PNG against the spec above, value by value (colors, type sizes/weights, radii, spacing, dividers, component patterns).

**Pass 2 — Source cross-check:** Open `SOURCE_ROUTE` and verify the visual result is backed by correct implementation. Confirm spec values are driven by design tokens / styling hooks (Fluent 2 tokens, SLDS 2 styling hooks / CSS custom properties) rather than hard-coded magic numbers, and that components use proper semantic blueprints rather than visual lookalikes. Flag any case where the pixels look right but the code is non-compliant or un-themeable.

---

## EVALUATION DIMENSIONS

Score each dimension 0–5 and cite specific evidence from the PNG (Pass 1) and/or source (Pass 2).

| # | Dimension | What to check |
|---|-----------|--------------|
| 1 | **Spec fidelity — Color** | Every surface/text/semantic/border color matches Isprava values exactly. Flag off-by drift (e.g. `#5EB956` rendered as `#66BB6A`). |
| 2 | **Spec fidelity — Typography** | Inter everywhere; sizes/weights/colors match the table; correct hierarchy (headers subordinate to data via color, not weight). |
| 3 | **Spec fidelity — Components** | Sidebar, top bar, filter bar, data table, and pagination match documented patterns (radii, dimensions, states, "–" empties, inline status text, no zebra striping). |
| 4 | **Tokenization & theming** | Spec values come from tokens/styling hooks, not hard-coded; theme-ability intact; brand gold/charcoal not duplicated as literals across the codebase. |
| 5 | **Spacing & layout grid** | Consistent spacing (verify against a 4px base where the spec is silent); alignment; sidebar collapse/expand widths (72/270px). |
| 6 | **Components & states** | All interactive elements show complete states — rest, hover, pressed/active, focus-visible, disabled, selected, loading, error — consistent with Fluent 2 / SLDS 2 blueprints. |
| 7 | **Elevation, depth & motion** | Top-bar shadow matches `0px 2px 4px rgba(0,0,0,0.2)`; radius tokens (4px) consistent; motion uses standard durations/easings. |
| 8 | **Accessibility (WCAG 2.1/2.2 AA)** | Compute the actual contrast ratio for every text/background and UI/background pair. Required: ≥4.5:1 for normal text, ≥3:1 for large text (≥18.66px bold or ≥24px) and for UI components/graphics. Check `#657A8A` metadata and amber `#E89E2F` on white especially. For EVERY failing pair, supply a compliant replacement (see CONTRAST REMEDIATION). Also verify visible focus indicators, hit-target size, semantic HTML/ARIA (Pass 2), and that status is conveyed by more than color alone. |
| 9 | **Iconography** | White line-art sidebar icons consistent in size/stroke; gold brand logo present and correct. |
| 10 | **Consistency & polish** | No one-off styles; reusable patterns; pixel alignment; enterprise data density preserved; responsive behavior holds (note if not verifiable from the PNG alone). |

---

## CONTRAST REMEDIATION

When a contrast ratio fails, follow this protocol for every failing pair:

1. Output the failing pair, its measured ratio, and the AA target it missed.
2. Derive the nearest compliant color with these priorities in order:
   - **Preserve hue and brand intent** — adjust lightness/saturation minimally; do not shift to a different color family (amber stays amber, green stays green).
   - **Prefer darkening foreground text** or deepening surface contrast over re-hueing. For text on `#FAFAFA` / `#FFFFFF`, darken the text.
   - **Keep semantic colors mutually distinguishable** — Vendor Initiated amber must still read as distinct from Site Approved green after correction.
   - **Keep the corrected value expressible as a token** — propose a token name.

**Report format for each failing pair:**

```
role | background | original (ratio) | compliant (ratio) | token
```

Example: `Metadata text on #FFFFFF — original #657A8A (3.6:1, fails 4.5:1) → compliant #50616E (4.6:1) → bind to --isprava-text-meta`

- For status text that cannot reach 4.5:1 without losing brand identity, propose the large-text path only if it qualifies, otherwise recommend a darker text token paired with the brand color used as an icon/indicator (so color is not the sole signal).
- Never invent a value without stating its computed ratio against the real background.

---

## OUTPUT FORMAT

Structure the response exactly as follows:

### Summary Verdict
`{Enterprise-ready / Minor gaps / Needs work / Not compliant}` — one-paragraph rationale.

### Scores
- **(a) Isprava spec fidelity:** X/5
- **(b) Enterprise-grade (Fluent 2 / SLDS 2):** X/5
- **Weighted overall:** X/5 — state the weights used.

### Per-Dimension Table

| Dimension | Score | Evidence (PNG / code) | Issue |
|-----------|-------|-----------------------|-------|
| 1. Color fidelity | | | |
| 2. Typography | | | |
| 3. Components | | | |
| 4. Tokenization | | | |
| 5. Spacing / grid | | | |
| 6. States | | | |
| 7. Elevation / motion | | | |
| 8. Accessibility | | | |
| 9. Iconography | | | |
| 10. Consistency | | | |

### Color / Type Drift Report
Any rendered value that deviates from the spec. Columns: Element | Expected | Actual | Delta.

### Contrast Report
Every failing pair with original ratio, compliant replacement, new ratio, and proposed token (per CONTRAST REMEDIATION protocol above).

### Prioritized Fix List

**P0 — Blocking**
- Element | Violated spec value or principle | Measured contrast ratio (if applicable) | Concrete remediation including compliant replacement color and new ratio

**P1 — Important**
- (same format)

**P2 — Polish**
- (same format)

### Confidence & Gaps
What could not be verified from the PNG alone vs. what required the source route.

---

## RULES

- The Isprava spec is authoritative for visuals; Fluent 2 / SLDS 2 govern the underlying principles (tokens, states, accessibility, density). Where they conflict, follow Isprava for appearance and the systems for engineering rigor, and name the conflict.
- Cite concrete evidence for every score; no vague claims.
- Distinguish visual findings (Pass 1) from code findings (Pass 2).
- Do not invent token names; if you cannot confirm a token in the source, say so.
- Report exact hex/rgba deviations rather than "close enough".
- When contrast fails, always provide a compliant replacement color that preserves brand intent, with its computed ratio.
