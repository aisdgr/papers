# Decision Analysis — Version History

This document records the evolution of the **Decision Analysis** framework,
which defines analytical states for observable effects under anchoring conditions.

Decision Analysis is positioned as the **analysis layer** in the research stack:

Anchor Architecture → Decision Analysis → Phenomena → Decision Risk → Governance.

---

## v0.1 — Initial Analytical Structure

**Status:** Draft  
**Purpose:** Extract analytical definitions from the early Decision Risk manuscript.

### Key Characteristics

- Introduced the concept of **effect-first decision analysis**.
- Established the separation between:
  - analysis
  - governance interpretation
- Defined early analytical categories.

### Analytical States (early form)

- Normal
- Over Outcome
- Indeterminate
- Decision Vacancy

### Limitations

- Anchoring conditions not explicitly defined.
- Carrier and trace concepts still implicit.
- Analytical observability not formally stated.

---

## v0.2 — Anchor Dependency Introduction

**Status:** Revised Draft  

### Major Changes

Introduced the requirement that analysis depends on **anchoring conditions**.

New elements added:

- Effect observability requirement
- Carrier-based decision hosting
- Trace structure concept

### Analytical Consequence

Analysis cannot occur if anchoring structures are absent.

This leads to the introduction of:

**DA-U — Unobservable**

### Structural Insight

Analysis failure is not automatically a risk condition.

Unobservability is treated as an **analytical outcome**, not a governance judgment.

---

## v0.3 — Trace-Oriented Interpretation

**Status:** Draft refinement  

### Major Changes

Introduced interpretation of analytical states using **trace structures**.

Carrier-to-carrier trace chains become the engineering interpretation of:

- attribution
- boundary determination
- decision hosting

### Engineering Interpretation

Analytical states may be observed through trace patterns:

| State | Trace Interpretation   |
| ----- | ---------------------- |
| DA-N  | Trace chain consistent |
| DA-O  | Trace exceeds boundary |
| DA-I  | Multiple attribution   |
| DA-V  | Reverse trace failure  |
| DA-U  | Trace structure absent |

### Impact

Decision Analysis becomes **artifact-agnostic**.

It can operate on:

- intent → code
- specification → test
- specification → specification

---

## v0.4 — Authority Separation

**Status:** Major conceptual revision  

### Problem Addressed

Earlier drafts implicitly assumed authority analysis.

This created a risk of circular reasoning.

### Major Changes

Authority is **removed from primary analytical definitions**.

New rule:

Authority is introduced **only after effect analysis**.

### New Principle

Effect → Boundary → Attribution → Authority

Authority becomes conditional analysis for:

- DA-O clarification
- DA-V interpretation

### Result

Decision Analysis becomes:

- governance-neutral
- purely structural

---

## v0.5 — Analytical Finalization

**Status:** Final Draft  

### Major Stabilizations

The framework stabilizes into five mutually exclusive analytical states.

| State    | Meaning          |
| -------- | ---------------- |
| **DA-N** | Normal           |
| **DA-O** | Over Outcome     |
| **DA-I** | Indeterminate    |
| **DA-V** | Decision Vacancy |
| **DA-U** | Unobservable     |

### Final Analytical Principles

1. **Effect-first analysis**
2. **Carrier-agnostic artifacts**
3. **Trace-based attribution**
4. **Authority as secondary analysis**
5. **Governance excluded from analytical layer**

### Relationship to Other Works

Decision Analysis underlies several observed phenomena:

| Phenomenon         | Analytical Projection     |
| ------------------ | ------------------------- |
| Ghost Intent       | DA-V                      |
| Inference Creep    | causal source of DA-O     |
| Semantic Expansion | carrier reinterpretation  |
| Decision Risk      | governance interpretation |

### Position in Research Stack

```
Anchor Architecture  
↓  
Decision Analysis  
↓  
Observed Phenomena  
↓  
Decision Risk  
↓  
Governance
```

Decision Analysis defines **when analytical determination is possible**
and **what analytical states exist**, without prescribing governance actions.

---

## v1.0 — Manuscript Consolidation

**Status:** Submission Manuscript

### Purpose

v1.0 represents the **first consolidated manuscript version** prepared for preprint or journal submission.

Earlier versions focused on stabilizing the analytical model.  
v1.0 focuses on **clarifying scope boundaries and removing residual ambiguity between analysis and governance layers**.

---

### Major Changes

#### 1. Explicit Scope Declaration

A new **Scope of This Work** section is introduced to explicitly define the boundaries of Decision Analysis.

The paper now clearly states that it defines:

- analytical determination conditions
- analytical state taxonomy
- effect-based decision evaluation

And explicitly excludes:

- governance policy
- risk classification
- accountability attribution
- mitigation strategies

This clarification ensures Decision Analysis remains a **pure analytical framework**.

2026-03_decision-analysis_v0.5

---

#### 2. Formalization of Anchoring Preconditions

Anchoring assumptions are expanded into a structured section:

**Analytical Preconditions: Anchoring Conditions**

Three necessary conditions are now explicitly defined:

1. **Decision Carriers**
2. **Trace Structures**
3. **Effect Observability**

These conditions clarify when analysis is **structurally possible**.

If these conditions are absent, the analysis collapses to **DA-U**.

---

#### 3. Mathematical Clarification of Effect

The definition of **effect** is formalized:

$$
E_t = \Delta(S_{t_0}, S_t)
$$

Where the effect represents a detectable deviation between system states.

This strengthens the **Effect-First Principle**, making observable effect the entry point of analysis.

---

#### 4. Outcome Boundary Definition

A formal definition of the **Outcome Boundary** is introduced:

$$
B(S_t)
$$

The boundary determines whether the observed system state is within admissible scope.

Possible boundary sources include:

- carrier declarations
- trace-derived constraints
- analyst-defined scope (explicitly marked)

This clarifies how **DA-O** and **DA-V** are analytically distinguished.

---

#### 5. Analytical State Formalization

All five analytical states are now expressed using explicit logical conditions:

| State | Condition                                        |
| ----- | ------------------------------------------------ |
| DA-N  | observable effect within boundary                |
| DA-O  | observable effect outside boundary               |
| DA-I  | effect observable but attribution ambiguous      |
| DA-V  | effect observable but no decision carrier exists |
| DA-U  | no observable effect anchor                      |

This formalization ensures the analytical states remain **mutually exclusive**.

---

#### 6. Carrier-Based Engineering Interpretation

A new section introduces **carrier-based interpretation** of analytical states.

This provides an engineering projection of the abstract analytical model.

| Analytical State | Carrier Interpretation         |
| ---------------- | ------------------------------ |
| DA-N             | consistent trace chain         |
| DA-O             | reverse trace exceeds boundary |
| DA-I             | multiple candidate carriers    |
| DA-V             | no plausible decision carrier  |
| DA-U             | trace structure absent         |

This addition allows the framework to operate within **artifact-driven environments**.

---

#### 7. Explicit Separation from Governance

v1.0 strengthens the separation between analysis and governance.

The paper now explicitly states that it **does not define**:

- risk classification
- governance response
- accountability attribution

Risk interpretation is delegated to the **Decision Risk framework**, which operates on top of Decision Analysis.

---

#### 8\. Structural Position Clarification

The research stack relationship is reaffirmed:

```
Anchor Architecture
↓
Decision Analysis
↓
Observed Phenomena
↓
Decision Risk
↓
Governance
```

Decision Analysis therefore defines:

- **analytical determinability**
- **analytical state classification**

without prescribing governance actions.

---

### Summary

v1.0 does not introduce new analytical states but significantly improves the manuscript by:

- clarifying analytical scope
- formalizing anchoring preconditions
- defining outcome boundary semantics
- strengthening the effect-first analytical principle
- reinforcing the separation between analysis and governance

This version serves as the **first submission-ready manuscript** of the Decision Analysis framework.
