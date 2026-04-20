---
name: career-hub-build
description: Interview-driven enrichment of a career hub. Given a category (foundations | roles | projects | capabilities) or a menu if no argument, reads existing stubs, drafts from known content, and asks the user only gap questions. Edits files in place, bumps last_updated, flips status from draft to active when substantively complete. Offers .private.md confidential siblings when candid content surfaces. Logs deferrals to g.backlog/ as one file per item.
---

# career-hub-build — Interview-Driven Enrichment

Enrich a career hub via conversational interview, one category at a time.

## When Claude Invokes This

Typical prompts:
- "build roles" / "build projects" / "build capabilities" / "build foundations"
- "fill out my role history"
- "let's update my career hub"

## Prerequisites

- `cwd` is a compliant hub (see `../references/hub-detection.md`). Refuse otherwise with a pointer to `init`.

## Behaviour

### Step 1 — Confirm hub

```
Hub detected at <cwd>.
- a.foundations: <4 files, X complete / Y stubs>
- b.history: <N roles, X active / Y draft>
- c.projects: <N projects, X active / Y draft>
- d.capabilities: <N cards, X active / Y skeleton>
- g.backlog: <N open threads>

Proceed with build <arg>? (y/n)
```

On explicit `y`, proceed.

### Step 2 — Select target unit(s)

**If invoked with a category argument** (`build roles`, `build projects`, `build capabilities`, `build foundations`):
- Enumerate files in that category directory.
- Ask the user the order: chronological, reverse-chronological, user-picks, auto-next-stub (next `status: draft` file in chronological order).

**If invoked bare** (`build`):
- Present a menu:
  ```
  Which category?
  1. foundations (4 files, 2 stubs)
  2. roles (12 files, 5 stubs)
  3. projects (9 files, 3 stubs)
  4. capabilities (6 skeletons)
  ```
- Wait for selection, then continue as above.

### Step 3 — For each unit, the draft-then-gap-questions loop

For each file selected:

1. **Read existing content** plus frontmatter, plus cross-references (linked roles, linked projects, linked capabilities, `a.foundations/biographical-facts.md`).
2. **Draft** a concise proposed fill-in for each of the category's body sections (Scope, Outcomes, Verification, Related, etc.).
3. **Ask gap questions only** — never ask what is already known or derivable from cross-references. Target 2-5 gap questions per unit for a quick pass.
4. On user response, **edit the file in place**:
   - Bump `last_updated` in frontmatter.
   - Flip `status: draft → active` if the unit is now substantively complete.
   - Cross-link to related files using relative paths.
5. **Offer confidential sibling** if candid content surfaces: "This includes sensitive political / failure / proprietary content. Create a `<filename>.private.md` sibling for candid notes?" — on yes, create the sibling with the confidential template.
6. **Log deferrals** — if a claim needs external info (reference name to confirm, conference event name, etc.), create a `g.backlog/<slug>.md` entry per the backlog item template, and register it in `g.backlog/README.md` index.
7. **Handle splits** — if the user flags that a single file should be split (e.g. a founder role covering two concurrent ventures), create the split files and update cross-references + README.md entries.

### Step 4 — Update downstream

After editing any role / project / capability file, also update:

- `README.md` — if the file's row caption changed (scope, active/draft status, headline).
- `a.foundations/biographical-facts.md` — if a numerical claim, tenure, or scope has changed.
- Cross-linked files — if a name, slug, or date changed.

### Step 5 — Commit at natural breakpoints

One commit per completed unit, OR one commit per category pass — operator's choice, default to one commit per unit.

Commit message format:
```
content(<category>): enrich <slug> — <brief summary>
```

Example:
```
content(b.history): enrich 2020-2021-nab-ad-optimisation — scope, outcomes, team structure
```

## Interview Posture

**Draft from known content. Ask only gap questions.**

The skill's differentiator. Don't ask what you can infer. Don't ask what cross-references already state. Don't run a fixed question list.

For each unit, after reading, your first message to the user is:

```
**<file name>** — draft from known content:

[short proposed fill-in for each body section, marked where gaps exist]

Gap questions:
1. <specific thing you can't infer>
2. <specific thing you can't infer>
3. <specific thing you can't infer>

Or skip ahead and answer in one message if easy.
```

Keep gap questions to 3-5 per unit on a quick pass. Offer deep-dive mode on request for high-CV-weight items.

## Mode: Quick vs Deep

Default is **quick pass** — fast gap-filling, target complete unit in one exchange where possible.

**Deep dive** on request — more thorough probing, additional questions about politics / proprietary details (offer `.private.md` sibling), follow-up on stories that would make good case studies.

## Refuses

- `cwd` not a hub (per `hub-detection.md`).
- Unit already `status: active` unless user explicitly asks to re-interview.

## Does Not

- Render to external artefacts (that is `publish`'s job).
- Enforce a fixed question list.
- Re-interview active files without explicit ask.
- Populate categories it wasn't asked to populate.
