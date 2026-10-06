# Engineering Before Governance: Why AI Governance Depends on Engineering-Visible State
> Governance Requirements, Engineering Design, and Engineering-Visible State in AI-Assisted Software Development

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  

---

## Abstract

This paper addresses AI governance at the software development stage, where humans and AI actors specify, modify, review, and transfer development work. Its central claim is that the "before" in Engineering Before Governance is an operational dependency: governance requirements may precede implementation, but a concrete governance judgment requires engineering-visible state before it can be made.

The paper synthesizes prior work on Viewpoint-driven Specification System, Scope, Boundary, Behavior Rule Architecture, Decision Analysis, Decision Risk, and continuation readiness. For development behavior governance, engineering-visible state includes persistent specification context, permitted scope, boundary classification, active behavior constraints, actual effect state, and evidence. For development workflow governance, it includes role state, work junctions, continuation packages, receiving capacity, evidence transfer, and rule-basis compatibility.

The resulting proposition is narrow but consequential: a software development workflow composed of individually governed AI-assisted actions is not necessarily governed unless the handoffs between those actions are also governed. Governability is therefore partly an engineered property, not merely a policy assertion.

**Keywords:** AI Governance; Software Development Governance; Engineering-Visible State; Governability; Behavior Rule Architecture; Decision Risk; Continuation Readiness; AI-Assisted Software Engineering

---

## 1. Introduction

This paper is limited to the software development stage of AI governance. Its object is not the runtime behavior of a deployed AI application, the operational monitoring of production inference, or model-level safety governance in general. The relevant setting is AI-assisted software development: humans and AI actors producing specifications, analyzing requirements, modifying code or artifacts, reviewing changes, invoking tools, deciding whether a change is within bounds, and transferring work across roles in a development workflow. In this paper, behavior means development behavior; execution means an AI-assisted development action or tool-mediated development operation; boundary means a development-stage classification of permitted visibility, operation, or modification; workflow means a software development workflow; and continuation means the transfer of development work between human and AI actors.

AI governance is often described in terms of the rules, obligations, controls, and accountability mechanisms placed around AI systems. A development action should remain within permitted scope. A human should review high-impact software changes. A policy should prohibit certain modifications. AI-assisted code generation should be auditable. An organization should be able to explain, justify, and attribute consequential AI-assisted development work.

These statements are governance requirements. They express what should be true. Yet none of them, by themselves, creates the operational state needed to evaluate whether the requirement has been satisfied. A rule saying that an AI system must remain within scope does not identify the scope. A requirement for human oversight does not guarantee that the human receives enough evidence, rule basis, or usable work state to perform oversight. A prohibition does not become reliably enforceable merely because it is written in policy language; its applicability, boundary, execution context, and evidence basis must be represented in a form that a governance mechanism can inspect.

This paper argues that a structural dependency is often left implicit in AI governance discussions:

> Engineering creates the state that governance evaluates.

The statement is not a claim that governance is secondary, optional, or created only after engineers finish building systems. Governance requirements may precede implementation. Law, organizational policy, risk appetite, and institutional accountability may define what must be governed before any technical realization exists. The argument is instead about operational governance judgment. Before a governance mechanism can constrain, evaluate, audit, or attribute a concrete AI-assisted development behavior, the relevant state must already have been made explicit through engineering.

This distinction matters because governance mechanisms frequently assume the existence of objects that engineering has not yet created. A policy assumes an object of applicability. Oversight assumes an inspectable work state. Accountability assumes traceable action and rule basis. Audit assumes persistent evidence. Handoff governance assumes that the receiving actor can continue work without reconstructing it from incomplete context. When these objects remain implicit, governance is forced to infer the state on which its judgment depends. The result is not simply weak enforcement; it is weak governability.

The paper develops this argument at two levels.

First, at the level of an individual AI-assisted development action, governance depends on engineered representations of specification, scope, boundary, behavioral rules, rule basis, and evidence. The author's prior work on Viewpoint-driven Specification System (VSS), Scope as a Governance Primitive, Boundary as an Execution-Time Primitive, Behavior Rule Architecture (BRA), Decision Analysis, and Decision Risk can be understood as repeated attempts to externalize state that must exist before a development action can be constrained, evaluated, or reviewed.

Second, at the level of enterprise development workflow, governed development actions do not automatically compose into governed workflows. Work crosses human and machine actors, organizational roles, temporal discontinuities, accountability discontinuities, and role discontinuities. At these transitions, governance requires a different class of engineered state: Role State, Work Junction, Continuation Package, Receiving Capacity, rule-basis compatibility, and evidence accessibility. The author's prior work on continuation readiness and Beyond HITL shows that handoffs themselves must become governance objects.

For development behavior, engineering makes intended behavior, allowed boundaries, context, actual effects, and risk evaluable. For development workflows, engineering makes continuation across actors governable.

The paper proceeds as follows. Section 2 states the research question and structural gap. Section 3 positions the argument against AI governance, oversight, audit, traceability, and related author work. Section 4 explains why governance requires observable state. Section 5 synthesizes development behavior governance. Section 6 provides a worked example. Sections 7 through 9 develop workflow and handoff governance. Section 10 presents a unified model. Sections 11 through 14 state propositions, implications, limitations, and conclusions.

---

## 2. Research Question and Structural Gap

The primary research question is:

> What engineering conditions must exist before AI-assisted software development behavior and development workflows can be meaningfully governed?

This question does not ask which policies should govern AI, which legal standards should apply, or which organizational accountability model should be adopted. Those questions remain important, but they operate at a different level. The question here concerns the preconditions under which such requirements become operationally evaluable.

Several secondary questions follow:

- How does the engineering prerequisite differ between an individual AI-assisted development action and a multi-actor enterprise development workflow?
- Why are policy, oversight, accountability, and audit insufficient when the state on which those mechanisms depend remains implicit?
- What is lost when governance requirements are treated as if they automatically create their own evaluation surfaces?

The paper's gap is structural rather than polemical. It does not claim that existing AI governance scholarship ignores engineering, nor that governance frameworks are wrong to emphasize policy, risk, oversight, human intervention, accountability, or compliance. Instead, it argues that these governance mechanisms often rely on an engineering dependency that is not always made explicit.

A policy can require an AI system to remain within permitted scope. But if the relevant scope is not represented, what exactly is evaluated? A governance framework can require human oversight. But if the human receives insufficient evidence, an unclear rule basis, or work state that cannot be acted upon, human presence does not produce meaningful oversight. A rule can prohibit an action. But if the action's applicability, context, or boundary condition remains implicit, compliance can be difficult to determine reliably.

The missing issue is not necessarily a lack of governance requirement. It is sometimes a lack of engineering-visible governance state.

This paper therefore distinguishes four connected layers:

**Governance requirement** is a normative expectation: the AI must remain within permitted scope; a human must approve high-impact decisions; a prohibited behavior must not occur; a workflow transfer must preserve accountability.

**Engineering design** determines how the relevant governance condition will be represented and preserved. It selects structures such as Scope, Boundary, Rule, Rule Basis, Evidence, Role State, Work Junction, Continuation Package, and Receiving Capacity. Here, Rule Basis denotes the inspectable policy, constraint, rule, and role-responsibility state needed for a governance judgment; it should not be confused with BRA's canonical term **Authority**, which denotes behavioral rules and constraints.

**Engineering-visible state** is a persistent or retrievable representation that makes a governance-relevant condition identifiable, bounded, inspectable, and attributable to the actor or process responsible for it. It need not formalize every fact or expose all internal model state. It must make the subset of state required for a particular governance judgment available in a usable form.

**Governance engineering** is the implementation and operation of mechanisms that transform engineering-visible state into enforceable, auditable, and attributable governance judgments and controls. It includes mechanisms for constraint, classification, approval, exception handling, audit, and feedback.

The relation can be stated as:

```
Governance Requirement
    -> Engineering Design
    -> Engineering-Visible State
    -> Governance Engineering
```

A governance requirement does not automatically create the state necessary to evaluate that requirement. It informs engineering design, but engineering must still externalize the relevant condition before governance engineering can act on it. Governance engineering may then produce judgments and feedback that refine the requirement, the design, or the represented state. The sequence is therefore a dependency chain with feedback, not a claim that governance policy begins only after engineering is complete.

---

## 3. Related Work and Positioning

This paper is not a general survey of AI governance. It positions a narrower claim: major governance frameworks and audit literatures require evidence, oversight, measurement, traceability, or accountability, but often leave implicit the engineering state on which those activities operate.

The NIST AI Risk Management Framework organizes AI risk work around Govern, Map, Measure, and Manage functions [1]. ISO/IEC 42001 defines requirements for establishing, implementing, maintaining, and improving an AI management system [2]. The EU AI Act requires high-risk AI systems to be designed for effective human oversight [3]. These frameworks define governance obligations at organizational, lifecycle, or system levels. The dependency this paper isolates is lower-level: Map, Measure, human oversight, audit, and management-system controls all require a state that can be mapped, measured, inspected, or transferred. In AI-assisted software development, that state includes specification context, permitted scope, boundary classifications, active behavior rules, actual effect state, and handoff evidence.

AI auditing literature makes the same dependency visible from another angle. Raji et al. define end-to-end internal algorithmic auditing as a process spanning scoping, mapping, artifact collection, testing, and reflection [4]. Mökander et al. analyze ethics-based auditing and its ability to operationalize governance through audit procedures and documented evidence [5]. These works establish the importance of audit practices, but audit still depends on the existence of auditable objects. This paper asks what engineering-visible state must exist before a development decision or handoff can be audited without reconstructing its governing context after the fact.

Human oversight and meaningful human control literature similarly motivate, but do not eliminate, the state dependency. The EU AI Act's human oversight requirement assumes that a human can understand, intervene, or stop relevant system behavior [3]. Green criticizes human oversight policies for legitimizing algorithmic systems without reliably addressing their underlying harms [6]. Work on meaningful human control translates control into designable properties across AI system development [7]. This paper extends that concern to AI-assisted software workflows: a human reviewer cannot provide meaningful oversight merely by being placed at a checkpoint. The reviewer must receive the specification basis, scope, rule basis, effect evidence, unresolved assumptions, and continuation package required for the role.

Software engineering research on provenance and traceability addresses adjacent state problems. Requirements traceability, code provenance, and recent work on AI-generated code provenance seek to preserve links among requirements, prompts, code, and development artifacts [8], [9]. This paper treats those links as necessary but not sufficient for governance. Traceability shows where an artifact came from; governance also needs to know which rule basis applied, what boundary was used, whether actual effects exceeded permitted scope, and whether the next actor can continue the work.

The paper also relates to the author's prior work. VSS externalizes intent as a persistent specification system [10]. Scope and Boundary separate the governed reference region from classification relative to that region [11], [12]. BRA treats **Authority** in the specific sense of behavioral rules and constraints: Policy MUST and Constraint MUST NOT [13]. Decision Analysis (DA) classifies observable development effects into structural states; Decision Risk (DR) interprets those states as governance risks [14], [15]. Continuation Readiness treats handoffs as governance objects [16]. Engineering Determinacy argues that established engineering information should exist in a determinate form rather than requiring repeated semantic reinterpretation [17]. This paper uses the same family of mechanisms, but its object differs: Engineering Determinacy concerns whether an established engineering state is determinate; Engineering Before Governance concerns whether the state required for a governance judgment is accessible to the actor or mechanism responsible for that judgment.

The synthesis is therefore not that prior work ignores governance or engineering. It is that governance literature often presupposes inspectable state, while engineering mechanisms often appear as separate local solutions. This paper names their shared dependency: governance requirements become operational only when engineering design produces engineering-visible state that governance engineering can use.

---

## 4. Governance Requires Observable State

Governance judgment is not performed against pure intention. It requires a state of affairs to which the judgment can be applied. This is true whether the mechanism is automated enforcement, human review, audit, risk scoring, compliance evaluation, or accountability attribution.

Consider five familiar governance mechanisms.

**Policy enforcement** requires an object of applicability. A policy that applies to "customer data," "high-risk decisions," "permitted repositories," or "regulated outputs" depends on a way to identify those objects. If the governed region is implicit, enforcement must infer policy applicability.

**Role-action basis** requires a representation of actor, rule basis, action, object, and context. If the rule basis is only implied by role labels or conversational history, a system may perform a decision without a stable basis for determining whether the action was permitted.

**Human oversight** requires an inspectable work state. A human cannot meaningfully oversee a decision merely by being present. The human must receive enough evidence, assumptions, unresolved questions, rule-basis boundaries, and work context to make a judgment rather than perform ceremonial approval.

**Accountability** requires attribution. It must be possible to identify who or what acted, under which rule basis, against which scope, using which evidence, and with which effect. If these states are not preserved, accountability becomes retrospective reconstruction.

**Audit** requires persistence and traceability. The state evaluated during or after execution must survive the execution event. If the relevant scope, boundary, rule basis, or evidence state is transient, audit becomes dependent on logs that may not encode the governance object itself.

In each case, governance is not made effective merely by stating a requirement. The requirement must be connected to an observable representation of the state it governs.

This is the core dependency:

> Governance cannot reliably constrain, evaluate, audit, or attribute a condition that engineering has not first made explicit.

The statement should not be overread. Some governance judgment remains qualitative. Some forms of risk cannot be fully formalized. Some legal and ethical determinations require human interpretation. The argument is not that all governance can be made deterministic. It is that where a governance judgment depends on scope, rule basis, behavioral constraint, evidence, or transfer state, the absence of explicit engineering representation weakens the judgment.

This is especially consequential for AI-assisted work because AI systems frequently operate through semantic inference. They interpret prompts, infer scope, generalize from examples, select relevant context, invoke tools, and produce outputs that appear complete. If the state governing these actions remains implicit, the AI may reasonably infer it differently from the governance system, the human operator, or a later auditor. Governance then becomes dependent on reconstructing hidden or ambiguous state after the fact.

Engineering-visible state reduces this dependency. It does not remove all interpretation, but it gives governance mechanisms something identifiable to inspect.

This use of *visible* is functional rather than absolute. A state is engineering-visible when the actor or mechanism responsible for governance can retrieve and interpret it for the relevant judgment. Visibility may therefore be role-dependent: evidence visible to an auditor may differ from evidence available to an executing agent, and a continuation package usable by one role may be insufficient for another. The concept concerns governance accessibility, not universal disclosure.

---

## 5. Development Behavior Governance

An individual AI-assisted development action becomes a governance concern before it becomes an engineering object. Governance first states a requirement: an output should conform to approved intent, an action should remain within scope, a prohibited behavior should not occur, only a permitted actor should decide or execute, and evidence should support later review. The engineering question follows: what design will make the condition addressed by that requirement visible enough for governance to act on it?

This section therefore does not organize development behavior governance as a catalogue of VSS, Scope, Boundary, BRA, rule basis, Decision Analysis, and Decision Risk. It begins with governance problems and traces each one through the dependency established in Section 2:

```text
Governance Problem or Requirement
    -> Engineering Design
    -> Engineering-Visible State
    -> Governance Engineering
```

The final stage does not imply that engineering automatically resolves a normative question. It means that governance can continue: a mechanism or responsible actor can constrain execution, make a judgment, request approval, escalate uncertainty, preserve a decision, or audit an outcome using explicit state rather than reconstructing an implicit condition.

Development behavior governance can be divided into pre-execution and post-execution requirements.

Before execution, governance requires at least three conditions. First, behavior constraints must be available: the AI actor must know which constraints, rules, and policies are active. Behavior Rule Architecture is one engineering design for this requirement. Second, execution boundaries must be available: the AI actor and governance mechanism must know what is visible, what is allowed, and what may be modified. Scope and Boundary are engineering designs for this requirement. Third, development context must be available in a form that exceeds transient prompt memory. Viewpoint-driven Specification System is one engineering design for preserving long-lived specification state across stakeholder, system, implementation, and governance viewpoints.

After execution, governance requires evidence of whether execution crossed a permitted boundary, expanded beyond permitted scope, ignored applicable constraints, or created risk. Decision Analysis and Decision Risk play different roles in this chain. Decision Analysis produces engineering-visible state by classifying actual changes and effects against visible, artifact, and outcome scopes. Decision Risk belongs to governance engineering: it interprets those analytical states as governance risks and responses.

### 5.1 Context Governance Requires a Stable Object of Intent

**Governance problem and requirement.** An AI-produced artifact must conform to the intent under which work was approved. The governance problem is that intent often remains distributed across prose, conversation, prompt fragments, and tacit assumptions. An output may appear plausible while omitting one viewpoint, expanding another, or satisfying an interpretation that was never approved. In that condition, a reviewer can judge only whether the result seems reasonable, not whether it conforms to a stable object of intent.

**Engineering design.** The design task is to represent relevant intent as persistent, addressable, and selectable specification. Viewpoint-driven Specification System (VSS) is one realization of this design. It organizes intent through persistent addressability, explicit scope, and viewpoint membership so that requirements do not disappear into transient prompt context. VSS is used here as prior engineering evidence, not as a mandatory governance architecture.

**Engineering-visible state.** The design produces a specification state that identifies which intent elements were active, how they were grouped, which viewpoints they represented, and which constraints were selected for the execution. This state functions as development context that can outlive model memory and prompt context. The governance-relevant object is no longer an assumed meaning reconstructed from the final output; it is an inspectable specification against which the output can be considered.

**How governance continues.** Governance engineering can now compare generated work with selected intent, identify omitted or expanded requirements, route unresolved differences to review, and preserve the basis of the conformance judgment. The specification does not decide whether the output is acceptable by itself. It gives automated controls, human reviewers, and later auditors a stable object on which that decision can be made.

### 5.2 Scope Governance Requires an Explicit Governed Region

**Governance problem and requirement.** An AI actor must remain within the region in which it is permitted to operate, and governance must determine where a policy, permission, or accountability obligation applies. The problem is that statements such as "within the project," "only customer records," or "limited to this task" assume a governed region without necessarily representing it. If the region remains implicit, both the AI actor and the governance mechanism must infer its extent.

**Engineering design.** The design task is to externalize Scope as the reference region for governance. Prior Scope work distinguishes Visible Scope, Permitted Operable Scope, and Actual Effect Scope because what an actor can see, what it may operate on, and what its actions ultimately affect are not necessarily identical. The design must represent the viewpoints relevant to the governance requirement and preserve their differences rather than compressing them into a single informal notion of access.

**Engineering-visible state.** The resulting state identifies the objects, resources, decisions, workflow stages, or effects included in the governed region. It identifies allowed boundaries, visible range, operable range, and modifiable range. It can also reveal divergence among exposure, permission, and effect. Governance can therefore inspect not only the nominal task area but also whether execution consumed information or produced consequences outside the permitted operable region.

**How governance continues.** Governance engineering can determine policy applicability, compare actual operation and effect with permitted scope, require approval for scope expansion, or escalate an undefined region. Scope does not enforce a policy by itself. It provides the reference region without which compliance, exception, and effect judgments have no stable object.

### 5.3 Boundary Enforcement Requires an Explicit Classification

**Governance problem and requirement.** Once a governed region exists, an action, item, transition, or effect must be classified relative to it before an allow, deny, or escalation consequence can be applied. The governance problem is not simply that a boundary rule may be absent. It is that the classification connecting a concrete action to the governed region may remain implicit, transient, or unavailable for later review.

**Engineering design.** The design task is to create a Boundary operation relative to an established Scope. Depending on the context, the classification may distinguish inside, outside, overlapping, undefined, allowed, denied, or requiring escalation. Scope and Boundary remain separate: Scope establishes the reference region, while Boundary determines how a particular governance object relates to that region.

**Engineering-visible state.** The design produces a preserved classification with enough context to identify the action or object classified, the Scope used as the reference, the classification result, and any uncertainty or exception condition. This state prevents an execution-time inference such as "this file appears related" or "this action seems within task scope" from disappearing after the action occurs.

**How governance continues.** Governance engineering can translate the classification into a consequence: allow the action, deny it, require approval, record an exception, or trigger further analysis. It can also audit whether the correct Scope and classification logic were used. Boundary does not supply the normative consequence on its own; it supplies the visible classification required to apply that consequence consistently.

### 5.4 Behavioral Constraint Governance Requires Operational Rule State

**Governance problem and requirement.** Governance may require that an AI actor perform an action, refrain from an action, or behave differently under specified conditions. Natural-language policy can state the obligation, but it may leave rule applicability, priority, actor, object, context, and evidence expectations unresolved at execution time. A policy that cannot be connected to a concrete execution remains difficult to enforce or evaluate.

**Engineering design.** The design task is to translate relevant normative intent into structured behavior rules. Behavior Rule Architecture (BRA) is one prior realization using MUST and MUST NOT semantics, rule metadata, reusable rule libraries, and composable rulesets. Its relevance here is not that every system should adopt BRA, but that an execution needs an engineering representation connecting a normative requirement to operational conditions.

**Engineering-visible state.** The design makes the applicable constraints, policies, rules, conditions, target actor or behavior, priority or composition context, and evidence expected for satisfaction or violation inspectable. Governance can identify which rule was active rather than inferring after execution which policy statement might have applied.

**How governance continues.** Governance engineering can constrain execution, detect a violation, request an exception, record satisfaction, or provide a rule-and-evidence basis for human review and audit. Structured rule state does not settle every legal or ethical interpretation. It allows the applicable normative requirement to participate in an operational governance process.

### 5.5 Post-Execution Governance Requires Actual Effect Evidence

**Governance problem and requirement.** After an AI-assisted development action occurs, governance must determine whether the action stayed within permitted boundaries, modified only permitted objects, used applicable constraints and policies, and created acceptable decision risk. The governance problem is that a successful output does not by itself show whether the execution remained within the permitted development region. A change may compile, pass tests, or appear useful while having crossed a boundary, ignored a constraint, or created downstream risk.

**Engineering design.** The design task is to preserve actual execution and effect state in a form suitable for Decision Analysis. This includes the actual modified scope, actual effect scope, tool invocations, selected constraints and policies, boundary classifications, exceptions, approvals, unresolved assumptions, and downstream effect indicators.

**Engineering-visible state.** The design produces post-execution evidence: what was actually read, changed, generated, deleted, transferred, approved, or left unresolved; which constraints and policies were active; and how the action related to the permitted boundary. This state distinguishes nominal compliance from evidence-supported compliance.

**How governance continues.** Governance engineering can use the Decision Analysis state as input for Decision Risk classification, identify boundary violation, request remediation, preserve an audit trail, or escalate to a responsible human. DA answers what structural state the development action produced; DR answers what governance significance that state has. The judgment is no longer limited to whether the artifact looks acceptable. It can consider whether the development behavior that produced the artifact remained governable.

### 5.6 Attribution and Accountability Require Evidence

**Governance problem and requirement.** Only an appropriately permitted actor should decide, approve, execute, modify, or transfer work, and consequential actions should remain attributable. Even when specification, Scope, Boundary, and rules are explicit, governance fails if it cannot determine who acted under what rule basis or on what evidence a judgment was made. AI-assisted work can otherwise shift silently from support to decision-making, from recommendation to execution, or from bounded operation to unauthorized change.

**Engineering design.** The design task is to bind actor identity, role responsibility, rule basis, permitted action, governed object, decision context, and validity conditions to the execution. It must also capture the evidence required by the governance purpose, which may include active specification, Scope, Boundary classification, rule applicability, execution trace, approval, tool invocation, and effect analysis.

**Engineering-visible state.** The resulting rule-basis state shows who or what was permitted to act and under which conditions. The resulting evidence state preserves what was known, applied, decided, and produced. Together they connect an execution to responsibility and provide a basis for evaluating compliance, violation, risk, or exception without relying entirely on retrospective reconstruction.

**How governance continues.** Governance engineering can allow or block execution, route a decision to an accountable approver, attribute an outcome, test compliance, investigate an exception, and conduct an audit. Rule basis and evidence do not guarantee that the judgment will be correct. They make the judgment attributable and reviewable.

The development behavior argument can therefore be summarized by governance dependency rather than framework capability:

| Governance problem or requirement                 | Engineering design                                    | Engineering-visible state                      | Governance can continue through                    |
| ------------------------------------------------- | ----------------------------------------------------- | ---------------------------------------------- | -------------------------------------------------- |
| Conformance to approved intent                  | Persistent, addressable specification design          | Active specification and viewpoint state       | Comparison, review, variance detection, audit      |
| Operation within a permitted region              | Scope design across visibility, operation, and effect | Governed reference region and scope divergence | Applicability judgment, scope control, escalation  |
| Consistent treatment of actions relative to scope | Boundary classification design                        | Preserved classification and uncertainty state | Allow, deny, exception, approval, audit            |
| Compliance with behavioral obligations            | Structured rule design                                | Applicable constraint, policy, and rule state  | Constraint, violation detection, exception, review |
| Post-execution boundary and effect analysis        | Decision Analysis design                              | Actual modified scope, effect, and rule state  | DA classification, evidence preservation, audit input |
| Post-execution governance interpretation           | Decision Risk design                                  | DA state, risk category, threat state, and severity basis | Risk classification, remediation, escalation |
| Attributable and accountable action              | Rule-basis binding and evidence capture               | Actor, role responsibility, rule basis, decision, and evidence state | Allow/block, attribution, investigation, audit |

These states do not eliminate governance judgment, and the engineering designs do not replace governance requirements. They create the explicit objects through which development behavior governance can proceed.

---

## 7. Why Development Action Governance Is Not Workflow Governance

A single AI-assisted development action may be well governed. It may have structured specification, explicit scope, boundary classification, behavioral rules, rule basis, and evidence. Yet the action may still exist inside a larger enterprise development workflow:

```
Human Product Owner
    -> AI Business Analyst
    -> Human Architect
    -> AI Specification Agent
    -> Human Reviewer
    -> Business System
```

Each node in this chain may be individually constrained. The AI Business Analyst may remain within scope. The AI Specification Agent may apply rules correctly. The Human Architect may have formal responsibility. The Human Reviewer may receive an output. Still, governance can fail between nodes.

The reason is that workflow governance requires continuity, not merely locally valid behavior. Work must cross actors, roles, tools, evidence states, rule-basis boundaries, and time gaps. What matters is not only whether Actor A was allowed to perform Action X. It is also whether the work produced by Actor A can be legitimately, sufficiently, and operationally continued by Actor B.

The governance question changes:

```
Development action governance:
Can Actor A perform action X?

Workflow governance:
Can work produced by Actor A be legitimately and sufficiently continued by Actor B?
```

This second question requires state that may not exist at the individual-action level.

For example, an AI actor may produce correct code, remain within permitted scope, satisfy behavior rules, and preserve evidence. The next development action may require a Product Owner to approve release. If the Product Owner receives only source code and technical logs, the transfer may fail as governance even if every action-level control reports success. The receiving actor does not have the capacity, context, or evidence format needed to continue the workflow.

The reverse can also occur. A human may delegate an underspecified task to an AI agent. The AI infers missing scope, produces a plausible result, and stays internally consistent. The downstream output may appear successful. Yet the workflow may have silently expanded responsibility at the handoff from human to AI because the transfer failed to externalize scope and intent.

These examples show the central extension:

> Governed development actions do not automatically produce a governed development workflow.

Enterprise AI-assisted development governance therefore requires two surfaces:

- development action governance: the governance of individual development execution states;
- handoff governance: the governance of transition states between actors.

---

## 8. The Handoff as a Governance Object

A development action can be represented as:

```
Input -> Actor -> Output
```

A development workflow requires another object:

```
Actor A
    -> Handoff
    -> Actor B
```

The handoff is not merely a message, output, file, approval request, or notification. It is a governance-relevant transfer of work state across an actor boundary. It must carry enough information for the receiving actor to continue the work under appropriate rule basis and accountability conditions.

The author's prior work on continuation readiness provides the main workflow-level demonstration. It argues that Human-in-the-Loop is insufficient when it only places a human at a checkpoint. Governance requires continuability: the receiving human or machine actor must be able to act on transferred work without reconstructing it. Continuability depends on both what is transferred and who receives it.

Several engineered states become necessary.

**Role State** represents the capability, responsibility, rule-basis position, and contextual position of an actor. It identifies what the actor can legitimately continue. A human role, AI role, reviewer role, architect role, or business owner role may require different evidence and may hold different responsibilities.

**Work Junction** represents the transfer point where work crosses actors or roles. It is the place where one development action's output becomes input for another actor and where governance must evaluate whether the transition is valid.

**Continuation Package** represents the transferred work state needed for continuation. It may include output, evidence, assumptions, unresolved decisions, scope, rule basis, risk flags, provenance, and required next actions.

**Receiving Capacity** represents whether the receiving actor can actually act on the transfer. A transfer can be complete from the sender's perspective while unusable from the receiver's perspective. Receiving Capacity is therefore not simply another evidence field. It is a relational condition between package and recipient.

These states support the same dependency pattern:

```
Implicit handoff condition
    -> engineering externalization
    -> governance visibility
    -> continuation judgment
```

At the development action level, explicit specification, scope, boundary, rules, rule basis, actual effect, and evidence make behavior governable. At the workflow level, Role State, Work Junction, Continuation Package, Receiving Capacity, rule-basis compatibility, and evidence transfer make continuation governable.

The handoff should therefore be treated as a governance object. It is a site where work can lose context, rule basis can silently expand, evidence can fail to transfer, accountability can become ambiguous, and human oversight can become ceremonial.

---

## 9. Continuous Workflow Governance

Enterprise AI-assisted development workflows are not governed by a single engineering act at the beginning of the lifecycle. Governance judgment recurs at development execution points and at the transitions between them. Here, *continuous* does not mean uninterrupted real-time monitoring. It means that governability must be re-established wherever development work is executed or transferred.

A development action and its outgoing handoff each require their own engineering-visible state and governance judgment:

```
Action State A1
    -> Action Judgment Ga1
    -> Handoff State H1
    -> Handoff Judgment Gh1
    -> Action State A2
    -> Action Judgment Ga2
```

where:

- **A** is engineering-visible state for a development action;
- **Ga** is a governance judgment about that action;
- **H** is engineering-visible state for a handoff;
- **Gh** is a governance judgment about that handoff.

The distinction matters because a valid action judgment does not imply a valid handoff judgment. A sender may have acted within scope while still transferring insufficient evidence, incompatible rule basis, or unusable work state to the receiver. Conversely, a well-formed handoff cannot cure an action that violated its own scope or rules.

The important proposition is that engineering-visible state precedes each operational governance judgment, not that governance requirements follow engineering as an institutional phase. Governance requirements may exist throughout, but a concrete action or handoff judgment requires corresponding state at the point of judgment.

A development workflow can therefore be understood as alternating execution and transfer surfaces:

```
[Development Action]
  Specification
  Scope
  Boundary
  Rules
  Rule Basis
  Evidence
      |
      v
[Handoff]
  Role compatibility
  Transfer state
  Rule-basis compatibility
  Evidence accessibility
  Continuation readiness
      |
      v
[Development Action]
  Specification
  Scope
  Boundary
  Rules
  Rule Basis
  Evidence
```

Enterprise AI-assisted development governance becomes continuous because the relevant engineering-visible state must be constructed, updated, or transferred at every execution and handoff boundary, and each surface must support its own governance judgment. A governed development workflow is therefore not merely the sum of governed actors. It is the composition of governed execution states and governed transition states.

This can be stated informally:

```
Governed Workflow
    = governed execution states
    + governed transition states
```

For this paper, the formula should be read as governed software development workflow, not as a general model of deployed runtime operation.

The formula is conceptual rather than mathematical. Its purpose is to prevent a common compression: treating a chain of locally constrained AI or human actions as if the chain itself were governed. The workflow is governed only if the transitions are governed as well.

---

## 10. Unified Model

The development-action and handoff arguments can be combined in a single model of engineering-visible governance state.

| Governance area | Governance problem or requirement | Engineering design | Engineering-visible state | Governance judgment |
| --- | --- | --- | --- | --- |
| Development behavior before execution | Behavior must follow applicable constraints and policies | Behavior Rule Architecture or equivalent rule design | Active constraints, policies, rules, targets, conditions, and priority | Is the intended action allowed, required, prohibited, or exception-bound? |
| Development behavior before execution | Execution must remain within permitted boundaries | Scope and Boundary design | Allowed boundary, visible range, operable range, modifiable range, and classification state | Is the action inside, outside, overlapping, undefined, or escalation-required? |
| Development behavior before execution | Context must be stable enough for intent conformance | Viewpoint-driven Specification System or equivalent specification design | Long-lived specification state, viewpoint membership, selected intent, and active assumptions | Does the action conform to approved development intent? |
| Development behavior after execution | Execution must be evaluated against actual change and actual effect | Decision Analysis design | Actual modified scope, actual effect scope, applied constraints and policies, exceptions, and evidence | What DA state did the action produce? |
| Development behavior after execution | Analytical state must be interpreted as governance risk | Decision Risk design | DA state, risk category, threat state, manifestation level, and severity basis | What governance risk or response follows from the DA state? |
| Development behavior across execution | Action must remain attributable and accountable | Rule-basis and evidence design | Actor, role responsibility, rule basis, decision record, and evidence state | Can the action be attributed, reviewed, investigated, or audited? |
| Development workflow | Work must be transferable across humans and AI actors | Continuation readiness design | Role State, Work Junction, Continuation Package, Receiving Capacity, rule-basis compatibility, and evidence accessibility | Can the receiving actor legitimately and sufficiently continue the work? |

The table should not be read as a mandatory implementation stack. Different systems may realize these states through different artifacts, schemas, logs, workflow engines, policy engines, review protocols, or human procedures. The table identifies the kind of state governance needs, not a single architecture for representing it.

The synthesis is:

> Development-action engineering makes behavior governable. Handoff-level engineering makes continuity governable.

The same general principle appears in both cases. A governance condition remains weak when it is only implicit. It becomes governable when engineering externalizes it into a state that can be identified, inspected, constrained, transferred, and audited.

---

## 11. Proposition Set

The paper's argument can be expressed through five propositions.

### P1: Visibility Dependency

A governance judgment depends on an observable representation of the state to which the judgment applies.

This does not mean every relevant fact must be perfectly observable. It means that a judgment about scope, rule basis, behavioral constraint, evidence, or transfer cannot be reliably made if the relevant object of judgment remains entirely implicit or inaccessible to the responsible governance mechanism.

### P2: Operationalization Dependency

Governance requirements become operational through a dependency chain from governance requirement to engineering design, engineering-visible state, and governance engineering.

If any link is absent, the requirement may remain normatively valid while being weakly enforceable, auditable, or attributable. The chain does not prescribe one implementation architecture; it identifies the dependency between normative expectation and operational judgment.

### P3: Development Behavior Governance

At the individual development-action level, specification, scope, boundaries, behavioral rules, rule basis, actual effect, and evidence constitute engineering prerequisites for governing AI-assisted development behavior.

Without these states, governance must infer what the AI was expected to do, where it was allowed to operate, how its actions should be classified, which rules applied, which role responsibility and rule basis applied, what was actually modified or affected, or what evidence supports evaluation. Development behavior governance therefore weakens as these conditions remain implicit.

### P4: Development Workflow Governance

At development workflow transitions, role state, transfer state, rule-basis compatibility, evidence accessibility, and receiving capacity constitute engineering prerequisites for governing continuation.

Without these states, governance cannot reliably determine whether transferred work can be legitimately and operationally continued by the receiving actor. A transfer may appear complete while leaving continuation rule basis, evidence, or capacity unresolved.

### P5: Development Workflow Composition

A software development workflow composed of individually governed AI-assisted actions is not necessarily governed unless the handoffs between those actions are also governed.

This is the paper's most important synthesis claim. Governance does not compose automatically across actor boundaries. Action-level correctness can coexist with workflow-level failure.

---

## 12. Implications

The dependency from governance requirement through engineering-visible state to governance engineering has implications for software development governance system design, AI-assisted engineering practice, HITL design, agentic development systems, and audit.

### 12.1 Governance System Design

Governance design should not begin only with the question:

> What policy should we enforce?

It should also ask:

> What state must exist for that policy to be evaluated?

It should then ask:

> What governance mechanism will use that state, and what judgment or control must it produce?

These questions connect governance requirement, engineering design, engineering-visible state, and governance engineering. A policy requiring permitted scope becomes a requirement to represent scope and a mechanism for classifying actions against it. A policy requiring human approval becomes a requirement to package evidence and rule basis in a usable form and a mechanism for recording the resulting decision. A policy requiring accountability becomes a requirement to preserve attribution state and an audit mechanism capable of interpreting it.

### 12.2 AI Engineering

Governability becomes a software engineering requirement. AI-assisted development systems should not be evaluated only by whether they produce correct outputs, but also by whether they produce or preserve the state needed for governance judgment. Specification, scope, boundary, rule, rule basis, actual effect, evidence, and transfer state become part of the development system's engineering surface.

This does not require every system to become heavy or formal. The amount of externalization should be proportionate to risk, organizational need, and governance purpose. But where governance judgment matters, the relevant state should not remain hidden in prompts, logs, tacit assumptions, or model inference.

### 12.3 HITL

Human presence is not sufficient. A human in the loop may still lack evidence, rule basis, context, time, tooling, or domain standing. HITL governance should therefore evaluate continuation readiness, not only intervention placement.

The relevant question is not merely whether a human was asked to approve. It is whether the human received a continuation package suitable for their role state and receiving capacity.

### 12.4 Agentic Systems

Multi-agent systems require transition state, not merely per-agent permission. An agent may be permitted to perform its own task, but the transfer to another agent or human may still fail if scope, assumptions, evidence, unresolved decisions, or rule basis do not move with the work.

Agentic development governance therefore needs a handoff model as much as it needs tool permissions and action constraints.

### 12.5 Audit

Auditability depends on engineered state persistence. A log of events may show that something happened, but development governance audit asks what happened relative to specification, scope, boundary, rule, rule basis, actual effect, evidence, and transfer conditions. Those objects must be preserved or reconstructable from preserved state.

The more governance depends on reconstructing implicit state after the fact, the weaker the audit.

---

## 13. Limitations

This paper makes a conceptual synthesis claim about AI-assisted software development governance. It does not propose a new mandatory architecture, empirical performance result, or universal formal model.

Several limitations should be stated explicitly.

First, the paper does not claim that engineering replaces governance. Governance requirements, organizational accountability, legal duties, and ethical principles remain necessary. Engineering-visible state makes those requirements operationally evaluable in software development settings; it does not define all normative content.

Second, the paper does not claim that policy is unimportant. Policy expresses governance requirements. The argument is that policy alone does not create the observable state required to evaluate its own satisfaction.

Third, the paper does not claim that all governance can be made deterministic. Many governance judgments remain qualitative, probabilistic, contested, or context-dependent. Engineering-visible state improves the object of judgment; it does not remove judgment.

Fourth, the paper does not claim that all AI state must be observable. Some internal model state may be inaccessible, irrelevant, proprietary, or too costly to externalize. The claim concerns the subset of state required for governance judgments involving scope, rule basis, behavioral constraints, evidence, or transfer.

Fifth, the paper does not claim that every development workflow needs the same structures. A low-risk internal drafting task may require little more than simple evidence and role clarity. A regulated enterprise software change may require explicit scope artifacts, rulesets, rule-basis records, continuation packages, Decision Risk assessment, and audit trails.

Sixth, the paper does not claim that VSS, Scope, Boundary, BRA, Decision Analysis, Decision Risk, Role State, Work Junction, Continuation Package, or Receiving Capacity are newly invented here. They are treated as prior work. This paper's contribution is their synthesis into a common dependency principle.

Finally, the paper does not claim that engineering organizationally happens before governance. Governance requirements may initiate and guide engineering design. The argument is about operational dependency: governance engineering cannot execute a specific judgment reliably until the relevant state has been represented in engineering-visible form.

---

## 14. Conclusion

Development-stage AI governance cannot operate only through rules placed above AI-assisted software systems. Policies, oversight, accountability, audit, and compliance all require objects of judgment. They require scope, boundary, rules, rule basis, actual effect, evidence, role state, and transfer state to exist in forms that can be identified, inspected, constrained, transferred, and preserved.

At the development behavior level, engineering makes AI-assisted development action governable. It externalizes intent, governed regions, classifications, rules, rule basis, actual effects, and evidence before an individual action can be evaluated.

At the development workflow level, engineering makes handoffs governable. It externalizes role state, work junctions, continuation packages, receiving capacity, evidence transfer, and rule-basis compatibility before multi-actor development work can continue under governance.

The dependency can therefore be stated simply:

```text
Governance Requirement
    -> Engineering Design
    -> Engineering-Visible State
    -> Governance Engineering
```

Governance requirements define what should be governed. Engineering design determines how the relevant condition will be represented. Engineering-visible state makes the condition inspectable. Governance engineering turns that state into operational judgment and control.

Engineering does not replace governance. It produces the explicit state through which governance engineering becomes operational.
