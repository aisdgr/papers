# Scope as a Governance Primitive
> Making Inference, Authority, Effect, and Evidence Explicit in AI Governance

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  

---

## Abstract

AI governance commonly begins with rules: what an AI system may do, what it must not do, who has authority, which risks must be controlled, and what evidence should be retained. These mechanisms implicitly assume that the region to which a governance judgment applies is already known. In practice, however, that region is often distributed across specifications, prompts, retrieved context, access-control policies, workflow configurations, behavioral rules, tool permissions, and the AI system’s own interpretation of a task.

This paper argues that **Scope should be treated as a first-order governance primitive**. Scope identifies an explicit governed region under a defined governance viewpoint and context. It is distinct from Boundary: Scope establishes the reference region, while Boundary determines how an item, action, or transition is classified relative to that region. Policy and authority can subsequently determine what governance consequence follows.

The argument consolidates a concept that has appeared in several earlier works by the author in application-specific forms. Viewpoint-Structured Specification requires explicit Scope for specification elements; Boundary uses Visible Scope as an input to execution-time admissibility; Behavior Rule Architecture uses scope to define rule applicability and execution binding; Decision Analysis distinguishes Visible, Artifact, and Outcome Scopes; Decision Risk extends these distinctions into Behavior Scope, observability, and over-scope risk; Structural Degradation identifies Inference Creep, Semantic Expansion, and Scope Absorption as scope-related degradation phenomena; and Continuation Readiness incorporates scope into cross-role work transfer. The present paper abstracts these uses into a common primitive rather than introducing another application-specific scope.

Scope is viewpoint-dependent. Three viewpoints are developed as representative examples. **Visible Scope** identifies what an actor is exposed to by design. **Authorized Operable Scope** identifies what an actor is authorized to operate on. **Actual Effect Scope** identifies what is ultimately affected as a consequence of execution. These regions cannot be assumed to coincide. In particular, the scope of an authorized operation does not determine the scope of its consequences.

The model also differs from Attribute-Based Access Control. ABAC evaluates attributes and policy to determine whether an access request is permitted; its effective authorization region may change dynamically as attributes and environmental conditions change. This paper does not claim that ABAC lacks scope. Rather, it argues that governance requires relevant scope states to be externalized so that the governed region itself remains identifiable, observable, and traceable before and after a decision.

Scope can then be composed with actors, policies, rules, boundaries, decisions, execution records, and evidence for different governance applications. It can make the intended inference region visible before a decision, provide a reference for authorization, support effect and Decision Analysis after execution, and anchor governance evidence across time.

Scope is therefore not merely metadata or a synonym for permission. It is the reusable structural reference that makes inference, authority, consequence, and evidence jointly interpretable by making explicit the region over which a governance decision has meaning.

**Keywords:** AI Governance, Scope, Governance Primitive, Boundary, Attribute-Based Access Control, Authorization, Inference Governance, Inference Creep, Decision Analysis, Decision Risk, Evidence, AI-Assisted Software Engineering

**Suggested JEL Classification:** M15 (IT Management), O33 (Technological Change: Choices and Consequences; Diffusion Processes), D23 (Organizational Behavior; Transaction Costs; Property Rights), L86 (Information and Internet Services)

---

# 1. Introduction

AI governance is usually discussed through rules, controls, permissions, responsibilities, risk management, human oversight, and auditability.

These mechanisms answer important questions:

- What may the AI do?
- What must it not do?
- Who may approve an action?
- What risks require intervention?
- What evidence must be preserved?
- Who is accountable when execution deviates from expectation?

Yet each of these questions depends on another question that occurs earlier:

> **To what region does this governance judgment apply?**

A rule may state that an AI coding agent is permitted to modify implementation code but prohibited from altering approved requirements. This appears precise until the governed region itself is examined.

Which files constitute implementation?

Which specifications were available to the AI when the decision was formed?

Which modules may actually be modified?

Which types of changes are permitted inside those modules?

If a legitimate implementation change affects an adjacent service, does that downstream effect fall inside or outside the original governance region?

If the model considers an artifact outside the intended task because it appears semantically related, has a boundary been violated—or was the intended inference region never defined in the first place?

These questions expose a structural problem.

AI systems do not operate only through discrete actions. Before acting, they select information, infer relevance, establish relationships, generate alternatives, and form decisions. After acting, their effects can propagate beyond the objects directly manipulated.

What an AI system can see, what it is authorized to operate on, and what its actions eventually affect may therefore constitute different regions.

Yet governance frequently treats these regions as though they were one.

The problem is not that AI systems have no effective Scope.

They necessarily do.

An effective Scope may emerge from:

- a prompt;
- a context window;
- retrieved documents;
- system instructions;
- specification selection;
- access-control policy;
- tool availability;
- workflow state;
- role configuration;
- the model’s own interpretation of relevance.

The governance problem is that this Scope may remain **implicit**.

When Scope remains implicit, the effective governed region is determined indirectly through execution.

A model infers relevance.

A policy engine derives applicability.

A workflow grants tool access.

An engineering artifact absorbs adjacent responsibilities.

A legitimate modification creates effects outside the directly modified area.

Each mechanism may behave correctly in isolation while the governed region itself remains difficult to observe as a persistent governance reference.

This paper argues that Scope should therefore be treated as a **Governance Primitive**.

The contribution is not the invention of the word *scope*. Scope already exists in access control, requirements engineering, project management, system architecture, policy systems, and AI governance.

Nor does this paper introduce Scope into the author’s research program for the first time.

Scope already appears repeatedly across earlier work:

- as Explicit Scope in Viewpoint-Structured Specification;
- as Visible Scope in task execution Boundary;
- as rule applicability and execution scope in Behavior Rule Architecture;
- as Visible, Artifact, and Outcome Scope in Decision Analysis;
- as Visible, Artifact, Behavior, and Outcome Scope in Decision Risk;
- as a failure surface in Inference Creep, Semantic Expansion, and Scope Absorption;
- and as part of Role State and cross-role transfer in Continuation Readiness.

The present paper asks a different question:

> **What do these apparently different uses have in common, and what becomes possible if Scope itself is treated as a reusable governance primitive rather than remaining embedded inside individual mechanisms?**

Four arguments follow.

First, **Scope is not Boundary**. Scope establishes the governed reference region. Boundary evaluates an item, action, or transition relative to that region. Policy and authority then determine what governance consequence follows.

Second, **Scope should be externalized**. Scope may change dynamically, but relevant Scope states and Scope transitions should remain identifiable and observable rather than becoming invisible consequences of AI inference or policy evaluation.

Third, **Scope is viewpoint-dependent**. Visibility, authorization, behavior, effect, audit, responsibility, and risk may select different governed regions from the same system.

Fourth, **Scope is composable**. Scope can be combined with actors, policies, rules, boundaries, decisions, effects, and evidence to support different governance mechanisms.

These properties explain why Scope is more useful as a primitive than as an application-specific label.

This paper is a theoretical synthesis rather than a formal verification model. It does not attempt to prove that one universal mathematical representation of Scope governs every AI system. Instead, it consolidates recurring structures across a sequence of prior governance studies and develops a common abstraction capable of explaining why those structures recur.

---

# 2. Scope Across the Existing Research Line

The purpose of this section is not to summarize earlier work. It is to show that Scope has already functioned as a structural necessity across a series of governance mechanisms without having been treated as an independent primitive.

Each subsection identifies three things:

1. what form Scope took;
2. what governance question it answered;
3. what remained implicit that the present paper makes explicit.

Seen together, these works reveal a conceptual progression.

Scope first appears as a requirement for structuring intent and execution. It subsequently becomes an input to Boundary, an applicability mechanism for behavioral rules, an analytical operand in Decision Analysis, a source of Decision Risk, a surface for structural degradation, and a condition of enterprise workflow continuation.

The present paper extracts the common structure behind these specialized uses.

## 2.1 Viewpoint-Structured Specification: Explicit Scope Before Decision Formation

Viewpoint-Structured Specification treats specification as a persistent, multi-viewpoint governance artifact rather than as a linear document.

Each specification element must satisfy three sufficiency conditions:

- Persistent Addressability;
- Explicit Scope;
- Viewpoint Membership.

The relevant contribution here is **Explicit Scope**.

In VSS, the scope of a specification element cannot remain implicit in document location or surrounding prose. It must be declared so that the element can later be selected, compared, traced, and included in an execution-time Boundary.

VSS also draws an explicit distinction between Scope and Boundary:

> Structured Specification declares Scope; Boundary emerges later through execution-time human selection.

Scope belongs to the declaration structure.

Boundary belongs to the decision structure.

This distinction is one of the conceptual foundations of the present paper.

VSS contributes a second idea: Scope is naturally **viewpoint-dependent**.

A functional requirement, security constraint, architectural concern, data model, or test intent does not describe the same region from the same governance perspective.

The present paper later generalizes this principle beyond specification.

## 2.2 Boundary: Scope as an Input to Execution-Time Governance

*Boundary as an Execution-Time Primitive for AI-Assisted Software Development Governance* distinguishes task-specific execution governance from model-level alignment.

In that model, Visible Scope describes the artifacts accessible to the model at execution time. It explicitly states that Scope determines what the model can observe, not what the model is permitted to do.

The Task Execution Boundary is then resolved from visible context and explicit constraints.

This earlier paper therefore establishes a dependency:

> Scope participates in Boundary formation, but is not itself Boundary.

It also introduces Boundary Evidence as an auditable execution record containing the resolved Scope, constraints, execution identity, and output reference.

The present paper moves one abstraction layer earlier.

The earlier work asks:

> How can an execution-time Boundary be resolved?

The present paper asks:

> What is the general governance role of the Scope that Boundary already requires?

## 2.3 Behavior Rule Architecture: Scope as Rule Applicability

Behavior Rule Architecture separates human intent from structured behavior rules and treats rules as reusable governance assets.

Scope appears at two different layers.

At the rule-definition level, rules have semantic applicability: the contexts or concerns in which a rule is relevant.

At execution time, rules are bound to the current task through a separate execution or Boundary mechanism.

This creates a useful distinction:

**Rule applicability Scope** answers where a reusable rule is semantically relevant.

**Execution Scope** answers where that rule is actually activated during one execution.

BRA therefore demonstrates another reason Scope should not remain buried inside application-specific structures.

A reusable rule cannot permanently encode one execution Boundary. The rule requires stable semantic applicability while execution requires contextual binding.

Scope operates as an interface between reusable governance assets and task-specific execution.

## 2.4 Decision Analysis: Scope as a Comparable Analytical Structure

Decision Analysis moves Scope from an input structure to an analytical structure.

It distinguishes:

- Visible Scope;
- Artifact Scope;
- Outcome Scope.

Visible Scope represents the governing information available before execution.

Artifact Scope represents the intended modification target.

Outcome Scope represents what was actually modified.

The analytical value emerges from their separation.

If Outcome Scope exceeds Artifact Scope, scope exceedance becomes structurally observable.

If an excess modification cannot be traced to known governing material, Decision Vacancy becomes observable.

If scope expansion accumulates across generation sessions, cumulative boundary erosion and Inference Creep can be investigated structurally rather than narratively.

Decision Analysis therefore demonstrates an important property:

> **Different governed regions become analytically useful only when they are represented separately enough to be compared.**

In the generalized model developed here, Artifact Scope can be understood as a specialized form of Authorized Operable Scope for code-modification tasks.

Outcome Scope remains important but is narrower than the Actual Effect Scope introduced later in this paper.

Outcome Scope asks:

> What was actually modified?

Actual Effect Scope asks:

> What was affected as a consequence of execution?

That distinction becomes central when authorization and downstream consequence diverge.

## 2.5 Decision Risk: Scope as Governance Interpretation

Decision Risk takes structural analytical results and interprets them through governance risk.

Its evidence model distinguishes condition evidence from decision evidence.

Condition evidence includes:

- Prompt;
- Visible Scope;
- Artifact Scope;
- Behavior Scope.

Decision evidence includes:

- Decision Record;
- Outcome Scope.

Behavior Scope is especially relevant to the present synthesis.

Artifact Scope answers:

> Where may the actor operate?

Behavior Scope answers:

> What types of action are permitted within that region?

An AI may therefore modify only authorized files while still performing an unauthorized architectural change.

This demonstrates that governance Scope cannot always be reduced to resource identity or directory membership.

Different governance questions select different dimensions.

Decision Risk also makes Scope central to observability. A decision can only be meaningfully evaluated when evidence exists about what was visible, what was authorized, what behavior was permitted, and what actually occurred.

The present paper generalizes this into a broader claim:

> **Scope can function as an evidence anchor.**

## 2.6 Structural Degradation: Scope as a Failure Surface

*Structural Degradation* describes a series of AI-generated software degradation phenomena, several of which directly concern the governed region.

**Inference Creep** occurs when generation expands beyond explicit instruction boundaries.

**Semantic Expansion** occurs when the meaning of an instruction expands beyond its declared semantic range.

**Scope Absorption** occurs when an artifact silently absorbs adjacent concerns.

**Intent Drift** occurs when repeated iterations gradually diverge from their original governing direction.

These conditions differ, but they share a structural feature:

> the effective region changes without a correspondingly explicit governance transition.

Scope Absorption is particularly important because it is not necessarily a conventional Boundary crossing.

A component can gradually absorb adjacent responsibilities without any single action appearing obviously unauthorized.

The reference region itself changes.

This leads to a broader proposition:

> Governance must observe not only whether an actor crosses a Boundary, but whether Scope itself is silently expanded, reinterpreted, or absorbed.

## 2.7 Viewpoint Structure and Scope

VSS used viewpoint as a structural property of specification. The present paper generalizes that property: **viewpoint is not specific to specification, but to Scope itself**.

In VSS, a Viewpoint is a declared semantic boundary associated with a specific concern.

A security viewpoint, functional viewpoint, architectural viewpoint, and testing viewpoint can each produce different structurally relevant sets of specification elements.

The present paper extends the same logic to governance more generally.

A Scope is not simply a set of things.

It is a set selected **under a governance viewpoint**.

This explains why Visible Scope, Operable Scope, Behavior Scope, Effect Scope, Audit Scope, and Responsibility Scope can all legitimately coexist without competing for one “correct” definition.

Each represents a different selection criterion applied to the same underlying system.

## 2.8 Continuation Readiness: Scope Across Role Transitions

*Beyond HITL: Continuation Readiness as a Governance Requirement for Enterprise AI Workflows* extends Scope beyond a single execution event.

Its Role State includes:

- actor;
- viewpoint;
- policy;
- scope;
- authority;
- evidence access;
- expected output.

At human-to-AI transitions, insufficiently specified scope can force the receiving AI to infer what the delegating actor failed to define.

At AI-to-human or AI-to-AI transitions, the receiving actor must have compatible scope, authority, and evidence access in order to continue the work.

Scope therefore becomes a transferable governance condition across role, responsibility, and authority boundaries.

This shows that Scope is not merely a software resource concept.

It belongs to a more general governance architecture.

## 2.9 Knowledge Evolution: Scope and the Reuse of Decision Evidence

Knowledge Evolution distinguishes among organizational materials such as:

- documents;
- decision records;
- action records;
- issue histories;
- outcome records.

It argues that decisions and outcomes can become reusable knowledge materials only when their provenance and validation status remain recoverable.

Scope strengthens this model.

A decision record without a clear governed region may reveal what was decided but not the region over which that decision was intended to apply.

An outcome may reveal what happened but not whether the outcome lies within or outside the original decision domain.

Scope can therefore contribute to the later reuse of decision evidence by preventing decontextualized generalization.

---

# 3. From Specialized Scopes to a General Primitive

Specialized Scope constructs in prior work are not competing definitions.

They are application-specific projections of a more general governance primitive.

The following mapping shows why.

| Earlier construct | Governance question | Position in the generalized model |
|---|---|---|
| VSS Explicit Scope | What concern does this specification element cover? | Specification-viewpoint Scope |
| Boundary Visible Scope | What can the AI observe in this execution? | Visible Scope |
| BRA Rule Scope | Where is this rule semantically applicable? | Rule-applicability Scope |
| BRA Execution Scope | Where is this rule bound now? | Context-bound Scope |
| DA Artifact Scope | What is intended to be modified? | Specialized Authorized Operable Scope |
| DA Outcome Scope | What was actually modified? | Observed operation/outcome Scope |
| DR Behavior Scope | What categories of action are permitted? | Behavioral authorization Scope |
| Actual Effect Scope | What was actually affected? | Consequence-viewpoint Scope |
| Role State Scope | What lies within the role’s working or authority region? | Role-viewpoint Scope |
| Audit Scope | What must retain traceable evidence? | Evidence/audit-viewpoint Scope |
| Responsibility Scope | What falls under a role’s accountability? | Responsibility-viewpoint Scope |

The table resolves an apparent terminology problem.

Earlier works do not need to be retroactively renamed.

Their terminology describes the specific problem being addressed in each paper.

The present paper instead provides the abstraction beneath them.

Three implications follow directly from the mapping.

First, Scope is **not tied to one artifact class**.

A Scope can concern code, data, specifications, behavior, responsibility, decisions, effects, or evidence.

Second, Scope is **not tied to one governance mechanism**.

Authorization uses Scope, but Scope is not authorization.

Boundary uses Scope, but Scope is not Boundary.

Audit uses Scope, but Scope is not evidence.

Third, Scope is **not defined by one fixed dimension**.

The same system can support several simultaneous Scope states because different viewpoints ask different governance questions.

The abstraction is therefore not:

> Scope equals a list of resources.

It is:

> **Scope is an explicitly identifiable governed region defined under a specific governance viewpoint and context.**

---

# 4. What Is Scope?

## 4.1 Definition

For the purposes of this paper:

> **Scope is an explicitly identifiable governed region selected according to a governance viewpoint within a governance context.**

Three terms require clarification:

- governed region;
- viewpoint;
- governance context.

## 4.2 Governed Region

A Scope contains items that governance must be able to identify as belonging or not belonging to a particular question.

The term *item* is intentionally broad.

A governed item may be:

- a requirement;
- a document;
- a source file;
- a function;
- an API;
- a configuration;
- a data element;
- a rule;
- a system state;
- a behavior;
- a relationship;
- an effect;
- a decision;
- a responsibility.

The common requirement is **identifiability**.

If governance cannot identify an item sufficiently to determine whether it belongs to a region, the Scope cannot function as a reusable reference.

## 4.3 Viewpoint

A governance viewpoint defines the criterion by which items are selected into a Scope.

A viewpoint therefore answers:

> **Under what governance question are these items being included?**

Examples:

A visibility viewpoint asks:

> What is the actor exposed to?

An authorization viewpoint asks:

> What may the actor operate on?

A behavior viewpoint asks:

> What categories of action are permitted?

An effect viewpoint asks:

> What was actually affected?

An audit viewpoint asks:

> What requires trace evidence?

A responsibility viewpoint asks:

> What falls under this role’s accountability?

This definition constrains the term *viewpoint*.

A viewpoint is not merely a stakeholder opinion.

It is a **selection criterion**.

Different viewpoints may produce different Scope regions from the same system.

This is not inconsistency.

It is a consequence of asking different governance questions.

## 4.4 Governance Context

Scope also exists within context.

A project may define a broad region.

A development stage may refine it.

A task may narrow it.

A particular decision may narrow or expand it again.

An execution event may instantiate a highly specific region.

Governance Context can therefore be hierarchical:

Project  
→ Development Stage  
→ Task  
→ Decision  
→ Execution

This paper does not treat Stage as an intrinsic dimension of Scope.

Stage is the context within which Scope is instantiated.

The consequence is important:

Scope can change.

The governance requirement is not immutability.

It is explicitness.

> **Scope may change, but relevant Scope states and Scope transitions should themselves become observable governance events.**

---

# 5. Scope Is Not Boundary

The distinction between Scope and Boundary is the first conceptual requirement of the model.

Scope answers:

> **What is the governed reference region?**

Boundary answers:

> **Where does a candidate item, action, or transition stand relative to that region?**

Policy and authority then answer:

> **What consequence follows from that classification?**

These roles should remain separate.

Consider an Authorized Operable Scope consisting of the payment service.

A proposed modification to the checkout service may be outside that Scope.

Scope defines the reference region.

Boundary determines that the candidate operation lies outside it.

Policy may then require:

- denial;
- approval;
- escalation;
- creation of a new task;
- expansion of Scope.

The concepts therefore form a dependency:

**Scope → Boundary → Governance Decision**

This resolves a frequent conflation.

Boundary is not merely “the edge of Scope.”

In governance, Boundary is a determination relative to a Scope state.

Likewise, Scope does not itself say whether something outside it is prohibited.

An outside classification can trigger different consequences under different policies.

This is why the present model also avoids collapsing:

**Scope ≠ Boundary ≠ Policy**

The earlier Boundary paper already relies on Visible Scope and explicit constraints in order to resolve execution-time admissibility. The present paper isolates the structure that such a Boundary presupposes.

---

# 6. Why Scope Must Be Externalized

An effective governed region can exist without being explicit.

That is the central governance problem addressed here.

## 6.1 Implicit Scope

In an AI system, an effective Scope may be produced by:

- prompt content;
- context selection;
- retrieval;
- workspace configuration;
- system instructions;
- model memory;
- policy rules;
- tool permissions;
- workflow routing;
- model-generated relevance judgment.

A policy engine may derive a permitted resource region dynamically.

A developer may informally assume which modules belong to a task.

A model may infer that adjacent functionality is relevant.

The system may function correctly.

Yet the governed region is visible only indirectly through the mechanism that used it.

## 6.2 Externalized Scope

Externalizing Scope turns the implicit region into a governance reference that can be:

- identified;
- inspected;
- versioned;
- compared;
- approved;
- expanded;
- narrowed;
- transferred;
- audited.

This does not require Scope to be static.

Dynamic AI workflows often need dynamic Scope.

The distinction is:

> **Dynamic Scope should mean explicitly changing Scope, not invisibly changing governance.**

An expansion from one Scope state to another can therefore become an observable governance event.

For example:

- additional repository region requested;
- new data source exposed;
- authorization expanded;
- responsibility reassigned;
- new effect region detected;
- inference region widened.

The value is not that the transition is always forbidden.

The value is that it can be seen.

## 6.3 Scope Artifact

Externalization requires a representation.

The conceptual Scope should therefore be distinguished from the artifact through which governance observes it.

A **Scope** is the governed region.

A **Scope Artifact** is the inspectable representation of that region.

A Scope Artifact may contain:

- Scope identity;
- Governance Context;
- viewpoint;
- included items;
- authority basis;
- version;
- provenance;
- change history;
- linked evidence.

This distinction prevents the term Scope from simultaneously meaning a governed set, a document, metadata, and evidence.

The region and its representation are related but not identical.

The Scope Artifact is the mechanism through which a changing Scope becomes a governance-visible object.

## 6.4 Externalization and Decision Meaning

A governance decision is only meaningful relative to a region.

“Permit” is incomplete without identifying what is permitted.

“Compliant” is incomplete without identifying the applicable domain.

“Effect exceeded expectation” is incomplete without identifying the expected region.

“Evidence exists” is incomplete without knowing which governance state it supports.

Externalized Scope therefore provides a semantic coordinate for governance decisions.

---

# 7. Scope and Attribute-Based Access Control

Attribute-Based Access Control is the closest neighboring concept because it already evaluates subject, action, resource, environmental attributes, and policy.

The distinction must therefore be stated carefully.

This paper does **not** claim that ABAC has no scope.

Any meaningful ABAC policy necessarily has applicability.

The difference lies in how the effective region is represented and what governance role it serves.

## 7.1 What ABAC Does

ABAC principally answers:

> **May this subject perform this action on this resource under the current attributes and environmental conditions?**

Its strength is dynamic authorization.

The result may legitimately change as:

- subject attributes change;
- resource attributes change;
- environment changes;
- relationships change;
- policy changes.

This flexibility is desirable.

## 7.2 Derived Authorization Region

In ABAC, the effective authorization region is typically derived through evaluation.

A specific request is matched against current attributes and policies.

The resulting authorization state may therefore differ from one request to another.

This paper does not treat that as a weakness.

Instead, it asks a separate question:

> **Should the governed region relevant to inference, authorization, effect, and evidence remain independently identifiable beyond the individual policy evaluation?**

## 7.3 Authorization as One Application of Scope

The proposed Scope Primitive and ABAC are therefore complementary.

An authorization application may combine:

- Actor;
- Authorized Operable Scope;
- Policy.

ABAC can perform the authorization evaluation.

Scope remains the governance reference.

This means ABAC can be understood as one mechanism operating over one particular Scope viewpoint.

The distinction matters because the authorization decision alone does not automatically represent:

- everything exposed to the AI before the request;
- the intended inference region;
- all downstream consequences of an authorized action;
- the audit region;
- the responsibility region of a receiving role.

Authorization is therefore an application of Scope, not a complete representation of Scope.

## 7.4 Scope Change Visibility

The most important distinction concerns change.

ABAC may produce a different effective authorization region when attributes change.

The present model permits the same dynamic behavior.

It adds one governance requirement:

> **When a change materially alters the governed decision region, the relevant Scope state or transition should remain identifiable and traceable.**

This converts a change in governance region from an invisible consequence of evaluation into an observable governance event.

The difference can be summarized as follows:

| Dimension | ABAC | Scope Governance |
|---|---|---|
| Primary question | Is this request permitted? | What governed region should remain explicit? |
| Main output | Authorization decision | Governance reference |
| Effective region | Commonly derived from policy and attributes | Explicitly identifiable Scope state |
| Dynamic change | Expected and supported | Expected, but governance-relevant transitions remain traceable |
| Visibility Scope | Not the central abstraction | Explicit viewpoint |
| Effect Scope | Not primary authorization output | Explicit viewpoint |
| Historical comparison | Depends on retained policy/attribute evidence | Scope state designed to be compared |
| Evidence role | Supports authorization reconstruction | Connects inference, authority, effect, and audit |

The proposed model is therefore not “ABAC plus another access-control layer.”

It operates at a broader governance abstraction.

---

# 8. Three Representative Scope Viewpoints

The model does not require exactly three types of Scope.

Three viewpoints are emphasized because together they expose an important governance discontinuity in AI systems:

- what the actor can see;
- what the actor may operate on;
- what execution actually affects.

## 8.1 Visible Scope

Visible Scope answers:

> **What has governance exposed to the actor?**

For an AI system this may include:

- requirements;
- specifications;
- source code;
- retrieved documents;
- previous decisions;
- data;
- tools;
- memory;
- external APIs.

Visible Scope refers to **designed exposure**.

It does not claim that the model:

- actually attended to everything;
- understood everything;
- used everything;
- inferred correctly from everything.

The distinction is essential.

Governance can specify what was exposed.

It cannot equate exposure with cognition.

Visible Scope is relevant to:

- information exposure;
- confidentiality;
- retrieval governance;
- context leakage;
- decision reconstruction.

## 8.2 Authorized Operable Scope

Authorized Operable Scope answers:

> **What is the actor explicitly authorized to operate on?**

This is the viewpoint closest to traditional access control.

For a software-development agent, Operable Scope may identify:

- files;
- modules;
- services;
- databases;
- specifications;
- configuration;
- external systems.

DA’s Artifact Scope can be understood as a specialized Authorized Operable Scope for modification tasks.

DR’s Behavior Scope adds a different but related dimension:

even inside an authorized artifact region, only some types of operations may be allowed.

For example, an agent may be allowed to modify files in `payment/` but prohibited from:

- introducing a new public API;
- changing database schema;
- removing tests;
- creating external dependencies.

This demonstrates that location Scope and behavioral authorization Scope are separate governance questions.

## 8.3 Actual Effect Scope

Actual Effect Scope answers:

> **What was ultimately affected as a consequence of execution?**

This is intentionally broader than DA’s Outcome Scope.

Outcome Scope records what was directly modified.

Actual Effect Scope includes downstream consequences.

An AI agent may modify only:

`payment/service/api.py`

yet the consequence may include:

- checkout behavior;
- billing integration;
- client contracts;
- test failures;
- operational behavior.

This leads to a central proposition:

> **The scope of an authorized operation does not determine the scope of its consequences.**

An operation can remain completely inside Authorized Operable Scope while its effects propagate outside it.

This is **Effect Expansion**.

Effect Expansion is not automatically an authorization violation.

The operation may have been fully legitimate.

Governance must therefore distinguish:

**Operational violation**

from

**Consequence expansion**.

This distinction is one of the principal reasons Scope cannot be reduced to access control.

## 8.4 Other Viewpoints

Visibility, authorization, and effect are representative rather than exhaustive.

Other possible Scope viewpoints include:

- Behavior Scope;
- Responsibility Scope;
- Approval Scope;
- Audit Scope;
- Risk Scope;
- Rule Applicability Scope;
- Knowledge Validity Scope.

The primitive is not the three-viewpoint taxonomy.

The primitive is the explicit governed region produced under a declared governance viewpoint.

---

# 9. Inference Scope Visibility

Section 8 defined three representative Scope viewpoints. This section examines a governance condition that cuts across all of them: **the relationship between what an actor can see and what governance intends for that actor to reason about**.

Visible Scope is not equivalent to the intended inference region.

This distinction is particularly important for AI governance.

An AI system may legitimately see much more information than should directly govern a particular decision.

Consider a coding agent with access to an entire repository.

Its Visible Scope may include:

- payment services;
- authentication;
- billing;
- checkout;
- observability;
- deployment;
- shared utilities.

The current task may concern a payment-validation rule.

The system needs broad visibility because dependencies may matter.

But broad visibility does not mean every visible artifact should automatically become part of the governed reasoning region.

If governance does not externalize an intended inference region, the model must still decide relevance.

The effective inference region becomes **model-determined**.

This is not inherently wrong.

Inference requires selecting relevance.

The governance issue is whether a change in the inferred problem region remains visible.

The relevant distinction is therefore:

**Visible Scope**  
What information was available?

**Inference Scope**  
What region was the decision expected to be grounded in?

The two may overlap substantially, but they are not necessarily identical.

## 9.1 Why This Matters

Suppose the payment task reveals that a shared contract must be changed.

The AI may be correct.

There are two very different governance situations.

### Situation A — Explicit Scope Transition

The agent identifies that the required region exceeds the current intended Scope.

A transition is requested.

Governance can:

- expand Scope;
- reject the expansion;
- create another task;
- request approval;
- escalate.

### Situation B — Silent Inference Expansion

The agent simply reinterprets the task as including the shared contract.

No explicit transition occurs.

The resulting behavior may be technically correct, but governance loses visibility into where the decision region changed.

The problem is therefore not inference itself.

The problem is:

> **Inference becoming the mechanism by which governance Scope is silently determined.**

## 9.2 Inference Creep

This distinction clarifies Inference Creep.

Inference Creep does not mean that an AI considers an adjacent dependency.

It means that the effective governed region expands through model interpretation without a corresponding governance-visible transition.

An implicit inference Scope therefore creates the structural conditions under which Inference Creep may occur.

It does not guarantee it.

A system may instead:

- stop;
- ask;
- escalate;
- apply Default Deny;
- explicitly request Scope expansion.

The governance objective is not to eliminate inference.

It is to make relevant inference-region changes observable.

---

# 10. Scope as a Composable Governance Primitive

A primitive becomes valuable through composition.

Scope does not itself perform authorization, risk analysis, audit, or enforcement.

It provides a reusable structural reference for those mechanisms.

## 10.1 Scope + Boundary

Scope supplies the reference region.

Boundary classifies an item, action, or transition relative to the region.

Policy determines what follows.

This relationship is already implicit in the earlier Boundary model.

## 10.2 Actor + Scope + Policy

Actor, Authorized Operable Scope, and Policy can provide input to an authorization mechanism.

Possible mechanisms include:

- ABAC;
- RBAC;
- policy engines;
- capability systems;
- workflow approval;
- human authorization.

Scope is not the authorization algorithm.

It is the region to which authorization applies.

## 10.3 Rule + Scope

BRA demonstrates that a reusable rule requires semantic applicability while execution requires context-specific activation.

A rule can therefore carry or reference one Scope while Boundary resolution selects the current execution Scope.

Scope connects reusable governance assets to dynamic execution.

## 10.4 Scope + Viewpoint

VSS demonstrates that viewpoint-specific regions make overlap and conflict observable.

The same principle generalizes.

A visibility region and an authorization region can be compared.

An authorization region and an effect region can be compared.

A responsibility region and an approval region can be compared.

The value arises precisely because the scopes are not collapsed.

## 10.5 Operable Scope + Effect Scope

Comparing Authorized Operable Scope with Actual Effect Scope exposes Effect Expansion.

The difference can become input to:

- impact analysis;
- Decision Analysis;
- Decision Risk;
- review;
- approval;
- change management.

Scope does not itself interpret the significance.

It makes the difference available for interpretation.

## 10.6 Role + Scope + Authority

Continuation Readiness demonstrates another form of composition.

A Role State combines:

- actor;
- viewpoint;
- policy;
- scope;
- authority;
- evidence access.

A transfer can fail if the receiving role’s Scope does not cover the issue transferred to it.

Likewise, H2A delegation can fail when the human provides insufficient Scope and the AI fills the missing region through inference.

This extends Scope from execution control into enterprise workflow governance.

## 10.7 Scope + Evidence

Perhaps the broadest composition is with evidence.

Evidence becomes governance evidence only when its relation to a governed region can be established.

This relationship is developed in the next section.

---

# 11. Scope as an Evidence Anchor

Decision governance requires evidence before and after execution.

The two sides become more useful when they can reference the same Scope state or sequence of Scope states.

## 11.1 Before the Decision

Pre-decision evidence may include:

- Governance Context;
- Scope identity;
- viewpoint;
- Visible Scope;
- intended inference region;
- Authorized Operable Scope;
- Behavior Scope;
- applicable rules;
- policy;
- authority.

This evidence answers:

> **Under what governed conditions was the AI expected to form this decision?**

This is more precise than merely retaining a prompt.

A prompt may describe intent.

Scope describes the region over which the intent applies.

## 11.2 During the Decision

Decision-time evidence may include:

- encountered ambiguity;
- alternatives considered;
- rules invoked;
- assumptions;
- requested Scope expansion;
- authority escalation;
- rejected actions;
- decision resolution.

This evidence answers:

> **What governance-relevant transitions occurred while the decision was being formed?**

A Scope change is especially important because it changes the meaning of subsequent actions.

## 11.3 After the Decision

Post-decision evidence may include:

- Decision Record;
- execution record;
- actual modifications;
- Outcome Scope;
- Actual Effect Scope;
- Boundary classifications;
- test evidence;
- traces;
- downstream observations.

This evidence answers:

> **What happened, and what region was actually affected?**

## 11.4 Scope Artifact as the Evidence Reference

The common reference for these records is not an abstract Scope alone.

It is the **Scope Artifact** introduced in Section 6.3: the identifiable representation of the Scope state that existed at the relevant time.

A Scope Artifact allows evidence to refer to:

- which Scope existed;
- under which viewpoint;
- in which Governance Context;
- under which authority;
- in which version;
- and through which subsequent transitions.

This makes Scope history inspectable rather than reconstructive.

The key property is continuity.

Pre-decision and post-decision records can refer to:

- the same Scope Artifact;
- or a traceable sequence of Scope Artifact versions.

This makes several questions answerable:

What was visible at the time?

What region was intended for inference?

What was authorized?

Was authorization expanded?

Who approved the change?

What was actually modified?

What else was affected?

Was effect expansion expected?

Which later decision was based on the resulting evidence?

The logs may already exist without Scope.

What Scope changes is their interpretability.

This provides one of the strongest arguments for treating Scope as a governance primitive:

> **Scope does not merely constrain action. It makes governance evidence locatable.**

---

# 12. Scope-Related Governance Conditions

Scope-related governance conditions can be grouped into three layers.

The first concerns how Scope is defined and exposed.

The second concerns what happens when execution interacts with Scope.

The third concerns how Scope changes accumulate over time.

This distinction is important because not every Scope difference is a failure, and not every governance failure is an authorization violation.

## 12.1 Scope Definition and Exposure Conditions

### 12.1.1 Undefined Scope

The governed region has not been explicitly established.

Governance applicability becomes interpretive.

The system may know that a rule exists without knowing exactly where it applies.

Undefined Scope is therefore not merely a documentation weakness.

It removes the reference against which later governance decisions are interpreted.

### 12.1.2 Exposure Region

An actor may see items that it is not authorized to operate on.

This region can be described as the **Exposure Region**.

Exposure is not automatically a violation.

Broad visibility may be necessary for comprehension.

However, exposure is governance-relevant because it affects:

- confidentiality;
- information leakage;
- inference possibilities;
- model-generated assumptions.

The important point is that visibility and authority are distinct.

### 12.1.3 Blind Operation

The inverse condition is also possible.

An actor may be authorized to operate on a region without sufficient visibility into the information required to make a responsible decision.

This is **Blind Operation**.

Blind Operation does not necessarily indicate access-control failure.

The authorization may be technically correct.

The governance problem is that authority exceeds the informational basis required for responsible execution.

## 12.2 Execution and Governance Interaction Conditions

### 12.2.1 Operational Scope Violation

An Operational Scope Violation occurs when an actor actually performs an operation outside its Authorized Operable Scope.

This is the condition most directly associated with authorization and Boundary enforcement.

The critical object is the actual operation.

It should not be inferred merely from downstream effects.

### 12.2.2 Effect Expansion

Effect Expansion occurs when an authorized operation produces consequences beyond its Authorized Operable Scope.

This must remain distinct from operational violation.

A valid local modification can create a broad system effect.

The governance question therefore becomes:

- Is the effect acceptable?
- Was it expected?
- Does it require review?
- Should authority change?
- Should future Scope definitions be revised?

Effect Expansion is an analytical condition before it becomes a risk judgment.

### 12.2.3 Decision Vacancy

Decision Vacancy occurs when an item, action, or Scope transition reaches a region for which no authoritative governance determination exists.

This differs from denial.

A denied action has an answer.

A Decision Vacancy has no authoritative answer yet.

The system may need:

- escalation;
- adjudication;
- Scope expansion;
- new policy;
- human decision.

## 12.3 Scope Evolution Conditions

### 12.3.1 Inference Creep

Inference Creep occurs when a missing or implicit governance region is filled through model inference and the effective Scope expands without an explicit governance transition.

The defining problem is not inference itself.

The problem is that AI interpretation silently substitutes for Scope governance.

### 12.3.2 Scope Absorption

Scope Absorption occurs when an artifact, component, or decision region gradually incorporates adjacent responsibilities.

Unlike a simple Boundary crossing, the effective responsibility of the artifact changes.

The original Scope is not merely exceeded.

It is redefined through accumulated local changes.

This is particularly difficult to detect without historical Scope states.

### 12.3.3 Cumulative Scope Expansion

A sequence of individually small and locally reasonable Scope expansions may accumulate into a region far broader than the original governed intent.

No single change needs to look serious.

The anomaly appears only longitudinally.

This condition is especially important in AI-assisted development, where repeated sessions may have limited awareness of prior Scope transitions.

---

# 13. Engineering Demonstration

Consider an AI coding agent assigned to implement a payment-validation change.

The organization provides:

- full repository visibility;
- payment requirements;
- architecture documentation;
- tests.

The current task defines:

**Visible Scope:** the repository and relevant engineering documents.

**Intended Inference Region:** payment validation and explicitly declared dependencies.

**Authorized Operable Scope:** files under the payment service.

**Behavior Policy:** shared API contracts cannot be changed without additional approval.

This single scenario illustrates several structurally different conditions.

## 13.1 Case A — Normal Authorized Operation

The agent modifies only payment-validation implementation files.

The operation remains within Authorized Operable Scope.

The change produces only the expected local behavior.

No Scope anomaly is observed.

This represents the baseline condition.

## 13.2 Case B — Operational Scope Violation

The agent modifies:

`shared/schema.py`

The file is outside Authorized Operable Scope.

The violation concerns the operation itself.

A Boundary and authorization mechanism can classify and respond to it.

The downstream quality of the modification is irrelevant to the initial finding.

The code might be excellent and still be outside authority.

## 13.3 Case C — Effect Expansion

The agent modifies only payment-service files.

No authorization Boundary is crossed.

After execution, however:

- checkout behavior changes;
- billing integration breaks;
- downstream tests fail.

The Actual Effect Scope exceeds the direct operational region.

This is Effect Expansion.

The appropriate question is not:

> Why did authorization fail?

Authorization may have worked exactly as intended.

The appropriate question is:

> What governance response is required by a legitimate operation whose consequences extend farther than its operable region?

This may trigger:

- impact analysis;
- Decision Analysis;
- Decision Risk;
- additional review;
- rollback;
- further authorization.

The distinction demonstrates why Operable Scope and Effect Scope cannot be collapsed.

## 13.4 Case D — Blind Operation

Suppose the agent is authorized to modify the payment module but has not been given access to the shared interface specification on which the module depends.

The operation remains inside authority.

The problem is insufficient visibility.

The agent is allowed to act in a region it cannot adequately understand.

This is Blind Operation.

It is a governance design weakness, not necessarily an access violation.

## 13.5 Case E — Decision Vacancy and Inference Creep

The agent determines that the cleanest solution requires modifying the shared contract.

Policy states that shared-contract modification requires additional approval.

However, the workflow does not specify:

- who may approve it;
- how approval is requested;
- whether execution should stop;
- whether the task should be split.

A Decision Vacancy exists.

If the agent stops and escalates, governance becomes aware of the vacancy.

If the agent infers that “completing the task” implies authority to modify the contract, the effective Scope expands through model interpretation.

That is the condition under which Inference Creep occurs.

The technical conclusion may be reasonable.

The governance transition is not.

## 13.6 Case F — Scope Absorption

Consider a different evolution.

The agent never directly modifies the shared contract.

Instead, several payment-related compatibility rules are gradually added to a common utility module.

Each individual change appears reasonable.

No obvious Boundary crossing occurs.

Over several iterations, however, the utility module begins to encode payment-domain responsibilities that were never part of its original role.

Its effective Scope has expanded.

This is Scope Absorption.

Unlike Cases B through E, Scope Absorption does not require any single identifiable Boundary crossing or explicit authorization failure.

The governed region expands incrementally as adjacent responsibilities become incorporated into an artifact or decision domain.

Each individual step may appear locally legitimate.

> **Governance can only detect this condition if the reference Scope state is preserved across time.**

This example illustrates why Scope history matters.

A Boundary evaluates a present candidate against a present region.

Scope governance can additionally ask:

> **Has the region itself changed?**

Without prior Scope evidence, this question becomes extremely difficult to answer.

## 13.7 Case G — Cumulative Scope Expansion

Suppose five sequential AI sessions each make a small, justified expansion.

Session 1 modifies payment validation.

Session 2 adds payment-specific helper logic.

Session 3 updates a shared utility.

Session 4 introduces billing compatibility.

Session 5 restructures checkout integration.

No individual session looks severely out of Scope.

Collectively, however, the cumulative governed region is no longer recognizable as the original payment-validation task.

This illustrates Cumulative Scope Expansion.

The failure is longitudinal rather than local.

## 13.8 Evidence

Without explicit Scope Artifacts, later review may contain:

- prompts;
- source-code diffs;
- policy logs;
- test failures;
- AI-generated explanations.

The reviewer must reconstruct:

- what the AI was supposed to consider;
- what it was allowed to modify;
- whether Scope changed;
- what effect propagated.

With explicit Scope Artifacts, the same evidence can instead reference identifiable Scope states:

- Visible Scope identifies exposure.
- Inference Scope identifies intended relevance.
- Operable Scope identifies authority.
- Outcome Scope identifies modification.
- Effect Scope identifies consequence.
- Scope Artifact history identifies expansion.

The difference is not necessarily more logging.

It is the presence of a persistent governance reference.

---

# 14. Broader Implications

## 14.1 Scope as a Prerequisite

Several governance mechanisms examined in this paper depend on Scope in different ways.

**Boundary** requires a reference region before an item or action can meaningfully be classified as inside, outside, or unresolved.

**Authorization** may be dynamically calculated, but its result is meaningful only relative to the region being authorized.

**Inference governance** cannot identify inference expansion unless some intended decision region has been made explicit.

**Decision Analysis** requires separately identifiable regions in order to compare authorized, observed, and affected states.

In each case, Scope is not the mechanism itself.

It is a structural prerequisite that gives the mechanism something to operate against.

## 14.2 Scope Before Risk Interpretation

A difference between regions is not automatically risk.

It is first a structural condition.

Risk interpretation can then consider:

- severity;
- reversibility;
- authority;
- system impact;
- organizational policy.

This maintains the separation between analytical observation and governance judgment developed in Decision Analysis and Decision Risk.

## 14.3 Scope Before Evidence

Evidence without Scope can show that an event occurred.

Evidence with Scope can help show:

- under what authority it occurred;
- whether it exceeded a governed region;
- whether the governed region itself changed.

This distinction strengthens auditability.

## 14.4 Scope Across Roles

Continuation Readiness demonstrates that work transfer requires compatible Scope and authority on both sides of a Work Junction.

Scope therefore belongs not only to agent execution but also to organizational workflow design.

## 14.5 Scope Across Time

A decision may be legitimate under one Scope state and inappropriate under another.

Preserving Scope state therefore improves:

- historical interpretation;
- audit;
- retrospective analysis;
- organizational learning;
- Knowledge Evolution.

More importantly, the Scope Absorption scenario in Section 13 illustrates a condition that cannot be detected from one execution event alone.

A current Boundary may be perfectly valid relative to the current Scope.

The governance problem may instead be that the Scope itself has silently changed over time.

This yields a broader principle:

> **Governance of dynamic Scope requires not only knowledge of the current Scope state, but preservation of prior Scope states against which structural change can be observed.**

This is one of the key differences between Scope governance and transaction-level authorization.

## 14.6 Scope as a Primitive, Not a Universal Policy

Treating Scope as a primitive does not mean defining one enterprise-wide Scope that governs everything.

A primitive is reusable precisely because it can be instantiated differently.

Each governance application may construct its own Scope under an explicit viewpoint and context.

The commonality lies in structural role, not identical content.

---

# 15. Limitations

This paper is a theoretical synthesis rather than an empirical validation.

Several limitations follow.

## 15.1 Scope Does Not Guarantee Good Governance

Explicit Scope does not ensure that a policy is:

- correct;
- ethical;
- complete;
- proportionate;
- effective.

A clearly defined bad policy remains a bad policy.

Scope improves structural interpretability, not policy quality.

## 15.2 Scope Is Necessary but Not Sufficient

The applications described here also require:

- Boundary;
- policy;
- authority;
- constraints;
- evidence;
- adjudication;
- enforcement.

Scope is a structural reference, not a complete governance system.

## 15.3 Visible Scope Is Designed Exposure

Visible Scope refers to what governance exposes to the actor.

It does not prove:

- actual model attention;
- actual comprehension;
- actual use.

Operationalizing the difference remains a research problem in LLM, RAG, and agent systems.

## 15.4 Inference Scope Cannot Fully Constrain Reasoning

The intended inference region should not be interpreted as an attempt to specify every legitimate reasoning step.

AI may discover relationships outside an initially expected region.

The purpose of inference Scope is to make expansion visible, not to eliminate adaptive reasoning.

## 15.5 Effect Scope May Be Incomplete

Actual Effect Scope may be difficult to reconstruct in:

- distributed systems;
- asynchronous systems;
- probabilistic systems;
- highly coupled architectures.

Effect observation may require:

- traces;
- dependency analysis;
- telemetry;
- tests;
- provenance;
- domain-specific evidence.

## 15.6 No Authorized Effect Scope Is Introduced

This paper deliberately does not introduce an **Authorized Effect Scope** as a fourth required viewpoint.

A governance system might eventually define acceptable consequence regions prospectively.

That is a legitimate future direction.

It is not required for the present primitive.

## 15.7 Viewpoints Are Not Exhaustive

Visibility, authorization, effect, behavior, responsibility, and audit are examples.

Different domains may require additional viewpoints.

The model does not propose a closed taxonomy.

## 15.8 Earlier Terminology Remains Valid

The paper does not retrospectively rename Artifact Scope, Outcome Scope, Behavior Scope, or other earlier constructs.

Those terms remain appropriate within their original analytical contexts.

The present contribution is the abstraction beneath them.

## 15.9 Empirical Validation Remains Future Work

The paper does not empirically demonstrate that explicit Scope reduces:

- AI failure;
- authorization errors;
- Decision Vacancy;
- Inference Creep;
- governance risk.

It establishes a theoretical relationship that can support later engineering implementation and empirical testing.

---

# 16. Conclusion

Across AI governance and AI-assisted engineering, Scope has often appeared as a secondary term embedded inside another mechanism.

Specifications have Scope.

Rules have Scope.

Access-control policies have applicability.

Executions have Scope.

Roles have Scope.

Decisions have Scope.

Effects have Scope.

Audits have Scope.

Earlier work in this research sequence used these forms separately because each paper examined a different governance problem.

Viewed together, they reveal a more general structure.

Scope is the explicit governed region against which other governance mechanisms operate.

It is not Boundary.

Boundary requires Scope.

It is not Authorization.

Authorization evaluates or consumes an applicable Scope.

It is not Policy.

Policy determines what follows from a Scope-relative classification.

It is not Effect.

Effect can be observed against Scope.

It is not Evidence.

Evidence becomes more meaningful governance evidence when it can refer back to an identifiable Scope state.

Nor is Scope necessarily static.

It may:

- expand;
- narrow;
- refine;
- transfer;
- be reinterpreted;
- evolve across time.

The governance requirement is not immutability.

The requirement is that relevant Scope changes not remain invisible consequences of inference, attribute evaluation, workflow routing, or execution.

This is especially important for AI systems.

An AI may see more than it is authorized to modify.

It may be authorized to modify more than it adequately understands.

It may legally operate on a narrow region while producing broad consequences.

It may infer itself into an undefined region when governance provides no authoritative decision.

It may gradually absorb adjacent responsibilities without any single obvious Boundary crossing.

These are not one problem.

They become distinguishable only when the relevant governed regions are made explicit.

For this reason, Scope is best understood as a **Governance Primitive**:

> **a reusable structural reference that makes the region of inference visible before a decision and makes authority, Boundary, effect, risk, and evidence interpretable after it.**

Governance does not begin by asking whether an AI action is permitted.

It begins one step earlier:

> **by making explicit the region over which that decision has meaning.**

---

# References

Hu, V. C., Ferraiolo, D. F., Kuhn, D. R., Schnitzer, A., Sandlin, K., Miller, R., & Scarfone, K. (2019). *Guide to Attribute Based Access Control (ABAC) Definition and Considerations*. NIST Special Publication 800-162. National Institute of Standards and Technology.

National Institute of Standards and Technology. (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0)*. NIST AI 100-1.

Park, J., & Sandhu, R. (2004). The UCONABC usage control model. *ACM Transactions on Information and System Security, 7*(1), 128–174.

Tsai, S. (2026). *From Inference Creep to Risk Acceleration Pipelines*. SSRN Working Paper 6146686. Zenodo. https://doi.org/10.5281/zenodo.18872172.

Tsai, S. (2026). *Toward Decision Behavior Governance: Governance Existence, Invocation, and Decision Formation*. SSRN Working Paper 6105226. Zenodo. https://doi.org/10.5281/zenodo.18876165.

Tsai, S. (2026). *Runtime Governance vs. Development Governance*. SSRN Working Paper 6341359. Zenodo. https://doi.org/10.5281/zenodo.18876913.

Tsai, S. (2026). *An Effect of Traceability Collapse in GenAI-Assisted SDLCs*. SSRN Working Paper 6348599. Zenodo. https://doi.org/10.5281/zenodo.18872540.

Tsai, S. (2026). *Anchor Architecture*. engrXiv. https://doi.org/10.31224/6580. Zenodo. https://doi.org/10.5281/zenodo.18856781.

Tsai, S. (2026). *Boundary as an Execution-Time Primitive for AI-Assisted Software Development Governance*. engrXiv. https://doi.org/10.31224/6583. Zenodo. https://doi.org/10.5281/zenodo.18883242.

Tsai, S. (2026). *Viewpoint-Structured Specification: A Framework for Structuring Intent into Traceable Specifications as the Basis for AI-Assisted Code Generation*. engrXiv. https://doi.org/10.31224/6612. Zenodo. https://doi.org/10.5281/zenodo.18930951.

Tsai, S. (2026). *Decision Analysis: Effect-Oriented Structural Scope Audit for AI-Assisted Software Development*. engrXiv. https://doi.org/10.31224/6616. Zenodo. https://doi.org/10.5281/zenodo.18934765.

Tsai, S. (2026). *Behavior Rule Architecture: Rule-Based Governance of AI System Behavior*. engrXiv. https://doi.org/10.31224/6681. Zenodo. https://doi.org/10.5281/zenodo.19174636.

Tsai, S. (2026). *Decision Risk: A Structural Governance Framework for AI-Assisted Software Development*. SSRN Working Paper 6655398. Zenodo. https://doi.org/10.5281/zenodo.19025533.

Tsai, S. (2026). *Structural Degradation: From Stateless Generation to Layered Software Decay in AI-Generated Code*. SSRN Working Paper 6655438. Zenodo. https://doi.org/10.5281/zenodo.19043086.

Tsai, S. (2026). *Beyond RAG: Knowledge Evolution as the Next Layer of Enterprise AI*. SSRN Working Paper 6972221.

Tsai, S. (2026). *Beyond HITL: Continuation Readiness as a Governance Requirement for Enterprise AI Workflows*. SSRN Working Paper 7252878. Zenodo. https://doi.org/10.5281/zenodo.21856291.
