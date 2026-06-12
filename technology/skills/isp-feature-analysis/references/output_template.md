# Output Template

Use this exact structure for the Phase 9 deliverable. Adjust section depth based on content, but do not reorder or rename top-level sections.

```markdown
# {{Feature}} — Analysis & Implementation Plan

## Document Metadata
- **Author:** {{Author / Claude session}}
- **Date:** {{YYYY-MM-DD}}
- **Version:** 1.0
- **Status:** Draft / Ready for Review / Approved
- **Inputs Used:**
  - PRD: `{{path or "not provided"}}`
  - Figma: `{{links or "not provided"}}`
  - Current desktop: `{{ref or "not provided"}}`
  - Current responsive: `{{ref or "not provided"}}`
  - Repo: `{{repo@branch or "not provided"}}`

## Table of Contents
1. Executive Summary
2. PRD Requirements
3. Figma Inventory
4. Current State Analysis
5. Gap Analysis
6. Open Questions
7. Implementation Checklist
8. Test Cases
9. Technical Specs
10. Assumptions

## 1. Executive Summary
- 5–8 bullets capturing: scope, top 3 gaps, biggest risks, recommended next step.

## 2. PRD Requirements

| ID | Category | Summary | Acceptance Criteria | Ambiguity? |
|----|----------|---------|---------------------|------------|

## 3. Figma Inventory

### 3.1 Components & States
### 3.2 Breakpoints
### 3.3 Design Tokens / Deviations
### 3.4 Interactions

## 4. Current State Analysis

| Element | Current Behavior | Disposition (Keep / Modify / Replace / Remove / New) | Notes |
|---------|------------------|-----|-------|

## 5. Gap Analysis

| # | Requirement / Element | PRD | Figma | Current | Gap Type | Severity | Owner | Notes |
|---|----------------------|-----|-------|---------|----------|----------|-------|-------|

## 6. Open Questions

- [ ] Question 1 — *Owner: Product*
- [ ] Question 2 — *Owner: Design*
- [ ] Question 3 — *Owner: Engineering*

## 7. Implementation Checklist

### 7.1 Components / Modules
- [ ] ...

### 7.2 API / Backend
- [ ] ...

### 7.3 State Management
- [ ] ...

### 7.4 Routing
- [ ] ...

### 7.5 Responsive
- [ ] ...

### 7.6 Accessibility
- [ ] ...

### 7.7 Analytics
- [ ] ...

### 7.8 SEO / Metadata
- [ ] ...

### 7.9 Feature Flags / Rollout
- [ ] ...

### 7.10 Documentation
- [ ] ...

## 8. Test Cases

| TC ID | Title | Preconditions | Steps | Expected Result | Type | Priority | Linked Req |
|-------|-------|---------------|-------|-----------------|------|----------|------------|

## 9. Technical Specs

### 9.1 File Changes

| Path | Action (New / Modify / Delete) | Purpose | Effort |
|------|-------------------------------|---------|--------|

### 9.2 Component Hierarchy & Props
### 9.3 Data Fetching & API Contracts
### 9.4 State Management
### 9.5 Reusable Utilities / Hooks / DS Additions
### 9.6 Migration & Backward Compatibility
### 9.7 Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|

## 10. Assumptions

- **[ASSUMPTION]** ...
- **[ASSUMPTION]** ...
```
