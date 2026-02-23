# Responsible AI in Practice: From Intake to Incident

**A practitioner's handbook for engineers, product managers, data scientists, and compliance leads building AI systems that are ethical, safe, accountable, and trustworthy.**

*By Divya Akula — Version 1.0, February 2026*

---

## 📥 Download

**[⬇ Download the full book (DOCX)](./output/Responsible_AI_in_Practice_Divya_Akula_v1.docx)**

---

## About This Book

Responsible AI in Practice is not a book about principles. It is a book about practice.

The frameworks are published. The harms are documented. The principles are well understood. And yet organisation after organisation builds AI systems that cause harm — not out of malice, but because nobody operationalised the discipline at the right moment, in the right place, with the right accountability.

This book is for the people who have to make responsible AI real: engineers deciding how to architect a moderation layer, product managers completing a risk assessment before a sprint review, compliance leads explaining to a regulator why their governance process is adequate, and data scientists who suspect their training data has a problem but do not yet have the vocabulary to name it.

It covers the full responsible AI lifecycle — from design-time risk scoring through runtime moderation, epistemic safety, incident handling, continuous monitoring, and the emerging challenge of agentic systems — and does so with the specificity that practitioners need.

---

## 📖 Read Online

Each chapter is available as a Markdown file for reading directly in the browser:

| # | Chapter | Description |
|---|---------|-------------|
| — | [To the Reader](./docs/00-to-the-reader.md) | Foreword — who this book is for and how to use it |
| 1 | [The Case for Responsible AI](./docs/01-the-case-for-responsible-ai.md) | Why responsibility cannot be optional |
| 2 | [Responsible AI Frameworks](./docs/02-responsible-ai-frameworks.md) | Microsoft, Google, OECD, EU, UNESCO, NIST — a practitioner's view |
| 3 | [The Responsible AI Lifecycle](./docs/03-the-responsible-ai-lifecycle.md) | Seven stages from ideation to decommissioning |
| 4 | [Risk Tiering for AI Use Cases](./docs/04-risk-tiering-for-ai-use-cases.md) | Calibrating governance to harm potential |
| 5 | [Human-in-the-Loop](./docs/05-human-in-the-loop.md) | Enforcing meaningful human accountability |
| 6 | [AI Use Case Intake and Risk Scoring](./docs/06-ai-use-case-intake-and-risk-scoring.md) | The governance gate that changes everything |
| 7 | [Moderation as Middleware](./docs/07-moderation-as-middleware.md) | Enforcing responsible AI at runtime |
| 8 | [Grounded AI](./docs/08-grounded-ai.md) | Evidence, epistemic safety, and trustworthy outputs |
| 9 | [Incident Handling](./docs/09-incident-handling.md) | Detecting and responding to silent failures |
| 10 | [Monitoring, Audits, and Continuous Improvement](./docs/10-monitoring-audits-and-continuous-improvement.md) | The discipline that keeps systems safe over time |
| 11 | [Operationalizing Responsible AI](./docs/11-operationalizing-responsible-ai-across-the-organization.md) | Building the function, embedding the culture |
| 12 | [The Future](./docs/12-the-future.md) | Governing intelligent and agentic systems |

---

## What Makes This Book Different

**It starts with failure.** Every chapter opens with a Reality Check — a real, documented incident that proves the chapter's point before the theory begins. Amazon's recruiting bias. The Dutch childcare scandal. IBM Watson's unsafe cancer recommendations. Cruise's robotaxi dragging a pedestrian. These are not cautionary tales from a safely distant past.

**It is lifecycle-oriented.** Most RAI content addresses one layer — moderation, or bias, or governance. This book follows the full arc, from the first design decision to the last decommissioning log.

**It names the illusions.** The Five Illusions of Responsible AI (Chapter 11) identifies the governance patterns that feel like safety but provide none: the dashboard without enforcement, the human-in-the-loop without friction, the policy without monitoring, the compliance without consequence, the ethics committee without authority.

**It is opinionated.** This book does not present every possible view. It makes recommendations. It names what fails and why. It gives practitioners something to act on.

---

## Repository Structure

```
responsible-ai-in-practice/
├── README.md                  — This file
├── LICENSE                    — CC BY-NC-ND 4.0
├── CHANGELOG.md               — Version history
├── output/
│   └── Responsible_AI_in_Practice_Divya_Akula_v1.docx
└── docs/
    ├── 00-to-the-reader.md
    ├── 01-the-case-for-responsible-ai.md
    ├── 02-responsible-ai-frameworks.md
    ├── 03-the-responsible-ai-lifecycle.md
    ├── 04-risk-tiering-for-ai-use-cases.md
    ├── 05-human-in-the-loop.md
    ├── 06-ai-use-case-intake-and-risk-scoring.md
    ├── 07-moderation-as-middleware.md
    ├── 08-grounded-ai.md
    ├── 09-incident-handling.md
    ├── 10-monitoring-audits-and-continuous-improvement.md
    ├── 11-operationalizing-responsible-ai-across-the-organization.md
    └── 12-the-future.md
```

---

## Licence

This work is licensed under [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)](./LICENSE).

**You are free to:**
- Share — copy and redistribute the material in any medium or format

**Under the following terms:**
- **Attribution** — You must give appropriate credit to Divya Akula and link to this repository
- **NonCommercial** — You may not use the material for commercial purposes
- **NoDerivatives** — You may not remix, transform, or build upon the material

© 2026 Divya Akula. All rights reserved.

---

## Citation

If you reference this work, please cite it as:

> Akula, D. (2026). *Responsible AI in Practice: From Intake to Incident* (Version 1.0). Retrieved from https://github.com/[your-username]/responsible-ai-in-practice

---

## Feedback and Contact

This is Version 1.0. A second version is planned with expanded coverage of epistemic safety, implementation artifacts, and an organisational maturity model.

If you find errors, have suggestions, or want to share how you have used this book, please open an issue in this repository.
