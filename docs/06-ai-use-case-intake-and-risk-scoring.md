# Chapter 6: AI Use Case Intake and Risk Scoring
### *Responsible AI at Design Time*

> **⚠ Reality Check — UK A-Level Grading Algorithm, 2020**
>
> In August 2020, the UK government replaced cancelled A-level exams with an algorithm to predict grades. The system downgraded 39% of teacher-predicted grades, disproportionately penalising students from state schools and lower-income areas while inflating grades at private schools. The logic was straightforward: the algorithm used historical school performance as a baseline, encoding decades of structural inequality into individual students' results. University places were lost overnight. The government reversed the decision within days after public outcry. None of this was caught at intake, because there was no structured intake. The harm ceiling was never named. The affected population was never adequately modelled.

An intake process is a structured gateway that every proposed AI use case must pass through before it enters development. Done well, it takes less than an hour and captures everything needed to assess risk, identify governance requirements, assign oversight responsibilities, and decide whether and how to proceed.

Organisations that skip this step typically discover its value the hard way: in a bias incident that reaches the press, a regulatory inquiry demanding documentation that does not exist, or a product recall that could have been prevented by asking the right questions six months earlier.


## The AI Use Case Intake Form

The intake form has six sections. It is completed by the team proposing the use case, typically the product manager or solution architect — before any development begins.


**Sections A & B — Identity and Capability**

  Section A — Use Case Identity:
- ▸  Use Case Name  ▸  Business Objective  ▸  Proposing Team  ▸  Target Users  ▸  Deployment Environment  ▸  Proposed Timeline
  Section B — AI Capability Description:
- ▸  AI Modality (LLM, classifier, recommender, vision, etc.)  ▸  Input Data Types  ▸  Output Type
- ▸  Decision Authority — binding decision, advisory recommendation, or informational output?
- ▸  Model Source — proprietary, third-party API, open-source, or fine-tuned?  ▸  Human Override — always technically possible?


**Sections C & D — Data, Privacy and Risk Identification**

  Section C — Data and Privacy:
- ▸  Personal Data Categories (including special categories: health, ethnicity, biometrics)
- ▸  Data Sources and consent documentation  ▸  Data Residency and cross-border transfer  ▸  Retention Policy  ▸  DPIA status
  Section D — Risk Identification:
- ▸  Potential Harms — realistic ways this AI could cause harm to individuals, groups, or society
- ▸  Affected Populations — who bears the risk? Any groups disproportionately exposed?
- ▸  Failure Mode Analysis — worst case if the AI produces a wrong output
- ▸  Bias Risk  ▸  Regulatory Exposure (EU AI Act, GDPR, HIPAA, FCA, etc.)  ▸  Dependency Risk


**Sections E & F — Risk Scoring and Proposed Controls**

  Section E — Risk Scoring (score each 1–3):
- ▸  Severity of Harm ___/3   ▸  Scale of Impact ___/3   ▸  Reversibility ___/3   ▸  Human Autonomy ___/3
- ▸  TOTAL ___/12   →   🟢 Tier 1 (4–5)   🟡 Tier 2 (6–7)   🟠 Tier 3 (8–10)   🔴 Tier 4 (11–12)
- ▸  ⚠️  Severity score of 3 = automatic minimum Tier 3, regardless of total.
  Section F — Proposed Controls:
- ▸  HITL Model  ▸  Moderation Approach  ▸  Bias Mitigation Plan
- ▸  Explainability Plan  ▸  Incident Response Plan  ▸  Named Accountable Owner


## Governance Gates

The intake form feeds into a governance gate: a structured decision point that routes each use case to the appropriate level of review based on its risk tier.


| Tier — Gate | Reviewers Required  |  Possible Outcomes |
|---|---|
| 🟢 Tier 1 Standard Review | Engineering lead + PM  /  Approve / Approve with conditions / Return for revision |
| 🟡 Tier 2 Enhanced Review | Engineering lead + PM + Privacy/legal  /  Approve / Conditions / Return / Escalate |
| 🟠 Tier 3 Ethics Review | RAI team + Legal + Compliance + Senior product leadership  /  Approve / Conditional / Reject / Escalate |
| 🔴 Tier 4 Executive Review | C-suite + External audit + Regulatory notification if required  /  Approve with full controls / Reject / Regulatory submission |


**Gate decisions must be:**

- ▸  Documented — every outcome recorded with rationale
- ▸  Signed — by the appropriate reviewer for the tier
- ▸  Retained — for the life of the AI system plus the applicable regulatory retention period
- ▸  Enforced — a conditional approval that was never fulfilled is a governance failure


## Worked Examples

Three examples showing how the intake and scoring process works in practice:


**Example 1 — Automated Loan Pre-Screening (Finance)**

  Key risks: discriminatory pre-screening based on language correlated with protected characteristics. Regulatory exposure: FCA, ECOA, GDPR.
  Scoring: Severity 3  •  Scale 2  •  Reversibility 2  •  Autonomy 2  =  9  →  🟠 Tier 3
  Gate outcome: Ethics Review. Mandatory bias testing. Human underwriter reviews every output. Explainability required for declined recommendations.


**Example 2 — Clinical Documentation Assistant (Healthcare)**

  Key risks: inaccurate clinical notes leading to wrong treatment; privacy breach of sensitive health conversations. Regulatory exposure: HIPAA, EU AI Act (High-Risk).
  Scoring: Severity 3  •  Scale 2  •  Reversibility 2  •  Autonomy 1  =  8  →  🟠 Tier 3
  Gate outcome: Ethics Review. Physician must review and sign every note before it enters the clinical record. Hallucination testing mandatory.


**Example 3 — Internal HR FAQ Bot (Corporate)**

  Key risks: incorrect policy information causing employees to make wrong decisions. Regulatory exposure: employment law accuracy only.
  Scoring: Severity 1  •  Scale 2  •  Reversibility 3  •  Autonomy 1  =  7  →  🟡 Tier 2
  Gate outcome: Enhanced Review. User disclosure required. Human HR contact always available. Quarterly accuracy audit against current policy documents.


**Chapter Takeaway**

1. Intake is the highest-leverage governance intervention; it costs an hour but prevents months of rework and harms that rework cannot undo.
2. The six-section form captures identity, capability, data, risk, scoring, and proposed controls: everything governance reviewers need in one place.
3. Each tier routes to a proportionate gate: Standard Review (Tier 1) through Executive Review with possible regulatory notification (Tier 4).
4. Gate decisions must be documented, signed, and retained. A conditional approval never fulfilled is a governance failure waiting to surface.
5. Intake is not one-time — resubmit when scope expands, the model changes, the population grows, or the deployment context shifts.
6. Chapters 1–6 have been about building responsibility in at design time. From here, the book shifts to the other half of the discipline: enforcing it at runtime, every day, at scale.
