# Decision Analysis
> An Anchor-Based Analytical Framework for Effect-Oriented Decision Determination

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Date:** March 2026  

---

## Abstract

Modern automated systems increasingly generate observable effects without transparent decision traceability. Traditional input–output validation fails to distinguish whether an outcome results from intended decisions, inference expansion, structural omission, or analytical insufficiency.

This work proposes an anchor-based Decision Analysis framework that determines analytical states solely through observable effects and traceable decision carriers. The framework deliberately separates analytical determination from governance interpretation.

Five mutually exclusive analytical states are defined: **DA-N (Normal), DA-O (Over Outcome), DA-I (Indeterminate), DA-V (Decision Vacancy), and DA-U (Unobservable).**

The framework assumes the existence of anchoring conditions but does not prescribe governance responses. Risk interpretation is explicitly excluded from this work.

---

## Keywords

---

## 1. Scope of This Work

This paper defines:

- When analysis is possible
- What analytical states exist
- How those states are determined

This paper does **not** define:

- Governance policies
- Accountability attribution
- Risk mitigation strategies
- Semantic intent correctness

---

## 2. Analytical Preconditions: Anchoring Conditions

Decision Analysis requires the existence of minimal anchoring structures.

### 2.1 Decision Carriers

A **Decision Carrier** is any artifact capable of hosting or propagating a decision.

Examples (non-exhaustive):

- Intent declarations
- Requirements documents
- Specifications
- Test artifacts
- Interface contracts
- Configuration artifacts
- Implementations

Analysis is carrier-agnostic.

---

### 2.2 Trace Structure

A **trace** is a carrier-to-carrier propagation relation.

```
Carrier_A → Carrier_B
```

Traces may exist between:

- Intent → Specification
- Specification → Test
- Specification → Implementation
- Test → Implementation
- Specification → Specification

This framework does not assume a specific artifact type.

---

### 2.3 Effect Observability

An **effect** is defined as a detectable state deviation:

$$
E_t = \Delta(S_{t_0}, S_t)
$$

Where:

- $S_{t_0}$  = prior system state
- $S_t$  = current system state

An effect may be:

- Output-level deviation
- Configuration change
- Interface exposure
- Structural modification
- Traceable state mutation

---

### 2.4 Outcome Boundary

An outcome boundary  $B$  defines admissible system states.

$$
B(S_t) = \begin{cases} 1 & \text{if } S_t \text{ within admissible scope} \\ 0 & \text{otherwise} \end{cases}
$$

Boundary sources may include:

- Explicit carrier declarations
- Trace-derived constraints
- Analyst-defined scope (explicitly marked)

---

## 3. Effect-First Principle
--------------------------

Decision Analysis proceeds from observable effect.

Analysis does not begin with intent or authority assumptions.

```
Observe Effect
      ↓
Establish Boundary
      ↓
Evaluate Traceability
      ↓
Determine Analytical State
```

Authority considerations are introduced only conditionally.

---

## 4. Analytical State Definitions
--------------------------------

Five mutually exclusive states are defined.

### 4.1 DA-N — Normal

Conditions:

$$
\mathcal{O}(E_t) = 1 \land B(S_t) = 1
$$
- Effect observable
- Within established boundary
- Trace consistent

No analytical anomaly.

---

### 4.2 DA-O — Over Outcome

Conditions:

$$
\mathcal{O}(E_t) = 1 \land B(S_t) = 0
$$
- Effect observable
- Outside established boundary

No governance conclusion implied.

Possible causal sources include:

- Inference expansion
- Delegation propagation
- Default behavior
- Configuration inheritance
- Structural permissiveness

DA-O is an analytical classification only.

---

### 4.3 DA-I — Indeterminate

Conditions:

$$
\mathcal{O}(E_t) = 1 \land B(S_t) = 0 \land |\mathcal{L}| > 1 \land \nexists \ell^*
$$

Where:

-  $\mathcal{L}$  = set of plausible decision-bearing loci
-  $\ell^*$  = uniquely attributable locus

Effect is observable but cannot be stably attributed.

---

### 4.4 DA-V — Decision Vacancy

Conditions:

$$
\mathcal{O}(E_t) = 1 \land B(S_t) = 0 \land \forall d_i \in \mathcal{D},\ d_i \not\models E_t
$$

Where:

-  $\mathcal{D}$  = identifiable decision-bearing carriers within engineering scope

No carrier can plausibly host the observed effect.

Authority consideration is introduced only at this stage.

---

### 4.5 DA-U — Unobservable

Condition:

$$
\mathcal{O}(E_t) = 0
$$

No observable effect anchor exists.

DA-U is an analytical result, not a risk state.

---

## 5. Carrier-Based Interpretation (Engineering Context)

In trace-enabled environments, analytical states may be instantiated as:

| Analytical State | Carrier-Based Interpretation              |
| ---------------- | ----------------------------------------- |
| DA-N             | Trace chain consistent                    |
| DA-O             | Reverse trace exceeds declared boundary   |
| DA-I             | Multiple or unstable carrier attribution  |
| DA-V             | Reverse trace yields no plausible carrier |
| DA-U             | No trace structure present                |

These interpretations instantiate, but do not redefine, the analytical categories.

---

## 6. Relationship to Observed Phenomena

This framework underlies, but does not define:

- Ghost Intent (DA-V under intent-to-code projection)
- Inference Creep (a causal source of DA-O)
- Semantic Expansion (carrier reinterpretation phenomena)

These phenomena are treated in separate works.

---

## 7. Authority Introduction (Conditional Layer)
----------------------------------------------

Authority is not a primary analytical dimension.

Authority considerations are introduced only when:

- DA-O cannot be structurally explained, or
- DA-V is detected

Authority analysis determines whether:

- Over-permissive delegation exists
- Structural vacancy exists

Authority is therefore secondary to effect analysis.

---

## 8. Analytical Completeness

Decision Analysis assumes:

- Observable effect anchor
- Boundary definability
- Carrier traceability

When any of these are absent, analysis collapses to DA-U.

Unobservability cannot be converted into risk classification.

---

## 9. Exclusions

This work explicitly excludes:

- Governance interpretation
- Risk taxonomy
- Accountability allocation
- Organizational policy evaluation
- Human intent validation

These are addressed in separate governance-layer works.

---

## 10. Conclusion

Decision Analysis defines a minimal analytical framework for determining decision states in automated systems.

It separates:

- Observability from governance
- Effect classification from risk interpretation
- Structural vacancy from semantic disagreement

Anchors determine whether analysis is possible.  
Analytical states determine what can be said.  
Governance begins only after analysis concludes.

---

## 11. Related Work

---

## References
