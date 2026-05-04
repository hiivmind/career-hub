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
