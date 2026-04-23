# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a **Claude Code plugin** (`career-hub`, see `.claude-plugin/plugin.json`) that packages two complementary skills for managing career artefacts. There is no build, test, or runtime — artefacts are markdown prompts loaded by Claude when a skill is invoked.

## Skills

Two top-level skills under `skills/`:

- **`career-hub/`** — builds and maintains a canonical career hub (markdown + YAML repo) as the single source of truth for roles, projects, capabilities, artefacts, and pipeline. Renders downstream targets (CV, LinkedIn, GitHub profile) from it. Composed of three phased sub-skills:
  - `init/` — scaffold an empty compliant hub at `cwd`.
  - `build/` — interview-driven enrichment of stubs; drafts from existing content and asks only gap questions.
  - `publish/` — render a draft target from hub content. Built-in targets live in `publish/targets/` (`cv.md`, `linkedin.md`, `github-profile.md`); see `publish/targets/_adding-targets.md` for the target-spec schema.
- **`cv-opti/`** — per-job CV optimization for the dual-AI hiring landscape (ATS + fraud detection). Produces a reformatted CV plus a strategy document explaining every change.

The two compose: `career-hub:publish cv` produces an ATS-friendly markdown CV that `cv-opti` then tunes against a specific job description.

## Architecture Conventions

- **Progressive disclosure.** Each `SKILL.md` is short and workflow-focused; detail lives in sibling `references/*.md` that Claude reads on demand. When editing, push specifics into references rather than bloating the entry point.
- **Frontmatter is the trigger.** The `description` field in each `SKILL.md` determines auto-invocation. Edits to it directly affect when Claude picks up the skill.
- **Hub-first, rendering-second** (career-hub). Every public claim must trace to a hub entry. `publish` filters confidential content and cross-checks against `a.foundations/biographical-facts.md`.
- **Verifiability** (cv-opti). No change should introduce unverifiable claims, even to improve ATS keyword density. Every achievement bullet must be defendable in interviews.
- **Two-output contract** (cv-opti). Always produce both deliverables: reformatted CV + strategy document.

## Shared References

`skills/career-hub/references/` — used by all three career-hub sub-skills:
- `hub-detection.md` — how each sub-skill confirms hub location at `cwd` before writing.
- `taxonomy.md` — four axes (category/visibility/audience/status), `.private.md` sibling convention, universal frontmatter.
- `templates.md` — entry templates.

## Design Docs

- `docs/superpowers/specs/2026-04-20-career-hub-skill-design.md` — design spec.
- `docs/superpowers/plans/2026-04-20-career-hub-skill-implementation.md` — implementation plan.

## Working on these skills

For structural/meta changes (frontmatter tuning, adding sub-skills, progressive disclosure restructuring), use the `skill-creator` or `plugin-dev:skill-development` skills rather than editing blind.
