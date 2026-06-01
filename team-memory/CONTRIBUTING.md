# Contributing to Team Memory

This directory holds shared knowledge that Claude Code loads at the start of every session. Learnings added here are available to every team member on their next `git pull`.

---

## How it works

1. Claude reads `team-memory/MEMORY.md` at session start (instructed by `CLAUDE.md`).
2. Claude loads the files listed there that are relevant to the current task.
3. When you add a new memory file and push, every teammate gets it automatically.

---

## Memory types

| Type | Folder | What belongs here |
|------|--------|------------------|
| **Feedback** | `feedback/` | What works / what doesn't when prompting Claude — patterns, corrections, confirmed approaches |
| **Project** | `project/` | Active initiatives, architectural decisions, constraints, deadlines |
| **Reference** | `reference/` | Where things live — Linear boards, Figma files, Confluence spaces, Slack channels |
| **Domain** | `domain/` | Isprava-specific terminology, business rules, domain concepts |

---

## Adding a new memory

### Option A — Add to an existing file

Open the relevant file, add your entry to the appropriate table, update the `updated` date in the frontmatter, and commit.

```
git add team-memory/<type>/<file>.md
git commit -m "docs(team-memory): add [what you added]"
git push
```

### Option B — Create a new file

Use this frontmatter template:

```markdown
---
name: short-kebab-case-slug
description: One-line summary of what this memory contains and when to use it
metadata:
  type: feedback | project | reference | domain
  updated: YYYY-MM-DD
---

# Title

Content here.
```

Then add a pointer to `MEMORY.md`:

```markdown
- [Title](type/filename.md) — one-line hook describing what's inside
```

Commit both files together:

```
git add team-memory/MEMORY.md team-memory/<type>/<file>.md
git commit -m "docs(team-memory): add [memory name]"
git push
```

---

## What makes a good memory

| Good | Not good |
|------|---------|
| A pattern that surprised you — not obvious from the code or docs | Obvious things any developer would know |
| A decision with a *why* — reason it was made | A decision without context |
| A term that means something different at Isprava than elsewhere | Standard industry definitions |
| A pointer to where something lives externally | Information that's already in the code or README |

**Rule of thumb:** If a future team member could figure it out by reading the codebase or asking Google, it doesn't need to be here.

---

## Updating or removing a memory

- **Update:** Edit the file, update the `updated` date, commit.
- **Remove:** Delete the file and remove its line from `MEMORY.md`, commit.
- **Outdated info is worse than no info** — if a memory is stale, remove or fix it rather than leaving it.

---

## Commit message convention

```
docs(team-memory): add [description]
docs(team-memory): update [file] — [what changed]
docs(team-memory): remove [file] — [why]
```
