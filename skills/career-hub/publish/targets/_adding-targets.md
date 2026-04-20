# Adding a Publish Target

New render targets drop into this directory as `<target-name>.md` files. No skill-code changes required. `publish <target-name>` resolves to this directory.

Underscore-prefixed files (`_adding-targets.md`) are meta-docs and are not themselves targets.

## Required sections in a target spec

Every target spec must declare these sections:

### `## Output`

- **Path:** where the rendered draft lands inside the hub (default convention: `f.pipeline/<target-name>-draft.md`).
- **Format:** file format (markdown, html, json, etc.).

### `## Source`

Which hub files drive the render. List specific files or globs.

Cross-reference `a.foundations/biographical-facts.md` for claim verification — this is conventional, not mandatory, but strongly recommended.

### `## Visibility filter`

Declare explicitly:
- Which visibility levels to include (`public`, optionally `private` for user's own drafts; never `confidential`).
- Which `status` values to include (default `active` only).

### `## Section structure`

Fenced code block showing the literal output shape with `<placeholder>` markers for content. This is the rendering recipe.

### `## Length constraints`

Per-section word / character / line limits. Explicit upper bounds, plus what to do on overshoot / undershoot.

### `## Consistency checks`

A checklist that the `publish` sub-skill appends to its output. Every render should cross-check claims against `biographical-facts.md` and cross-surface sibling drafts.
