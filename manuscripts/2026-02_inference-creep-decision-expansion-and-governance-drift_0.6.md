# An Anchor Architecture for Observing Decision-Level Phenomena in AI-Assisted Software Development

**Author:** Spark Tsai  
**Date:** February 2026  
**Category:** cs.SE (Software Engineering)  
**Keywords:** Inference Creep, AI-Assisted Software Engineering, Decision Expansion, Governance Drift, Decision Accountability, Traceability, Probabilistic Systems, Decision Boundary, AI4SE, Human-AI Decision Making
---

## Abstract

This paper introduces **Inference Creep** as an engineering-level governance phenomenon in AI-assisted software engineering: the gradual and unauthorized expansion of AI-mediated decision influence beyond its originally authorized boundary.

Unlike traditional software risks that stem from faulty implementations or incorrect outputs, Inference Creep arises when AI systems participate in decisions without explicit authorization, traceability, or boundary definition. We argue that this risk cannot be adequately addressed by runtime controls or output filtering alone.

Crucially, this paper demonstrates that Inference Creep is not merely a conceptual concern. It is **engineering-detectable, observable, and reproducible** through minimal structural criteria that link specifications and execution artifacts. By reframing AI risk as a **decision-stage governance problem**, this work positions Inference Creep as a distinct and falsifiable risk category within software engineering.

---

## 1. Introduction

AI-assisted tools are now deeply embedded in modern software engineering workflows, including code generation, refactoring, testing, review, and deployment. While these systems are often framed as productivity aids, their influence increasingly extends into areas traditionally governed by human decision authority.

This shift introduces a structural risk that is insufficiently captured by existing discussions of model accuracy, bias, or hallucination. The core issue is not whether AI outputs are correct, but **whether AI is making or shaping decisions it was never authorized to influence**.

This paper addresses that gap by defining **Inference Creep** as a software engineering phenomenon. It argues that current governance approaches focus disproportionately on runtime behavior, while neglecting the decision formation stage where governance boundaries should be enforced.

---

## 2. From Feature Creep to Inference Creep

In traditional software engineering, **Feature Creep** describes the uncontrolled expansion of system functionality beyond its original scope. Feature Creep is visible, measurable, and typically managed through requirement control and scope management.

**Inference Creep**, by contrast, does not introduce new features or capabilities. Instead, it alters **who participates in decisions and how far that participation extends**.

Key distinctions include:

- No change in model architecture or parameters  
- No explicit addition of system functionality  
- A shift in decision influence without corresponding authorization  

Inference Creep therefore represents a **boundary violation**, not a functional expansion. The affected boundary is not an API or module interface, but a **decision boundary**.

---

## 3. Decision Expansion and Boundary Erosion

In AI-assisted development environments, decision influence often expands incrementally:

- Suggestions become defaults  
- Defaults become expectations  
- Expectations become de facto authority  

Because these transitions are gradual and probabilistic, they are rarely documented as explicit design changes. As a result, the system’s decision boundary erodes without formal recognition.

Unlike traditional software boundaries enforced through interfaces or contracts, decision boundaries in AI-assisted workflows often lack concrete artifacts. This absence makes boundary violations difficult to detect using conventional engineering tools.

---

## 4. Probabilistic Amplification and Risk Acceleration

Large language models operate through probabilistic inference. When AI-generated suggestions influence subsequent decisions, early deviations can propagate and amplify across development stages.

This creates **Risk Acceleration**, where:

- A minor, unreviewed inference influences later design choices  
- Subsequent AI interactions build upon earlier decisions  
- Errors or overreach compound rather than self-correct  

Importantly, this amplification is not a statistical anomaly but a structural property of probabilistic decision chains. Runtime correctness checks may catch individual failures, but they cannot prevent systemic drift originating at the decision formation stage.

---

## 5. Engineering-Detectable Criteria for Inference Creep

To avoid reducing Inference Creep to a purely semantic concept, we introduce a **minimal, engineering-level detection criterion** based on traceability between specification and execution.

### 5.1 System Entities

Let:

- **S_spec** denote the set of authorized specifications or documented intents.
- **E_exec** denote the set of executed behaviors, code changes, or AI-mediated decisions.
- Each element in both sets may optionally carry a **Trace ID**, serving as an anchor between intent and execution.

### 5.2 Trace-Based Creep Criterion

For any executed element *e* ∈ E_exec:

- **Authorized execution**  
  If there exists *s* ∈ S_spec such that  
  `TraceID(e) = TraceID(s)`

- **Inference Creep**  
  If  
  `TraceID(e) ∉ { TraceID(s) | s ∈ S_spec }`

This criterion does not require complex mathematics. It relies solely on the presence or absence of traceable authorization.

### 5.3 Engineering Interpretation

This formulation yields immediate, practical interpretations:

- A specification exists, but no corresponding execution → *Unimplemented intent*
- One specification maps to multiple executions → *Decision expansion*
- Execution exists without specification → *Unauthorized decision*
- Introduction of a new Trace ID without prior authorization → *Future Inference Creep*

Inference Creep is therefore defined as **crossing an authorization boundary**, not as producing an incorrect output.

---

## 6. Limits of Runtime Controls

Runtime controls—such as output filtering, policy enforcement, or execution-time checks—operate after decisions have already been formed.

While necessary for operational safety, they cannot address inference creep because:

- They react to outcomes, not decision formation
- They filter content, not authority
- They cannot reconstruct intent or authorization after the fact

Inference creep is therefore not a runtime failure. It is a **decision-stage governance failure**.

---

## 7. Governance Observability Gap and Orphaned Decisions

A critical consequence of inference creep is the emergence of what we term a **Governance Observability Gap**.

In engineering terms, a decision that cannot be traced to an authorized source should be treated as an **orphaned decision**.

An orphaned decision is not defined by incorrect output.  
It is defined by **missing provenance**.

> A decision without traceability is not merely risky; it is ungoverned.

From a software engineering perspective, orphaned decisions are analogous to dangling pointers or unreferenced processes: their existence signals structural integrity failure, regardless of whether immediate faults are observed.

Importantly, the absence of traceability itself constitutes observable governance risk. Governance failure does not require misbehavior to manifest; it is present the moment decision provenance becomes indeterminate.

This reframes audit and compliance from “detecting violations” to **detecting orphaned decision artifacts**.


---

## 8. Scope and Intentional Non-Solutions

This paper deliberately avoids prescribing specific governance frameworks, tooling, or enforcement mechanisms. Its contribution lies in establishing **a falsifiable engineering definition** of Inference Creep.

Subsequent work may explore how decision boundaries are defined, authorized, or enforced. However, such solutions are only meaningful once the phenomenon itself is rendered observable and testable.

---

## 9. Conclusion

Inference Creep represents a distinct class of risk in AI-assisted software engineering—one that originates at the decision formation stage rather than at execution or output.

By providing an engineering-detectable definition grounded in traceability and authorization boundaries, this paper demonstrates that Inference Creep is neither abstract nor inevitable. It is a measurable governance failure.

As AI systems increasingly participate in software development decisions, the ability to detect and reason about unauthorized decision expansion will become a foundational requirement for trustworthy engineering practice.
