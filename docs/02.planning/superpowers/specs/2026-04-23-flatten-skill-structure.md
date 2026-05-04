# Flatten Skill Structure

## Problem

The career-hub plugin uses a 2-layer nested skill structure (`skills/career-hub/` containing `init/`, `build/`, `publish/` sub-directories each with their own `SKILL.md`). Claude Code does not support sub-skills — each `SKILL.md` must be a direct child of a top-level directory under `skills/`.

## Design

Flatten to four independent top-level skills. Move shared references to a non-skill `skills/references/` directory.

### Target Structure

```
skills/
├── references/                    # shared, not a skill
│   ├── hub-detection.md
│   ├── taxonomy.md
│   └── templates.md
├── career-hub-init/
│   └── SKILL.md
├── career-hub-build/
│   └── SKILL.md
├── career-hub-publish/
│   ├── SKILL.md
│   └── targets/
│       ├── _adding-targets.md
│       ├── cv.md
│       ├── linkedin.md
│       └── github-profile.md
├── career-hub-optimise-cv/
│   ├── SKILL.md
│   └── references/
│       ├── achievement-bullets.md
│       ├── ats-optimization.md
│       ├── customization-protocol.md
│       └── fraud-proofing.md
```

### Changes per skill

**career-hub-init**
- Move from `skills/career-hub/init/SKILL.md` to `skills/career-hub-init/SKILL.md`.
- Fold in the hub structure diagram and principles list from the deleted parent `SKILL.md`.
- Update relative paths: shared references become `../references/`.

**career-hub-build**
- Move from `skills/career-hub/build/SKILL.md` to `skills/career-hub-build/SKILL.md`.
- Fold in the hub-first / draft-from-known-content philosophy from the deleted parent.
- Update relative paths: shared references become `../references/`.

**career-hub-publish**
- Move from `skills/career-hub/publish/` to `skills/career-hub-publish/`.
- Fold in the composition-with-cv-opti note from the deleted parent, updated to reference `career-hub-optimise-cv`.
- Update relative paths: shared references become `../references/`, targets stay as `targets/`.

**career-hub-optimise-cv**
- Rename from `skills/cv-opti/` to `skills/career-hub-optimise-cv/`.
- Update `name` field in frontmatter from `cv-opti` to `career-hub-optimise-cv`.
- References subdirectory moves as-is (no path changes needed internally).

### Deletions

- `skills/career-hub/` — entire directory (parent SKILL.md + old nested structure).
- `skills/cv-opti/` — replaced by `skills/career-hub-optimise-cv/`.

### Other files to update

- `CLAUDE.md` — update skill descriptions and structure references to reflect flat layout.
- `plugin.json` — no change needed (auto-discovery by directory convention).

### Content distribution from parent SKILL.md

The deleted parent `skills/career-hub/SKILL.md` contains content that must be preserved:

| Content | Destination |
|---------|-------------|
| Hub structure diagram (directory tree) | career-hub-init SKILL.md |
| Principles list (10 items) | career-hub-init SKILL.md |
| Hub-first / draft-from-known-content philosophy | career-hub-build SKILL.md |
| Composition with cv-opti note | career-hub-publish SKILL.md |
| Prior art section | career-hub-init SKILL.md |
| Future work section | Drop (tracked elsewhere or not yet relevant) |
| "When to Use" routing table | Drop (each skill's own description handles routing) |

### What does NOT change

- Shared reference content (hub-detection.md, taxonomy.md, templates.md) — unchanged, just moved.
- Target spec files (cv.md, linkedin.md, github-profile.md, _adding-targets.md) — unchanged, just moved.
- cv-opti references (achievement-bullets.md, etc.) — unchanged, just moved.
- Each skill's core SKILL.md behaviour/workflow — unchanged beyond path fixes and folded-in context.
- plugin.json — unchanged.
