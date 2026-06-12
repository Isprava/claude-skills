# Technology Skills

15 skills across two categories: general engineering and the ISP feature-analysis pipeline.

---

## General Engineering

| Skill | Description |
|-------|-------------|
| **code-review** | Conduct thorough, constructive code reviews aligned with engineering best practices. Trigger on "review this PR", "check my code", or any pull-request review request. |
| **incident-response** | Lead and coordinate production incident response. Trigger on "production is down", "incident in progress", "site is broken", or any live outage report. |

---

## ISP Feature Analysis Pipeline

A set of 13 skills that can be run individually or chained end-to-end to produce a complete implementation plan from PRD + Figma inputs.

### Entry Points

| Skill | Description |
|-------|-------------|
| **isp-prd-builder** | Build a comprehensive PRD from a single-line idea through structured interactive rounds. Use when starting a feature from scratch. |
| **isp-feature-analysis** | Run a full end-to-end gap analysis between a PRD, Figma designs, current production UI, and a target repo. Produces a complete implementation plan as a single Markdown deliverable. |
| **isp-gap-audit** | Deep gap and ambiguity audit between a PRD, Figma design, and the actual codebase. Surfaces missing requirements, conflicting specs, and open questions. |

### Pipeline Phases (run individually or in sequence)

| Phase | Skill | Description |
|-------|-------|-------------|
| 1 | **isp-intake** | Validate all inputs (repo path, PRD, Figma, feature name) before any analysis begins. |
| 2 | **isp-prd-analysis** | Extract and classify every requirement from a PRD through five independent reading passes. |
| 3 | **isp-figma-analysis** | Enumerate every component, state, breakpoint, and interaction visible in Figma designs through five inspection passes. |
| 4 | **isp-current-state** | Classify every existing production UI component as Keep / Modify / Replace / Remove / New across five passes. |
| 5 | **isp-gap-analysis** | Three-way gap comparison between PRD requirements, Figma design, and current production state across five passes. |
| 6 | **isp-checklist** | Generate a developer-actionable implementation checklist from the verified gap register. |
| 7 | **isp-test-cases** | Generate comprehensive test cases covering unit, integration, E2E, visual regression, responsive, and accessibility. |
| 8 | **isp-tech-specs** | Produce grounded technical specifications — file-level change list, component hierarchy, API contracts, state management. |
| 9 | **isp-effort-estimate** | Produce three-mode effort estimates: Unsupervised AI, Supervised AI, and Manual. |
| 10 | **isp-deliverable** | Assemble all phase outputs into a single, standalone Markdown deliverable with five completeness verification passes. |

---

## Recommended Workflow

```
Single idea → isp-prd-builder → isp-feature-analysis
                                        │
                    ┌───────────────────┼───────────────────┐
                    ▼                   ▼                   ▼
              isp-gap-audit      Phase pipeline       isp-deliverable
```

For a full phase-by-phase run:
`isp-intake → isp-prd-analysis → isp-figma-analysis → isp-current-state → isp-gap-analysis → isp-checklist → isp-test-cases → isp-tech-specs → isp-effort-estimate → isp-deliverable`
