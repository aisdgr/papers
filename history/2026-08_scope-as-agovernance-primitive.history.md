# Scope as a Governance Primitive — Version History

This document records the conceptual development of the paper  
**“Scope as a Governance Primitive.”**

The paper began as an investigation into governance applicability and
decidability, and later evolved into a broader theoretical synthesis of Scope
as a reusable structural reference across inference, authorization, Boundary,
effect analysis, evidence, and cross-role governance.

Earlier versions are preserved as part of the conceptual development history.
Where a prior formulation has been narrowed, generalized, or superseded, the
change is stated explicitly rather than retroactively rewriting the earlier
version.

---

## v0.1 — Problem Statement: Governance Without Applicability
**Status:** Concept Exploration

### Purpose
- Identify a class of governance failures that cannot be explained by
  weak enforcement, missing rules, or implementation defects.
- Argue that many governance claims fail because their applicability
  is never structurally specified.

### Key Contributions
- Introduced the idea that governance statements may become
  *logically undecidable* when their domain of applicability is undefined.
- Distinguished governance rhetoric from governable structure.
- Framed missing applicability as a structural rather than ethical failure.

### Deliberate Non-Goals
- No formal definition of Scope.
- No mathematical or structural criteria.
- No linkage to specific AI failure phenomena.

### Historical Significance
This version identified the original problem: governance cannot meaningfully
evaluate a rule, decision, or violation when the region to which the judgment
applies is unknown.

---

## v0.2 — Scope as a First-Order Governance Element
**Status:** Concept Formalization

### Purpose
- Elevate Scope from an implicit assumption to an explicit governance element.
- Differentiate governance primitives from governance outcomes.

### Key Contributions
- Proposed Scope as a first-order governance element.
- Introduced three early criteria for a governance primitive:
  declarability, diagnosable absence, and structural observability.
- Positioned Scope as a precondition for governance evaluation.

### Earlier Formulation
This version described governance primitives as **static, declarable artifacts**
and emphasized governance decidability.

### Later Refinement
The current paper no longer requires Scope itself to be static.
Scope may change, narrow, expand, or be transferred across contexts.
The governance requirement is instead that relevant Scope states and changes
remain explicit, identifiable, and traceable.

The current paper also distinguishes the conceptual **Scope** from the
**Scope Artifact** through which a Scope state is externalized and inspected.

---

## v0.3 — Formal Scope Definition and Decidability
**Status:** Structural Definition

### Purpose
- Provide a minimal formal representation of Scope suitable for engineering analysis.
- Establish conditions under which governance applicability could be evaluated.

### Key Contributions
- Defined Scope as the operational quadruple:

  `⟨Actor, Action, Object, Stage⟩`

- Introduced structural-completeness predicates.
- Argued that incomplete Scope can make governance evaluation undefined.
- Distinguished non-governance from weak governance.

### Historical Significance
This version established that Scope must be structurally representable rather
than left entirely to prose or inference.

### Later Refinement
The quadruple is no longer the general definition of Scope.

`Actor–Action–Object` remains useful as an operational coordinate in some
authorization or execution applications, but it is now treated as one possible
representation rather than the ontology of Scope itself.

`Stage` has also been moved conceptually outside Scope and is now treated as
part of **Governance Context**.

The current definition is broader:

> **Scope is an explicitly identifiable governed region selected according to
> a governance viewpoint within a governance context.**

The current paper also narrows the earlier decidability claim.
Explicit Scope can make governance applicability, membership, comparison, and
structural evaluation more determinate, but Scope alone does not make policy
correctness, compliance, risk, or governance outcomes universally decidable.

---

## v0.4 — Structural Failure Modes from Missing Scope
**Status:** Analytical Consolidation

### Purpose
- Analyze predictable governance failures arising from absent or partial Scope.
- Connect missing Scope to downstream decision-behavior pathologies.

### Key Contributions
- Linked missing or undefined Scope to:
  - Decision Vacancy,
  - non-evaluable governance claims,
  - and Inference Creep.
- Clarified the distinction between Scope and Boundary.
- Argued that a Boundary cannot be meaningfully evaluated without a reference Scope.

### Interpretation Note
This version deliberately refrained from proposing enforcement mechanisms.
Its contribution was to show that governance failure may occur before
enforcement is invoked.

### Later Refinement
The relation is now stated more precisely:

- **Scope** establishes the governed reference region.
- **Boundary** classifies an item, action, or transition relative to that region.
- **Policy / Authority** determines what governance consequence follows.

The current paper therefore avoids treating Boundary itself as a synonym for
permission or prohibition.

---

## v0.5 — Viewpoint-Based Scope and Explicit Governance Regions
**Status:** Conceptual Generalization

### Purpose
- Move beyond a single operational representation of Scope.
- Generalize Scope as a viewpoint-dependent governed region.
- Separate visibility, authorization, operation, and effect.

### Key Contributions

#### 1. Scope Becomes Viewpoint-Dependent
Scope is no longer treated as one universal range.

A **governance viewpoint** defines the selection criterion under which items
belong to a Scope.

Representative viewpoints include:

- **Visible Scope** — what an actor is exposed to by design.
- **Authorized Operable Scope** — what an actor is authorized to operate on.
- **Actual Effect Scope** — what is ultimately affected as a consequence of execution.

These are representative instantiations rather than an exhaustive taxonomy.

#### 2. Scope ≠ Authorization
The paper separates Scope from access-control decisions.

Authorization is treated as one possible application of Scope rather than the
definition of Scope itself.

This enables comparison with ABAC without claiming that ABAC lacks scope.

#### 3. Actual Operation ≠ Actual Effect
The paper distinguishes direct operation from downstream consequence.

An authorized operation may remain within its Operable Scope while producing
effects outside that region.

This condition becomes **Effect Expansion**, which is descriptive before it is
interpreted as risk or violation.

#### 4. Inference Region Becomes a Governance Concern
Visible information is distinguished from the region within which governance
expects AI reasoning to be grounded.

The paper therefore introduces **Inference Scope Visibility** as a governance
application without creating a mandatory fourth Scope type.

#### 5. Governance Context Replaces Stage as an Intrinsic Scope Dimension
Scope may be instantiated and refined across:

`Project → Development Stage → Task → Decision → Execution`

The hierarchy is treated as Governance Context rather than as part of the
general Scope definition.

---

## v0.6 — Scope Externalization and Scope Artifact
**Status:** Governance Architecture Consolidation

### Purpose
- Explain why an effective Scope is insufficient if it remains implicit.
- Make Scope changes visible as governance events.
- Connect Scope to evidence before, during, and after decision formation.

### Key Contributions

#### 1. Explicit vs. Implicit Scope
The paper distinguishes a governed region that exists operationally from one
that is explicitly represented.

Implicit Scope may arise from:

- prompts,
- retrieved context,
- workspace configuration,
- policy evaluation,
- tool permissions,
- workflow routing,
- or model-determined relevance.

The governance requirement is not that Scope never changes, but that material
Scope changes remain observable.

#### 2. Dynamic Scope Is Retained
The earlier static-primitive formulation is replaced by:

> **Dynamic Scope should mean explicitly changing Scope, not invisibly changing governance.**

Scope may expand, narrow, refine, or transfer.

A material Scope transition should itself become a governance-visible event.

#### 3. Scope Artifact
The paper distinguishes:

- **Scope** — the governed region.
- **Scope Artifact** — the inspectable representation of that region.

A Scope Artifact may contain:

- Scope identity,
- Governance Context,
- viewpoint,
- included items,
- authority basis,
- version,
- provenance,
- change history,
- linked evidence.

This distinction allows Scope to remain conceptually clean while still being
persisted, versioned, audited, and referenced.

#### 4. Scope as an Evidence Anchor
Pre-decision, decision-time, and post-decision evidence can reference the same
Scope Artifact or a traceable sequence of Scope Artifact versions.

This supports questions such as:

- What was visible?
- What was intended for inference?
- What was authorized?
- Was Scope expanded?
- What was actually modified?
- What was actually affected?

Scope therefore becomes a common reference across decision evidence rather than
merely a constraint on action.

---

## v0.7 — Theoretical Synthesis Across the Existing Research Line
**Status:** SSRN Theoretical Synthesis Draft

### Purpose
- Consolidate specialized Scope constructs already present across the author's
  prior EDBG / EDBF research.
- Show that Scope has functioned as a structural necessity across multiple
  governance mechanisms before being explicitly abstracted as a primitive.
- Position the paper as a theoretical synthesis rather than a narrow concept
  or formal-decidability paper.

### Research-Line Consolidation

The paper now explicitly maps Scope-related constructs from prior works:

| Earlier Construct | Governance Role in the Current Synthesis |
|---|---|
| VSS Explicit Scope | Specification-viewpoint Scope |
| Boundary Visible Scope | Visible Scope |
| BRA Rule Scope | Rule-applicability Scope |
| BRA Execution Scope | Context-bound Scope |
| DA Artifact Scope | Specialized Authorized Operable Scope |
| DA Outcome Scope | Observed operation / modification Scope |
| DR Behavior Scope | Behavioral authorization Scope |
| Actual Effect Scope | Consequence-viewpoint Scope |
| Role State Scope | Role-viewpoint Scope |
| Audit Scope | Evidence / audit-viewpoint Scope |
| Responsibility Scope | Responsibility-viewpoint Scope |

### Key Contributions

#### 1. Scope as an Abstraction Layer
Earlier Scope terms are no longer treated as competing definitions.
They are interpreted as application-specific projections of a more general
governance primitive.

Existing papers are not retrospectively renamed.

#### 2. Scope as a Prerequisite
Scope is positioned as a structural prerequisite for:

- Boundary,
- authorization,
- inference governance,
- Decision Analysis,
- risk interpretation,
- and evidence anchoring.

Scope is not any of these mechanisms itself.

#### 3. ABAC Positioning
The paper explicitly rejects the claim that ABAC has no Scope.

Instead:

- ABAC typically derives an effective authorization region from policy,
  attributes, and environmental conditions.
- Scope Governance externalizes the governed region so relevant Scope states
  can remain identifiable and traceable across inference, authorization,
  effect, and evidence.

The distinction is therefore one of abstraction and observability, not
existence versus absence.

#### 4. Three Layers of Scope-Related Governance Conditions
Scope-related conditions are organized into:

**Scope Definition and Exposure**
- Undefined Scope
- Exposure Region
- Blind Operation

**Execution and Governance Interaction**
- Operational Scope Violation
- Effect Expansion
- Decision Vacancy

**Scope Evolution**
- Inference Creep
- Scope Absorption
- Cumulative Scope Expansion

This taxonomy prevents every Scope difference from being treated as an
authorization violation.

#### 5. Longitudinal Scope Governance
Scope Absorption and Cumulative Scope Expansion establish that some governance
conditions cannot be detected from a single execution event.

A current Boundary may be valid relative to the current Scope while the
governance problem is that the Scope itself has silently changed.

This yields a central principle:

> **Governance of dynamic Scope requires not only knowledge of the current
> Scope state, but preservation of prior Scope states against which structural
> change can be observed.**

#### 6. Scope as a Reusable Governance Primitive
The current synthesis positions Scope as:

> **a reusable structural reference that makes the region of inference visible
> before a decision and makes authority, Boundary, effect, risk, and evidence
> interpretable after it.**

---

## Current Status — Theoretical Synthesis
**Status:** SSRN Draft / Pre-Submission

The paper is no longer primarily a formal Scope-completeness or governance-
decidability paper.

Its current thesis is broader:

> **Scope is an explicitly identifiable governed region selected according to
> a governance viewpoint within a governance context.**

Its principal contribution is the abstraction of Scope from specialized uses
already distributed across the author's research line into a reusable
governance primitive.

The current paper emphasizes five properties:

1. **Scope is explicit.**
   The governed region should not remain only an implicit result of prompt
   interpretation, policy evaluation, workflow configuration, or AI inference.

2. **Scope is viewpoint-dependent.**
   Visibility, authorization, behavior, effect, responsibility, audit, and
   other governance questions may produce different Scope regions.

3. **Scope is dynamic but traceable.**
   Scope may change, but relevant Scope states and transitions should remain
   observable governance events.

4. **Scope is composable.**
   Boundary, authorization, rules, Decision Analysis, Decision Risk,
   Continuation Readiness, and evidence can consume Scope without redefining it.

5. **Scope is longitudinal.**
   Preserving Scope state across time enables governance to detect Scope
   Absorption and cumulative expansion that cannot be identified from a
   single transaction.

The current manuscript is positioned as a **theoretical synthesis paper for
SSRN**, not as a mathematical proof or a replacement for access-control,
Boundary, policy, or enforcement frameworks.

---

## Superseded or Narrowed Claims

The following earlier formulations remain part of the conceptual history but
are no longer the current paper's general claims:

| Earlier Formulation | Current Position |
|---|---|
| Governance primitives are static artifacts | Scope may be dynamic; Scope Artifact externalizes each relevant state |
| Scope = `⟨Actor, Action, Object, Stage⟩` | Operational representation only; not the general definition |
| Stage is intrinsic to Scope | Stage belongs to Governance Context |
| Scope makes governance decidable | Scope improves structural applicability and evaluability; it does not make all governance outcomes decidable |
| Boundary determines permitted/prohibited | Boundary classifies relative to Scope; Policy / Authority determines consequence |
| Missing Scope inevitably causes Inference Creep | Missing/implicit Scope creates conditions under which model-determined expansion may occur |
| Visible Scope is the complete inference region | Visible Scope is exposure; intended inference region is a separate governance concern |
| Outcome Scope captures all consequence | Outcome Scope captures actual modification; Actual Effect Scope is broader |

---

## Continuing Research Directions

Future work may examine:

- operational representations and serialization of Scope Artifacts;
- versioning and Scope transition protocols;
- empirical detection of Scope Absorption and cumulative Scope expansion;
- automated comparison between Operable Scope and Actual Effect Scope;
- inference-region observability in LLM, RAG, and agent systems;
- integration with ABAC, UCON, policy engines, and workflow authorization;
- relationships among Scope, Evidence, Authority, and other candidate
  governance primitives;
- cross-domain validation beyond AI-assisted software engineering.

No earlier version is considered erased or retroactively invalid.
Each version represents a stage in the progression from governance
applicability, through formal Scope representation, to the current
viewpoint-based and evidence-oriented theoretical synthesis.
