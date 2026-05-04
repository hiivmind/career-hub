# career-hub

A Claude Code plugin for managing the full lifecycle of career artefacts — from a canonical career repository to per-job CV tuning.

## Skills

Four independent skills, usable separately or composed:

| Skill | Purpose |
|-------|---------|
| **`career-hub-init`** | Scaffold an empty compliant hub at `cwd`. |
| **`career-hub-build`** | Interview-driven enrichment of stubs (roles, projects, capabilities, foundations). Drafts from existing content; asks only *gap* questions. |
| **`career-hub-publish`** | Render a draft target from hub content. Built-in targets: `cv`, `linkedin`, `github-profile`. Custom targets supported via the [target-spec schema](skills/career-hub-publish/targets/_adding-targets.md). |
| **`career-hub-optimise-cv`** | Optimize a CV for a specific job posting against the dual-AI hiring landscape (ATS screening + employer fraud detection). Produces both a reformatted CV and a strategy document. |

### Composition

`career-hub-publish cv` emits an ATS-friendly markdown CV that `career-hub-optimise-cv` then tailors per job description. Each step is independent — enter the flow at any point with whatever artefact you already have.

| Scenario | Skills |
|----------|--------|
| First-time career repo | `career-hub-init` → `career-hub-build` |
| Generate a fresh CV from your hub | `career-hub-publish cv` |
| Tune CV for a specific JD | `career-hub-optimise-cv` |
| Generate then tune for a job | `career-hub-publish cv` → `career-hub-optimise-cv` |
| LinkedIn / GitHub-profile draft | `career-hub-publish linkedin` / `github-profile` |

## Installation

This is a Claude Code plugin. Install via your plugin marketplace, or point Claude Code at this directory.

Plugin manifest: [`.claude-plugin/plugin.json`](.claude-plugin/plugin.json).

## Repository layout

```
.claude-plugin/plugin.json          # plugin manifest
skills/
  career-hub-init/SKILL.md          # scaffold a hub
  career-hub-build/SKILL.md         # enrich hub content
  career-hub-publish/
    SKILL.md                        # render targets from hub
    targets/                        # built-in + custom target specs
  career-hub-optimise-cv/
    SKILL.md                        # per-job CV tuning
    references/                     # ATS, fraud-proofing, bullets, customization
  references/                       # shared: hub-detection, taxonomy, templates
```

## Design principles

- **Hub-first, rendering-second.** The hub is the source of truth; CVs, LinkedIn, and GitHub profile pages are views onto it.
- **Every claim verifiable.** No unverifiable adjectives. Scale numbers and verification methods live in `a.foundations/biographical-facts.md`.
- **Authentic optimization.** Never fabricates. Every achievement bullet must be defendable in interview.
- **Progressive disclosure.** `SKILL.md` files stay short; detail lives in sibling `references/*.md` loaded on demand.

## Related documentation

- [`CLAUDE.md`](CLAUDE.md) — guidance for Claude Code working on this repo.
- [`CV_OPTIMIZATION_SKILL_GUIDE.md`](CV_OPTIMIZATION_SKILL_GUIDE.md) — deep-dive on the cv-opti skill architecture.
- [`QUICK_REFERENCE.md`](QUICK_REFERENCE.md) — both skills at a glance.

## License

MIT — see [`.claude-plugin/plugin.json`](.claude-plugin/plugin.json).
