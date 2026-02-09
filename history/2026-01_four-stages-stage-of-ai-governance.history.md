# Four Stages of AI Governance — Version History

This document records the conceptual evolution of
**Four Stages of AI Governance: A Stage-Based Framing of Contemporary Practices**.
The paper serves as a *descriptive and classificatory* work, not a prescriptive
governance framework.

---

## v0.1 — Problem Reframing  
**Status:** Exploratory / Diagnostic Phase

### Purpose
- Challenge the dominant assumption that “AI governance” is primarily a
  **runtime enforcement problem**.
- Reframe governance failure as a **stage misalignment** rather than
  insufficient controls or weak policies.
- Establish the need for a temporal and structural decomposition of governance
  practices across the AI-assisted SDLC.

### Key Contributions
- Identified a recurring category error in contemporary AI governance discourse:
  conflating *execution-time intervention* with *decision formation governance*.
- Observed that most governance discussions implicitly assume:
  - a stable intent,
  - a traceable decision origin,
  - and a single locus of control.
- Introduced the intuition that governance effectiveness is **stage-dependent**,
  not tool-dependent.
- Positioned runtime interception as a *late-stage corrective*, not a primary
  governance mechanism.

### Deliberate Non-Goals
- No stage taxonomy yet.
- No definitions of governance maturity.
- No alignment with standards (e.g., ISO/IEC 42001).
- No solutions, tools, or processes.

### Rationale
v0.1 functions as a **problem diagnosis document**: it explains *why current
AI governance debates talk past each other*, without yet proposing a structure.

---

## v0.2 — Stage Differentiation  
**Status:** Structural Decomposition Phase

### Purpose
- Introduce a **stage-based lens** to separate qualitatively different forms of
  governance activity in AI-assisted development.
- Make governance discussions *comparable* by anchoring them to SDLC stages.

### Key Contributions
- Distinguished governance concerns across emerging phases:
  - intent formation,
  - specification and constraint articulation,
  - generation and transformation,
  - execution and operation.
- Clarified that governance failures at earlier stages **cannot be repaired**
  at later stages without cost amplification.
- Introduced the idea of **governance irreversibility**:
  once a decision passes certain stages without evidence, later governance
  becomes reconstructive rather than preventive.
- Explicitly separated:
  - *governance existence* from
  - *governance invocation*.

### Deliberate Non-Goals
- No fixed number of stages declared yet.
- No normative judgment of “good” or “bad” governance.
- No claims of completeness.

### Rationale
v0.2 establishes **structural separability**: governance is not monolithic and
must be analyzed relative to *when* decisions are formed and transformed.

---

## v0.3 — Four-Stage Framing  
**Status:** Conceptual Consolidation Phase

### Purpose
- Formalize the analysis into **Four Stages of AI Governance** as an explanatory
  model of contemporary practices.
- Provide a neutral taxonomy that accommodates both engineering and policy
  perspectives.

### Key Contributions
- Defined four analytically distinct governance stages (descriptive framing):
  1. **Intent & Decision Formation Governance**
  2. **Specification & Constraint Governance**
  3. **Generation & Transformation Governance**
  4. **Execution & Operational Governance**
- Demonstrated that most “AI governance solutions” cluster almost exclusively
  in Stage 4.
- Explained why Stage 4 governance is structurally incapable of:
  - recovering lost intent,
  - resolving decision vacancy,
  - or preventing inference creep.
- Connected stage misalignment to observed phenomena:
  - Ghost Intent,
  - orphaned decisions,
  - auditability collapse,
  - and false confidence in runtime controls.

### Deliberate Non-Goals
- No proposal of a governance framework.
- No maturity model or scoring system.
- No implementation guidance.

### Rationale
v0.3 serves as a **classification and clarification paper**: it explains *what
people are actually doing* when they claim to “govern AI,” and *why outcomes
differ*, without prescribing what should be done.

---

## v0.4 — Standards & Discourse Positioning (Planned)
**Status:** Alignment & Boundary Definition

### Planned Focus
- Position the four-stage framing relative to:
  - ISO/IEC 42001,
  - AI risk management standards,
  - and enterprise governance narratives.
- Clarify which stages standards implicitly assume, omit, or collapse.
- Explicitly state the paper’s non-claims to avoid framework misinterpretation.

---

## Versioning Note
Early versions intentionally avoid prescriptive language. The work is designed
to function as a **conceptual lens**, not a governance solution. Any future
extension into methods, tools, or enforcement mechanisms will be published as
separate work.
