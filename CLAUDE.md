# CLAUDE.md

This file provides guidance to Claude Code when working with skills in this repository.

## Repository Purpose

This is the organization-wide skills library for Claude Code agents. Skills provide specialized domain knowledge, frameworks, and SOPs for each department: Technology, Marketing, Sales, Construction, Hospitality Operations, and Construction Operations.

## Repository Structure

```
{department}/                   # each department folder IS one plugin
├── .claude-plugin/
│   └── plugin.json            # Plugin manifest (name, version, author)
└── skills/
    └── {skill-name}/
        ├── SKILL.md           # Main skill file (YAML frontmatter + markdown instructions)
        └── references/        # Supporting reference files (optional, 1500–3000 words each)
            └── *.md
_templates/
└── SKILL-TEMPLATE.md          # Blank template for new skills
.claude-plugin/
└── marketplace.json           # Marketplace catalog (lists each department plugin by source)
CLAUDE.md                      # This file
README.md                      # Full skill catalog
```

> **Plugin layout matters.** For skills to surface in the Claude desktop app, each
> department is a plugin: a `.claude-plugin/plugin.json` manifest plus skills nested
> under a `skills/` subdirectory. Skills placed directly in the department root are
> NOT discovered. The `marketing` folder backs the `marketing` plugin; Lohono brand
> skills live in their own `lohono-marketing/` plugin folder.

## Departments

| Folder | Department |
|--------|-----------|
| `technology/` | Technology & Engineering |
| `marketing/` | Marketing & Communications |
| `sales/` | Sales & Business Development |
| `construction/` | Construction (Project Side) |
| `hospitality-operations/` | Hospitality Operations |
| `construction-operations/` | Construction Operations (Site Side) |

## Skill File Format

Each skill has a `SKILL.md` with this structure:

```markdown
---
name: skill-name
description: 'What this skill does and when to use it. Trigger phrases: "keyword 1", "keyword 2". Also use when X, Y, or Z scenario occurs.'
license: proprietary
metadata:
  author: your-org
  version: "1.0.0"
  department: technology
---

# Skill Title

One paragraph introduction.

## Core Principle

**Bold statement.** Foundation paragraph.

## Scoring

**Goal: 10/10.** Rate 0–10 based on adherence to the principles below...

## Framework Sections
...

## Common Mistakes
(Table: Mistake | Why It Fails | Fix)

## Quick Diagnostic
(Table: Question | If No | Action)
```

### Required Fields
- `name`: Unique identifier (lowercase, hyphens, max 64 chars)
- `description`: What it does and when to trigger it (max 1024 chars)
- `metadata.department`: The owning department

## Adding New Skills

1. Create `{department}/skills/{skill-name}/SKILL.md` — copy from `_templates/SKILL-TEMPLATE.md`
2. Add supporting files to `{department}/skills/{skill-name}/references/` (optional)
3. Add the skill to `README.md` — catalog table + skill details section
4. Add the skill to `.claude-plugin/marketplace.json`

## Versioning

- **MAJOR**: Complete rewrite or breaking change
- **MINOR**: New content, new sections
- **PATCH**: Typo fixes, small clarifications

Always bump the version in `SKILL.md` frontmatter when editing a skill.

## Commit Policy

Commit directly to main. Use conventional commit messages:
- `feat(technology): add incident-response skill`
- `fix(sales): correct qualification framework`
- `docs: update README catalog`

## Team Memory

The `team-memory/` directory holds shared knowledge that persists across sessions and team members. It is version-controlled and shared via git — any team member who pushes a memory entry makes it available to the whole team on their next `git pull`.

**At the start of every session:**
1. Read `team-memory/MEMORY.md`.
2. Load any files listed there that are relevant to the current task.
3. Apply the loaded knowledge throughout the session without being asked.

**Memory types:**

| Folder | Type | What it contains |
|--------|------|-----------------|
| `team-memory/feedback/` | Feedback | Prompting patterns that work or don't — apply these proactively |
| `team-memory/project/` | Project | Active decisions, constraints, initiatives — use to inform suggestions |
| `team-memory/reference/` | Reference | Where things live externally — check before asking the user |
| `team-memory/domain/` | Domain | Isprava-specific terms and rules — apply these definitions always |

**When to save a new memory:**
- A pattern that surprised you or contradicts a default assumption
- A decision whose *why* is not in the code or git history
- A term that means something specific at Isprava
- A pointer to an external resource that Claude would otherwise have to ask about

See `team-memory/CONTRIBUTING.md` for how to add, update, or remove entries.

## Feature Context Chain

When a skill produces a deliverable for a named feature (PRD, spec document, test suite, etc.), it must save a compact context file so downstream skills can pick up where it left off — without the user needing to re-brief the next team.

### Protocol for every isp- skill

**On start:**
1. Determine the feature slug (derive from the output filename the user provides, or ask once: "What is the feature name or slug for this work?").
2. Check `team-memory/features/<feature-slug>/` for any existing context files.
3. If context files exist — load them and apply throughout the session. Do not ask about scope, roles, requirements, or decisions already captured there.

**On completion:**
1. After writing the main deliverable file, extract a compact context summary.
2. Write it to `team-memory/features/<feature-slug>/<phase>-context.md` using the template at `team-memory/features/_TEMPLATE.md`.
3. Confirm to the user: `Feature context saved → team-memory/features/<feature-slug>/<phase>-context.md`

### What each phase saves

| Skill | Context file | What to capture |
|-------|-------------|-----------------|
| `isp-prd-builder` | `prd-context.md` | Problem statement, user roles, scope (in/out), Must requirements, open questions, impacted areas |
| `isp-tech-specs` | `tech-specs-context.md` | Architecture decisions, new/modified files, API contracts, breaking changes, risks |
| `isp-test-cases` | `test-cases-context.md` | Coverage summary, uncovered requirements, regression risks tested, accessibility gaps |
| `isp-checklist` | `checklist-context.md` | CL item count by tier, high-complexity items, items flagged for team review |
| `isp-effort-estimate` | `effort-context.md` | Effort ranges by mode, key assumptions, high-uncertainty items |
| `isp-deliverable` | — | Reads all; does not save a new context file |

### Feature slug convention

Lowercase the feature name, replace spaces with hyphens.
`WhatsApp booking confirmation` → `whatsapp-booking-confirmation`
