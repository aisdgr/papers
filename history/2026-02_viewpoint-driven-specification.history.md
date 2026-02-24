# VDS Version History  
**Viewpoint-Driven Specification — Research Evolution Log**

This document records the methodological evolution of **Viewpoint-Driven Specification (VDS)**.  
The versioning reflects shifts in *research focus, diagnostic capability, and governance formalization*, rather than incremental feature changes.

VDS did not emerge as a monolithic framework. Instead, it evolved through repeated cycles of observation, hypothesis formation, validation, and consolidation in AI-assisted software engineering contexts.

---

## Pre-Version Phase — Exploratory Observation

**Status:** Pre-formalization  
**Artifacts:** Research notes, internal drafts, case observations

### Key Observations
- AI-assisted development frequently produces outputs that are *logically coherent but misaligned with human intent*.
- These outcomes cannot be adequately described using traditional notions of bugs, errors, or hallucinations.
- Early terms such as *Inference Creep* and *Scope Drift* were used descriptively but lacked operational grounding.

### Outcome
- Identification of a governance problem rather than a model-quality problem.
- Recognition that existing software engineering review mechanisms are insufficient under AI-scale generation.

---

## v0.1 — Concept Framing Phase

**Status:** Archived Concept  
**Working Name:** Viewpoint-Driven Development (VDD)

### Contributions
- Introduction of **Viewpoint** as a semantic constraint surface for AI generation.
- Reframing documents as *semantic commitments* rather than passive records.
- Initial proposal of traceability between documents and generated artifacts.

### Limitations
- Scope too broad under the notion of “development.”
- No clear operational procedure.
- Viewpoints and documents not yet clearly distinguished.

### Transition Trigger
- Realization that the core problem resides in **AI-generated specifications**, not general development workflows.

---

## v0.2–v0.3 — Method Emergence Phase

**Status:** Deprecated (Superseded)  
**Renamed:** Viewpoint-Driven Specification (VDS)

### Key Advances
- Formal shift from *Development* to *Specification*.
- Introduction of **Over Outcome** to describe AI-generated outputs that exceed or escape intended semantic boundaries.
- Viewpoints explicitly treated as **hypotheses**, not fixed structures.
- Alignment of viewpoint introduction with a PDCA-style validation loop.

### Additions
- Early differentiation between intent-oriented and engineering-oriented document roles.
- Preliminary case studies demonstrating stabilization effects.

### Limitations
- Viewpoint discovery remained largely intuitive.
- Model dependency concerns not yet fully addressed.

---

## v0.4 — Governance Reframing Phase

**Status:** Milestone Version

### Major Conceptual Shift
- VDS reframed from a “problem-solving method” to a **governance observation framework**.
- Explicit stance:  
  > VDS does not judge correctness; it renders boundary displacement observable.

### Key Additions
- Stability Validation as an acceptance criterion for viewpoints.
- Viewpoints allowed to be compositional and non-exclusive.
- Clear positioning of VDS as AI-native and unsuitable for manual specification authoring.

### Outcome
- Full-paper narrative became viable (ASE-level structure).
- However, engineering formalization was still incomplete.

---

## v0.5 — Coordinate Formalization & Model Decoupling

**Status:** Beta Method

### Core Breakthrough
- Introduction of the semantic coordinate system:

```
(Document, Version, Trace ID)
```

### Definitions
- **Trace ID:** Semantic spatial anchor.
- **Version:** Temporal anchor.
- Governance decisions operate on coordinates, not model internals.

### Impact
- Explicit decoupling from model-specific reasoning mechanisms.
- Human role reframed as **Regulator / Coordinate System Designer**.
- AI positioned as a content generator constrained by external structure.

---

## v0.6–v0.6.2 — Diagnostic Closure Phase

**Status:** Submission Candidate

### Restored & Formalized Core Logic
A previously implicit but essential diagnostic process was fully reintegrated:

- Semantic perturbation
- Multi-viewpoint change observation
- Attribution-based diagnosis

### Viewpoint Attribution Diagnosis
Observed semantic displacement is classified into:
1. **Semantic Noise** — model variability, no governance action required.
2. **Viewpoint Ambiguity** — existing viewpoint boundaries require refinement.
3. **Latent Over Outcome** — emergence of an unmodeled semantic dimension, triggering viewpoint discovery.

### Significance
- Establishes VDS as an *active diagnostic system*, not a passive control layer.
- Addresses root-cause analysis concerns from automated software engineering perspectives.
- Clarifies automation boundaries without over-claiming autonomy.

---

## Current Status

**Latest Stable Draft:** v0.6.2  
**Intended Use:**
- arXiv submission
- ASE full-paper candidate
- Foundation for subsequent IGEF-focused work

**Next Planned Iterations:**
- v0.6.3+: Reviewer-driven clarifications (metrics, heuristics, rebuttal support)

---

## Summary Statement

> VDS evolved from descriptive problem framing to a coordinate-based diagnostic and governance framework, enabling early-stage boundary observability in AI-generated specifications without reliance on model internals.
