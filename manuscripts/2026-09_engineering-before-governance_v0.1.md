# Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State
> From Step-Level Behavioral Constraints to Continuous Handoff Governance

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Version:** v0.1  
**Status:** Conceptual synthesis draft  

---

## Abstract

AI governance is commonly expressed through policies, authorization, human oversight, accountability, audit, risk evaluation, and compliance obligations. These mechanisms are necessary, but they do not operate on intention in the abstract. They require identifiable objects of judgment: a scope to which a rule applies, a boundary against which an action can be classified, a structured representation of intended behavior, evidence that can be inspected, authority that can be attributed, and workflow state that can be transferred across actors. This paper argues that effective AI governance therefore depends on a prior engineering condition: the state required for governance judgment must first be made explicit, bounded, inspectable, and traceable.

The central proposition is that engineering creates the state that governance evaluates. This does not mean governance requirements must chronologically follow engineering. Governance objectives, policies, and legal obligations may be defined before implementation. The claim is narrower and operational: before a specific governance judgment can constrain, evaluate, audit, or attribute an AI behavior, the relevant state must already exist in an engineering-visible form.

The paper develops this proposition at two granularities. At the step level, prior work on Viewpoint-Structured Specification, Scope, Boundary, and Behavior Rule Architecture shows how intent, governed regions, admissibility classifications, and normative rules must be externalized before an individual AI execution can be meaningfully governed. At the workflow level, prior work on continuation readiness shows that individually governed steps do not necessarily compose into a governed workflow unless the handoffs between human and AI actors are also engineered as governance objects. Role State, Work Junctions, Continuation Packages, Receiving Capacity, evidence transfer, and authority compatibility make continuation governable.

The resulting synthesis is the principle of Engineering Before Governance: governance effectiveness depends on prior engineering externalization of the state required to make governance judgments decidable, inspectable, and attributable. Governability is therefore partly an engineered property.

**Keywords:** AI Governance; Engineering-Visible State; Governability; Scope; Boundary; Behavior Rules; Human-in-the-Loop; Continuation Readiness; Enterprise AI Workflow; Auditability

---

## 1. Introduction

AI governance is often described in terms of the rules, obligations, controls, and accountability mechanisms placed around AI systems. A system should remain within authorized scope. A human should review high-impact decisions. A policy should prohibit certain actions. A model's outputs should be auditable. An organization should be able to explain, justify, and attribute consequential AI-assisted work.

These statements are governance requirements. They express what should be true. Yet none of them, by themselves, creates the operational state needed to evaluate whether the requirement has been satisfied. A rule saying that an AI system must remain within scope does not identify the scope. A requirement for human oversight does not guarantee that the human receives enough evidence, authority, or usable work state to perform oversight. A prohibition does not become reliably enforceable merely because it is written in policy language; its applicability, boundary, execution context, and evidence basis must be represented in a form that a governance mechanism can inspect.

This paper argues that a structural dependency is often left implicit in AI governance discussions:

> Engineering creates the state that governance evaluates.

The statement is not a claim that governance is secondary, optional, or created only after engineers finish building systems. Governance requirements may precede implementation. Law, organizational policy, risk appetite, and institutional accountability may define what must be governed before any technical realization exists. The argument is instead about operational governance judgment. Before a governance mechanism can constrain, evaluate, audit, or attribute a concrete AI behavior, the relevant state must already have been made explicit through engineering.

This distinction matters because governance mechanisms frequently assume the existence of objects that engineering has not yet created. A policy assumes an object of applicability. Oversight assumes an inspectable work state. Accountability assumes traceable action and authority. Audit assumes persistent evidence. Handoff governance assumes that the receiving actor can continue work without reconstructing it from incomplete context. When these objects remain implicit, governance is forced to infer the state on which its judgment depends. The result is not simply weak enforcement; it is weak governability.

The paper develops this argument at two levels.

First, at the level of an individual AI execution, governance depends on engineered representations of specification, scope, boundary, behavioral rules, authority, and evidence. The author's prior work on Viewpoint-Structured Specification (VSS), Scope as a Governance Primitive, Boundary as an Execution-Time Primitive, and Behavior Rule Architecture (BRA) can be understood as repeated attempts to externalize state that must exist before a single AI-assisted action can be governed.

Second, at the level of enterprise workflow, governed steps do not automatically compose into governed workflows. Work crosses human and machine actors, organizational roles, temporal discontinuities, accountability discontinuities, and role discontinuities. At these transitions, governance requires a different class of engineered state: Role State, Work Junction, Continuation Package, Receiving Capacity, authority compatibility, and evidence accessibility. The author's prior work on continuation readiness and Beyond HITL shows that handoffs themselves must become governance objects.

These are not two separate governance theories. They are the same dependency principle applied at different granularities:

```
implicit condition
    -> engineering externalization
    -> governance visibility
    -> governance judgment
```

At the step level, engineering makes behavior governable. At the workflow level, engineering makes continuation governable.

The paper proceeds as follows. Section 2 states the research question and the structural gap addressed by the paper. Section 3 explains why governance requires observable state. Section 4 synthesizes step-level governability. Section 5 explains why step governance does not automatically become workflow governance. Section 6 introduces handoffs as governance objects. Section 7 develops the principle of continuous handoff governance. Section 8 presents a unified model. Section 9 states the main propositions. Section 10 discusses implications. Section 11 identifies limitations. Section 12 concludes.

---

## 2. Research Question and Structural Gap

The primary research question is:

> What engineering conditions must exist before AI behavior and AI-assisted workflows can be meaningfully governed?

This question does not ask which policies should govern AI, which legal standards should apply, or which organizational accountability model should be adopted. Those questions remain important, but they operate at a different level. The question here concerns the preconditions under which such requirements become operationally evaluable.

Several secondary questions follow:

- How does the engineering prerequisite differ between an individual AI execution and a multi-actor enterprise workflow?
- Why are policy, oversight, accountability, and audit insufficient when the state on which those mechanisms depend remains implicit?
- What is lost when governance requirements are treated as if they automatically create their own evaluation surfaces?

The paper's gap is structural rather than polemical. It does not claim that existing AI governance scholarship ignores engineering, nor that governance frameworks are wrong to emphasize policy, risk, oversight, human intervention, accountability, or compliance. Instead, it argues that these governance mechanisms often rely on an engineering dependency that is not always made explicit.

A policy can require an AI system to remain within authorized scope. But if the relevant scope is not represented, what exactly is evaluated? A governance framework can require human oversight. But if the human receives insufficient evidence, unclear authority, or work state that cannot be acted upon, human presence does not produce meaningful oversight. A rule can prohibit an action. But if the action's applicability, context, or boundary condition remains implicit, compliance can be difficult to determine reliably.

The missing issue is not necessarily a lack of governance requirement. It is sometimes a lack of engineering-visible governance state.

This paper therefore distinguishes two layers:

**Governance requirement** is a normative expectation: the AI must remain within authorized scope; a human must approve high-impact decisions; a prohibited behavior must not occur; a workflow transfer must preserve accountability.

**Engineering realization** is the explicit structure that makes the requirement operationally decidable: a scope artifact, a boundary classification, a rule representation, an authority state, an evidence record, a continuation package, or a receiving-capacity condition.

The relation can be stated as:

```
Governance Requirement
    -> Engineering Realization
    -> Governable State
    -> Governance Judgment
```

A governance requirement does not automatically create the state necessary to evaluate that requirement. Engineering realization is the bridge between normative expectation and operational governability.

---

## 3. Governance Requires Observable State

Governance judgment is not performed against pure intention. It requires a state of affairs to which the judgment can be applied. This is true whether the mechanism is automated enforcement, human review, audit, risk scoring, compliance evaluation, or accountability attribution.

Consider five familiar governance mechanisms.

**Policy enforcement** requires an object of applicability. A policy that applies to "customer data," "high-risk decisions," "authorized repositories," or "regulated outputs" depends on a way to identify those objects. If the governed region is implicit, enforcement must infer policy applicability.

**Authorization** requires a representation of actor, authority, action, object, and context. If authority is only implied by role labels or conversational history, a system may perform a decision without a stable basis for determining whether the actor was authorized to make it.

**Human oversight** requires an inspectable work state. A human cannot meaningfully oversee a decision merely by being present. The human must receive enough evidence, assumptions, unresolved questions, authority boundaries, and work context to make a judgment rather than perform ceremonial approval.

**Accountability** requires attribution. It must be possible to identify who or what acted, under which authority, against which scope, using which evidence, and with which effect. If these states are not preserved, accountability becomes retrospective reconstruction.

**Audit** requires persistence and traceability. The state evaluated during or after execution must survive the execution event. If the relevant scope, boundary, rule, authority, or evidence state is transient, audit becomes dependent on logs that may not encode the governance object itself.

In each case, governance is not made effective merely by stating a requirement. The requirement must be connected to an observable representation of the state it governs.

This is the core dependency:

> Governance cannot reliably constrain, evaluate, audit, or attribute a condition that engineering has not first made explicit.

The statement should not be overread. Some governance judgment remains qualitative. Some forms of risk cannot be fully formalized. Some legal and ethical determinations require human interpretation. The argument is not that all governance can be made deterministic. It is that where a governance judgment depends on scope, authority, behavioral constraint, evidence, or transfer state, the absence of explicit engineering representation weakens the judgment.

This is especially consequential for AI-assisted work because AI systems frequently operate through semantic inference. They interpret prompts, infer scope, generalize from examples, select relevant context, invoke tools, and produce outputs that appear complete. If the state governing these actions remains implicit, the AI may reasonably infer it differently from the governance system, the human operator, or a later auditor. Governance then becomes dependent on reconstructing hidden or ambiguous state after the fact.

Engineering-visible state reduces this dependency. It does not remove all interpretation, but it gives governance mechanisms something identifiable to inspect.

---

## 4. Step-Level Governability

An individual AI execution can be governed only if the relevant execution state is explicit enough to support constraint, evaluation, and attribution. The author's prior work can be read as a series of mechanisms that make different parts of this state visible before or during execution.

### 4.1 VSS: Intent Must First Become Structured Specification

Viewpoint-Structured Specification addresses the problem that intent often exists as prose, conversation, prompt fragments, or transient assumptions. AI-assisted generation may appear to satisfy the user's intention while actually selecting, omitting, or expanding meaning in ways that are difficult to evaluate later.

VSS represents intent as persistent, addressable, multi-viewpoint specification before AI-assisted code generation. It emphasizes persistent addressability, explicit scope, and viewpoint membership. These properties allow later boundary formation, traceability, and evaluation.

The step-level sequence is:

```
Unstructured Intent
    -> Structured Specification
    -> Selectable Constraints
    -> Governable AI Execution
```

Governance cannot reliably determine whether generated work conforms to intent if the relevant intent remains distributed through prose and transient prompts. A human reviewer may read the output and judge whether it "seems right," but that judgment depends on reinterpreting the intent. A governance mechanism may compare output against requirements, but only if the requirements have been represented in a sufficiently stable and addressable form.

The contribution of VSS to this paper is not that VSS is the only way to structure intent. Its importance is that it illustrates the general dependency: engineering first creates a specification state against which governance can later evaluate generation.

### 4.2 Scope: Governance Needs a Reference Region

Scope should be understood as the explicit governed region. It is not the same as Boundary, authorization, policy, or enforcement. Scope establishes the reference region to which a governance judgment applies.

This distinction matters because many governance statements implicitly assume a region. A policy may apply within a project, repository, dataset, workflow stage, role responsibility, or decision context. An AI system may be allowed to read some artifacts but operate only on others. An execution may directly modify one region but produce downstream effects in another.

Prior Scope work distinguishes several viewpoints, including:

- **Visible Scope:** what an actor is exposed to by design.
- **Authorized Operable Scope:** what an actor is allowed to operate on.
- **Actual Effect Scope:** what execution ultimately affects.

These viewpoints show that what AI sees, what AI may operate on, and what its execution affects cannot be assumed to be identical. A model may see information it should not use for inference. It may operate within an authorized region while causing effects outside that region. It may produce an output whose consequences extend beyond the immediate object of modification.

The dependency can be stated as:

```
No explicit Scope
    -> no stable governed region
    -> weak decidability of governance judgment
```

Governance does not create the governed region. Engineering must first make that region explicit enough for governance to evaluate applicability, membership, comparison, change, and effect.

### 4.3 Boundary: Governance Requires Classification Relative to Scope

Boundary comes after Scope. A Boundary classifies an item, action, transition, or effect relative to a Scope. It can classify something as inside, outside, overlapping, undefined, allowed, denied, or requiring escalation depending on the local model. The important point is not the exact taxonomy, but the sequence:

```
Scope
    -> Boundary
    -> Classification
    -> Governance Consequence
```

Without engineered Scope and Boundary, governance must infer whether an action lies inside or outside the permitted region. That itself becomes probabilistic governance. The system may decide that a file is "related to authentication," that a data field is "customer data," or that a tool action is "within task scope," but if these classifications are not represented and preserved, later governance can only reconstruct the decision from surrounding context.

Boundary also prevents policy from doing too much conceptual work. A policy may say what happens if an action is outside scope, but the policy does not itself classify every action. Engineering must supply the classification surface.

### 4.4 BRA: Normative Intent Must Become Operational Rules

Behavior Rule Architecture separates natural-language normative intent from structured behavior rules. It uses MUST and MUST NOT semantics, rule metadata, rule libraries, and composable rulesets to create an engineering foundation for controllable, auditable, and governable AI behavior.

The relevant sequence is:

```
Normative Intent
    -> Structured Rule
    -> Rule Applicability
    -> Execution Constraint
    -> Governance Evaluation
```

Policy language alone is not equivalent to an engineered control surface. A natural-language policy may express what an AI system should or should not do, but governance evaluation still needs to know which rule applies, under what conditions, to which actor, object, action, and context, with what evidence of satisfaction or violation.

BRA illustrates the same pattern as VSS, Scope, and Boundary:

```
implicit normative meaning
    -> explicit engineering state
    -> governability
```

It is not necessary for every governance system to implement BRA as a specific architecture. The general lesson is that normative meaning must become operationally inspectable before it can serve as a reliable constraint or audit object.

### 4.5 Authority and Evidence

Specification, Scope, Boundary, and rules are insufficient without authority and evidence.

Authority identifies who or what may decide, approve, execute, modify, or transfer work under a given condition. It connects governance judgment to actors and responsibility. If authority is implicit, AI-assisted work may silently expand from support into decision-making, from suggestion into execution, or from bounded operation into unauthorized change.

Evidence provides the basis on which compliance, violation, risk, or accountability is assessed. Evidence may include the specification used, scope artifact, boundary classification, rule applicability, execution trace, human approval, tool invocation, effect analysis, or handoff package. Without evidence, governance judgment becomes assertion.

At the step level, governability therefore depends on a minimum set of engineering-visible state:

- specification: what the AI is expected to produce;
- scope: where the governance judgment applies;
- boundary: how an action is classified relative to scope;
- rule: what must or must not occur;
- authority: who or what may decide or execute;
- evidence: on what basis compliance can be assessed.

These states do not eliminate judgment. They make judgment possible.

---

## 5. Why Step Governance Is Not Workflow Governance

A single AI execution may be well governed. It may have structured specification, explicit scope, boundary classification, behavioral rules, authority, and evidence. Yet the execution may still exist inside a larger enterprise workflow:

```
Human Product Owner
    -> AI Business Analyst
    -> Human Architect
    -> AI Specification Agent
    -> Human Reviewer
    -> Business System
```

Each node in this chain may be individually constrained. The AI Business Analyst may remain within scope. The AI Specification Agent may apply rules correctly. The Human Architect may have formal authority. The Human Reviewer may receive an output. Still, governance can fail between nodes.

The reason is that workflow governance requires continuity, not merely locally valid behavior. Work must cross actors, roles, tools, evidence states, authority boundaries, and time gaps. What matters is not only whether Actor A was allowed to perform Action X. It is also whether the work produced by Actor A can be legitimately, sufficiently, and operationally continued by Actor B.

The governance question changes:

```
Step governance:
Can Actor A perform action X?

Workflow governance:
Can work produced by Actor A be legitimately and sufficiently continued by Actor B?
```

This second question requires state that may not exist at the individual-step level.

For example, an AI actor may produce correct code, remain within authorized scope, satisfy behavior rules, and preserve evidence. The next step may require a Product Owner to approve release. If the Product Owner receives only source code and technical logs, the transfer may fail as governance even if every step-level control reports success. The receiving actor does not have the capacity, context, or evidence format needed to continue the workflow.

The reverse can also occur. A human may delegate an underspecified task to an AI agent. The AI infers missing scope, produces a plausible result, and stays internally consistent. The downstream output may appear successful. Yet the workflow may have silently expanded authority at the handoff from human to AI because the transfer failed to externalize scope and intent.

These examples show the central extension:

> Governed steps do not automatically produce a governed workflow.

Enterprise AI governance therefore requires two surfaces:

- step governance: the governance of individual execution states;
- handoff governance: the governance of transition states between actors.

---

## 6. The Handoff as a Governance Object

A step can be represented as:

```
Input -> Actor -> Output
```

A workflow requires another object:

```
Actor A
    -> Handoff
    -> Actor B
```

The handoff is not merely a message, output, file, approval request, or notification. It is a governance-relevant transfer of work state across an actor boundary. It must carry enough information for the receiving actor to continue the work under appropriate authority and accountability conditions.

The author's prior work on continuation readiness provides the main workflow-level demonstration. It argues that Human-in-the-Loop is insufficient when it only places a human at a checkpoint. Governance requires continuability: the receiving human or machine actor must be able to act on transferred work without reconstructing it. Continuability depends on both what is transferred and who receives it.

Several engineered states become necessary.

**Role State** represents the capability, responsibility, authority, and contextual position of an actor. It identifies what the actor can legitimately continue. A human role, AI role, reviewer role, architect role, or business owner role may require different evidence and may hold different authority.

**Work Junction** represents the transfer point where work crosses actors or roles. It is the place where step output becomes input for another actor and where governance must evaluate whether the transition is valid.

**Continuation Package** represents the transferred work state needed for continuation. It may include output, evidence, assumptions, unresolved decisions, scope, authority basis, risk flags, provenance, and required next actions.

**Receiving Capacity** represents whether the receiving actor can actually act on the transfer. A transfer can be complete from the sender's perspective while unusable from the receiver's perspective. Receiving Capacity is therefore not simply another evidence field. It is a relational condition between package and recipient.

These states support the same dependency pattern:

```
Implicit handoff condition
    -> engineering externalization
    -> governance visibility
    -> continuation judgment
```

At the step level, explicit specification, scope, boundary, rules, authority, and evidence make behavior governable. At the workflow level, Role State, Work Junction, Continuation Package, Receiving Capacity, authority compatibility, and evidence transfer make continuation governable.

The handoff should therefore be treated as a governance object. It is a site where work can lose context, authority can silently expand, evidence can fail to transfer, accountability can become ambiguous, and human oversight can become ceremonial.

---

## 7. Continuous Handoff Governance

Enterprise AI workflows are not governed by a single engineering act at the beginning of the lifecycle. Governance judgment recurs at every execution and transition point. A more accurate conceptual model is:

```
Engineering-visible state
    -> Execution
    -> Governance judgment
    -> Handoff engineering
    -> Next execution
    -> Next governance judgment
```

Or, more compactly:

```
E1 -> G1 -> H1 -> E2 -> G2 -> H2 -> E3 -> G3
```

where:

- E is engineered governable state for a step;
- G is governance judgment;
- H is engineered handoff state.

The important proposition is that engineering precedes each governance judgment, not merely governance as a lifecycle phase. Governance requirements may exist throughout, but a concrete judgment requires concrete state at the point of judgment.

A workflow can therefore be understood as alternating execution and transfer surfaces:

```
[Step]
  Specification
  Scope
  Boundary
  Rules
  Authority
  Evidence
      |
      v
[Handoff]
  Role compatibility
  Transfer state
  Authority compatibility
  Evidence accessibility
  Continuation readiness
      |
      v
[Step]
  Specification
  Scope
  Boundary
  Rules
  Authority
  Evidence
```

Enterprise AI governance becomes continuous because the relevant engineering state must be reconstructed, updated, or transferred at every execution and handoff boundary. A governed workflow is therefore not merely the sum of governed actors. It is the composition of governed execution states and governed transition states.

This can be stated informally:

```
Governed Workflow
    = governed execution states
    + governed transition states
```

The formula is conceptual rather than mathematical. Its purpose is to prevent a common compression: treating a chain of locally constrained AI or human actions as if the chain itself were governed. The workflow is governed only if the transitions are governed as well.

---

## 8. Unified Model

The step-level and handoff-level arguments can be combined in a single model of engineering-visible governance state.

| Governance unit | Engineering-visible state | Governance question |
|---|---|---|
| Specification | VSS / explicit intent | What is the AI expected to produce? |
| Scope | Governed reference region | Where does the judgment apply? |
| Boundary | Admissibility classification | Is this action inside the relevant region? |
| Rule | Structured normative constraint | What must or must not occur? |
| Authority | Actor authorization and responsibility | Who may decide, approve, execute, or transfer? |
| Evidence | Inspectable basis | On what basis can compliance be assessed? |
| Role State | Actor capability / responsibility state | What can this actor legitimately continue? |
| Work Junction | Transfer point | What exactly is being transferred? |
| Continuation Package | Transferred work state | Is enough state available to continue? |
| Receiving Capacity | Receiver-side capability | Can the receiver actually act on the transfer? |

The table should not be read as a mandatory implementation stack. Different systems may realize these states through different artifacts, schemas, logs, workflow engines, policy engines, review protocols, or human procedures. The table identifies the kind of state governance needs, not a single architecture for representing it.

The synthesis is:

> Step-level engineering makes behavior governable. Handoff-level engineering makes continuity governable.

The same general principle appears in both cases. A governance condition remains weak when it is only implicit. It becomes governable when engineering externalizes it into a state that can be identified, inspected, constrained, transferred, and audited.

---

## 9. Proposition Set

The paper's argument can be expressed through five propositions.

### P1: Visibility Dependency

A governance judgment depends on an observable representation of the state to which the judgment applies.

This does not mean every relevant fact must be perfectly observable. It means that a judgment about scope, authority, behavioral constraint, evidence, or transfer cannot be reliably made if the relevant object of judgment remains entirely implicit.

### P2: Engineering Precondition

Where the required governance state is not naturally observable, engineering must externalize it before reliable governance evaluation is possible.

Externalization may occur through structured specification, scope artifacts, boundary states, rule representations, authority records, evidence packages, workflow state, or human-readable transfer formats.

### P3: Step Governability

At the individual execution level, specification, scope, boundaries, behavioral rules, authority, and evidence constitute engineering prerequisites for governing AI behavior.

These states allow governance to ask what the AI was expected to do, where it was allowed to operate, how its actions were classified, which rules applied, who held authority, and what evidence supports evaluation.

### P4: Transition Governability

At workflow transitions, role state, transfer state, authority compatibility, evidence accessibility, and receiving capacity constitute engineering prerequisites for governing continuation.

These states allow governance to ask whether transferred work can be legitimately and operationally continued by the receiving actor.

### P5: Workflow Composition

A workflow composed of individually governed AI steps is not necessarily governed unless the handoffs between those steps are also governed.

This is the paper's most important synthesis claim. Governance does not compose automatically across actor boundaries. Step-level correctness can coexist with workflow-level failure.

---

## 10. Implications

The principle of Engineering Before Governance has implications for governance system design, AI engineering practice, HITL design, agentic systems, and audit.

### 10.1 Governance System Design

Governance design should not begin only with the question:

> What policy should we enforce?

It should also ask:

> What state must exist for that policy to be evaluated?

This question changes the design task. A policy requiring authorized scope becomes a requirement to represent scope. A policy requiring human approval becomes a requirement to package evidence and authority in a form the human can use. A policy requiring accountability becomes a requirement to preserve attribution state.

### 10.2 AI Engineering

Governability becomes an engineering requirement. AI systems should not be evaluated only by whether they produce correct outputs, but also by whether they produce or preserve the state needed for governance judgment. Specification, scope, boundary, rule, authority, evidence, and transfer state become part of the system's engineering surface.

This does not require every system to become heavy or formal. The amount of externalization should be proportionate to risk, organizational need, and governance purpose. But where governance judgment matters, the relevant state should not remain hidden in prompts, logs, tacit assumptions, or model inference.

### 10.3 HITL

Human presence is not sufficient. A human in the loop may still lack evidence, authority, context, time, tooling, or domain standing. HITL governance should therefore evaluate continuation readiness, not only intervention placement.

The relevant question is not merely whether a human was asked to approve. It is whether the human received a continuation package suitable for their role state and receiving capacity.

### 10.4 Agentic Systems

Multi-agent systems require transition state, not merely per-agent permission. An agent may be authorized to perform its own task, but the transfer to another agent or human may still fail if scope, assumptions, evidence, unresolved decisions, or authority basis do not move with the work.

Agentic governance therefore needs a handoff model as much as it needs tool permissions and action constraints.

### 10.5 Audit

Auditability depends on engineered state persistence. A log of events may show that something happened, but governance audit asks what happened relative to specification, scope, boundary, rule, authority, evidence, and transfer conditions. Those objects must be preserved or reconstructable from preserved state.

The more governance depends on reconstructing implicit state after the fact, the weaker the audit.

---

## 11. Limitations

This paper makes a conceptual synthesis claim. It does not propose a new mandatory architecture, empirical performance result, or universal formal model.

Several limitations should be stated explicitly.

First, the paper does not claim that engineering replaces governance. Governance requirements, organizational accountability, legal duties, and ethical principles remain necessary. Engineering-visible state makes those requirements operationally evaluable; it does not define all normative content.

Second, the paper does not claim that policy is unimportant. Policy expresses governance requirements. The argument is that policy alone does not create the observable state required to evaluate its own satisfaction.

Third, the paper does not claim that all governance can be made deterministic. Many governance judgments remain qualitative, probabilistic, contested, or context-dependent. Engineering-visible state improves the object of judgment; it does not remove judgment.

Fourth, the paper does not claim that all AI state must be observable. Some internal model state may be inaccessible, irrelevant, proprietary, or too costly to externalize. The claim concerns the subset of state required for governance judgments involving scope, authority, behavioral constraints, evidence, or transfer.

Fifth, the paper does not claim that every workflow needs the same structures. A low-risk internal drafting task may require little more than simple evidence and role clarity. A regulated enterprise decision may require explicit scope artifacts, rulesets, authority records, continuation packages, and audit trails.

Sixth, the paper does not claim that VSS, Scope, Boundary, BRA, Role State, Work Junction, Continuation Package, or Receiving Capacity are newly invented here. They are treated as prior work. This paper's contribution is their synthesis into a common dependency principle.

Finally, the paper does not claim that engineering organizationally happens before governance. Governance objectives may precede implementation. The argument is about operational sequencing: before a specific governance judgment can be executed, the relevant state must already have been represented in engineering-visible form.

---

## 12. Conclusion

AI governance cannot operate only through rules placed above AI systems. Policies, oversight, accountability, audit, and compliance all require objects of judgment. They require scope, boundary, rules, authority, evidence, role state, and transfer state to exist in forms that can be identified, inspected, constrained, transferred, and preserved.

At the step level, engineering makes behavior governable. It externalizes intent, governed regions, classifications, rules, authority, and evidence before an individual AI execution can be evaluated.

At the workflow level, engineering makes handoffs governable. It externalizes role state, work junctions, continuation packages, receiving capacity, evidence transfer, and authority compatibility before multi-actor work can continue under governance.

The principle can therefore be stated simply:

> Engineering Before Governance is the principle that governance effectiveness depends on prior engineering externalization of the state required to make governance judgments decidable, inspectable, and attributable.

Engineering does not replace governance. It produces the explicit state through which governance becomes operational.

