# Research Paper Glossary

## Alphabetical Index

### A

- [Anchor](#anchor)
- [Anchor Architecture](#anchor-architecture)
- [Anchor-less State](#anchor-less-state)
- [Authorless Traceability Collapse (ATC)](#authorless-traceability-collapse)

### B

- [Behavioral Drift](#behavioral-drift)
- [Boundary Evidence](#boundary-evidence)
- [Boundary Vacuum](#boundary-vacuum)

### C

- [Compliance Vacuum](#compliance-vacuum)

### D

- [Debug Cost Inversion](#debug-cost-inversion)
- [Decidable Governance](#decidable-governance)
- [Decision Authorization](#decision-authorization)
- [Decision Behavior](#decision-behavior)
- [Decision Behavior Governance](#decision-behavior-governance)
- [Decision Boundary Collapse](#decision-boundary-collapse)
- [Decision Formation](#decision-formation)
- [Decision Friction](#decision-friction)
- [Decision Premise](#decision-premise)
- [Decision Provenance](#decision-provenance)
- [Decision Traceability](#decision-traceability)
- [Decision Vacancy](#decision-vacancy)
- [Deployment Governance](#deployment-governance)
- [Development Governance](#development-governance)
- [Due Diligence](#due-diligence)

### E

- [Engineering-Stage Governance](#engineering-stage-governance)
- [Epistemic Opacity](#epistemic-opacity)
- [Evidence Sovereignty](#evidence-sovereignty)

### G

- [Ghost Code](#ghost-code)
- [Ghost Intent](#ghost-intent)
- [Governance Blind Spot](#governance-blind-spot)
- [Governance Context](#governance-context)
- [Governance Evidence](#governance-evidence)
- [Governance Existence](#governance-existence)
- [Governance Invocation](#governance-invocation)
- [Governance Nullity](#governance-nullity)

### H

- [Human Involvement Ratio (HIR)](#human-involvement-ratio)

### I

- [Inference Creep](#inference-creep)
- [Intent Anchors](#intent-anchors)
- [Intent Evaporation](#intent-evaporation)

### M

- [Model Alignment Boundary](#model-alignment-boundary)
- [Model Governance](#model-governance)

### O

- [Operation Governance](#operation-governance)

### P

- [Pre-Analytical Anchoring](#pre-analytical-anchoring)
- [Prohibitive Constraints](#prohibitive-constraints)

### R

- [Relationship](#relationship)
- [Resolvability](#resolvability)
- [Risk Acceleration Pipeline](#risk-acceleration-pipeline)
- [Runtime Governance](#runtime-governance)

### S

- [Spatiotemporal Coordinate](#spatiotemporal-coordinate)
- [Structural Examinability](#structural-examinability)

### T

- [Task Execution Boundary](#task-execution-boundary)
- [Traceability Assumption Failure](#traceability-assumption-failure)

### V

- [Visible Scope](#visible-scope)

---

## Concept Map

### Decision Phenomenon

- <a id="behavioral-drift"></a> Behavioral Drift
    > A shift in how a model interprets or applies constraints over time without explicit premise changes. Detecting it depends on accumulated governance evidence.
    *Origin*: [Decision Behavior Governance](manuscripts/2026-01_decision-behavior-governance-at-the-engineering-stage_v1.0.md)

#### Ghost Intent

- <a id="ghost-intent"></a> Ghost Intent
    > A condition where software remains behaviorally functional, but the original engineering rationale for structure and trade-offs is no longer recoverable.
    *Origin*: [Ghost Intent](manuscripts/2026-03_ghost-intent-an-effect-of-traceability-collapse-in-genai-assisted-sdlcs_v1.0.md)
- <a id="authorless-traceability-collapse"></a> Authorless Traceability Collapse (ATC)
    > A structural collapse in which traceability records still exist but no longer preserve decision intent, because human authorship continuity is missing.
    *Origin*: [Ghost Intent](manuscripts/2026-03_ghost-intent-an-effect-of-traceability-collapse-in-genai-assisted-sdlcs_v1.0.md)
- <a id="intent-evaporation"></a> Intent Evaporation
    > The progressive loss of decision context after AI-assisted generation, leaving artifacts without stable explanatory rationale.
    *Origin*: [Ghost Intent](manuscripts/2026-03_ghost-intent-an-effect-of-traceability-collapse-in-genai-assisted-sdlcs_v1.0.md)
- <a id="debug-cost-inversion"></a> Debug Cost Inversion
    > A reversal where generation becomes faster while debugging and diagnosis effort grows disproportionately over time.
    *Origin*: [Ghost Intent](manuscripts/2026-03_ghost-intent-an-effect-of-traceability-collapse-in-genai-assisted-sdlcs_v1.0.md)
- <a id="decision-provenance"></a> Decision Provenance
    > Traceable lineage of why a decision was formed, including constraints, alternatives, and boundary choices behind artifacts.
    *Origin*: [Ghost Intent](manuscripts/2026-03_ghost-intent-an-effect-of-traceability-collapse-in-genai-assisted-sdlcs_v1.0.md)
- <a id="intent-anchors"></a> Intent Anchors
    > Stable references that connect code artifacts to the decisions that shaped them, so rationale stays navigable during evolution.
    *Origin*: [Ghost Intent](manuscripts/2026-03_ghost-intent-an-effect-of-traceability-collapse-in-genai-assisted-sdlcs_v1.0.md)
- <a id="anchor-less-state"></a> Anchor-less State
    > A state where artifacts persist without durable links to original decision coordinates, making reverse reconstruction unreliable.
    *Origin*: [Ghost Intent](manuscripts/2026-03_ghost-intent-an-effect-of-traceability-collapse-in-genai-assisted-sdlcs_v1.0.md)
- <a id="traceability-assumption-failure"></a> Traceability Assumption Failure
    > Failure of the traditional SDLC assumption that intent is naturally durable and recoverable from commits, reviews, and documents.
    *Origin*: [Ghost Intent](manuscripts/2026-03_ghost-intent-an-effect-of-traceability-collapse-in-genai-assisted-sdlcs_v1.0.md)
- <a id="epistemic-opacity"></a> Epistemic Opacity
    > A condition where system behavior is observable but the underlying decision logic is not institutionally intelligible to maintainers.
    *Origin*: [Ghost Intent](manuscripts/2026-03_ghost-intent-an-effect-of-traceability-collapse-in-genai-assisted-sdlcs_v1.0.md)

---

#### Inference Creep

- <a id="inference-creep"></a> Inference Creep
    > AI-driven expansion of change scope beyond explicit human instruction while outputs remain technically valid. The risk is governance drift rather than immediate functional failure.
    *Origin*: [From Inference Creep to Risk Acceleration Pipelines](manuscripts/2026-01_from-inference-creep-to-risk-acceleration-pipelines_v1.0.md)
- <a id="ghost-code"></a> Ghost Code
    > Code that appears stable in repository history but cannot be traced to explicit human decisions or requirements. It preserves behavior while losing accountable intent.
    *Origin*: [From Inference Creep to Risk Acceleration Pipelines](manuscripts/2026-01_from-inference-creep-to-risk-acceleration-pipelines_v1.0.md)
- <a id="risk-acceleration-pipeline"></a> Risk Acceleration Pipeline
    > A chained automation path (such as Auto PR, Auto Merge, Auto Deploy) that amplifies governance risk by outpacing explicit decisions. It shifts systems toward incident-driven rather than decision-driven operation.
    *Origin*: [From Inference Creep to Risk Acceleration Pipelines](manuscripts/2026-01_from-inference-creep-to-risk-acceleration-pipelines_v1.0.md)
- <a id="human-involvement-ratio"></a> Human Involvement Ratio (HIR)
    > An auditable metric comparing human review involvement to the share of AI-generated changes. Low HIR under high AI contribution signals potential decision vacancy.
    *Origin*: [From Inference Creep to Risk Acceleration Pipelines](manuscripts/2026-01_from-inference-creep-to-risk-acceleration-pipelines_v1.0.md)
- <a id="governance-blind-spot"></a> Governance Blind Spot
    > A condition where quality checks pass but decision accountability is missing or obscured. It explains why technically valid pipelines can still be governance-unsafe.
    *Origin*: [From Inference Creep to Risk Acceleration Pipelines](manuscripts/2026-01_from-inference-creep-to-risk-acceleration-pipelines_v1.0.md)

---

### Core Concept

#### Governance Stage

- <a id="model-governance"></a> Model Governance
    > Governance practices that focus on the general behavior and safety characteristics of AI models prior to integration into organizational systems.
    *Origin*: [Four Stages of AI Governance](manuscripts/2026-01_four-stages-of-ai-governance_v1.0.md)
- <a id="development-governance"></a> Development Governance
    > Governance applied during the development stage that structures how AI-assisted decisions will be formed through constraints, rules, and design assumptions.
    *Origin*: [Four Stages of AI Governance](manuscripts/2026-01_four-stages-of-ai-governance_v1.0.md)
- <a id="deployment-governance"></a> Deployment Governance
    > Governance mechanisms that determine which AI systems or configurations are authorized to operate in a given environment.
    *Origin*: [Four Stages of AI Governance](manuscripts/2026-01_four-stages-of-ai-governance_v1.0.md)
- <a id="operation-governance"></a> Operation Governance
    > Governance applied during system execution that monitors behavior, collects evidence, and detects anomalies.
    *Origin*: [Four Stages of AI Governance](manuscripts/2026-01_four-stages-of-ai-governance_v1.0.md)
- <a id="runtime-governance"></a> Runtime Governance
    > Governance that intervenes during execution by monitoring, filtering, or blocking outputs after decisions are formed. It governs operational behavior, not the decision formation structure itself.
    *Origin*: [Runtime Governance vs. Development Governance](manuscripts/2026-01_runtime-governance-vs-development-governance_v1.0.md)
- <a id="governance-existence"></a> Governance Existence
    > The ex-ante condition in which decision boundaries are defined and authorized before execution starts. It shows that governance is structurally present even when no runtime event is triggered.
    *Origin*: [Runtime Governance vs. Development Governance](manuscripts/2026-01_runtime-governance-vs-development-governance_v1.0.md)
- <a id="governance-invocation"></a> Governance Invocation
    > The ex-post activation of governance mechanisms during execution, such as interception or policy-triggered blocking. Invocation responds to events and presupposes prior governance existence.
    *Origin*: [Runtime Governance vs. Development Governance](manuscripts/2026-01_runtime-governance-vs-development-governance_v1.0.md)

---

#### Decision Behavior

- <a id="engineering-stage-governance"></a> Engineering-Stage Governance
    > Governance established before execution as a structural condition of decision formation. It emphasizes ex-ante boundaries rather than ex-post correction.
    *Origin*: [Realizing ISO/IEC 42001](manuscripts/2026-01_realizing-ISO-IEC-42001-through-decision-behavior-governance_v1.0.md)
- <a id="decision-formation"></a> Decision Formation
    > The stage where an AI-assisted system composes and selects a decision under given premises and constraints. In this research system, it is the primary governance target.
    *Origin*: [Runtime Governance vs. Development Governance](manuscripts/2026-01_runtime-governance-vs-development-governance_v1.0.md)
- <a id="decision-behavior"></a> Decision Behavior
    > The process through which an AI-assisted agent composes premises, applies constraints, and forms outcomes with organizational impact. In this system, behavior is the primary governance target rather than output artifacts alone.
    *Origin*: [Decision Behavior Governance](manuscripts/2026-01_decision-behavior-governance-at-the-engineering-stage_v1.0.md)
- <a id="decision-premise"></a> Decision Premise
    > The authorized knowledge base and legitimacy boundary that defines what a decision is allowed to rely on. It sets ex-ante scope for acceptable decision formation.
    *Origin*: [Decision Behavior Governance](manuscripts/2026-01_decision-behavior-governance-at-the-engineering-stage_v1.0.md)
- <a id="decision-vacancy"></a> Decision Vacancy
    > A governance condition where execution proceeds without clearly attributable human decision-making. It marks a gap between operational action and accountable authorization.
    *Origin*: [From Inference Creep to Risk Acceleration Pipelines](manuscripts/2026-01_from-inference-creep-to-risk-acceleration-pipelines_v1.0.md)
- <a id="decision-boundary-collapse"></a> Decision Boundary Collapse
    > The structural collapse where analysis and execution occur in the same automated action. Inference is silently substituted for explicit human choice.
    *Origin*: [From Inference Creep to Risk Acceleration Pipelines](manuscripts/2026-01_from-inference-creep-to-risk-acceleration-pipelines_v1.0.md)
- <a id="decision-friction"></a> Decision Friction
    > Deliberate governance resistance added at critical boundaries to force explicit review and authorization. It preserves decision visibility without rejecting automation.
    *Origin*: [From Inference Creep to Risk Acceleration Pipelines](manuscripts/2026-01_from-inference-creep-to-risk-acceleration-pipelines_v1.0.md)
- <a id="decision-traceability"></a> Decision Traceability
    > The ability to trace how a decision was formed, including applied premises and constraints. It supports auditability, accountability, and legal review.
    *Origin*: [Realizing ISO/IEC 42001](manuscripts/2026-01_realizing-ISO-IEC-42001-through-decision-behavior-governance_v1.0.md)
- <a id="due-diligence"></a> Due Diligence
    > In this framework, due diligence means demonstrating that decisions were formed within an institutionally authorized governance context. It is not equivalent to "no incidents occurred."
    *Origin*: [Realizing ISO/IEC 42001](manuscripts/2026-01_realizing-ISO-IEC-42001-through-decision-behavior-governance_v1.0.md)
- <a id="decision-authorization"></a> Decision Authorization
    > The governed definition and versioning of what decisions are institutionally allowed. In this paper, it is central to the PDCA reinterpretation at the engineering stage.
    *Origin*: [Realizing ISO/IEC 42001](manuscripts/2026-01_realizing-ISO-IEC-42001-through-decision-behavior-governance_v1.0.md)

---

### Governance

- <a id="decision-behavior-governance"></a> Decision Behavior Governance
    > A governance approach that constrains how decisions are formed before execution, rather than only checking outcomes after they appear. It targets attributable decision formation conditions.
    *Origin*: [Runtime Governance vs. Development Governance](manuscripts/2026-01_runtime-governance-vs-development-governance_v1.0.md)
- <a id="governance-evidence"></a> Governance Evidence
    > The traceable residue of decision formation, such as constraint references and execution traces. It supports validity checks, auditability, and institutional learning.
    *Origin*: [Decision Behavior Governance](manuscripts/2026-01_decision-behavior-governance-at-the-engineering-stage_v1.0.md)
- <a id="evidence-sovereignty"></a> Evidence Sovereignty
    > The organizational ability to establish and analyze authoritative traces of how decisions were formed. It becomes critical when model internals are opaque or externally controlled.
    *Origin*: [Decision Behavior Governance](manuscripts/2026-01_decision-behavior-governance-at-the-engineering-stage_v1.0.md)
- <a id="governance-nullity"></a> Governance Nullity
    > A state where a decision cannot be attributed to an identifiable governance regime, even if procedural compliance artifacts exist. It marks behavioral non-governance under administrative completeness.
    *Origin*: [Decision Behavior Governance](manuscripts/2026-01_decision-behavior-governance-at-the-engineering-stage_v1.0.md)
- <a id="governance-context"></a> Governance Context
    > The identifiable set of premises, constraints, and legitimacy boundaries under which a decision is formed. Attributability depends on linking a decision to this context.
    *Origin*: [Realizing ISO/IEC 42001](manuscripts/2026-01_realizing-ISO-IEC-42001-through-decision-behavior-governance_v1.0.md)
- <a id="compliance-vacuum"></a> Compliance Vacuum
    > A state where documentation is complete but decision formation cannot be shown to occur within an identifiable governance context. It marks the gap between administrative completeness and behavioral control.
    *Origin*: [Realizing ISO/IEC 42001](manuscripts/2026-01_realizing-ISO-IEC-42001-through-decision-behavior-governance_v1.0.md)
- <a id="decidable-governance"></a> Decidable Governance
    > Governance in which boundary violations can be checked with clear pass/fail criteria at runtime. It depends on explicit prohibitions rather than interpretive post-hoc narratives.
    *Origin*: [Execution Boundary](manuscripts/2026-02_boundary-as-an-execution-time-primitive-v1.0.md)

---

### Framework

#### Anchor Architecture

- <a id="anchor-architecture"></a> Anchor Architecture
    > A minimal structural foundation that makes traceability deterministic by binding artifacts to coordinates before analysis. It is model-independent and does not depend on semantic interpretation.
    *Origin* [Anchor Architecture](manuscripts/2026-02_anchor-architecture_v1.0.md)
- <a id="anchor"></a> Anchor
    > A spatiotemporal coordinate that binds identity, location, and time to an artifact state. It defines where and when content can be resolved.
    *Origin* [Anchor Architecture](manuscripts/2026-02_anchor-architecture_v1.0.md)
- <a id="relationship"></a> Relationship
    > A directed structural adjacency between anchors used to form traceable paths. Meaning labels such as implements or tests are applied at higher layers, not in the primitive itself.
    *Origin* [Anchor Architecture](manuscripts/2026-02_anchor-architecture_v1.0.md)
- <a id="spatiotemporal-coordinate"></a> Spatiotemporal Coordinate
    > The coordinate form combining identity, location, and temporal index for deterministic reference. It separates persistent identity from versioned state.
    *Origin* [Anchor Architecture](manuscripts/2026-02_anchor-architecture_v1.0.md)
- <a id="pre-analytical-anchoring"></a> Pre-Analytical Anchoring
    > The requirement that anchors exist at creation time rather than being reconstructed later. Without it, traceability becomes speculative.
    *Origin* [Anchor Architecture](manuscripts/2026-02_anchor-architecture_v1.0.md)
- <a id="structural-examinability"></a> Structural Examinability
    > The condition under which artifact states and relations can be checked deterministically across time. It depends on resolvable coordinates, not post-hoc narratives.
    *Origin* [Anchor Architecture](manuscripts/2026-02_anchor-architecture_v1.0.md)
- <a id="resolvability"></a> Resolvability
    > The ability to retrieve artifact content from a declared coordinate. It is a binary prerequisite for structural validity checks.
    *Origin* [Anchor Architecture](manuscripts/2026-02_anchor-architecture_v1.0.md)

---

#### Boundary

- <a id="task-execution-boundary"></a> Task Execution Boundary
    > The resolved permissible action space for a specific task at execution time, defined by what the model can see and what it is explicitly forbidden to do. It is a runtime governance primitive, not a training-time property.
    *Origin*: [Execution Boundary](manuscripts/2026-02_boundary-as-an-execution-time-primitive-v1.0.md)
- <a id="model-alignment-boundary"></a> Model Alignment Boundary
    > Statistical safety tendencies established during training (for example RLHF and safety tuning) that generalize across tasks. They reduce harmful output likelihood but do not define task-specific engineering permission.
    *Origin*: [Execution Boundary](manuscripts/2026-02_boundary-as-an-execution-time-primitive-v1.0.md)
- <a id="boundary-evidence"></a> Boundary Evidence
    > The minimal auditable record of boundary state at execution time, including visible scope, explicit constraints, and execution outputs. It enables reproducibility and accountable verification.
    *Origin*: [Execution Boundary](manuscripts/2026-02_boundary-as-an-execution-time-primitive-v1.0.md)
- <a id="visible-scope"></a> Visible Scope
    > The set of artifacts accessible to the model in a task instance, such as code, tests, specs, and goals. Scope determines what can be observed, not what is permitted.
    *Origin*: [Execution Boundary](manuscripts/2026-02_boundary-as-an-execution-time-primitive-v1.0.md)
- <a id="prohibitive-constraints"></a> Prohibitive Constraints
    > Explicit MUST NOT rules that define non-negotiable no-go zones for execution. In this framework, they provide the primary source of decidability in governance.
    *Origin*: [Execution Boundary](manuscripts/2026-02_boundary-as-an-execution-time-primitive-v1.0.md)
- <a id="boundary-vacuum"></a> Boundary Vacuum
    > A state where no decidable task boundary is established for execution. In this condition, model-level preferences dominate and governance claims become hard to verify objectively.
    *Origin*: [Execution Boundary](manuscripts/2026-02_boundary-as-an-execution-time-primitive-v1.0.md)
