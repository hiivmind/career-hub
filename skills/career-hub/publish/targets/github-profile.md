# Target Spec — GitHub Profile README

Renders a GitHub profile README for the user's profile repository (`<username>/<username>`). Lo-fi ASCII-box style, project-indexed (not temporal), under 250 lines. No emojis by default.

## Output

- **Path:** `f.pipeline/github-profile-README.md`
- **Format:** Markdown with fenced ASCII-box code blocks.

## Source

- `a.foundations/identity.md` — name, location, public contact links, GitHub handle.
- `a.foundations/positioning.md` — active variant drives the header subtitle.
- `b.history/2023-present-founder.md` (or equivalent current-chapter role) — current ventures list.
- `c.projects/*.md` where `visibility: public` and `status: active` — Selected Prior Work boxes.
- `d.capabilities/*.md` — Technical Skills table.

## Visibility filter

- Include: `public` only (this is a public surface).
- Include `status: active` only.

## Section structure

```
# <Name> | <Active positioning subtitle>

[LinkedIn badge] [Kaggle badge] [Email badge]

> <location>. <1-2 sentence experience anchor>. Full career timeline on [LinkedIn](...).

## Current Ventures

<ASCII box per current venture — ~4 boxes expected: founder role's listed ventures>

## Selected Prior Work

<ASCII box per curated project — ~6 boxes; NOT temporal, NOT exhaustive; chosen for technical or commercial interest; mix big-scale banking with open-source>

## Technical Skills

| Category | Tools |
| --- | --- |
| **Languages** | <from languages.md> |
| **AI / LLM Engineering** | <from ai-llm.md if present> |
| **Modern data stack** | <from data-stack.md> |
| **ML / Statistics** | <from ml-statistics.md> |
| **Infra & DevOps** | <from infra-platforms.md> |
| **<Domain>** | <from domain-expertise.md> |
| **Legacy / enterprise** | <from infra-platforms.md filtered to legacy> |

## Open-Source Projects

<ASCII box per actively-maintained public project; ~5 boxes expected>

## Let's Connect

- LinkedIn: [<handle>](...)
- Email: [<email>](mailto:...)
- <other public channels>

Open to: <from active positioning variant's "open to" line>.
```

### ASCII box format

```
┌────────────────────────────────────────────────────────────┐
│ <Project / Venture Name>                   <dates>         │
└────────────────────────────────────────────────────────────┘
  <role>

  • <bullet>
  • <bullet>
  • <bullet>

  <URL if public>
```

Fixed width: 60 columns. Pad or truncate accordingly.

## Length constraints

- Total: under 250 lines.
- Current Ventures: up to ~4 boxes.
- Selected Prior Work: up to ~6 boxes — curated, not exhaustive.
- Open-Source Projects: up to ~5 boxes.

## Consistency checks

- [ ] Every scale number in the boxes appears in `biographical-facts.md`.
- [ ] No `private` or `confidential` content.
- [ ] No internal project names for banking work — describe architecture and numbers, not internal names.
- [ ] GitHub handle in header matches `identity.md`.
- [ ] Email matches `identity.md`.
- [ ] "Open to" line matches active positioning variant.

## Notes

- Project-indexed, not temporal. Chronological career order belongs on LinkedIn.
- No emojis by default. Override via a `--emoji` flag on publish if the user explicitly wants them.
- GitHub uses CommonMark; tables and ASCII boxes both render cleanly in monospace.
- For a "hiring-signal" profile (vs "recruiter-sourced" profile), lead with a clear "Open to:" line at the end — specific engagement types, not "open to opportunities".
