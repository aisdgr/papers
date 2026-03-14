# Decision Risk:
> A Reproducible Forensic Framework for Identifying Decision Vacancy and Structural Risks in Automated Systems

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Date:** March 2026  

---

## Abstract

As automation and AI-assisted agents increasingly participate in software development and delivery, system risk no longer arises solely from incorrect implementations or faulty inference. An emerging class of failures originates from the structure and attribution of decisions themselves. Traditional debugging and auditing approaches, which focus on input–output behavior or execution traces, are insufficient to determine whether an observed action resulted from an explicit decision, an over-extended authorization, or the absence of any attributable decision.

This paper introduces **Decision Risk** as a unifying concept for governance and accountability risks arising from decision absence, decision over-extension, and decision indeterminacy in automated systems. We propose a reproducible forensic framework for identifying and classifying Decision Risk based on observable engineering evidence. The framework defines a minimal set of decision-relevant artifacts—including scope specifications, authority models, directive records, and execution traces—and enforces a strict evaluation order: scope stability must be established first, inference-based explanations must be excluded next, and only then may decision-related risks be assessed.

Decision Risk is systematically classified into three mutually exclusive categories: **Decision Vacancy**, where no attributable authority exists; **Over Decision Risk**, where a valid decision introduces structural risk through excessive scope, duration, or context insensitivity; and **Indeterminate Decision Risk**, where insufficient or structurally incomplete evidence prevents reliable classification. Crucially, this work argues that indeterminacy is not an analytical failure but a property of systems whose decision evidence is inadequate.

By reframing responsibility analysis as a forensic engineering problem rather than an outcome-based judgment, this framework enables reproducible, defensible evaluation of decision-related risks in automated software development pipelines, including LLM-based coding agents and CI/CD automation. Scope Drift and Inference Creep are treated as exclusionary conditions and will be addressed in separate studies.

---

## 1. Introduction

Software systems are increasingly shaped by automated execution pipelines and AI-assisted agents that generate, modify, and deploy code with minimal human intervention. In such environments, failures are often diagnosed through behavioral anomalies, test regressions, or incorrect outputs. However, these symptoms obscure a deeper governance challenge: determining whether a system action resulted from an explicit decision, an overly permissive decision, or no decision at all.

As automation accelerates execution velocity, traditional assumptions about decision-making—namely that decisions are explicit, attributable, and reviewable—begin to erode. Responsibility analysis becomes ambiguous when behavior appears legitimate but lacks a traceable decision basis. This ambiguity introduces a distinct class of risk that cannot be reduced to inference error or implementation defect.

This paper argues that **decision structure itself** has become a primary source of risk in automated software systems. We introduce *Decision Risk* as an analytical lens for identifying and classifying such risks using reproducible engineering evidence rather than outcome-based intuition.

---

## 2. From Behavioral Failure to Decision Risk

Conventional software analysis methods implicitly assume that if a system behaves incorrectly, the root cause must lie in faulty logic, incorrect inference, or inadequate testing. In AI-assisted development, this assumption fails in two ways.

First, automated agents may produce behavior that is technically correct within allowed boundaries yet strategically or operationally harmful. Second, some harmful behaviors arise not from errors but from the absence of any explicit decision governing the action.

Treating all unintended outcomes as inference failures or bugs leads to misattribution. Decision Risk reframes the problem: the central question is not *what happened*, but *what decision—if any—authorized it*.

---

## 3. Observability Prerequisites for Reproducible Analysis

Decision Risk analysis is only meaningful when based on reproducible evidence. This work defines a **minimal observable set** required for forensic evaluation within software development and delivery contexts.

### 3.1 Required Elements

The following artifacts must be available and version-aligned:

- **Scope specification**  
  Explicit definition of input scope (what information may influence execution) and output scope (what artifacts may be modified).
- **Authority model**  
  Allow, deny, or default rules governing execution permissions.
- **Directive record**  
  A record of the command or instruction initiating execution, captured prior to execution.
- **Execution trace**  
  Observable evidence of actions taken during execution.
- **Artifact diff**  
  Concrete changes produced by execution.

---

### 3.2 Evidence Sufficiency and Information Asymmetry

Evidence may be present yet structurally insufficient. For example, execution traces without corresponding directive records create asymmetry between intent and behavior. Such asymmetry directly leads to indeterminate outcomes, as discussed in Section 5.3.

---

## 4. Evaluation Order and Exclusion Conditions

Decision Risk must not be assessed in isolation. Two exclusionary checks are mandatory and must be evaluated first.

### 4.1 Scope Drift

If the effective execution scope differs from the declared scope without an explicit scope-change decision, the analytical baseline is invalid. In such cases, decision analysis is suspended.

### 4.2 Inference Creep

If observed behavior can be sufficiently explained by inference expansion—i.e., the system derives new objectives or interpretations beyond the declared input scope—decision attribution is inappropriate. In accordance with the principle of minimal assumptions, inference-based explanations take precedence over structural decision analysis.

Only when **both Scope Drift and Inference Creep are excluded** may Decision Risk be evaluated.

---

## 5. Decision Risk Taxonomy

Decision Risk is defined as governance and accountability risk arising from the existence, structure, or determinability of decisions in automated systems.

The taxonomy comprises three mutually exclusive and collectively exhaustive categories.

---

### 5.1 DR-V: Decision Vacancy

**Definition.**  
Decision Vacancy occurs when no attributable authority exists for an observed execution path, despite sufficient and reproducible evidence.

**Characteristics.**

- No corresponding authority rule exists, or
- Authority exists but is not attributable to any accountable role.

Decision Vacancy represents the most severe form of Decision Risk, as responsibility cannot be assigned or corrected without structural intervention.

---

### 5.2 DR-O: Over Decision Risk

**Definition.**  
Over Decision Risk arises when a valid, attributable decision introduces systemic risk due to its structure rather than its absence.

**Subtypes include:**

- **Delegation Risk:** Excessive delegation of discretion to automated agents.
- **Granularity Risk:** Decisions too coarse to distinguish high-risk and low-risk paths.
- **Temporal Risk:** Decisions that persist beyond their original context.
- **Context Risk:** Decisions applied across incompatible environments or artifacts.
- **Cascade Risk:** Decisions amplified across multi-stage pipelines.

In these cases, responsibility exists, but the decision design itself creates risk.

---

### 5.3 DR-I: Indeterminate Decision Risk

**Definition.**  
Indeterminate Decision Risk arises when available evidence is insufficient or structurally incomplete, preventing reliable classification as either DR-V or DR-O.

**Causes include:**

- Missing directive records
- Incomplete execution traces
- Overly broad scope or authority definitions

Indeterminacy is not an analytical failure. It is a property of systems that cannot support accountable decision analysis.

---

## 6. Discussion: Decision Risk as a Governance Problem

Decision Risk highlights a shift in software governance: correctness alone is insufficient. Systems must also support decision traceability and accountability.

Notably, the presence of a decision does not imply safety. Over Decision Risk demonstrates that explicit authority can be more dangerous than absence when amplified by automation.

Equally important, Indeterminate Decision Risk reveals that systems incapable of supporting analysis are themselves governance risks, regardless of observed outcomes.

---

## 7. Limitations and Future Work

This work is intentionally scoped to software development and delivery contexts where execution artifacts and authority models are observable. Extensions to runtime agents, organizational decision systems, or societal governance are outside the scope of this study.

Scope Drift and Inference Creep are treated as exclusion conditions and will be addressed in dedicated future work.

---

## 8. Conclusion

Decision Risk reframes responsibility analysis in automated systems from outcome-based judgment to forensic evaluation. By enforcing reproducible evidence requirements and a strict evaluation order, this framework distinguishes between missing decisions, over-extended decisions, and fundamentally indeterminate situations.

As automation continues to reshape software engineering, the ability to analyze decisions—not just behavior—will become a prerequisite for effective governance.
