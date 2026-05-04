# career-hub — Quick Reference

This plugin ships **four skills**. Use them separately or compose them.

| Skill | When to invoke |
|-------|----------------|
| **`career-hub-init`** | You want a canonical, single-source-of-truth career repo scaffolded at `cwd`. |
| **`career-hub-build`** | You have a hub with stubs that need enriching via interview. |
| **`career-hub-publish`** | You want to render a CV, LinkedIn, or GitHub-profile draft from your hub. |
| **`career-hub-optimise-cv`** | You have a CV and a target job description and want it tuned to pass ATS + fraud detection. |

**Composed flow:** `career-hub-publish cv` → markdown CV → `career-hub-optimise-cv` → per-job tuned CV + strategy doc.

---

## `career-hub-init` / `career-hub-build` / `career-hub-publish`

| Phase | Skill | What you get |
|-------|-------|--------------|
| 1 | `career-hub-init` | Empty compliant hub scaffolded at `cwd`. |
| 2 | `career-hub-build` | Stubs enriched via interview. Drafts from existing content; asks only **gap** questions, never redundant ones. |
| 3 | `career-hub-publish` | Draft target rendered from hub content. |

### Built-in publish targets

`cv` · `linkedin` · `github-profile`

Custom targets: drop a `<name>.md` into `skills/career-hub-publish/targets/` following [`_adding-targets.md`](skills/career-hub-publish/targets/_adding-targets.md).

### Hub principles

- **Hub-first, rendering-second** — every public claim traces to a hub entry.
- **Verifiable only** — no unverifiable adjectives. Scale numbers + verification methods live in `a.foundations/biographical-facts.md`.
- **Visibility filtering** — `publish` strips `.private.md` siblings; public claims cross-check against biographical facts.

### Shared references

- `references/hub-detection.md` — how each skill confirms hub location.
- `references/taxonomy.md` — category / visibility / audience / status axes; `.private.md` convention; universal frontmatter.
- `references/templates.md` — entry templates.

---

## `career-hub-optimise-cv` — two outputs, every time

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
| First-time career repo | `career-hub-init` then `career-hub-build` |
| Stub roles/projects need filling in | `career-hub-build` |
| Generate a fresh CV from your hub | `career-hub-publish cv` |
| Tune CV for a specific JD | `career-hub-optimise-cv` |
| Generate then tune for a job | `career-hub-publish cv` → `career-hub-optimise-cv` |
| New LinkedIn / GitHub-profile draft | `career-hub-publish linkedin` / `github-profile` |

---

## Design principles (apply to all skills)

- **Progressive disclosure.** `SKILL.md` files stay short; detail lives in sibling `references/*.md` loaded on demand.
- **Frontmatter is the trigger.** `description` in each `SKILL.md` decides auto-invocation.
- **Authentic optimization.** Never fabricate. Every claim defendable in interview.

## See also

- [`README.md`](README.md) — overview and installation.
- [`CLAUDE.md`](CLAUDE.md) — guidance for Claude Code working on this repo.
- [`CV_OPTIMIZATION_SKILL_GUIDE.md`](CV_OPTIMIZATION_SKILL_GUIDE.md) — `career-hub-optimise-cv` deep dive.
