# Runtime Governance vs. Development Governance — Version History

This history documents the evolution of this paper as a **category-separation**
and **misdiagnosis-correction** work. It argues that runtime interception and
development-stage governance address fundamentally different objects, and that
conflating them produces governance illusions.

---

## v0.1 — Category Error Declaration
**Status:** Exploratory / Misdiagnosis Correction Phase

### Purpose
- Declare the central claim: **runtime interception is not Decision Behavior Governance**.
- Identify the recurring category error in contemporary “AI governance” discourse:
  treating runtime controls as equivalent to governance of decision formation.
- Establish the paper as a conceptual boundary document, not a solution proposal.

### Key Contributions
- Introduced the framing: **Runtime Governance** vs **Development Governance** as
  orthogonal governance domains.
- Clarified that “interception/guardrails” operate on *outputs and actions*,
  while Decision Behavior Governance targets *decision formation legitimacy*.
- Positioned runtime controls as an enforcement layer that presupposes
  upstream legitimacy, not a substitute for it.

### Deliberate Non-Goals
- No tool recommendations (policy engines, interceptors, filters).
- No maturity model, metrics, or audit checklist.
- No claims that runtime controls are useless—only that they are *not* DBG.

### Rationale
v0.1 functions as a **conceptual firewall**: it prevents DBG/EDBG from being
misclassified as “runtime guardrails” by asserting a strict boundary of concern.

---

## v0.2 — Governance Existence vs. Enforcement
**Status:** Conceptual Differentiation Phase

### Purpose
- Separate **governance existence** from **enforcement mechanisms**.
- Explain how organizations become “administratively governed” while remaining
  “behaviorally ungoverned”.

### Key Contributions
- Distinguished governance as an *institutional fact* from runtime controls as
  *operational mechanisms*.
- Argued that runtime interception can improve safety without improving
  **attribution** or **legitimacy** of decision formation.
- Made explicit the inversion: runtime controls often increase confidence while
  leaving decision premises and constraint authority unanchored.

### Deliberate Non-Goals
- No attempt to formalize a full governance framework.
- No attempt to audit or certify interception products.

### Rationale
v0.2 reframes “runtime governance” as **late-stage compliance optics** unless it
is grounded in earlier-stage decision authority and evidence.

---

## v0.3 — Development Governance as the Primary Locus
**Status:** Structural Consolidation Phase

### Purpose
- Establish **Development Governance** as the primary locus for governing AI-assisted
  software production.
- Push governance upstream: runtime → deploy → generate code → specification analysis.

### Key Contributions
- Articulated the upstream governance path:
  - specification/intent anchoring,
  - constraint declaration and versioning,
  - generation-time traceability,
  - evidence capture before execution.
- Connected the critique to engineering reality:
  governance must be placed where choices are made and artifacts are produced,
  not only where actions are executed.
- Clarified the “human minimal effort” principle:
  human authority is preserved through **monitoring and audit of anomalies**,
  not constant intervention.

### Deliberate Non-Goals
- No claim that development governance eliminates runtime risk.
- No operational design for pipelines or tooling (handled by other works).

### Rationale
v0.3 positions the paper as an architectural argument:
**if governance is to be industrialized and auditable, it must be engineered
into development stages**, not bolted onto runtime.

---

## v0.4 — Boundary of Applicability (Planned)
**Status:** Scope Lock & Non-Claims Hardening

### Planned Focus
- Add explicit scope boundaries to prevent misreadings:
  - what “runtime governance” can and cannot guarantee,
  - what “development governance” presupposes.
- Clarify terms that are frequently conflated:
  governance, controls, enforcement, alignment, safety, compliance.
- Add non-claims to keep the paper purely classificatory and avoid being treated
  as a solution framework.

---

## Versioning Note
This paper is intentionally **anti-framework**: it aims to correct vocabulary and
prevent governance theater by separating objects of governance across stages.
Operational methods, pipelines, or tool designs are delegated to separate works
in the ecosystem.
