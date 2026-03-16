# Structural Degradation in AI-Generated Code - Version History


## v0.1 — Initial Concept Draft

**Date:** 2026-03

Initial conceptual draft establishing the core problem of **AI-generated artifacts interacting with evolving software systems**.

**Key Elements Introduced**

- Preliminary observation of degradation patterns in AI-generated codebases
- Early distinction between **intent-level and structural anomalies**
- Initial terminology including:
    - Ghost Intent
    - Inference Creep
    - Architectural Amnesia

**Limitations**

- Root cause mechanism not yet formalized
- No layered taxonomy
- No propagation dynamics model
- Concept list incomplete and loosely categorized

---

## v0.2 — Taxonomy Expansion

**Date:** 2026-03

Expanded the conceptual framework into a **three-layer degradation taxonomy**.

**Major Additions**

- Formal separation of degradation phenomena into:
  - Intent Layer
  - Structural Layer
  - Behavioral Layer
- Definition of **14 degradation phenomena**
- Introduction of **Degradation Paths** within each layer
- First articulation of the mismatch between: `Stateless Generation vs Stateful System Evolution`

**Improvements**

- Added distinctions between related phenomena
- Added worked examples for selected concepts
- Introduced early form of cross-layer propagation idea

**Remaining Issues**

- Root cause mechanism still descriptive rather than structural
- Behavioral layer insufficiently defined
- No explicit theoretical model for degradation dynamics
- Visualization absent

---

## v0.3 — Root Cause Model and Propagation Dynamics

**Date:** 2026-03

Major theoretical revision introducing a **structural explanation for degradation phenomena**.

**Major Additions**

**1. Triple Discontinuity Model**

Defined the root cause of degradation as three structural discontinuities:

- Temporal Discontinuity
- Authorial Discontinuity
- State Discontinuity

These discontinuities emerge when **stateless AI generation interacts with stateful software evolution**.

**2. Non-Cumulative Integration Mechanism**

Introduced the mechanism:

```
Triple Discontinuity
      ↓
Non-Cumulative Integration
      ↓
Cumulative Staged Degradation
```

Explains how repeated generation events progressively destabilize system structure.

**3. Cross-Layer Degradation Dynamics**

Added formal explanation of downward propagation:

```
Intent → Structural → Behavioral
```

and clarified that **behavioral failures are manifestations rather than root causes**.

**4. Visibility Inversion Principle**

Defined the relationship between abstraction depth and detectability:

```
Layer Depth ↑
Detection Probability ↓
Damage Magnitude ↑
```

This principle explains why degradation is often inexpensive early but catastrophic when discovered at runtime.

**5. Visual Models**

Two conceptual diagrams introduced:

- **Figure 1 — Triple Discontinuity Model**
- **Figure 2 — Layered Degradation Propagation Model**

These diagrams illustrate root cause structure and cross-layer propagation dynamics.

---

## v1.0 — Full Paper Draft

**Date:** 2026-03

First complete paper draft, expanding from internal working manuscript (v0.3) to **full academic prose with formal structure, comprehensive definitions, and extended analysis**.

**Structural Changes**

Paper reorganized from v0.3's flat working structure into a formal 10-section academic layout:

```
v0.3 Structure               →  v1.0 Structure
─────────────────────────────────────────────────────
Central Thesis (inline)       →  §1 Introduction (formal)
(implicit)                    →  §2 Structural Degradation (new)
1. Root Cause                 →  §3 Root Cause
2–4. Layer Degradation        →  §4 Three-Layer Taxonomy
5. Cross-Layer Dynamics       →  §5 Cross-Layer Dynamics
   (inline principle)         →  §6 Visibility Inversion Principle (new)
(absent)                      →  §7 Implications for SE (new)
6. Limitations                →  §8 Limitations
7. Contribution               →  §9 Conclusion
References                    →  §10 Related Work (new) + References
```

**Major Additions**

**1. Formal Introduction (§1)**

Replaced the brief Central Thesis with a full Introduction section:

- Contextualizes the research problem within AI-assisted software engineering landscape
- Articulates four explicit contributions (Root Cause Model, Taxonomy, Propagation Model, Visibility Inversion Principle)
- Provides a section-by-section roadmap of the paper

**2. Structural Degradation Definition (§2 — New Section)**

Dedicated section establishing the core concept with six subsections:

- Definition, Nature, Manifestation, Root Cause, Distinction from Adjacent Concepts, Propagation Mechanism
- Formally distinguishes Structural Degradation from: Bug, Technical Debt, Dead Code, Hallucination

**3. Taxonomy Expansion: 14 → 18 Phenomena**

Extended the degradation taxonomy from 14 to **18 phenomena** across three layers:

| Layer      | v0.3              | v1.0                                      |
| ---------- | ----------------- | ----------------------------------------- |
| Intent     | 7 phenomena       | 7 phenomena + formalized Degradation Path |
| Structural | 6 phenomena       | 6 phenomena + formalized Degradation Path |
| Behavioral | 5 phenomena       | 5 phenomena + formalized Degradation Path |
| **Total**  | **18 (numbered)** | **18 with full prose**                    |

Each phenomenon now includes:

- Full prose **Definition** (expanded from bullet-point form)
- Detailed **Distinction** with explicit comparison targets
- **Worked Example** for every phenomenon (v0.3 had examples for only selected concepts)
- **Path Logic** label identifying the degradation mode

Added **Taxonomy Summary Table** (Table 1) consolidating all 18 phenomena.

**4. Visibility Inversion Principle (§6 — Elevated to Standalone Section)**

Promoted from an inline observation within Cross-Layer Dynamics to a **dedicated section** with five subsections:

- §6.1 Detection Difficulty
- §6.2 Damage Magnitude
- §6.3 Governance Implications
- §6.4 Architectural Implications
- §6.5 Process Implications

**5. Implications for Software Engineering (§7 — New Section)**

New section articulating five categories of implications:

- Unified Ontology: taxonomy as coherent conceptual framework
- Diagnostic Orientation: three-dimensional discontinuity as diagnostic lens
- Architectural Innovation: new principles for AI-generated artifact integration
- Governance Transformation: cross-layer tracing and observability requirements
- Process Optimization: new SDLC activities for degradation-aware development

**6. Related Work (§10 — New Section)**

Systematic literature positioning across seven research directions:

- AI-Assisted Software Engineering
- Software Architecture Decay
- Technical Debt Management
- Software Evolution Governance
- AI Testing and Verification
- Software Modularity and Decomposition
- Ontological Approaches to Software Engineering

**7. Expanded References**

References expanded from 7 to **16 entries**, incorporating:

- Classical foundations: Parnas (1972), Brooks (1975), Belady & Lehman (1976), Perry & Wolf (1992)
- Ontological grounding: Gruber (1993)
- Recent AI code quality: Chen et al. (2021), Vaithilingam et al. (2022), Yetiştiren et al. (2023)

**Improvements over v0.3**

- Transformed from working manuscript to publication-ready prose
- Added formal front matter: Abstract, Keywords, JEL Classification
- Every phenomenon expanded from outline-level to full academic paragraphs
- All degradation paths within each layer formalized with explicit causal chain narratives
- Cross-layer dynamics expanded with three-level remediation strategy analysis (Behavioral/Structural/Intent intervention)
- Limitations section expanded from three concise points to five detailed subsections
- Conclusion restructured: five numbered contributions + five future research directions