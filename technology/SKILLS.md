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
| **isp_prd_builder** | Build a comprehensive PRD from a single-line idea through structured interactive rounds. Use when starting a feature from scratch. |
| **isp_feature_analysis** | Run a full end-to-end gap analysis between a PRD, Figma designs, current production UI, and a target repo. Produces a complete implementation plan as a single Markdown deliverable. |
| **isp_gap_audit** | Deep gap and ambiguity audit between a PRD, Figma design, and the actual codebase. Surfaces missing requirements, conflicting specs, and open questions. |

### Pipeline Phases (run individually or in sequence)

| Phase | Skill | Description |
|-------|-------|-------------|
| 1 | **isp_intake** | Validate all inputs (repo path, PRD, Figma, feature name) before any analysis begins. |
| 2 | **isp_prd_analysis** | Extract and classify every requirement from a PRD through five independent reading passes. |
| 3 | **isp_figma_analysis** | Enumerate every component, state, breakpoint, and interaction visible in Figma designs through five inspection passes. |
| 4 | **isp_current_state** | Classify every existing production UI component as Keep / Modify / Replace / Remove / New across five passes. |
| 5 | **isp_gap_analysis** | Three-way gap comparison between PRD requirements, Figma design, and current production state across five passes. |
| 6 | **isp_checklist** | Generate a developer-actionable implementation checklist from the verified gap register. |
| 7 | **isp_test_cases** | Generate comprehensive test cases covering unit, integration, E2E, visual regression, responsive, and accessibility. |
| 8 | **isp_tech_specs** | Produce grounded technical specifications — file-level change list, component hierarchy, API contracts, state management. |
| 9 | **isp_effort_estimate** | Produce three-mode effort estimates: Unsupervised AI, Supervised AI, and Manual. |
| 10 | **isp_deliverable** | Assemble all phase outputs into a single, standalone Markdown deliverable with five completeness verification passes. |

---

## Recommended Workflow

```
Single idea → isp_prd_builder → isp_feature_analysis
                                        │
                    ┌───────────────────┼───────────────────┐
                    ▼                   ▼                   ▼
              isp_gap_audit      Phase pipeline       isp_deliverable
```

For a full phase-by-phase run:
`isp_intake → isp_prd_analysis → isp_figma_analysis → isp_current_state → isp_gap_analysis → isp_checklist → isp_test_cases → isp_tech_specs → isp_effort_estimate → isp_deliverable`
