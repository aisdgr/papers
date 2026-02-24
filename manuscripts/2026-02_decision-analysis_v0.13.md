# Decision Analysis  
## Effect-First and Authority-Conditional Classification of Decision States  
**Version: v0.13**

> **Version Note (v0.13)**  
> This version stabilizes an *effect-first, asymmetric two-phase inference structure*.  
> Authority is **not** defined as a primary analytical construct.  
> It is introduced **only when logically required** to establish a Decision Vacancy.  
>  
> This document defines **decision analysis results**, not governance judgments  
> and not risk evaluation.

---

## Abstract

As automated and AI-assisted systems increasingly participate in engineering-stage execution, decision-relevant effects are frequently produced without explicit decision representation. Traditional evaluation approaches emphasize outcome correctness or system quality, leaving the underlying decision structure opaque and non-reproducible.

This paper introduces **Decision Analysis** as an engineering-stage analytical framework that classifies observable decision-related effects **prior to governance interpretation**. The proposed approach adopts an intentionally asymmetric inference structure. Observable effects are analyzed first without assuming the existence of decision authority. Authority is considered only in a secondary interpretive phase when required to establish the absence of a decision-bearing locus.

The framework defines a closed set of analytical outcomes—**DA-N, DA-O, DA-I, DA-V, and DA-U**—distinguishing observable, indeterminate, vacant, and unobservable decision states. Importantly, not all analytical outcomes constitute decision risk. In particular, unobservability is treated as an analytical result rather than a risk condition, as it cannot be determined through engineering means.

Decision Analysis is presented as an enabling analytical layer that determines whether decision-related phenomena are observable, classifiable, and eligible for subsequent governance interpretation.

---

## 1. Introduction

Engineering-stage systems increasingly exhibit decision-like behavior without explicit decision artifacts. Effects emerge through automation, pipelines, defaults, and tool interactions, often without a clearly identifiable decision event.

This work does not ask whether a decision was correct, optimal, or justified.  
Instead, it asks a more fundamental question:

> **Can a decision-related phenomenon be observed, analyzed, and classified
> without presupposing governance constructs?**

Decision Analysis is positioned as a prerequisite analytical layer. Governance, accountability, and risk interpretation are treated as subsequent concerns and are intentionally excluded from this paper.

---

## 2. Scope and Assumptions

This work is strictly scoped to **Engineering-stage Decision Behavior (EDB)**.

### Assumptions

- Decisions may be implicit or latent.
- Effects may be produced without explicit commands.
- Outcome correctness is not an analytical criterion.
- Analysis must be reproducible without normative judgment.

The framework does not address organizational authority, policy compliance, or responsibility attribution.

---

## 3. Decisions as Latent Structures

A decision is not treated as an observable event.

Instead, a decision is understood as a **latent structural commitment** that enables or constrains a range of possible effects. Effects may manifest even when no explicit decision record exists.

Consequently, decision analysis cannot rely on intent, command logs, or approval records as primary evidence. Observable effects must be analyzed directly.

---

## 4. Effect-First Analysis Principle

This framework adopts an **effect-first analytical principle**:

> **Analysis begins with observable effects, not assumed decision structures.**

No decision authority, responsibility, or governance concept is introduced at this stage. Effects are treated as descriptive phenomena relative to an assumed or declared outcome boundary.

---

## 5. Anchoring Preconditions

Decision Analysis presupposes minimal anchoring conditions.

Anchors are **existence conditions**, not analytical steps.

### 5.1 Scope Anchoring
An identifiable reference for what constitutes inside vs. outside an outcome boundary.

### 5.2 Effect Anchoring
Observable differences, expansions, or manifestations.

### 5.3 Decision Admissibility
Acceptance that effects may originate from latent decisions.

If anchoring cannot be established, analysis proceeds but may result in an unobservable outcome (DA-U).

---

## 6. Asymmetric Two-Phase Inference Structure

Decision Analysis is intentionally **asymmetric**.

### Phase 1 — Effect-Based Classification
- Authority-free
- Governance-free
- Produces DA results

### Phase 2 — Authority-Conditional Interpretation
- Invoked **only when necessary**
- Used exclusively to establish Decision Vacancy

Authority is **not** a general analytical primitive.

---

## 7. Decision Analysis Result States

Decision Analysis yields one of the following analytical outcomes.

---

### 7.1 DA-N — Normal Decision State

- Effects are observable.
- No over outcome is identified.
- Effects are explainable within assumed boundaries.

DA-N does not imply optimality or correctness.  
It indicates the absence of decision-relevant anomalies.

---

### 7.2 DA-O — Over Outcome State

- Effects are observable.
- Outcomes exceed assumed or declared boundaries.
- Effects are explainable at the effect level.

DA-O does **not** imply risk or authority failure.  
It indicates over-extension without structural classification.

---

### 7.3 DA-I — Indeterminate Decision State

- Effects are observable.
- Anchoring or attribution is insufficient for stable classification.

DA-I is a **decidable analytical result**, not a failure.  
It deterministically induces **Indeterminate Decision Risk (DR-I)** at the governance layer.

---

### 7.4 DA-V — Decision Vacancy State

- Effects are observable.
- Over outcome is present.
- No decision-bearing locus can be identified.

DA-V requires **authority-conditional interpretation**.  
Authority is introduced **only** to establish the absence of any structure capable of hosting the implied decision.

---

### 7.5 DA-U — Unobservable Decision State

- Analysis has been attempted.
- No observable anchors can be established.

DA-U is an analytical outcome indicating **structural unobservability**.

> **DA-U is not a risk classification.**

Unobservability cannot be engineered into comparison, estimation, or attribution.  
Any escalation beyond acknowledgment requires human judgment.

---

## 8. Mapping to Decision Risk (Informative, Non-Normative)

| Decision Analysis Result | Governance Interpretation              |
| ------------------------ | -------------------------------------- |
| DA-N                     | No Decision Risk                       |
| DA-I                     | DR-I                                   |
| DA-O                     | DR-O *or* DR-V (authority-conditional) |
| DA-V                     | DR-V                                   |
| DA-U                     | Not applicable                         |

This mapping is informative only.  
Risk interpretation is outside the scope of this paper.

---

## 9. Boundary of Interpretation

This paper does **not**:

- Assign responsibility
- Evaluate severity
- Recommend controls
- Define policy

Decision Analysis determines **whether governance discussion is eligible**, not what that discussion should conclude.

---

## 10. Conclusion

Decision Analysis establishes a reproducible, effect-first analytical foundation for engineering-stage decision behavior.

By separating:
- observability from risk,
- analysis from governance,
- effects from authority,

the framework prevents premature escalation and false precision.

> **Not all uncertainty is risk.  
> Not all effects imply decisions.  
> Authority appears only when absence must be proven.**

Decision Analysis enables governance—but does not perform it.
