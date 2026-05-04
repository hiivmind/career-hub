# Career Hub Skill Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Implement the `career-hub` Claude Code skill (init + build + publish sub-skills) as a sibling of the existing `cv-opti` skill in the `cv-optimiser` repository. The skill turns the interview-plus-rendering process piloted on `nathanielramm-central` into a repeatable, documented pattern.

**Architecture:** Documented-thin Claude Code skill — markdown SKILL.md files plus reference markdown files, no code. Umbrella skill at `skills/career-hub/SKILL.md`, three phased sub-skills at `init/`, `build/`, `publish/`, shared references at `skills/career-hub/references/`, extensible render targets at `skills/career-hub/publish/targets/`.

**Tech Stack:** Markdown with YAML frontmatter. No runtime, no build, no tests — "tests" are read-back-and-verify-against-spec-section passes. No Python, no code. Claude performs file operations via Read/Write/Edit/Bash at skill invocation time.

**Note on version control:** `cv-optimiser` is currently not a git repository (verified via `git rev-parse --is-inside-work-tree` at plan time). Task 1 initialises git so every subsequent task can commit. If the operator prefers no version control, they skip Task 1 and the per-task commit steps.

**Note on TDD:** Since this is a docs-only skill with no executable code, the Test-Driven Development practice is adapted: each task's "verify" step reads the newly-written file back and cross-checks it against the spec section it implements. The verify step fails if content is missing or inconsistent.

---

## File Structure

Files created in this plan (13 markdown files + 1 `.gitignore`):

```
cv-optimiser/
├── .gitignore                                              (Task 1)
└── skills/career-hub/
    ├── SKILL.md                                            (Task 5)
    ├── references/
    │   ├── taxonomy.md                                     (Task 2)
    │   ├── templates.md                                    (Task 3)
    │   └── hub-detection.md                                (Task 4)
    ├── init/
    │   └── SKILL.md                                        (Task 6)
    ├── build/
    │   └── SKILL.md                                        (Task 7)
    └── publish/
        ├── SKILL.md                                        (Task 8)
        └── targets/
            ├── cv.md                                       (Task 9)
            ├── linkedin.md                                 (Task 10)
            ├── github-profile.md                           (Task 11)
            └── _adding-targets.md                          (Task 12)
```

Final self-review task: Task 13.

**Spec reference used throughout:** `/home/nathanielramm/git/discreteds/cv-optimiser/docs/superpowers/specs/2026-04-20-career-hub-skill-design.md`.

---

## Task 1: Initialise git repo and scaffold skill directory

**Files:**
- Create: `/home/nathanielramm/git/discreteds/cv-optimiser/.gitignore`
- Create (directories only): `skills/career-hub/`, `skills/career-hub/references/`, `skills/career-hub/init/`, `skills/career-hub/build/`, `skills/career-hub/publish/`, `skills/career-hub/publish/targets/`

- [ ] **Step 1: Initialise git repo**

Run:
```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git init
```
Expected: `Initialized empty Git repository in /home/nathanielramm/git/discreteds/cv-optimiser/.git/`

- [ ] **Step 2: Create `.gitignore`**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/.gitignore` with:

```gitignore
# OS / editor
.DS_Store
.vscode/
.idea/
*.swp

# Python (if ever used)
__pycache__/
*.pyc
.venv/
.env

# Node
node_modules/

# Build artefacts
*.docx
*.pdf
!skills/**/*.docx
!skills/**/*.pdf
```

- [ ] **Step 3: Create directory structure**

Run:
```bash
mkdir -p /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/{references,init,build,publish/targets}
```

- [ ] **Step 4: Verify structure**

Run:
```bash
find /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub -type d | sort
```
Expected output:
```
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/build
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/init
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references
```

- [ ] **Step 5: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add .gitignore && git commit -m "chore: init cv-optimiser as git repo; scaffold career-hub skill dirs"
```

---

## Task 2: `references/taxonomy.md`

**Files:**
- Create: `skills/career-hub/references/taxonomy.md`

Purpose: the 4 axes (category, visibility, audience, status) plus the `.private.md` sibling convention and category precedence. Referenced by every sub-skill.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references/taxonomy.md` with:

```markdown
# Taxonomy — Four Axes plus Conventions

Every file in a career hub declares four things in YAML frontmatter. Rendering and interview behaviour are driven by these axes. Two conventions (category precedence, `.private.md` siblings) sit on top of the axes.

## Axis 1 — Category

Files live under one of seven top-level category directories:

| Category | Purpose |
|----------|---------|
| `a.foundations/` | Canonical facts about the person — identity, positioning, biographical-facts, operating-notes. |
| `b.history/` | Role cards, one per paid or formal engagement. |
| `c.projects/` | Project case-study cards. |
| `d.capabilities/` | Claim-plus-evidence cards per capability area. |
| `e.artefacts/` | Pointer index to rendered outputs and evidence artefacts. |
| `f.pipeline/` | Forward-looking working docs (target roles, unwritten case studies, open threads, application log). |
| `g.backlog/` | One file per deferred item. Promoted to a canonical home when resolved. |

### Precedence rule

When a fact could live in two categories, the **lower-letter category wins**. Other categories reference via relative cross-links and do not duplicate content.

Worked example: a claim like *"directed a 4-person team on the stress-testing engagement"* has a natural home in `b.history/<role>.md` (role-level context, lower letter) AND in `c.projects/stress-testing.md` (project-level team detail). Per precedence, the fact is authored in `b.history/` and `c.projects/` links to it.

## Axis 2 — Visibility

| Value | Meaning | Examples |
|-------|---------|----------|
| `public` | Safe to render verbatim into any public artefact. | Current-ventures descriptions, publicly-known scale numbers, publicly-known clients, published case studies. |
| `private` | For the user and AI agents working with them only. Skippable by most publish targets. | Draft positioning notes, application-log entries, reference-contact names, unpublished case-study drafts, some client identities. |
| `confidential` | Sensitive specifics; never leaves the hub regardless of target. | Internal model names, specific regulatory submission content, unresolved politics, security specifics. |

`publish` filters on this axis per-target. Confidential content is never emitted.

## Axis 3 — Audience

| Value | Meaning |
|-------|---------|
| `human` | Primary audience is a human reader. Use readable prose. |
| `ai-agent` | Primary audience is an AI agent consuming the file for context (e.g. a publish-time renderer). Structure-heavy, prose-light. |
| `both` | Written to serve both. Most hub files are this. |

## Axis 4 — Status

| Value | Meaning |
|-------|---------|
| `active` | Current, reviewed, and rendering-ready. |
| `draft` | Stub or in-progress. May contain `<!-- TODO -->` markers. Excluded from `publish` unless target spec allows drafts. |
| `archived` | Deletion candidate. Kept for historical reference; excluded from `publish`. There is no `deprecated`. |

## Convention — `.private.md` confidential sibling files

For a role or project with a public card, candid retrospection (politics, failures, proprietary details, people) lives in a sibling file alongside the public one:

- Public file: `b.history/<role>.md` — `visibility: public`
- Confidential sibling: `b.history/<role>.private.md` — `visibility: confidential`

Same frontmatter shape. Sibling adds a `## Candid Notes` section and any other confidential-only sections. `publish` never emits confidential siblings. Keeps the public file clean and unfiltered, preserves the record.

## Universal frontmatter

Every file starts with:

```yaml
---
visibility: public | private | confidential
audience: human | ai-agent | both
status: active | draft | archived
last_updated: YYYY-MM-DD
---
```

Category-specific additions to frontmatter and category-specific body templates live in `templates.md` (sibling of this file).
```

- [ ] **Step 2: Verify**

Run:
```bash
head -3 /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references/taxonomy.md
```
Expected first three lines:
```
# Taxonomy — Four Axes plus Conventions

Every file in a career hub declares four things in YAML frontmatter. Rendering and interview behaviour are driven by these axes. Two conventions (category precedence, `.private.md` siblings) sit on top of the axes.
```

Confirm by reading back that all four axes, precedence rule, `.private.md` convention, and universal frontmatter are covered (matches spec §6 principles 1-3 and §8).

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/references/taxonomy.md && git commit -m "feat(career-hub): add taxonomy reference"
```

---

## Task 3: `references/templates.md`

**Files:**
- Create: `skills/career-hub/references/templates.md`

Purpose: universal frontmatter plus per-category body templates. Canonical template source for `init` (creating stubs) and `build` (extending stubs).

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references/templates.md` with:

````markdown
# Templates

Universal frontmatter plus per-category body templates. Used by `init` to seed stubs and by `build` to extend stubs. Templates are mandatory shapes; content is free-form within the shape.

See `taxonomy.md` for the four axes and the `.private.md` sibling convention.

## Universal frontmatter

Every file starts with:

```yaml
---
visibility: public | private | confidential
audience: human | ai-agent | both
status: active | draft | archived
last_updated: YYYY-MM-DD
---
```

## `a.foundations/` — canonical facts

Four specific files. Each has its own shape.

### `a.foundations/identity.md`

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# Identity

| Field | Value |
|-------|-------|
| Full name | <!-- name --> |
| Location | <!-- city, country --> |
| Email (primary) | <!-- email --> |
| Phone | <!-- phone --> |
| LinkedIn | <!-- https://... --> |
| GitHub | <!-- https://... --> |
| Kaggle / other | <!-- optional --> |
| Website | <!-- optional --> |

## Public vs private contact

<!-- Which of the above are safe on a public CV or GitHub profile vs private/application-only? -->
```

### `a.foundations/positioning.md`

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# Positioning

Alternative professional narratives by audience. One variant is marked `active` at a time.

| Label | Tagline | Primary Audience | Active |
|-------|---------|------------------|:------:|
| <!-- variant 1 --> | <!-- tagline --> | <!-- audience --> | |
| <!-- variant 2 --> | <!-- tagline --> | <!-- audience --> | |

## Notes on variant use

- Active variant drives the default CV framing and public profile content.
- Variants are positioning, not identity — all claims across variants are verifiable; difference is emphasis.
- Do not mix variants in the same application.
```

### `a.foundations/biographical-facts.md`

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# Biographical Facts

Verifiable claims used across all downstream artefacts. When a claim appears on a CV, LinkedIn, or profile README, it traces back to an entry here.

| Claim | Value | Verification Method | Last Verified |
|-------|-------|---------------------|---------------|
| <!-- claim --> | <!-- value --> | <!-- method --> | YYYY-MM-DD |
```

### `a.foundations/operating-notes.md`

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# Operating Notes

Cross-surface consistency rules and conventions for this hub.

## Conventions

- <!-- rule --> — <!-- rationale -->

## Do not publish

- <!-- content the hub owner never wants rendered -->

## Always cross-check before posting

- <!-- consistency checks against external surfaces (LinkedIn, GitHub) -->
```

## `b.history/` — role card template

File name: `YYYY-YYYY-<employer-slug>.md` or `YYYY-<employer-slug>-<role-slug>.md` for short tenures.

```markdown
---
visibility: public
audience: both
status: draft
last_updated: YYYY-MM-DD
role: "<role title>"
employer: "<employer>"
start: YYYY-MM
end: YYYY-MM | present
---

# <role title> — <employer>

**TL;DR:** <!-- one sentence -->

## Context

<!-- division / team / reporting line / business context -->

## Scope

<!-- team size / direct reports, budget / remit, portfolio / stakeholder reach -->

## Key Systems & Projects

- [<project-slug>](../c.projects/<project-slug>.md)

## Outcomes

<!-- quantified outcomes only — no unverifiable claims -->

## Verification

- <!-- LinkedIn URL -->
- <!-- reference contact; publicly-known corroboration -->

## Related Roles

- Preceded by: [<role-file>](<role-file>.md)
- Succeeded by: [<role-file>](<role-file>.md)
```

## `c.projects/` — case-study card template

File name: `<project-slug>.md`.

```markdown
---
visibility: public | private
audience: both
status: draft
last_updated: YYYY-MM-DD
project: "<project name>"
employer: "<employer>"
via: "<optional sub-consulting vehicle>"
client: "<optional, usually private>"
dates: "YYYY-MM to YYYY-MM"
role: "<role played>"
---

# <project name>

## Headline

<!-- 2-3 sentences covering scope + key numbers + hook -->

## Problem

<!-- the real problem the project addressed, with context -->

## Approach

<!-- key design moves, architecture, team structure -->

## Result

<!-- quantified outcomes; scale; regulatory or business use -->

## Tech

<!-- technologies, in usage order -->

## Context

<!-- employer, dates, via, role -->

## Verifiability

<!-- which claims are publicly corroborable; reference contacts -->

## External Publications

<!-- links to published case studies, blogs, talks -->

## Related

- Role: [<role-file>](../b.history/<role-file>.md)
- Capabilities demonstrated:
  - [<capability>](../d.capabilities/<capability>.md)
```

## `d.capabilities/` — claim-and-evidence card template

File name: `<capability-slug>.md`.

```markdown
---
visibility: public
audience: both
status: draft
last_updated: YYYY-MM-DD
capability: "<capability name>"
---

# <capability name>

## Summary

<!-- one paragraph positioning this capability -->

## Proficiency Claim

<!-- specific claim: e.g. "Deep, current — day-to-day use in 2024-2026 across ..." -->

## Evidence

- [<role>](../b.history/<role-file>.md) — <!-- what this role evidences -->
- [<project>](../c.projects/<project-slug>.md) — <!-- what this project evidences -->

## Interview-Defensibility

<!-- specific things the user can discuss fluently in an interview; depth cues -->

## Recency Notes

<!-- when last used; what has and hasn't kept up -->
```

## `e.artefacts/index.md` — pointer-index rows

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# Artefacts Index

See this directory's [README](README.md) for the rationale and migration model.

## Canonical artefacts (source lives in this hub or is referenced from here)

| Artefact | Canonical Location | Mirror(s) | Purpose | Format | Updated | Visibility |
|----------|---------------------|-----------|---------|--------|---------|------------|
| <!-- name --> | <!-- path or URL --> | <!-- mirror --> | <!-- purpose --> | <!-- .md / .pdf / .png --> | YYYY-MM-DD | <!-- public / private --> |

## Notes

- **External canonical migration rule:** when an externally-canonical artefact migrates into the hub, update the row so `Canonical Location` points inside the hub and the external location moves to `Mirror(s)`.
- **"Last Updated" is authoritative for this row, not the artefact itself.** Update when the row's accuracy changes — not every time the artefact content is tweaked.
```

## `e.artefacts/README.md` — directory rationale

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# e.artefacts — Pointer Index, Not Content Store

This directory is a pointer index to rendered outputs and evidence artefacts. Content mostly lives elsewhere — in downstream output files, in external repositories, on disk as images/PDFs — and `index.md` tracks where.

## Why pointers-only

- Canonical content often lives outside the hub (e.g. a public case study in a product repo, a LinkedIn post, a conference slide deck). Duplicating it invites drift.
- The hub is the *source of career facts*; artefacts are rendered *from* the hub. They belong near their rendering context, not back in the hub.

## Migration rule

If an externally-canonical artefact's natural home changes and it should live inside the hub, move it to `e.artefacts/images/` or similar, then flip `index.md` so `Canonical Location` points inside the hub and the external location becomes the mirror.
```

## `f.pipeline/` — working doc shapes

### `target-roles.md`

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# Target Roles

| Role | Employer | Source | Positioning Variant | Status |
|------|----------|--------|---------------------|--------|
| <!-- role --> | <!-- employer --> | <!-- job board / referral --> | <!-- positioning variant --> | <!-- applied / shortlist / ignore --> |
```

### `unwritten-case-studies.md`

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# Unwritten Case Studies

Prioritised backlog of project writeups not yet promoted to `status: active` in `c.projects/`.

| Priority | Project | Why Priority | Blockers |
|----------|---------|--------------|----------|
| <!-- 1 --> | <!-- project --> | <!-- why --> | <!-- blocker --> |
```

### `open-threads.md`

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# Open Threads

Loose ideas, half-started writeups, unresolved questions.

## Threads

- **<thread name>** — <!-- summary + current state -->
```

### `application-log.md`

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# Application Log

| Date | Role | Employer | Positioning Used | Outcome |
|------|------|----------|-------------------|---------|
| YYYY-MM-DD | <!-- role --> | <!-- employer --> | <!-- positioning variant --> | <!-- submitted / interview / offer / rejected --> |
```

## `g.backlog/` — one file per deferred item

### `g.backlog/README.md`

```markdown
---
visibility: private
audience: both
status: active
last_updated: YYYY-MM-DD
---

# g.backlog — Open Threads

Deferred items from interviews, enrichment passes, and reviews. Each item is small and self-contained; promote to the relevant category file when resolved.

## Index

| Item | Category it feeds | Status |
|------|-------------------|--------|
| <!-- item file --> | <!-- destination category --> | open / resolved |

## Conventions

- One open thread per file.
- Frontmatter: universal shape.
- Status: `open` (outstanding), `resolved` (close and delete, or archive inline note in destination file).
- When resolved, update the destination file and delete the backlog entry; commit both in one commit.
```

### Individual backlog item

```markdown
---
visibility: private
audience: both
status: open
last_updated: YYYY-MM-DD
---

# Open: <short description>

## Context

<!-- what this is about; background -->

## Missing

<!-- what specifically is missing or deferred -->

## Resolution path

<!-- how to resolve; who to ask; where to look -->

## Destination when resolved

<!-- which file in the hub receives this content -->
```

## `.private.md` confidential sibling template

File name: `<base-filename>.private.md` alongside the public file.

```markdown
---
visibility: confidential
audience: both
status: active
last_updated: YYYY-MM-DD
---

# <Base title> — Candid Notes (confidential)

> Confidential sibling of [<base file>](<base-filename>.md). Not for external rendering.

## Candid Notes

- <!-- politics, failures, proprietary details, people -->
```
````

- [ ] **Step 2: Verify**

Run:
```bash
grep -c "^## " /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references/templates.md
```
Expected: at least 10 `##` headings (universal frontmatter + 7 category sections + 1 private-sibling section + extras).

Read back and confirm every category mentioned in spec §5 has a template: `a.foundations` (4 files), `b.history`, `c.projects`, `d.capabilities`, `e.artefacts` (index + README), `f.pipeline` (4 files), `g.backlog` (README + item), plus `.private.md`.

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/references/templates.md && git commit -m "feat(career-hub): add templates reference"
```

---

## Task 4: `references/hub-detection.md`

**Files:**
- Create: `skills/career-hub/references/hub-detection.md`

Purpose: defines how sub-skills detect whether `cwd` is a career hub, how they confirm with the user before acting, and how `init` detects an empty-or-near-empty directory safely.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references/hub-detection.md` with:

```markdown
# Hub Detection

How sub-skills decide whether the current working directory is a career hub, and how they confirm before acting.

## Signals of a compliant hub

A directory is a hub if all of these are true:

1. `PRINCIPLES.md` exists at the directory root.
2. All seven category directories exist: `a.foundations/`, `b.history/`, `c.projects/`, `d.capabilities/`, `e.artefacts/`, `f.pipeline/`, `g.backlog/`.
3. `README.md` exists at the directory root.

A directory with some but not all of these is **malformed** — refuse to proceed and surface the gap.

## Sub-skill confirmation behaviour

All three sub-skills (`init`, `build`, `publish`) confirm the hub location with the user on invocation, before taking any write action.

### For `init`

Refuses if the current directory already looks like a hub (any of the three signals present).

Refuses if the current directory is non-empty and does not look like a fresh scaffold target (contains files that are not `.gitignore`, `README.md`, or a single non-hub placeholder).

Confirms with:
```
Create a career hub at <cwd>? This will create approximately 40 files
(seven category directories, PRINCIPLES.md, README.md, templates).
Proceed? (y/n)
```

Proceeds only on explicit `y`.

### For `build` and `publish`

Requires all three signals present. If any signal is missing, refuse with a message identifying the gap and suggesting `init`.

Confirms with:
```
Hub detected at <cwd>.
<summary of category stub counts, e.g. "12 roles, 8 projects, 6 capabilities, 3 open backlog items">
Proceed with <build|publish> <arg>? (y/n)
```

Proceeds only on explicit `y`.

## Why cwd-scoped, not config-based

We deliberately do not use a `~/.career-hub/config.yaml` pointer. Rationale:

- Keeps per-machine state out of home directory.
- Matches the existing `cv-opti` pattern (cwd-scoped).
- A user with multiple hubs simply `cd`s to the right one.
- Explicit confirmation on every invocation catches mistakes early.

## Multi-hub situations

A user may maintain more than one hub (personal vs client-facing, for example). Each hub is independent. Sub-skills operate on whichever hub is at `cwd` when invoked.
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c "^## " /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references/hub-detection.md
```
Expected: at least 4 `##` sections.

Confirm the file covers: three hub signals, confirmation behaviour for each sub-skill, cwd-scoped rationale (matches spec §7.1/7.2/7.3 confirm-first requirement and §9 interaction design).

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/references/hub-detection.md && git commit -m "feat(career-hub): add hub-detection reference"
```

---

## Task 5: Umbrella `skills/career-hub/SKILL.md`

**Files:**
- Create: `skills/career-hub/SKILL.md`

Purpose: entry point. Claude reads this when the skill is invoked without a sub-phase. Describes when-to-use, the end-to-end loop, visibility/taxonomy/template references, and how to enter each sub-skill.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/SKILL.md` with:

```markdown
---
name: career-hub
description: Build and maintain a canonical career hub — a markdown-plus-YAML repository that is the single source of truth for role history, project case studies, capabilities, artefacts, and pipeline. Renders downstream artefacts (CV, LinkedIn, GitHub profile) from it. Three phased sub-skills: init (scaffold), build (interview-driven enrichment), publish (render a draft target from hub content).
---

# Career Hub

Build and maintain a canonical career hub, then render downstream artefacts from it.

## When to Use

Invoke this skill when the user wants to:

- **Set up a career-facts repository** from scratch — use `init`.
- **Fill in or update role / project / capability content** via a conversational interview — use `build`.
- **Generate a CV, LinkedIn draft, or GitHub profile README** from the hub — use `publish`.

If the user wants to optimise an existing CV against a specific job description, use the sibling `cv-opti` skill instead. The two compose: `career-hub:publish cv` produces an ATS-friendly markdown CV, which `cv-opti` then tunes per-job.

## Design Philosophy

**Hub-first, rendering-second.** The hub is the source of truth; CVs, LinkedIn, and GitHub profile pages are views onto it. Every public claim traces to an entry in the hub.

**Draft-from-known-content, ask-only-gap-questions.** When `build` enriches a stub, Claude drafts from existing hub content and cross-references, and asks the user only *gap questions* — never redundant questions. Fast, low-friction enrichment; the interview-style differentiator from empathetic-open-ended predecessors.

**Every claim verifiable.** No unverifiable adjectives ("expert", "pioneered"). Scale numbers and verification methods live in `a.foundations/biographical-facts.md`. `publish` filters out confidential content; public-facing claims cross-check against the biographical-facts table.

## Three Sub-Skills

| Phase | Sub-skill | Purpose |
|-------|-----------|---------|
| 1 | [`init`](init/SKILL.md) | Scaffold an empty compliant hub at `cwd`. |
| 2 | [`build`](build/SKILL.md) | Interview-driven enrichment of hub stubs (roles, projects, capabilities, foundations). |
| 3 | [`publish`](publish/SKILL.md) | Render a draft target (CV, LinkedIn, GitHub profile, or custom) from hub content. |

Each sub-skill confirms the hub location at `cwd` before taking any write action (see [`references/hub-detection.md`](references/hub-detection.md)).

## Shared References

- [`references/taxonomy.md`](references/taxonomy.md) — four axes (category, visibility, audience, status), category precedence rule, `.private.md` sibling convention, universal frontmatter.
- [`references/templates.md`](references/templates.md) — universal frontmatter plus per-category body templates. Mandatory shapes.
- [`references/hub-detection.md`](references/hub-detection.md) — signals, confirmation dialogues, multi-hub handling.

## Hub Structure Produced by `init`

```
<hub>/
├── PRINCIPLES.md
├── README.md
├── a.foundations/
│   ├── identity.md
│   ├── positioning.md
│   ├── biographical-facts.md
│   └── operating-notes.md
├── b.history/
├── c.projects/
├── d.capabilities/
├── e.artefacts/
│   ├── README.md
│   └── index.md
├── f.pipeline/
│   ├── target-roles.md
│   ├── unwritten-case-studies.md
│   ├── open-threads.md
│   └── application-log.md
├── g.backlog/
│   └── README.md
└── docs/superpowers/
    ├── specs/
    └── plans/
```

Mandated, not configurable.

## Principles (in `PRINCIPLES.md`)

1. **Category precedence.** Lower-letter category wins; others cross-link.
2. **Visibility is explicit.** Every file declares `public | private | confidential`.
3. **Confidential sibling pattern.** `.private.md` sibling for candid retrospection.
4. **Status markers.** `active | draft | archived`. No `deprecated`.
5. **Templates for all docs.**
6. **Stubs, not blanks.** `init` seeds stubs with `<!-- TODO -->` markers.
7. **Canonical-here vs external.** `e.artefacts/index.md` tracks both with a migration rule.
8. **Hub-first.** Source of truth.
9. **Draft-from-known-content-ask-only-gap-questions.**
10. **Every claim verifiable.**

## Composition with `cv-opti`

```
career-hub:publish cv  →  skills/cv-opti/SKILL.md  →  ATS-optimised, JD-tuned CV
```

The two skills do not depend on each other at runtime but compose naturally.

## Prior Art

This skill draws on and differentiates from:

- **olegvg/resume-tailor-plugin** — single-file master profile, per-role visibility tags.
- **nyinyinyanlin/profile-vault-obsidian** — folder-per-category Obsidian vault.
- **erichowens/career-biographer + cv-creator** — interview-plus-render split, empathetic interview style.
- **jacksenechal/resume** — markdown resume with branch-based tailoring.
- **demansou/resume-builder** — evidence-mining, confidentiality-by-design.

Differentiators: category taxonomy with precedence; `.private.md` siblings; discrete phased sub-skills; gap-question-only interview posture; `e.artefacts/` with migration rule; `g.backlog/` category; hub-first philosophy.

## Future Work

Tracked for future releases, not in v1:

- `publish jsonresume` target (JSON Resume schema interop).
- `publish obsidian` target (Obsidian-vault render with wikilinks).
- `practise interview` sub-skill (voice-mode rehearsal against target roles).
- Evidence-mining mode (`build --evidence-scan` from git/docs).
- Cross-surface consistency lint (`check` sub-skill).
```

- [ ] **Step 2: Verify**

Run:
```bash
head -5 /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/SKILL.md
```
Expected first five lines contain the YAML `name: career-hub` and `description:` fields. The description is what triggers skill auto-invocation.

Read back and confirm: frontmatter present, all three sub-skills linked, three references linked, hub structure mirrors spec §5, principles match spec §6, prior art present, future work present.

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/SKILL.md && git commit -m "feat(career-hub): add umbrella SKILL.md"
```

---

## Task 6: `init/SKILL.md`

**Files:**
- Create: `skills/career-hub/init/SKILL.md`

Purpose: instructs Claude how to scaffold an empty compliant hub at `cwd`. Produces ~40 files and commits.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/init/SKILL.md` with:

````markdown
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
````

- [ ] **Step 2: Verify**

Run:
```bash
head -5 /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/init/SKILL.md
```
Expected: YAML frontmatter with `name: career-hub-init` and a `description:` field.

Read back and confirm: step-by-step behaviour matches spec §7.1; refuses conditions match spec §7.1 refuses list; PRINCIPLES.md and README.md skeletons are declared.

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/init/SKILL.md && git commit -m "feat(career-hub): add init sub-skill"
```

---

## Task 7: `build/SKILL.md`

**Files:**
- Create: `skills/career-hub/build/SKILL.md`

Purpose: interview-driven enrichment. Takes a category argument (`foundations`, `roles`, `projects`, `capabilities`) or a bare invocation that shows a menu.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/build/SKILL.md` with:

````markdown
---
name: career-hub-build
description: Interview-driven enrichment of a career hub. Given a category (foundations | roles | projects | capabilities) or a menu if no argument, reads existing stubs, drafts from known content, and asks the user only gap questions. Edits files in place, bumps last_updated, flips status from draft to active when substantively complete. Offers .private.md confidential siblings when candid content surfaces. Logs deferrals to g.backlog/ as one file per item.
---

# career-hub-build — Interview-Driven Enrichment

Enrich a career hub via conversational interview, one category at a time.

## When Claude Invokes This

Typical prompts:
- "build roles" / "build projects" / "build capabilities" / "build foundations"
- "fill out my role history"
- "let's update my career hub"

## Prerequisites

- `cwd` is a compliant hub (see `../references/hub-detection.md`). Refuse otherwise with a pointer to `init`.

## Behaviour

### Step 1 — Confirm hub

```
Hub detected at <cwd>.
- a.foundations: <4 files, X complete / Y stubs>
- b.history: <N roles, X active / Y draft>
- c.projects: <N projects, X active / Y draft>
- d.capabilities: <N cards, X active / Y skeleton>
- g.backlog: <N open threads>

Proceed with build <arg>? (y/n)
```

On explicit `y`, proceed.

### Step 2 — Select target unit(s)

**If invoked with a category argument** (`build roles`, `build projects`, `build capabilities`, `build foundations`):
- Enumerate files in that category directory.
- Ask the user the order: chronological, reverse-chronological, user-picks, auto-next-stub (next `status: draft` file in chronological order).

**If invoked bare** (`build`):
- Present a menu:
  ```
  Which category?
  1. foundations (4 files, 2 stubs)
  2. roles (12 files, 5 stubs)
  3. projects (9 files, 3 stubs)
  4. capabilities (6 skeletons)
  ```
- Wait for selection, then continue as above.

### Step 3 — For each unit, the draft-then-gap-questions loop

For each file selected:

1. **Read existing content** plus frontmatter, plus cross-references (linked roles, linked projects, linked capabilities, `a.foundations/biographical-facts.md`).
2. **Draft** a concise proposed fill-in from the known content — for each of the category's body sections (Scope, Outcomes, Verification, Related, etc.).
3. **Ask gap questions only** — never ask what is already known or derivable from cross-references. Target 2-5 gap questions per unit for a quick pass.
4. On user response, **edit the file in place**:
   - Bump `last_updated` in frontmatter.
   - Flip `status: draft → active` if the unit is now substantively complete.
   - Cross-link to related files using relative paths.
5. **Offer confidential sibling** if candid content surfaces: "This includes sensitive political / failure / proprietary content. Create a `<filename>.private.md` sibling for candid notes?" — on yes, create the sibling with the confidential template.
6. **Log deferrals** — if a claim needs external info (reference name to confirm, conference event name, etc.), create a `g.backlog/<slug>.md` entry per the backlog item template, and register it in `g.backlog/README.md` index.
7. **Handle splits** — if the user flags that a single file should be split (e.g. a founder role covering two concurrent ventures), create the split files and update cross-references + README.md entries.

### Step 4 — Update downstream

After editing any role / project / capability file, also update:

- `README.md` — if the file's row caption changed (scope, active/draft status, headline).
- `a.foundations/biographical-facts.md` — if a numerical claim, tenure, or scope has changed.
- Cross-linked files — if a name, slug, or date changed.

### Step 5 — Commit at natural breakpoints

One commit per completed unit, OR one commit per category pass — operator's choice, default to one commit per unit.

Commit message format:
```
content(<category>): enrich <slug> — <brief summary>
```

Example:
```
content(b.history): enrich 2020-2021-nab-ad-optimisation — scope, outcomes, team structure
```

## Interview Posture

**Draft from known content. Ask only gap questions.**

The skill's differentiator. Don't ask what you can infer. Don't ask what cross-references already state. Don't run a fixed question list.

For each unit, after reading, your first message to the user is:

```
**<file name>** — draft from known content:

[short proposed fill-in for each body section, marked where gaps exist]

Gap questions:
1. <specific thing you can't infer>
2. <specific thing you can't infer>
3. <specific thing you can't infer>

Or skip ahead and answer in one message if easy.
```

Keep gap questions to 3-5 per unit on a quick pass. Offer deep-dive mode on request for high-CV-weight items.

## Mode: Quick vs Deep

Default is **quick pass** — fast gap-filling, target complete unit in one exchange where possible.

**Deep dive** on request — more thorough probing, additional questions about politics / proprietary details (offer `.private.md` sibling), follow-up on stories that would make good case studies.

## Refuses

- `cwd` not a hub (per `hub-detection.md`).
- Unit already `status: active` unless user explicitly asks to re-interview.

## Does Not

- Render to external artefacts (that is `publish`'s job).
- Enforce a fixed question list.
- Re-interview active files without explicit ask.
- Populate categories it wasn't asked to populate.
````

- [ ] **Step 2: Verify**

Run:
```bash
head -5 /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/build/SKILL.md
```
Expected: YAML frontmatter with `name: career-hub-build` and a `description:` field.

Read back and confirm: matches spec §7.2 behaviour (confirm, enumerate, order, draft-gap-questions, edit, confidential sibling offer, deferral logging, README/biographical-facts updates, natural-breakpoint commits); draft-from-known-content posture is named and explained (matches spec §6 principle 9 and §3 differentiator 4); refuses matches spec §7.2.

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/build/SKILL.md && git commit -m "feat(career-hub): add build sub-skill"
```

---

## Task 8: `publish/SKILL.md`

**Files:**
- Create: `skills/career-hub/publish/SKILL.md`

Purpose: render a target artefact from hub content. Reads a target spec under `targets/`, applies visibility filter, drafts into `f.pipeline/<target>-*.md`.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/SKILL.md` with:

````markdown
---
name: career-hub-publish
description: Render a draft target artefact from career-hub content. Built-in targets — cv, linkedin, github-profile. Extensible via target spec files in targets/. Applies visibility filter (public-only by default, never confidential). Drafts into f.pipeline/<target>-draft.md inside the hub — user copy-pastes out to the destination surface. Prints a cross-surface consistency posting checklist.
---

# career-hub-publish — Render a Draft Target

Render a draft CV / LinkedIn / GitHub-profile / custom target from the career hub's canonical content.

## When Claude Invokes This

Typical prompts:
- "publish cv"
- "publish linkedin"
- "publish github-profile"
- "render a <custom-target>"

## Prerequisites

- `cwd` is a compliant hub (see `../references/hub-detection.md`). Refuse otherwise with a pointer to `init`.

## Behaviour

### Step 1 — Confirm hub

```
Hub detected at <cwd>.
Publish target: <target>
Output path: <f.pipeline/<target>-draft.md>
Active positioning: <value from a.foundations/positioning.md>
Visibility filter: <from target spec, e.g. "public-only">

Proceed? (y/n)
```

On explicit `y`, proceed.

### Step 2 — Resolve the target spec

Read `targets/<target>.md` from this skill package. Built-in targets:
- `cv` → `targets/cv.md`
- `linkedin` → `targets/linkedin.md`
- `github-profile` → `targets/github-profile.md`

Custom target: read `targets/<target>.md` if it exists. Refuse with guidance if it doesn't.

See `targets/_adding-targets.md` for the target-spec schema.

### Step 3 — Apply the target spec

A target spec declares:
- **Source categories / files** — which hub files to read.
- **Output section structure** — the sections in the rendered output.
- **Length / character limits** per section.
- **Visibility filter** — default `public`, can widen to include `private` (for the user's own drafts) but never `confidential`.
- **Positioning variant** — read from `a.foundations/positioning.md` active marker unless the target overrides.
- **Output path** — where the draft lands inside the hub (default `f.pipeline/<target>-draft.md`).

Render the output following the spec exactly.

### Step 4 — Draft to hub

Write the rendered draft to the output path declared by the spec. Do not mutate any other hub files.

If the output file already exists, refuse with guidance:
```
Draft already exists at <path>. Pass --force to overwrite, or review the existing draft first.
```

### Step 5 — Print posting checklist

After writing, print a cross-surface consistency checklist tailored to the target:
```
Draft saved to <path>.

Posting checklist:
- [ ] Verify <claim X> against a.foundations/biographical-facts.md.
- [ ] Verify dates on <role Y> against b.history/<role Y>.md.
- [ ] Cross-check Headline / Summary consistency with <sibling surface>.
- [ ] Confirm no confidential content leaked.
- [ ] Paste <section-by-section for LinkedIn, whole-file for CV, etc.>.
```

Specific checklist items come from the target spec.

### Step 6 — Commit the draft

```bash
cd <cwd>
git add <output-path>
git commit -m "render(<target>): draft from hub content"
```

## Extending

New targets drop into `targets/<target>.md` following the schema in `targets/_adding-targets.md`. No skill-code changes required.

Example future targets (not in v1):
- `cover-letter` — per-application cover-letter template.
- `conference-bio` — short third-person bio for talk abstracts.
- `jsonresume` — JSON Resume schema-compatible render.
- `obsidian` — Obsidian-vault-shaped render with wikilinks.

## Refuses

- `cwd` not a hub.
- Target spec not found under `targets/<target>.md`.
- Output file already exists and no `--force` passed.

## Does Not

- Post to LinkedIn / GitHub / any external surface directly.
- Mutate hub content outside the declared output path.
- Render confidential content — regardless of target spec.
````

- [ ] **Step 2: Verify**

Run:
```bash
head -5 /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/SKILL.md
```
Expected: YAML frontmatter with `name: career-hub-publish` and a `description:` field.

Read back and confirm: matches spec §7.3 behaviour (confirm, resolve spec, apply, draft to hub, checklist, commit); extensibility matches spec §4 layout and §11 future work; target spec schema referenced.

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/publish/SKILL.md && git commit -m "feat(career-hub): add publish sub-skill"
```

---

## Task 9: `publish/targets/cv.md`

**Files:**
- Create: `skills/career-hub/publish/targets/cv.md`

Purpose: CV render spec — maps hub content to a 1-2 page ATS-friendly markdown CV, which can feed into `cv-opti` for per-job tuning.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/cv.md` with:

```markdown
# Target Spec — CV

Renders an ATS-friendly, 1-2 page markdown CV from the hub's canonical content. Feeds into `cv-opti` for per-job tuning.

## Output

- **Path:** `f.pipeline/cv-draft.md`
- **Format:** Markdown (single column, plain text — ATS-parseable).

## Source

- `a.foundations/identity.md` — contact block.
- `a.foundations/positioning.md` — active variant → Professional Summary tone and emphasis.
- `a.foundations/biographical-facts.md` — all numerical claims cross-check against this.
- `b.history/*.md` — role block per role (reverse-chronological).
- `c.projects/*.md` — "Selected engagements" bullets nested under the role they occurred in (for consultant / multi-engagement roles).
- `d.capabilities/*.md` — Technical Skills section.

## Visibility filter

- Include: `public`
- Exclude: `private`, `confidential`
- Exclude: files with `status: draft` or `status: archived`

## Section structure

```
# <Full Name>

<location> | <phone> | <email> | <LinkedIn> | <Kaggle/other> | <GitHub>

## Professional Summary

<2-3 sentences from active positioning variant — experience anchor, current focus, differentiators>

## Core Competencies

<single-line pipe-separated list from d.capabilities, weighted to active positioning>

## Professional Experience

### <Role title> — <Employer>
*<start> – <end> | <Location>*

<2-3 sentence role summary>

- <quantified outcome>
- <quantified outcome>

**Selected engagements** (for consultant roles):
- **<Project name>** — <one-sentence quantified summary with scale numbers>

### <Next role, reverse-chronological>
...

## Education

- **<Degree>**, <Institution>, <Location> — <Year>. <optional coursework line>

## Technical Skills

- **Languages:** <list from d.capabilities/languages.md>
- **ML / Statistics:** <list from d.capabilities/ml-statistics.md>
- **Modern data stack:** <list from d.capabilities/data-stack.md>
- **AI / LLM:** <list from d.capabilities/ai-llm.md if present>
- **Domain:** <list from d.capabilities/domain-expertise.md>
- **Legacy / enterprise:** <list from d.capabilities/infra-platforms.md filtered to legacy>

## Online

- LinkedIn: <URL>
- <other profiles from identity.md>

## References

Available upon request.
```

## Length constraints

- Target: 1-2 pages (~700-1200 words total).
- If over 2 pages: truncate oldest roles' bullet lists, keep titles/dates/employer; drop older Selected Engagements detail.
- If under 1 page: surface an additional quantified outcome per role, or expand Professional Summary.

## Consistency checks (included in the posting checklist)

- [ ] Every scale number (portfolio, exposure, team size, tenure) appears in `a.foundations/biographical-facts.md`.
- [ ] Role dates match `b.history/*.md` frontmatter exactly.
- [ ] Role titles match `b.history/*.md` frontmatter exactly.
- [ ] No `confidential` content leaked.
- [ ] LinkedIn URL, email, phone match `a.foundations/identity.md`.
- [ ] Professional Summary tone matches the active positioning variant.

## Notes

- This is the CV pre-optimisation. Feed the output to the sibling `cv-opti` skill for per-JD tuning, ATS keyword extraction, and fraud-proofing.
- Do not include the Objective or Career Summary Objective pattern — too generic; replaced by Professional Summary.
- If the user explicitly requests a longer academic CV (publications, talks, etc.), note the mismatch and suggest they add sections via a `cv-academic` target spec instead.
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c "^## " /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/cv.md
```
Expected: at least 6 `##` sections (Output, Source, Visibility filter, Section structure, Length constraints, Consistency checks, Notes).

Read back and confirm: Output path, Source, Visibility filter, Section structure, Length constraints, Consistency checks all present; matches spec §7.3 target-spec-schema.

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/publish/targets/cv.md && git commit -m "feat(career-hub): add cv publish target"
```

---

## Task 10: `publish/targets/linkedin.md`

**Files:**
- Create: `skills/career-hub/publish/targets/linkedin.md`

Purpose: LinkedIn render spec — produces Headline, About, Experience descriptions (one per role), Skills, and Featured item list.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/linkedin.md` with:

```markdown
# Target Spec — LinkedIn Profile Refresh

Renders a LinkedIn profile draft: Headline, About, Experience descriptions (one per role), Skills, Featured items, and a posting checklist. Output is a single markdown file the user pastes section-by-section into LinkedIn.

## Output

- **Path:** `f.pipeline/linkedin-refresh.md`
- **Format:** Markdown with fenced code blocks per LinkedIn section (paste-ready).

## Source

- `a.foundations/identity.md` — LinkedIn URL, location.
- `a.foundations/positioning.md` — active variant drives Headline and About tone.
- `a.foundations/biographical-facts.md` — all numerical claims cross-check.
- `b.history/*.md` — one Experience description per role.
- `c.projects/*.md` — case-study bullets nested in consultant roles.
- `d.capabilities/*.md` — Skills list (top 3 pinned + up to 50 total).
- `e.artefacts/index.md` — candidates for Featured items.

## Visibility filter

- Include: `public`
- Exclude: `private`, `confidential`
- Include `status: active` only.

## Section structure

```
# LinkedIn Refresh — Draft

**Positioning:** <active variant name>

## Headline

> <120-220 char headline built from active positioning variant>

## About

<≤2,600 chars; 3-5 paragraphs; lead with current focus, then experience anchor, then specific highlights with scale numbers, then close with open-to.>

## Experience — Role Descriptions

### <YYYY-MM – YYYY-MM · Role · Employer>
```

<500-2000 chars per role; 1 short intro paragraph + 3-8 bullet points of quantified outcomes>

### <next role>
...

## Featured (pin in this order)

1. <item from e.artefacts/index.md with public visibility>
2. <item>
3. <item>
4. <item>

## Skills

**Top 3 pinned:**
1. <skill>
2. <skill>
3. <skill>

**Full list (50-cap):**

<skill> · <skill> · ...

## Posting Checklist

- [ ] Review About for tone and factual accuracy.
- [ ] Paste role descriptions role-by-role (LinkedIn requires updating each role individually).
- [ ] Pin the 3 top skills.
- [ ] Add Featured items in order.
- [ ] Cross-check: biographical-facts.md → LinkedIn (every claim consistent).
- [ ] Cross-check: cv-draft.md → LinkedIn (dates, tenures, numbers match).
- [ ] Post once all sections updated so the refresh shows as one coherent change.
```

## Length constraints

- Headline: 120-220 chars.
- About: ≤2,600 chars (LinkedIn hard limit).
- Experience per role: 500-2,000 chars. Senior / current roles favour the upper end; early-career roles the lower.
- Skills full list: ≤50 items (LinkedIn cap).

## Consistency checks

- [ ] Headline ties to the active positioning variant.
- [ ] About opens with current focus (not historical), matches positioning.
- [ ] Every scale number appears in `biographical-facts.md`.
- [ ] Role dates match `b.history/*.md` frontmatter.
- [ ] Role titles match `b.history/*.md` frontmatter.
- [ ] No `confidential` content leaked.
- [ ] Skills top-3 align with active positioning variant.

## Notes

- LinkedIn does not allow HTML in role descriptions — emit plain text with bullet markers (•) inside the code blocks.
- LinkedIn Featured accepts links and uploads; the draft lists candidates, the user adds them manually.
- Emit one code block per paste-section so the user can copy cleanly.
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c "^## " /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/linkedin.md
```
Expected: at least 6 `##` sections.

Read back and confirm: Headline / About / Experience / Featured / Skills / Checklist sections covered; length constraints stated; consistency checks present.

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/publish/targets/linkedin.md && git commit -m "feat(career-hub): add linkedin publish target"
```

---

## Task 11: `publish/targets/github-profile.md`

**Files:**
- Create: `skills/career-hub/publish/targets/github-profile.md`

Purpose: GitHub profile README render spec — lo-fi ASCII-box style, project-indexed (not temporal), designed for the `<user>/<user>` profile repository.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/github-profile.md` with:

```markdown
# Target Spec — GitHub Profile README

Renders a GitHub profile README for the user's profile repository (`<username>/<username>`). Lo-fi ASCII-box style, project-indexed (not temporal), under 250 lines. No emojis by default.

## Output

- **Path:** `f.pipeline/github-profile-README.md`
- **Format:** Markdown with fenced ASCII-box code blocks.

## Source

- `a.foundations/identity.md` — name, location, public contact links, GitHub handle.
- `a.foundations/positioning.md` — active variant drives the header subtitle.
- `b.history/2023-present-founder.md` (or equivalent current-chapter role) — current ventures list.
- `c.projects/*.md` where `visibility: public` and `status: active` — Selected Prior Work boxes.
- `d.capabilities/*.md` — Technical Skills table.

## Visibility filter

- Include: `public` only (this is a public surface).
- Include `status: active` only.

## Section structure

```
# <Name> | <Active positioning subtitle>

[LinkedIn badge] [Kaggle badge] [Email badge]

> <location>. <1-2 sentence experience anchor>. Full career timeline on [LinkedIn](...).

## Current Ventures

<ASCII box per current venture — ~4 boxes expected: founder role's listed ventures>

## Selected Prior Work

<ASCII box per curated project — ~6 boxes; NOT temporal, NOT exhaustive; chosen for technical or commercial interest; mix big-scale banking with open-source>

## Technical Skills

| Category | Tools |
| --- | --- |
| **Languages** | <from languages.md> |
| **AI / LLM Engineering** | <from ai-llm.md if present> |
| **Modern data stack** | <from data-stack.md> |
| **ML / Statistics** | <from ml-statistics.md> |
| **Infra & DevOps** | <from infra-platforms.md> |
| **<Domain>** | <from domain-expertise.md> |
| **Legacy / enterprise** | <from infra-platforms.md filtered to legacy> |

## Open-Source Projects

<ASCII box per actively-maintained public project; ~5 boxes expected>

## Let's Connect

- LinkedIn: [<handle>](...)
- Email: [<email>](mailto:...)
- <other public channels>

Open to: <from active positioning variant's "open to" line>.
```

### ASCII box format

```
┌────────────────────────────────────────────────────────────┐
│ <Project / Venture Name>                   <dates>         │
└────────────────────────────────────────────────────────────┘
  <role>

  • <bullet>
  • <bullet>
  • <bullet>

  <URL if public>
```

Fixed width: 60 columns. Pad or truncate accordingly.

## Length constraints

- Total: under 250 lines.
- Current Ventures: up to ~4 boxes.
- Selected Prior Work: up to ~6 boxes — curated, not exhaustive.
- Open-Source Projects: up to ~5 boxes.

## Consistency checks

- [ ] Every scale number in the boxes appears in `biographical-facts.md`.
- [ ] No `private` or `confidential` content.
- [ ] No internal project names for banking work — describe architecture and numbers, not internal names.
- [ ] GitHub handle in header matches `identity.md`.
- [ ] Email matches `identity.md`.
- [ ] "Open to" line matches active positioning variant.

## Notes

- Project-indexed, not temporal. Chronological career order belongs on LinkedIn.
- No emojis by default. Override via a `--emoji` flag on publish if the user explicitly wants them.
- GitHub uses CommonMark; tables and ASCII boxes both render cleanly in monospace.
- For a "hiring-signal" profile (vs "recruiter-sourced" profile), lead with a clear "Open to:" line at the end — specific engagement types, not "open to opportunities".
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c "^## " /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/github-profile.md
```
Expected: at least 6 `##` sections.

Read back and confirm: Output / Source / Visibility filter / Section structure / ASCII box format / Length / Consistency checks all covered.

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/publish/targets/github-profile.md && git commit -m "feat(career-hub): add github-profile publish target"
```

---

## Task 12: `publish/targets/_adding-targets.md`

**Files:**
- Create: `skills/career-hub/publish/targets/_adding-targets.md`

Purpose: documents the target-spec schema. Users drop new specs in here to extend `publish` without modifying skill code.

- [ ] **Step 1: Write the file**

Write `/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/_adding-targets.md` with:

```markdown
# Adding a Publish Target

New render targets drop into this directory as `<target-name>.md` files. No skill-code changes required. `publish <target-name>` resolves to this directory.

Underscore-prefixed files (`_adding-targets.md`) are meta-docs and are not themselves targets.

## Required sections in a target spec

Every target spec must declare these sections:

### `## Output`

- **Path:** where the rendered draft lands inside the hub (default convention: `f.pipeline/<target-name>-draft.md`).
- **Format:** file format (markdown, html, json, etc.).

### `## Source`

Which hub files drive the render. List specific files or globs.

Cross-reference `a.foundations/biographical-facts.md` for claim verification — this is conventional, not mandatory, but strongly recommended.

### `## Visibility filter`

Declare explicitly:
- Which visibility levels to include (`public`, optionally `private` for user's own drafts; never `confidential`).
- Which `status` values to include (default `active` only).

### `## Section structure`

Fenced code block showing the literal output shape with `<placeholder>` markers for content. This is the rendering recipe.

### `## Length constraints`

Per-section word / character / line limits. Explicit upper bounds, plus what to do on overshoot / undershoot.

### `## Consistency checks`

A checklist that the `publish` sub-skill appends to its output. Every render should cross-check claims against `biographical-facts.md` and cross-surface sibling drafts.

### `## Notes`

Free-form caveats, format-specific quirks, or composition suggestions (e.g. "feed to `cv-opti` for per-JD tuning").

## Optional sections

### `## Positioning variant override`

By default, the active variant in `a.foundations/positioning.md` drives tone. A target can override:
```
Default positioning: <variant label>
```

### `## Argument extensions`

If the target accepts modifiers (e.g. `--emoji`, `--verbose`), document them here.

## Example: cover-letter target (not in v1)

A `cover-letter.md` target spec might look like:

```
# Target Spec — Cover Letter

## Output

- **Path:** `f.pipeline/cover-letters/<YYYY-MM-DD-<employer>-<role>.md`
- **Format:** markdown.

## Source

- `a.foundations/identity.md`
- `a.foundations/positioning.md` — active variant.
- `b.history/2023-present-founder.md` — current chapter.
- `f.pipeline/target-roles.md` — the row matching this application.
- User provides: JD paste, employer name, role title.

## Visibility filter

- Include: `public`, `private` (user's own draft).
- Exclude: `confidential`.

## Section structure

<2-3 paragraphs, no subheadings>

## Length constraints

- 250-400 words.

## Consistency checks

- [ ] Hook (para 1) references something specific to the employer — not generic enthusiasm.
- [ ] Evidence (para 2) ties to a specific quantified outcome from `b.history` or `c.projects`.
- [ ] Close (para 3) states next-step intent.
- [ ] No `confidential` content.

## Notes

- One cover letter per application. Filed by date and employer.
- Feed to `cv-opti` alongside the CV if tuning both against the JD.
```

## Conventions

- File names: lowercase, hyphen-separated (`cover-letter.md`, not `coverLetter.md`).
- Draft output paths live under `f.pipeline/` or a subdirectory of it. Do not write outside `f.pipeline/`.
- Target specs are themselves public — they describe a rendering recipe, not the user's content.
```

- [ ] **Step 2: Verify**

Run:
```bash
grep -c "^## " /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/_adding-targets.md
```
Expected: at least 5 `##` sections.

Read back and confirm: schema matches what `cv.md`, `linkedin.md`, `github-profile.md` use (Output, Source, Visibility filter, Section structure, Length constraints, Consistency checks, Notes).

- [ ] **Step 3: Commit**

```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add skills/career-hub/publish/targets/_adding-targets.md && git commit -m "feat(career-hub): document target-spec schema for extensibility"
```

---

## Task 13: Self-review — validate against spec success criteria

**Files:** no file changes. Final verification pass.

- [ ] **Step 1: Confirm file count and layout**

Run:
```bash
find /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub -type f | sort
```
Expected:
```
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/SKILL.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/build/SKILL.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/init/SKILL.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/SKILL.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/_adding-targets.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/cv.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/github-profile.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/publish/targets/linkedin.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references/hub-detection.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references/taxonomy.md
/home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/references/templates.md
```
(11 files.)

- [ ] **Step 2: Verify internal cross-links**

Run:
```bash
grep -rn --include='*.md' '\[.*\](' /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/
```

For every relative link in the output, confirm the target file exists. If any link is broken, fix and re-commit.

Key links to verify:
- Umbrella `SKILL.md` links to `init/SKILL.md`, `build/SKILL.md`, `publish/SKILL.md`, `references/taxonomy.md`, `references/templates.md`, `references/hub-detection.md`.
- `init/SKILL.md`, `build/SKILL.md`, `publish/SKILL.md` link to `../references/hub-detection.md`.
- `publish/SKILL.md` references `targets/_adding-targets.md` and the three built-in target specs.

- [ ] **Step 3: Validate against spec §12 success criteria**

For each success criterion in the spec, confirm the implementation supports it:

| Criterion | Supported by |
|-----------|--------------|
| User can run `init` in empty directory and get a compliant hub | Task 6 `init/SKILL.md` |
| `build roles` reaches complete cards in 1-2 sessions via gap-questions-only | Task 7 `build/SKILL.md` + Task 2 taxonomy precedence + Task 3 templates |
| `publish cv` emits markdown that feeds `cv-opti` without rework | Task 9 `cv.md` |
| `publish linkedin` emits paste-ready draft | Task 10 `linkedin.md` |
| User can add a new publish target by dropping a spec | Task 12 `_adding-targets.md` |
| Four-axis self-check passes (no hallucinations, no unverifiable adjectives, no confidential leaks, no inconsistencies) | Task 2 taxonomy + Task 7 build's draft-from-known-content posture + Task 8 publish's visibility filter |

- [ ] **Step 4: Validate principle coverage**

Check that every principle in spec §6 appears in the relevant file(s):

| Principle | Where | Location |
|-----------|-------|----------|
| 1. Category precedence | `references/taxonomy.md` | Axis 1 → Precedence rule |
| 2. Visibility explicit | `references/taxonomy.md` | Axis 2 |
| 3. Confidential sibling pattern | `references/taxonomy.md` + `references/templates.md` | Convention + template |
| 4. Status markers | `references/taxonomy.md` | Axis 4 |
| 5. Templates for all docs | `references/templates.md` | Every category template |
| 6. Stubs not blanks | `init/SKILL.md` | Seed step + TODO markers |
| 7. Canonical vs external | `references/templates.md` (e.artefacts) + `init/SKILL.md` (README) | Migration rule |
| 8. Hub-first | umbrella `SKILL.md` | Design Philosophy |
| 9. Draft-from-known-content-ask-only-gap-questions | `build/SKILL.md` | Interview Posture section |
| 10. Every claim verifiable | `references/templates.md` (biographical-facts) + all targets' consistency checks | Verification table + checklists |

- [ ] **Step 5: Placeholder scan**

Run:
```bash
grep -rn --include='*.md' -E '(TBD|TODO|FIXME|implement later|fill in details)' /home/nathanielramm/git/discreteds/cv-optimiser/skills/career-hub/ | grep -v -E 'TODO marker|<!-- TODO -->'
```
Expected output: empty (or only matches inside explicit "`<!-- TODO -->`" examples in the templates).

Explanation: the templates in `templates.md` legitimately contain `<!-- TODO -->` markers as part of the template content (those are what `init` seeds into new hub stubs). Any TBD / TODO / FIXME that is *not* a deliberate template marker is a plan failure.

- [ ] **Step 6: Commit the review**

If any fixes were needed during this task, commit them with:
```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git add -A && git commit -m "fix(career-hub): self-review corrections"
```

If no fixes, tag the completed skill:
```bash
cd /home/nathanielramm/git/discreteds/cv-optimiser && git tag -a career-hub-v1 -m "career-hub skill v1 complete"
```

- [ ] **Step 7: Print completion summary**

```
career-hub skill v1 complete.

Package: cv-optimiser/skills/career-hub/
Files: 11 markdown files + .gitignore
Git: initialised, <N> commits, tag career-hub-v1

Next:
- Test end-to-end: navigate to an empty directory and invoke `career-hub-init`.
- Then `career-hub-build foundations` to seed identity / positioning / facts.
- Then `career-hub-build roles`, `career-hub-build projects`, etc.
- Then `career-hub-publish cv` + `career-hub-publish linkedin` + `career-hub-publish github-profile`.

Sibling: cv-optimiser/skills/cv-opti/ — feeds from `career-hub-publish cv` output.
```

---

## Self-Review Addendum (writer's check, for the spec author)

Ran these spot checks before handoff:

**Spec §4 package layout** — Tasks 1, 5, 6, 7, 8, 12 produce exactly the layout in spec §4. Confirmed.

**Spec §5 hub structure** — Task 6 `init/SKILL.md` specifies the mandated structure. Confirmed.

**Spec §6 principles** — Task 13 Step 4 maps principles 1-10 to files. Confirmed each principle has a home.

**Spec §7.1 / 7.2 / 7.3** — Tasks 6, 7, 8 respectively cover init, build, publish behaviours. Confirmed.

**Spec §8 data shapes** — Task 3 `templates.md` covers universal frontmatter + per-category templates. Confirmed.

**Spec §9 interaction design** — Tasks 6, 7, 8 all include confirmation-first behaviour per `hub-detection.md`. Confirmed.

**Spec §10 cv-opti composition** — Umbrella `SKILL.md` (Task 5) names the composition; `cv.md` target (Task 9) notes it in Notes section. Confirmed.

**Spec §11 future work** — Umbrella `SKILL.md` (Task 5) lists future work; `_adding-targets.md` (Task 12) shows extensibility path. Confirmed.

**Spec §12 success criteria** — Task 13 Step 3 explicitly maps each criterion to the file supporting it. Confirmed.

**Type consistency check:**
- Sub-skill names: `career-hub-init`, `career-hub-build`, `career-hub-publish` — used consistently in umbrella + each sub-skill's frontmatter.
- Path convention `f.pipeline/<target>-draft.md` — appears in publish/SKILL.md and each target spec.
- Frontmatter field names (`visibility`, `audience`, `status`, `last_updated`) — consistent across taxonomy.md, templates.md, SKILL.md files.
- Category slugs (`a.foundations`, `b.history`, …) — consistent across all files.

No gaps detected. Plan ready for execution.
