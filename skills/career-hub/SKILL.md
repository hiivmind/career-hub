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
