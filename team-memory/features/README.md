# Feature Context Chain

Each folder here holds the shared context for one feature — accumulated as each skill phase runs. When a skill finishes, it saves a context file here. When the next skill starts on the same feature, it reads what's already been learned.

This means Product can run `isp-prd-builder` and Dev can run `isp-tech-specs` days later — Dev picks up everything Product discovered without needing to be briefed.

---

## How it works

```
isp-prd-builder   → saves  prd-context.md
       ↓
isp-tech-specs    → reads  prd-context.md
                  → saves  tech-specs-context.md
       ↓
isp-test-cases    → reads  prd-context.md + tech-specs-context.md
                  → saves  test-cases-context.md
```

Each context file is a compact summary — not the full deliverable. The full deliverable (PRD, spec doc, test suite) is saved as its own output file. The context file captures only what downstream skills need: decisions, scope, roles, risks, open questions.

---

## Directory structure

```
team-memory/features/
├── README.md                            ← this file
├── _TEMPLATE.md                         ← copy this when adding a new phase context
└── <feature-slug>/
    ├── prd-context.md                   ← saved by isp-prd-builder
    ├── tech-specs-context.md            ← saved by isp-tech-specs
    ├── test-cases-context.md            ← saved by isp-test-cases
    └── (other phase contexts as needed)
```

**Feature slug convention:** lowercase feature name, hyphens for spaces.
`WhatsApp booking confirmation` → `whatsapp-booking-confirmation`

---

## Which skills save and read context

| Skill | Reads | Saves |
|-------|-------|-------|
| `isp-prd-builder` | — | `prd-context.md` |
| `isp-tech-specs` | `prd-context.md` | `tech-specs-context.md` |
| `isp-test-cases` | `prd-context.md`, `tech-specs-context.md` | `test-cases-context.md` |
| `isp-effort-estimate` | `prd-context.md`, `tech-specs-context.md` | `effort-context.md` |
| `isp-checklist` | `prd-context.md` | `checklist-context.md` |
| `isp-deliverable` | all context files present | — |

---

## Lifecycle of a feature context folder

1. **Product** runs `isp-prd-builder` → folder created, `prd-context.md` written
2. **Dev** runs `isp-tech-specs` → reads `prd-context.md`, writes `tech-specs-context.md`
3. **QA** runs `isp-test-cases` → reads both, writes `test-cases-context.md`
4. **PM** runs `isp-deliverable` → reads all context files, assembles final deliverable
5. After the feature ships → folder can be archived or deleted

---

## Adding context for a new skill phase

Use `_TEMPLATE.md` as your starting point. Save the file as `team-memory/features/<feature-slug>/<phase>-context.md`.
