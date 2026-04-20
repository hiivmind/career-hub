# Target Spec — LinkedIn Profile Refresh

Renders a LinkedIn profile draft: Headline, About, Experience descriptions (one per role), Skills, Featured items, and a posting checklist. Output is a single markdown file the user pastes section-by-section into LinkedIn.

## Output

- **Path:** `f.pipeline/linkedin-refresh.md`
- **Format:** Markdown with fenced code blocks per LinkedIn section (paste-ready).

## Source

- `a.foundations/identity.md` — LinkedIn URL, location.
- `a.foundations/positioning.md` — active variant drives Headline and About tone.
- `a.foundations/biographical-facts.md` — all numerical claims cross-check.
- `b.history/*.md` — one Experience description per role.
- `c.projects/*.md` — case-study bullets nested in consultant roles.
- `d.capabilities/*.md` — Skills list (top 3 pinned + up to 50 total).
- `e.artefacts/index.md` — candidates for Featured items.

## Visibility filter

- Include: `public`
- Exclude: `private`, `confidential`
- Include `status: active` only.

## Section structure

```
# LinkedIn Refresh — Draft

**Positioning:** <active variant name>

## Headline

> <120-220 char headline built from active positioning variant>

## About

<≤2,600 chars; 3-5 paragraphs; lead with current focus, then experience anchor, then specific highlights with scale numbers, then close with open-to.>

## Experience — Role Descriptions

### <YYYY-MM – YYYY-MM · Role · Employer>
```

<500-2000 chars per role; 1 short intro paragraph + 3-8 bullet points of quantified outcomes>

### <next role>
...

## Featured (pin in this order)

1. <item from e.artefacts/index.md with public visibility>
2. <item>
3. <item>
4. <item>

## Skills

**Top 3 pinned:**
1. <skill>
2. <skill>
3. <skill>

**Full list (50-cap):**

<skill> · <skill> · ...

## Posting Checklist

- [ ] Review About for tone and factual accuracy.
- [ ] Paste role descriptions role-by-role (LinkedIn requires updating each role individually).
- [ ] Pin the 3 top skills.
- [ ] Add Featured items in order.
- [ ] Cross-check: biographical-facts.md → LinkedIn (every claim consistent).
- [ ] Cross-check: cv-draft.md → LinkedIn (dates, tenures, numbers match).
- [ ] Post once all sections updated so the refresh shows as one coherent change.
```

## Length constraints

- Headline: 120-220 chars.
- About: ≤2,600 chars (LinkedIn hard limit).
- Experience per role: 500-2,000 chars. Senior / current roles favour the upper end; early-career roles the lower.
- Skills full list: ≤50 items (LinkedIn cap).

## Consistency checks

- [ ] Headline ties to the active positioning variant.
- [ ] About opens with current focus (not historical), matches positioning.
- [ ] Every scale number appears in `biographical-facts.md`.
- [ ] Role dates match `b.history/*.md` frontmatter.
- [ ] Role titles match `b.history/*.md` frontmatter.
- [ ] No `confidential` content leaked.
- [ ] Skills top-3 align with active positioning variant.

## Notes

- LinkedIn does not allow HTML in role descriptions — emit plain text with bullet markers (•) inside the code blocks.
- LinkedIn Featured accepts links and uploads; the draft lists candidates, the user adds them manually.
- Emit one code block per paste-section so the user can copy cleanly.
