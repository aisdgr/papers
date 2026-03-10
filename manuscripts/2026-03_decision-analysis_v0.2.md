# Decision Analysis — Terminology and Conceptual Foundations (v0.11)

> **Scope note**  
> This document defines terminology and conceptual categories related to decisions,
> authority, and risk in engineering-stage systems.
>  
> It does **not** introduce decision elements, formal analysis procedures,
> or formula-based determination methods.
>  
> All content in this document is descriptive and non-normative.

---

## 1. Introduction

As automated and AI-assisted systems increasingly participate in engineering-stage activities,
decisions are often enacted without being explicitly defined, recorded, or conceptually bounded.

Discussions about correctness, quality, or performance frequently obscure a more fundamental issue:
**what constitutes a decision, how its effects manifest, and when such manifestations indicate risk
at the governance level**.

This document serves as a **terminological and conceptual foundation**.
It consolidates and stabilizes the core concepts previously discussed under the *Decision Risk*
line of work, without introducing analytical methods or evaluative criteria.

---

## 2. Decision (Conceptual Definition)

A **Decision** is not treated as a discrete action, command, or event.

Instead, within this framework, a decision is understood as:

> A latent structural commitment that enables or constrains a range of possible execution effects.

Key clarifications:

- A decision may exist without being explicitly stated.
- A decision may be enacted through tools, agents, configurations, or defaults.
- The presence of an outcome does not imply the presence of an explicit decision.

This definition deliberately avoids assumptions about intent, correctness, or responsibility.

---

## 3. Decision Authority

**Decision Authority** refers to the structural capability by which a system, agent, or configuration
is able to produce effects that would normally require deliberate choice.

Authority in this context is:

- Structural, not moral
- Enabling, not evaluative
- Observable only through its effects, not through intent

Authority is not judged as legitimate or illegitimate in this document.

---

## 4. Decision Authority Effect (DAE)

**Decision Authority Effect (DAE)** denotes the observable consequences enabled by a given authority configuration.

DAE is defined as:

> The set of execution effects that become possible or reachable due to an authority configuration,
> regardless of whether a decision was explicitly recorded.

Important boundaries:

- DAE is not a decision.
- DAE is not a judgment.
- DAE is an observable effect surface.

DAE provides a vocabulary for discussing authority without invoking governance conclusions.

---

## 5. Over Outcome

**Over Outcome** describes an observable condition in which system effects exceed what was
initially expected or assumed.

Over Outcome:

- Is a descriptive phenomenon, not a diagnosis
- Does not imply error, failure, or risk by itself
- Serves only as an indication that further conceptual examination may be required

Over Outcome is intentionally decoupled from correctness and severity.

---

## 6. Decision Risk (Conceptual Category)

**Decision Risk** is a governance-oriented concept describing situations in which
decision-related structures introduce uncertainty, exposure, or loss of accountability.

In this document, Decision Risk is defined conceptually, not analytically.

Key properties:

- Decision Risk may exist even when outcomes are correct.
- Decision Risk is independent of implementation defects.
- Decision Risk concerns governance visibility, not system performance.

---

## 7. Decision Risk Categories (Terminology)

The following categories describe **types of decision-related risk conditions**.
They are classifications of meaning, not analytical results.

### DR-V — Decision Vacancy

A condition in which:

- Observable authority effects exist
- No explicit or attributable decision structure can be identified

Decision Vacancy highlights the absence of decision representation, not the presence of error.

---

### DR-O — Over Decision Risk

A condition in which:

- Decisions are identifiable or attributable
- The resulting authority effects extend broadly, persistently, or non-convergently

This category describes structural exposure, not misbehavior.

---

### DR-I — Indeterminate Decision Risk

A condition in which:

- Authority effects are observable
- Available information is insufficient to determine whether a decision structure exists

Indeterminacy is treated as a legitimate governance concern, not an analytical failure.

---

## 8. Normal Decision (Baseline Concept)

For completeness, this framework also recognizes a **Normal Decision** condition,
in which:

- Decisions are conceptually identifiable
- Authority effects are bounded and explainable
- No governance ambiguity is apparent at the conceptual level

This category provides a baseline reference and does not imply optimality.

---

## 9. Relationship to Governance

This document does not perform governance evaluation.

However, the concepts defined here enable governance discussions by:

- Making implicit decision structures discussable
- Providing a shared vocabulary for authority-related effects
- Separating descriptive conditions from normative judgment

Interpretation, responsibility assignment, and policy implications are explicitly out of scope.

---

## 10. Conclusion

This document establishes a stable conceptual vocabulary for discussing decisions,
authority, and risk in engineering-stage systems.

By separating terminology from analysis and governance judgment,
it provides a neutral foundation upon which multiple analytical
or governance-oriented works may build.

---

> **This document defines what decision-related conditions mean.  
> It does not determine what should be done about them.**
