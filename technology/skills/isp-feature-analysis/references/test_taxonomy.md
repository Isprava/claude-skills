# Test Taxonomy

Use this during Phase 7 to make sure coverage is real, not theoretical. Aim for at least one test per applicable type for every major requirement.

## Types

### Unit
- Scope: a single function, hook, or pure component in isolation
- Tools (typical): Jest, Vitest, React Testing Library
- Good targets: formatters, validators, derived state, prop-to-render mapping

### Integration
- Scope: a small group of components or a feature slice with mocked external deps
- Good targets: form submission flows, data-fetch + render, state transitions between components

### End-to-End (E2E)
- Scope: full user journey in a real browser against a real or staged backend
- Tools (typical): Playwright, Cypress
- Good targets: booking flows, search → details → action paths, auth-gated journeys

### Visual Regression
- Scope: pixel-level diff against an approved baseline
- Tools (typical): Chromatic, Percy, Playwright snapshots
- Good targets: design-system components, hero sections, anything where a layout regression would be embarrassing

### Responsive
- Scope: layout and behavior across breakpoints
- Required breakpoints: at minimum the breakpoints listed in the Figma; usually 360 / 768 / 1024 / 1440
- Test both **layout** (no overflow, correct stacking) and **behavior** (mobile menu opens, touch targets ≥ 44px)

### Accessibility (a11y)
- Required checks per component:
  - Keyboard reachability and logical tab order
  - Visible focus indicator
  - Sufficient color contrast (WCAG AA: 4.5:1 text, 3:1 UI)
  - Screen reader landmark + label coverage
  - Reduced-motion respected
  - Form fields have associated labels and error messaging
- Tools: axe, Lighthouse, manual screen-reader pass (VoiceOver / NVDA)

### Edge Cases
- Slow network (throttled 3G)
- Offline / API failure
- Empty states (no results, no inventory, no permissions)
- Error states (4xx, 5xx, validation)
- Very long content (50-char names, 500-char descriptions, 30-image galleries)
- Internationalization: RTL, long German compound words, multibyte CJK characters
- Stale auth / session expiry mid-flow

## Priority

- **P0** — Must pass before merge. Blocker-level gaps or core flows.
- **P1** — Must pass before release.
- **P2** — Should pass; can ship with known issue + ticket.
- **P3** — Nice to have; track but don't gate release.

## Linking to requirements

Every test case row must populate **Linked Req** with at least one `REQ-XX` ID from Phase 2 or a checklist item ID from Phase 6. A test case with no linked requirement is a smell — either it's testing speculative behavior or there's a missing requirement to add.
