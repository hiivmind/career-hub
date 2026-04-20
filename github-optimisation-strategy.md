# GitHub Optimisation Strategy — Nathaniel Ramm

Tailored synthesis of current (2025–2026) recruiter practices, sourcing-tool behaviour, and signal-intelligence research, mapped onto your existing GitHub footprint (`discreteds`, `hiivmind`, `mountainash-io`, `kleene-games`).

---

## 1. How recruiters actually read a GitHub profile

Across 150+ recruiter surveys reported by HireResume and Riem.ai, the consistent order of attention is:

| # | Element | % of recruiters check | What they want |
| - | --- | --- | --- |
| 1 | **Pinned repos + their READMEs** | 92% | Does the work look serious? Clear README = click into code |
| 2 | **Contribution graph** | 78% | "Is this person actively coding?" (not counting squares) |
| 3 | **Profile bio + README** | 71% | Role title, specialisation, contact path |
| 4 | **Recent activity feed** | 54% | Commits, PRs, issues in last 30–90 days |
| 5 | **Code quality in top repo** | 41% | Only technical screeners; they read file structure, then one random file |
| 6 | **Stars / forks** | 38% | Social proof; 50+ stars gets attention |
| 7 | **OSS contributions to known projects** | 35% | Merged PRs = instant credibility |

**The 30-second rule:** average time a recruiter spends before deciding to dig deeper. Optimise for the first three rows — they're 100% of what 70% of recruiters see.

---

## 2. The 30-second filter applied to your profile

When a recruiter lands on `github.com/discreteds` today, here's what they see and what it signals:

| Observation | Signal | Action |
| --- | --- | --- |
| No profile README | Looks unset / amateur | ✅ Drafted in `github-profile-README.md` — push to `discreteds/discreteds` |
| No pinned repos (none configured) | Recruiter sees most-recent-push, which may be noise | Pin 4–6 curated — see §4 |
| 17 public repos, many 2–3 yr old, zero stars | "Graveyard of abandoned half-projects" red flag (WPRiders, Anti-pattern) | Archive / privatise dead ones — see §7 |
| Active contribution graph (fresh commits) | Good signal | Keep doing what you're doing |
| No public org membership visible | Can't connect you to `hiivmind` / `mountainash-io` | **Make yourself a public member of each org — single highest-ROI fix** |
| No bio visible on profile | Empty bio = noise | Add: "Data Scientist & Founder. 24 yrs ML / credit risk. Building Mountain Ash + Hiivmind." |
| Location empty | Recruiters filter by location in sourcing tools | Set to "Melbourne, Australia" |
| Email not in profile (only in README) | Recruiters use email as dedupe key | Expose email in profile settings |

---

## 3. Profile README — what to keep and what to refine

Your draft in `github-profile-README.md` already hits the 2026 best-practice structure: hero → current ventures → journey → skills table → featured projects → contact. Two refinements based on the research:

1. **Drop the Kaggle "21st globally" line from Summary to a Credentials block.** It's a massive signal but reads boastful in paragraph form. Put it next to the LinkedIn/Kaggle badges where recruiters scan credentials.
2. **Add a "Currently working on" section** with 2–3 bullets of active projects (Codeboards 2026 guide; DEV Community). Recruiters want *active* more than *impressive*. Suggestion:
   - 🟢 `hiivmind-corpus` — persistent LLM context management (Claude Code plugin)
   - 🟢 `mountainash` — universal Python dataframe library, v0.x
   - 🟢 Solstice Health — pre-seed health AI platform

Do NOT add: animated typing effects, visitor counters, GitHub Trophy, Spotify-now-playing widgets. Multiple 2026 sources explicitly cite these as "unserious" markers for senior candidates.

---

## 4. Pinned repos — highest-leverage real estate

You get 6 slots. Per HireResume, 68% of recruiters say this is the single biggest factor. Recommended mix for your positioning (senior DS + AI tooling + consulting):

| Slot | Repo | Org / owner | Why |
| --- | --- | --- | --- |
| 1 | `mountainash` | mountainash-io | Flagship Python library — anchors "regulatory pipelines" CV claim |
| 2 | `hiivmind-corpus` | hiivmind | Active LLM-tooling — direct Outlier-relevant signal |
| 3 | `claudecode-pseudocode` | hiivmind | Distinctive, shows LLM internals expertise |
| 4 | `hiivmind-pulse-gh` | hiivmind | GitHub automation + Claude Code — shows breadth |
| 5 | `parkrun-scraper-sdk` | discreteds | Only repo with a fork — shows something built, consumed |
| 6 | `fairgo-journeys` | discreteds | Consumer-facing product work |

**How to pin cross-org repos:** you can only pin from your own account's repos. Workaround: fork each org repo to your personal account *purely for pinning*, or use the profile README "Highlighted Projects" list (already done) as the substitute — that's what most senior founders do.

**Remove from pin consideration:** any `-25WOL`, `-public`, or `.github` meta-repos; anything not pushed in 12+ months; anything without a README.

---

## 5. Contribution graph — what it actually signals

Starfolio's eye-tracking research: **92% of recruiters look at the graph within the first 10 seconds**. But:

| Pattern | Interpretation |
| --- | --- |
| Consistent, moderate daily activity | ✅ "Professional, disciplined" |
| Sporadic intense bursts | ⚠️ "Hobbyist or burnout risk" |
| Suspiciously perfect (every day green) | ❌ "Gaming the system" |
| Long gap with recent burst | ❌ "Resume-oriented" |
| Mostly empty | ❌ Red flag even if you code in private |

**Your graph is healthy** — active pushes across multiple repos this month. Don't try to improve it. Specifically **don't** use commit-automation tools or empty README-tweak commits; both are detectable and flag you as a gamer (Starfolio, Hire Resume, Zumo Talent).

**If you work on private/client repos:** enable "private contributions" visibility in settings (no code exposed, but squares fill in) — addresses the false-negative "stopped coding" read.

---

## 6. Repository README — the 7-part template recruiters expect

For each pinned repo, the 2026-consensus structure (HireResume, Unicorn Platform, Zumo) is:

```
# Project Name
One-line description of what it does and who it's for.

[Optional: screenshot / GIF / badges for build-status, license]

## Problem / motivation
2–3 sentences. Why does this exist?

## Quick start
$ install / run commands that work

## Architecture / design choices
High-level diagram or bullet list. Trade-offs you made.

## Features
- ...

## Tech stack
Languages, frameworks, infra.

## Status & limitations
Known issues, planned improvements. (Signals self-awareness.)

## License
```

**What NOT to include:** TODO sections of unfinished work (looks abandoned); 15+ badges (noise); animated GIFs on code-only projects.

**For `mountainash`**, add a problem statement tying it to regulatory-compliance pipelines. That single edit turns it from "yet another dataframe lib" into evidence for your CV claim.

---

## 7. Red-flag audit across your public footprint

Common disqualifiers and whether they apply to you:

| Red flag | Status for you | Action |
| --- | --- | --- |
| Empty / missing profile README | Currently empty | Push draft to `discreteds/discreteds` |
| Dead repos (no push 12+ months) | `dbt-init` (2022), `COSSPlaybook` (2023), `Large-Language-Model-Notebooks-Course` (2023), `lml_frontend_client`, `music_festival_calendars` | **Archive** (don't delete) — shows history but signals "not current" |
| Forks without contribution | `ibis`, `polars`, `Large-Language-Model-Notebooks-Course`, `prompt-eng-interactive-tutorial` | Delete or privatise — these look like credential padding |
| Repos with no README | Several `hiivmind-corpus-*` are thin | Add 3-line README minimum to each |
| Exposed secrets in history | Not verified — **audit required** | Run `gitleaks` or `trufflehog` against all public repos |
| Placeholder names (`test-`, `TODO-`, `learning-`) | None visible ✅ | — |
| Tutorial / course projects pinned | None ✅ | — |
| Vague commit messages | Not audited | Review your most-likely-to-be-clicked repos |
| Empty org `.github` profiles | hiivmind, mountainash-io, kleene-games all thin | Add 5-line org README to each |
| No public org membership | Confirmed issue | Toggle on for all 3 orgs |

---

## 8. Organisation visibility — the verification linkage

Recruiters use your org memberships as **employer proof**. Right now `hiivmind` and `mountainash-io` are unlinked from you publicly. A background-check system or diligent recruiter following your CV link will:

1. Visit `github.com/hiivmind` → see anonymous org, no public members.
2. Visit `github.com/mountainash-io` → same.
3. Fail to corroborate the CV claim that you *founded* them.

**Fixes (2 minutes each):**
- For each org, go to **Members → your row → visibility dropdown → Public**.
- Add a one-line `README.md` in each org's `.github` repo:
  - `mountainash-io`: "Mountain Ash — open-source data tooling and regulatory-compliance pipelines. Founded by Nathaniel Ramm (linkedin.com/in/nathaniel-ramm)."
  - `hiivmind`: "Hiivmind — Claude Code plugins and LLM-context tooling. Founded by Nathaniel Ramm."
  - `kleene-games`: one line or leave blank; lower priority.

---

## 9. How recruiters find you (sourcing-tool reality)

Tools actively used by tech recruiters (AmazingHiring, SeekOut, Pin, Zumo):

- **GitHub native search** — `language:python location:Melbourne followers:50..500`
- **X-ray / boolean via Google** — `site:github.com "Melbourne" "data scientist" "Python"`
- **SeekOut GitHub Search** — aggregates profile + repos + language distribution into one record
- **AmazingHiring Chrome extension** — indexes GitHub + Kaggle + Stack Overflow + LinkedIn and auto-connects identities
- **Developer signal intelligence** (LeadCognition, starfolio) — passive monitoring of *your* activity as intent signal

**What makes you findable:**

| Lever | Current state | Fix |
| --- | --- | --- |
| Location field | Empty | Set to Melbourne |
| Languages (auto-detected from repos) | Python, Shell, HTML — thin on R/SQL | Push an R project (you have history); add SQL examples |
| Followers | Unknown — likely <50 | Low priority; organic over time |
| Email visible | Currently via README only | Expose in profile |
| Full name on profile | Confirm "Nathaniel Ramm" (not nickname/handle) | Verify in settings |
| Bio | Empty | Add 1-line role + focus |
| Company field | Empty | Set to "Discrete Data Science" or "Mountain Ash" |
| Organisations visible | Private | Public membership toggle |

The AmazingHiring extension will fail to correlate your CV/LinkedIn to the GitHub footprint until the location, name, and org links are in place. That's invisible to you but meaningful for passive sourcing.

---

## 10. CV ↔ GitHub coherence (fraud-detection angle)

From the sourcing-tool survey earlier: the moment a recruiter hits "verify", they cross-reference CV claims against GitHub activity. Your CV claims in `CV-202604-optimised.md` that need github-side evidence:

| CV claim | GitHub evidence needed | Status |
| --- | --- | --- |
| Python, R, Spark, SAS | Public repos in each | ✅ Python strong; ⚠️ R thin; ❌ Spark none visible; ❌ SAS (understandable — rare OSS) |
| Founder of Mountain Ash | Public org membership + org README naming you | ❌ Fix (§8) |
| Founder of Hiivmind | Same | ❌ Fix (§8) |
| "Hands-on use of LLM coding assistants" | `claudecode-pseudocode`, `hiivmind-corpus-claude` | ✅ |
| ACRDS compliance pipelines | A repo (even stub + README) referencing ACRDS | ⚠️ None visible; consider adding |
| 24 yrs experience | GitHub joined date + LinkedIn | ✅ `discreteds` joined 2020 — age-of-account isn't a signal |
| Kaggle rank 21 | `kaggle.com/rambeaux` profile history | ✅ verifiable |

---

## 11. Prioritised action list (in order of ROI)

**Do today (15 min total):**
1. Push `github-profile-README.md` to `github.com/discreteds/discreteds` as `README.md`.
2. Toggle public membership on `hiivmind`, `mountainash-io`, `kleene-games`.
3. Fill in profile: location (Melbourne), bio (1 line), company (Discrete Data Science), email visible.

**Do this week (1–2 hrs):**
4. Pin the 4–6 repos listed in §4.
5. Add 5-line README to each org's `.github` repo, naming you as founder with LinkedIn link.
6. Archive dead repos: `dbt-init`, `COSSPlaybook`, `lml_frontend_client`, `music_festival_calendars`.
7. Delete or privatise non-contributed forks: `ibis`, `polars`, `prompt-eng-interactive-tutorial`, `Large-Language-Model-Notebooks-Course`.
8. Write a proper README for `mountainash` (problem statement → quick start → architecture → status).
9. Enable private-contribution visibility in settings.

**Do this month (4–6 hrs):**
10. Write READMEs for each pinned repo following the 7-part template in §6.
11. Run `gitleaks` across all public repos; rewrite history if secrets found.
12. Add one public R project (transplant something non-sensitive from old work).
13. Consider one merged PR to a known OSS project (even small) — recruitment research shows 35% of recruiters check this and it creates disproportionate credibility.

---

## 12. What *not* to do (2026 consensus against)

From converging research (Codeboards, Anti-pattern, DEV Community, Riem.ai):

- ❌ Animated typing effects, flashy GIFs, "visitor counter" badges — reads as junior/amateur at your seniority
- ❌ Exhaustive tech-stack badge walls — "nobody believes you're an expert in 47 technologies"
- ❌ GitHub Trophy cabinets and auto-generated stats cards beyond one basic stats block
- ❌ Commit-automation tools to keep the graph green
- ❌ Pinning forks you haven't modified
- ❌ Fun-fact / coffee emojis on a senior profile (appropriate for juniors, not for a 24-yr founder)
- ❌ Deleting old repos wholesale — archive instead, preserves history but signals "not current"
- ❌ Marketing-copy READMEs ("stunning", "revolutionary") — engineers find these cringe; it costs you on the 41% who read code

---

## Sources

- [GitHub Profile That Gets You Hired — Hire Resume](https://hireresume.ai/blogs/github-profile-that-gets-you-hired-optimization-guide) — the 150-recruiter priority ranking.
- [GitHub Recruiting: 9 Signals — Riem.ai (Mar 2026)](https://riem.ai/blog/github-recruiting-guide.html)
- [The Green Square Effect — Starfolio](https://www.starfolio.dev/blog/green-square-effect-github-activity-heatmap) — eye-tracking data on contribution graphs.
- [How to Optimise Your GitHub Profile — Git to Hire (Feb 2026)](https://gittohire.com/blog/optimize-github-profile-job-hunting-2026)
- [GitHub Profile README: Complete Guide — Codeboards (Mar 2026)](https://codeboards.io/blog/github-profile-readme-guide)
- [Showcase Projects With a GitHub Personal Page — Unicorn (Mar 2026)](https://www.unicornplatform.com/blog/showcase-your-projects-with-a-github-personal-page/)
- [8 GitHub Profile Mistakes Ruining Your Job Search — WPRiders (Mar 2026)](https://inside.wpriders.com/8-github-profile-mistakes-ruining-job-search/)
- [GitHub Recruiting — Pin](https://www.pin.com/blog/github-recruiting/) — sourcing syntax and org-membership signal.
- [How to Source Developers on GitHub — Zumo Talent (Apr 2026)](https://zumotalent.com/blog/how-to-source-developers-on-github) — 3-tier scoring framework.
- [Developer Signal Intelligence Guide — LeadCognition (Mar 2026)](https://leadcognition.io/blog/developer-signal-intelligence-guide) — how your activity is tracked for intent.
- [SeekOut GitHub Search](https://www.seekout.com/resources/release-notes/introducing-github-search-your-source-for-finding-and-qualifying-dev-talent) — how the major recruiter-side aggregator indexes you.
- [X-ray Search / AmazingHiring](https://amazinghiring.com/x-ray-search-how-to-source-using-google-and-other-platforms) — boolean / Chrome-extension sourcing.
- [Your GitHub Profile Is Your Real Resume — DEV Community (Feb 2026)](https://dev.to/sira_ai/your-github-profile-is-your-real-resume-and-most-developers-are-setting-it-up-wrong-3f44)
- [GitHub Is Your Resume Now — Anti-pattern](https://anti-pattern.com/github-is-your-resume-now)
