---
name: incident-response
description: 'Lead and coordinate production incident response efficiently. Use when the user mentions "production is down", "incident", "outage", "degraded service", "P1/P2 alert", "on-call", "post-mortem", "runbook", or "escalation". Also trigger when diagnosing live system failures, writing incident timelines, or running a blameless retrospective. For code quality issues that led to incidents, see code-review.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# Incident Response Skill

A structured framework for detecting, containing, and resolving production incidents — then learning from them. Good incident response minimizes customer impact, keeps the team calm under pressure, and turns every incident into a system improvement.

## Core Principle

**Stabilize first, diagnose second, fix third.** The instinct to find the root cause immediately causes longer outages. The right sequence is: stop the bleeding → understand what broke → fix it → learn from it.

## Scoring

**Goal: 10/10.** When handling or reviewing an incident, rate 0–10 based on speed of detection, containment, communication, and quality of the post-mortem. A 10/10 means the incident was resolved quickly, stakeholders were informed proactively, and the post-mortem produced concrete preventive actions.

## Incident Response Phases

### Phase 1: Detect & Declare

**Core concept:** An incident is declared the moment a significant user-facing impact is detected or strongly suspected.

**Why it matters:** Declaring early activates the response team. Waiting for certainty wastes precious minutes.

**Key practices:**
- Define severity levels upfront so declaration is automatic, not a judgment call
- Any on-call engineer can declare an incident — no permission needed
- Create a dedicated incident channel immediately (e.g., `#incident-2024-01-15`)
- Assign an Incident Commander (IC) — one person owns coordination

**Severity definitions:**

| Level | Impact | Response SLA | Example |
|-------|--------|-------------|---------|
| P1 (Critical) | Full service outage or data loss | Respond in 5 min | Payment processing down |
| P2 (High) | Major feature broken for many users | Respond in 15 min | Login failing for 30% of users |
| P3 (Medium) | Degraded performance or partial feature failure | Respond in 1 hour | Reports loading slowly |
| P4 (Low) | Minor issue, workaround exists | Next business day | Cosmetic bug on admin page |

See: [references/severity-runbook.md](references/severity-runbook.md)

### Phase 2: Communicate

**Core concept:** Proactive, clear communication to stakeholders while the incident is ongoing.

**Why it matters:** Silence during an incident causes panic, floods support channels, and erodes trust. Regular updates — even "no new information" — keep stakeholders calm.

**Key practices:**
- Post an initial incident message within 5 minutes of declaration
- Update every 15–30 minutes during active incidents
- Use a public status page for customer-facing incidents
- Assign a Communications Lead (separate from IC for P1/P2)
- Avoid technical jargon in customer-facing updates

**Communication template:**
```
[INCIDENT UPDATE - 14:32]
Status: Investigating
Impact: Users are unable to complete checkout
Started: ~14:15
Actions taken: Rolled back v2.3.1 deployment, monitoring
Next update: 15:00
```

### Phase 3: Investigate & Contain

**Core concept:** Find the proximate cause fast and take action to limit impact — even if you don't fully understand why yet.

**Why it matters:** A partial fix that reduces impact by 80% is far better than waiting for a perfect fix.

**Investigation checklist:**
- What changed recently? (deployments, config changes, feature flags, infrastructure)
- Check dashboards: error rate, latency, saturation, traffic
- Check logs for error spikes correlated with impact start time
- Check dependency health (databases, external APIs, third-party services)
- Use the 5-Whys to drill from symptom to cause

**Containment options (fastest to slowest):**
1. Roll back the most recent deployment
2. Disable the feature flag that introduced the change
3. Restart the affected service
4. Scale up capacity
5. Implement a hotfix

### Phase 4: Resolve & Verify

**Core concept:** Confirm the incident is fully resolved before declaring it closed.

**Why it matters:** Premature resolution declarations cause confusion and erode trust when the issue resurfaces.

**Key practices:**
- Verify all affected metrics have returned to baseline
- Check with Support that ticket volume has dropped
- Monitor for 15–30 minutes post-fix before declaring resolved
- Send a resolution message to all stakeholders

### Phase 5: Post-Mortem

**Core concept:** A blameless, structured retrospective that turns the incident into a system improvement.

**Why it matters:** Without structured learning, the same incidents recur. Post-mortems are the highest-leverage reliability investment.

**Post-mortem structure:**
1. **Summary** — What happened, impact, duration
2. **Timeline** — Chronological events from first detection to resolution
3. **Root Cause** — The underlying system/process failure (not the human)
4. **Contributing Factors** — Other conditions that made the incident worse
5. **Action Items** — Specific, owned, time-bounded improvements
6. **What Went Well** — Reinforce good practices

**Blameless rule:** The post-mortem identifies system and process failures, not individual failures. People make mistakes — systems should be designed to prevent or contain them.

See: [references/postmortem-template.md](references/postmortem-template.md)

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|-----|
| No Incident Commander assigned | Multiple people pulling in different directions | Always assign IC in the first 2 minutes |
| Trying to fix before containing | Extends outage duration | Roll back or disable first; diagnose after |
| Updating stakeholders only when resolved | Creates panic and escalation calls | Send updates every 15–30 min, even "no change" |
| Blaming individuals in post-mortem | Kills psychological safety, people hide future mistakes | Enforce blameless language; focus on system design |
| Action items with no owner or deadline | Nothing gets fixed | Every action item: owner + due date |

## Quick Diagnostic

| Question | If No | Action |
|----------|-------|--------|
| Is an Incident Commander assigned? | Coordination chaos | Assign IC immediately |
| Have stakeholders been notified? | Escalation calls incoming | Send initial communication now |
| Has anything changed in the last 24h? | Missing the likely cause | Check deployment log and config history |
| Are all metrics back to baseline? | Incident not fully resolved | Continue monitoring before closing |
| Does the post-mortem have owner + deadline per action? | Action items will be forgotten | Add owner and due date to every item |

## Reference Files

- [references/severity-runbook.md](references/severity-runbook.md) — Severity level definitions and escalation contacts
- [references/postmortem-template.md](references/postmortem-template.md) — Blank post-mortem document template
