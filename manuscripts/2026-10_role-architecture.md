# Role Architecture
> Persistent Role Definitions Against Role Drift Across AI Models and Workflows

**Author:** Spark Tsai
**ORCID:** https://orcid.org/0009-0006-8847-4703
**Email:** spark.tsai@gmail.com

---

## Abstract

Enterprise AI systems increasingly reuse roles across language models, agent configurations, workflow stages, and repeated executions. Yet a role is commonly preserved only as an abstract label—*architect*, *reviewer*, *analyst*, *validator*—or as a prompt persona, workflow lane, access-control group, or responsibility category. The label persists, while the meaning needed to enact it does not. Each consuming model or workflow must reconstruct what the role is for, which viewpoints it applies, what work it performs, which responsibilities it carries, what it may decide, and where its applicability ends. Under probabilistic model execution, the same label can therefore produce materially different Role States without an explicit role change.

This paper defines that condition as **Role Drift** and proposes **Role Architecture** as an engineering response. Applying Engineering Determinacy, it adopts the principle that once role meaning has been explicitly established, it should not change merely because the model, workflow, or execution consuming it changes. Role Architecture externalizes that meaning as a persistent, versioned **Role Definition**, separates the definition from both the Actor and its contextual **Role State**, and governs reuse through explicit, extensible bindings and structural fidelity checks. The schema requires only `id`, `description`, `version`, and `status`; viewpoints, responsibilities, authority, work, scope, skills, and domain-specific structures are named binding types rather than a closed universal field list. Drift is made observable along two axes: its locus—Definition, Binding, or Enactment—and its affected dimension, such as Viewpoint, Responsibility, Decision Right, Scope, Work, Skill, Interaction, or Evidence.

The contribution is not the invention of structured roles, permissions, organizational relations, or separation of duties. Those mechanisms have substantial prior art in role-based access control and multi-agent organization models. The contribution is their use under a different architectural responsibility: preserving established role meaning across probabilistic models and heterogeneous workflows, distinguishing versioned evolution from implicit drift, and retaining a comparison basis against which drift can be detected. An illustrative cross-model verification case shows how one validator begins issuing release recommendations outside its defined Decision Right, while an identical role label provides no basis for detecting the change.

**Keywords:** Role Architecture; Role Inference Boundary; Role Drift; Persistent Role Definition; Extensible Binding; Skills; Enterprise AI Governance; Agentic Workflow; Role State; Engineering Determinacy

---

# 1. Introduction

An enterprise defines a *Verification Role* for AI-assisted software delivery. In one repository the role is instantiated through Model A; in another it is instantiated through Model B. Both agents receive a prompt describing them as reviewers. Initially, both check implementation evidence and report findings. After repeated use, Model B begins adding the conclusion *recommended for production release*. No workflow configuration has formally assigned release authority to the role. No role identifier has changed. The output is plausible, helpful, and operationally convenient.

The role label remains the same. The role meaning has changed.

This paper addresses that separation between **label continuity** and **meaning continuity**. A role used by an AI-enabled workflow may be represented through a title, prompt, permission group, process lane, or responsibility code. Each representation can preserve part of the role. None necessarily preserves the complete interpretation required to enact it. When the missing meaning is supplied locally by a model, prompt author, workflow designer, or receiving actor, role reuse becomes repeated role reconstruction.

Repeated reconstruction is especially consequential under large language models. A conventionally programmed component can be incomplete yet still execute a fixed interpretation; a human may rely on organizational convention, training, and professional formation, though human interpretation can also vary. An LLM enactment is generated from the current context. Different models, prompt arrangements, retrieved materials, and conversation histories may therefore produce different enactments of the same role label. The claim is not that only LLMs can drift, but that probabilistic reconstruction makes label continuity an especially weak proxy for meaning continuity.

The paper applies Engineering Determinacy through one governing principle:

> **Once role meaning has been explicitly established, it should not change merely because the model, workflow, or execution consuming it changes.**

Role Architecture establishes a **Role Inference Boundary**, not a complete Task Execution Boundary. The former constrains how a model may interpret and instantiate Role meaning; the latter constrains what a particular Actor may observe, modify, or affect during one task. Their dependency is:

> **Role Definition → Role Inference Boundary → Role State → Task Execution Boundary**

The proposed architectural object is a persistent **Role Definition** with a minimal identity core and extensible named bindings. Its required core makes the role resolvable and lifecycle-aware; bindings may make viewpoints, work, responsibilities, Authority, Decision Rights, Scopes, skills, interfaces, interaction rules, escalation conditions, and evidence requirements explicit. A human or AI Actor does not become the role merely by receiving its name. The Role Definition must be bound to the Actor and context to form a **Role State**, and every applicable binding must preserve its declared invariants.

The research question is:

> **How can an established role meaning be represented, bound, reused, and examined so that changes across AI models, workflows, and executions become explicit evolution rather than implicit drift?**

This paper makes four contributions.

First, it identifies **Role Drift** as divergence from an identified Role Definition occurring at one of three loci: the Definition, its Binding, or its Enactment. Second, it proposes a minimal Role Definition core plus schema-governed, extensible bindings, avoiding a closed universal role schema. Third, it introduces type-specific binding invariants: some dimensions may only narrow, prohibitive rules may only strengthen, while Responsibility cannot be removed unless another Role explicitly accepts it. Fourth, it defines structural Role Fidelity as a categorical comparison and demonstrates how version, binding, and execution evidence provide a basis for detecting drift.

The novelty claim is deliberately bounded. Gaia, MOISE+, OperA, RBAC, role engineering, and contemporary agent specifications already represent roles, permissions, objectives, activities, protocols, norms, capabilities, or constraints in substantial ways [1–8]. This paper does not claim otherwise. Its contribution concerns the persistence, binding, and drift control of established role meaning when probabilistic AI systems repeatedly instantiate roles across heterogeneous execution contexts.

---

# 2. Why Role Meaning Drifts

## 2.1 Existing Representations Preserve Partial Role Meaning

Common role representations answer different questions.

| Representation        | Primarily preserves                             | Meaning commonly left to context                                 |
| --------------------- | ----------------------------------------------- | ---------------------------------------------------------------- |
| Job title             | Organizational identity                         | Stage-specific work, Decision Right, Scope, evidence             |
| RBAC role             | Permissions and access constraints              | Viewpoint, work semantics, responsibility, output meaning        |
| Workflow lane         | Activity assignment                             | Decision legitimacy, interpretation, capability, reuse semantics |
| Prompt persona        | Behavioral tendency and framing                 | Institutional standing, governed Scope, responsibility transfer  |
| RACI category         | Responsibility relationship                     | Work content, evidence, behavioral rules, operational authority  |
| Agent capability card | Discoverable service and capability description | Organizational responsibility, Decision Right, role lineage      |

The problem is not that any one representation is defective. Each is designed for a narrower responsibility. The problem appears when the representation is treated as the complete role and the missing dimensions are reconstructed at use time.

A workflow lane may say that the *Reviewer* performs a review task. A prompt may say *You are a security reviewer*. An access-control system may grant read access to the repository and permission to post a finding. None of these facts alone determines whether the role reviews security design, code correctness, policy compliance, business acceptability, or release readiness. The unrepresented distinction must enter from somewhere else.

## 2.2 Repeated Inference Is the Drift Mechanism

Role Drift is not caused merely by missing documentation. It arises when missing role meaning is repeatedly reconstructed and the reconstruction is allowed to govern action.

A role label enters a model context together with a task, instructions, retrieved material, tool access, prior conversation, and workflow position. The model infers an effective role from this combined context. A later execution may change any of those inputs. A different model may resolve the same ambiguity differently. A workflow may implicitly treat a recommendation as approval. Repeated use can gradually normalize work that the original role never contained.

The important distinction is therefore:

- **role specification incompleteness** means some role meaning has not been externalized;
- **role reconstruction** means an actor supplies that missing meaning for a particular use; and
- **Role Drift** means the resulting effective role diverges from an identified Role Definition without an explicit, attributable, versioned change.

Incompleteness creates the condition. Reconstruction supplies the variation. Uncontrolled reuse converts variation into drift.

## 2.3 Prior Structured-Role Models

Structured roles are not new. The relevant distinction is summarized below.

| Prior approach                                      | Role structure already provided                                                                               | Responsibility retained by Role Architecture                                                                               |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Gaia** [1]                                        | Responsibilities, permissions, activities, and interaction protocols                                          | Preserve an admitted role meaning across probabilistic implementations and compare enactment with that meaning             |
| **MOISE+** [2]                                      | Structural, functional, and deontic organization; roles, missions, obligations, permissions, and prohibitions | Govern Role Definition identity, version, binding, override, and cross-context drift                                       |
| **OperA / OMNI** [3, 4]                             | Objectives, roles, norms, rights, interaction structures, and role-enacting agreements                        | Distinguish versioned evolution from Definition, Binding, and Enactment Drift                                              |
| **NIST RBAC and role engineering** [5, 6]           | Permissions, hierarchies, constraints, and static/dynamic separation of duties                                | Preserve semantic role meaning beyond access control and compare probabilistic enactment                                   |
| **A2A Agent Cards and agent configurations** [7, 8] | Discoverable identity, description, version, skills, capabilities, goal, and persona-like fields              | Add organizational Responsibility, bound Authority, Decision Right, governed Scope, binding invariants, and drift evidence |

Role Architecture builds on, rather than displaces, these precedents. Separation of duties, permission grouping, role objectives, protocols, norms, and structured role descriptions are prior mechanisms, not contributions of this paper. Prior structures can supply elements of a Role Definition. The proposed distinction is the architectural responsibility assigned to those elements: the Role Definition becomes a persistent comparison target across models and workflows, while binding and enactment evidence distinguish explicit evolution from implicit drift.

---

# 3. Role Definition

## 3.1 Actor, Role Definition, and Role State

An **Actor** is an identifiable human, AI agent, team, service, or other participant capable of action. Actor properties include actual capability, available tools, credentials, availability, model configuration, and accessible evidence.

A **Role Definition** is a persistent, versioned specification of established role meaning. It exists independently of the Actor, model, prompt, or workflow that later consumes it.

A **Role State** is the contextual state produced when a specific Role Definition version is bound to an Actor within a workflow stage and governance context.

This paper preserves the canonical Role State dimensions introduced in Continuation Readiness:

> **Role State = {actor, viewpoint, policy, scope, authority, evidence-access, expected-output}**

It does not replace that construct. It explains where the established values used to instantiate it come from and adds binding metadata required for cross-context comparison: Role Definition identity and version, workflow and stage, binding time, Actor capability, Decision Right, explicit overrides, and receiving-role contract.

The separation is essential:

- the **Role Definition** states what the role means;
- the **Actor** supplies actual capacity and performs action; and
- the **Role State** records what the role means in this bounded execution context.

## 3.2 Minimal Core and Extensible Bindings

Role Architecture does not prescribe one closed list of fields for every domain. A Role Definition has a minimal identity core and a set of named bindings:

> **Role Definition = Minimal Core + Binding Declarations + Referenced Bindings**

The schema requires four fields.

| Required field | Architectural responsibility |
| -------------- | ---------------------------- |
| **`id`** | Supplies the stable identifier used by references, version comparison, and drift tracking |
| **`description`** | Provides a human-readable semantic anchor for binding and review |
| **`version`** | Identifies the admitted semantic state consumed by a binding |
| **`status`** | Records lifecycle state such as `draft`, `active`, or `deprecated` |

All other content is expressed through named binding types. The architecture predefines `viewpoints`, `responsibilities`, `authority`, `work`, `scope`, and `skills`, while organizations may add types such as `risk_profile`, `data_classification`, or `regulatory_scope`. Each binding type has an identifier, schema, version, source, applicability rule, and compatibility rule. A Role Definition can therefore remain structurally resolvable without pretending that every role needs the same semantic, governance, or domain fields.

Minimal schema validity is not executable completeness. A role with only the four required fields is identifiable but leaves its enactment boundary unresolved. Before use, the applicable binding profile must declare which binding types are required and resolve them, restrict the Role's use, or escalate the unresolved condition. An absent binding never means unrestricted scope, arbitrary work, implicit authority, or permission to infer missing responsibility.

## 3.3 Identity and Description

Identity must be stable across wording, deployment, and actor changes. Version identifies an accepted state of the Role Definition. Description states the role's organizational purpose; it is not a substitute for the remaining fields.

Role identity should be anchored to a resolvable artifact and version. A prompt string, model name, or workflow node is insufficient because each may change independently of the role. This applies Anchor Architecture at the role-definition level: comparison requires a stable coordinate before semantic analysis begins.

## 3.4 Viewpoints, Work, and Responsibilities

**Viewpoints** enumerate the declared perspectives from which the role interprets its material. A Verification Role might apply security, reliability, and conformance viewpoints. A viewpoint shapes interpretation; it does not grant institutional standing or Decision Right.

**Work Definition** states the activities and decision behaviors expected from the role. It may include analysis, production, comparison, verification, classification, reporting, or transfer. Work answers *what does the role do?*

**Responsibilities** state the outcomes, judgments, or obligations for which the role must answer. Responsibility answers *what must the role ensure or account for?* Work and Responsibility are distinct. A role may perform analysis without being responsible for accepting its conclusion, or execute a change without owning the decision that authorized it.

These binding types commonly carry the semantic content most exposed to probabilistic reconstruction. They are predefined for interoperability, but are not mandatory schema fields for every Role Definition.

## 3.5 Bound Rule Set, Decision Right, and Scope

This paper follows Behavior Rule Architecture in reserving **Authority** for the bound normative rule set:

> **Authority = Policy (MUST) + Constraint (MUST NOT)**

To avoid conflating Authority with permission or institutional authorization, **Decision Right** is introduced separately:

> **Decision Right identifies what the Role may decide, approve, reject, accept, or cause within its declared Scope.**

Scope is also not treated as one undifferentiated region.

- **Visible Scope** identifies what the Role may read, observe, retrieve, or use as evidence.
- **Artifact Scope** identifies what artifacts or states the Role may directly modify.

The Role's preliminary **Behavior Space** is:

> **Behavior Space = Artifact Scope × Authority**

Decision Right then determines which consequential judgments the Role may form or activate over that governed region. A Role may therefore be able to modify an artifact without holding the right to redefine the requirement the artifact implements.

## 3.6 Skills and Actor Capability

The predefined **`skills` binding** identifies versioned skill or capability units explicitly associated with the Role, rather than leaving their availability as a prompt assumption. It may reference a reusable skill package, capability type, tool-mediated procedure, or locally mapped equivalent.

Actual capability still belongs to the Actor and is evaluated when the Role is bound. A declared skill is not proof that a particular Actor can perform it. Binding checks resolve the skill reference, test availability or an accepted equivalent, and record the result. Skill upgrades and local substitutions remain attributable changes instead of silently altering the Role's capability boundary.

## 3.7 Binding Types in Use

The predefined types support different operational settings.

**`viewpoints` in chat.** A PM Role may bind `product strategy`, `user value`, and `feasibility trade-off`. When asked to prioritize features, the model interprets the task through those perspectives rather than silently substituting an engineering or regulatory viewpoint.

**`responsibilities` and `authority` in agent governance.** An Implementation Agent may be responsible for writing code, running tests, and proposing architecture while its Authority contains `MUST NOT merge to production without approval`. Evidence can then distinguish work outside the declared responsibility from conduct that violates a bound rule, without treating the binding as an RBAC permission grant.

**`skills` in reusable role packages.** A Code Reviewer may reference `code-review@2` and `testing-strategy@1`. Binding verifies that the Actor can resolve or validly map those skills; a skill upgrade or organizational substitution is recorded and compatibility-tested rather than absorbed into an unchanged prompt.

---

# 4. Binding and Versioning

## 4.1 Binding

Binding creates a Role State from a particular Role Definition version:

> **Role State = Bind(Role Definition Version, Referenced Bindings, Actor, Context, Explicit Overrides)**

Binding is not textual prompt expansion. It is a governed operation that resolves the persistent definition and its applicable named bindings into a specific model, workflow, stage, policy context, and evidence environment. A prompt, system instruction, tool policy, access configuration, workflow node, and output schema may all be generated implementation artifacts of one binding. None is independently authoritative when it conflicts with the resolved Role Definition. Binding must also reject a non-active lifecycle state unless an explicit governance rule permits its use.

## 4.2 Binding Invariants

Role dimensions do not all adapt in the same direction. The following invariants apply unless a new Role Definition version is admitted.

| Dimension             | Permitted binding behavior                                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Visible Scope         | May remain equal or narrow; expansion requires an explicit binding or Definition version permitted by the type's compatibility rule and applicable Decision Right |
| Artifact Scope        | May remain equal or narrow; expansion requires an explicit binding or Definition version permitted by the type's compatibility rule and applicable Decision Right |
| Decision Right        | May remain equal or narrow; expansion requires a versioned change and approval by a Role already holding the right to grant it |
| Policy (MUST)         | Required policies must be preserved; contextual specialization must not remove or contradict them                         |
| Constraint (MUST NOT) | May remain equal or strengthen; removal requires a new version approved under the applicable Decision Right               |
| Viewpoints            | Required viewpoints cannot be omitted; optional viewpoints may be selected explicitly                                     |
| Work Definition       | May specialize within declared work; expansion requires a versioned change under the binding type's compatibility rule    |
| Responsibilities      | May not be removed unless a named receiving Role accepts them                                                             |
| Skills                | Actor capability must satisfy or validly map each required skill binding; it must not rewrite the declaration             |

The Responsibility rule is intentionally asymmetric. Narrowing Scope or Decision Right can be a safe local restriction. Silently narrowing Responsibility can create a vacancy: the work no longer has an accountable owner. A binding that removes Responsibility is valid only if it simultaneously records a transfer to another Role Definition or Role State whose acceptance is explicit and evidenced. Otherwise the condition is a role-layer cause of DR-V Decision Vacancy.

A binding evaluation therefore has four possible outcomes:

- **Accept** — all required elements are preserved and every override satisfies its invariant;
- **Accept with explicit transfer** — a Responsibility reduction is paired with an evidenced receiving Role;
- **Require new Definition version** — the proposed change expands or replaces established Role meaning rather than specializing it; or
- **Reject** — the binding violates an invariant or lacks the evidence needed to evaluate it.

An override record must identify the affected element, previous value, bound value, change basis, approving Decision Right, receiving Role where applicable, and duration. Without this record, the difference is not an override; it is a Binding Drift candidate.

## 4.3 Versioned Evolution Versus Drift

Role Definitions may evolve. A new regulation may add a viewpoint; organizational restructuring may transfer a Decision Right; a new model capability may change the Work Definition. Role Architecture does not prevent change.

The distinction is whether change is explicit.

- **Governed Role Evolution** creates a new version, records the changed elements and authority basis, evaluates downstream compatibility, and migrates bindings deliberately.
- **Role Drift** changes effective meaning under the same apparent Role identity without an explicit, attributable, versioned transition.

Versioning is therefore not administrative metadata. It separates authorized change from silent reinterpretation.

---

# 5. Role Drift and Fidelity

## 5.1 Drift Loci

Role Drift becomes observable when its locus is specified.

| Locus                | Definition                                                                     | Primary detection point                              |
| -------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------- |
| **Definition Drift** | Core content or referenced binding identity changes under the same Role identifier and version | Definition, dependency, and version comparison       |
| **Binding Drift**    | Instantiation expands, replaces, or omits elements without a declared override | Pre-execution binding conformance                    |
| **Enactment Drift**  | Actual behavior, decisions, outputs, or transfers exceed the Role State        | Execution-time or post-execution evidence comparison |

Cross-model, cross-workflow, cross-stage, and repeated-use conditions are **triggers or contexts**, not drift types. The same cross-model reuse may cause Binding Drift in one case and Enactment Drift in another.

## 5.2 Drift Dimensions

Drift may affect different dimensions:

- **Viewpoint Drift** — a required viewpoint is omitted or an undeclared one governs interpretation;
- **Responsibility Drift** — an obligation is added, removed, or transferred implicitly;
- **Authority Drift** — the bound MUST/MUST NOT rule set is changed or ignored;
- **Decision-Right Drift** — the Role begins making, approving, rejecting, or activating decisions outside its declared right;
- **Scope Drift** — Visible or Artifact Scope silently expands, contracts, or changes meaning;
- **Work Drift** — performed activities expand beyond or depart from the Work Definition;
- **Interaction Drift** — review, challenge, escalation, separation, or receiving-role relations change;
- **Evidence Drift** — the Role relies on or produces a different evidentiary basis while retaining the same standing.
- **Skill Drift** — a declared skill is unavailable, silently substituted, or changed incompatibly while the Role identity remains unchanged.

The two axes form a **locus × dimension matrix**. A changed Output Contract under the same version is Definition–Interaction Drift. Omitting the security viewpoint when instantiating Model B is Binding–Viewpoint Drift. Issuing a release recommendation during execution is Enactment–Decision-Right Drift.

## 5.3 Structural Role Fidelity

**Role Fidelity** is a structural conformance result, not a numerical degree:

> **A Role State has structural fidelity when the minimal core resolves, every applicable binding is resolved, and every change is permitted, explicit, and evidenced under that binding type's rules.**

The result is **pass**, **fail**, or **unresolved** when evidence is insufficient. `Unresolved` is not partial fidelity and must not be treated as approval. This avoids implying that a single score can compensate for a critical mismatch: perfect output formatting cannot offset an unauthorized Decision Right.

## 5.4 Five Fidelity Checks

The earlier validity conditions are retained as checks of Role State fidelity rather than as an independent accountability theory.

| Check              | Question                                                                                                    | Primary time                                |
| ------------------ | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| **Identity**       | Can the proposed or active Role State resolve to one unique Role Definition version?                        | During binding and execution reconstruction |
| **Responsibility** | Do enacted responsibilities match the Definition, and is every reduction accepted by a receiving Role?      | Binding and post-binding                    |
| **Authority**      | Are the bound rule set, Decision Right, Visible Scope, and Artifact Scope within the Definition?            | Binding and execution                       |
| **Capacity**       | Does the Actor's actual capability satisfy or validly map the required `skills` bindings?                    | Binding                                     |
| **Continuity**     | Do outputs and unresolved obligations reach the roles declared by the interaction and escalation contracts? | After execution                             |

These checks do not determine substantive correctness. They determine whether the enacted role remains structurally attributable to the Role Definition it claims to instantiate.

---

# 6. Role Relations and Composition

## 6.1 Relations and Architectural Planes

Roles become an architecture when they can be composed without losing their individual governance meaning. Relations fall into three classes.

| Class          | Definition-level declaration                                                                                       | State-level realization                                                                  |
| -------------- | ------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| **Flow**       | `delegates-to`, `produces-for`, and `continues-from` identify permitted transfer topology and contracts            | A specific Role State delegates, produces, or continues through a realized Work Junction |
| **Governance** | `reviews`, `challenges`, `authorizes`, `accepts`, and `escalates-to` identify standing and required response paths | A specific review, challenge, authorization, acceptance, or escalation is evidenced      |
| **Constraint** | `separates-from` and `incompatible-with` restrict simultaneous or sequential bindings                              | A candidate or active binding is rejected when it violates the declared constraint       |

The relation itself does not erase the Role boundaries it connects. A role that reviews does not thereby authorize. A role that receives an escalation does not automatically accept the originating responsibility. A role that produces an artifact cannot infer that the receiving role accepts every embedded decision.

Role Architecture separates two architectural planes.

**Design-time Role Architecture** contains Role Definitions, their version lineage, typed relations, interface contracts, and binding constraints.

**Run-time Role Architecture** contains Actor bindings, active Role States, realized Work Junctions, explicit overrides, and Role Evidence Records.

The design-time plane supplies the comparison target. The run-time plane supplies the observed instantiation. Drift is detected through differences between them and through unauthorized change within either plane.

## 6.2 Specialization and Substitution

A specialized Role may substitute for its parent only when every parent requirement remains satisfiable and every affected interface remains compatible. Specialization does not grant a general right to override inherited meaning.

- required viewpoints and policies cannot be removed;
- constraints may strengthen but cannot silently relax;
- Responsibility remains with the child unless an explicit composition or binding transfers it and records acceptance;
- Decision Right does not expand merely because the Role is specialized;
- Artifact Scope may narrow, while expansion requires explicit authorization and version treatment;
- Visible Scope expansion requires applicable data authorization and declared parameterization; and
- input and output contracts must remain compatible with parent consumers and receivers.

If composition produces both `MUST X` and `MUST NOT X` under the same condition, the result is unsatisfiable. Constraint-first filtering cannot resolve the contradiction by discarding the positive obligation. The Definition must be rejected or referred to a governance process holding the applicable Decision Right.

## 6.3 Role Library

A **Role Library** is the governed registry for Role Definitions, named binding types, referenced binding instances, lineage, dependencies, and compatibility metadata. Shared units carry identifiers, versions, content identities, and dependency manifests. Consumers pin the Role Definition and material binding or BRA Application Ruleset versions rather than relying on mutable latest-state resolution.

The Role Library does not replace the BRA Rule Library. Authority bindings reference admitted Application Rulesets; they do not recompose atomic Rules under a second authority. Cross-organizational reuse may publish a complete Definition, a parameterized Role template, or an abstract Role. Localization of Scope, Authority, Responsibility, skills, evidence, ontology, or legal context must use declared parameters, registered bindings, or explicit binding records. Copying content, changing it locally, and retaining the same identifier is Definition Drift.

---

# 7. Failure Modes by Locus

## 7.1 Definition Defects

**Decision Vacancy at the role layer.** A necessary decision or responsibility has no defined owner, or a Role Definition allows it to disappear during transfer. This is not a new vacancy category; it is a Role Architecture cause of DR-V Decision Vacancy, including Never Authorized, Lost in Transition, and Implicit Handoff conditions.

**Authority–Responsibility Divergence.** A Role carries responsibility without the Decision Right needed to discharge it, or holds Decision Right without corresponding responsibility.

**Role Collision.** One permissible binding combines duties that must remain separate, such as production and certification. Static and dynamic separation of duties are established RBAC mechanisms [5]; Role Architecture uses those mechanisms and extends the conformance question to probabilistic role enactment.

## 7.2 Binding Defects

**Role Label Substitution.** An Actor receives only a title or persona, and local inference substitutes for binding to a resolvable Role Definition.

**Persona–Standing Confusion.** A professional viewpoint in a prompt is treated as institutional Decision Right.

**Capability-Blind Assignment.** An Actor is bound despite failing or not resolving required skill bindings. The Role Definition may be valid while the resulting Role State is not.

## 7.3 Enactment Drift

Enactment Drift is observed through one or more dimensions in Section 5.2. It includes actions beyond Artifact Scope, decisions beyond Decision Right, omitted required viewpoints, changed work, unsupported evidence, and bypassed escalation or separation relations.

**Orphaned Output** is an interaction or continuity form of Enactment Drift when a Role produces an artifact outside its declared receiving-role contract or leaves an unresolved obligation without a valid successor.

## 7.4 Derived Consequence: Accountability Laundering

Accountability Laundering is a consequence rather than a separate locus. It occurs when a drifted or defective action passes through another Role whose nominal approval makes the action appear authorized, reviewed, or human-owned even though the receiving Role lacked the capacity, evidence, responsibility, or Decision Right to exercise that judgment.

---

# 8. Illustrative Application: Cross-Model Verification Drift

## 8.1 Persistent Definition

An enterprise admits **Verification Role v1.2** with the following abbreviated structure:

- **ID / Version / Status:** `verification-role` / `1.2` / `active`;
- **Description:** independently evaluate whether a candidate software change conforms to its accepted specification and declared technical policies;
- **Viewpoints:** correctness, security, reliability, and policy conformance;
- **Work Definition:** inspect the change and evidence, execute or evaluate required tests, identify findings, and issue a verification result;
- **Responsibility:** provide an evidence-grounded conformance assessment;
- **Authority:** MUST evaluate declared criteria; MUST disclose unresolved findings; MUST NOT certify business acceptance or production readiness;
- **Decision Right:** may classify verification as pass, fail, or unresolved; may not authorize release;
- **Visible Scope:** specification, change set, test results, declared policies, and relevant repository context;
- **Artifact Scope:** verification report only; no modification of production code or release state;
- **Output Contract:** structured findings, evidence references, unresolved issues, and verification classification;
- **Interaction:** produces-for Business Acceptance Role and Release Authorization Role; escalates unresolved policy interpretation;
- **Evidence Requirement:** model identity, prompt binding, tool record, inspected artifact versions, tests, and output.
- **Skills:** `software-verification@1`, `test-evidence-analysis@1`, and an organization-approved policy-conformance mapping.

## 8.2 Two Bindings

Repository X binds v1.2 to **Model A**. Repository Y binds the same definition to **Model B**. Both satisfy the required skill bindings. Their generated prompts differ because tool syntax and repository conventions differ, but each Role State resolves to the same Definition version and preserves the same semantic and governance bindings.

Model A continues to emit the declared verification classification.

Model B, after workflow examples increasingly include deployment discussions, begins appending: *Recommended for production release.* The recommendation is accepted downstream as a release signal.

## 8.3 Detection

The drift is classified as:

- **Locus:** Enactment Drift;
- **Dimension:** Decision-Right Drift and Interaction Drift;
- **Triggering context:** repeated execution under Model B with release-oriented context.

The Role Evidence Record makes the divergence testable. Model B's output contains a decision effect outside the v1.2 Output Contract and beyond the `pass/fail/unresolved` Decision Right. The output also bypasses the Release Authorization Role by supplying a conclusion reserved to it. Model A's output remains conformant.

The comparison does not require proving that Model B's recommendation was technically wrong. It shows that the recommendation was not a valid enactment of Verification Role v1.2.

If the role existed only as the prompt *You are a reviewer*, the organization would have no persistent semantic or governance baseline. The new sentence might appear to be a helpful variation rather than drift. Label continuity would conceal role change.

## 8.4 Secondary Case: Over Decision

An AI Implementation Role receives an ambiguous performance requirement and selects a new caching strategy. Its Artifact Scope permits code modification, but its Decision Right does not include architecture selection. The action is therefore Enactment–Decision-Right Drift and corresponds to DR-O Over Decision. Passing tests do not repair the governance defect: the Actor exercised a decision beyond the bound Role State.

---

# 9. Evidence and Conformance

Role evidence should support the three drift loci rather than exist as an undifferentiated log.

| Evidence group          | Minimum content                                                                                                                 | Drift use                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **Definition Evidence** | Role identifier, version, content hash, lineage, change record, admission basis                                                 | Detect content change without version transition and resolve the comparison target |
| **Binding Evidence**    | Actor and model identity, context, capability check, generated prompt and policy artifacts, explicit overrides, accepting roles | Test binding invariants and detect undeclared expansion, replacement, or omission  |
| **Enactment Evidence**  | inputs, applied rules, accessed Scope, actions, decision effects, outputs, transfers, escalations, unresolved conditions        | Compare observed behavior with the active Role State and detect Enactment Drift    |

Pre-binding conformance resolves `id`, `version`, and `status`, checks the description anchor, determines the binding profile applicable to the intended use, resolves every required named binding, compares Actor capability with required skill bindings, and validates every override against type-specific invariants. Schema validity alone is insufficient evidence that a Role is executable.

Execution-time conformance can enforce deterministic boundaries such as Artifact Scope, tool permission, prohibitive rules, and required escalation. Semantic dimensions such as Viewpoint and Work may require evidence-based post-execution analysis rather than universal runtime enforcement.

Post-execution conformance compares observed actions, outputs, decision effects, evidence use, and junction transitions with the Role State. Conformance must always identify both the drift locus and affected dimension; a generic `role mismatch` finding is insufficient. The result should distinguish:

- **conformant enactment**;
- **non-conformant enactment**;
- **unresolved conformance** because evidence is insufficient; and
- **version mismatch** because the claimed comparison target cannot be resolved.

Role Architecture therefore does not promise that every form of drift is automatically decidable. It requires that established meaning and execution evidence exist in forms that make drift structurally examinable.

---

# 10. Relationship to This Research Program

## 10.1 Engineering Determinacy

Engineering Determinacy supplies the governing principle: established information should not repeatedly return to probabilistic reconstruction. Role Architecture applies that principle to Role meaning. Models may assist in discovering or revising a Role; routine reuse consumes an admitted Definition.

## 10.2 Anchor Architecture

Role identity and version require a resolvable coordinate before comparison. Anchor Architecture supplies the structural principle that identity, state, and time must be anchored before later semantic or governance analysis can be reliable.

## 10.3 Behavior Rule Architecture

Behavior Rule Architecture supplies the canonical Authority construction of Policy (MUST) plus Constraint (MUST NOT). Role Architecture binds that rule set to a Role Definition and separates it from Decision Right.

## 10.4 Scope and Behavior Space

Scope as a Governance Primitive explains why visibility, operation, effect, and responsibility regions cannot be assumed equivalent. Role Architecture uses Visible Scope and Artifact Scope explicitly. Artifact Scope combined with Authority establishes the preliminary Behavior Space against which enactment can be compared.

## 10.5 Decision Analysis and Decision Risk

DR-V and DR-O already describe Decision Vacancy and Over Decision. Role Architecture does not rename them. It identifies role-definition, binding, and enactment conditions that can produce them: unowned Responsibility can lead to DR-V; action beyond Decision Right can produce DR-O.

## 10.6 Continuation Readiness

Continuation Readiness defines Role State and evaluates whether a receiving Role State can continue transferred work. Role Architecture supplies the persistent Definitions from which those states are instantiated and tests whether their meaning remains stable across repeated junctions.

---

# 11. Research Propositions

**P1 — Label continuity does not establish Role Fidelity.** Neither reuse of a Role name nor substitution of a human for an AI Actor guarantees fidelity when the enactment cannot be resolved to a persistent Role Definition.

**P2 — Cross-model Role reuse requires structural identity.** Two model-specific configurations instantiate the same Role only when both resolve to the same Definition version and satisfy its binding invariants.

**P3 — Drift requires a comparison target.** Role Drift cannot be distinguished from ordinary variation when established Role meaning is not externalized and versioned.

**P4 — Responsibility reduction requires simultaneous acceptance.** A binding may not remove Responsibility unless another identified Role explicitly accepts it; otherwise the binding creates a role-layer condition for Decision Vacancy.

**P5 — Explicit change distinguishes evolution from drift.** A difference is governed Role Evolution when it is attributable, versioned, and propagated through affected bindings; an equivalent implicit difference is Role Drift.

**P6 — Drift locus and dimension are independent.** The same dimension can drift in the Definition, Binding, or Enactment, and detection must therefore identify both axes.

---

# 12. Limitations and Research Agenda

This paper is conceptual and does not empirically establish how frequently Role Drift occurs, whether the proposed structure reduces it, or which binding types are necessary across domains. The predefined types may prove incomplete, and domain-specific roles may require additional semantic, legal, temporal, or organizational bindings.

The distinction from prior work also requires disciplined validation. Gaia, MOISE+, OperA, RBAC, role engineering, agent organization theory, normative multi-agent systems, workflow languages, and agent specifications already provide rich role structures. Future work must test whether Definition–Binding–Enactment drift is absent from those mechanisms, merely implicit, or directly representable through extensions. The current novelty claim concerns the architectural responsibility assigned to persistence and comparison under probabilistic reuse, not exclusive ownership of the component mechanisms.

Role Fidelity is presently structural and categorical. The paper does not define a quantitative score, semantic-equivalence algorithm, or complete conformance language. Viewpoint, Work, and Responsibility comparison may themselves require interpretation, creating a recursion problem: AI may be used to detect AI role drift. Deterministic checks should therefore be used where possible, and model-assisted findings should retain uncertainty and supporting evidence.

Further research should develop:

- a machine-readable minimal-core schema and a registry format for named binding types;
- profiles that distinguish schema validity, bindable completeness, and executable completeness;
- formal binding invariants and responsibility-transfer semantics;
- skill-resolution and compatibility rules across organizations;
- compatibility rules for Role Definition versions;
- conformance methods for the locus × dimension drift matrix;
- mappings to RBAC, BPMN, A2A Agent Cards, and agent orchestration frameworks;
- empirical cross-model and longitudinal workflow studies;
- and governance processes for admitting, revising, deprecating, and migrating Role Definitions.

---

# 13. Conclusion

Enterprise AI systems can preserve a Role label while repeatedly reconstructing the Role behind it. Across models, workflows, and executions, that reconstruction can alter Viewpoint, Responsibility, Authority, Decision Right, Scope, Work, Interaction, or Evidence without producing an explicit role change. The result is Role Drift: organizational meaning changes while nominal identity remains stable.

Role Architecture addresses this problem by making established Role meaning a persistent engineering object. A minimal Role Definition core supplies resolvable identity, description, version, and lifecycle status; schema-governed bindings add the semantic, governance, skill, and domain structures required by a particular use. Binding creates a contextual Role State under type-specific invariants. Versioning distinguishes governed evolution from silent reinterpretation. Definition, Binding, and Enactment evidence provide comparison points for a locus × dimension model of drift.

The resulting shift is not from informal roles to structured roles in general; prior work already made that move. It is from **role structure as a design description** to **role meaning as a persistent, reusable, and examinable organizational state under probabilistic execution**.

The governing principle can therefore be stated directly:

> **Once role meaning has been explicitly established, it should not change merely because the model, workflow, or execution consuming it changes.**

---

## AI Assistance Disclosure

This manuscript was developed with AI-assisted drafting, editing, structural review, and literature cross-checking. The author selected the research question, conceptual framing, model definitions, examples, references to include, and final wording, and remains responsible for all claims, citations, analysis, and conclusions.

---

## References

[1] Wooldridge, M., Jennings, N. R., & Kinny, D. (2000). The Gaia methodology for agent-oriented analysis and design. *Autonomous Agents and Multi-Agent Systems, 3*(3), 285–312. https://doi.org/10.1023/A:1010071910869

[2] Hübner, J. F., Sichman, J. S., & Boissier, O. (2002). MOISE+: Towards a structural, functional, and deontic model for MAS organization. In *Proceedings of the First International Joint Conference on Autonomous Agents and Multiagent Systems*, 501–502. https://doi.org/10.1145/544862.544939

[3] Dignum, V. (2004). *A Model for Organizational Interaction: Based on Agents, Founded in Logic*. Utrecht University.

[4] Dignum, V., Vázquez-Salceda, J., & Dignum, F. (2005). Omni: Introducing social structure, norms and ontologies into agent organizations. In R. H. Bordini et al. (Eds.), *Programming Multi-Agent Systems* (LNCS 3346), 181–198. Springer. https://doi.org/10.1007/978-3-540-32260-3_11

[5] Ferraiolo, D. F., Sandhu, R., Gavrila, S., Kuhn, D. R., & Chandramouli, R. (2001). Proposed NIST standard for role-based access control. *ACM Transactions on Information and System Security, 4*(3), 224–274. https://doi.org/10.1145/501978.501980

[6] Coyne, E. J. (1996). Role engineering. In *Proceedings of the First ACM Workshop on Role-Based Access Control*, 15–16. https://doi.org/10.1145/270152.270181

[7] Agent2Agent Protocol Project. (2025). *Agent2Agent Protocol Specification: Agent Card*. https://google-a2a.github.io/A2A/specification/

[8] CrewAI. (2026). *Agents*. https://docs.crewai.com/en/concepts/agents
