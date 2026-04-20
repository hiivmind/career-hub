# Career Hub Skill — Design Spec

**Date:** 2026-04-20
**Status:** Draft, awaiting user review
**Location on disk:** `cv-optimiser/skills/career-hub/` (sibling to existing `cv-opti`)

---

## 1. Purpose

A Claude Code skill that turns the interview-plus-rendering process piloted on `nathanielramm-central` (April 2026) into a repeatable, opinionated pattern for any professional.

The skill produces and maintains a **canonical career hub** — a markdown-plus-YAML repository that is the single source of truth for role history, project case studies, capabilities, artefacts, and pipeline — and renders downstream artefacts (CV, LinkedIn profile, GitHub profile README) from it.

**Design philosophy:** hub-first, renders-second. The hub is what you maintain; CVs, LinkedIn content, and profile pages are views onto it. Every claim in every downstream artefact traces to an entry in the hub.

## 2. Scope

**In scope (v1):**
- `init` sub-skill — scaffold an empty, compliant hub in the current directory.
- `build` sub-skill — interview-driven enrichment of hub stubs, category-by-category.
- `publish` sub-skill — render CV / LinkedIn / GitHub-profile drafts from hub content.
- Mandated category taxonomy (`a.foundations` → `g.backlog`).
- Mandated visibility taxonomy (`public` / `private` / `confidential`) + `.private.md` sibling-file pattern.
- Extensible publish targets — new rendering specs drop into `publish/targets/`.

**Out of scope (v1), tracked for future work:**
- `publish jsonresume` — JSON Resume schema-compatible render for interop with HackMyResume, resumx, etc.
- `publish obsidian` — render hub content as an Obsidian vault (folders + wikilinks + dataview frontmatter).
- `practise interview` sub-skill — generate typical role questions from `f.pipeline/target-roles.md` + hub content, encourage voice-mode practice, identify gaps and weak stories.
- Evidence-mining from git commits or docs (demansou/resume-builder style).
- Dashboard or metrics views over the hub (lucidRESUME, career-ops style — deliberately excluded; markdown-first is the whole point).

## 3. Prior Art and Differentiation

This design builds on a crowded landscape. Notable predecessors worth acknowledging in `PRINCIPLES.md`:

- **[olegvg/resume-tailor-plugin](https://github.com/olegvg/resume-tailor-plugin)** — Claude Code plugin with a persisted "master profile" and per-role visibility tagging. Closest architecture match; single-file profile rather than a multi-category hub.
- **[nyinyinyanlin/profile-vault-obsidian](https://github.com/nyinyinyanlin/profile-vault-obsidian)** — folder-per-category Obsidian vault with self-documenting templates. Closest structural match; Obsidian-native rather than skill-invoked.
- **[erichowens/career-biographer + cv-creator](https://skills.sh/erichowens/some_claude_skills/career-biographer)** — two-skill split (interview → render). Closest process match; empathetic-open-ended interview versus our gap-question-only posture.
- **[jacksenechal/resume](https://github.com/jacksenechal/resume)** — markdown resume with branch-based tailoring and AGENTS.md/CONTEXT.md. Shares the canonical-facts-plus-variants philosophy, uses git branches rather than a hub.
- **[demansou/resume-builder](https://github.com/demansou/resume-builder)** — evidence-mining and confidentiality-by-design. Similar anti-hallucination stance to our fraud-proofing principle.

**Where this skill is distinct:**

1. **Category taxonomy with precedence** (`a.foundations` → `g.backlog`, canonical-home-is-lower-letter rule).
2. **`.private.md` sibling-file pattern** for candid retrospection on otherwise-public roles/projects.
3. **Interview as discrete phased sub-skills** — roles, projects, capabilities, foundations as separable passes.
4. **Draft-from-known-content-ask-only-gap-questions** interview posture (named as a principle, see §6).
5. **`e.artefacts/` pointer-index** with explicit external-canonical-plus-migration-rule.
6. **`g.backlog/` deferred-items convention** as a first-class category.
7. **Hub-first philosophy** — enriching the hub is the primary action; rendering is a consumer.

## 4. Package Layout

```
cv-optimiser/skills/career-hub/
├── SKILL.md                    # umbrella: when-to-use, workflow, links to sub-skills
├── references/
│   ├── taxonomy.md             # 4 axes: category / visibility / audience / status
│   ├── templates.md            # universal frontmatter + per-category body templates
│   └── hub-detection.md        # how to detect / confirm a hub at cwd
├── init/
│   └── SKILL.md                # scaffold an empty hub in cwd
├── build/
│   └── SKILL.md                # interview-driven enrichment; category arg or menu
└── publish/
    ├── SKILL.md                # render a draft from hub content; target arg
    └── targets/
        ├── cv.md               # CV render spec
        ├── linkedin.md         # LinkedIn render spec
        ├── github-profile.md   # GitHub profile README render spec
        └── _adding-targets.md  # target-spec schema; how to add a new target
```

Umbrella `SKILL.md` is the entry point. It describes the end-to-end loop (init → build → publish), delegates to sub-skills for phase-specific work, and points at references for taxonomy and templates.

Implementation is **documented, thin** — no code, no bespoke tooling. Skills are markdown instructions that tell Claude how to do file operations via Read / Write / Edit / Bash. Matches the existing `cv-opti` pattern.

## 5. Hub Structure (produced by `init`)

```
<hub>/
├── PRINCIPLES.md               # taxonomy, precedence, templating, .private.md convention, prior-art notes
├── README.md                   # cross-category index table
├── a.foundations/              # canonical facts
│   ├── identity.md
│   ├── positioning.md          # alternative narratives per audience; one marked active
│   ├── biographical-facts.md   # verifiable-claims table with verification methods
│   └── operating-notes.md      # cross-surface consistency rules
├── b.history/                  # role cards (one per role)
├── c.projects/                 # project case-study cards
├── d.capabilities/             # claim-and-evidence cards per capability area
├── e.artefacts/                # pointer index to rendered outputs + evidence artefacts
│   ├── README.md               # why pointers-only
│   └── index.md                # pointer table
├── f.pipeline/                 # forward-looking working docs
│   ├── target-roles.md
│   ├── unwritten-case-studies.md
│   ├── open-threads.md
│   └── application-log.md
├── g.backlog/                  # one file per deferred item
│   └── README.md
└── docs/superpowers/
    ├── specs/
    └── plans/
```

Mandated, not configurable.

## 6. Principles (appearing in `PRINCIPLES.md`)

1. **Category precedence.** When a fact could live in multiple categories, the lower-letter category wins. Other categories reference via cross-links, do not duplicate content.
2. **Visibility is explicit.** Every file declares `visibility: public | private | confidential` in frontmatter. Rendering filters on this; confidential never leaves the hub.
3. **Confidential sibling pattern.** For roles/projects with public cards, candid retrospection lives in a sibling `.private.md` file with `visibility: confidential`.
4. **Status markers.** `active` / `draft` / `archived`. Archived = deletion candidate; no "deprecated".
5. **Templates for all docs.** Every file type has a template; `init` creates from templates; `build` extends from templates.
6. **Stubs, not blanks.** `init` produces stubs with frontmatter, TL;DR, and `TODO` markers — not empty files. Stubs show what to fill in.
7. **Canonical-here vs external.** Some artefacts (e.g. a public case study) live outside the hub. `e.artefacts/index.md` tracks both with a migration rule (flip "canonical location" to inside-the-hub when migrated).
8. **Hub-first.** The hub is the source of truth. Downstream CVs / LinkedIn / GitHub are rendered views; update the hub, then re-render.
9. **Draft-from-known-content.** When Claude enriches a stub in `build`, it drafts first from existing content (role files, cross-referenced projects, biographical facts) and asks the user only **gap questions** — never redundant questions. (This is the primary interview-style differentiator from empathetic-interview predecessors.)
10. **Every claim verifiable.** No unverifiable adjectives, no hallucinations. Scale numbers and verification methods live in `biographical-facts.md`.

## 7. Sub-Skill Behaviours

### 7.1 `init`

**Inputs:** invocation from `<cwd>` (an empty or near-empty directory).

**Behaviour:**
1. Confirm hub creation: `"Create a career hub at <cwd>? This will create ~40 files. Proceed?"`
2. On approval, create the full structure in §5. Seed `a.foundations/` with prompts. Seed `d.capabilities/` with six skeleton cards (languages, data stack, ML, domain expertise, platforms, credentials). Leave `b.history/`, `c.projects/`, `f.pipeline/`, `g.backlog/` as empty directories with README pointers.
3. `git init`, initial commit.
4. Print path + next-step suggestion (`build foundations` or `build roles`).

**Refuses:**
- `cwd` already contains a hub (detected per `references/hub-detection.md`).
- `cwd` is a non-empty directory that is not a hub (to avoid accidental overwrite).

### 7.2 `build`

**Inputs:**
- Bare `build` — lists categories with stub counts, asks user to pick.
- `build foundations | roles | projects | capabilities` — category-targeted.

**Behaviour:**
1. Confirm hub at `cwd`: `"Hub detected at <path>. Proceed?"`
2. Enumerate units in the chosen category.
3. Ask order (chronological / reverse-chron / user-picks / auto-next-stub).
4. For each unit:
   - Read existing content and cross-references.
   - Draft from known content; ask **gap questions only**.
   - Edit the file in place; bump `last_updated`; flip `status` to `active` when substantively complete.
   - Handle splits (e.g. one role → two files) when user flags them.
   - Offer a `.private.md` sibling if candid content surfaces.
   - Log deferrals to `g.backlog/` as one file per item.
5. Update `README.md` and `biographical-facts.md` when role dates or scope change.
6. Commit at natural breakpoints (per-category pass, or per major split).

**Refuses:**
- `cwd` is not a hub.
- Units already `status: active` are not re-interviewed unless user explicitly asks.

### 7.3 `publish`

**Inputs:** `publish cv | linkedin | github-profile | <custom-target>`.

**Behaviour:**
1. Confirm hub at `cwd`.
2. Read target spec at `publish/targets/<target>.md`.
3. Draft the output to `f.pipeline/<target>-draft.md` (or whatever path the target spec declares inside the hub).
4. Apply the visibility filter declared in the spec (public-only by default; never includes `confidential`).
5. Print a posting checklist (cross-surface consistency: does this match LinkedIn, CV, biographical facts?).
6. Commit the draft.

**Target spec schema** (see `publish/targets/_adding-targets.md`):
- Source categories / files.
- Output section structure.
- Length / character limits per section.
- Visibility filter.
- Positioning variant (read from `a.foundations/positioning.md` active marker).
- Output path (inside hub).

**Refuses:**
- A draft already exists at the output path and no `--force` was passed.

## 8. Data Shapes

Universal frontmatter (every file):

```yaml
visibility: public | private | confidential
audience: human | ai-agent | both
status: active | draft | archived
last_updated: YYYY-MM-DD
```

Category-specific frontmatter additions and body templates live in `references/templates.md`. Categories:

- **`b.history`** — role card: `role`, `employer`, `start`, `end`. Body: TL;DR / Context / Scope / Key Systems & Projects / Outcomes / Verification / Related Roles.
- **`c.projects`** — case-study card: `project`, `employer`, `via` (optional, for sub-consulting), `dates`, `role`, `client` (optional, usually private). Body: Headline / Problem / Approach / Result / Tech / Context / Verifiability / External Publications / Related.
- **`d.capabilities`** — claim card: `capability`. Body: Summary / Proficiency Claim / Evidence (links to `b.history` and `c.projects`) / Interview-Defensibility / Recency Notes.
- **`a.foundations`** — per-file shapes documented in `references/templates.md`.
- **`e.artefacts`** — pointer-index rows (canonical location, mirror(s), purpose, format, visibility, updated).
- **`f.pipeline`** — working-doc shapes.
- **`g.backlog`** — one-file-per-item: context, missing info, resolution path, destination-when-resolved.

## 9. Interaction Design

- **`init`** is a one-shot scaffold with a single confirmation.
- **`build`** is a conversational pass. For each unit, Claude presents a concise draft from known content, numbered gap questions, and awaits user input. Fast, gap-filling style — not empathetic open-ended.
- **`publish`** is a non-conversational transformation. Produces a draft file + checklist.

All three sub-skills confirm the detected hub path before acting.

## 10. Integration with `cv-opti`

`cv-opti` already exists in `cv-optimiser/skills/cv-opti/` and tunes an existing CV for ATS and fraud detection against a specific JD. Integration is sequential:

1. `career-hub:publish cv` — produces an ATS-friendly CV markdown from hub content.
2. `cv-opti` — takes that markdown (or any existing CV) and tunes it to a specific job description.

The two skills compose; neither depends on the other at runtime. Documentation in both SKILL.md files notes this composition.

## 11. Future Work (explicit backlog)

Items deferred from v1, tracked for future releases:

1. **`publish jsonresume`** — render the hub as a JSON Resume schema document. Enables interop with HackMyResume, resumx, incipit, and any JSON-Resume-compatible downstream tool.
2. **`publish obsidian`** — render the hub as an Obsidian vault structure (folders, wikilinks, dataview-friendly frontmatter) so it can be opened and edited in Obsidian without losing the skill's shape.
3. **`practise interview`** sub-skill — given the hub and an entry in `f.pipeline/target-roles.md`, generate typical interview questions for the target role, encourage voice-mode rehearsal, and identify story gaps or weak answers to drill.
4. Evidence-mining (`build --evidence-scan` mode) — scan git commits, docs, and external artefacts for accomplishments worth surfacing in stubs. Inspired by demansou/resume-builder.
5. Cross-surface consistency lint — a `check` sub-skill that validates every public claim in the hub against CV draft, LinkedIn draft, and biographical-facts table.

## 12. Success Criteria

- A new user can run `init` in an empty directory and end up with a compliant hub they can start editing immediately.
- `build roles` reaches complete, `status: active` cards for a 10–15 role career in one or two sessions, with gap-questions-only interaction.
- `publish cv` emits a markdown CV that passes downstream `cv-opti` tuning without rework.
- `publish linkedin` emits a draft that can be pasted into LinkedIn section-by-section without a second editing pass.
- A user can add a new publish target (e.g. cover-letter) by dropping a spec into `publish/targets/` — no skill code changes.
- The skill passes the four-axis self-check for public rendering: no hallucinations, no unverifiable adjectives, no confidential content leaks, no cross-surface inconsistencies.

---

*Spec written after brainstorming session, 2026-04-20, following a 4-day pilot building `nathanielramm-central`. Ready for user review before implementation planning.*
