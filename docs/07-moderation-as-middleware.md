# Chapter 7: Moderation as Middleware
### *Enforcing Responsible AI at Runtime*

> **⚠ Reality Check — Air Canada Chatbot Invents a Policy, 2024**
>
> In early 2024, a British Columbia tribunal ruled against Air Canada in a case where its customer service chatbot had told a grieving passenger that he could apply for a bereavement discount after his flight, and then claim it retroactively. The policy did not exist. When the passenger attempted to claim the discount, Air Canada denied it, arguing the chatbot was a 'separate legal entity' responsible for its own outputs. The tribunal rejected this defence, holding Air Canada liable for what its AI said. The case established a landmark precedent: organisations are legally responsible for the representations their AI systems make to customers, regardless of whether a human reviewed them.

Most teams think of content moderation as a filter, something you add to catch bad outputs before they reach users. That framing is dangerous. A filter is optional, easy to bypass, and frequently disabled under performance pressure. Middleware is structural: it sits in the request-response path by design, and removing it requires an explicit architectural decision.

The difference matters in practice. A filter gets turned off when latency targets are missed. Middleware gets optimised. A filter gets skipped in edge cases. Middleware handles them. When moderation is designed as middleware, as a layer the application routes through rather than a check it occasionally runs; safety becomes consistent, auditable, and enforceable at scale.


## The Moderation Middleware Pattern

The middleware pattern places moderation at two points in every AI interaction: before the model sees the user's input (input moderation), and before the user sees the model's output (output moderation). Both gates are essential: input moderation prevents prompt injection and misuse; output moderation catches harmful, biased, or false content before it reaches users.

Each gate inspects content against a configurable set of categories: toxicity, violence, sexual content, hate speech, self-harm, misinformation, prompt injection, and domain-specific risks, returning a risk score or decision. The application then acts on that decision according to its graduated response policy.


### What the Middleware Layer Provides


## The Moderation Platforms — A Practitioner's Comparison

Six platforms dominate the moderation landscape. Each has a different philosophy, different strengths, and a different fit depending on your architecture, risk tier, and enterprise requirements.

Azure AI Content Safety is the most enterprise-ready moderation platform available. It provides a visual Content Safety Studio for configuring and testing policies, prebuilt classifiers for hate, violence, sexual content, and self-harm, and the ability to create custom categories for domain-specific risks: brand violations, IP leakage, competitor mentions, and more. Every prompt and response can be logged with full audit trails, making it the natural choice for regulated industries and Tier 3–4 use cases.

OpenAI's Moderation API is free to use with any OpenAI API call and classifies content across eleven categories including hate, violence, harassment, sexual content, and self-harm. It returns a confidence score for each category, allowing developers to set custom thresholds rather than relying on binary pass/fail decisions. Model-level safety filters are also applied to every GPT API call before a response is returned, providing a baseline of protection even without explicit moderation calls.

Google offers two distinct moderation tools. Vertex AI Content Safety provides enterprise-grade, customisable moderation layers with multi-layered classifiers tuned for misinformation, civil discourse, and regional legal requirements. The Perspective API, originally built for comment moderation, excels at toxicity detection in conversational text and is widely used for user-generated content moderation. Google's human-in-the-loop integration makes it strong for enterprise workflows requiring review queues.

Amazon Bedrock Guardrails provides a configurable moderation layer for any model deployed on Bedrock, including Claude, Llama, Titan, and others. It supports topic denial (blocking entire subject areas), content filtering across standard harm categories, word/phrase blocklists, grounding checks (to prevent hallucination in RAG systems), and sensitive information redaction. The fact that guardrails apply regardless of which model is running makes it the right choice for multi-model architectures.

Meta's primary contribution to open moderation is Llama Guard, an open-source safety classifier built on the Llama model architecture that can be self-hosted and fine-tuned. Llama Guard classifies both inputs and outputs against a configurable taxonomy of harm categories and is designed to run as a companion to any LLM deployment. Meta also publishes its red teaming methodologies and model risk evaluations openly, making its safety research uniquely accessible.

The open-source ecosystem offers a range of moderation tools suitable for teams that need flexibility, cost control, or domain-specific fine-tuning. Detoxify provides pre-trained toxicity classifiers. Hugging Face hosts a wide range of community moderation models with model cards documenting risks and limitations. Custom fine-tuned classifiers trained on domain-specific data often outperform general-purpose models for specialised use cases: legal, medical, financial, or cultural contexts where standard toxicity definitions do not apply.


## Block, Warn, Escalate — The Graduated Response System

A binary block/allow decision is rarely the right moderation policy. Real-world moderation requires a graduated response, matching the severity of the action to the severity of the risk signal. The following framework applies across all platforms:


| Risk Signal | Recommended Action |
|---|---|
| Score below low threshold | ✅  Proceed normally — no intervention |
| Score above low, below medium | 💬  Soften or reframe the response — adjust tone without blocking |
| Score above medium threshold | ⚠️  Warn the user — display a safety notice or caveat |
| Score above high threshold | 🚫  Block — return a safe fallback response; do not surface the AI output |
| Score uncertain / ambiguous | 👤  Escalate to human review — do not guess on borderline cases |
| Prompt injection detected | 🚫  Block immediately — log the attempt; do not attempt to respond |
| Category: self-harm / crisis | 🆘  Override all thresholds: always surface crisis resources regardless of other scores |


**The Self-Harm Override Rule:**

  Self-harm and crisis content must never be subject to standard threshold logic. Regardless of confidence score, any indication of self-harm intent should trigger an immediate, unconditional safe response that surfaces appropriate crisis resources. This is not configurable; it is a hard requirement for any responsible AI deployment.


## Integration Scenarios

The right integration pattern depends on your architecture. Here are the six most common scenarios and how moderation middleware fits into each:

Moderate user input before it reaches the model, and moderate the model response before it reaches the user. Use Azure Content Safety Studio to monitor violation patterns in production. If input is flagged, block and return a safe fallback; do not send flagged prompts to the model.

Apply Content Safety Studio with low tolerance thresholds for hallucination and brand risk. Route high-risk outputs through a human review workflow before surfacing to the user. Internal copilots warrant stricter policies than public-facing ones; configure separate policy profiles per deployment context.

Without built-in moderation, open-source deployments must add an explicit middleware layer. Use Llama Guard for input/output classification, Perspective API for toxicity scoring, and custom regex rules for domain-specific risks. Both prompt and response should be scored before the conversation continues.

Run the moderation pipeline offline on content submissions before they are published or processed. Classify severity (urgent, high, medium, low) and route to human review queues accordingly. Use OpenAI Moderation API or Google Cloud Content Safety for text; Azure Vision Content Safety for images.

Score text and image components independently, then apply a combined safety decision: if either component is unsafe, the combined output is unsafe. Use Azure Vision Content Safety or Google Vision AI for images; any standard text moderation API for the text component. Do not allow a safe text score to override an unsafe image score.

Use Microsoft Purview for compliance and sensitivity label enforcement on source data. Apply Azure Content Safety to all generated responses before they surface in workflows. Build moderation into approval workflows so that AI-generated content in regulated contexts requires human sign-off before action is taken.


**Chapter Takeaway**

1. Moderation middleware is an architectural pattern, not a feature. It sits in the request-response path by design, applying safety policies consistently at every interaction.
2. Every AI interaction needs two moderation gates: input moderation (before the model) and output moderation (before the user). Both are required — neither substitutes for the other.
3. Match the platform to the deployment: Azure for enterprise and regulated industries, OpenAI for native GPT apps, Google for UGC and regional compliance, AWS Bedrock for multi-model and RAG, Meta/OSS for open-source and air-gapped environments.
4. Use a graduated response system — block, warn, escalate, or soften, rather than binary block/allow. Match the severity of the action to the severity of the risk signal.
5. Self-harm and crisis content must always trigger an unconditional safe response with crisis resources, regardless of confidence score or threshold configuration.
