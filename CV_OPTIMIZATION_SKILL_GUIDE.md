# cv-opti — Skill Guide

Deep dive on the `cv-opti` skill within the [`career-hub`](README.md) plugin.

> **Sibling skill:** `career-hub` produces a canonical career repo and renders an ATS-friendly markdown CV via `publish cv`. `cv-opti` then tunes that CV (or any existing CV) against a specific job description. Use them together for the full flow; either alone is fine.

## Overview

`cv-opti` is a Claude skill that helps job seekers navigate the dual-AI hiring landscape. It addresses two opposing AI systems:

1. **ATS screening** — employer systems that reject the majority of resumes before human review.
2. **Fraud detection** — employer verification systems that flag fabricated claims.

Every invocation produces two outputs:

1. **Reformatted CV** — ready for submission.
2. **Strategy document (markdown)** — explains every change and how to customize for future jobs.

## Skill Structure

```
skills/cv-opti/
├── SKILL.md                          # entry + workflow
└── references/
    ├── ats-optimization.md           # formatting & keyword extraction
    ├── fraud-proofing.md             # verification strategies & red flags
    ├── achievement-bullets.md        # quantification framework
    └── customization-protocol.md     # per-job tailoring workflow
```

### Design principles

- **Progressive disclosure.** Frontmatter triggers the skill; `SKILL.md` body explains the workflow; references load on demand.
- **High freedom, reference-based.** Frameworks and principles, not rigid templates.
- **Generic and reusable.** Not tied to any individual or industry.
- **Authentic optimization.** Never encourages fabrication. Claims must survive interview.

## How Claude Uses This Skill

### Triggers

The skill auto-invokes when users ask about:
- CV / resume optimization or creation
- ATS compatibility, keyword matching
- Resume rejection analysis
- Employment gap framing
- Achievement-bullet improvement
- Fraud-detection avoidance

### Workflow

1. User provides current CV (any format) and optionally a target JD.
2. Claude analyzes for ATS issues (formatting, keywords) and fraud red flags (inconsistencies, vague claims, unverifiable metrics).
3. Claude rewrites bullets via `achievement-bullets.md`, formats via `ats-optimization.md`, removes red flags via `fraud-proofing.md`.
4. If a JD is provided, applies `customization-protocol.md`.
5. Delivers reformatted CV + strategy document.

### Output contract

**Reformatted CV**
- ATS-parseable formatting
- Keywords naturally integrated (when JD provided)
- Bullets follow Action + Task + Result + Impact
- Every claim verifiable
- Typically 1–2 pages

**Strategy document**
- Line-by-line change log with reasoning
- ATS impact per change
- Fraud-detection impact per change
- Employment-gap handling (if applicable)
- Interview-prep notes for defended claims
- Per-job customization guidance

## Reference Guides

### `references/ats-optimization.md`

Formatting requirements (.docx vs PDF), single-column layout, fonts, prohibited elements (graphics, special characters), section-header standardization, keyword extraction and natural integration, contact-info formatting, length.

### `references/fraud-proofing.md`

Fraud-detection reality and statistics, claim-to-evidence mapping, cross-platform consistency (CV ↔ LinkedIn ↔ company records), audit checklist, "interview question" defensibility test, the ten red-flag patterns that trigger investigation, employment-gap strategy, verification-resistant language.

### `references/achievement-bullets.md`

Action + Task + Result + Impact formula, action-verb rankings, five quantification patterns with examples, strong vs weak bullet patterns from real roles (data, software, product, finance), the skill-honesty framework (Expert / Proficient / Intermediate / Basic / Outdated), interview-question test, bullet-count and date-formatting guidance.

### `references/customization-protocol.md`

Why per-job tailoring matters, static vs dynamic sections, eight-step ~15–20-minute customization workflow, professional-summary rewriting, core-competencies reordering, achievement-bullet prioritization, keyword-coverage verification, consistency check, optional ATS testing, customization tracking.

## Use Cases

| Scenario | Workflow |
|----------|----------|
| **New CV** | Gather work history → quantified bullets → ATS-formatted CV → fraud-proof against LinkedIn → deliver CV + strategy doc. |
| **Existing CV optimization** | Analyze for red flags → rewrite weak bullets → eliminate inconsistencies → deliver optimized CV + improvement explanation. |
| **Employment gap** | Apply `fraud-proofing.md` gap strategy → frame honestly and coherently → prepare interview narrative → deliver strategy doc. |
| **Job-specific tailoring** | Run `customization-protocol.md` → extract 15–25 keywords → reorder competencies and achievements → verify coverage → deliver tuned CV. |
| **Rejection analysis** | Cross-check CV against all references → identify ATS + fraud + customization gaps → deliver improvement plan + optimized CV. |

## Composition with `career-hub`

When a user has both skills available, the canonical flow is:

```
career-hub:init     → empty hub scaffolded at cwd
career-hub:build    → roles, projects, capabilities enriched via interview
career-hub:publish cv  → ATS-friendly markdown CV rendered from hub
cv-opti             → CV tuned against a specific job description
```

Each step is independent — users can enter the flow at any point with whatever artefact they already have.

## Strengths

1. **Comprehensive** — covers ATS and fraud detection simultaneously.
2. **Practical** — every principle has concrete, actionable guidance.
3. **Verifiable** — emphasizes claims defendable in interview.
4. **Efficient** — per-job tailoring in ~15–20 minutes.
5. **Honest** — never encourages fabrication.
6. **Reusable** — works across technical and professional roles.
7. **Composable** — pairs cleanly with `career-hub:publish cv`.

## Limitations

1. Requires the user to provide their actual CV and work history (or a populated hub).
2. Doesn't auto-scan or score CVs against ATS engines — Claude reads and reasons.
3. English-language CVs and JDs assumed.
4. Best fit for tech / data / professional roles; other industries may need adaptation.

## See Also

- [`README.md`](README.md) — plugin overview and installation.
- [`QUICK_REFERENCE.md`](QUICK_REFERENCE.md) — both skills at a glance.
- [`CLAUDE.md`](CLAUDE.md) — guidance for Claude Code working on this repo.
- [`skills/career-hub/SKILL.md`](skills/career-hub/SKILL.md) — sibling skill entry point.
- [`skills/cv-opti/SKILL.md`](skills/cv-opti/SKILL.md) — `cv-opti` skill entry point.
