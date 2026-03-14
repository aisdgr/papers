# Decision Risk
> Governance Interpretation of Decision Analysis Undecidability

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Date:** March 2026  
**Status:** Conceptual Governance Paper (SSRN)

---

# Abstract

As AI systems increasingly participate in software development and operational decision-making, existing discussions of risk remain primarily outcome-oriented, focusing on incorrect results, harmful behaviors, or system failures. Such perspectives implicitly assume that the decisions being evaluated are already legitimate and governable objects.

This paper challenges that assumption.

We introduce **Decision Risk (DR)** as a governance-relevant condition arising when **Decision Analysis (DA)** determines that a decision’s legitimacy cannot be established at formation time. Decision Risk does not measure the probability of harm or failure. Instead, it describes the structural situation in which governance cannot determine whether a decision falls within legitimate scope, authority, or boundary conditions.

The purpose of this paper is not to redefine Decision Analysis. Rather, it explains why **DA-identified undecidability must be interpreted as risk from a governance perspective**, and characterizes the categories, causes, and implications of such risk conditions.

By establishing Decision Risk as the governance interpretation of DA results, this work clarifies the relationship between analytical validity and governance applicability in AI-assisted systems.

---

## Keywords

---

## 1。 Introduction

The integration of AI into engineering and operational workflows has significantly increased the speed and scale at which decisions are produced. AI-assisted systems can generate code, configuration changes, architectural suggestions, and operational actions with minimal human intervention.

Most governance frameworks evaluate these systems through outcome-based perspectives, asking whether the resulting behavior is correct, safe, or compliant. While these approaches are valuable, they implicitly assume that the decisions being evaluated are already legitimate objects of governance.

In practice, many AI-assisted decisions are formed under conditions where legitimacy cannot be determined. Their scope may be unclear, their authorization may be implicit, or their boundaries may be undefined. Such decisions may still produce correct outcomes, yet they remain structurally ambiguous with respect to governance.

To address this gap, a separate work introduces **Decision Analysis (DA)** as a formal method for evaluating whether a decision satisfies the structural conditions required for legitimate formation. DA examines artifacts, boundaries, authorization structures, and decision evidence to determine whether a decision is **decidable** from a governance perspective.

This paper focuses on a different question:

**What does it mean for governance when Decision Analysis determines that a decision is undecidable?**

The answer to this question is defined here as **Decision Risk (DR)**.

---

## 2. Decision Formation and Governance Applicability

Governance frameworks generally assume the existence of a stable decision object. Policies, rules, and auditing mechanisms operate on the premise that a decision has identifiable scope, traceable authority, and bounded applicability.

However, AI-assisted decision environments often compress multiple phases of reasoning into a single generation step. Intent interpretation, scope determination, and execution planning may occur simultaneously within probabilistic inference.

Under these conditions, the legitimacy of a decision may never be explicitly established. Instead, governance mechanisms evaluate only the observable outcome.

This creates a structural gap:

Governance may attempt to regulate decisions whose **formation conditions are unknown or undecidable**.

Decision Analysis addresses this gap by evaluating decision legitimacy before execution. When DA determines that legitimacy cannot be established, the resulting condition is interpreted here as **Decision Risk**.

---

## 3. Relationship Between Decision Analysis and Decision Risk

Decision Analysis and Decision Risk serve distinct roles.

Decision Analysis provides the **methodological process** for determining whether a decision is structurally valid.

Decision Risk provides the **governance interpretation** of DA outcomes.

The relationship can be summarized as follows:

| Concept                | Role                                                    |
| ---------------------- | ------------------------------------------------------- |
| Decision Analysis (DA) | Determines whether a decision is structurally decidable |
| Decision Risk (DR)     | Interprets undecidable decisions as governance risk     |

Thus, Decision Risk does not arise independently. It emerges **only after Decision Analysis identifies structural undecidability**.

This distinction ensures that Decision Risk remains grounded in analytical evidence rather than subjective interpretation.

---

## 4. Structural Definition of Decision Risk

Decision Risk occurs when a decision's legitimacy cannot be determined at the moment of formation.

Formally:

$$
DR = \neg Decidable(Scope, Boundary, Authority)
$$

Where:

- **Scope** represents the domain of applicability of the decision.
- **Boundary** represents the limits within which the decision is authorized to operate.
- **Authority** represents the traceable source of authorization or accountability.

If any of these conditions cannot be evaluated or verified through Decision Analysis, the decision becomes **undecidable**, producing Decision Risk.

This formulation is intentionally non-probabilistic. Decision Risk does not measure likelihood or severity; it identifies the absence of governance determinability.

---

## 5. Categories of Decision Risk

Decision Risk can be categorized according to the structural cause identified by Decision Analysis.

### 5.1 DR-V — Validity Undecidable

DR-V occurs when Decision Analysis cannot determine whether the decision is structurally valid.

Typical conditions include:

- Missing boundary definition
- Undefined scope
- Incomplete decision artifacts

Governance implication:  
Governance cannot determine whether the decision is a legitimate object subject to rules or oversight.

---

### 5.2 DR-O — Outcome-Governance Disconnect

DR-O occurs when decision outcomes appear acceptable or successful, yet Decision Analysis identifies formation ambiguity.

Typical conditions include:

- Outcome correctness masking structural defects
- Compliance checks passing despite unclear decision legitimacy

Governance implication:  
Governance may develop a false sense of compliance due to successful outcomes.

---

### 5.3 DR-A — Authority Indeterminacy

DR-A occurs when Decision Analysis cannot identify the responsible authority behind a decision.

Typical conditions include:

- Implicit delegation
- Missing authorization records
- Ambiguous accountability chains

Governance implication:  
Audit and responsibility assignment become infeasible.

---

### 5.4 DR-C — Composite Decision Risk

DR-C occurs when multiple undecidability sources coexist.

Typical conditions include simultaneous ambiguity in scope, boundary, and authority.

Governance implication:  
The decision is operationally executable but structurally ungovernable.

---

## 6. Root Causes of Decision Risk

Decision Risk frequently emerges from structural characteristics of AI-assisted systems, including:

- implicit scope expansion through probabilistic inference
- authority delegation without explicit constraints
- absence of declared decision boundaries
- compression of deliberation and execution phases
- post-hoc rationalization replacing ex-ante justification

These causes are systemic rather than individual and do not depend on model accuracy or developer intent.

---

## 7. Possible Decision Risk Configurations

Decision Risk categories may appear in combination.

Examples include:

**DR-V + DR-O**  
Structurally illegitimate decisions repeatedly producing acceptable outcomes.

**DR-A + DR-V**  
Decisions whose authority and validity cannot both be established.

**DR-C**  
Multiple simultaneous structural ambiguities.

These configurations are diagnostic indicators of governance exposure rather than measures of severity.

---

## 8. Governance Implications of Decision Risk

When Decision Risk exists, governance mechanisms face several structural risks.

**Jurisdictional Risk**

Governance cannot determine whether it has authority to intervene.

**Analytical Misalignment Risk**

Decision Analysis outputs may appear valid but lack normative grounding.

**Audit Failure Risk**

Audit trails exist but cannot establish legitimate responsibility.

**Compliance Illusion Risk**

Outcome success creates the appearance of compliance despite illegitimate decision formation.

These risks persist even when system behavior appears correct.

---

## 9. Scope and Non-Claims

This paper does not propose mitigation techniques, enforcement systems, or governance architectures.

Such mechanisms presuppose that Decision Risk has already been identified through Decision Analysis.

The purpose of this work is limited to explaining why DA-identified undecidability must be interpreted as governance risk.

---

## 10. Conclusion

Decision Risk reframes governance risk as a structural condition arising during decision formation rather than as an outcome probability.

By interpreting Decision Analysis results through a governance lens, Decision Risk clarifies when governance mechanisms can meaningfully apply and when they cannot.

In AI-assisted systems, many failures attributed to operational behavior originate from decisions whose legitimacy was never established. Recognizing Decision Risk allows governance to identify these conditions before analytical evaluation or policy enforcement occurs.

Decision Analysis determines whether decisions are structurally decidable.  
Decision Risk explains why undecidable decisions matter for governance.

Together, they provide the foundation for a governance framework capable of operating within AI-assisted decision environments.

---

## 11. Related Work

---

## References
