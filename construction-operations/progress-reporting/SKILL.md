---
name: progress-reporting
description: 'Produce clear, accurate construction progress reports for clients and stakeholders. Use when the user mentions "progress report", "monthly report", "construction update", "project status report", "programme update", "cost report", "project dashboard", "stakeholder reporting", "earned value", or "construction reporting". Also trigger when communicating project delays, budget variances, or risk updates to clients. For project planning, see project-planning. For site inspections, see site-inspection.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: construction-operations
---

# Progress Reporting Skill

A framework for producing construction progress reports that keep stakeholders informed, build client confidence, and create a documented record of the project's history. Great progress reports are honest, concise, and action-oriented — they tell the client where the project is, why, and what is being done about any issues.

## Core Principle

**Report the truth, with solutions.** The worst progress report is one that hides problems until they are unavoidable. The best reports communicate issues early, with a clear description of the impact and the action being taken. Clients who are surprised by bad news lose trust; clients who are kept informed — even of bad news — become partners.

## Scoring

**Goal: 10/10.** When reviewing or producing a progress report, rate 0–10 based on accuracy, timeliness, completeness, and action-orientation. A 10/10 means the report accurately reflects programme and cost status, identifies issues with their impact, and includes a clear corrective action plan.

## Reporting Framework

### 1. Report Structure

**Core concept:** A consistent structure that clients can navigate quickly and that covers all critical project dimensions.

**Standard progress report sections:**

| Section | Content | Length |
|---------|---------|--------|
| **Executive Summary** | Overall status (on track / at risk / delayed), top 3 highlights, top 3 issues | 1 page |
| **Programme Status** | % complete vs. planned, critical path status, forecast completion date | 1–2 pages |
| **Cost Status** | Approved contract sum, variations to date, forecast final cost, approved vs. pending variations | 1 page |
| **Work Completed This Period** | What was physically done since last report | 1 page |
| **Work Planned Next Period** | What will be done before the next report | 1 page |
| **Issues & Risks** | Active issues with impact and corrective action; updated risk register | 1 page |
| **Decisions Required** | Items the client needs to decide for the project to proceed | 1/2 page |
| **Photo Record** | Progress photos showing representative works | 1–2 pages |
| **Programme (updated)** | Updated Gantt chart or summary bar chart | Appendix |
| **Variation Log** | All variations with status | Appendix |

### 2. Programme Status Reporting

**Core concept:** An honest, data-driven assessment of where the project stands against the baseline programme.

**Key metrics to include:**

| Metric | Description | How to Calculate |
|--------|-------------|-----------------|
| % Complete (planned) | How far along the project should be today per baseline | From baseline programme |
| % Complete (actual) | How far along the project actually is | Measured from site |
| Schedule variance | Difference between planned and actual | Planned % - Actual % |
| Forecast completion | Current expected end date based on progress | Baseline end date ± schedule variance in days |
| Critical path status | Is the critical path being maintained? | On track / At risk / Delayed |

**Programme status RAG rating:**

| Status | Meaning | Condition |
|--------|---------|-----------|
| Green | On track | Forecast completion ≤ 1 week behind baseline |
| Amber | At risk | Forecast completion 1–4 weeks behind baseline; recovery plan in place |
| Red | Delayed | Forecast completion >4 weeks behind baseline or recovery plan uncertain |

**Delay reporting:**
When delays are reported, always include:
1. The activity or activities that are delayed
2. The cause of the delay
3. The impact on the overall programme (days/weeks)
4. Whether the delay is contractor-caused, client-caused, or force majeure (relevant to EOT claims)
5. The corrective action being taken

See: [references/programme-reporting-template.md](references/programme-reporting-template.md)

### 3. Cost Status Reporting

**Core concept:** A transparent financial summary that shows where the budget stands and what the project is forecast to cost at completion.

**Cost report structure:**

| Line Item | Amount |
|-----------|--------|
| Original contract sum | $ |
| Approved variations to date | $ |
| Current approved contract sum | $ |
| Claimed to date | $ |
| Certified to date | $ |
| Remaining contract value | $ |
| Pending variations (submitted, not yet approved) | $ |
| Potential variations (identified, not yet submitted) | $ |
| **Forecast final cost** | $ |
| Contingency remaining | $ |

**Variation log columns:**
- Variation number
- Description
- Date submitted
- Date approved (if approved)
- Amount claimed
- Amount approved
- Status (Pending / Approved / Rejected / In dispute)

### 4. Issues & Risks Reporting

**Core concept:** A clear, honest summary of active issues that could impact the project — with the corrective action being taken.

**Issue report format:**

| # | Issue | Impact | Action | Owner | Due |
|---|-------|--------|--------|-------|-----|
| 1 | Design clarification on Level 3 services coordination outstanding | Could delay M&E rough-in by 1 week if not resolved by [date] | RFI #42 submitted; following up with structural engineer | PM | [date] |
| 2 | Concrete supply shortage due to batching plant shutdown | Risk of 2-day delay to slab pour | Sourcing alternative supplier; contingency pour date [date] | Site Mgr | [date] |

**Issue severity coding:**
- Red: Active impact on programme or cost; immediate action required
- Amber: Potential impact if not resolved; monitoring and action underway
- Green: Resolved or no longer a risk

### 5. Photo Record

**Core concept:** A photographic record that shows progress visually and supplements the written report.

**Why it matters:** Photos build client confidence, resolve disputes about what was done and when, and create the project archive.

**Photo selection criteria:**
- Representative of major work packages active this period
- Before/after pairs where relevant
- Any unusual conditions or events (weather events, latent conditions, incidents)
- Good quality: well-lit, in focus, clear context
- Caption every photo with location, date, and description of what is shown

**Photo management:**
- Store photos in a dated, organized folder structure (e.g., `Photos/2024-W14/`)
- Minimum 10–20 photos per monthly report
- Never use unedited or uncaptioned photos in a client report

### 6. Decisions Required

**Core concept:** A clear list of decisions the client must make for the project to proceed unimpeded.

**Why it matters:** Client decisions are one of the most common causes of construction delay. Surfacing them clearly and early creates accountability.

**Format:**

| # | Decision Required | Impact if Not Resolved | Response Required By |
|---|------------------|----------------------|---------------------|
| 1 | Confirm Level 2 joinery specification from shortlist provided | Delay to joinery procurement of up to 3 weeks | [Date] |
| 2 | Approve colour schedule for external render | Cannot order materials | [Date] |

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| Reporting only good news | Client is blindsided by problems at month end | Report issues early with corrective action |
| Vague programme status ("progressing well") | Client has no real picture of where the project is | Always include % complete planned vs. actual |
| Cost report without forecast final cost | Client doesn't know if they're on budget | Always include a forecast final cost in every cost report |
| Issues listed without corrective action | Looks like the team has no plan | Every issue must have a corrective action, owner, and due date |
| Report issued late | Stakeholder confidence erodes | Report on a fixed, pre-agreed schedule; treat it like a site meeting |

## Quick Diagnostic

| Question | If No | Action |
|----------|-------|--------|
| Is the report issued on the agreed schedule? | Stakeholder trust eroding | Fix the report date in the programme and build it into the site routine |
| Does the report include % complete planned vs. actual? | Programme status is vague | Add the comparison; calculate from the updated programme |
| Does every issue have a corrective action and owner? | Issues look unmanaged | Add action and owner before issuing the report |
| Is there a decisions required section? | Client decisions are being delayed | Add the section; track client response times |

## Reference Files

- [references/programme-reporting-template.md](references/programme-reporting-template.md) — Monthly progress report template (Word/Excel)
