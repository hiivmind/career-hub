# Target Spec — CV

Renders an ATS-friendly, 1-2 page markdown CV from the hub's canonical content. Feeds into `cv-opti` for per-job tuning.

## Output

- **Path:** `f.pipeline/cv-draft.md`
- **Format:** Markdown (single column, plain text — ATS-parseable).

## Source

- `a.foundations/identity.md` — contact block.
- `a.foundations/positioning.md` — active variant → Professional Summary tone and emphasis.
- `a.foundations/biographical-facts.md` — all numerical claims cross-check against this.
- `b.history/*.md` — role block per role (reverse-chronological).
- `c.projects/*.md` — "Selected engagements" bullets nested under the role they occurred in (for consultant / multi-engagement roles).
- `d.capabilities/*.md` — Technical Skills section.

## Visibility filter

- Include: `public`
- Exclude: `private`, `confidential`
- Exclude: files with `status: draft` or `status: archived`

## Section structure

```
# <Full Name>

<location> | <phone> | <email> | <LinkedIn> | <Kaggle/other> | <GitHub>

## Professional Summary

<2-3 sentences from active positioning variant — experience anchor, current focus, differentiators>

## Core Competencies

<single-line pipe-separated list from d.capabilities, weighted to active positioning>

## Professional Experience

### <Role title> — <Employer>
*<start> – <end> | <Location>*

<2-3 sentence role summary>

- <quantified outcome>
- <quantified outcome>

**Selected engagements** (for consultant roles):
- **<Project name>** — <one-sentence quantified summary with scale numbers>

### <Next role, reverse-chronological>
...

## Education

- **<Degree>**, <Institution>, <Location> — <Year>. <optional coursework line>

## Technical Skills

- **Languages:** <list from d.capabilities/languages.md>
- **ML / Statistics:** <list from d.capabilities/ml-statistics.md>
- **Modern data stack:** <list from d.capabilities/data-stack.md>
- **AI / LLM:** <list from d.capabilities/ai-llm.md if present>
- **Domain:** <list from d.capabilities/domain-expertise.md>
- **Legacy / enterprise:** <list from d.capabilities/infra-platforms.md filtered to legacy>

## Online

- LinkedIn: <URL>
- <other profiles from identity.md>

## References

Available upon request.
```

## Length constraints

- Target: 1-2 pages (~700-1200 words total).
- If over 2 pages: truncate oldest roles' bullet lists, keep titles/dates/employer; drop older Selected Engagements detail.
- If under 1 page: surface an additional quantified outcome per role, or expand Professional Summary.

## Consistency checks (included in the posting checklist)

- [ ] Every scale number (portfolio, exposure, team size, tenure) appears in `a.foundations/biographical-facts.md`.
- [ ] Role dates match `b.history/*.md` frontmatter exactly.
- [ ] Role titles match `b.history/*.md` frontmatter exactly.
- [ ] No `confidential` content leaked.
- [ ] LinkedIn URL, email, phone match `a.foundations/identity.md`.
- [ ] Professional Summary tone matches the active positioning variant.

## Notes

- This is the CV pre-optimisation. Feed the output to the sibling `cv-opti` skill for per-JD tuning, ATS keyword extraction, and fraud-proofing.
- Do not include the Objective or Career Summary Objective pattern — too generic; replaced by Professional Summary.
- If the user explicitly requests a longer academic CV (publications, talks, etc.), note the mismatch and suggest they add sections via a `cv-academic` target spec instead.
