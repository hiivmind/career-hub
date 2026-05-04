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
