# Severity Rubric

Use this when assigning severity in the Phase 5 gap analysis table. When in doubt, err one level higher — under-classifying gaps is more dangerous than over-classifying.

## Blocker
The feature cannot ship without resolving this. Examples:
- A required user flow has no design (e.g., booking flow shown only on desktop)
- PRD contradicts Figma on a primary CTA's behavior
- A regulated/legal requirement (accessibility minimums, consent flows, pricing display) is missing
- Performance budget mentioned in the PRD is contradicted by the design (e.g., 30 high-res images on a page with a 2s LCP target)

## High
The feature can technically ship but with material risk. Examples:
- Error / empty / loading states missing from design
- Responsive behavior unspecified for a major breakpoint
- An analytics event in the PRD has no obvious trigger point in the design
- A core component will be replaced but no migration path is defined

## Medium
Noticeable gap that should be resolved before code freeze but won't block initial implementation. Examples:
- Microcopy not finalized
- Edge cases (long names, missing images) not addressed in design
- Hover/focus states underspecified
- A11y nice-to-haves (skip links, reduced-motion support) missing

## Low
Polish-level. Can be tracked as follow-ups. Examples:
- Spacing inconsistencies vs the design system
- Suggested copy improvements
- Animation timing not specified

## Owner assignment

- **Product** — owns requirement clarification, scope, prioritization, content
- **Design** — owns visual states, interaction details, design system alignment
- **Engineering** — owns technical feasibility, perf budget, repo conventions
- **QA** — owns testability concerns, missing acceptance criteria

A single gap can have multiple potential owners; pick the **primary decision-maker**.
