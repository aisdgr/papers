# Scope as a Governance Primitive — Version History

This document records the conceptual development of the paper
**“Scope as a Governance Primitive.”**
The history reflects a focused investigation into governance decidability,
distinct from but foundational to related work on Inference Creep,
Decision Vacancy, and Boundary.

---

## v0.1 — Problem Statement: Governance Without Applicability  
**Status:** Concept Exploration

### Purpose
- Identify a class of governance failures that cannot be explained by
  weak enforcement, missing rules, or implementation defects.
- Argue that many governance claims fail because their applicability
  is never formally specified.

### Key Contributions
- Introduced the notion that governance statements can be
  *logically undecidable*.
- Distinguished between governance rhetoric and governable structures.
- Framed missing applicability as a structural, not ethical, failure.

### Deliberate Non-Goals
- No formal definition of scope.
- No mathematical or structural criteria.
- No linkage to specific AI failure phenomena.

---

## v0.2 — Scope as a First-Order Governance Element  
**Status:** Concept Formalization

### Purpose
- Elevate Scope from an implicit assumption to an explicit governance element.
- Differentiate governance primitives from governance outcomes.

### Key Contributions
- Defined **governance primitives** as static, declarable artifacts.
- Established three criteria for a governance primitive:
  declarability, diagnosable absence, and structural observability.
- Positioned Scope as necessary for governance decidability.

### Rationale
This version clarifies that governance cannot be evaluated unless
its applicability is structurally defined.

---

## v0.3 — Formal Scope Definition and Decidability  
**Status:** Structural Definition

### Purpose
- Provide a minimal, formal definition of Scope suitable for engineering analysis.
- Establish explicit conditions under which governance becomes decidable.

### Key Contributions
- Defined Scope as a quadruple:
  ⟨Actor, Action, Object, Stage⟩.
- Introduced formal predicates for structural completeness.
- Demonstrated that incomplete scope renders governance evaluation undefined.
- Distinguished non-governance from weak governance.

### Rationale
This version establishes Scope as a necessary precondition for any
auditable or enforceable governance system.

---

## v0.4 — Structural Failure Modes from Missing Scope  
**Status:** Analytical Consolidation

### Purpose
- Analyze the predictable failure modes arising from absent or partial scope.
- Connect missing scope to downstream governance pathologies.

### Key Contributions
- Linked scope absence to:
  - Decision Vacancy,
  - non-decidable governance claims,
  - and Inference Creep.
- Clarified the distinction between Scope and Boundary.
- Argued that boundaries without scope create an illusion of governance.

### Interpretation Note
This version deliberately refrains from proposing enforcement mechanisms.
Its contribution is to demonstrate that governance failure often precedes
any attempt at control or compliance.

---

## Current Status — Stable Conceptual Core  
**Status:** Pre-Extension

The current manuscript establishes Scope as a first-order governance primitive
necessary for decidable AI governance.

Future extensions may examine:
- Boundary as a complementary primitive,
- default logic and partial scope resolution,
- and the role of scope completeness in preventing inference creep.

No version is considered deprecated; each represents a necessary step
in isolating governance decidability as a structural problem.
