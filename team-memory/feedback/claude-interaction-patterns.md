---
name: claude-interaction-patterns
description: Patterns that work well and patterns to avoid when working with Claude in this repository — accumulated from team sessions
metadata:
  type: feedback
  updated: 2026-05-25
---

# Claude Interaction Patterns

Learnings about how to get the best results from Claude Code in this repo.

**Why:** Collected from real sessions — these save time and avoid known frustrations.
**How to apply:** Apply these patterns before and during every session.

---

## What works well

| Pattern | When to use | Why it works |
|---------|------------|-------------|
| Provide a one-line idea + one sentence of context | When starting isp_prd_builder or any feature analysis skill | Reduces the number of inference questions Claude has to ask |
| Reference the skill by name (e.g. "use isp_gap_audit") | When you know exactly which skill fits | Skips the trigger-phrase matching and goes straight to the skill |
| Confirm the "Today vs. After" table in Round 3 of PRD sessions | During isp_prd_builder sessions | Catches misunderstandings before the full PRD is drafted |
| State what you already know and what you need | Any research or analysis task | Prevents Claude from repeating work you've done |

---

## What to avoid

| Pattern | Why it fails | Do this instead |
|---------|-------------|----------------|
| Asking Claude to "just figure it out" without any context | Produces generic output; wastes rounds on clarification | Provide at minimum: who it's for and what problem it solves |
| Saying "make it better" without specifying what "better" means | Claude will make arbitrary improvements that may not match intent | Name the dimension: speed, clarity, completeness, tone, etc. |
| Asking for a complete implementation plan in one message | Produces shallow output; misses edge cases | Use the isp_ phase skills sequentially with review between phases |
| Skipping confirmation steps mid-skill | Errors compound across phases | Confirm tables and summaries when the skill asks — it asks for a reason |

---

## Add a pattern

Copy this format and add a row to the relevant table above:

```
| [What you did] | [When / context] | [Why it worked or failed] |
```

Then update the `updated` date in the frontmatter and commit.
