# Chapter 4: Risk Tiering for AI Use Cases
### *Not All AI Is Equal*

> **⚠ Reality Check — Uber Self-Driving Fatality, Tempe Arizona, 2018**
>
> On 18 March 2018, an Uber autonomous vehicle struck and killed Elaine Herzberg as she crossed a road in Tempe, Arizona. Investigators found the system had detected her six seconds before impact but classified her as an 'unknown object', then as a vehicle, then as a bicycle, never settling on a classification. Because the software could not decide what she was, it could not decide how to respond. The safety driver was looking at a device at the time. This was the world's first recorded pedestrian fatality caused by a self-driving vehicle. The risk tier was Tier 4 from the first day. The governance applied was not.

One of the most common failure modes in Responsible AI programmes is uniform treatment. Either every use case drowns in process overhead and nothing ships, or everything defaults to low-risk and dangerous systems slip through without scrutiny. Risk tiering solves this by calibrating governance to actual harm potential.

The approach is used by the EU AI Act, NIST AI RMF, and Microsoft's Responsible AI Standard. Risk is determined by four dimensions. Score each dimension 1 to 3, sum the scores, and the tier follows, with one critical exception: a score of 3 on Severity of Harm alone is a veto that triggers minimum Tier 3, regardless of total score. Catastrophic potential cannot be offset by small scale or high reversibility.


| Dimension | 1 — Low  |  2 — Medium  |  3 — High |
|---|---|
| Severity of Harm | Minor inconvenience  /  Financial loss or discrimination  /  Physical harm or loss of liberty |
| Scale of Impact | One person at a time  /  Tens to hundreds  /  Thousands to millions |
| Reversibility | Easily corrected  /  Reversible but costly or slow  /  Irreversible or very difficult to undo |
| Human Autonomy | Human reviews every output  /  Human reviews some outputs  /  AI acts autonomously, minimal oversight |


## The Four Tiers — What Each One Means

Each tier carries a different governance weight, from standard engineering QA at Tier 1 to executive sign-off and independent audit at Tier 4. The tier is not about the technology; it is about the deployment context and the consequences of failure.


## Real-World Examples Across Eight Industries

The same scoring logic applies across industries. What determines the tier is not the sector; it is how the AI is deployed and what autonomy it holds. The same technology can land in different tiers depending on the deployment context.


| Industry — Use Case | Tier  |  The Deciding Factor |
|---|---|
| Retail — Product recommendation engine | 🟢 Tier 1  /  Advisory, reversible, no personal harm potential |
| Marketing — Personalised email campaign targeting | 🟡 Tier 2  /  Personal data processed, but harm is limited and reversible |
| HR — CV screening and candidate ranking | 🟠 Tier 3  /  Affects livelihoods, significant bias risk, difficult to appeal |
| Finance — Loan pre-screening (human reviews all) | 🟠 Tier 3  /  Binding financial impact, but HITL present for every decision |
| Finance — Fully automated loan approval | 🔴 Tier 4  /  Binding and autonomous — no human review before decision |
| Healthcare — Clinical documentation assistant | 🟠 Tier 3  /  Health stakes, but physician reviews and signs every note |
| Healthcare — Autonomous diagnostic tool | 🔴 Tier 4  /  Life at stake, high autonomy, errors potentially irreversible |
| Public Sector — Benefits eligibility decision | 🔴 Tier 4  /  Vulnerable populations, binding decisions, systemic scale |


**The Same Technology, Different Tiers:**

  An AI that flags loan applications for human review is Tier 3. The same AI that approves or rejects loans autonomously is Tier 4.
  The technology may be identical. The deployment context, specifically the degree of human autonomy surrendered, and the binding nature of the decision — determines the tier.
  This is why risk tiering must be re-evaluated whenever the deployment model changes, not just when the underlying model changes.


**Chapter Takeaway**

1. Risk tiering calibrates governance to harm potential, preventing both negligence for dangerous use cases and paralysis for harmless ones.
2. Four dimensions determine risk: severity, scale, reversibility, and human autonomy. A score of 3 on severity alone is a veto — minimum Tier 3 regardless of total.
3. The same technology can land in different tiers depending on deployment context. An advisory AI is never the same risk as the same AI making autonomous decisions.
4. Risk tier is not permanent — use cases must be re-evaluated when the model changes, the user population expands, or the deployment context shifts.
