# A Taxonomy of Degradation Phenomena in AI-Generated Code

## Abstract
--------

Generative AI introduces a structural mismatch into software engineering: code is produced through stateless probabilistic generation, yet integrated into systems that evolve through stateful, temporally constrained architectures. Existing discourse focuses on hallucinations, defects, and productivity gains, but lacks a unified account of structural degradation mechanisms unique to AI-assisted development.

This paper proposes a three-layer taxonomy of AI-generated code degradation across the Intent, Structural, and Behavioral layers. Fourteen distinct phenomena are defined, differentiated, and organized into causal degradation paths. We demonstrate that these phenomena share a common root cause—stateless generation interacting with stateful system evolution—and propagate across layers through identifiable mechanisms not reducible to hallucination, technical debt, or dead code.

The contribution of this paper is foundational. It establishes a coherent ontology of degradation patterns and their cross-layer propagation dynamics, providing a necessary conceptual foundation for future analytical, governance, and architectural research.

---

## Central Thesis

AI-generated artifacts are stateless outputs inserted into stateful systems.  
This mismatch produces layered degradation patterns that remain under-theorized in current software engineering discourse.

Stateless generation and stateful evolution create **three-dimensional discontinuities**—temporal, authorial, and state-based—that destabilize cumulative system growth and enable cross-layer degradation.

---

## Structure Overview

The paper is divided into:

1. Root Cause Model
2. Intent Layer Degradation
3. Structural Layer Degradation
4. Behavioral Layer Degradation
5. Cross-Layer Degradation Dynamics
6. Limitations and Scope

Each layer includes:

- Definition
- Distinction
- Worked example (where necessary)
- Degradation path logic

---

## 1. Root Cause: Stateless Generation vs Stateful Evolution

**Core Argument**

Traditional SDLC assumes:

- Persistent authorship
- Incremental structural evolution
- Boundary-respecting modification

AI-assisted generation violates these assumptions.

We conceptualize this mismatch as a **three-dimensional discontinuity mechanism**:

---

### 1.1 Temporal Discontinuity

Generation occurs as isolated completion events without persistent awareness of historical iterations.

Each regeneration partially resets local structure rather than extending it cumulatively.

---

### 1.2 Authorial Discontinuity

Traditional systems assume persistent authorship chains.  
AI generation disperses authorship across probabilistic outputs and transient prompts.

Artifacts lack recoverable authorial continuity.

---

### 1.3 State Discontinuity

Generation treats the system as a snapshot, not an evolving stateful organism.

Implicit architectural constraints, dependencies, and accumulated invariants may be ignored.

---

**Mechanistic Consequence**

When temporal, authorial, and state discontinuities co-exist:

Integration becomes **non-cumulative**.

Instead of extending prior structure, each generation partially reinitializes local structure.

Degradation emerges not from isolated defects, but from repeated structural resets embedded into an evolving system.

This is the causal foundation of all subsequent phenomena.

---

## 2. Intent Layer Degradation

This layer concerns instability in decision intent.

---

### 2.1 Ghost Intent
----------------

**Definition**  
Executable artifacts whose originating decision cannot be recovered.

**Distinction**  
Not undocumented code (implicit intent may exist).  
Not missing requirements (specification gap).

Ghost Intent concerns absence of origin.

**Nature:** Static absence.

**Worked Example**  
AI generates caching logic without any requirement specifying performance optimization.

---

### 2.2 Inference Creep

Generation exceeds explicit instruction boundaries.

**Distinction**  
Not hallucination.  
Not bug.  
Not traditional scope creep (deliberate negotiation outcome).

Inference Creep is probabilistic overreach without explicit decision.

---

### 2.3 Semantic Expansion

Conceptual meaning broadens during generation.

**Distinction**  
Not prompt drift.  
Not misunderstanding.

Semantic reinterpretation beyond declared meaning.

**Worked Example**  
Prompted to "validate input," generation expands validation into sanitization, normalization, and transformation.

---

### 2.4 Intent Fragmentation

Intent exists but is structurally dispersed.

**Distinction**  
Origin present; cohesion absent.

Ontological difference:  
Ghost Intent = absence of origin.  
Fragmentation = loss of cohesion.

---

### 2.5 Scope Absorption

Adjacent concerns absorbed without explicit declaration.

Boundary swallowing rather than crossing.

---

### 2.6 Intent Drift

Gradual deviation across iterations.

Not deliberate modification.  
Each local regeneration optimizes without reference to original anchor.

---

### 2.7 Intent Collision

Conflicting intents across agents or iterations.

---

**Intent Degradation Path (Causal Logic)**

Ghost Intent creates unanchored implementation conditions.  
Unanchored implementation leads to Fragmentation.  
Fragmented components evolve independently, accelerating Drift.  
Drift across multiple agents produces Collision upon integration.

---

## 3. Structural Layer Degradation

This layer concerns topology and architecture.

---

### 3.1 Ghost Code

Code whose purpose is indeterminate.

Executability ≠ Interpretability.

Dead code is unreachable.  
Ghost Code may execute but lacks recoverable origin.

In human-authored systems, interpretability can be reconstructed via authorship memory.  
In AI-generated systems, that memory is structurally absent.

---

### 3.2 Architectural Amnesia

Conflicting implicit architectural models coexist.

---

### 3.3 Rigidity Calcification

Unconscious standardization reduces structural evolvability.

Unlike technical debt (conscious trade-offs), calcification emerges from cumulative pattern uniformity.

---

### 3.4 Shadow Coupling

Undeclared dependency paths.

---

### 3.5 Interface Erosion

Incremental boundary blurring.

---

### 3.6 Dependency Blindness

Implicit external assumptions surface only upon failure.

**Worked Example**  
Generated code assumes API response order.  
API version changes silently break behavior.

---

**Structural Degradation Path (Causal Logic)**

Architectural Amnesia introduces conflicting implicit models.  
Conflict resists refactoring and hardens into Calcification.  
Calcification forces undeclared workarounds → Shadow Coupling.  
Shadow Coupling blurs boundaries → Interface Erosion.  
Erosion exposes implicit external fragility → Dependency Blindness.

---

## 4. Behavioral Layer Degradation

Behavioral degradation is a **manifestation layer**.

Runtime instability often reflects upstream discontinuities.

---

### 4.1 Conditional Blindspot

Systematic omission of rare boundary cases.

Not random bug.  
Bias correlates with generative distribution.

---

### 4.2 State Assumption Leak

Hidden state assumptions violated under specific sequences.

---

### 4.3 Observation Bias

**Distinction**  
Not incomplete logging.  
Not random monitoring gaps.

Observation Bias is directional.  
Monitoring correlates with expected behaviors, excluding anomalous ones.

This distorts feedback signals for future development.

---

### 4.4 Non-Deterministic Degradation

Not localized bug.

Load-dependent and sequence-dependent instability.  
Behavior neither consistently correct nor incorrect.

---

### 4.5 Confidence Propagation

System expresses certainty despite degraded assumptions.

Hardest to detect, as error signal is suppressed by apparent stability.

---

**Behavioral Degradation Path**

Blindspot → State Leak → Observation Bias →  
Non-Deterministic Degradation → Confidence Propagation

Confidence Propagation is terminal because false certainty suppresses detection.

---

## 5. Cross-Layer Degradation Dynamics

Degradation primarily propagates downward:

Intent → Structural → Behavioral

Abstraction loss is easier than abstraction reconstruction.  
Once intent instability embeds into structure, recovering original context becomes exponentially difficult.

---

**Propagation Mechanisms**

### 5.1 Intent → Structural

Inference Creep absorbs adjacent concerns (Scope Absorption).  
Absorbed logic standardizes into templates (Rigidity Calcification).  
Rigid templates prevent adaptation under load, enabling later instability.

---

### 5.2 Structural → Behavioral

Shadow Coupling creates hidden state dependencies.  
Hidden dependencies trigger State Assumption Leaks under stress.  
Repeated leaks produce Non-Deterministic Degradation.

---

**Diagnostic Upward Pathway**

Behavioral failures may reveal structural or intent-layer issues.  
This is diagnostic, not causal propagation.

Behavioral intervention cannot reverse upstream degradation.

---

**Visibility Inversion Principle**

Detection probability is inversely proportional to layer depth at generation time,  
but directly proportional to damage magnitude at failure time.

Intent-layer issues are cheap to detect early.  
Behavioral-layer failures are costly and late.

---

## 6. Limitations and Scope

This taxonomy is conceptual, not empirical.

Boundaries between certain intent-layer concepts may overlap.

The model assumes integration into long-lived evolving systems.  
Short-lived or disposable systems may not exhibit full degradation dynamics.

No measurement claims are made.

---

## 7. Contribution

- Root Cause Model via three-dimensional discontinuities
- Three-layer degradation taxonomy (14 phenomena)
- Cross-layer propagation model
- Conceptual differentiation from hallucination, bug, technical debt

Without layered ontology, AI degradation is systematically misclassified under traditional defect taxonomies, leading to misaligned remediation strategies.

---

## References (Expanded Foundational Support)

Parnas, D. (1972). On the Criteria To Be Used in Decomposing Systems into Modules.  
Brooks, F. (1975). The Mythical Man-Month.  
Cunningham, W. (1992). The WyCash Portfolio Management System (Technical Debt).  
Gruber, T. (1993). A Translation Approach to Portable Ontologies.  
Shumailov et al. (2023). The Curse of Recursion.  
Abbassi et al. (2025). Taxonomy of Inefficiencies in LLM Code.  
Shukla et al. (2025). Security Degradation in AI Code Generation.

(Additional empirical AI code quality literature to be incorporated in final submission draft.)
