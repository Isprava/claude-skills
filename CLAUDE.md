# CLAUDE.md

This file provides guidance to Claude Code when working with skills in this repository.

## Repository Purpose

This is the organization-wide skills library for Claude Code agents. Skills provide specialized domain knowledge, frameworks, and SOPs for each department: Technology, Marketing, Sales, Construction, Hospitality Operations, and Construction Operations.

## Repository Structure

```
{department}/
├── {skill-name}/
│   ├── SKILL.md           # Main skill file (YAML frontmatter + markdown instructions)
│   └── references/        # Supporting reference files (optional, 1500–3000 words each)
│       └── *.md
_templates/
└── SKILL-TEMPLATE.md      # Blank template for new skills
.claude-plugin/
└── marketplace.json       # Plugin/marketplace configuration
CLAUDE.md                  # This file
README.md                  # Full skill catalog
```

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

1. Create `{department}/{skill-name}/SKILL.md` — copy from `_templates/SKILL-TEMPLATE.md`
2. Add supporting files to `{department}/{skill-name}/references/` (optional)
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
