# Anchor Architecture  
## Structural Anchors for Traceability and Impact Examination in Agentic Software Development

**Version:** 0.22  

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Date:** February 2026  

---

## Abstract

As agentic AI systems increasingly participate in software development activities such as code generation, modification, execution, and validation, long-standing assumptions about traceability, attribution, and impact analysis no longer hold by default.

In human-driven development, engineers could directly judge why a change was made, what it affected, and how it related to specifications or prior work—either through personal understanding or with the aid of tools. With agentic AI, these relationships often become opaque: actions are carried out by probabilistic systems, intermediate reasoning is not fully observable, and post-hoc interpretation replaces structural certainty.

This paper introduces **Anchor Architecture**, a pre-analytical structural framework that defines the conditions under which relationships across artifacts, executions, time, and viewpoints become **structurally examinable**. Rather than prescribing workflows, governance mechanisms, or tools, Anchor Architecture specifies what must structurally exist for questions of traceability, attribution, and impact scope to be examined without relying on guesswork.

The framework applies not only to decision-related contexts, but also to specification–code relationships, execution–evidence alignment, multi-viewpoint systems, and impact scope analysis in agentic software development environments.

---

## Keywords

Anchor Architecture, Agentic AI, Software Development, Structural Traceability, Impact Scope Analysis, Pre-Analytical Framework

---

## 1. Introduction

Agentic AI systems are no longer limited to passive assistance. They increasingly act as autonomous or semi-autonomous participants in software development: generating code, modifying artifacts, executing pipelines, and producing validation results.

In traditional, human-authored workflows, developers could usually determine—explicitly or implicitly—why a change occurred, what it affected, and how it related to requirements or design. Even when tooling was imperfect, the human developer served as the integrator of meaning.

With agentic AI, this assumption no longer holds. Actions may be initiated or completed by systems whose internal reasoning is not observable, and whose outputs may span multiple artifacts and execution contexts. When structural references are missing, engineers are left with logs, diffs, and narratives from which they can only **guess** causal relationships.

The purpose of this work is not to interpret AI reasoning, enforce governance, or guarantee correctness. Instead, it addresses a more foundational question:

> Under what structural conditions can relationships in AI-assisted software development be examined without relying on speculation?

Anchor Architecture proposes that many failures in traceability and impact analysis arise not from insufficient tools or policies, but from the absence of explicit structural anchors that make such relationships examinable *before* analysis begins.

---

## 2. What Is an Anchor?

An **anchor** is a non-inferable structural reference that fixes a point of distinction within a system.

Anchors are not logs, tags, policies, or workflows.  
They do not describe what should happen.  
They determine what can be distinguished.

An anchor satisfies four defining properties:

1. **Pre-Analytical Existence**  
   An anchor exists before analysis, interpretation, or evaluation is attempted.

2. **Non-Reconstructibility**  
   An anchor cannot be reliably reconstructed from outputs, logs, or execution traces alone. If it is created after the fact, it loses structural authority.

3. **Structural Authority**  
   An anchor serves as a reference point against which relationships may be examined.

4. **Uniqueness**  
   **Every anchor MUST have a unique identifier.**  
   Uniqueness is a defining property of anchors, not an implementation detail.

Without uniqueness, anchors collapse into indistinguishable references, and structural examination degrades into guesswork.

---

## 3. Architectural Scope and Non-Claims

Anchor Architecture deliberately does **not** prescribe:

- workflows or processes,
- enforcement or governance mechanisms,
- tooling choices,
- or operational policies.

Its scope is limited to defining **structural prerequisites** for examinability.

How anchors are produced, enforced, or consumed belongs to the **operational layer**, not to this architecture.

---

## 4. Application Perspectives (Revised)

Anchor Architecture is examined through **two anchor-bearing application perspectives**, plus one derived structural perspective.

These perspectives are **not classification axes**, and they do not need to be jointly satisfied.

---

## 5. Carrier Perspective — Persistent Referencing

> Every anchor **must** correspond to a clear, non-ephemeral carrier.

### Definition

A carrier is a persistent, referencable artifact that can be revisited after the fact.

Valid carriers include (but are not limited to):

- Specifications (e.g., SRS, STS)
- Code artifacts (files, modules, commits, patches)
- Documents
- Logs or artifact records

Ephemeral entities—such as in-memory prompts, transient contexts, or unpersisted states—**do not** constitute valid carriers.

### Rationale

If an anchor does not resolve to a stable carrier, its relationships cannot be re-examined. In such cases, traceability relies on memory or inference and becomes **hard to determine** rather than structurally examinable.

---

## 6. Execution Perspective — Time-Bound Uniqueness

> Execution-related anchors **must** exist as carriers and be uniquely identifiable at the moment they occur.

### Execution Directives

Execution commands or directives (e.g., job definitions, pipeline steps, execution instructions):

- must be persisted as carriers,
- must be uniquely identifiable in their execution context.

Identical commands executed at different times still represent **distinct execution anchors**.

### Execution Evidence

Execution evidence (e.g., logs, reports, attestations):

- must exist as carriers,
- must correspond to exactly one execution instance,
- must not be reused across executions.

Evidence anchors are **existentially dependent** on execution anchors.

---

## 7. Scope as a Derived Anchor Set (Not an Anchor Type)

Scope is **not** a third anchor-bearing category.

> Scope is a **time-bound Anchor Set**, not an anchor itself.

### Definition

At a given moment, scope is defined by a set of anchors pointing to carriers involved in that context, such as:

- source carriers,
- target carriers,
- input carriers,
- output or modification carriers,
- execution and evidence anchors.

### Key Properties

- The Anchor Set itself does **not** require an identifier.
- **Every item in the set must have its own Anchor ID.**
- Scope is inherently time-dependent: the same carriers at different times define different scopes.

### Implication

If any item in the scope lacks an anchor or resolves to an ephemeral carrier, the scope can only be described narratively and becomes **hard to determine**, rather than structurally examinable.

---

## 8. Identifiers and Trace Structures

### Anchor Identifiers

Anchor identifiers may be represented using:

- hash-based identifiers, or
- custom-defined identifiers.

The architecture does not constrain format or generation strategy, provided uniqueness holds.  
Human-readable identifiers are recommended for inspection and communication but are not required.

---

### Trace Chain

A **Trace Chain** is a linear composition of anchors representing a causal or engineering progression.

**Example:**

```
SRS-FR-001  
→ STS-TC-012  
→ Code-Module-A  
→ Code-Module-B
```

---

### Trace Net

A **Trace Net** is a non-linear structure in which anchors are connected across perspectives and time.

**Example:**

```
SRS-FR-001  
├─ STS-TC-012  
│ ├─ Code-XXX  
│ └─ Code-YYY  
└─ Directive-20260210-AAA  
└─ Evidence-20260210-BBB
```

Trace Chains and Trace Nets are structural outcomes, not additional anchor types.

---

## 9. Structural Examinability vs. Hard-to-Determine States

When anchors exist and resolve to persistent carriers, relationships can be **structurally examined**.

When anchors are missing, ambiguous, or ephemeral:

- no explicit causal structure exists,
- only speculative explanations are possible.

This condition is defined as **hard to determine**:
there is no verifiable causal relationship, only post-hoc inference.

---

## 10. Basic Applications (Illustrative)

Anchor Architecture enables examination of:

- specification–code traceability,
- execution–evidence alignment,
- multi-viewpoint consistency,
- impact scope analysis.

It does **not** compute impact magnitude, enforce correctness, or judge desirability.  
It establishes whether such questions can be examined without guesswork.

---

## 11. Related Work

*To be completed once citation scope is finalized.*

---

## 12. References

*To be completed.*

---

## 13. Conclusion

Anchor Architecture defines anchoring as a structural prerequisite for examining relationships in agentic software development.

By separating structural existence from operational enforcement, the framework explains why many AI-assisted workflows degrade into speculation—and how that degradation can be avoided without constraining agent behavior.

Where anchors exist, relationships can be examined.  
Where anchors do not exist, interpretation replaces structure.

---

## Notes: 0.3 Plan  *(Non-Normative)*

Planned additions for version 0.3 include:

- Related Work positioning against:
  - provenance systems (e.g., PROV-DM, PBOM),
  - software supply-chain frameworks (SLSA, in-toto),
  - agentic software engineering traceability research.
- Concrete illustrative scenarios:
  - with-anchor vs. without-anchor comparisons,
  - impact scope determination examples.
- Failure modes:
  - missing anchors,
  - identifier collisions,
  - anchor bypass by agents.
- Minimal reference implementation:
  - toy example demonstrating automatic anchor injection and validation.
- Terminology refinements and glossary for non-specialist readers.
