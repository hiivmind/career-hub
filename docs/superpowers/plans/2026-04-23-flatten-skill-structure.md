# Flatten Skill Structure — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Flatten the 2-layer nested skill structure into four independent top-level skills with a shared references directory.

**Architecture:** Move files, update relative paths, distribute parent SKILL.md content into child skills, rename cv-opti to career-hub-optimise-cv. No code — all markdown.

**Tech Stack:** Markdown, YAML frontmatter, git.

---

### Task 1: Create `skills/references/` and move shared reference files

**Files:**
- Create: `skills/references/hub-detection.md` (moved from `skills/career-hub/references/hub-detection.md`)
- Create: `skills/references/taxonomy.md` (moved from `skills/career-hub/references/taxonomy.md`)
- Create: `skills/references/templates.md` (moved from `skills/career-hub/references/templates.md`)

- [ ] **Step 1: Create directory and move files**

```bash
cd /home/nathanielramm/git/hiivmind/career-hub
mkdir -p skills/references
cp skills/career-hub/references/hub-detection.md skills/references/hub-detection.md
cp skills/career-hub/references/taxonomy.md skills/references/taxonomy.md
cp skills/career-hub/references/templates.md skills/references/templates.md
```

- [ ] **Step 2: Update `hub-detection.md` — replace "sub-skills" with "skills"**

In `skills/references/hub-detection.md`, make these edits:

- Line 3: `How sub-skills decide whether` → `How skills decide whether`
- Line 15: `## Sub-skill confirmation behaviour` → `## Skill confirmation behaviour`
- Line 17: `All three sub-skills (\`init\`, \`build\`, \`publish\`) confirm` → `All three skills (\`career-hub-init\`, \`career-hub-build\`, \`career-hub-publish\`) confirm`

- [ ] **Step 3: Verify files exist at new location**

```bash
ls -la skills/references/
```

Expected: three `.md` files.

- [ ] **Step 4: Commit**

```bash
git add skills/references/
git commit -m "refactor: move shared references to skills/references/"
```

---

### Task 2: Create `skills/career-hub-init/SKILL.md`

**Files:**
- Create: `skills/career-hub-init/SKILL.md`

Content is the existing `skills/career-hub/init/SKILL.md` with:
1. Relative path updates (`../references/` → `../references/`)  — paths happen to stay the same depth, so `../references/` is correct.
2. Folded-in content from the parent `skills/career-hub/SKILL.md`:
   - Hub structure diagram (lines 46–71 of parent)
   - Principles list (lines 75–86 of parent)
   - Prior art section (lines 98–106 of parent)

- [ ] **Step 1: Create directory**

```bash
mkdir -p /home/nathanielramm/git/hiivmind/career-hub/skills/career-hub-init
```

- [ ] **Step 2: Write the SKILL.md**

Copy the full content of `skills/career-hub/init/SKILL.md` into `skills/career-hub-init/SKILL.md`, then apply these changes:

1. After the "## When Claude Invokes This" section (after line 16 of the original), add:

```markdown

## Hub Structure

The hub produced by this skill has this mandated structure:

\`\`\`
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
\`\`\`

## Principles (seeded into `PRINCIPLES.md`)

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
```

2. Update the reference path on line 17 of the original: `See \`../references/hub-detection.md\`` stays as `../references/hub-detection.md` (same relative depth).

3. Update the next-step suggestion at the end (Step 7) — replace `build foundations`, `build roles`, etc. with the new skill names:

```markdown
Next steps:
- `career-hub-build foundations` — fill identity, positioning, biographical facts, operating notes.
- `career-hub-build roles` — start populating role cards.
- `career-hub-build projects` — start populating project case studies.
- `career-hub-build capabilities` — enrich the 6 seed capability cards.

Or `career-hub-build` with no argument to get a menu.
```

4. Before the final `## Does Not` section, add:

```markdown
## Prior Art

This skill draws on and differentiates from:

- **olegvg/resume-tailor-plugin** — single-file master profile, per-role visibility tags.
- **nyinyinyanlin/profile-vault-obsidian** — folder-per-category Obsidian vault.
- **erichowens/career-biographer + cv-creator** — interview-plus-render split, empathetic interview style.
- **jacksenechal/resume** — markdown resume with branch-based tailoring.
- **demansou/resume-builder** — evidence-mining, confidentiality-by-design.

Differentiators: category taxonomy with precedence; `.private.md` siblings; gap-question-only interview posture; `e.artefacts/` with migration rule; `g.backlog/` category; hub-first philosophy.
```

- [ ] **Step 3: Verify the file**

```bash
head -5 skills/career-hub-init/SKILL.md
```

Expected: frontmatter with `name: career-hub-init`.

- [ ] **Step 4: Commit**

```bash
git add skills/career-hub-init/
git commit -m "refactor: create top-level career-hub-init skill"
```

---

### Task 3: Create `skills/career-hub-build/SKILL.md`

**Files:**
- Create: `skills/career-hub-build/SKILL.md`

Content is the existing `skills/career-hub/build/SKILL.md` with:
1. Relative path updates (`../references/` → `../references/` — same depth, no change needed).
2. Folded-in content from parent: hub-first / draft-from-known-content philosophy.

- [ ] **Step 1: Create directory**

```bash
mkdir -p /home/nathanielramm/git/hiivmind/career-hub/skills/career-hub-build
```

- [ ] **Step 2: Write the SKILL.md**

Copy the full content of `skills/career-hub/build/SKILL.md` into `skills/career-hub-build/SKILL.md`, then apply these changes:

1. After the "## When Claude Invokes This" section (after line 11), add:

```markdown

## Design Philosophy

**Hub-first, rendering-second.** The hub is the source of truth; CVs, LinkedIn, and GitHub profile pages are views onto it. Every public claim traces to an entry in the hub.

**Draft-from-known-content, ask-only-gap-questions.** When `build` enriches a stub, Claude drafts from existing hub content and cross-references, and asks the user only *gap questions* — never redundant questions. Fast, low-friction enrichment.

**Every claim verifiable.** No unverifiable adjectives ("expert", "pioneered"). Scale numbers and verification methods live in `a.foundations/biographical-facts.md`.
```

2. Update the pointer to `init` in the Prerequisites section (line 19): change `Refuse otherwise with a pointer to \`init\`.` to `Refuse otherwise with a pointer to \`career-hub-init\`.`

- [ ] **Step 3: Verify the file**

```bash
head -5 skills/career-hub-build/SKILL.md
```

Expected: frontmatter with `name: career-hub-build`.

- [ ] **Step 4: Commit**

```bash
git add skills/career-hub-build/
git commit -m "refactor: create top-level career-hub-build skill"
```

---

### Task 4: Create `skills/career-hub-publish/`

**Files:**
- Create: `skills/career-hub-publish/SKILL.md`
- Create: `skills/career-hub-publish/targets/_adding-targets.md` (moved as-is)
- Create: `skills/career-hub-publish/targets/cv.md` (moved as-is)
- Create: `skills/career-hub-publish/targets/linkedin.md` (moved as-is)
- Create: `skills/career-hub-publish/targets/github-profile.md` (moved as-is)

- [ ] **Step 1: Create directory and copy targets**

```bash
cd /home/nathanielramm/git/hiivmind/career-hub
mkdir -p skills/career-hub-publish/targets
cp skills/career-hub/publish/targets/_adding-targets.md skills/career-hub-publish/targets/
cp skills/career-hub/publish/targets/cv.md skills/career-hub-publish/targets/
cp skills/career-hub/publish/targets/linkedin.md skills/career-hub-publish/targets/
cp skills/career-hub/publish/targets/github-profile.md skills/career-hub-publish/targets/
```

- [ ] **Step 2: Write the SKILL.md**

Copy the full content of `skills/career-hub/publish/SKILL.md` into `skills/career-hub-publish/SKILL.md`, then apply these changes:

1. Update the pointer to `init` in the Prerequisites section (line 16): change `Refuse otherwise with a pointer to \`init\`.` to `Refuse otherwise with a pointer to \`career-hub-init\`.`

2. After the "## When Claude Invokes This" section (after line 11), add:

```markdown

## Composition with `career-hub-optimise-cv`

```
career-hub-publish cv  →  career-hub-optimise-cv  →  ATS-optimised, JD-tuned CV
```

The two skills do not depend on each other at runtime but compose naturally: `career-hub-publish cv` produces an ATS-friendly markdown CV, which `career-hub-optimise-cv` then tunes against a specific job description.
```

3. Reference paths: `../references/hub-detection.md` stays correct (same depth). `targets/` paths stay as `targets/` (same relative location).

- [ ] **Step 3: Verify the file and targets**

```bash
head -5 skills/career-hub-publish/SKILL.md
ls skills/career-hub-publish/targets/
```

Expected: frontmatter with `name: career-hub-publish`, four target files listed.

- [ ] **Step 4: Commit**

```bash
git add skills/career-hub-publish/
git commit -m "refactor: create top-level career-hub-publish skill"
```

---

### Task 5: Create `skills/career-hub-optimise-cv/`

**Files:**
- Create: `skills/career-hub-optimise-cv/SKILL.md` (moved from `skills/cv-opti/SKILL.md`)
- Create: `skills/career-hub-optimise-cv/references/achievement-bullets.md` (moved as-is)
- Create: `skills/career-hub-optimise-cv/references/ats-optimization.md` (moved as-is)
- Create: `skills/career-hub-optimise-cv/references/customization-protocol.md` (moved as-is)
- Create: `skills/career-hub-optimise-cv/references/fraud-proofing.md` (moved as-is)

- [ ] **Step 1: Create directory and copy references**

```bash
cd /home/nathanielramm/git/hiivmind/career-hub
mkdir -p skills/career-hub-optimise-cv/references
cp skills/cv-opti/references/achievement-bullets.md skills/career-hub-optimise-cv/references/
cp skills/cv-opti/references/ats-optimization.md skills/career-hub-optimise-cv/references/
cp skills/cv-opti/references/customization-protocol.md skills/career-hub-optimise-cv/references/
cp skills/cv-opti/references/fraud-proofing.md skills/career-hub-optimise-cv/references/
```

- [ ] **Step 2: Write the SKILL.md**

Copy the full content of `skills/cv-opti/SKILL.md` into `skills/career-hub-optimise-cv/SKILL.md`, then change the frontmatter `name` field:

```yaml
name: career-hub-optimise-cv
```

No other changes needed — internal reference paths (`references/achievement-bullets.md` etc.) stay the same relative to SKILL.md.

- [ ] **Step 3: Verify**

```bash
head -5 skills/career-hub-optimise-cv/SKILL.md
ls skills/career-hub-optimise-cv/references/
```

Expected: frontmatter with `name: career-hub-optimise-cv`, four reference files listed.

- [ ] **Step 4: Commit**

```bash
git add skills/career-hub-optimise-cv/
git commit -m "refactor: rename cv-opti to career-hub-optimise-cv"
```

---

### Task 6: Delete old skill directories

**Files:**
- Delete: `skills/career-hub/` (entire directory)
- Delete: `skills/cv-opti/` (entire directory)

- [ ] **Step 1: Remove old directories**

```bash
cd /home/nathanielramm/git/hiivmind/career-hub
git rm -r skills/career-hub/
git rm -r skills/cv-opti/
```

- [ ] **Step 2: Verify only new structure remains**

```bash
find skills/ -name "SKILL.md" | sort
```

Expected output:
```
skills/career-hub-build/SKILL.md
skills/career-hub-init/SKILL.md
skills/career-hub-optimise-cv/SKILL.md
skills/career-hub-publish/SKILL.md
```

- [ ] **Step 3: Verify references directory**

```bash
ls skills/references/
```

Expected: `hub-detection.md  taxonomy.md  templates.md`

- [ ] **Step 4: Commit**

```bash
git commit -m "refactor: remove old nested skill directories"
```

---

### Task 7: Update `CLAUDE.md`

**Files:**
- Modify: `CLAUDE.md`

- [ ] **Step 1: Replace the Skills section**

Replace the existing `## Skills` section (lines 9–17 of `CLAUDE.md`) with:

```markdown
## Skills

Four top-level skills under `skills/`:

- **`career-hub-init/`** — scaffold an empty compliant hub at `cwd`.
- **`career-hub-build/`** — interview-driven enrichment of stubs; drafts from existing content and asks only gap questions.
- **`career-hub-publish/`** — render a draft target from hub content. Built-in targets live in `career-hub-publish/targets/` (`cv.md`, `linkedin.md`, `github-profile.md`); see `career-hub-publish/targets/_adding-targets.md` for the target-spec schema.
- **`career-hub-optimise-cv/`** — per-job CV optimization for the dual-AI hiring landscape (ATS + fraud detection). Produces a reformatted CV plus a strategy document explaining every change.

The latter two compose: `career-hub-publish cv` produces an ATS-friendly markdown CV that `career-hub-optimise-cv` then tunes against a specific job description.
```

- [ ] **Step 2: Update the Shared References section**

Replace the existing `## Shared References` section (lines 29–33) with:

```markdown
## Shared References

`skills/references/` — used by career-hub-init, career-hub-build, and career-hub-publish:
- `hub-detection.md` — how each skill confirms hub location at `cwd` before writing.
- `taxonomy.md` — four axes (category/visibility/audience/status), `.private.md` sibling convention, universal frontmatter.
- `templates.md` — entry templates.
```

- [ ] **Step 3: Update the Architecture Conventions section**

In the `## Architecture Conventions` bullet list, update references:
- Change `(career-hub)` to `(career-hub-init/build/publish)` where it appears.
- Change `(cv-opti)` to `(career-hub-optimise-cv)` where it appears.

- [ ] **Step 4: Update the Working on these skills section**

Replace `sub-skills` with `skills` in the last section.

- [ ] **Step 5: Commit**

```bash
git add CLAUDE.md
git commit -m "docs: update CLAUDE.md for flat skill structure"
```

---

### Task 8: Final verification

- [ ] **Step 1: Verify complete directory structure**

```bash
cd /home/nathanielramm/git/hiivmind/career-hub
find skills/ -type f | sort
```

Expected:
```
skills/career-hub-build/SKILL.md
skills/career-hub-init/SKILL.md
skills/career-hub-optimise-cv/SKILL.md
skills/career-hub-optimise-cv/references/achievement-bullets.md
skills/career-hub-optimise-cv/references/ats-optimization.md
skills/career-hub-optimise-cv/references/customization-protocol.md
skills/career-hub-optimise-cv/references/fraud-proofing.md
skills/career-hub-publish/SKILL.md
skills/career-hub-publish/targets/_adding-targets.md
skills/career-hub-publish/targets/cv.md
skills/career-hub-publish/targets/github-profile.md
skills/career-hub-publish/targets/linkedin.md
skills/references/hub-detection.md
skills/references/taxonomy.md
skills/references/templates.md
```

- [ ] **Step 2: Verify no stale references remain**

```bash
cd /home/nathanielramm/git/hiivmind/career-hub
grep -r "sub-skill" skills/ || echo "No stale sub-skill references"
grep -r "cv-opti" skills/ CLAUDE.md || echo "No stale cv-opti references"
grep -r "skills/career-hub/" skills/ CLAUDE.md || echo "No stale nested path references"
```

Expected: no matches (all three commands print the "No stale..." fallback).

- [ ] **Step 3: Fix any stale references found in Step 2**

If any grep matches, edit the offending files to use the new names/paths.

- [ ] **Step 4: Final commit if fixes were needed**

```bash
git add -A
git commit -m "fix: remove remaining stale references to old skill structure"
```

Only run this if Step 3 produced changes.

- [ ] **Step 5: Review git log**

```bash
git log --oneline -10
```

Expected: 7-8 commits from this plan (Tasks 1–7, plus optional Task 8 fix).
