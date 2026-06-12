---
name: isp-init-project
description: 'Mandatory governance standards for generating prototypes and proof-of-concepts. When active, all generated code, UI, and implementation decisions must comply — frontend-only, mock-data, Cosmos Terra Refined design system, light mode, sharp edges. Use when the user mentions "build a prototype", "init a project", "scaffold a POC", "proof of concept", "Cosmos prototype", "high-fidelity mockup", "frontend-only demo", or starts a new prototype/screen. Also trigger whenever generating standalone browser prototypes that must follow the organisation design language.'
license: proprietary
metadata:
  author: isprava
  version: "1.1.0"
  department: technology
---

# Cosmos Prototype Implementation Standards

This skill defines the mandatory standards for generating prototypes and proof-of-concepts within the organisation. Whenever this skill is active, all generated code, UI, and implementation decisions must comply with these rules. If a user request conflicts with these standards, the implementation must either adapt the request or explicitly state the conflict before proceeding.

## Core Principle

**Prototypes are frontend-only, high-fidelity, and design-system-true by default.** Produce standalone browser applications that are easy to understand and review, easy for AI coding tools to modify and extend, closely represent the intended user experience, follow the organisation's design language consistently, avoid unnecessary technical complexity, and can later be migrated into production implementations.

## Scoring

**Goal: 10/10.** Rate every prototype 0–10 based on adherence to the standards below. A 10/10 means full compliance with the Self-Validation Checklist. Lower scores indicate specific defects. Always provide the current score and actionable corrections to reach 10/10. **Failure to comply should be treated as an implementation defect and corrected before the work is considered complete.**

## Mandatory Compliance

Every implementation generated while using this skill MUST comply with these guidelines. Failure to comply should be treated as an implementation defect.

## Framework

### 1. Technology Constraints — Frontend Only

**Core concept:** Prototypes must be entirely frontend-based and function as a standalone browser application.

**Allowed:**
- HTML5
- CSS3
- Vanilla JavaScript (minimal)
- Static JSON objects
- Browser-native APIs

**Not allowed unless explicitly requested:**
- Backend services, Express, NestJS, Node server logic
- Authentication, databases, REST APIs, GraphQL, WebSockets
- File storage, external business services, server-side rendering

### 2. Simulated Data

**Core concept:** Use only mock data.

```javascript
const users = [
  {
    id: 1,
    name: "John Doe",
    role: "Project Manager",
    status: "Active"
  }
];
```

**Never include:** production credentials, API keys, secrets, internal URLs, real customer information, or real employee information.

### 3. Design System Compliance

**Core concept:** All generated interfaces must strictly follow the **Cosmos Terra Refined Design System** provided by the organisation.

**Mandatory requirements:**
- Default to **light mode**. (Dark mode is available only when the user explicitly requests it.)
- Use the official design tokens and CSS variables.
- Use **muted gold** as the primary accent.
- Use **warm ivory / off-white** backgrounds with **warm coffee-black** text for readable contrast.
- Maintain compact spacing and typography.
- Use **sharp edges with 0px border radius**.
- Only avatars and pill badges may be fully rounded.
- Never substitute alternative color palettes or visual styles.
- Never invent new component styles when an existing pattern applies.

### 4. Typography

**Core concept:** Use the official type stack at compact sizing consistent with the design system.

- **Inter** → body text
- **Space Grotesk** → headings
- **JetBrains Mono** → technical values

### 5. Layout Principles

**Core concept:** Prefer dense, hierarchical layouts. Avoid excessive whitespace.

```
+------------------------------------------------+
| Sidebar | Header                               |
|         +--------------------------------------|
|         |                                      |
|         | Main Content                         |
|         |                                      |
|         |                        Right Panel   |
|         |                                      |
+------------------------------------------------+
```

Maintain consistent spacing, visual hierarchy, information density, and clear alignment.

### 6. Component Rules

**Core concept:** Buttons, inputs, cards, tables, navigation, labels, forms, dialogs, and interactive rows must follow the official component specifications defined by the design system.

Focus states must use **glow-based shadows** and never browser outlines.

### 7. Accessibility

**Core concept:** Every prototype should:
- Support keyboard navigation.
- Use semantic HTML.
- Meet minimum 44×44px touch targets.
- Respect reduced-motion preferences.
- Maintain readable contrast.

### 8. Code Organization

**Core concept:** Generated code should be easy for humans and AI agents to understand.

Use clearly separated sections:

```html
<!-- Sidebar -->
<!-- Header -->
<!-- Filters -->
<!-- Dashboard -->
<!-- Modal -->
<!-- Footer -->
```

Group CSS into:
1. Variables
2. Base styles
3. Layout
4. Components
5. Utilities
6. Responsive rules

### 9. Naming Standards

**Core concept:** Prefer descriptive names.

| Good | Avoid |
|------|-------|
| `project-card` | `box1` |
| `activity-feed` | `div2` |
| `status-pill` | `container-final` |
| `task-table` | `temp` |
| `approval-modal` | |

### 10. JavaScript Rules

**Core concept:** JavaScript should only demonstrate interactions.

**Allowed:** modal open/close, accordion expansion, tab switching, client-side filtering, local sorting, toast notifications, static charts, mock search.

**Do not implement:** authentication, persistence, network requests, real-time synchronization, production business logic.

### 11. AI Readability

**Core concept:** The generated implementation must be easy for future AI tools to modify.

- Keep files logically organized.
- Avoid deeply nested structures.
- Avoid unnecessary abstraction.
- Avoid minified code.
- Prefer explicit implementations over clever optimizations.
- Add concise comments where intent may not be obvious.

## Expected Deliverable

Unless instructed otherwise, produce `index.html` containing:
- Embedded CSS
- Embedded JavaScript
- Static data
- A fully functional prototype
- No external runtime dependencies

## Self-Validation Checklist

Before considering the implementation complete, verify:

- [ ] Frontend-only implementation
- [ ] No backend or API dependencies
- [ ] Uses only mock data
- [ ] Conforms to the Cosmos Terra Refined design system
- [ ] Defaults to light mode
- [ ] Uses sharp edges (0px border radius except approved exceptions)
- [ ] Uses official typography and color tokens
- [ ] Includes accessible focus and interaction states
- [ ] Has clear structure and descriptive naming
- [ ] Is easy for AI coding tools to read and extend
- [ ] Can be opened directly in a browser without additional setup

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Adding a backend or API to "make it real" | Prototype must run standalone in a browser | Use static JSON mock data |
| Using rounded corners everywhere | Violates the 0px border-radius rule | Sharp edges; round only avatars and pill badges |
| Substituting a different color palette | Breaks design-system consistency | Use muted gold accent + warm ivory surfaces (light tokens by default) |
| Browser default focus outlines | Off-brand and against component spec | Use glow-based shadow focus states |
| Generic names like `div2`, `temp` | Hard for humans and AI to extend | Use descriptive names like `project-card` |
| Real customer/employee data | Security and privacy defect | Use clearly fictional mock data only |

## Quick Diagnostic

| Question | If No | Action |
|----------|-------|--------|
| Does it run standalone in a browser? | Backend dependency present | Strip backend; use mock data |
| Is light mode the default? | Off-brand | Apply Cosmos Terra Refined light tokens |
| Are edges sharp (0px radius)? | Visual defect | Remove border-radius except avatars/pills |
| Are focus states glow-based? | Accessibility/brand gap | Replace outlines with glow shadows |
| Is the code free of minification and deep nesting? | AI-unfriendly | Flatten structure, add intent comments |

## Enforcement Directive

If this skill is active, every generated project, screen, or prototype must comply with these standards by default. Any deviation should be treated as a defect and corrected before the implementation is considered complete.
