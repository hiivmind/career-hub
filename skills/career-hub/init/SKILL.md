---
name: career-hub-init
description: Scaffold an empty, compliant career hub in the current working directory. Produces the mandated 7-category structure (a.foundations through g.backlog), PRINCIPLES.md, README.md index, and stub files with frontmatter and TODO markers. Use when starting a new career-facts repository. Refuses if cwd already contains a hub or is non-empty with unrelated content.
---

# career-hub-init — Scaffold a Career Hub

Scaffold an empty, compliant career hub at the current working directory.

## When Claude Invokes This

The user wants to start a fresh career hub. Typical prompts:
- "Create a career hub here"
- "Scaffold a career-facts repo"
- "Start a new personal knowledge base for my CV / LinkedIn content"

See `../references/hub-detection.md` for when to refuse.

## Behaviour

### Step 1 — Confirm

Check that `cwd`:
- Does not already contain a hub (no `PRINCIPLES.md`, no full category directories — see `hub-detection.md`).
- Is empty or contains only `.gitignore`, `README.md`, or similar scaffolding remnants.

Ask the user:
```
Create a career hub at <cwd>?

This will create approximately 40 files:
- PRINCIPLES.md (governance), README.md (index)
- 7 category directories (a.foundations through g.backlog)
- a.foundations: 4 seeded files (identity, positioning, biographical-facts, operating-notes)
- b.history, c.projects, g.backlog: category READMEs only (populate via `build`)
- d.capabilities: 6 skeleton capability cards
- e.artefacts: README + index.md
- f.pipeline: 4 working docs (target-roles, unwritten-case-studies, open-threads, application-log)
- docs/superpowers/{specs,plans}/

Proceed? (y/n)
```

On explicit `y`, proceed. On `n` or ambiguous response, stop.

### Step 2 — Create Directory Structure

Use `Bash`:
```bash
mkdir -p <cwd>/{a.foundations,b.history,c.projects,d.capabilities,e.artefacts,f.pipeline,g.backlog,docs/superpowers/specs,docs/superpowers/plans}
```

### Step 3 — Seed Files

Use `Write` to create each file per the templates in `../references/templates.md`. File list and contents:

**Root level:**

- `PRINCIPLES.md` — full governance document (see below for content skeleton).
- `README.md` — cross-category index table.
- `.gitignore` — standard ignores.

**`a.foundations/` (4 files):**

- `identity.md`, `positioning.md`, `biographical-facts.md`, `operating-notes.md` — all from `templates.md` templates, with `<!-- TODO -->` markers seeded for the user to fill in.

**`b.history/`, `c.projects/`, `g.backlog/` — empty at init except:**

- `b.history/README.md` — one-line pointer: "Populate via `build roles`."
- `c.projects/README.md` — one-line pointer: "Populate via `build projects`."
- `g.backlog/README.md` — from the `g.backlog/README.md` template.

**`d.capabilities/` (6 skeleton capability cards):**

- `languages.md`, `data-stack.md`, `ml-statistics.md`, `domain-expertise.md`, `infra-platforms.md`, `credentials.md` — each from the `d.capabilities` template, with `capability` frontmatter field set to the file's topic and body as `<!-- TODO -->` markers.

**`e.artefacts/` (2 files):**

- `README.md` — directory rationale template.
- `index.md` — artefact index template.

**`f.pipeline/` (4 files):**

- `target-roles.md`, `unwritten-case-studies.md`, `open-threads.md`, `application-log.md` — all from their respective `f.pipeline` templates.

### Step 4 — PRINCIPLES.md skeleton

The `PRINCIPLES.md` created at init must include at minimum:

```markdown
---
visibility: private
audience: both
status: active
last_updated: <today>
---

# PRINCIPLES — Governance for this Career Hub

## Quick Reference

<table summarising: category precedence, visibility filter for publish, .private.md convention>

## Why This Directory Exists

<Hub-first philosophy, 2-3 sentences>

## Visibility Taxonomy

<copy from ../skills/career-hub/references/taxonomy.md axis 2>

## Confidential Sibling Files (`.private.md`)

<copy from taxonomy.md>

## Audience Taxonomy

<copy from taxonomy.md axis 3>

## Status Markers

<copy from taxonomy.md axis 4>

## Category Precedence

<copy from taxonomy.md>

## Templates

<pointer to templates.md in skill package; note that each category has a mandated template>

## Confidential Sibling Pattern

<how to create and use .private.md siblings>

## Cross-Linking Convention

<relative links between categories>

## Prior Art

<acknowledge olegvg/resume-tailor-plugin, nyinyinyanlin/profile-vault-obsidian, erichowens/career-biographer, jacksenechal/resume, demansou/resume-builder>
```

### Step 5 — README.md skeleton

The `README.md` created at init must include:

```markdown
# <hub-name> — Canonical Career Hub

> See [PRINCIPLES.md](PRINCIPLES.md) for governance.

Canonical source of career facts for <user>. Downstream CVs, GitHub profiles, LinkedIn content, and published case studies render from here.

## a. Foundations

| Document | Visibility | Summary |
|----------|------------|---------|
| [identity](a.foundations/identity.md) | private | Name, location, contact, public links |
| [positioning](a.foundations/positioning.md) | private | Alternative professional narratives by audience |
| [biographical-facts](a.foundations/biographical-facts.md) | private | Verifiable claims with verification methods |
| [operating-notes](a.foundations/operating-notes.md) | private | Cross-surface consistency rules |

## b. History

*Populate via `build roles`.*

## c. Projects

*Populate via `build projects`.*

## d. Capabilities

| Document | Visibility | Summary |
|----------|------------|---------|
| [languages](d.capabilities/languages.md) | public | Programming and data languages |
| [data-stack](d.capabilities/data-stack.md) | public | Modern data tooling |
| [ml-statistics](d.capabilities/ml-statistics.md) | public | ML and statistical methods |
| [domain-expertise](d.capabilities/domain-expertise.md) | public | Domain knowledge (credit risk, etc.) |
| [infra-platforms](d.capabilities/infra-platforms.md) | public | Infrastructure and platforms |
| [credentials](d.capabilities/credentials.md) | public | Education, awards, public artefacts |

## e. Artefacts

| Document | Purpose |
|----------|---------|
| [README](e.artefacts/README.md) | Why this directory is pointers-only |
| [index](e.artefacts/index.md) | Pointer table to rendered outputs |

## f. Pipeline

| Document | Visibility | Summary |
|----------|------------|---------|
| [target-roles](f.pipeline/target-roles.md) | private | Current target roles and application status |
| [unwritten-case-studies](f.pipeline/unwritten-case-studies.md) | private | Prioritised case-study backlog |
| [open-threads](f.pipeline/open-threads.md) | private | Loose ideas and half-started writeups |
| [application-log](f.pipeline/application-log.md) | private | Chronological application log |

## g. Backlog

| Document | Visibility | Summary |
|----------|------------|---------|
| [README](g.backlog/README.md) | private | Index of open threads deferred from interviews |
```

### Step 6 — `git init` and first commit

```bash
cd <cwd>
git init
git add -A
git commit -m "chore: initial scaffold of career hub per career-hub-init v1"
```

If the user already has `cwd` under git, skip `git init` and add-commit on the current branch.

### Step 7 — Print next-step suggestion

```
Career hub scaffolded at <cwd>.

Next steps:
- `build foundations` — fill identity, positioning, biographical facts, operating notes.
- `build roles` — start populating role cards.
- `build projects` — start populating project case studies.
- `build capabilities` — enrich the 6 seed capability cards.

Or `build` with no argument to get a menu.
```

## Refuses

- `cwd` already contains a hub. Direct the user to `build`.
- `cwd` is non-empty with content not matching init-compatible scaffolding.

## Does Not

- Populate role / project content beyond stubs (that is `build`'s job).
- Assume a remote git host — the user decides whether to push.
- Publish anything.
