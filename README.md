# career-hub

A Claude Code plugin for managing the full lifecycle of career artefacts — from a canonical career repository to per-job CV tuning.

Two complementary skills:

| Skill | Purpose |
|-------|---------|
| **`career-hub`** | Build and maintain a canonical career hub (markdown + YAML) as the single source of truth for roles, projects, capabilities, and pipeline. Render CVs, LinkedIn drafts, and GitHub profile READMEs from it. |
| **`cv-opti`** | Optimize an existing CV for a specific job posting against the dual-AI hiring landscape (ATS screening + employer fraud detection). |

The two compose naturally: `career-hub:publish cv` emits an ATS-friendly markdown CV that `cv-opti` then tailors per job description.

## Installation

This is a Claude Code plugin. Install via your plugin marketplace, or point Claude Code at this directory.

Plugin manifest: [`.claude-plugin/plugin.json`](.claude-plugin/plugin.json).

## `career-hub` — canonical career repository

Three phased sub-skills:

| Phase | Sub-skill | What it does |
|-------|-----------|--------------|
| 1 | `init` | Scaffold an empty compliant hub at `cwd`. |
| 2 | `build` | Interview-driven enrichment of stubs (roles, projects, capabilities, foundations). Drafts from existing content and cross-references; asks only *gap* questions — never redundant ones. |
| 3 | `publish` | Render a draft target from hub content. Built-in targets: `cv`, `linkedin`, `github-profile`. Custom targets supported via the target-spec schema. |

### Design philosophy

- **Hub-first, rendering-second.** The hub is the source of truth; CVs, LinkedIn, and GitHub profile pages are views onto it.
- **Every claim verifiable.** No unverifiable adjectives. Scale numbers and verification methods live in `a.foundations/biographical-facts.md`. `publish` filters confidential content; public-facing claims cross-check against the biographical-facts table.
- **Draft-from-known-content.** Fast, low-friction enrichment.

### Custom publish targets

See [`skills/career-hub/publish/targets/_adding-targets.md`](skills/career-hub/publish/targets/_adding-targets.md) for the target-spec schema. Drop a new `<name>.md` into `publish/targets/` and `publish` picks it up.

## `cv-opti` — per-job CV optimization

Optimizes a CV to pass two opposing AI systems:

1. **ATS screening** — employer systems that reject the majority of resumes before human review.
2. **Fraud detection** — employer verification that flags fabricated claims.

### Two-output contract

Every invocation produces both:

1. **Reformatted CV** — ATS-friendly formatting, keyword extraction from the job description (if provided), quantified achievement bullets, claims cross-checked for verifiability.
2. **Strategy document (markdown)** — every change made, why it improves ATS parsing, why it reduces fraud red flags, gap handling, customization guidance for future jobs.

### Principles

- **Authentic optimization** — never fabricates.
- **Dual-AI balanced** — optimizes for both automated screening AND human verification.
- **Verifiable claims** — every achievement bullet defendable in technical interviews.

Detailed reference material lives in [`skills/cv-opti/references/`](skills/cv-opti/references/) (ATS rules, fraud-proofing, achievement bullets, per-job customization protocol).

## Repository layout

```
.claude-plugin/plugin.json     # plugin manifest
skills/
  career-hub/
    SKILL.md                   # entry point + when-to-use
    init/SKILL.md              # phase 1
    build/SKILL.md             # phase 2
    publish/
      SKILL.md                 # phase 3
      targets/                 # built-in + custom target specs
    references/                # shared: hub-detection, taxonomy, templates
  cv-opti/
    SKILL.md
    references/                # ATS, fraud-proofing, bullets, customization
docs/superpowers/              # design spec + implementation plan
```

## Related documentation

- [`CLAUDE.md`](CLAUDE.md) — guidance for Claude Code working on this repo.
- [`CV_OPTIMIZATION_SKILL_GUIDE.md`](CV_OPTIMIZATION_SKILL_GUIDE.md) — deep-dive on the cv-opti skill architecture.
- [`QUICK_REFERENCE.md`](QUICK_REFERENCE.md) — cv-opti quick reference.
- [`docs/superpowers/specs/`](docs/superpowers/specs/) — career-hub design spec.

## License

MIT — see [`.claude-plugin/plugin.json`](.claude-plugin/plugin.json).
