# Organisation Skills Library

A collection of Claude Code skills organized by department. Each skill encodes domain knowledge, frameworks, and standard operating procedures that guide Claude to deliver expert-level assistance for specific departmental tasks.

## Departments

| Department | Skills | Description |
|-----------|--------|-------------|
| [Technology](#technology) | 2 | Engineering practices: code review, incident response |
| [Marketing](#marketing) | 2 | Marketing frameworks: content strategy, campaign planning |
| [Sales](#sales) | 2 | Sales methodology: sales playbook, proposal writing |
| [Construction](#construction) | 2 | Construction project: planning, safety compliance |
| [Hospitality Operations](#hospitality-operations) | 2 | Hospitality ops: guest experience, staff scheduling |
| [Construction Operations](#construction-operations) | 2 | Site operations: inspection, progress reporting |

---

## Technology

### `code-review`
**Conduct thorough, constructive code reviews**

A structured framework for delivering high-signal code reviews that improve quality, catch bugs, and share knowledge — without becoming a bottleneck.

**Use when:** "review this code", "PR review", "code quality", "pull request feedback", "tech debt"

**Covers:** Correctness, security (OWASP Top 10), readability, performance, test coverage, review tone

---

### `incident-response`
**Lead and coordinate production incident response**

A structured framework for detecting, containing, resolving, and learning from production incidents. Covers the full lifecycle from declaration to blameless post-mortem.

**Use when:** "production is down", "incident", "outage", "P1/P2 alert", "on-call", "post-mortem"

**Covers:** Severity levels, communication templates, investigation, containment, post-mortem structure

---

## Marketing

### `content-strategy`
**Plan, create, and optimize content that builds brand awareness**

A systematic approach to audience research, content planning, brand voice, and distribution that turns content into a measurable growth engine.

**Use when:** "content calendar", "blog post", "content strategy", "editorial plan", "brand voice", "content marketing"

**Covers:** Audience personas, content goals & metrics, editorial calendar, brand voice, distribution

---

### `campaign-planning`
**Plan and execute integrated marketing campaigns**

A framework for building campaigns from brief to results — starting with goal and audience, not channel and creative.

**Use when:** "marketing campaign", "campaign brief", "launch plan", "go-to-market", "GTM strategy", "paid media"

**Covers:** Campaign brief, SMART goals, audience segmentation, channel strategy, message architecture, measurement

---

## Sales

### `sales-playbook`
**Execute a consistent, repeatable sales process**

A stage-by-stage sales methodology from prospecting to close, built around deep discovery and qualified pipeline.

**Use when:** "sales process", "discovery call", "qualification", "MEDDIC", "deal review", "objection handling"

**Covers:** ICP, outreach, SPIN discovery, MEDDIC qualification, solution/demo, negotiation, close, handoff

---

### `proposal-writing`
**Write compelling, client-winning business proposals**

A framework for writing proposals that lead with the client's problem, demonstrate tailored value, and close with a clear next step.

**Use when:** "write a proposal", "proposal template", "RFP response", "bid document", "scope of work"

**Covers:** Executive summary, problem statement, solution, deliverables, proof, pricing, risk reduction, CTA

---

## Construction

### `project-planning`
**Plan construction projects from pre-construction through handover**

A structured framework for defining scope, building realistic programmes, planning procurement, and managing risk — before ground is broken.

**Use when:** "construction schedule", "project plan", "WBS", "Gantt chart", "construction programme", "project milestones"

**Covers:** Scope definition, WBS, programme types, critical path, procurement, risk register, communication plan

---

### `safety-compliance`
**Ensure construction sites meet WHS/OHS obligations**

A framework for maintaining a safe site: hazard identification, SWMS, inductions, toolbox talks, and incident reporting — all grounded in legal compliance.

**Use when:** "safety plan", "SWMS", "safe work method statement", "JSA", "WHS compliance", "safety audit"

**Covers:** SSMP, hierarchy of controls, SWMS for HRCW, inductions, toolbox talks, incident reporting, notifiable incidents

---

## Hospitality Operations

### `guest-experience`
**Design and deliver exceptional guest experiences**

A framework for mapping the guest journey, setting service standards, executing service recovery, and managing guest feedback across all touchpoints.

**Use when:** "guest experience", "guest satisfaction", "NPS score", "service recovery", "complaint handling", "guest journey"

**Covers:** Guest journey mapping, service standards, LEARN recovery framework, review management, team training

---

### `staff-scheduling`
**Create efficient, fair hospitality staff rosters**

A framework for demand-driven scheduling that balances service quality, labour cost efficiency, and award/EBA compliance.

**Use when:** "staff roster", "shift scheduling", "labour cost", "workforce planning", "award compliance", "housekeeping schedule"

**Covers:** Demand forecasting, roster construction, labour cost metrics, award compliance, staff wellbeing

---

## Construction Operations

### `site-inspection`
**Conduct thorough construction site inspections**

A framework for systematic inspections that catch quality issues early, manage hold points, issue NCRs, and build the documentation trail for compliance and client confidence.

**Use when:** "site inspection", "site audit", "quality inspection", "hold point", "NCR", "non-conformance report", "defect inspection"

**Covers:** Inspection types, ITP, hold vs. witness points, defect classification, NCRs, practical completion

---

### `progress-reporting`
**Produce clear, accurate construction progress reports**

A framework for monthly progress reporting that covers programme status, cost, issues, decisions required, and photographic record — with honest RAG ratings.

**Use when:** "progress report", "monthly report", "construction update", "project status report", "programme update", "cost report"

**Covers:** Report structure, programme RAG, cost reporting, issue/risk log, decisions required, photo record

---

## Adding New Skills

1. Copy `_templates/SKILL-TEMPLATE.md` to `{department}/{skill-name}/SKILL.md`
2. Fill in the frontmatter (`name`, `description`, `metadata.department`) and skill content
3. Add supporting reference files to `{department}/{skill-name}/references/` (optional)
4. Add the skill to this README under the correct department
5. Add the skill to `.claude-plugin/marketplace.json`

See `CLAUDE.md` for full authoring guidelines.

---

## Repository Structure

```
claude-skills/
├── technology/
│   ├── code-review/
│   └── incident-response/
├── marketing/
│   ├── content-strategy/
│   └── campaign-planning/
├── sales/
│   ├── sales-playbook/
│   └── proposal-writing/
├── construction/
│   ├── project-planning/
│   └── safety-compliance/
├── hospitality-operations/
│   ├── guest-experience/
│   └── staff-scheduling/
├── construction-operations/
│   ├── site-inspection/
│   └── progress-reporting/
├── _templates/
│   └── SKILL-TEMPLATE.md
├── .claude-plugin/
│   └── marketplace.json
├── CLAUDE.md
└── README.md
```
