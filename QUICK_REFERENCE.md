# career-hub — Quick Reference

This plugin ships **two skills**. Use them separately or compose them.

| Skill | When to invoke |
|-------|----------------|
| **`career-hub`** | You want a canonical, single-source-of-truth career repo, or to render a CV / LinkedIn / GitHub-profile draft from one. |
| **`cv-opti`** | You have a CV and a target job description and want it tuned to pass ATS + fraud detection. |

**Composed flow:** `career-hub:publish cv` → markdown CV → `cv-opti` → per-job tuned CV + strategy doc.

---

## `career-hub` — three sub-skills

| Phase | Sub-skill | What you get |
|-------|-----------|--------------|
| 1 | `init` | Empty compliant hub scaffolded at `cwd`. |
| 2 | `build` | Stubs enriched via interview. Drafts from existing content; asks only **gap** questions, never redundant ones. |
| 3 | `publish` | Draft target rendered from hub content. |

### Built-in publish targets

`cv` · `linkedin` · `github-profile`

Custom targets: drop a `<name>.md` into `skills/career-hub/publish/targets/` following [`_adding-targets.md`](skills/career-hub/publish/targets/_adding-targets.md).

### Hub principles

- **Hub-first, rendering-second** — every public claim traces to a hub entry.
- **Verifiable only** — no unverifiable adjectives. Scale numbers + verification methods live in `a.foundations/biographical-facts.md`.
- **Visibility filtering** — `publish` strips `.private.md` siblings; public claims cross-check against biographical facts.

### Shared references

- `references/hub-detection.md` — how each sub-skill confirms hub location.
- `references/taxonomy.md` — category / visibility / audience / status axes; `.private.md` convention; universal frontmatter.
- `references/templates.md` — entry templates.

---

## `cv-opti` — two outputs, every time

1. **Reformatted CV** — ATS-friendly formatting, keywords from the JD (if provided), quantified bullets, claims cross-checked.
2. **Strategy document (markdown)** — every change made, ATS impact, fraud-detection impact, gap handling, future-customization guidance.

### Reference guides

| File | Use for |
|------|---------|
| `references/ats-optimization.md` | Formatting, keyword extraction, section naming. |
| `references/fraud-proofing.md` | Verification, red flags, consistency, employment-gap strategy. |
| `references/achievement-bullets.md` | Action + Task + Result + Impact framework, quantification patterns, interview-question test. |
| `references/customization-protocol.md` | Per-job tailoring workflow (~15–20 min). |

### Use-case map

| Scenario | Skill(s) |
|----------|----------|
| First-time career repo | `career-hub:init` then `career-hub:build` |
| Stub roles/projects need filling in | `career-hub:build` |
| Generate a fresh CV from your hub | `career-hub:publish cv` |
| Tune CV for a specific JD | `cv-opti` |
| Generate then tune for a job | `career-hub:publish cv` → `cv-opti` |
| New LinkedIn / GitHub-profile draft | `career-hub:publish linkedin` / `github-profile` |

---

## Design principles (apply to both skills)

- **Progressive disclosure.** `SKILL.md` files stay short; detail lives in sibling `references/*.md` loaded on demand.
- **Frontmatter is the trigger.** `description` in each `SKILL.md` decides auto-invocation.
- **Authentic optimization.** Never fabricate. Every claim defendable in interview.

## See also

- [`README.md`](README.md) — overview and installation.
- [`CLAUDE.md`](CLAUDE.md) — guidance for Claude Code working on this repo.
- [`CV_OPTIMIZATION_SKILL_GUIDE.md`](CV_OPTIMIZATION_SKILL_GUIDE.md) — `cv-opti` deep dive.
- [`docs/superpowers/specs/`](docs/superpowers/specs/) — `career-hub` design spec.
