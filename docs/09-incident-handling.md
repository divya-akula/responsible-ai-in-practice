# Chapter 9: Incident Handling
### *Detecting and Responding to Silent Failures*

> **⚠ Reality Check — Zillow Offers Collapse, 2021**
>
> In November 2021, Zillow shut down its iBuying division and laid off 25% of its workforce after its pricing algorithm systematically overvalued homes, leaving the company holding billions in property it could not sell at a profit. Total write-downs exceeded $500 million. The algorithm had been performing well, until it wasn't, and nobody noticed until the losses were already catastrophic. CEO Rich Barton acknowledged the algorithm's error rate had been 'far more volatile than we ever expected possible.' The failure was not a dramatic crash. It was a quiet drift: the model's predictions diverging from reality over months, with no monitoring capable of detecting the gap until it had become a financial crisis.

Imagine your AI system has been running in production for three months. Your moderation hit rate is stable. No regulatory flags. User satisfaction scores are healthy. And then someone in your legal team pulls a random sample of outputs and finds that your HR copilot has been answering benefits questions using a policy document that was superseded eight months ago. Hundreds of employees have made decisions, some of them irreversible, based on information that was confidently, helpfully, completely wrong.

This is a silent violation. The system functioned exactly as designed. The moderation layer passed everything. The logs show nothing unusual. But the harm was real, cumulative, and entirely preventable, if anyone had been looking in the right place.

Silent violations are the failure mode that most AI governance programmes are not built to catch. They require a different kind of attention: not monitoring for what goes wrong loudly, but watching for what drifts quietly.


## Five Silent Violation Patterns

Silent violations cluster into five recognisable patterns. Understanding each one, including how it manifests, why it is missed, and what leaves a detectable signal, is the foundation of building an effective detection system.


| Violation Pattern | What It Looks Like  |  Why It's Missed  |  The Signal to Watch |
|---|---|
| Grounding Failure | The model answers from cached or hallucinated knowledge rather than the current source documents. Responses sound authoritative and are factually wrong.  Why missed: output moderation passes; the content is not toxic, just incorrect.  Signal: responses that cannot be traced to a retrieved source; grounding check failures; user correction rate increase. |
| Prompt Injection | A user embeds instructions in their input that override the system prompt, changing the model's behaviour, extracting training data, or bypassing safety constraints.  Why missed: the injected content is often phrased benignly; standard moderation looks for harm in content, not for adversarial structure.  Signal: outputs that deviate from system persona; anomalous response length or format; requests for information outside scope. |
| Persona Drift | The model gradually shifts from its defined persona, becoming more familiar, more opinionated, or adopting a role it was not designed to play. Users may come to trust the drifted persona more than the intended one.  Why missed: no single output is obviously wrong; drift is cumulative across a conversation or across time.  Signal: tone analysis deviation from baseline; outputs that include first-person opinions or emotional language outside the system prompt scope. |
| Fallback Failure | The moderation layer flags an input or output but the block does not execute, due to a configuration error, a race condition, or an edge case in the moderation logic. The response is generated and delivered despite the flag.  Why missed: the flag is logged, but the response delivery is not cross-referenced against it. Teams assume that a flag equals a block.  Signal: moderation flag logs that are not matched by a corresponding block action; user receives content that should have been blocked. |
| Polite Misinformation | The model produces content that is factually wrong, subtly biased, or psychologically harmful, but is phrased in a warm, helpful, confident tone that makes it feel trustworthy. No harm category is triggered.  Why missed: this is the hardest pattern to detect automatically. Standard moderation looks for explicit harm markers, not for epistemic quality.  Signal: user correction rate; expert audit sampling; downstream harm reports; hallucination test failures in scheduled red-team runs. |


## Building an AI Incident Detection System

Standard application monitoring — uptime, latency, error rates, is necessary but not sufficient for AI systems. You need a second layer of monitoring specifically designed to surface the signals that silent violations leave behind. The following mechanisms form the core of that layer.


### Grounding Integrity Checks

For every RAG-based response, verify that the output is supported by the retrieved context, not just that retrieval occurred. Attach a document ID or hash to every source used at inference time, and run a post-generation check that flags responses whose claims cannot be traced to the retrieved material. AWS Bedrock Guardrails includes a built-in grounding check for this purpose; for other platforms, it can be implemented as a lightweight consistency classifier.


### Prompt-Response Consistency Monitoring

Monitor whether the model's outputs remain consistent with its system prompt across conversations and over time. A model whose outputs drift significantly in tone, scope, or persona from its system definition is exhibiting the early signal of persona drift or prompt injection. Automated consistency scoring, comparing outputs against system prompt embedding similarity, can surface these deviations before they become patterns.


### Fallback Cross-Reference Logging

Every moderation flag should be logged alongside the action that followed it: block, warn, escalate, or pass. Any flag that is not matched by a corresponding block action within the expected latency window is a fallback failure candidate and should trigger an automated alert. This cross-reference does not happen by default in most platforms; it must be explicitly built into the logging pipeline.


### Shadow Red-Teaming in Production

Periodically inject known adversarial prompts: prompt injection attempts, jailbreak patterns, persona-shifting requests, into your production system using a shadow testing account. If your system fails on patterns it should catch, you will know before a real user finds them. Run these tests on a schedule, not just at deployment time. The threat landscape evolves; your detection should too.


### Scheduled Expert Audit Sampling

Automated systems will miss polite misinformation. No classifier reliably catches a confident, fluent, well-structured answer that is simply wrong. The only defence against this pattern is periodic human review: a structured sample of real production outputs reviewed by a domain expert against the current ground truth. For high-risk domains (medical, legal, financial), this is non-negotiable.


## The AI Incident Response Playbook

When a silent violation is detected — or when a user or auditor surfaces a failure the system missed, the response must be immediate, structured, and documented. The following playbook applies to any AI incident regardless of severity.


**The Four-Phase AI Incident Response**

  Phase 1 — CONTAIN  (within 1 hour)
- ▸  Determine scope: is this a single output, a pattern, or a systemic failure?
- ▸  If systemic: disable or throttle the affected capability immediately
- ▸  Preserve all relevant logs, outputs, and configuration state — do not modify or delete
- ▸  Notify the named accountable owner and the RAI team
  Phase 2 — ASSESS  (within 24 hours)
- ▸  Identify the root cause: grounding failure, prompt injection, persona drift, fallback failure, or other
- ▸  Quantify impact: how many users affected, over what time period, with what downstream consequences?
- ▸  Determine regulatory notification obligations — some incidents require disclosure under GDPR, EU AI Act, or sector-specific regulation
- ▸  Classify severity: P1 (life/safety/legal), P2 (significant harm), P3 (limited harm), P4 (near miss)
  Phase 3 — REMEDIATE  (timeline depends on severity)
- ▸  Fix the root cause — not the symptom. Patching an output is not a fix; the system that produced it still exists
- ▸  Test the fix under adversarial conditions before re-enabling
- ▸  Notify affected users if required — with honest, plain-language explanation
- ▸  Update moderation thresholds, system prompts, or detection logic as appropriate
  Phase 4 — LEARN  (within 2 weeks of resolution)
- ▸  Conduct a blameless post-incident review — focus on system failures, not individual failures
- ▸  Document the incident in the AI incident register with full timeline, root cause, impact, and fix
- ▸  Update the red-team test suite to include this failure pattern
- ▸  Review whether the intake risk tier for this use case needs to be revised upward


## Post-Incident Hardening

Every incident is a gift — provided you extract the learning. The teams that build the most robust AI systems are not the ones that have never had incidents; they are the ones that have built the best feedback loop from incidents back to system design.

After every incident, ask three questions beyond the immediate fix: First, what in the design-time process should have prevented this, and why didn't it? A production persona drift incident often traces back to an evaluation suite that never tested for persona stability under adversarial inputs. Second, what in the detection system should have surfaced this earlier, and why didn't it? A fallback failure that ran for three months undetected is a monitoring gap, not just a bug. Third, what does this tell you about your risk tier assignment? An incident that causes significant harm in a use case classified as Tier 2 is a signal that the tier was wrong.

The AI incident register — a structured log of every incident, its root cause, impact, and resolution: a compliance asset and a learning tool. Review it quarterly. Look for patterns. Build them into your test suites before the next system launches, not after the next incident surfaces.


**Chapter Takeaway**

1. Silent violations are the failures that happen while your system reports green: no error log, no moderation flag, no user complaint until the damage is done.
2. The five patterns to watch for: grounding failure, prompt injection, persona drift, fallback failure, and polite misinformation. Each leaves a different signal.
3. Standard monitoring is not enough. Build a second layer: grounding integrity checks, prompt-response consistency monitoring, fallback cross-reference logging, shadow red-teaming, and scheduled expert audit sampling.
4. When an incident occurs, contain first, then assess scope and root cause, then remediate the system (not just the symptom), then learn and harden.
5. Every incident is a gift — if you extract the right learning. Update your red-team suites, review your risk tier assignments, and build the failure pattern into your design-time process before the next system launches.
