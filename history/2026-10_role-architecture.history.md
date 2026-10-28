# Role Architecture — Version History

This document records the conceptual development of the paper
**“Role Architecture.”**

The paper begins from a specific engineering problem: a Role is often retained
only as an abstract name, job title, workflow label, access-control group, or
prompt persona. When that Role is reused across models, workflows, sessions,
or organizational contexts, its meaning must be reconstructed. Its viewpoint,
responsibilities, authority, applicable Scope, and work definition can
therefore change while the Role name remains unchanged.

Role Architecture addresses this problem by treating a Role as an explicit,
versioned, reusable engineering structure rather than an abstract label.

The stages below preserve the paper's conceptual development. Later
refinements may narrow, extend, or replace parts of the initial model without
retroactively rewriting the earlier formulation.

---

## v0.1 — From Abstract Role Labels to Engineering Structure

**Status:** Conceptual Draft

### Purpose

- Identify why an abstract Role name is insufficient for repeated use across
  AI models, workflows, and execution contexts.
- Externalize the governance meaning that would otherwise need to be inferred
  whenever a Role is instantiated.
- Establish Role Architecture as an engineering structure for preserving Role
  meaning across reuse.

### Core Problem

A stable Role name does not guarantee stable Role meaning.

The same label may be interpreted differently by different models, prompts,
workflow stages, orchestration systems, or human participants. Repeated use can
silently change:

- the viewpoint from which the Role acts;
- the responsibilities assigned to it;
- the authority it may exercise;
- the Scope within which it applies;
- the work it is expected to perform;
- the evidence it requires and produces;
- and the conditions under which it must stop or escalate.

This condition is provisionally described as **Role Drift**. Responsibility
and authority may drift even when the Role label remains unchanged.

### Initial Thesis

> A Role should not exist only as an abstract noun. It should be represented
> as an explicit, reusable, and versioned engineering structure whose meaning
> can persist across models, workflows, and repeated execution.

### Initial Role Structure

The first draft treats a Role as a structured configuration containing, at
minimum:

- Description;
- Viewpoints;
- Responsibilities;
- Authority;
- Applicable Scope;
- Work Definition;
- Constraints;
- Inputs;
- Outputs;
- interaction rules;
- escalation conditions;
- and evidence requirements.

The element list is provisional. Later versions must determine which elements
belong to the core Role definition, which belong to contextual Role State, and
which should be represented as relations or execution evidence.

### Key Distinctions

- **Actor is not Role.** A human, AI agent, team, or service may occupy a Role,
  but actor identity does not define the Role's governance meaning.
- **Role label is not Role structure.** A title or persona may identify a Role
  informally without making its viewpoint, authority, Scope, or work explicit.
- **Permission is not responsibility.** Ability to perform an operation does
  not establish responsibility for the resulting decision or effect.
- **Viewpoint is not authority.** Instructing an actor to reason from a
  professional perspective does not grant institutional standing.
- **Role Definition is not Role State.** A reusable definition must be bound to
  an actor, workflow stage, time, policy, evidence, and active Scope before it
  becomes an executable Role State.

### Preliminary Architecture

The initial architecture contains:

- reusable Role Definitions;
- contextual Role States;
- typed relations among Roles;
- Work Junction and transfer contracts;
- constraints such as separation of duties;
- and evidence showing how Roles were instantiated and enacted.

Five preliminary validity conditions are proposed:

1. Identity Validity;
2. Responsibility Validity;
3. Authority Validity;
4. Capacity Validity; and
5. Continuity Validity.

### Relationship to Earlier Work

This paper develops the Role State construct introduced in **Continuation
Readiness**. That paper uses Role State to determine whether a receiving actor
can continue transferred work at a Work Junction. Role Architecture moves
upstream: it asks how the Role itself must be engineered so its governance
meaning does not need to be reconstructed whenever it is reused.

The paper also composes with:

- **Scope as a Governance Primitive**, which supplies the governed region to
  which Role responsibility and authority apply;
- **Viewpoint-Structured Specification**, which distinguishes interpretive
  viewpoint from institutional Role;
- **Behavior Rule Architecture**, which supplies explicit behavioral policies
  and constraints; and
- **Engineering Determinacy**, which supports the principle that an established
  Role meaning should not repeatedly return to probabilistic inference.

### Deliberate Non-Goals

- No claim that organizational roles can be reduced completely to a static
  schema.
- No claim that Role Architecture replaces RBAC, ABAC, workflow notation,
  organizational charts, or responsibility matrices.
- No assumption that assigning a human actor makes a Role governed.
- No assumption that assigning separate AI agents establishes independence or
  separation of duties.
- No complete formal language or executable conformance engine in this stage.

### Open Questions for v0.2

- What is the minimum complete Role Definition?
- Which elements are intrinsic to a Role, and which belong to Role State?
- How should viewpoint enumeration be represented and bounded?
- How should responsibility, authority, permission, and capability be related
  without conflating them?
- How should Role equivalence and compatibility be tested across models and
  workflows?
- What observable changes constitute Role Drift?
- How should Role versions and migrations be governed?
- Which existing role, workflow, access-control, responsibility-modeling, and
  human–AI teaming theories provide direct prior art?

### Historical Significance

Version 0.1 establishes the paper's central transition:

> **Role as abstract label → Role as persistent engineering structure**

It also identifies cross-model, cross-workflow, and repeated-use Role Drift as
the primary problem the architecture is intended to control.

---

## v0.2 — Persistent Role Engineering and Role Drift

**Status:** Thesis Refocusing

### Purpose

- Refocus the paper from the general governance of workflow participation to
  the engineering persistence of Role meaning.
- Make cross-model, cross-workflow, and repeated-use Role Drift the primary
  problem rather than a secondary execution failure.
- Specify the content that must persist when a Role is reused.

### Title Adjustment

The working title is expanded to:

> **Role Architecture: Engineering Persistent Roles to Prevent Responsibility
> and Authority Drift Across AI Models and Workflows**

The new title states the architectural object, engineering objective, target
failure, and reuse contexts directly.

### Thesis Adjustment

The v0.1 manuscript primarily framed Role Architecture as the structure that
makes human and AI participation governable across an enterprise workflow.
That framing remains valid but is now treated as a downstream consequence.

Version 0.2 moves the argument upstream:

> An organization cannot preserve Role accountability if it preserves only
> Role names. The semantic and governance content of a Role must become a
> persistent engineering object that can be inspected, bound, compared,
> versioned, and reused across models and workflows.

### Role Definition Expansion

The Role Definition is expanded to make its engineering content explicit:

`Role Definition = {Identity, Version, Description, Viewpoints,
Responsibilities, Authority, Applicable Scope, Work Definition,
Required Capabilities, Input Contract, Output Contract, Constraints,
Interaction Rules, Escalation Conditions, Evidence Requirements}`

The revision gives particular emphasis to the elements that an abstract Role
name does not preserve:

- **Description** states the organizational purpose of the Role.
- **Viewpoints** enumerate the perspectives the Role must or may apply.
- **Responsibilities** state what the Role must answer for.
- **Authority** states what the Role may decide, approve, change, reject, or
  cause.
- **Applicable Scope** bounds the governed region within which the Role has
  meaning.
- **Work Definition** states the activities and decision behaviors expected of
  the Role.

### Definition–State Separation

Version 0.2 strengthens the distinction among:

- **Actor** — the human, AI agent, team, or service performing action;
- **Role Definition** — the persistent and reusable meaning of the Role; and
- **Role State** — the contextual instantiation created by binding a Role
  Definition to a particular Actor, model, workflow, stage, policy set, and
  time.

This separation prevents a model prompt or workflow-local configuration from
becoming the only authoritative definition of a Role.

### Binding and Explicit Adaptation

Role reuse is introduced as a binding operation:

`Role State = Bind(Role Definition Version, Actor, Context, Overrides)`

Contextual adaptation is permitted, but it must be explicit, attributable, and
reviewable. Silent expansion, replacement, or omission of Role elements is not
adaptation; it is drift.

### Role Fidelity

Version 0.2 introduces **Role Fidelity** as the degree to which an instantiated
Role State preserves the Role Definition's declared:

- Viewpoints;
- Responsibilities;
- Authority boundaries;
- Applicable Scope;
- Work Definition;
- Constraints;
- and interaction obligations.

The concept remains preliminary and does not yet have a quantitative measure.

### Role Drift Becomes the Primary Failure

Role Drift is refined as divergence between an effective Role and its
identified Role Definition without an explicit, attributable, and versioned
change.

The draft distinguishes:

- Viewpoint Drift;
- Responsibility Drift;
- Authority Drift;
- Scope Drift;
- Work Drift;
- Interaction Drift; and
- Evidence Drift.

Drift can occur across models, workflows, stages, executions, organizations,
teams, and Role versions even when the same label or prompt is retained.

### Architectural Model Adjustment

The provisional architecture changes from:

`RA = (D, R, J, K, E)`

to:

`RA = (D, V, B, R, J, K, E)`

where `V` adds Role version and lineage structure, and `B` adds bindings,
adaptations, and explicit overrides.

### New Research Propositions

Two propositions are added:

- cross-model reuse requires structural identity rather than repeated labels or
  prompts; and
- explicit, versioned adaptation distinguishes governed Role evolution from
  Role Drift.

### Conceptual Consequence

Version 0.2 changes the paper's center of gravity:

> **Governable participation is an effect of persistent Role engineering; it
> is no longer the primary definition of Role Architecture.**

The workflow case, validity conditions, Role relations, and governance evidence
remain, but they now demonstrate whether persistent Role meaning survives
instantiation and reuse.

---

## v0.3 — Role Drift as the Primary Architecture Problem

**Status:** Structural Refactoring

### Review Basis

Version 0.3 responds to the structural review recorded in
`manuscripts/2026-10_role-architecture_review.md`.

The review identified two competing argument lines in v0.2:

- Role Drift across models, workflows, and repeated use; and
- Role Validity within an individual workflow execution.

Version 0.3 makes Role Drift the sole primary thesis. Role Validity is retained
only as a set of fidelity checks used to determine whether a Role State remains
attributable to its persistent Role Definition.

### Title Refinement

The subtitle changes from:

> Engineering Persistent Roles to Prevent Responsibility and Authority Drift
> Across AI Models and Workflows

to:

> **Persistent Role Definitions Against Role Drift Across AI Models and
> Workflows**

This avoids narrowing drift to Responsibility and Authority when the model also
identifies Viewpoint, Decision Right, Scope, Work, Interaction, and Evidence
dimensions.

### Governing Principle

The thesis is restated through Engineering Determinacy:

> **Once role meaning has been explicitly established, it should not change
> merely because the model, workflow, or execution consuming it changes.**

This principle replaces governable participation as the paper's organizing
claim. Governable participation remains a consequence of persistent Role
meaning.

### Problem Definition: Repeated Reconstruction

Version 0.3 distinguishes:

- role specification incompleteness;
- role reconstruction at the point of use; and
- Role Drift as unversioned divergence from an identified Role Definition.

Existing representations are treated as partial rather than deficient:

- job titles preserve organizational identity;
- RBAC preserves permissions and access constraints;
- workflow lanes preserve activity assignment;
- prompt personas shape behavioral tendency;
- RACI preserves responsibility relationships; and
- agent capability cards support discovery and capability declaration.

Role Drift becomes possible when the remaining dimensions are reconstructed by
each model or workflow rather than consumed from persistent structure.

### Prior-Work Positioning

The paper now addresses structured-role prior art directly.

- **Gaia** already represents responsibilities, permissions, activities, and
  interaction protocols.
- **MOISE+** already combines structural, functional, and deontic organization
  specifications.
- **OperA** already represents objectives, norms, rights, interactions, and
  role-enacting agreements.
- **NIST RBAC** already includes role hierarchy and static and dynamic
  separation of duties.
- **Role engineering** already addresses the definition of RBAC roles,
  permissions, constraints, and hierarchies.
- **A2A Agent Cards and agent frameworks** already externalize agent identity,
  descriptions, capabilities, skills, goals, and persona-like fields.

The novelty claim is consequently narrowed. The paper does not claim the
invention of structured Roles or their individual elements. Its proposed
contribution is the Definition–Binding–Enactment architecture for preserving
and comparing established Role meaning under probabilistic reuse.

The keyword **Role Engineering** is removed because it has an established RBAC
meaning.

### Four-Layer Role Definition

The flat element list is replaced by four layers:

1. **L1 — Identity:** Identity, Version, Description.
2. **L2 — Semantic Core:** Viewpoints, Work Definition, Responsibilities.
3. **L3 — Governance Boundary:** Bound Rule Set, Decision Right, Visible Scope,
   Artifact Scope, Required Capabilities.
4. **L4 — Interface and Interaction:** Input Contract, Output Contract,
   Interaction Rules, Escalation Conditions, Evidence Requirements.

Minimum completeness requires L1, L2, and L3. L4 becomes mandatory when the
Role participates in governed workflow composition or transfer.

### Canonical Terminology Alignment

Several v0.2 terms are revised to align with earlier papers.

#### Authority and Decision Right

Authority now retains the Behavior Rule Architecture meaning:

`Authority = Policy (MUST) + Constraint (MUST NOT)`

**Decision Right** is introduced for what a Role may decide, approve, reject,
accept, or cause. This removes the earlier conflation of normative Authority
with permission or institutional authorization.

#### Scope

Applicable Scope is divided into:

- **Visible Scope**, governing what the Role may observe or use as evidence;
  and
- **Artifact Scope**, governing what the Role may modify.

The preliminary Role Behavior Space is expressed as:

`Behavior Space = Artifact Scope × Authority`

#### Decision Vacancy and Over Decision

Responsibility Vacancy is no longer presented as a new failure category. It is
treated as a Role Architecture cause of **DR-V Decision Vacancy**.

Action beyond Decision Right, including the caching-strategy example, is
explicitly connected to **DR-O Over Decision**.

#### Role State

The Continuation Readiness definition remains canonical:

`Role State = {actor, viewpoint, policy, scope, authority, evidence-access,
expected-output}`

Role Architecture supplies its persistent Definition source and adds binding
metadata for cross-context comparison rather than replacing the construct.

### Binding Invariants

Binding remains:

`Role State = Bind(Role Definition Version, Actor, Context, Explicit Overrides)`

Version 0.3 makes adaptation rules dimension-specific:

- Visible Scope, Artifact Scope, and Decision Right may only remain equal or
  narrow during ordinary binding;
- prohibitive Constraints may only remain equal or strengthen;
- required Viewpoints cannot be omitted;
- Work may specialize only within the declared definition;
- Actor capability must satisfy Required Capabilities; and
- Responsibility cannot be removed unless another Role explicitly accepts it.

The Responsibility invariant is a central refinement. Narrowing Scope can be a
safe restriction; narrowing Responsibility without simultaneous acceptance
creates a role-layer cause of Decision Vacancy.

### Role Drift Operationalization

Drift is reorganized as a two-axis model.

#### Locus Axis

- **Definition Drift** — content changes under the same Role identifier and
  version.
- **Binding Drift** — instantiation introduces undeclared expansion,
  replacement, or omission.
- **Enactment Drift** — observed behavior departs from the active Role State.

#### Dimension Axis

- Viewpoint;
- Responsibility;
- Authority;
- Decision Right;
- Scope;
- Work;
- Interaction; and
- Evidence.

Cross-model, cross-workflow, cross-stage, and repeated-use conditions are now
treated as triggers or contexts, not drift types.

### Role Fidelity Becomes Categorical

Role Fidelity is changed from an undefined degree to a structural conformance
result. A Role State passes only when every required Definition element is
preserved or changed through a permitted, explicit, and evidenced binding.

The possible results are:

- pass;
- fail; or
- unresolved because evidence is insufficient.

No compensating aggregate score is proposed.

### Validity Conditions Repositioned

Identity, Responsibility, Authority, Capacity, and Continuity are retained but
rewritten as fidelity checks against a Role Definition. They no longer form a
parallel accountability theory.

### Design-Time and Run-Time Separation

The v0.2 tuple mixing definitions and executions is removed from the main
model.

- **Design-time Role Architecture** contains Role Definitions, version lineage,
  typed relations, contracts, and binding constraints.
- **Run-time Role Architecture** contains Actor bindings, Role States, realized
  Work Junctions, explicit overrides, and evidence.

Role relations are regrouped into:

- **flow** relations;
- **governance** relations; and
- **constraint** relations.

### Failure-Mode Reorganization

Failure modes are reorganized by locus:

- Definition defects;
- Binding defects;
- Enactment Drift; and
- Accountability Laundering as a derived consequence.

Role Collision explicitly acknowledges static and dynamic separation of duties
as established RBAC mechanisms.

### Cross-Model Illustrative Case

The primary example now follows **Verification Role v1.2** across two model
bindings.

Model B begins emitting a production-release recommendation even though the
Role Definition permits only verification classification. The failure is
classified as Enactment–Decision-Right Drift and Interaction Drift. Because
both Role States resolve to v1.2, the output can be compared with its Output
Contract and Decision Right.

The example includes a counterfactual: if the Role existed only through the
prompt *You are a reviewer*, no persistent comparison target would exist and
the drift could appear to be ordinary helpful variation.

### Evidence Reorganization

Role Evidence Records are divided according to their detection purpose:

- Definition Evidence;
- Binding Evidence; and
- Enactment Evidence.

This connects each evidence field to a drift locus instead of presenting one
undifferentiated audit list.

### Proposition Consolidation

The previous nine propositions are replaced by six propositions centered on:

- label continuity versus fidelity;
- structural identity for cross-model reuse;
- the need for a persistent comparison target;
- simultaneous acceptance when Responsibility is reduced;
- explicit evolution versus implicit drift; and
- independence of drift locus and dimension.

### Structural Outcome

Version 0.3 completes the main transition begun in v0.2:

> **Role Architecture is no longer presented primarily as a workflow
> accountability framework. It is presented as an architecture for preserving
> established Role meaning and detecting its drift under probabilistic,
> cross-context reuse.**

---

## v0.4 — Conformance Tightening

**Status:** Model Precision Review

### Review Basis

Version 0.4 applies the second review block recorded under **v0.4 — 修訂筆記**
in `manuscripts/2026-10_role-architecture_review.md`.

The v0.4 review substantially repeats the structural recommendations that
produced v0.3. The manuscript therefore does not undergo another thesis or
chapter reorganization. Instead, v0.4 audits v0.3 against those recommendations
and tightens the remaining under-specified rules.

### Abstract and Problem Qualification

The Abstract now identifies the governing principle explicitly as an
application of Engineering Determinacy.

The Introduction also narrows the deterministic-versus-probabilistic contrast.
It no longer implies that human interpretation cannot vary. The revised claim
is that probabilistic, context-conditioned enactment makes a stable Role label
an especially weak proxy for stable Role meaning.

### Prior-Work Comparison Matrix

The prose discussion of prior work is replaced with an explicit comparison
covering:

- Gaia;
- MOISE+;
- OperA / OMNI;
- NIST RBAC and established role engineering; and
- A2A Agent Cards and agent configurations.

For each, the manuscript now separates mechanisms already provided from the
architectural responsibility claimed here. Structured roles, separation of
duties, permissions, protocols, objectives, norms, and capability descriptions
remain acknowledged prior art. The retained contribution is the use of a Role
Definition as a persistent comparison target across probabilistic bindings and
enactments.

### L4 Completeness Rule

Version 0.3 described the Interface and Interaction layer as context-dependent.
Version 0.4 makes the applicability rule explicit:

- any Role that exchanges work, delegates, reviews, authorizes, escalates, or
  produces reusable output must declare the applicable L4 elements; and
- an L4 field may be omitted only when it is inapplicable and that
  inapplicability is explicit.

This prevents `optional` from becoming an unexamined absence.

### Binding Artifacts Are Not Authoritative Definitions

The binding section now identifies prompts, system instructions, tool policies,
access configurations, workflow nodes, and output schemas as possible generated
artifacts of a binding. None supersedes the persistent Role Definition when a
conflict exists.

### Binding Decision Outcomes

The binding invariants now lead to four explicit outcomes:

1. **Accept**;
2. **Accept with explicit transfer**;
3. **Require new Definition version**; or
4. **Reject**.

This converts the invariants from descriptive guidance into a preliminary
decision procedure.

An explicit override must now record:

- affected element;
- previous and bound values;
- change basis;
- approving Decision Right;
- receiving Role where applicable; and
- duration.

An unrecorded difference is treated as a Binding Drift candidate rather than an
override.

### Responsibility Transfer Precision

The v0.3 principle that Responsibility cannot simply narrow is retained.
Version 0.4 connects it to the binding decision outcomes: a reduction is valid
only through **Accept with explicit transfer**, with evidence that an identified
receiving Role accepted the Responsibility.

### Role Fidelity Result Semantics

Role Fidelity remains categorical:

- pass;
- fail; or
- unresolved.

Version 0.4 clarifies that `unresolved` is not partial fidelity and cannot be
treated as approval.

The Identity check timing is corrected from `before binding` to `during
binding and execution reconstruction`, because a Role State does not yet exist
before binding.

### Relation-Level Separation

The Role relation table now separates:

- Definition-level declarations; and
- State-level realizations.

Flow, governance, and constraint relations therefore state both what the
design-time architecture permits or requires and what evidence must exist when
a concrete Role State enacts the relation.

### Evidence Purpose Tightening

Definition, Binding, and Enactment Evidence are retained, but each is now tied
to a more precise conformance purpose:

- resolving the comparison target and detecting unversioned Definition change;
- testing binding invariants and detecting undeclared adaptation; and
- comparing observed behavior and decision effects with the active Role State.

Every conformance finding must identify both its drift locus and affected
dimension. A generic `role mismatch` result is insufficient.

### Historical Significance

Version 0.4 does not change the thesis established by v0.3. It changes the
model from a structurally coherent proposal into a more operationally
checkable one by clarifying completeness, binding outcomes, override evidence,
relation realization, and conformance result semantics.

---

## v0.5 — Role Inference Boundary and Extensible Role Structure

**Status:** Conceptual Reframing

### Role Inference Boundary

Version 0.5 distinguishes the boundary established by Role Architecture from
the boundary enforced during a task:

> **Role Definition → Role Inference Boundary → Role State → Task Execution Boundary**

A Role Definition constrains how a model may interpret and complete Role
meaning. It does not independently determine every object the Actor may
observe or modify during a particular execution. Task-specific Scope,
constraints, runtime context, and enforcement remain downstream concerns.

This distinction prevents Role Architecture from claiming that a Role label
or Definition is itself a complete execution boundary. Its primary purpose is
to prevent context from silently adding viewpoints, responsibilities,
Authority, Decision Rights, Scope, or Work to the Role being instantiated.

### Stable Core and Extension Sections

The prior flat and four-layer formulations are generalized into a stable core
plus schema-governed extensions. Scope, Work, Evidence, Interaction, and
Capability structures can be referenced and versioned rather than frozen into
one universal field list. An unresolved required extension does not imply an
unrestricted value and cannot be completed through unrecorded model inference.

### Specialization, Composition, and Sharing

Version 0.5 adds explicit rules for Role specialization, composition,
binding-time override, and Role Library reuse. Substitutability is checked per
affected element; specialization cannot automatically expand Decision Right,
remove Responsibility, relax constraints, or widen Scope. Authority references
an admitted BRA Application Ruleset rather than creating a second rule
composition authority.

The Role Library becomes a registry for Definition identity, versions,
extensions, dependencies, compatibility metadata, and parameterized templates.
Cross-organizational localization must occur through declared parameters,
extensions, or binding records rather than divergent copies retaining the same
identifier.

### Historical Significance

Version 0.5 relocates the paper's architectural boundary. Role Drift remains
the principal observable failure, but the positive object being engineered is
now the Role Inference Boundary and its extensible, reusable definition
structure.

---

## v0.6 — Minimal Role Core and Extensible Named Bindings

**Status:** Schema Simplification

### Minimal Required Schema

Version 0.6 reduces the universally required Role Definition schema to four
fields:

- `id`;
- `description`;
- `version`; and
- `status`.

This follows the extensibility principle used by the Behavior Rule schema: a
small interoperable core identifies the governed object, while domain and
governance content is supplied through explicit extensions. The change
replaces the v0.4 claim that semantic and governance layers are universally
required for minimum schema completeness.

Minimal schema validity is explicitly separated from bindable or executable
completeness. A four-field Definition is resolvable but cannot be treated as
unrestricted or execution-ready. The applicable binding profile determines
which named bindings must be resolved, restricted, or escalated before use.

### Predefined and Custom Binding Types

The paper now predefines six interoperable binding types:

- `viewpoints`;
- `responsibilities`;
- `authority`;
- `work`;
- `scope`; and
- `skills`.

Organizations may register additional types such as `risk_profile`,
`data_classification`, or `regulatory_scope`. Each type carries its own schema,
version, source, applicability, and compatibility rules instead of inheriting
one uniform adaptation rule.

### Skills Binding

The new `skills` binding makes reusable skill or capability units explicit and
versionable. A declared skill is still distinct from Actor capability: binding
must resolve the reference and verify that the Actor supplies the skill or an
accepted local equivalent. Skill upgrades and substitutions therefore become
auditable changes rather than prompt-local assumptions.

### Examples and Conformance Updates

The manuscript adds concrete uses for viewpoint bindings in chat,
responsibility and Authority bindings in agent-governance audit, and skill
bindings in reusable role packages. The illustrative Verification Role now
includes its minimal core and skills. Pre-binding conformance checks lifecycle
status, applicable binding profiles, named binding resolution, skill capacity,
and type-specific override invariants.

### Historical Significance

Version 0.6 preserves the Role Inference Boundary thesis while removing a
closed completeness model. The architectural transition is:

> **fixed universal Role field set → minimal identity core + extensible,
> schema-governed named bindings**

This makes Role Definitions easier to share across domains without allowing
missing governance content to acquire permissive semantics.
