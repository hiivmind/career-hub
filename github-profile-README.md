# Nathaniel Ramm | Data Scientist, Software Engineer, Founder

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/nathaniel-ramm)
[![Kaggle](https://img.shields.io/badge/Kaggle-rambeaux-20BEFF?style=for-the-badge&logo=kaggle)](https://kaggle.com/rambeaux)
[![Email](https://img.shields.io/badge/Email-Contact-red?style=for-the-badge&logo=protonmail)](mailto:nathaniel@mountainash.io)

> Melbourne, Australia. 24 years building predictive models, credit-risk systems, and analytical software. Former Head of Data Science at NAB. Formerly ranked 21st globally on Kaggle. Full career timeline on [LinkedIn](https://linkedin.com/in/nathaniel-ramm).

## Current Ventures

```
┌────────────────────────────────────────────────────────────┐
│ Mountain Ash                               2023 - Present  │
└────────────────────────────────────────────────────────────┘
  Founder, Lead Architect

  • Open-source Python data tooling and rules engine
  • Regulatory-compliance pipelines for consumer-lending businesses
  • Automation of Australian Credit Reporting Data Standards (ACRDS)
  • Advisory on credit-portfolio stress-testing and SAS-to-Python migrations

  https://mountainash.io
  https://github.com/mountainash-io
```

```
┌────────────────────────────────────────────────────────────┐
│ Hiivmind                                   2024 - Present  │
└────────────────────────────────────────────────────────────┘
  Founder, Lead Developer

  • Claude Code plugins and skills for AI-assisted engineering
  • Persistent, curated documentation corpora for LLM context
  • MCP servers, agentic workflows, pseudocode reverse-engineering
  • Cross-platform CLI plugins for GitHub automation, data, and infra

  https://github.com/hiivmind
```

```
┌────────────────────────────────────────────────────────────┐
│ Solstice Health  (pre-seed)                2024 - Present  │
└────────────────────────────────────────────────────────────┘
  Lead Developer and Architect

  • Personalised health-data aggregation and AI platform
  • Focused on perimenopausal women's health analytics
```

```
┌────────────────────────────────────────────────────────────┐
│ FairGo  (fairgo.app)                       2024 - Present  │
└────────────────────────────────────────────────────────────┘
  Lead Developer

  • Zero-friction expense-splitting web app
  • AI-assisted sharing workflows

  https://github.com/discreteds/fairgo-journeys
```

## Selected Prior Work

Systems, engines, and analytical platforms built across two decades in banking and consulting. Curated, not exhaustive — selected for technical or commercial interest.

```
┌────────────────────────────────────────────────────────────┐
│ Whole-of-Bank Credit Stress-Testing Engine                 │
└────────────────────────────────────────────────────────────┘
  APRA ICAAP stress-testing engine for a Big-4 Australian bank.
  Retail, non-retail, wholesale, sovereign, and international
  credit books — ~80 portfolios, $800bn+ in exposures.

  • Account-level Monte-Carlo simulation (~500M simulation records)
  • All regulatory credit models stressed: PD, EAD, LGD, IFRS 9
  • Macro-economic scenarios translated directly to model stress settings
  • Re-engineered legacy SAS process (2 weeks on dedicated server) into
    a 2-hour R + Spark + Parquet pipeline running on commodity hardware
  • Modular, service-oriented, cloud-deployable architecture

  Tech: R, Spark, Parquet, PyArrow, SAS (legacy)
  Context: NAB, via Discrete Data Science, 2013-2020
  Role: Lead architect and developer
```

```
┌────────────────────────────────────────────────────────────┐
│ Home Lending Pricing Rules Engine                          │
└────────────────────────────────────────────────────────────┘
  Mortgage pricing rules engine for a Big-4 Australian bank's
  home-lending book: ~$500bn portfolio, ~10k applications per week,
  ~200 mortgage products.

  • Replaced Excel-driven process; rule-team approvals reached banker
    terminals in under 1 hour, with a full per-quote audit trail
  • ~2,000 logical rules covering the full pricing hierarchy:
    base rates, risk adjustments, customer/channel overlays, and
    multi-level banker/desk discretion
  • ~250,000× compression vs the ~500M-rule physical enumeration
    required by the replacement vendor system (FICO)
  • Ran unattended for 2 years with zero architectural rewrites

  Tech: T-SQL, SQL Server, web rule-management UI
  Context: NAB, via Discrete Data Science
  Role: Lead architect and developer

  Case study: https://github.com/mountainash-io/mountainash-utils-rules/blob/main/docs/superpowers/specs/2026-04-07-big-4-pricing-engine-case-study.md
```

```
┌────────────────────────────────────────────────────────────┐
│ MRMS — Model Risk Management System                        │
└────────────────────────────────────────────────────────────┘
  Bank-wide model-governance platform covering >4,000 predictive
  models across credit, market, operational, and strategic domains.

  • Datalake + R-based reporting framework for modellers,
    validators, and model owners
  • Integrated into model-lifecycle, validation, and audit workflows
  • Business ownership and maintenance of the system

  Tech: R, Shiny, Parquet, Teradata, SQL Server
  Context: NAB, 2020-2022
  Role: Associate Director, Optimisation (Model Risk)
```

```
┌────────────────────────────────────────────────────────────┐
│ Internet Banking Malware Detection                         │
└────────────────────────────────────────────────────────────┘
  Machine-learning and analytics framework for malware detection
  in Internet Banking transactional and login data.

  • Feature engineering from clickstream, login, and device signals
  • Anomaly and behavioural detection models
  • Production scoring pipeline and investigator-facing dashboards

  Tech: Python, Spark, Tableau
  Context: NAB, via Discrete Data Science
  Role: Lead data scientist
```

```
┌────────────────────────────────────────────────────────────┐
│ Retail Basel II Methodology Programme                      │
└────────────────────────────────────────────────────────────┘
  Multi-year programme building and maintaining the analytical
  foundations of NAB's retail Basel II IRB approach.

  • Through-the-Cycle PD modelling methodology for new-generation
    mortgage PD models (PoC lead architect)
  • Basel II Expected Loss Stress Testing methodology (PoC)
  • Risk Appetite framework linking acquisition strategies to
    Economic Capital and Expected Loss stress tests
  • Monitoring framework for all retail IRB models (PD, EAD, LGD)
    and credit scorecards
  • APRA annual self-assessments and internal governance deliverables

  Tech: SAS, SQL, Teradata
  Context: NAB, 2009-2013
  Role: Senior Manager, Strategic Analytics and Model Performance
```

```
┌────────────────────────────────────────────────────────────┐
│ Enterprise Data Science Function  (NAB)                    │
└────────────────────────────────────────────────────────────┘
  Centralised 40-person data-science capability delivering ML
  into retail, business, digital, and financial-crime divisions.

  • Model-lifecycle and evaluation frameworks for production ML
  • Cloud-migration and tooling uplift of legacy SAS / Teradata stack
  • Governance uplift of analytics infrastructure and delivery teams
  • Cross-divisional project scoping, delivery, and stakeholder alignment

  Context: NAB, 2022-2023
  Role: Head of Data Science
```

## Technical Skills

| Category | Tools |
| --- | --- |
| **Languages** | Python, SQL, TypeScript, Shell, R |
| **AI / LLM Engineering** | Claude Code plugin & skill development, agentic workflows, MCP servers, prompt engineering, rubric design, RAG & documentation-corpus design, LLM evaluation |
| **Modern data stack** | Polars, DuckDB, Apache Arrow / Parquet, Ibis, dbt, LanceDB (vector), pandas, pyspark |
| **ML / Statistics** | scikit-learn, gradient boosting, ensembles, neural networks, logistic regression, Monte-Carlo simulation, feature engineering, model evaluation & validation |
| **Infra & DevOps** | Azure, Fly.io, GitHub Actions, Cloudflare Workers, Docker, systemd, Linux |
| **Credit Risk (domain)** | Basel II (PD, EAD, LGD), RWA, credit scorecards, stress testing, strategy optimisation, model risk management |
| **Legacy / enterprise** | SAS, Teradata, SQL Server / SSAS, Oracle, Apache Drill, Java, PHP — deep NAB-era credit-risk analytics and model-risk governance experience |

## Open-Source Projects

```
┌────────────────────────────────────────────────────────────┐
│ mountainash                                                │
└────────────────────────────────────────────────────────────┘
  Universal Python dataframe expression and transformation library.
  Designed to underpin regulatory-compliance pipelines for
  small-to-mid lenders without enterprise platform licensing.

  https://github.com/mountainash-io/mountainash
```

```
┌────────────────────────────────────────────────────────────┐
│ hiivmind-corpus                                            │
└────────────────────────────────────────────────────────────┘
  Claude Code plugin for building persistent, curated documentation
  corpora that stay in an LLM's working context across sessions.

  https://github.com/hiivmind/hiivmind-corpus
```

```
┌────────────────────────────────────────────────────────────┐
│ claudecode-pseudocode                                      │
└────────────────────────────────────────────────────────────┘
  LMPL pseudocode specifications reconstructing Claude Code's
  internal architecture from observed behaviour.

  https://github.com/hiivmind/claudecode-pseudocode
```

```
┌────────────────────────────────────────────────────────────┐
│ hiivmind-pulse-gh                                          │
└────────────────────────────────────────────────────────────┘
  Context-enriched GitHub operations plugin for Claude Code.
  Automatic project linking, field resolution, milestone mapping.

  https://github.com/hiivmind/hiivmind-pulse-gh
```

```
┌────────────────────────────────────────────────────────────┐
│ parkrun-scraper-sdk                                        │
└────────────────────────────────────────────────────────────┘
  Python SDK for Parkrun data. Event results, athlete history,
  and venue metadata scraping.

  https://github.com/discreteds/parkrun-scraper-sdk
```

## Let's Connect

- LinkedIn: [nathaniel-ramm](https://linkedin.com/in/nathaniel-ramm)
- Email: [nathaniel@mountainash.io](mailto:nathaniel@mountainash.io)
- Kaggle: [rambeaux](https://kaggle.com/rambeaux)

Open to: AI-training and LLM-evaluation freelance work, credit-risk and model-governance advisory, and selective data-science consulting engagements.
