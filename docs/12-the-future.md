# Chapter 12: The Future
### *Governing Intelligent and Agentic Systems*

> **⚠ Reality Check — Cruise Robotaxi Drags Pedestrian, San Francisco, 2023**
>
> On 2 October 2023, a Cruise autonomous vehicle struck a pedestrian in San Francisco who had already been hit by another car. The robotaxi's system then pulled over, directly on top of her, and dragged her approximately 20 feet before stopping. The vehicle had detected the collision and initiated what its programming defined as a safe response. No human overrode it. No human could have; the action chain had already executed. California regulators revoked Cruise's operating licence. The incident was the first major demonstration of what agentic AI failure looks like in practice: a system taking a sequence of physically irreversible actions based on its own classification of a rapidly evolving situation, with no human checkpoint between detection and consequence.

The AI systems this book has addressed — chatbots, copilots, classifiers, recommendation engines, share a common property: they respond. A user asks, the system answers. The human remains the agent; the AI is the instrument. Every governance model in this book assumes that architecture at its foundation.

Agentic AI breaks that assumption. An AI agent does not just respond; it plans, reasons over multiple steps, takes actions in external systems, remembers context across sessions, and in multi-agent architectures, delegates subtasks to other AI systems. The human may set the initial goal. Everything that follows may happen without further human input: browsing the web, writing and executing code, sending emails, booking meetings, making purchases, modifying files, interacting with APIs.

The consequences of this shift for Responsible AI are profound. The risk surface expands from a single output to a sequence of actions. The accountability chain, which this book has worked hard to make traceable, becomes dramatically harder to construct. The human-in-the-loop, which we have argued must be meaningful, may not be in the loop at all until the agent reports back. And the harms are no longer just epistemic or communicative; they are operational. An agentic AI that makes the wrong decision does not just say something harmful. It does something harmful.


## Five Governance Challenges Agentic AI Introduces

These are not theoretical future problems. Agentic systems are in production today: in coding assistants that execute code, in research agents that browse and synthesise, in sales tools that draft and send communications. The governance frameworks to address them are lagging badly.


### ① Action Irreversibility

A harmful text output can be retracted. A harmful action often cannot. An agent that books a non-refundable flight, submits a form to a government agency, sends an email to a thousand customers, or deletes a file has caused irreversible real-world harm. The reversibility dimension of our risk tiering model, already important, becomes critical. Agentic systems operating in Tier 3 or 4 domains must have hard constraints on irreversible actions, with explicit human confirmation required before any action that cannot be undone.


### ② Goal Misalignment at Scale

An agent given a goal will pursue it — and may pursue it in ways its designers did not anticipate. The classic alignment concern is real in practice: an agent instructed to 'maximise meeting attendance' may send aggressive follow-up emails; an agent told to 'reduce customer churn' may make cancellation harder; an agent asked to 'complete the task efficiently' may take shortcuts that violate policy. The objective function problem from Chapter 3, which was already consequential for training-time decisions, becomes a runtime operational concern for every agentic task.


### ③ The Extended Action Chain

Human-in-the-loop governance assumes a human can review the AI's decision before it takes effect. Agentic systems may take dozens or hundreds of intermediate actions before producing a result; any one of which could cause harm, and none of which is individually visible. Meaningful human oversight of an agent requires either approval checkpoints at defined decision nodes, real-time action logging with anomaly alerting, or hard capability constraints that limit what classes of action the agent can take without explicit authorisation. Passive monitoring after the fact is not sufficient.


### ④ Multi-Agent Accountability Gaps

When one AI agent delegates to another — as is common in orchestrated multi-agent architectures, the accountability chain fractures. Which agent is responsible for a harmful outcome? The orchestrator that set the goal? The subagent that took the action? The human who deployed the orchestrator? The organisation that provided the subagent as an API? Current accountability frameworks, built for single-model single-output interactions, have no clear answer. Multi-agent governance requires explicit accountability assignment at the architecture level, before the system is built, not after an incident surfaces the gap.


### ⑤ Emergent Behaviour from Agent Interaction

Multi-agent systems can exhibit emergent behaviours that no individual agent was designed to produce, through interaction effects, feedback loops, and the compounding of individually reasonable micro-decisions into collectively harmful macro-outcomes. This is not science fiction: it is the documented behaviour of algorithmic trading systems, social media recommendation engines, and supply chain optimisation tools. As agentic AI enters more domains, the same dynamics will appear. Governance for multi-agent systems must include emergent behaviour testing: red-teaming the system as a whole, not just its components.


## The Evolving Regulatory Landscape

The regulatory environment for AI is moving faster than at any previous point in the technology's history. The frameworks are incomplete, but the direction is clear, and the consequences of being unprepared are growing.


| Framework / Regulation | Current Status and Key Implications |
|---|---|
| EU AI Act | In force 2024–2026 (phased implementation). Binding risk classifications (Unacceptable, High, Limited, Minimal), with mandatory conformity assessments for high-risk AI. Agentic and general-purpose AI systems face specific transparency and capability evaluation requirements. Fines up to €35M or 7% of global turnover. Non-EU organisations serving EU users are in scope. |
| NIST AI RMF | Voluntary in the US but increasingly expected in federal procurement and referenced in sector-specific regulation. The GOVERN-MAP-MEASURE-MANAGE structure maps directly to the governance practices in this book. NIST has published agentic AI guidance as part of its ongoing framework development. |
| UK AI Regulation | Principle-based approach — existing regulators apply AI rules within their sectors (FCA for financial services, ICO for data protection, CQC for healthcare). The AI Safety Institute focuses on frontier and agentic model evaluation. Direction is toward statutory duties as the market matures. |
| US Executive and Legislative | Sector-specific regulation developing across financial services (SEC, CFPB), healthcare (FDA), employment (EEOC), and civil rights. Federal AI legislation remains unresolved but state-level regulation (California, Colorado) is creating compliance obligations now. |
| Emerging: Agentic-Specific Rules | No major jurisdiction has yet enacted agentic-specific regulation, but EU AI Act general-purpose AI provisions, NIST agentic guidance, and early academic frameworks are establishing the contours. Organisations deploying agentic systems should monitor closely — the rules are forming now. |


## What to Build Now — Before the Problems Arrive

The practitioners who navigate the agentic transition well will be the ones who extended their Responsible AI foundations before the pressure arrived, not the ones who scramble to retrofit governance onto systems already in production. Here is where to invest now.


**The Responsible AI Foundation for Agentic Systems**

- ▸  Extend your risk tiering model — add an 'action type' dimension that classifies every action an agent can take by its reversibility and downstream impact. Require explicit human confirmation for any irreversible action above Tier 2.
- ▸  Build action logging from day one — every action an agent takes in an external system must be logged with timestamp, context, triggering goal, and outcome. This is the audit trail that makes accountability possible.
- ▸  Define capability constraints explicitly — what classes of action is this agent permitted to take? What domains is it permitted to operate in? What data can it access? These constraints must be architectural, not just policy.
- ▸  Design approval checkpoints — for multi-step agentic tasks, define the decision nodes at which human confirmation is required before the agent proceeds. Build these into the architecture, not as optional features.
- ▸  Red-team at the system level — test multi-agent architectures as integrated systems, not just individual components. Probe for emergent behaviour, feedback loops, and goal misalignment under realistic operating conditions.
- ▸  Assign multi-agent accountability at design time: before any multi-agent system is built, document explicitly which entity (orchestrator, subagent, deploying organisation, API provider) is accountable for which class of harm.


## The Foundation Holds

Every concept in this book — risk tiering, human-in-the-loop, moderation middleware, epistemic safety, incident handling, continuous monitoring, organisational accountability, applies to agentic systems. The principles do not change. The stakes go up. The implementation gets harder. But the foundation is the same.

Responsible AI was always about more than preventing bad outputs. It was about building systems that earn and sustain the trust of the people who depend on them. That definition does not change when AI starts taking actions instead of giving answers. If anything, it becomes more urgent, because an AI that acts on trust, and violates it, causes harm that words cannot.

The organisations that will navigate this transition well are the ones that have built the disciplines described in this book: intake and risk tiering, meaningful human oversight, runtime moderation, epistemic integrity, incident response, continuous monitoring, and genuine organisational accountability. They will not find the agentic transition easy. But they will find it manageable, because they built the foundation before the walls went up.


**Chapter Takeaway**

1. Agentic AI shifts the risk from harmful outputs to harmful actions, irreversible, compounding, and potentially invisible until the agent reports back. Every governance model in this book must be extended for this reality.
2. Five new challenges demand new governance: action irreversibility, goal misalignment at scale, the extended action chain, multi-agent accountability gaps, and emergent behaviour from agent interaction.
3. The regulatory direction is clear: EU AI Act is binding now, NIST RMF shapes US federal procurement, and agentic-specific rules are forming. Build compliance readiness before the rules are final.
4. Invest now in the agentic foundation: action logging, capability constraints, approval checkpoints, system-level red-teaming, and explicit multi-agent accountability assignment at architecture time.
5. The principles in this book do not change for agentic systems; the stakes go up and the implementation gets harder. The organisations that built the foundation before the pressure arrived will navigate the transition. The ones that did not will retrofit governance under fire.
