# An Anchor Architecture for Observing Decision-Level Phenomena in AI-Assisted Software Development - Version History

This document records the conceptual evolution of the paper currently titled:

**An Anchor Architecture for Observing Decision-Level Phenomena in AI-Assisted Software Development**

The version history reflects an intentional progression from phenomenon identification,
through governance analysis, toward observability and anchoring as an engineering concern.
Earlier versions should be read as **conceptual predecessors**, not superseded or discarded drafts.

---

## v0.1 — Phenomenon Declaration  
**Status:** Exploratory / Naming Phase

### Purpose
- Introduce *Inference Creep* as a distinct phenomenon in AI-assisted software development.
- Describe the experiential and structural conditions under which AI systems gradually
  expand their influence over decisions without explicit authorization.
- Establish the phenomenon without proposing detection, mitigation, or governance solutions.

### Key Contributions
- Coined **Inference Creep** to distinguish decision-level expansion from:
  - hallucination,
  - model error,
  - or traditional scope/feature creep.
- Identified the gradual, probabilistic nature of decision influence expansion.
- Framed the risk as *latent* and *structural*, rather than outcome-driven.
- Emphasized that technical correctness does not imply governance correctness.

### Deliberate Non-Goals
- No detection or measurement methods.
- No enforcement or tooling proposals.
- No governance framework design.

### Rationale
v0.1 serves as a **phenomenon boundary document**, defining what Inference Creep *is* and
why existing software engineering assumptions fail to capture it.

---

## v0.2 — Boundary Clarification and Concept Differentiation  
**Status:** Concept Refinement

### Purpose
- Sharpen the conceptual boundary of Inference Creep.
- Differentiate it explicitly from adjacent concepts in software engineering and AI safety.

### Key Contributions
- Systematic comparison with:
  - Feature Creep,
  - Scope Creep,
  - AI hallucination,
  - automation bias.
- Clarified that Inference Creep concerns **decision participation**, not functionality.
- Introduced the notion of *decision boundary erosion* as a non-functional failure mode.

### Rationale
This version reduces ambiguity and positions Inference Creep as a falsifiable engineering
phenomenon rather than a subjective governance concern.

---

## v0.3 — Decision Expansion and Latent Risk Accumulation  
**Status:** Structural Analysis

### Purpose
- Analyze how inference-driven decisions propagate across development stages.
- Examine why small, local inferences can produce system-level risk.

### Key Contributions
- Introduced **decision expansion** as a cumulative process.
- Described **risk acceleration** in probabilistic decision chains.
- Highlighted why runtime validation and output correctness are insufficient.
- Shifted analysis from isolated decisions to longitudinal decision behavior.

### Rationale
This version establishes that Inference Creep is not an anomaly but an emergent property
of AI-assisted workflows.

---

## v0.4 — Decision Vacancy and Observability Failure  
**Status:** Governance-Oriented Analysis

### Purpose
- Investigate why Inference Creep remains undetected in practice.
- Analyze governance failure modes resulting from missing decision attribution.

### Key Contributions
- Introduced **Decision Vacancy**: execution occurring without attributable authority.
- Identified the **Governance Observability Gap**, where decisions cannot be traced to intent.
- Framed untraceable decisions as *orphaned*, regardless of correctness.
- Connected inference-driven expansion to accountability erosion in DevOps environments.

### Deliberate Non-Goals
- No policy prescriptions.
- No compliance framework mapping.
- No enforcement mechanisms.

### Rationale
v0.4 explains *why* organizations fail to see Inference Creep even when technical controls exist.

---

## v0.5 — Architectural Boundary Exploration  
**Status:** Transitional / Architectural Reasoning

### Purpose
- Explore whether governance failures stem from missing architectural intervention points.
- Examine the role of structural boundaries in decision accountability.

### Key Contributions
- Proposed architectural separation between decision intent and execution.
- Analyzed why post-hoc monitoring cannot reconstruct authorization.
- Introduced early notions of constraint placement and evidence linkage.

### Rationale
These versions mark the transition from phenomenon analysis to structural reasoning,
without committing to prescriptive architectures.

---

## v0.6 — Governance Architecture and PDCA Alignment  
**Status:** Governance Formalization

### Purpose
- Formalize governance requirements as architectural properties.
- Align decision governance with institutional audit cycles.

### Key Contributions
- Introduced governance properties (identity, authority, applicability, versioning).
- Mapped architectural elements to PDCA-style governance cycles.
- Emphasized evidence determinism over model transparency.

### Rationale
These versions establish that governance cannot be procedural alone; it must be structural.
However, the emphasis remained governance-centric rather than observability-centric.

---

## Current Direction — Anchor Architecture and Observability  
**Status:** Conceptual Reframing (Ongoing)

### Purpose
- Reinterpret prior architectural constructs as **anchoring mechanisms** rather than
  prescriptive governance layers.
- Focus on *observability*, *comparability*, and *falsifiability* of decision-level phenomena.

### Key Shifts
- From governance enforcement → **decision observability**
- From compliance alignment → **engineering-detectable criteria**
- From boundary prescription → **anchored comparison across time and artifacts**

### Interpretation Note
Earlier governance- and boundary-oriented constructs are retained as conceptual foundations,
but are reinterpreted as providing **stable reference points** that make phenomena such as
Inference Creep, Future Creep, Ghost Code, and orphaned decisions observable and analyzable.
