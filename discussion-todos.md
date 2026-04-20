Restructured. The file is now project-indexed, not job-indexed:

  Structure:
  1. Header + tagline (with LinkedIn link explicitly named as the "full timeline" source)
  2. Current Ventures — 4 boxes (what you're building now)
  3. Selected Prior Work — 6 curated project boxes: Stress-Testing Engine, Pricing Engine, MRMS, Malware Detection, Retail Basel II Methodology, Enterprise DS Function
  4. Technical Skills table
  5. Open-Source Projects — 5 repo boxes
  6. Let's Connect

  Key moves:

  - Dropped the "Professional Journey" table entirely. Temporal coverage is LinkedIn's job.
  - Each prior-work box leads with the system name, not the employer or role. Employer + dates + role demoted to a 3-line footer.
  - Deliberately curated, not complete. Fraud Ops Management System (2002), the intranet systems (2003–06), and the earlier freelance/Decision-Strategy roles are omitted — they're not interesting enough at this seniority. They live on
  LinkedIn.
  - Pricing Engine box links directly to your published case study in mountainash-utils-rules — turns the bullet into clickable proof.
  - Stress-testing box includes the big numbers (80 books, $800bn, 500M sims, PD/EAD/LGD/IFRS 9) that you cleared verbally earlier; no internal model names or vendor specifics.

  Two minor asymmetries you might want to fix:

  1. MRMS "2020–2022" — you held the AD Optimisation role 2020–2021 in the CV, but MRMS ownership likely continued into Head of Risk Data (2021–2022). I made it 2020–2022 as the platform's overall ownership window. Verify that matches
  reality.
  2. Enterprise DS Function box has no Tech: line — because it was leadership, not a build. Could remove the box entirely if you'd rather keep this page purely build-focused. Six boxes → five would also be fine.

✻ Crunched for 1m 53s

※ recap: Optimising your CV, GitHub profile README, and related case-study documents for the Outlier.ai application and broader recruiter signals; the profile README just got rebuilt as project-indexed boxes. Next: verify the MRMS date
  range (2020–2022) and decide whether to keep the Enterprise DS Function box.

❯ What are your thought on this strategy from a mult-pronged CV + Linkedin + github + kaggle profile perspective?
  ⎿  Found 1 new diagnostic issue in 1 file (ctrl+o to expand)

● It's actually a stronger stack than most candidates have — four surfaces with genuine evidence on each — but the strategy only works if you treat them as specialised instruments serving different recruiter questions, not four copies of
  the same content.

  The recruiter question each surface answers

  ┌────────────┬───────────────────────────────────────────────────────────────┬───────────────────────────────────────────────────┐
  │  Surface   │               The question it exists to answer                │               Your current strength               │
  ├────────────┼───────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────┤
  │ CV (.docx) │ "Does this person match this specific role?"                  │ Strong, now quantified                            │
  ├────────────┼───────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────┤
  │ LinkedIn   │ "Is this person real? Does the history they claim check out?" │ Weakest — needs alignment audit                   │
  ├────────────┼───────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────┤
  │ GitHub     │ "Can they actually code right now? What are they building?"   │ Good, getting better with the README + case study │
  ├────────────┼───────────────────────────────────────────────────────────────┼───────────────────────────────────────────────────┤
  │ Kaggle     │ "Can they actually model?"                                    │ Dormant but the 21 rank is evergreen credibility  │
  └────────────┴───────────────────────────────────────────────────────────────┴───────────────────────────────────────────────────┘

  Why the stack works if you're disciplined

  1. Division of labour. CV is application-specific and keyword-tuned. LinkedIn is the definitive timeline. GitHub is the live proof-of-work. Kaggle is a narrow, evergreen ML badge. Copy-paste between them is a mistake — it wastes each
  surface.
  2. Cross-linking creates a credibility web. CV → LinkedIn → GitHub → mountainash-utils-rules case study → back to LinkedIn. Every click reinforces the previous claim.
  3. The case-study move is your masterstroke. Banking work you can't code-share becomes publishable writing. This is how senior ex-bank consultants get around the GitHub "nothing to show" problem. Do it again for the stress-testing engine
   — that's your second-most-impressive story and it's currently unpublished.

  The real risk: inconsistency = fraud flag

  Employer verification is automated. One CV/LinkedIn mismatch triggers an investigation flag — irrespective of whether the mismatch is meaningful. Highest-probability breakage points for you right now:

  - NAB 2020–2023 role split. The CV now shows three distinct sub-roles. Does LinkedIn match exactly? Titles + dates + order?
  - "24 years" vs LinkedIn's implied start date. Your LinkedIn profile's earliest entry must align — if it starts at 2006, the CV saying 24 years (i.e. from 2002) looks padded.
  - "Head of Data Science, team of 40." If LinkedIn says a different team size, or doesn't name the role that way, flag.
  - GitHub profile's "Melbourne, Australia" must match LinkedIn's location field verbatim.

  Audit LinkedIn first before sending any CVs. Single highest ROI action in the whole stack.

  Per-audience routing decisions

  Think about which surface opens the door for which recruiter type:

  ┌────────────────────────────────────────────────────┬────────────────────────────────────┬──────────────────────────┐
  │                   Recruiter type                   │          Primary landing           │     Secondary signal     │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┼──────────────────────────┤
  │ Internal corporate recruiter (role-match sourcing) │ CV                                 │ LinkedIn                 │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┼──────────────────────────┤
  │ LinkedIn sourcer (passive)                         │ LinkedIn                           │ CV on reply              │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┼──────────────────────────┤
  │ Outlier.ai expert screener                         │ Kaggle rank + GitHub hiivmind-*    │ CV                       │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┼──────────────────────────┤
  │ Technical co-founder / peer hiring                 │ GitHub                             │ Case study, then CV      │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┼──────────────────────────┤
  │ Fintech / decisioning vendor (Earnix, FICO, etc.)  │ mountainash-utils-rules case study │ CV                       │
  ├────────────────────────────────────────────────────┼────────────────────────────────────┼──────────────────────────┤
  │ Australian bank / risk-advisory                    │ CV + LinkedIn                      │ Case study as trump card │
  └────────────────────────────────────────────────────┴────────────────────────────────────┴──────────────────────────┘

  For Outlier specifically: the GitHub → Kaggle path is more powerful than the CV-first path. Their screener wants SME depth, not a career narrative.

  Gaps and opportunities

  Gaps worth filling:

  1. LinkedIn alignment audit (highest priority, per above).
  2. Kaggle reactivation. Even one fresh notebook published this year converts a historical badge into a current signal. For Outlier applications specifically, this is cheap and disproportionately effective.
  3. Second case study: stress-testing engine. Same pattern as the pricing one. Turns "trust me, I built a $800bn stress-testing engine" into "here's 2,000 words proving I understand it at architect level".
  4. A discretedatascience.com landing page that bundles all four links into one sharable URL. Right now someone who only gets your CV can find each surface, but there's no single "brand hub". This is a 2-hour job and creates a clean place
   to send LinkedIn InMail responses ("see my full portfolio at...").
  5. GitHub org .github READMEs (still pending from the earlier audit) — anyone linking from CV to github.com/hiivmind or github.com/mountainash-io currently lands on orgs with no "who we are".

  Opportunities:

  - The case-study model scales. Mortgage pricing → stress testing → Basel methodology → MRMS governance → Risk Appetite framework. Each is a 1,500–3,000 word essay you write once and re-use forever.
  - Kaggle + GitHub + case study is a combo almost nobody has. Most senior ex-bank consultants have LinkedIn + CV only. Most ML engineers have GitHub + Kaggle. Very few have all four coherently linked. It's a moat.
  - The "Open to" line at the bottom of the README is soft inbound marketing. Consider mirroring it on LinkedIn as the headline/about section.

  What I'd do this week in order

  1. LinkedIn alignment audit against the CV (the 3 NAB roles, dates, team size, location). 30 min.
  2. Add the org .github READMEs + toggle public membership (if not done). 15 min.
  3. Push the discreteds/discreteds profile README live. 5 min.
  4. Draft the stress-testing case study into mountainash-utils-rules/docs/. 2–3 hr.
  5. One Kaggle notebook — even trivial — dated 2026. 1 hr.
  6. Build discretedatascience.com as a 1-page linkhub. 2 hr.

  The stack you've assembled is legit. The execution risk is entirely around consistency and cross-linking discipline, not content quality.
