# dr-history.md
# Decision Risk — Version History

> Formal analytical constructs are primarily defined in Decision Analysis. Decision Risk focuses on the governance interpretation of analytical results, while lightweight indicators may be used for operational governance diagnostics.

---

## Versioning Scheme

- **v0.x** = preprint iteration (conceptual stabilization, terminology, scope boundary, and narrative coherence)
- Patch versions (e.g., **v0.2.1**) are used only for editorial fixes (typos, phrasing), not conceptual changes.

---

## v0.1 — Initial Framing (Concept Seed)

**Intent:** Establish Decision Risk as a governance phenomenon, not an engineering correctness metric.

**Key additions**
- Defined the core idea: decision-related risk can exist **independent of output correctness**.
- Introduced a reproducible-forensics framing at a high level.
- Began the taxonomy direction: Decision Vacancy as a distinct class of governance risk.

**Key exclusions / constraints**
- **MUST** not claim correlation between decision risk and correctness metrics.
- **MUST** avoid turning the work into defect analysis / QA metrics.

---

## v0.2 — Forensic Structure + Taxonomy (Method-leaning)

**Intent:** Strengthen internal logic and make the taxonomy operational (without scoring).

**Key additions**
- Formalized the elimination order:
  1) scope stability (Scope Drift exclusion)
  2) semantic cause exclusion (Inference Creep exclusion)
  3) decision-structure classification (Decision Risk)
- Stabilized the taxonomy:
  - **DR-V**: Decision Vacancy
  - **DR-O**: Over Decision Risk
  - **DR-I**: Indeterminate Decision Risk
- Clarified that **over outcome** is an observable trigger, not a classification.

**Key exclusions / constraints**
- **MUST** not quantify DR as a scalar “risk score”.
- **MUST** treat “indeterminacy” as a governance property, not analytic failure.
- **MUST** maintain “decision-centric” rather than “outcome-centric” language.

**Notable improvements prompted by review feedback**
- Stronger thesis statement: “Indeterminacy is a governance risk, not an analysis failure.”
- Clearer separation between:
  - outcome symptom (over outcome)
  - semantic cause (Inference Creep)
  - structural cause (Decision Risk)

---

## v0.3 — DAE Pivot (Effect-Based Stabilization)

**Intent:** Remove normative traps (e.g., “drift” judgment) by anchoring decision analysis on observable effects.

**Key additions**
- Introduced **Decision Authority Effect (DAE)** as the stable, observable construct:
  - authority is discussed through **effects**, not value judgments.
- Reframed “authority change” language:
  - Avoid “Authority Drift” (too normative / human-judgment-laden).
  - Prefer effect-based terminology (what the authority *enables in practice*).
- Explicitly positioned the **domain as governance**:
  - Software development pipelines are used as an *instrumented environment* for reproducible evidence.

**Key exclusions / constraints**
- **MUST** avoid terms that imply post-hoc human adjudication (e.g., “drift”, “improper”, “misaligned”) unless strictly defined as observable deltas.
- **MUST** keep DAE descriptive (observable), not prescriptive (normative).
- **MUST** not collapse DAE into “good/bad” judgments; DAE is a measurement substrate.

---

## v0.4 — Decision Analysis Alignment (Governance Interpretation Stabilization)

**Intent:**  
Align Decision Risk with the Decision Analysis framework and
stabilize its role as a governance interpretation layer rather than an analytical method.

**Key additions**

- Established the explicit relationship:

  Decision Analysis → Decision Risk

- Reframed Decision Risk as the **governance interpretation of DA-identified undecidability**.
- Introduced the structural definition:

  DR = ¬Decidable(Scope, Boundary, Authority)

- Clarified that Decision Risk does not independently evaluate decisions;
  it **inherits analytical results from Decision Analysis**.

**Conceptual stabilization**

Decision Risk now functions as:

- a governance-domain interpretation layer
- independent of outcome correctness
- dependent on analytical determination produced by Decision Analysis

**Key exclusions / constraints**

- **MUST NOT** redefine Decision Analysis constructs.
- **MUST NOT** introduce independent analytical classification.
- **MUST** treat DR taxonomy as governance interpretation of DA results.

**Taxonomy clarification**

The DR taxonomy is now interpreted as governance implications of
DA states and authority evidence:

- **DR-V** — validity undecidable (structural legitimacy unclear)
- **DR-O** — outcome-governance disconnect
- **DR-A** — authority indeterminacy
- **DR-C** — composite undecidability

**Impact on research stack**

This version stabilizes the research layering:

Anchor Architecture  
→ Decision Analysis  
→ Decision Risk  
→ Governance interpretation

Decision Risk is now explicitly positioned as the **governance layer**
built on top of analytical determination.

---

## v1.0 — Structural Risk Model Expansion

**Intent**

Expand Decision Risk from a governance interpretation concept into a structured analytical framework that can support engineering observability and governance diagnostics.

This version introduces the structural elements required to connect Decision Analysis results with operational governance mechanisms in AI-assisted software development.

**Key additions**

**1. Decision Observability Premise**

Introduced the concept of **Decision Observability** as the precondition for governance evaluation.

Observable decisions require evidence components including:

- Scope
- Rule (policy / constraint)
- Prompt
- Decision record
- Execution trace
- Outcome scope

This establishes the minimum evidence structure necessary for Decision Analysis and Decision Risk interpretation.

**2. Decision Risk Model**

Expanded Decision Risk into a structured model including:

- DR taxonomy
- structural risk sources
- threat classification
- governance implications

Decision Risk is explicitly defined as:

`Decision Risk = governance interpretation of a Decision Analysis result`

This ensures that DR remains dependent on DA rather than introducing an independent analytical method.

**3. Structural Threat Taxonomy**

Introduced three classes of structural threats:

- **Structural Threats (ST)** — rule and governance structure failures
- **Temporal Threats (TT)** — governance degradation over time
- **Referential Threats (RT)** — traceability and lineage failures

Threat types explain **why Decision Risk arises within AI-assisted development environments**.

**4. Risk Manifestation Levels**

Defined a staged manifestation model:

- L0 — Latent
- L1 — Observable
- L2 — Operational
- L3 — Systemic

This distinguishes **structural existence of risk** from **visible operational impact**.

**5. Governance Mapping**

Introduced governance interpretation layers:

- Operational fixes
- Process adjustments
- Structural governance interventions

The PDCA cycle is used to illustrate governance response to Decision Risk conditions.

**6. Engineering Case Demonstration**

Added a staged demonstration based on a JWT authentication refactor scenario.

The case illustrates how governance observability evolves:

`Prompt-only → Specification → Rule-constrained execution`


Decision states evolve accordingly:

```
DA-U → DA-V → DA-O
```

with corresponding Decision Risk transitions:

```
DR-U → DR-V → DR-O
```

**Conceptual stabilization**

This version establishes the full conceptual pipeline:

```
Anchor Architecture  
↓  
Decision Analysis  
↓  
Decision Observability  
↓  
Decision Risk  
↓  
Governance interpretation
```

Decision Risk is now positioned as the **governance diagnostic layer** derived from Decision Analysis
and supported by observable decision evidence.

---

**Key constraints**

- **MUST NOT** redefine Decision Analysis logic.
- **MUST** treat Decision Risk as governance interpretation.
- **MUST** maintain structural rather than probabilistic risk framing.

