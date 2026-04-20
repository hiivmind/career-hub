---
name: career-hub-publish
description: Render a draft target artefact from career-hub content. Built-in targets — cv, linkedin, github-profile. Extensible via target spec files in targets/. Applies visibility filter (public-only by default, never confidential). Drafts into f.pipeline/<target>-draft.md inside the hub — user copy-pastes out to the destination surface. Prints a cross-surface consistency posting checklist.
---

# career-hub-publish — Render a Draft Target

Render a draft CV / LinkedIn / GitHub-profile / custom target from the career hub's canonical content.

## When Claude Invokes This

Typical prompts:
- "publish cv"
- "publish linkedin"
- "publish github-profile"
- "render a <custom-target>"

## Prerequisites

- `cwd` is a compliant hub (see `../references/hub-detection.md`). Refuse otherwise with a pointer to `init`.

## Behaviour

### Step 1 — Confirm hub

```
Hub detected at <cwd>.
Publish target: <target>
Output path: <f.pipeline/<target>-draft.md>
Active positioning: <value from a.foundations/positioning.md>
Visibility filter: <from target spec, e.g. "public-only">

Proceed? (y/n)
```

On explicit `y`, proceed.

### Step 2 — Resolve the target spec

Read `targets/<target>.md` from this skill package. Built-in targets:
- `cv` → `targets/cv.md`
- `linkedin` → `targets/linkedin.md`
- `github-profile` → `targets/github-profile.md`

Custom target: read `targets/<target>.md` if it exists. Refuse with guidance if it doesn't.

See `targets/_adding-targets.md` for the target-spec schema.

### Step 3 — Apply the target spec

A target spec declares:
- **Source categories / files** — which hub files to read.
- **Output section structure** — the sections in the rendered output.
- **Length / character limits** per section.
- **Visibility filter** — default `public`, can widen to include `private` (for the user's own drafts) but never `confidential`.
- **Positioning variant** — read from `a.foundations/positioning.md` active marker unless the target overrides.
- **Output path** — where the draft lands inside the hub (default `f.pipeline/<target>-draft.md`).

Render the output following the spec exactly.

### Step 4 — Draft to hub

Write the rendered draft to the output path declared by the spec. Do not mutate any other hub files.

If the output file already exists, refuse with guidance:
```
Draft already exists at <path>. Pass --force to overwrite, or review the existing draft first.
```

### Step 5 — Print posting checklist

After writing, print a cross-surface consistency checklist tailored to the target:
```
Draft saved to <path>.

Posting checklist:
- [ ] Verify <claim X> against a.foundations/biographical-facts.md.
- [ ] Verify dates on <role Y> against b.history/<role Y>.md.
- [ ] Cross-check Headline / Summary consistency with <sibling surface>.
- [ ] Confirm no confidential content leaked.
- [ ] Paste <section-by-section for LinkedIn, whole-file for CV, etc.>.
```

Specific checklist items come from the target spec.

### Step 6 — Commit the draft

```bash
cd <cwd>
git add <output-path>
git commit -m "render(<target>): draft from hub content"
```

## Extending

New targets drop into `targets/<target>.md` following the schema in `targets/_adding-targets.md`. No skill-code changes required.

Example future targets (not in v1):
- `cover-letter` — per-application cover-letter template.
- `conference-bio` — short third-person bio for talk abstracts.
- `jsonresume` — JSON Resume schema-compatible render.
- `obsidian` — Obsidian-vault-shaped render with wikilinks.

## Refuses

- `cwd` not a hub.
- Target spec not found under `targets/<target>.md`.
- Output file already exists and no `--force` passed.

## Does Not

- Post to LinkedIn / GitHub / any external surface directly.
- Mutate hub content outside the declared output path.
- Render confidential content — regardless of target spec.
