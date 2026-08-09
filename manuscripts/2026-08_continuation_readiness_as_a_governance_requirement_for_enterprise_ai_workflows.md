# Beyond HITL: Continuation Readiness as a Governance Requirement for Enterprise AI Workflows
> A Role State, Work Junction, and Continuation Package Framework

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  

---

## Abstract

Human-in-the-Loop (HITL) is widely treated as the default mechanism for satisfying AI governance requirements: when an AI system reaches a checkpoint it cannot resolve, a human is asked to intervene. This paper argues that intervention is not sufficient. Enterprise AI governance requires **continuability** — the ability of a receiving human or machine actor to act on transferred work without reconstructing it — and continuability is a property of the relationship between what is transferred and who receives it, not a property of the transferred content alone. We show that checkpoint-scoped HITL, by construction, cannot observe this relational property: it evaluates only whether AI output is evidentially complete and whether authority is clearly bounded, both of which are visible from the delivering side. A third, independent condition — Receiving Capacity — determines whether the receiving actor can actually act on the work, and this condition is invisible to any evaluation surface that inspects only the delivered content. We formalize Enterprise AI Workflow as the unit of governance analysis (rather than the individual AI system or the individual agentic pipeline), and introduce three model objects — Role State, Work Junction, and Continuation Package — together with a Role Requirement Feedback Loop that operationalizes the co-design of human roles and AI delivery formats. We identify six classes of governance failure that checkpoint-scoped HITL cannot detect — including one on the delegation (H2A) side, where an underspecified transfer causes the receiving AI to silently infer scope it was never given — the most consequential of which — Capacity-blind transfer — occurs when every indicator visible to the delivering side is satisfied while the receiving side is structurally unable to continue the work: a governance failure disguised as a completed junction closure. We situate this model against Joint Cognitive Systems theory, recent formal HITL governance frameworks (HAIG; Chiodo et al.), AI-in-the-Loop scholarship, process-notation extensions (BPMN, Agentic BPMS), and human-robot handover research, and argue that the reviewed work does not treat continuation as a jointly determined, receiving-side-verified condition of enterprise work transfer.

**Keywords:** AI Governance, Human-in-the-Loop, Enterprise AI Workflow, Role-Bounded Systems, Continuation Readiness, Engineering Determinacy

**Suggested JEL Classification:** M15 (IT Management), O33 (Technological Change: Choices and Consequences; Diffusion Processes), D23 (Organizational Behavior; Transaction Costs; Property Rights), L86 (Information and Internet Services)

---

## 1. Introduction

Human-in-the-Loop is usually defined by **when** a human is inserted into an AI process: a checkpoint, an approval gate, an escalation trigger. This framing has produced a large and useful literature on intervention timing, oversight levels, and failure-triggered escalation. It has not produced an equally developed account of what happens **after** the human is inserted — whether the human who arrives at that checkpoint can actually do anything with what the AI has produced.

This paper's central claim can be stated in three sentences:

> HITL requires intervention, but governance requires continuability. Continuability depends not only on what AI provides, but on whether the receiving role can actually act on it. Therefore, Enterprise AI Governance must design human roles, AI delivery, and workflow junctions together.

The first sentence separates two things that are routinely conflated: the **presence** of a human at a decision point, and the **capacity** of that human to meaningfully continue the work. The second sentence locates the source of governance failure not in the AI's output alone, nor in the human's competence alone, but in the **relationship** between the two — a relationship that has rarely been isolated as a formal evaluation criterion in HITL governance. The third sentence states the design consequence: if continuability is relational, then human role design, AI delivery format, and the structure of the workflow junction between them cannot be designed independently of one another.

This reframing matters because it exposes a specific and structurally under-specified failure mode, and it applies symmetrically in both directions of transfer. Consider a Continuation Package — the structured work content that crosses a workflow junction — that is evidentially complete, whose assumptions are disclosed, whose authority boundary is explicit, and whose unresolved decisions are clearly flagged. By every indicator a checkpoint-scoped HITL design can inspect, this transfer is governed: evidence is sufficient, authority is clear. Yet if the human receiving this package (an A2H transfer) lacks the domain standing, the time, or the organizational mandate to act on it, the transfer has not, in fact, transferred anything governable. The same is true in reverse: if the human delegating to an AI role (an H2A transfer) under-specifies intent or scope, the AI does not stop and ask — it infers, and the resulting decision can be wrong in a way no downstream checkpoint will catch, because the output that eventually surfaces looks well-formed. In both directions, the junction reports success. Governance has failed. This is not a hypothetical edge case; it is the structural blind spot of any governance design that evaluates only one side of a transfer, in either direction.

### 1.1 Contributions

This paper makes three contributions.

First, it repositions the unit of governance analysis from the individual AI system or the individual agentic pipeline to the **Enterprise AI Workflow** — a sequence of role-bounded work segments, human and machine alike, connected by governance-relevant transitions. We show that this repositioning is necessary because enterprise work crosses temporal, accountability, and role discontinuities that single-session AI pipelines do not (Section 2).

Second, it formalizes three model objects — **Role State**, **Work Junction**, and **Continuation Package** — together with a symmetric taxonomy of transitions (H2H, H2A, A2H, A2A) and a **Role Requirement Feedback Loop** that treats human role design and AI delivery format as co-determined rather than derived in either direction alone (Section 4).

Third, and centrally, it identifies **three conditions of Continuation Readiness** — Content Sufficiency, Authority Clarity, and Receiving Capacity — and shows that checkpoint-scoped HITL evaluates only the first two. **Receiving Capacity is this paper's principal addition to the governance literature**: it is not a third item on an evidence-and-authority checklist, but an independent, relational condition that determines whether the receiving actor can act on a transfer at all — and its absence produces a specific, structurally invisible failure mode we call **Capacity-blind transfer** (Sections 5–6). A simple illustration makes the stakes concrete: an AI actor may generate code, document it completely, and stay within its authorized scope, and still hand this off to a Product Owner or compliance officer who cannot read code. Every checkpoint-scoped indicator reports success; the sign-off that follows is ceremonial. The paper's resolution — regenerating the transfer as a business-readable verification report rather than reassigning the review to an engineer — is developed in full in Section 6 and previewed here because it illustrates, more concretely than any definition can, what Receiving Capacity adds that existing HITL governance frameworks do not check.

### 1.2 Roadmap

Section 2 establishes why Enterprise AI Workflow, not the agentic pipeline, is the correct unit of analysis, through three structural discontinuities. Section 3 positions this work against six adjacent literatures. Section 4 presents the model. Section 5 formalizes the three conditions of Continuation Readiness. Section 6 shows why checkpoint-scoped HITL cannot detect all resulting failure modes. Section 7 connects the model to Engineering Determinacy. Section 8 walks through an illustrative application. Sections 9–11 discuss implications, limitations, and conclude.

---

## 2. Motivation: The Structural Discontinuities of Enterprise AI Workflow

An AI pipeline — a single prompt, a single agent task, a single orchestrated run — is typically executed within a continuous, shared context. Even when such pipelines include logs, traces, memory, or checkpoints, these artifacts primarily serve execution, debugging, replay, and monitoring. They are **runtime** artifacts, consumed by the same process (or its operator) that produced them, usually within the same session or a tightly coupled resumption of it.

Enterprise AI Workflow is different in kind, not merely in scale. Work does not proceed through a continuous, shared execution context; it crosses three structural discontinuities that an ordinary pipeline does not need to bridge.

### 2.1 Temporal Discontinuity

A human or machine actor may receive work hours or days after a previous segment has completed, with no shared session context. If the AI segment supplies only an **answer**, the receiving actor must reconstruct the reasoning, the rejected alternatives, and the boundary conditions before they can trust or extend the result. This reconstruction cost is precisely what causes HITL, in practice, to degrade into what we term **full-review collapse**: rather than a bounded transfer, the human ends up redoing the AI's analytic work in order to verify it, defeating the purpose of delegation in the first place.

### 2.2 Accountability Discontinuity

Enterprise workflows carry legal, regulatory, and audit obligations that a single AI pipeline run does not. If the evidence, assumptions, and unresolved risk behind a judgment are not preserved in structured form, the organization cannot, after the fact, reconstruct why a given decision was made or apportion responsibility for its consequences. An **artifact** — the output alone — is therefore insufficient; what is required is the **evidentiary trail** behind the artifact.

### 2.3 Role Discontinuity

The actor who receives a segment of enterprise work is frequently not the actor who initiated it, and is frequently not even in the same professional role. A Product Manager who defines the intent for a piece of AI-assisted analysis is not necessarily the Product Manager (or any Product Manager) who later authorizes its release; a Reviewer, a Risk Owner, a Security Validator, and a Developer each require different evidence, hold different authority, and can be asked to bear different responsibility. The **same output** is therefore not adequate for different receiving roles — what must be transferred depends on who is receiving it.

### 2.4 A Running Example

Throughout this paper we use one illustrative chain: **Human Product Owner → AI Business Analyst → Human Architect → AI Specification Agent → Human Reviewer.** No segment in this chain fails. The AI Business Analyst does not encounter an error; the AI Specification Agent does not hit a confidence threshold. Yet at every arrow, work, evidence, and unresolved decisions must cross a temporal, accountability, and role discontinuity in order for the chain to function as a single governed process rather than five disconnected episodes.

### 2.5 Defining the Object of Transfer

We can now state the object this paper is built around:

> **A Continuation Package is the structured work content required for a receiving actor to continue enterprise work across temporal, accountability, and role discontinuities without reconstructing prior work.**

A Continuation Package is not runtime state and not an execution log; both of those serve the **producing** process. A Continuation Package serves the **receiving** actor, at a different time, under a different authority boundary, and with independent responsibility for what happens next. This distinction — cross-boundary continuation object, not runtime artifact — is what separates the concept from adjacent notions of agent state, checkpointing, or session memory used in orchestration engineering.

The concept is also distinct from data provenance. Provenance is backward-looking: it records where a piece of data or an output came from, by whom it was handled, and how it changed, primarily to support later audit or dispute. A Continuation Package is forward-actionable: its purpose is not to reconstruct history for an auditor but to supply the receiving actor, at the moment of transfer, with the minimum sufficient context to act on the work now. A Continuation Package will typically draw on provenance information (Section 4.3's Evidence field), but provenance alone — a complete historical record — does not guarantee that a receiving actor can act on what they receive; that additional, forward-facing, receiver-specific requirement is what this paper formalizes.

---

## 3. Related Work

We position this paper against six literatures. For each, we identify which of the three structural discontinuities (Section 2) it addresses and which it leaves open.

### 3.1 Joint Cognitive Systems and Dynamic Function Allocation

Cognitive Systems Engineering has, since Hollnagel and Woods (2005), rejected the **a priori** allocation of functions between human and machine — the "Fitts List" / MABA-MABA tradition (Fitts, 1951) — on the grounds that static allocation cannot accommodate the reciprocal, adaptive nature of joint work. Joint Cognitive Systems (JCS) theory conceptualizes human and machine as interdependent components of a single cognitive system rather than as separately optimized entities, and this principle has recently been extended explicitly to AI through Human–AI Joint Cognitive Systems (Xu and Gao, 2024).

This paper's central refusal to derive human role from AI transfer design, or AI delivery from a fixed human role, in either direction alone, is a direct descendant of this critique. We do not claim the co-design principle itself as novel. Our contribution is to extend it from its traditional domain — real-time cognitive task-sharing in safety-critical control systems, where the governing criterion is cognitive workload and situational awareness — to enterprise business workflow governance, where the governing criterion is accountability, evidentiary traceability, and multi-actor responsibility across organizational stages that may be separated by hours, days, or organizational boundaries. We further depart from human-centered extensions such as HAJCS, which retain human decision primacy "especially in critical contexts," by treating human and AI actors symmetrically across all four transition types (H2H, H2A, A2H, A2A) defined in Section 4.

The same disciplinary neighborhood has also produced a well-documented empirical account of what happens when human oversight is present but structurally hollow: automation bias, in which a human overseer accepts an automated system's output without independent verification, at rates that can be unacceptable in purely human decision chains (Cummings, 2004). This paper treats automation bias not merely as a behavioral tendency to be mitigated through training or vigilance, but as the predictable behavioral consequence of a structural condition — an absence of Receiving Capacity — that this paper formalizes and traces to specific, detectable Work Junctions. We return to this connection in Section 6.

**Discontinuities addressed:** none directly, at the level of enterprise multi-stage workflow (JCS operates at the level of a single human-machine control loop). **Contribution taken:** the philosophical rejection of unidirectional derivation.

### 3.2 Formal HITL Governance: HAIG and Chiodo et al.

Two recent papers formalize HITL governance at a different level of abstraction than this one. HAIG (Engin, 2025/2026) introduces three continuous governance dimensions — Decision Authority Distribution, Process Autonomy, and Accountability Configuration — replacing discrete HITL/HOTL categories with a positional, threshold-based architecture. Chiodo et al. (2025) formalize HITL setups using oracle machines and reductions from computability theory, distinguishing trivial monitoring, single-endpoint action, and Turing-reduction-level involvement, and derive a taxonomy of HITL failure modes tied to legal-moral responsibility attribution.

Both papers formalize governance at the level of a single AI system or a single human-AI relationship. Neither addresses how responsibility, evidence, and authority transfer as work moves across multiple human roles and agentic execution segments within a business process; neither defines a workflow segment, a junction, or a role-bounded transfer object. This paper addresses that distinct unit of analysis: the enterprise workflow, in which junctions between multiple actors and stages — not the configuration of a single system — are the object of governance.

**Discontinuities addressed:** accountability discontinuity, at the single-relationship level. **Not addressed:** temporal discontinuity across stages; role discontinuity across multiple, sequentially different actors.

### 3.3 AI-in-the-Loop (AI2L)

Recent work explicitly contrasts systems commonly labeled Human-in-the-Loop with AI-in-the-Loop (AI2L) configurations, where primary decision authority remains with the human and AI serves an advisory or supportive role (Natarajan et al., 2025). Building on this taxonomy, operational architectures for agentic workflows have begun decoupling HITL components into standalone governance artifacts parameterized across When, Who, What, and Where dimensions (Cheng & Cheng, 2026). While these frameworks clarify where decision authority resides during a single human-AI interaction segment, they do not extend to governing multi-stage, role-bounded transfers across heterogeneous organizational actors.

**Discontinuities addressed:** partial accountability discontinuity (authority attribution). **Not addressed:** temporal and role discontinuity.

### 3.4 Process Notation: BPMN Extensions and Agentic BPMS

Recent extensions to business process notation, such as the BPMN extension for human-agentic collaborative workflows proposed by Ait et al. (2025), introduce constructs for agent profiling, reflection, and role-based execution boundaries. Parallel industry practice positions BPMN and Agentic Business Process Management Systems as the orchestration and governance layer for autonomous agents embedded in enterprise processes.

This literature addresses **notation and orchestration**: how a diagram or process model represents participants, roles, and agent collaboration. It does not specify the **content** that must cross a lane boundary for the receiving participant to act without reconstruction. This paper is complementary rather than competing: while process notation addresses how a workflow is represented, this paper addresses what must be carried across each junction for the transition to be governable, independent of how the workflow is diagrammed or executed.

**Discontinuities addressed:** role discontinuity, at the representational level (who is where). **Not addressed:** the content specification of what crosses each junction; accountability and receiving-capacity conditions.

### 3.5 Escalation-Based Handoff Practice

A substantial and fast-moving body of engineering practice on multi-agent AI systems has independently converged on several of the intuitions formalized here. For example, OpenAI's Agents SDK treats handoffs as tool-mediated control transfers between specialized agents, while LangGraph supports human-in-the-loop interrupt and resume patterns backed by persisted graph state. These implementation patterns show that production systems increasingly need explicit transfer, interruption, and resumption mechanisms. However, this practitioner literature remains implementation-oriented: it does not provide a field-level governance definition of role, work, or transfer content; it does not connect transfer mechanics to enterprise accountability requirements; and it does not treat human and AI actors symmetrically across all four transfer directions.

We treat this literature as external validation that the problem is real and increasingly acute in production systems, and as a further reason not to treat the routing-level meaning of "handoff" in specific orchestration frameworks (e.g., agent-to-agent control transfer in some multi-agent SDKs) as equivalent to the governance-level transfer this paper formalizes: the former is a session-local, implementation-level routing mechanism agnostic to organizational authority; the latter additionally requires crossing a role, authority, or responsibility boundary as defined in Section 4.

**Discontinuities addressed:** temporal discontinuity, at the engineering-pattern level (context preservation). **Not addressed:** accountability and role discontinuity as governance requirements rather than engineering reliability requirements.

### 3.6 Human-Robot Handover

Human-Robot Interaction research on physical object handover offers a mature, decades-deep account of a related structure: a **giver** and **receiver** coordinate across a **pre-handover** phase, in which the giver plans motion in anticipation of the receiver's task, and a **physical handover** phase (Ortenzi et al., 2020). This literature demonstrates, at the sensorimotor timescale, exactly the principle we apply at the organizational timescale in Section 4.5: that a transfer should be shaped by the receiver's requirements **before** release, not reconstructed by the receiver after the fact.

We treat this literature as a cross-domain conceptual anchor, not a competing model. The two domains differ in what is being coordinated: physical handover coordinates grip timing and trajectory at millisecond resolution; enterprise work transfer coordinates authority, evidence sufficiency, and acceptance conditions at organizational resolution. We borrow the anticipatory-shaping principle; we do not import the domain's specific mechanisms.

**Discontinuities addressed:** none directly (single-actor-pair, single-transfer scope). **Contribution taken:** the anticipatory-shaping principle underlying continuation-aware generation.

### 3.7 Summary

The comparison can be summarized without treating the literatures as direct competitors:

- **JCS / Dynamic Function Allocation**: provides the philosophical basis for rejecting unidirectional human-machine function allocation, but does not directly address temporal, accountability, role, or receiving-capacity discontinuities at the level of enterprise multi-stage workflow.
- **HAIG / Chiodo et al.**: partially address accountability, but at the level of a single human-AI relationship rather than a multi-stage enterprise workflow.
- **AI2L**: partially addresses accountability by clarifying authority attribution, but does not address temporal or role discontinuity across work stages.
- **BPMN / Agentic BPMS**: partially addresses role discontinuity at the representational level by showing who appears where in a process model, but does not specify what content must cross each junction or whether the receiving actor can act on it.
- **Escalation-based practice**: partially addresses temporal discontinuity as an engineering reliability issue, especially through context preservation, but does not treat accountability and role discontinuity as governance requirements.
- **Human-Robot Handover**: contributes the anticipatory-shaping principle, but does not directly address enterprise workflow discontinuities.
- **This paper**: addresses temporal, accountability, role, and receiving-capacity discontinuities as joint requirements of governed enterprise work transfer.

Within the reviewed literature, Receiving Capacity is not treated as an independent, formally required condition of a governed transfer. This is the gap this paper addresses.

---

## 4. The Model: Role State, Work Junction, and Continuation Package

### 4.1 Role State

An actor's behavior within a workflow is governed not by its type (human or AI) but by its **Role State** at a given stage:

> **R = {actor, viewpoint, policy, scope, authority, evidence-access, expected-output}**

Formally, let `R` be drawn from the product space `Actors x Viewpoints x Policies x Scopes x Authorities x EvidenceSets x Outputs`, where `Actors` includes human and agentic actors without privileging either type. A Role State is a single point in this product space, not a label; two actors sharing a job title can occupy different Role States at different workflow stages.

Role State is stage-specific. A single named position — a Product Manager, say — may hold different Role States across Discovery, Specification, and Acceptance stages of the same workflow: different viewpoint, different decision authority, different required evidence, different expected output. Human and AI actors are both instances of *`actor`*; nothing in the model privileges one type over the other. This is a deliberate departure from approaches that treat "human role" as a pre-given organizational category and "AI role" as something engineered around it. Here, both are outputs of the same schema.

### 4.2 Work Junction

A **Work Junction** is a point in the enterprise workflow at which work, evidence, and responsibility must cross from one Role State to another. Not every technical transition is a Work Junction. We adopt the following test:

> A transition constitutes a Work Junction if and only if it crosses at least one of: role boundary, authority boundary, responsibility boundary, evidence boundary, or decision boundary. Transitions crossing none of these — sequential tool calls within a single agent's plan, or session-local routing between agents operating under the same authority grant — are implementation-level transitions, not governance-relevant junctions.

This test is what allows a single, symmetric taxonomy (Section 4.4) to apply uniformly whether the actors on either side are human, AI, or mixed.

We add a validity condition, developed in full in Section 5:

> A Work Junction is only **valid** — in the governance sense — if the Role State of the receiving actor is compatible with the work being transferred: its scope, authority, and evidence-access must be sufficient to act on the transferred content. A Continuation Package delivered to an incompatible Role State does not constitute a governed transfer; it constitutes a governance failure disguised as a completed junction closure.

### 4.3 Continuation Package

The content that crosses a Work Junction is the **Continuation Package**:

> **Continuation Package = Artifact + Work State + Evidence + Authority Context + Open Issues + Continuation Instructions**

where **Artifact** is the produced output; **Work State** is what has been completed and what remains; **Evidence** includes the assumptions made and the basis relied upon; **Authority Context** specifies what decisions the delivering actor was and was not authorized to make; **Open Issues** are unresolved questions, exceptions, and risks; and **Continuation Instructions** specify the required next action and the recommended receiving role.

A **Continuation Package Contract** specifies, for a given Work Junction, which of these fields are mandatory, and in what form — e.g., which stages require a Human Authorization field to be non-empty before the junction is considered closed.

**The Continuation Package is directional-agnostic.** Everything stated above applies with equal force to H2A junctions, not only to A2H junctions. An H2A Continuation Package — what a human role delegates to an agentic role — requires the same fields under the same schema: the **Artifact** slot becomes the task specification itself; **Evidence** becomes the context and data the AI is granted access to; **Authority Context** becomes the explicit policy and constraint under which the AI may act (what it MUST do, what it MUST NOT do); **Open Issues** becomes whatever remains ambiguous in the human's own intent at the point of delegation. This symmetry is not cosmetic. Sections 5 and 6 apply Content Sufficiency, Authority Clarity, and Receiving Capacity to both directions.

### 4.4 Symmetric Transition Taxonomy: H2H, H2A, A2H, A2A

Because the Work Junction test (Section 4.2) is defined independently of actor type, it produces four transition types as a direct consequence of *`source ∈ {Human, Agentic}`* and *`target ∈ {Human, Agentic}`*, rather than as four independently stipulated categories:

- **H2H** — Human Role to Human Role (e.g., a Reviewer's sign-off transferred directly to a Decision Owner, with no agentic segment between them). This case demonstrates that Enterprise AI Workflow, as a unit of analysis, must be able to represent segments with no AI involvement at all — a requirement that agentic-workflow-scoped models cannot satisfy by construction.
- **H2A** — delegation from a human role to an agentic workflow.
- **A2H** — transfer from an agentic workflow to a human role, which may occur on **failure** (the AI cannot resolve the task within its authority) or on **completion** (the AI has finished and the work must proceed to review, acceptance, or authorization). We emphasize that A2H is not exclusively an exception path: the running example in Section 2.4 contains A2H transitions with no failure involved.
- **A2A** — transfer between two agentic roles with **different** authority or responsibility — for example, an AI Generator producing a candidate artifact and an AI Validator assessing it against policy, risk, and acceptance criteria. A2A qualifies as a governance-relevant Work Junction only when it crosses one of the boundaries defined in Section 4.2; purely technical routing between agents operating under identical authority is not.

**A brief terminological note.** Some multi-agent orchestration frameworks use "handoff" to denote a session-local, tool-mediated control transfer between agents operating under the same authority. This is an implementation concern outside the scope of this model. An A2A Work Junction, as defined here, additionally requires crossing a role, authority, or responsibility boundary — a condition framework-level routing does not by itself satisfy.

### 4.5 Continuation-Aware Generation

The receiving role should shape an AI actor's output **before** the Work Junction occurs, not only after. We formalize this as:

> **Output = f(Task, Current Role, Next Role, Continuation Package Contract)**

rather than the conventional *`Output = f(Task)`*. This principle has a well-established analogue in human-robot handover research, where the pre-handover phase involves the giver planning motion in anticipation of the receiver's task (Section 3.6). We extend this from physical object transfer to informational work transfer: an AI actor's output should be shaped by the receiving role's evidence, authority, and format requirements before the Continuation Package is finalized, not reconstructed by the receiver afterward.

### 4.6 The Role Requirement Feedback Loop

The preceding sections risk implying that Role State is fixed input and Continuation Package generation is the only variable to be designed. This is incorrect, and correcting it is necessary to make good on the co-design principle inherited from Section 3.1.

When a Work Junction fails specifically because the receiving Role State cannot act on an otherwise complete Continuation Package (the **Capacity-blind transfer** failure formalized in Sections 5–6), this failure is informative. It indicates one of two things: either the Role Requirement at that junction is under-specified relative to the work it must receive (the role needs broader authority, different evidence access, or reassignment to a more senior or differently qualified actor), or the AI's delivery format must be adapted to the actual — not assumed — capacity of the existing role (lower assumption density, higher explanatory scaffolding, decomposition into smaller decision units).

> When a Work Junction fails due to Capacity-blind transfer, the failure is not attributed to the Continuation Package alone, nor to the receiving Role State alone, but treated as a signal requiring joint revision on both sides.

This feedback loop is what operationalizes the claim, otherwise merely asserted, that human roles, AI roles, and junction design are co-designed within the enterprise workflow rather than derived from any single direction: co-design is not a one-time design decision but an ongoing correction mechanism triggered by observed junction failures.

The loop has two distinct resolution paths, and choosing correctly between them matters. One path revises the **Role Requirement** — assigning a differently qualified actor to the junction. The other revises the **AI Delivery Format** — regenerating the Continuation Package in a form the existing Role State can act on. These are not interchangeable, and the choice depends on what governance question the junction was meant to answer, not merely on who can technically process the content (see the code-review case in Section 6, where reassigning to an engineer would answer the wrong question).

---

## 5. Three Conditions of Continuation Readiness

We now state formally what must be true for a Work Junction transfer to be governed.

### 5.1 Content Sufficiency

The Continuation Package contains what is required to understand the work performed: artifact, work state, evidence, assumptions, and open issues, at a level of completeness specified by the Continuation Package Contract for that junction. This is an **epistemic** condition — it concerns whether enough is known. Applied to an H2A junction, Content Sufficiency concerns whether the delegating human has supplied enough intent, context, and evidence-access for the receiving AI role to act correctly, rather than filling gaps by inference.

### 5.2 Authority Clarity

The Authority Context field explicitly establishes which decisions the delivering actor was and was not authorized to make, and — critically — who holds authority over the unresolved decisions that remain. This is a **governance** condition in the strict sense used in this paper: Authority means behavioral rules and constraints (Policy = MUST, Constraint = MUST NOT), not merely the disclosure of information. A Continuation Package can be evidentially rich and still fail this condition if it does not specify who may accept the remaining risk, who may override, and who is accountable if the eventual decision proves wrong. Applied to an H2A junction, Authority Clarity concerns whether the delegating human has explicitly bounded what the AI MAY decide and what it MUST NOT decide; an under-specified delegation does not merely risk inefficiency, it is the structural precondition for the AI silently expanding its own decision scope to cover the gap.

### 5.3 Receiving Capacity

The receiving actor's Role State — its domain access, its authority, its scope — must actually correspond to the demands of the transferred work. This is a **relational** condition: it cannot be evaluated from the content of the Continuation Package alone. It requires checking the Package against the Role State of whoever is on the receiving end of a specific Work Junction, at the time of that transfer.

We decompose Receiving Capacity into two sub-dimensions, because they fail differently and require different remedies:

- **Structural Capacity** — whether the receiving actor holds the domain standing, legal authority, and explicit permissions the work requires. A failure here is a mismatch of **kind**: the actor is not the right actor for this decision, regardless of how much time they are given.
- **Operational Capacity** — whether the receiving actor has the cognitive budget, time availability, and inspection throughput the transfer demands at this moment. A failure here is a mismatch of **degree**: the actor may be the right actor in principle, but a five-page analysis delivered for a thirty-second decision window exceeds what they can actually process, regardless of their formal standing.

The code-review case in Section 6 is a Structural Capacity failure — no amount of time restores an untrained reader's ability to evaluate source code. A senior executive with full authority over a decision but a three-line attention budget for a five-page brief is an Operational Capacity failure of the same underlying condition. Both are invisible to checkpoint-scoped HITL for the same reason: neither is observable from the delivered content alone.

### 5.4 The Formal Relationship, and Where Traditional HITL Stops

> **Continuation Readiness = Content Sufficiency ∧ Authority Clarity ∧ Receiving Capacity**

All three conditions must hold for a Work Junction to be governed. Traditional, checkpoint-scoped HITL evaluates only the first two — both of which are observable from the delivering side, because both concern what the AI actor has produced and how clearly its authority is bounded. When Content Sufficiency and Authority Clarity are satisfied but Receiving Capacity is not, a checkpoint-scoped HITL design will report the transfer as complete, because nothing in its evaluation surface — which never inspects the receiving actor's actual Role State against the work — can detect the third condition's absence.

This is the central failure this paper identifies: governance appears satisfied by every indicator the delivering side can report, while the junction, in fact, is not governed.

---

## 6. Why Checkpoint-Scoped HITL Cannot Satisfy Enterprise AI Governance

A HITL design scoped to individual AI checkpoints cannot, by construction, detect governance failures that arise between checkpoints, across AI-to-AI transitions, or from a mismatch between transferred work and receiving capacity — because such failures are invisible to a model that never represents the enterprise workflow, or the receiving Role State, as a whole.

We distinguish two groups of failure.

### Group A — Failures Correctable by Improving the Continuation Package or Junction Contract

1. **Unmodeled junction authority gap.** A checkpoint-scoped HITL design specifies where AI should stop, but not the complete inventory of junctions across the workflow; junctions between two checkpoints, or between two AI segments, fall outside its representation entirely, and authority defaults to whoever is nearest to the outcome rather than whoever was meant to hold it.
2. **Orphaned evidence.** An A2H transfer that is not required to carry assumptions and evidence leaves the receiving human unable to reconstruct the basis for the AI's work — not because this was done poorly on a given occasion, but because checkpoint-scoped HITL has no mechanism that requires it.
3. **AI-to-AI responsibility diffusion.** Because traditional HITL treats only the human as the object of governance, an A2A transition between an AI Generator and an AI Validator with different authority is invisible to it as a governance-relevant event; it is treated as pure technical routing, and responsibility is silently lost between the two AI actors.
4. **Workflow-blind role assignment.** New human roles (e.g., "Agent Supervisor," "Exception Handler") are assigned by direct enumeration from observed organizational experience, without any mechanism to check whether these roles, taken together, cover every junction the workflow actually contains.
5. **Underspecified delegation.** This is the H2A mirror of the first four failures, and is easy to overlook because checkpoint-scoped HITL designs are built to inspect AI **output**, not the human-supplied **input** that produced it. When an H2A Continuation Package under-specifies intent, scope, or authority, the receiving AI role does not halt — it fills the gap by inference. We term the first pattern **Ghost Intent** (the AI acts on an intent the human never actually specified, inferred from an underspecified delegation) and the second **Inference Creep** (the AI's inferred scope silently expands beyond what was delegated, decision by decision, without ever crossing a checkpoint that would catch it). A checkpoint placed only at the far end of the workflow — where AI output is reviewed — cannot see this failure originate, because by the time output is produced, the incorrect inference is already baked into it and presents as a normal, well-formed artifact.

All five failures in Group A share a structural feature: they can, in principle, be corrected by making the Continuation Package or the junction inventory more complete — on whichever side (A2H or H2A) the deficiency originates. They are failures of **specification**, not of the model's fundamental scope.

### Group B — The Failure That Cannot Be Corrected by Improving the Package Alone

6. **Capacity-blind transfer.** A Continuation Package is evidentially complete and its authority boundary explicit — Content Sufficiency and Authority Clarity both hold — yet the receiving actor's Role State does not correspond to the demands of the work: insufficient domain standing, insufficient time, or a scope of authority narrower than the decision now required of them. No checkpoint-scoped indicator flags this, because no such indicator inspects the correspondence between transferred work and receiving Role State. **This is a governance failure disguised as a completed junction closure.**

**Illustrative case.** An AI actor generates source code and hands it off to a designated human reviewer whose Role State does not include the ability to read code — a common configuration when the receiving role is a Product Owner, a compliance officer, or a business-side Decision Owner rather than a software engineer. The Continuation Package may be, by every checkpoint-scoped indicator, complete: the code is syntactically valid, the commit is annotated, assumptions are documented in comments, and the delivering AI has stayed within its authorized scope. Content Sufficiency and Authority Clarity both hold. Under a checkpoint-scoped HITL design, this junction reports success — a human is "in the loop." In practice, the human cannot evaluate what was just handed to them, and the checkpoint is ceremonial: sign-off occurs, but no governance-relevant judgment has actually been exercised.

This case also demonstrates that Capacity-blind transfer is not resolved by escalating to a different role — reassigning the review to an engineer changes who is in the loop, but does not change **what governance question this junction was meant to answer** (does this change meet business intent, risk tolerance, and compliance requirements — a business-side judgment, not a code-correctness judgment). The correct resolution operates on the AI Delivery Format side of the Role Requirement Feedback Loop (Section 4.6): the AI actor must instead produce a Continuation Package whose Artifact is a **verification report** — a structured account of what changed, why, what was tested, what risks were identified, and what business-relevant behavior is affected — expressed in terms the existing Role State can act on, without requiring the receiving actor to read the code at all. Only once the Continuation Package is regenerated in a form compatible with the receiving Role State does the junction satisfy Receiving Capacity, and only then does the human's sign-off constitute an exercise of governance rather than its appearance.

This is the general pattern Capacity-blind transfer describes: the failure is not that the AI produced insufficient content, nor that its authority was unclear, but that **content sufficient for one Role State is not sufficient for another**, and no checkpoint-scoped design checks which Role State is actually on the receiving end.

Capacity-blind transfer also names the structural precondition for a well-documented failure in the human factors literature: automation bias, in which a human overseer accepts an automated system's output without independent verification (Cummings, 2004). Cummings shows that even trained operators, under time pressure and facing recommendations they are not equipped to independently evaluate, approve machine-generated solutions at rates that would be unacceptable in a purely human decision chain — with consequences documented in safety-critical domains including fratricide incidents in combat identification systems. Automation bias is typically discussed as a **behavioral** tendency — humans defer to automation. This paper's contribution is to locate a **structural** precondition beneath that behavior: when Receiving Capacity is absent, deference is not a lapse in vigilance but the only available response, because the receiving actor has no independent basis on which to do otherwise. A checkpoint that structurally cannot be exercised will, predictably, be rubber-stamped; the remedy is not to demand more vigilance from the human, but to close the Receiving Capacity gap through the mechanism in Section 4.6.

Group B cannot be resolved by adding more fields to the Continuation Package Contract; the package can already be maximally complete. It can only be resolved by the mechanism introduced in Section 4.6 — the Role Requirement Feedback Loop — which treats the failure as a signal to revise either the receiving Role State or the delivery format, rather than as a defect in the delivered content.

This is, in our view, the central reason checkpoint-scoped HITL is structurally insufficient for enterprise AI governance: not because any given checkpoint is poorly designed, but because the model has no evaluation surface on which Capacity-blind transfer can even register as a failure.

---

## 7. Engineering Determinacy as the Governing Criterion

We connect the preceding model to a single governing criterion:

> **A human–AI workflow is determinate when, at each Work Junction, it is possible to establish who is acting, under what role and authority, what work state has been transferred, what remains unresolved, and who is responsible for the next decision.**

This criterion requires all three conditions of Section 5 jointly: **who is acting, under what role and authority** corresponds to Authority Clarity together with the Role State framework of Section 4.1; **what work state has been transferred, what remains unresolved** corresponds to Content Sufficiency; and the implicit requirement that this determination be **actionable** by the party who must act on it corresponds to Receiving Capacity.

This criterion can be mapped to four governance boundary types — Knowledge, Decision, Action, and Evidence Boundary. The Work Junction crossing test in Section 4.2 (role, authority, responsibility, evidence, decision boundary) is the workflow-level operationalization of these boundaries: a Work Junction is precisely a point at which one or more governance boundary is crossed.

---

## 8. Illustrative Application

We return to the running example: **Human Product Owner → AI Business Analyst → Human Architect → AI Specification Agent → Human Reviewer.**

**Junction 1 (H2A): Product Owner → AI Business Analyst.** Role State of the Product Owner specifies intent, scope, and acceptance criteria for the analysis. Continuation Package Contract at this junction requires: research question, prioritization criteria, and explicit exclusions (H2A content, per Section 4.3's schema applied to the delegating side). This junction is not exempt from the three conditions merely because it is a delegation rather than a completion. Content Sufficiency here means the intent and scope are specific enough that the AI Business Analyst does not need to infer what "prioritize" or "relevant" means; Authority Clarity means the Product Owner has stated what the AI may decide autonomously (e.g., which sources to consult) versus what it may not (e.g., excluding a competitor from scope without flagging the exclusion); Receiving Capacity means the AI Business Analyst's Role State — its tool access, data access, and model capability — actually matches what the task requires. An underspecified Junction 1 is a textbook case of the Underspecified Delegation failure in Section 6: the Product Owner's intent, if incompletely stated, will be silently completed by inference rather than surfaced as an open question.

**Junction 2 (A2H): AI Business Analyst → Human Architect.** This is a **completion** transfer, not a failure escalation — the AI has finished; the Architect's task is to proceed to specification design, not to rescue a failed process. Continuation Package includes the analysis artifact, the evidence and data sources used, assumptions made in scoping the analysis, and open issues flagged as requiring architectural judgment. Applying the three conditions: Content Sufficiency and Authority Clarity can both be satisfied by a well-designed AI output. Receiving Capacity must additionally be checked: does this particular Architect's Role State include the domain access and authority to act on the flagged open issues, or does the analysis assume a level of infrastructure authority this Architect does not hold? If the latter, this junction is a candidate Capacity-blind transfer, and the Role Requirement Feedback Loop (Section 4.6) is triggered — either escalate to an Architect with broader authority, or have the AI Business Analyst regenerate its Continuation Package at a level the current Architect's Role State can act on.

**Junction 3 (H2A): Architect → AI Specification Agent.** A delegation junction; the Architect's own Role State (design authority, but not release authority) bounds what the Specification Agent is authorized to finalize.

**Junction 4 (A2H): AI Specification Agent → Human Reviewer.** The Continuation Package here must explicitly separate what the Specification Agent decided within its delegated authority from what it flags as exceeding that authority and requiring the Reviewer's explicit sign-off — this is the Authority Clarity condition in concrete form.

**A supplementary A2A example.** Insert an AI Validator between Junctions 3 and 4: **AI Specification Agent → AI Validator → Human Reviewer.** The Specification Agent (Generator role) and the Validator (Validation role) hold different authority — the Generator may propose; only the Validator may certify policy and risk compliance. This is a governance-relevant A2A Work Junction under the Section 4.2 test, not mere technical routing, because it crosses a responsibility boundary between generation and certification.

**Contrast with checkpoint-scoped HITL.** A traditional design would place a single human checkpoint at the end of this chain — "human reviews the final specification" — and would have no representation of Junctions 1–3, no requirement that evidence or assumptions survive from the Business Analyst through to the Reviewer, and no mechanism to detect whether the Architect at Junction 2 could actually act on what was delivered. The failure modes of Section 6, Group A and Group B alike, would be invisible to it by construction.

The same chain can be evaluated step by step as follows:

- **Junction 1 - H2A: Product Owner -> AI Business Analyst.** The delivering Role State is the Product Owner. The receiving Role State is the AI Business Analyst. Content Sufficiency requires the intent and scope to be specific enough to avoid inference. Authority Clarity requires explicit MAY / MUST NOT boundaries. Receiving Capacity requires the AI role's tool and data access to match the task. If the check fails, the Role Requirement Feedback Loop clarifies intent or restricts AI autonomy.
- **Junction 2 - A2H: AI Business Analyst -> Architect.** The delivering Role State is the AI Business Analyst. The receiving Role State is the Architect. Content Sufficiency and Authority Clarity can pass through a well-formed Continuation Package. Receiving Capacity must still verify domain and infrastructure authority. If the check fails, the workflow either reassigns the role or reformats the package.
- **Junction 3 - H2A: Architect -> AI Specification Agent.** The delivering Role State is the Architect. The receiving Role State is the AI Specification Agent. Content Sufficiency requires design intent specific enough for specification work. Authority Clarity requires design authority to be separated from release authority. Receiving Capacity requires the Specification Agent's scope to match the task. If the check fails, the loop clarifies or restricts the delegation.
- **Junction 3a - A2A: AI Specification Agent -> AI Validator.** The delivering Role State is the AI Specification Agent acting as Generator. The receiving Role State is the AI Validator. Content Sufficiency can pass, but Authority Clarity must separate proposed output from certified output. Receiving Capacity checks validator policy/risk scope and certification authority. If the check fails, the contract must enforce separation and verifier capacity.
- **Junction 4 - A2H: AI Specification Agent / AI Validator -> Reviewer.** The delivering Role State is the Specification Agent or Validator. The receiving Role State is the Reviewer. Content Sufficiency and Authority Clarity can pass, but Receiving Capacity must verify the sign-off mandate. If the check fails, the loop reassigns the receiver or reformats the package.

---

## 9. Implications

### 9.1 For AI Governance Practice

A governance checklist for enterprise AI deployment should verify all three conditions of Section 5 at every Work Junction, not only Content Sufficiency and Authority Clarity. Receiving Capacity verification requires an explicit step — checking the transferred work against the actual Role State of the specific individual or team receiving it — that most current HITL implementations do not include.

### 9.2 For Human Role Redefinition

Industry practice has begun asserting that AI deployment requires new human roles, typically by direct enumeration from observed organizational experience (e.g., "Agent Supervisor," "Exception Handler"). What is absent from this practice is a principled derivation: no existing framework treats human role redefinition as an output of a prior, formalized structure. This paper reverses the sequence for a subset of the problem: rather than asserting new roles directly, the Role Requirement Feedback Loop (Section 4.6) derives **when and how** an existing role's requirements must be revised, as a consequence of observed Capacity-blind transfer failures at specific Work Junctions — providing a mechanism, not merely a conclusion.

### 9.3 For Enterprise AI System Design

The Continuation Package Contract (Section 4.3) can serve as a design artifact for API and interface specifications between AI systems and downstream human or agentic consumers, independent of the underlying orchestration engine (BPMN-based, LangGraph-based, or Agent SDK-based).

---

## 10. Limitations and Future Work

This is a conceptual and structural paper in the tradition of integrative theory development; it does not present empirical validation. Three directions for future work follow directly from this limitation: (1) case studies applying the three-condition test to real enterprise AI deployments, to assess how often Capacity-blind transfer occurs and whether it is currently undetected in practice; (2) standardization of Continuation Package Contract field schemas across common enterprise workflow types; and (3) mapping this model's constructs onto specific orchestration frameworks (e.g., BPMN-based agentic orchestration, LangGraph, Agent SDKs) to determine what additional engineering support would be required to make Receiving Capacity verification operationally checkable, not merely conceptually required.

---

## 11. Conclusion

Human-in-the-Loop, scoped to the checkpoint, answers the question of when a human should be asked to act. It does not answer the question of whether that human can act on what is placed in front of them. This paper has argued that the second question, not the first, is what enterprise AI governance actually requires, and that answering it requires treating human role design, AI delivery format, and workflow junction structure as jointly determined rather than independently specified. A Continuation Package is what makes the intervention governable rather than ceremonial.

---

## AI Assistance Disclosure

This manuscript was developed with AI-assisted drafting, editing, formatting, and literature cross-checking. The author selected the research question, conceptual framing, model definitions, examples, references to include, and final wording, and remains responsible for all claims, citations, analysis, and conclusions.

---

## Appendix A: Continuation Package Contract — Field Specification

- **Artifact** (Always): the produced output, such as a document, code artifact, decision draft, or analysis.
- **Work State** (Always): completed versus remaining work at this junction.
- **Evidence** (Content Sufficiency): data sources and basis for conclusions.
- **Assumptions** (Content Sufficiency): explicit assumptions made in producing the artifact.
- **Authority Context** (Authority Clarity): what the delivering actor was, and was not, authorized to decide.
- **Open Issues** (Content Sufficiency): unresolved questions, exceptions, and flagged risks.
- **Required Next Action** (Authority Clarity): what the receiving actor must do.
- **Recommended Receiving Role** (Receiving Capacity input): the Role State profile the package assumes on the receiving side.
- **Acceptance Condition** (Authority Clarity): what constitutes successful continuation at this junction.

## Appendix B: Running Example — Work Junction Inventory

- **Junction 1 (H2A).** Delivering Role State: Product Owner with intent, scope, and acceptance criteria. Receiving Role State: AI Business Analyst. Continuation Readiness check: intent-completeness to avoid Ghost Intent, scope authority, and tool/data access.
- **Junction 2 (A2H).** Delivering Role State: AI Business Analyst. Receiving Role State: Architect. Continuation Readiness check: Content yes, Authority yes, and Capacity verification for domain access.
- **Junction 3 (H2A).** Delivering Role State: Architect with design authority. Receiving Role State: AI Specification Agent. Continuation Readiness check: design-intent completeness, MAY/MUST NOT boundary, and agent capability match.
- **Junction 3a, supplementary (A2A).** Delivering Role State: AI Specification Agent as Generator. Receiving Role State: AI Validator. Continuation Readiness check: Content yes, Authority yes, and Capacity verification for validator scope and certification authority.
- **Junction 4 (A2H).** Delivering Role State: AI Specification Agent / AI Validator. Receiving Role State: Reviewer. Continuation Readiness check: Content yes, Authority yes, and Capacity verification for sign-off mandate.

---

## AI Assistance Disclosure

The author used AI tools for drafting assistance, language refinement, structural review, and citation-checking support. The author independently developed the paper’s concepts, reviewed and revised the arguments, verified references where possible, and is solely responsible for the final text, analysis, claims, and conclusions.

---

## References

Ait, A., Cánovas Izquierdo, J. L., & Cabot, J. (2025). Towards Modeling Human-Agentic Collaborative Workflows: A BPMN Extension. In D. Taibi & D. Smite (Eds.), **Software Engineering and Advanced Applications** (SEAA 2025), 367–382. Springer. https://doi.org/10.1007/978-3-032-04190-6_22. (Also available as arXiv:2412.05958).

Cheng, E. C., & Cheng, J. (2026). **A Decoupled Human-in-the-Loop System for Controlled Autonomy in Agentic Workflows**. arXiv:2604.23049.

Chiodo, M., Müller, D., Siewert, P., Wetherall, J.-L., Yasmine, Z., & Burden, J. (2025). **Formalising Human-in-the-Loop: Computational Reductions, Failure Modes, and Legal-Moral Responsibility**. arXiv:2505.10426.

Cummings, M. L. (2004). Automation Bias in Intelligent Time Critical Decision Support Systems. **AIAA 1st Intelligent Systems Technical Conference**. https://doi.org/10.2514/6.2004-6313

Engin, Z. (2025, revised 2026). **Human-AI Governance (HAIG): A Trust-Utility Approach**. arXiv:2505.01651.

Fitts, P. M. (Ed.). (1951). **Human Engineering for an Effective Air-Navigation and Traffic-Control System**. National Research Council, Committee on Aviation Psychology.

Hollnagel, E., & Woods, D. D. (2005). **Joint Cognitive Systems: Patterns in Cognitive Systems Engineering**. CRC Press.

LangChain. (2026). **Interrupts**. LangGraph Documentation. Accessed August 9, 2026.

OpenAI. (2026). **Handoffs**. OpenAI Agents SDK Documentation. Accessed August 9, 2026.

Natarajan, S., Mathur, S., Sidheekh, S., Stammer, W., & Kersting, K. (2025). Human-in-the-Loop or AI-in-the-Loop? Automate or Collaborate? **Proceedings of the AAAI Conference on Artificial Intelligence**, 39(27), 28594–28600. (Also available as arXiv:2412.14232).

Ortenzi, V., Cosgun, A., Pardi, T., Chan, W. P., Croft, E., & Kulić, D. (2020). Object Handovers: A Review for Robotics. **IEEE Transactions on Robotics**, 37(6), 1855–1873.

Xu, W., & Gao, Z. (2024). Applying human-centered AI in developing effective human-AI teaming: A perspective of human-AI joint cognitive systems. **Interactions**, 31(1), 32–37. https://doi.org/10.1145/3635116
