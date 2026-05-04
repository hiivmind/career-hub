# Customization Protocol: Per-Job Tailoring Workflow

## Why Customization Matters

**The reality**: 75% of resumes are rejected by ATS before human review. Generic CVs fail screening at higher rates than customized ones.

**The payoff**: 15-20 minutes of customization per job can move your CV from automated rejection to human review.

## Static vs. Dynamic Sections

### Static Sections (Create Once, Reuse)

These remain consistent across applications:
- Education
- Certifications/Licenses
- Basic contact information
- General technical skills
- Basic work history dates and titles

### Dynamic Sections (Customize Per Application)

These change based on job requirements:
- Professional Summary
- Core Competencies (reorder by relevance)
- Achievement bullets (reorder; add/remove based on job fit)
- Keyword emphasis

## Pre-Customization: Job Analysis

Before tailoring your CV, analyze the job posting systematically:

### Step 1: Extract Keywords (15-25 terms)

Scan the job description for:
- **Repeated terms** appearing 2+ times
- **Hard skills** (tools, languages, frameworks, methodologies)
- **Soft skills** (leadership, communication, cross-functional collaboration, etc.)
- **Domain jargon** specific to the industry or role
- **Job titles or role designations** mentioned

Create a keyword list ranked by frequency and relevance.

**Example extraction from a Data Engineer job posting**:
```
High priority: Python, Apache Spark, SQL, AWS Redshift, ETL Pipelines, Data Warehousing
Medium priority: Docker, Kubernetes, Apache Airflow, CI/CD, Data Modeling
Lower priority: Project leadership, Mentorship, Cross-functional collaboration
```

### Step 2: Identify Role Priorities

- What's the primary responsibility? (Infrastructure? Analytics? Feature delivery?)
- What technical depth is required? (Entry-level? Senior/Staff?)
- What's the team structure? (Individual contributor? Leadership? Mentorship?)
- What business context matters? (Revenue impact? Scale? User-facing? Internal tools?)

### Step 3: Extract Success Metrics

What outcomes matter most to this role?
- Performance/speed improvements?
- Cost reduction?
- Reliability/uptime?
- User impact?
- Team development?

## Customization Workflow Per Application

### Time Investment: 15-20 minutes

### Workflow Steps

#### 1. Create a Job-Specific Copy

Start with your master CV and create a copy named `CV_[Company]_[Role].docx`

#### 2. Rewrite Professional Summary

Update the summary to mirror job description language and priorities.

**Template**:
```
[Years of experience] professional in [domain/role] with proven expertise in [3 key skills 
from job description]. Track record of [quantifiable achievement matching job priorities]. 
Seeking [target role] to [how you'll contribute to this specific role/company].
```

**Before** (generic):
```
Senior Software Engineer with 8+ years building scalable systems. Experienced in multiple 
programming languages and cloud platforms. Seeking challenging technical roles.
```

**After** (customized for job posting emphasizing distributed systems, Python, AWS):
```
Senior Software Engineer with 8+ years designing and deploying distributed systems on AWS. 
Reduced data processing latency by 58% through architecture optimization and Python-based 
pipelines. Seeking Senior Engineer role to lead infrastructure decisions for high-scale systems.
```

**Why it works**:
- Keywords (AWS, Python, distributed systems, architecture) appear in first 2 lines
- Quantified proof (58%) signals impact
- Direct alignment with job posting priorities
- Verifiable claims with specific methodologies

#### 3. Reorder Core Competencies

Reorganize skills section to match job posting priorities.

**Before** (generic order):
```
CORE COMPETENCIES
Python | Java | Kubernetes | AWS | SQL | Docker | React | TypeScript | System Design | Leadership
```

**After** (reordered for Data Engineer role emphasizing Python, Spark, SQL, AWS):
```
CORE COMPETENCIES
Python | Apache Spark | SQL | AWS Redshift | Data Warehousing | ETL Pipelines | 
Apache Airflow | Docker | Data Modeling | CI/CD Pipelines | Project Leadership
```

**Logic**: Keywords from job description appear first and in matching order.

#### 4. Reorder Professional Experience Bullets

Reorganize achievement bullets under each role to emphasize relevant accomplishments.

**Strategy**:
- Move most relevant achievements to the top of each role
- Emphasize achievements matching job posting priorities
- De-emphasize unrelated accomplishments

**Example for Data Engineer role**:

**Generic order** (emphasis on all achievements equally):
```
Senior Data Engineer | DataCorp Inc. | January 2021 – Present

• Mentored 4 junior engineers on Python best practices
• Built data ingestion pipelines processing 500M+ events daily
• Implemented CI/CD pipeline reducing deployment time by 72%
• Optimized SQL queries reducing execution time by 64%
```

**Customized order** (for job emphasizing ETL, data warehousing, optimization):
```
Senior Data Engineer | DataCorp Inc. | January 2021 – Present

• Redesigned ETL pipeline architecture consolidating 12 jobs into 3 Airflow workflows, 
  reducing processing time by 58% and saving $180K annually
• Optimized SQL queries on 15 critical reports, reducing execution time by 64% on average 
  and lowering database load by 40%
• Implemented CI/CD pipeline using Docker and GitHub Actions, reducing deployment cycle 
  by 72% (from 6 hours to 100 minutes)
• Mentored 4 junior engineers on Python best practices and data engineering, resulting in 
  2 promotions within 18 months
```

**Why first order is stronger here**: ETL/data warehouse achievements (job priorities) are highlighted first.

#### 5. Add/Remove Bullets Based on Job Fit

Consider adding or removing bullets to emphasize job-specific accomplishments.

**When to add**:
- You have relevant achievements not currently listed
- Job description emphasizes an area where you have strong proof points
- Achievement addresses specific requirements mentioned in job posting

**When to remove**:
- Bullet emphasizes skill not mentioned in job posting
- Space is limited (approaching 2 pages)
- Achievement is less impressive than alternatives

**Example decision logic**:
- Job posting emphasizes "mentorship and team development" → Add mentorship bullets
- Job posting emphasizes "startup environments" → Add startup/fast-growth bullets
- Job posting emphasizes "regulatory compliance" → Highlight compliance achievements

#### 6. Verify Keyword Coverage

Cross-check your customized CV against the job description:

**Checklist**:
```
☐ Professional Summary includes 3-5 top keywords from job posting
☐ Core Competencies section includes 8-12 keywords from job description
☐ Achievement bullets across all roles include 5-7 additional keywords naturally
☐ Keywords appear in multiple places (summary + competencies + achievements)
☐ Keyword integration feels natural (not keyword-stuffed)
☐ Technical depth matches job posting level
☐ No new claims added that you can't defend in an interview
```

#### 7. Consistency Check

Before submission, verify:

**Verification checklist**:
```
☐ Job title/company names match LinkedIn profile exactly
☐ Dates are consistent across CV and LinkedIn
☐ Skills listed in Core Competencies appear in achievement bullets
☐ No typos or formatting inconsistencies
☐ All sentences are grammatically correct
☐ Date format is consistent throughout
☐ Achievement bullets are in logical order (reverse chronological or impact-based)
☐ Contact information is current and professional
```

#### 8. Optional: ATS Testing

Use free ATS scanning tools to verify keyword match:
- **Jobscan** (jobscan.co) — Compare CV to job posting, get match score
- **Rezi** (rezi.ai) — Free resume scanner with keyword analysis
- **Resumeworded** — Identifies weak achievement bullets

**How to use**:
1. Paste job description into tool
2. Upload customized CV
3. Tool highlights missing keywords or weak bullets
4. Revise based on feedback; re-scan until 70%+ match

## Customization Tracking

Keep a record of customizations:

```
[Company] | [Role] | [Date Applied] | [Key Customizations]
Company A | Senior Engineer | 2025-01-15 | Added Kubernetes bullets; reordered skills for microservices focus
Company B | Data Engineer | 2025-01-18 | Emphasized ETL and cost optimization; added Airflow examples
Company C | Tech Lead | 2025-01-20 | Highlighted mentorship achievements; expanded leadership section
```

This helps you iterate and identify patterns in what resonates with different roles.

## The Effort-to-Reward Tradeoff

**15-20 minutes of customization** can move your CV from automatic rejection to human review.

**At scale**: 
- 10 applications × 15 minutes = 2.5 hours total
- Typical improvement: 30-40% increase in interview requests for comparable roles

The ROI is strong. Don't send generic CVs to competitive roles.
