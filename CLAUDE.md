# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is not a code project — it is a **Claude Skill** package (`cv-opti`) that guides Claude through optimizing CVs for the dual-AI hiring landscape (ATS screening + employer fraud detection). There is no build, test, or runtime; the artifacts are markdown prompts loaded by Claude when the skill is invoked.

## Structure

- `skills/cv-opti/SKILL.md` — skill entry point. Frontmatter (`name`, `description`) determines when Claude auto-invokes this skill. The body defines the workflow, the two-output contract (reformatted `.docx` CV + markdown strategy document), and delegates detail to the references.
- `skills/cv-opti/references/` — progressive-disclosure detail files that `SKILL.md` points to. Claude reads these on demand rather than up front:
  - `ats-optimization.md` — ATS formatting rules, keyword extraction, section naming.
  - `fraud-proofing.md` — verification, red flags, consistency/gap handling.
  - `achievement-bullets.md` — quantification framework, action verbs, interview-question test.
  - `customization-protocol.md` — per-job tailoring workflow used after initial optimization.
- `CV_OPTIMIZATION_SKILL_GUIDE.md`, `QUICK_REFERENCE.md`, `README.md` — top-level documentation about the skill package.

## Working on this skill

- Keep `SKILL.md` short and workflow-focused; push specifics into `references/*.md`. The description field is what triggers the skill, so edits to it directly affect invocation behavior.
- When producing CV output for a user, always generate **both** deliverables (reformatted CV + strategy document) — this two-output contract is the skill's defining promise.
- Preserve the authenticity/verifiability principle throughout: no change should introduce unverifiable claims, even to improve ATS keyword density.

## Related Skill Authoring Guidance

For structural/meta changes to this skill (frontmatter, progressive disclosure, description tuning), use the `skill-creator` or `plugin-dev:skill-development` skills rather than editing blind.
