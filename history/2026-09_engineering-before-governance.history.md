# Engineering Before Governance — Version History

This document records the conceptual development of the paper  
**"Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State."**

The paper began as a synthesis attempt across the author's existing work on
step-level AI behavior governance and workflow-level continuation governance.
Rather than introducing a new framework, it identifies a common dependency
principle: governance can only evaluate, constrain, audit, or attribute states
that engineering has first made explicit enough to inspect.

Earlier versions are preserved as part of the conceptual development history.
Where a prior formulation is narrowed, generalized, or superseded, the change
should be stated explicitly rather than retroactively rewriting the earlier
version.

---

## v0.3 — Development-Stage Scope and Governance Requirement Framing
**Status:** Scope clarification and conceptual reframing

### Purpose
- Make explicit from the beginning that the paper concerns AI governance at the
  software development stage, especially AI-assisted software engineering.
- Prevent behavior, execution, boundary, decision, workflow, and handoff from
  being read as production-runtime concepts.
- Replace the prior **Step-Level Governability** framing with a governance
  requirement chain:

```text
Governance Problem or Requirement
    -> Engineering Design
    -> Engineering-Visible State
    -> Governance Engineering
```

### Scope Clarification
v0.3 adds an explicit stage boundary in the abstract and introduction:

- **Behavior** means AI-assisted development behavior.
- **Execution** means a development action or tool-mediated development
  operation.
- **Boundary** means a development-stage classification of permitted
  visibility, operation, or modification.
- **Workflow** means a software development workflow.
- **Continuation** means transfer of development work between human and AI
  actors.

The paper therefore does not primarily address runtime governance of deployed
AI systems, production inference monitoring, or model-level safety governance.

### Governance Requirement Reframing
Section 4 is renamed from step-level governability to **Development Behavior
Governance**. It is reorganized around governance needs rather than framework
names.

Before execution:

- **Behavior constraints** require visibility into applicable constraints,
  policies, rules, targets, conditions, and priorities. Behavior Rule
  Architecture is treated as one engineering design.
- **Execution boundaries** require visibility into allowed boundaries, visible
  range, operable range, and modifiable range. Scope and Boundary are treated
  as engineering designs.
- **Context** requires specification state that can outlive prompt memory and
  represent multiple viewpoints. Viewpoint-Structured Specification is treated
  as one engineering design.

After execution:

- **Boundary and risk judgment** require visibility into actual modified scope,
  actual effect scope, applied constraints and policies, exceptions, and
  evidence. Decision Analysis and Decision Risk provide the post-execution
  judgment surface.

### Workflow Governance Clarification
Workflow discussion is reframed as **development workflow governance**. The
central claim is preserved but narrowed:

> A software development workflow composed of individually governed
> AI-assisted actions is not necessarily governed unless the handoffs between
> those actions are also governed.

Continuation readiness remains the workflow-level evidence for this claim:
Role State, Work Junction, Continuation Package, Receiving Capacity, authority
compatibility, and evidence accessibility make handoffs governable.

### Unified Model Revision
The unified model is revised from a list of governance units to a requirement
table with five columns:

1. Governance area;
2. Governance problem or requirement;
3. Engineering design;
4. Engineering-visible state;
5. Governance judgment.

This makes the paper's analytical movement explicit:

```text
governance need
    -> required visible state
    -> possible governance judgment
```

### Terminology Changes
- Removed the phrase **Step-Level Governability** from the manuscript.
- Replaced step-oriented claims with **development action governance**,
  **development behavior governance**, and **development workflow governance**.
- Added Decision Analysis and Decision Risk to the synthesis alongside VSS,
  Scope, Boundary, BRA, and continuation readiness.

---

## v0.2 — From Governance Requirement to Governance Engineering
**Status:** Conceptual model refinement

### Purpose
- Clarify the relationship between normative governance requirements and the
  engineering work required to make them operational.
- Define **Engineering-Visible State** and **Governance Engineering** as
  distinct concepts.
- Separate governance judgments about execution steps from governance
  judgments about handoffs.
- Remove wording that could imply governance policy chronologically follows
  engineering or that continuous governance means uninterrupted monitoring.

### Revised Dependency Chain
v0.2 replaces the earlier realization shorthand with:

```text
Governance Requirement
    -> Engineering Design
    -> Engineering-Visible State
    -> Governance Engineering
```

The layers are interpreted as follows:

- **Governance Requirement** defines what should be governed.
- **Engineering Design** determines how the relevant condition will be
  represented and preserved.
- **Engineering-Visible State** makes the condition identifiable, bounded,
  inspectable, retrievable, and attributable for the relevant governance use.
- **Governance Engineering** implements and operates mechanisms for constraint,
  classification, authorization, approval, audit, attribution, and feedback.

This chain expresses operational dependency rather than organizational or
chronological precedence. Governance requirements may initiate and guide
engineering design.

### Revised Workflow Model
The compact v0.1 sequence:

```text
E1 -> G1 -> H1 -> E2 -> G2 -> H2 -> E3 -> G3
```

did not show a separate governance judgment for each handoff. v0.2 supersedes
that shorthand with:

```text
Step State S1
    -> Step Judgment Gs1
    -> Handoff State H1
    -> Handoff Judgment Gh1
    -> Step State S2
    -> Step Judgment Gs2
```

This makes explicit that execution and transition are separate governance
surfaces. A governed step does not imply a governed outgoing handoff.

### Terminology Refinements
- **Engineering-visible** means accessible and interpretable to the actor or
  mechanism responsible for a particular governance judgment. It does not
  imply universal disclosure or complete observability of model internals.
- **Governance engineering** is narrower than governance as a whole. It is the
  implementation and operation of mechanisms that turn visible state into
  operational judgments and controls.
- **Continuous workflow governance** means that governability is re-established
  at successive step and handoff boundaries. It does not necessarily mean
  continuous-time or real-time monitoring.

### Proposition Changes
- P2 is renamed from **Engineering Precondition** to **Operationalization
  Dependency** and now expresses the complete four-layer chain.
- P3 and P4 now state the governance uncertainty created when step or handoff
  state remains implicit, rather than functioning only as component lists.
- P5 remains the central synthesis claim: governance does not compose
  automatically across actor boundaries.

### Step-Level Argument Restructuring
Section 4 no longer uses VSS, Scope, Boundary, BRA, authority, and evidence as
the primary organizing subjects. Each subsection now begins with a governance
problem or requirement and follows the same analytical sequence:

```text
Governance Problem or Requirement
    -> Engineering Design
    -> Engineering-Visible State
    -> Governance Engineering
```

The prior frameworks are treated as evidence of engineering design choices
within that sequence. The section then identifies how governance can continue
through constraint, judgment, approval, escalation, attribution, or audit. This
avoids presenting the paper as a catalogue of what each prior framework can
solve.

---

## v0.1 — Synthesis Seed: Engineering-Visible State as a Governance Precondition
**Status:** Conceptual synthesis draft

### Purpose
- Establish the core thesis that operational AI governance depends on
  engineering-visible state.
- Synthesize existing work on VSS, Scope, Boundary, BRA, authority, evidence,
  and continuation readiness into a single dependency principle.
- Clarify that "Engineering Before Governance" is not an institutional
  sequencing claim, but an operational governability claim.

### Central Proposition
> Engineering creates the state that governance evaluates.

The version also states the stronger operational form:

> Governance cannot reliably constrain, evaluate, audit, or attribute a
> condition that engineering has not first made explicit.

### Key Contributions
- Distinguished **Governance Requirement** from **Engineering Realization**.
- Framed step-level governability as the externalization of specification,
  scope, boundary, rules, authority, and evidence.
- Framed workflow-level governability as the externalization of Role State,
  Work Junction, Continuation Package, Receiving Capacity, authority
  compatibility, and evidence transfer.
- Introduced the synthesis claim that governed steps do not automatically
  produce a governed workflow.
- Positioned the handoff as a governance object rather than a mere message,
  output, or checkpoint.

### Conceptual Model
The initial model is:

```text
implicit condition
    -> engineering externalization
    -> governance visibility
    -> governance judgment
```

For continuous workflow governance, the initial model is:

```text
E1 -> G1 -> H1 -> E2 -> G2 -> H2 -> E3 -> G3
```

where:

- **E** = engineered governable state for a step;
- **G** = governance judgment;
- **H** = engineered handoff state.

### Prior Work Interpreted in This Version
- **VSS** externalizes intent as structured specification.
- **Scope** externalizes the governed reference region.
- **Boundary** classifies actions, items, or transitions relative to Scope.
- **BRA** converts normative intent into structured behavior rules.
- **Authority and Evidence** provide attribution and assessment basis.
- **Beyond HITL / Continuation Readiness** externalizes handoff state needed
  to govern continuation across humans and AI actors.

### Deliberate Non-Goals
- Does not introduce a new mandatory architecture.
- Does not claim that engineering replaces governance.
- Does not claim that policy is unimportant.
- Does not claim that all governance can be deterministic.
- Does not claim that all AI state must be observable.
- Does not claim that VSS, Scope, Boundary, BRA, Role State, Work Junction,
  Continuation Package, or Receiving Capacity are newly invented in this paper.

### Terminology Constraints
This version explicitly preserves the following distinctions:

| Distinction | Current Position |
|---|---|
| Scope vs. Boundary | Scope is the governed reference region; Boundary is classification relative to that region. |
| Policy vs. engineering realization | Policy expresses a governance requirement; engineering provides observable state and control/evaluation surfaces. |
| HITL vs. continuation readiness | Human presence does not prove receiver capacity. |
| Step governance vs. workflow governance | Governed actors or steps do not imply governed handoffs. |
| Engineering Before Governance vs. organizational sequencing | Governance objectives may precede implementation; operational judgment requires pre-existing engineering-visible state. |

### Historical Significance
This version identifies the paper's main synthesis contribution: existing
mechanisms that previously appeared as separate governance constructs can be
read as instances of a shared dependency between governance judgment and
engineering-visible state.

The paper is positioned for a conceptual governance / information-systems
audience rather than a software-engineering-only audience.

---

## Current Status — v0.2 Conceptual Model Refinement

The manuscript currently contains:

1. an abstract and introduction;
2. a structural gap statement;
3. a step-level synthesis of VSS, Scope, Boundary, BRA, authority, and evidence;
4. a workflow-level synthesis of handoff governance and continuation readiness;
5. a four-layer dependency from governance requirement to governance
   engineering;
6. separate step and handoff governance judgments;
7. a unified table of governance units and required engineering-visible state;
8. five propositions;
9. implications and limitations.

The next revision should likely strengthen:

- related-work positioning against AI governance, HITL, auditability, policy
  engineering, and information-systems governance literature;
- examples showing how a governance requirement fails when its required state
  remains implicit;
- the distinction between engineering-visible state and full formalization;
- the relationship between this paper and Engineering Determinacy;
- publication framing, including whether the target is SSRN, a conceptual
  journal article, or a broader research-line synthesis note.

v0.1 remains preserved as the initial paper draft generated from the working
brief. Its central thesis remains active, while its realization shorthand and
compact workflow sequence are superseded by the more explicit v0.2 models.
