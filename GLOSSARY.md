# Research Paper Glossary

## Alphabetical Index

### A

- [Anchor](#anchor)
- [Anchor Architecture](#anchor-architecture)
- [Anchor-less State](#anchor-less-state)
- [Application Ruleset](#application-ruleset)
- [Artifact Scope](#artifact-scope)
- [Authorial Discontinuity](#authorial-discontinuity)
- [Authorless Traceability Collapse (ATC)](#authorless-traceability-collapse)

### B

- [Behavior Rule Architecture (BRA)](#behavior-rule-architecture)
- [Behavioral Drift](#behavioral-drift)
- [Boundary Evidence](#boundary-evidence)
- [Boundary Formation](#boundary-formation)
- [Boundary Vacuum](#boundary-vacuum)

### C

- [Category Ruleset](#category-ruleset)
- [Compliance Vacuum](#compliance-vacuum)
- [Constraint (MUST NOT)](#constraint-must-not)
- [Context Overload](#context-overload)

### D

- [DA-I (Indeterminate)](#da-i)
- [DA-N (Normal)](#da-n)
- [DA-O (Over Outcome)](#da-o)
- [DA-U (Unobservable)](#da-u)
- [DA-V (Decision Vacancy)](#da-v)
- [Debug Cost Inversion](#debug-cost-inversion)
- [Decidable Governance](#decidable-governance)
- [Decision Authorization](#decision-authorization)
- [Decision Behavior](#decision-behavior)
- [Decision Behavior Governance](#decision-behavior-governance)
- [Decision Behavior Normative Category](#decision-behavior-normative-category)
- [Decision Boundary Collapse](#decision-boundary-collapse)
- [Decision Effect](#decision-effect)
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

- [Effect-First Principle](#effect-first-principle)
- [Engineering-Stage Governance](#engineering-stage-governance)
- [Epistemic Opacity](#epistemic-opacity)
- [Evidence Sovereignty](#evidence-sovereignty)
- [Execution View](#execution-view)

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
- [Intent Fragmentation](#intent-fragmentation)

### M

- [Model Alignment Boundary](#model-alignment-boundary)
- [Model Governance](#model-governance)
- [Multi-Viewpoint](#multi-viewpoint)

### N

- [Normative Natural Language (NNL)](#normative-natural-language)

### O

- [Operation Governance](#operation-governance)
- [Outcome Scope](#outcome-scope)

### P

- [Policy (MUST)](#policy-must)
- [Pre-Analytical Anchoring](#pre-analytical-anchoring)
- [Prohibitive Constraints](#prohibitive-constraints)

### R

- [Relationship](#relationship)
- [Resolvability](#resolvability)
- [Risk Acceleration Pipeline](#risk-acceleration-pipeline)
- [Risk Potential](#risk-potential)
- [Rule (BRA)](#rule-bra)
- [Rule Library](#rule-library)
- [Rule Normative Language (RNL)](#rule-normative-language)
- [Runtime Governance](#runtime-governance)

### S

- [Semantic Conflict Detection](#semantic-conflict-detection)
- [Semantic Conflation](#semantic-conflation)
- [Semantic Drift](#semantic-drift)
- [Spatiotemporal Coordinate](#spatiotemporal-coordinate)
- [Structural Examinability](#structural-examinability)
- [Structural Scope Audit](#structural-scope-audit)

### T

- [Task Execution Boundary](#task-execution-boundary)
- [Traceability Assumption Failure](#traceability-assumption-failure)

### V

- [Viewpoint](#viewpoint)
- [Viewpoint-Structured Specification (VSS)](#viewpoint-structured-specification)
- [Visibility Inversion Principle](#visibility-inversion-principle)
- [Visible Scope](#visible-scope)

---

## Concept Map

### Decision Phenomenon

- <a id="behavioral-drift"></a> Behavioral Drift
    > A shift in how a model interprets or applies constraints over time without explicit premise changes. Detecting it depends on accumulated governance evidence.
    *Origin*: [Decision Behavior Governance](manuscripts/2026-01_decision-behavior-governance-at-the-engineering-stage_v1.0.md)
- <a id="authorial-discontinuity"></a> Authorial Discontinuity
    > The structural absence of a recoverable chain connecting each prompt-driven generation event to the Intent that authorized it. It results from the stateless, single-use nature of prompts as a specification artifact class.
    *Origin*: [Viewpoint-Structured Specification](manuscripts/2026-03_viewpoint-structured-specification_v1.0.md)
- <a id="visibility-inversion-principle"></a> Visibility Inversion Principle
    > The principle that conflict detection probability decreases as generation proceeds deeper into implementation layers, while resolution cost increases proportionally. It motivates pre-coding conflict surfacing as the primary VSS intervention.
    *Origin*: [Viewpoint-Structured Specification](manuscripts/2026-03_viewpoint-structured-specification_v1.0.md)
- <a id="intent-fragmentation"></a> Intent Fragmentation
    > The dispersal of Intent across unrelated artifacts such that it cannot function as a coherent governing constraint over code generation. It compounds upstream governance failure when no structured decomposition precedes generation.
    *Origin*: [Viewpoint-Structured Specification](manuscripts/2026-03_viewpoint-structured-specification_v1.0.md)
- <a id="semantic-conflation"></a> Semantic Conflation
    > The fundamental failure mode of current AI behavior governance approaches, where three distinct concerns—system intent, boundary constraints, and behavior normatives—are merged into natural language expressions. AI cannot reliably distinguish their normative force, leading to semantic drift, context overload, and rule conflicts.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="semantic-drift"></a> Semantic Drift
    > A failure mode where AI interprets behavioral constraints expressed as natural language suggestions as optional guidelines rather than mandatory requirements. Over time, as context accumulates and attention dilutes, AI progressively relaxes these constraints. Root cause is the absence of normative keywords signaling enforcement semantics.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="context-overload"></a> Context Overload
    > A failure mode where accumulated instructions, prompts, and configurations consume the AI's context window capacity, causing attention dilution and critical rules to be ignored. It results from the absence of systematic mechanisms for rule prioritization, conflict resolution, or contextual activation.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)

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
- <a id="boundary-formation"></a> Boundary Formation
    > The emergent capacity to form a human-determined subset selection from a versioned Structured Specification as the governing context for a code generation event. It is a consequence of unitization, not an added mechanism.
    *Origin*: [Viewpoint-Structured Specification](manuscripts/2026-03_viewpoint-structured-specification_v1.0.md)

---

#### Viewpoint-Structured Specification

- <a id="viewpoint-structured-specification"></a> Viewpoint-Structured Specification (VSS)
    > A structural framework that decomposes Intent into a versioned, multi-viewpoint Specification prior to AI-assisted code generation. It provides the pre-coding structural basis for governed, traceable generation.
    *Origin*: [Viewpoint-Structured Specification](manuscripts/2026-03_viewpoint-structured-specification_v1.0.md)
- <a id="viewpoint"></a> Viewpoint
    > A declared semantic boundary representing a specific concern, constraint, or intent in a system. It is the foundational structural unit through which Intent is decomposed in VSS.
    *Origin*: [Viewpoint-Structured Specification](manuscripts/2026-03_viewpoint-structured-specification_v1.0.md)
- <a id="multi-viewpoint"></a> Multi-Viewpoint
    > The structural requirement in VSS that Intent be expressed across multiple declared Viewpoints, each assumed by an AI acting in a distinct role. The deliberative tension between roles is the mechanism through which latent conflicts in Intent become structurally observable before code generation.
    *Origin*: [Viewpoint-Structured Specification](manuscripts/2026-03_viewpoint-structured-specification_v1.0.md)
- <a id="semantic-conflict-detection"></a> Semantic Conflict Detection
    > The structural observability of incompatible constraints between elements from different Viewpoints, made possible by multi-viewpoint structuring before code generation begins. It surfaces latent Intent conflicts at the point where resolution cost is lowest.
    *Origin*: [Viewpoint-Structured Specification](manuscripts/2026-03_viewpoint-structured-specification_v1.0.md)

---

#### Decision Analysis

- <a id="decision-effect"></a> Decision Effect
    > A detectable state deviation between system states before and after a generation event. It serves as the unified analytical entry point for scope authorization analysis, independent of intent assumptions or outcome correctness.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)
- <a id="artifact-scope"></a> Artifact Scope
    > The set of code-layer anchors identified as the intended modification targets for a generation event, established either by direct human specification or by AI derivation through structural relations from the Visible Scope.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)
- <a id="outcome-scope"></a> Outcome Scope
    > The set of anchors whose content was actually modified during execution, determined after the generation event by observation. It is the structural fact against which scope authorization is evaluated.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)
- <a id="effect-first-principle"></a> Effect-First Principle
    > The analytical constraint that scope analysis must begin from observable effect rather than intent assumptions or outcome evaluation. It is a structural necessity in AI-assisted environments where generation reasoning is not introspectable.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)
- <a id="structural-scope-audit"></a> Structural Scope Audit
    > An automated, pre-merge determination of whether a generation event remained within its authorized scope, expressed as set-membership queries over Anchor Sets without requiring semantic understanding of the generated code.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)
- <a id="da-n"></a> DA-N (Normal)
    > An analytical state in which all observable modifications fall within the Artifact Scope and the Artifact Scope is structurally reachable from the Visible Scope. No scope anomaly is detected.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)
- <a id="da-o"></a> DA-O (Over Outcome)
    > An analytical state in which observable modifications extend beyond the Artifact Scope. It identifies the structural fact of scope exceedance without evaluating the correctness or governance implications of the excess modifications.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)
- <a id="da-i"></a> DA-I (Indeterminate)
    > An analytical state in which scope-exceeding modifications can be traced to multiple specification-layer anchors with no unique attribution. It identifies attribution instability without resolving which source drove the modification.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)
- <a id="da-v"></a> DA-V (Decision Vacancy)
    > An analytical state in which scope-exceeding modifications cannot be traced to any known anchor in the system. It provides the formal structural detection criterion for Ghost Intent.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)
- <a id="da-u"></a> DA-U (Unobservable)
    > An analytical state in which no observable modification is detected, terminating analysis without state determination. It marks the analytical boundary beyond which scope authorization cannot be assessed.
    *Origin*: [Decision Analysis](manuscripts/2026-03_decision-analysis_v1.0.md)

---

#### Behavior Rule Architecture

- <a id="behavior-rule-architecture"></a> Behavior Rule Architecture (BRA)
    > A structured framework for defining and managing AI execution behavior through normative rules. BRA establishes a clear separation between Normative Natural Language (NNL) for intent expression and Rule Normative Language (RNL) for behavior enforcement using MUST/MUST NOT semantics. It comprises three layers: Rule Language Layer, Rule Architecture Layer, and Governance Asset Layer.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="normative-natural-language"></a> Normative Natural Language (NNL)
    > Human-readable natural language used to express task intent and operational descriptions. NNL is non-enforceable, serves exclusively as prompt input, and does not participate in behavior control. It accommodates ambiguity and semantic flexibility but is prone to semantic drift.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="rule-normative-language"></a> Rule Normative Language (RNL)
    > A normative language for expressing executable behavior rules using MUST/MUST NOT statements. RNL restricts keywords to MUST and MUST NOT only, prohibits vague terms, and follows the sentence structure: Subject + Normative Keyword + Action + Target + Condition. It constrains AI's interpretation space by reducing degrees of freedom.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="rule-bra"></a> Rule (BRA)
    > The smallest unit that carries governance meaning in Behavior Rule Architecture, formally represented as Rule = ⟨RNL, Metadata, Boundary_Declaration⟩. Each rule encapsulates one explicit behavioral Policy (MUST) or Constraint (MUST NOT), its applicable scope, governance interpretation context, and accountability expectations.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="policy-must"></a> Policy (MUST)
    > A mandatory behavior policy in BRA defining behaviors AI should achieve. Triggering is implicit—compliance is difficult to directly observe or produce evidence for. Enforcement level is medium, requiring post-hoc verification through output review and compliance checks.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="constraint-must-not"></a> Constraint (MUST NOT)
    > A prohibitive behavior constraint in BRA defining behaviors AI must avoid. Triggering is explicit—violations can be detected and produce clear evidence. Enforcement level is high, supporting runtime detection and immediate enforcement through violation evidence generation.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="decision-behavior-normative-category"></a> Decision Behavior Normative Category
    > A classification mechanism for AI decision behavior normatives, not a classification of AI behaviors themselves. It defines decision behavior normative types first, then derives corresponding rules. Primary categories include AR (Artifact Isolation), BD (Boundary & Stop), CN (Constraint Neutrality), TR (Traceability), LG (Logging & Report), ST (Structural Change), and TI (Test Integrity).
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="category-ruleset"></a> Category Ruleset
    > A collection of all rules based on the same Decision Behavior Normative Category, with a 1:N cardinality (each rule belongs to exactly one Category). Different Category Rulesets are mutually exclusive, and their union constitutes the complete Rule Library. Category Rulesets only classify rules; they do not compose rules.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="application-ruleset"></a> Application Ruleset
    > A rule collection designed based on arbitrary application principles such as workflow-based, domain-based, risk-based, or compliance-based composition. It has N:N cardinality with rules—one rule can be composed into multiple Application Rulesets, and one Application Ruleset can combine rules from different Decision Behavior Normative Categories.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="rule-library"></a> Rule Library
    > A centralized storage and management system for all rules, serving as an accumulatable governance asset. Mathematically, the library equals the union of all Category Rulesets. It supports cross-boundary sharing (industry, enterprise, project) and evolves through three stages: Rule Pool, Repository, and Marketplace.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="execution-view"></a> Execution View
    > An optional rule structure component that defines the interpretation viewpoint the AI should adopt when processing a rule, such as security, quality assurance, or architecture. It reduces rule interpretation ambiguity without affecting execution control. It is not a responsibility assignment or role-playing instruction.
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)
- <a id="risk-potential"></a> Risk Potential
    > An a priori risk assessment within BRA scope, representing the first layer of the Three-Layer Risk Model. It estimates potential impact if something goes wrong, expressed as impact_score and rationale. Distinguished from Risk Signal (runtime detection by BCM) and Realized Risk (actual consequences assessed during audit).
    *Origin*: [Behavior Rule Architecture](manuscripts/2026-03_behavior-rule-architecture_v1.0.md)

