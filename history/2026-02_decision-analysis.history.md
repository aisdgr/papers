# Decision Analysis — Version History

This document records the conceptual evolution of the *Decision Analysis* line.
Each version intentionally stabilizes a specific layer of reasoning.
Later versions do not invalidate earlier ones; they add constraints
to prevent analytical and governance misclassification.

---

## v0.1 — Initial Consolidation (Unreleased Draft)

**Status:** internal working draft  
**Role:** concept aggregation

### Characteristics
- Mixed terminology from *Decision Risk* and *Decision Analysis*
- Authority, decision, effect, and risk concepts not yet separated
- Analysis and governance language partially interleaved

### Limitations Identified
- Authority implicitly treated as a primary analytical construct
- Risk language introduced before analytical preconditions were clarified
- No clear boundary between:
  - analysis result
  - governance interpretation
  - pre-analytical absence

This version was never intended for publication.

---

## v0.2 — Terminology Stabilization (Semantic Baseline)

**Status:** semantic baseline  
**Role:** terminology and conceptual definitions only

### Key Contributions
- Stabilized core terms:
  - Decision (latent structural commitment)
  - Effect (observable manifestation)
  - Over Outcome
  - Decision Risk (conceptual category)
- Explicitly excluded:
  - decision elements
  - analytical procedures
  - formulas
  - governance judgments
- Established DR categories as **semantic classifications**, not analytical outputs:
  - DR-N (implicit baseline)
  - DR-O
  - DR-V
  - DR-I

### Explicit Non-Goals
- No analysis workflow
- No determinability criteria
- No notion of observability or anchoring

### Rationale
v0.2 fixed *what the words mean*,
but not *when those words are applicable*.

---

## v0.3 — Anchoring Preconditions (Applicability Boundary)

**Status:** conceptual gatekeeping layer  
**Role:** defining when analysis and risk discussion are even possible

### Key Contributions
- Introduced **Anchoring Preconditions**:
  - Scope anchoring
  - Effect anchoring
  - Decision admissibility
- Established that:
  - Absence of anchors ≠ risk
  - Absence of anchors ≠ DA-I
- Clarified that:
  - Decision Risk requires anchoring
  - Governance discussion without anchoring is speculative

### Structural Impact
- Prevented premature escalation from “unknown” to “risk”
- Formally separated:
  - non-existent problems
  - indeterminate problems
  - analyzable problems

### Rationale
v0.3 answered:
> *Why some decision-related problems cannot even be surfaced or estimated.*

---

## v0.4 — Effect-First, Authority-Conditional Analysis (Asymmetric Inference)

**Status:** analytical structure stabilized  
**Role:** defining valid analysis results and their governance transitions

### Key Contributions
- Established **effect-first analysis** as mandatory
- Introduced **asymmetric two-phase inference**:
  1. Effect-based decision analysis (authority-free)
  2. Authority-conditional interpretation (only if required)
- Clarified Decision Analysis result set:
  - DA-N — Normal (observable, explainable)
  - DA-O — Over (observable, attributable at effect level)
  - DA-I — Indeterminate (observable, not stably classifiable)
  - DA-V — Vacancy (observable, no decision-bearing locus)
  - **DA-U — Unobservable** (analysis attempted, no observable anchors)

### Critical Clarifications
- Authority is **not** an analytical primitive
- Authority is required **only** to establish DA-V
- DA-I deterministically induces DR-I
- DA-U:
  - is an analysis result
  - is **not** a risk
  - cannot be engineering-determined as risk
  - may only be acknowledged by human judgment

### Mapping to Decision Risk
- DA-N → no Decision Risk
- DA-I → DR-I
- DA-O → DR-O *or* DR-V (authority-conditional)
- DA-V → DR-V
- DA-U → no DR classification

### Rationale
v0.4 fixed the inference order problem and prevented
authority and governance from contaminating analytical validity.


