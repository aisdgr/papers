# An Architectural Boundary for Decision Behavior Governance: Decision Constraint Layer, Governance Properties, and PDCA Alignment

**Author:** Spark Tsai
**Date:** January 2026
**Keywords:** AI Governance, Decision Constraint Layer (DCL), ISO/IEC 42001, AISCL, Evidence Sovereignty, PDCA.

---

## Abstract

In the era of foundation models deployed via commercial APIs, organizations no longer possess control over internal model reasoning, version semantics, or behavioral consistency. This loss of model sovereignty creates a structural governance problem: how can accountable AI governance be realized without model ownership? This paper introduces the **Decision Constraint Layer (DCL)** as an explicit architectural boundary for **Decision Behavior Governance**. Positioned between decision intent and action execution, the DCL serves as the non-bypassable location where organizational governance is enforced, evidenced, and attributed. We define the structural conditions required for governability—governance properties and carriers—and demonstrate how these elements align with the **PDCA cycle** mandated by **ISO/IEC 42001**, eenabling auditable AI governance as an architectural property, rather than a post-hoc procedural claim.

---

## 1. Introduction: From Conceptual Governance to Architectural Realization

This paper builds upon prior work defining Decision Behavior as the governance target and identifying governance nullity in foundation model environments.

As AI systems increasingly participate in organizational decision-making, governance discussions have shifted toward accountability and responsibility. However, acknowledging decision behavior as a governance target does not automatically resolve how governance is realized in practice.

In black-box model environments, governance mechanisms relying on model introspection or post-hoc monitoring cannot guarantee that governance conditions were enforced during decision formation. Without a clearly defined architectural intervention point, governance remains declarative rather than operative. This paper contends that AI governance requires a non-bypassable architectural boundary—the **Decision Constraint Layer (DCL)**—to transform governance from a procedural assertion into an engineering fact.

## 2. Architectural Requirements for Decision Behavior Governance

To govern decision behavior meaningfully, three requirements must be satisfied:

1. **Ex-ante Intervention:** Governance must intervene during decision formation, not merely observe outcomes.
2. **Structural Decoupling:** Governance must have a clearly defined boundary independent of the model engine.
3. **Deterministic Evidence:** Governance must be provable through traceable residues that establish Evidence Sovereignty.

## 3. The Decision Constraint Layer (DCL)

### 3.1 Architectural Positioning

The DCL is a structural boundary located between **Decision Intent** and **Action Execution**. It is the sole location authorized to mediate decision behavior through enforceable constraints.

- **Mediation:** Ensuring behavior adheres to organizational premises.
- **Attribution:** Establishing a causal link between institutional rules and AI outcomes.

### 3.2 Boundary by Exclusion (Non-Goals)

To maintain integrity, the DCL explicitly does **NOT** perform:

- Prompt optimization or reasoning enhancement.
- Model inference or training.
- Post-hoc logging without prior constraint mapping.

These exclusions ensure that the DCL remains a governance boundary rather than a reasoning enhancement mechanism.

## 4. Governance Properties: Conditions for Governability

Before a governance cycle (e.g., PDCA) can operate, governance elements must be governable. This paper defines five atomic properties:

1. **Identity:** Unique identification of each governance element.
2. **Versioning:** Supporting evolution and comparison across time.
3. **Applicability Boundary:** Determinable trigger conditions.
4. **Risk Attribution:** Mapping elements to identifiable impacts.
5. **Authority:** Explicit institutional source of ownership.

## 5. Governance Carriers: Operationalizing Properties

Governance properties are embodied through three carriers:

- **Constraint Carrier:** Limits the admissible decision space (e.g., AISCL).
- **Trigger Evidence Carrier:** Records how constraints were invoked during execution.
- **Effective Artifact Carrier:** Represents the finalized outcome with traceable governance metadata.

## 6. Carrier Utilization across the Decision Lifecycle

Governance is established only when carriers are actively utilized during decision formation:

- **Premise Establishment:** Deployment of Constraint Carriers.
- **Decision Formation:** Integration of Constraint and Trigger Evidence.
- **Post-decision Review:** Analysis of Trigger Evidence and Artifacts.

## 7. Alignment with ISO/IEC 42001 (PDCA)

The DCL architecture provides a direct technical correspondence to the ISO/IEC 42001 PDCA cycle:

- **Plan:** Defining Constraint Properties and AISCL rules.
- **Do:** Constraint-mediated decision formation within the DCL.
- **Check:** Aggregating Trigger Evidence to detect behavioral drift.
- **Act:** Issuing versioned governance updates based on evidence analysis.

## 8. Evidence Sovereignty and Institutional Learning

The DCL ensures that while model inference may remain probabilistic, the resulting governance evidence is deterministic by construction. Aggregated evidence allows organizations to detect when a model's interpretation of constraints fails, enabling the **Act** phase of PDCA to be a versioned governance action informed by data.

## 9. Conclusion

The Decision Constraint Layer provides an architectural foundation for accountable AI governance without requiring model ownership. By defining explicit boundaries and evidence-driven cycles, AI governance transcends static documentation and becomes a verifiable engineering reality.
