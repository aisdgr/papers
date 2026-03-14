# Decision Risk: A Structural Governance Framework for AI-Assisted Software Development
> Interpreting Decision Analysis Outcomes through Observability, Risk Taxonomy, and Governance Mechanisms

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Date:** March 2026  

---

# Abstract

AI-assisted software development accelerates code production but undermines the governance infrastructure that makes development decisions reproducible, attributable, and auditable. When AI agents generate code, the governing conditions—authorized scope, governing rules, and decision reasoning—are rarely preserved as persistent evidence. As a result, code artifacts accumulate while the governance legitimacy of the decisions that produced them remains indeterminate.

This paper introduces Decision Risk, a structural governance framework that addresses this gap through four integrated components. Decision observability defines the evidence conditions under which development decisions can be structurally examined. Decision Analysis classifies observable decisions into five mutually exclusive states based on set-relational conditions among visible scope, artifact scope, and outcome scope. The Decision Risk model interprets these analytical states as governance risks, defining four risk categories, twelve threat types across three families, four manifestation levels, and a severity assessment matrix. The Risk Governance Model translates risk assessments into governance actions through three intervention levels and a PDCA cycle with risk-type-specific strategies.

A case demonstration shows a single development task progressing through three governance stages, producing a measurable risk trajectory from unobservable risk to contained over-scope risk as governance infrastructure matures.

---

## Keywords

AI-assisted software development, Decision analysis, Decision risk, AI governance, Software traceability, Decision observability

---

## JEL Classification

M15 Information Technology Management  
O33 Technological Change  
L86 Information and Internet Services

---

## 1. Introduction

Software development has always been a decision-intensive activity. Every function created, every module restructured, every dependency introduced reflects a development decision—a choice that alters the persistent structure of the system. In traditional development, these decisions are formed by human developers operating within organizational processes: design reviews, specification documents, coding standards, and approval workflows. The decisions may not be individually documented, but they are embedded in a governance infrastructure that makes them, in principle, reproducible and attributable. A reviewer can ask "why was this module restructured?" and the developer can explain the reasoning, point to the governing specification, and identify the approval that authorized the change.

AI-assisted software development disrupts this governance assumption. When an AI agent generates code—creating functions, modifying modules, introducing dependencies—development decisions are produced at a scale and speed that fundamentally alters the evidence landscape. The agent's reasoning is not introspectable. The context it consumed during generation is not automatically preserved. The boundary between what it was authorized to do and what it actually did is rarely recorded. The result is a structural inversion: development decisions multiply while decision evidence diminishes. Code artifacts accumulate in version control, but the governance conditions under which those artifacts were produced—what rules applied, what scope was authorized, what reasoning connected input to output—are lost.

This is not a speculative concern. It is a present structural condition. Every AI-assisted commit that enters a codebase without persistent evidence of its governing context creates what this paper terms **governance debt**: the code exists, but its decision legitimacy is indeterminate. The code may be functionally correct—AI agents frequently produce high-quality output—but functional correctness does not establish governance legitimacy. A module that works perfectly but was created without any traceable authorization, outside any defined scope, and in violation of unstated constraints is both correct and ungoverned simultaneously.

The core problem is that existing governance frameworks assume development decisions are observable—that the conditions, boundaries, and reasoning behind each decision can be recovered when needed. This assumption held when decisions were formed entirely by human developers within institutional processes. It fails when decisions are formed by or with AI agents that operate outside those processes, or within processes that do not capture the evidence required for structural governance.

This paper addresses this governance gap through a structural framework that makes development decisions amenable to governance evaluation. The framework operates as an analytical chain: from evidence conditions through decision classification to risk assessment and governance response. Five specific contributions constitute the chain.

First, the paper defines **decision observability**—the evidence conditions under which a development decision can be structurally examined (Chapter 3). Observability requires persistent condition evidence (what the decision-maker knew and was authorized to do) and decision evidence (what the decision produced and why). Without observability, governance cannot operate.

Second, the paper introduces **Decision Analysis**—a classification method that takes observable evidence as input and produces one of five mutually exclusive decision states as output (Chapter 4). Decision Analysis is governance-neutral: it identifies structural facts (scope exceedance, missing attribution, absent evidence) without prescribing governance responses.

Third, the paper formalizes **Decision Risk**—a risk taxonomy that interprets Decision Analysis states as governance risks (Chapter 5). Four risk categories (Unobservable, Vacancy, Over-Scope, Indeterminate) map directly from analytical states and identify specific governance deficiencies rather than probabilistic predictions.

Fourth, the paper identifies the **structural origins** of Decision Risk through twelve threat types organized in three families—structural threats, temporal threats, and referential threats—and defines four manifestation levels that capture risk progression from latent condition to systemic impact (Sections 5.3–5.6).

Fifth, the paper proposes a **Risk Governance Model** that translates risk assessments into governance actions through three intervention levels and a PDCA cycle with risk-type-specific strategies (Chapter 6).

The framework is demonstrated through a case study (Chapter 7) in which a single development task progresses through three governance stages, producing a measurable trajectory from unobservable risk to contained over-scope risk as governance infrastructure matures.

---

## 2. Problem: Non-Reproducible Development Decisions

Software development decisions differ fundamentally from runtime decisions. Runtime decisions operate within predefined system logic and can typically be reconstructed through execution logs. Development decisions, however, create or modify the system structure itself—introducing new functions, altering modules, or changing architectural relationships.

These development decisions produce persistent artifacts: new functions, modified modules, altered test suites, and changed dependencies. Once committed, they become part of the evolving system. However, the governance context that legitimized these decisions—the boundaries, conditions, and decision evidence—is rarely preserved.

This is not primarily a runtime governance problem. It is a development-time governance gap: structural decisions that alter the system are produced without persistent governance context, making them difficult to reproduce, attribute, or evaluate after the fact.

---

### 2.1 Decision Boundary Loss in Development Scope

In software development, scope operates on multiple dimensions simultaneously:

**Visible Scope**: what information and development context are available to the AI during decision formation.
**Artifact Scope**: which files, modules, or components may be modified.  
**Behavior Scope**: what types of changes are permitted within those artifacts—including allowed change types, execution policies, and explicit behavior constraints.  

Current practice defines only the first. When an AI agent receives a prompt like "Fix the login timeout bug in `src/auth/`," the prompt serves as the sole condition input. From it, the artifact scope is inferable. What remains undefined:

**May the agent**:
- Create new files within `src/auth/`?
- Create new API endpoints?
- Modify the authentication flow architecture?
- Introduce new dependencies?
- Change the session management strategy?

These are **development decisions**—choices that determine system structure, not just system behavior. Without explicit boundaries, the agent operates in interpretive space:

- Creating a helper function: *probably acceptable*
- Creating a new module: *unclear*
- Creating a new API endpoint: *unclear*
- Changing authentication architecture: *probably unacceptable*

But "probably" is not governance. Organizations discover the boundary violation only after code review—or after deployment.

The problem is structural: **development scope cannot be inferred from artifact scope**. Knowing *where* to work does not determine *what kinds of work* are permitted. Yet development tooling provides no mechanism to specify behavior scope for code generation.

This becomes critical in AI-assisted development because development decisions are **immediate and structural**. A human developer might pause when considering "Should I create a new API for this?" An AI agent generates the code instantly. By the time the decision becomes visible (in the commit), it is already embedded in the artifact.

Without persistent behavior scope definitions, every code generation task operates partially in undefined scope.

---

### 2.2 Missing Decision Conditions in Development Rules

Development decisions require context-dependent rules. The same action—modifying a test file—may be:
- **Prohibited** during bug fixes (tests should validate the fix, not be changed)
- **Required** during test refactoring (the entire purpose is modifying tests)
- **Conditional** during feature development (tests may be updated if they validate new behavior)

Organizations rarely specify these conditions. Instead, they define **universal behavior constraints**:

**Behavior Constraint**: "Do not modify test files"

This constraint makes sense for bug fixes. But when applied uniformly:
- Test refactoring becomes impossible (blocking legitimate work)
- Feature development becomes ambiguous (should new features update tests?)

The behavior constraint exists, but the **execution policy** that determines when it applies does not. The missing conditions include:
- **Task Type**: Bug fix, feature addition, refactoring, hotfix
- **Change Scope**: Modifying behavior, restructuring internals, adding capabilities
- **Test Impact**: Tests validate existing behavior, tests validate new behavior, tests validate internal structure

Without an execution policy that activates constraints conditionally, development rules become binary: either too strict (blocking necessary work) or too loose (permitting unintended changes).

Consider a concrete development scenario:

**Task**: "Refactor the authentication module for better maintainability"  
**Behavior Constraint**: "Do not create new files"  
**Result**: AI cannot extract helper functions into separate modules, defeating the refactoring goal

The behavior constraint was designed under an execution policy for bug fixes (minimal change principle) but applied to refactoring (where structural change is the objective). The constraint exists, but the **execution policy that scopes its application** does not.

This is endemic in development governance: behavior constraints defined without execution policies that account for the development context. Organizations specify constraints for "AI agents" generically, not for "AI agents performing refactoring" or "AI agents fixing production hotfixes."

**Development decisions require behavior scope definitions—allowed types, execution policies, and behavior constraints—appropriate to the development context**. Current practice provides none of these.

---

### 2.3 Absence of Decision Evidence in Development Process

When code is committed, what governance evidence exists?

**Artifact Evidence** (what exists):
- git diff: +127 lines, −45 lines in auth.py  
- commit message: "Fix login timeout bug"  
- CI/CD records: all tests passed

**Condition evidence** (what is missing before the decision):
- What prompt initiated the task?
- What visible scope was available to the decision-maker?
- What artifact scope was authorized?
- What behavior scope was defined—allowed types, execution policies, behavior constraints?

**Decision evidence** (what is missing after the decision):
- What decision points were encountered and how were they resolved?
- Why was approach X chosen over alternative approaches?
- What is the outcome scope—did actual changes stay within the authorized boundary?

The artifact evidence proves *what changed*. Condition evidence would prove *under what governance conditions the decision was formed*. Decision evidence would prove *how the decision was made and what it actually produced*.

This gap is critical in development because **development decisions are one-way**: once code is generated and committed, reconstructing the decision logic becomes forensic work. Unlike runtime decisions (which can be re-executed with the same inputs), development decisions cannot be replayed.

Consider investigating a security issue three months after deployment:

**Question**: "Why was this API endpoint created?"  
**Available Evidence**:
- Commit shows the endpoint was added during bug fix #1234
- Task was "Fix authentication timeout"
- No mention of API creation in task description

**Missing Condition Evidence**:
- Was creating an API an allowed type for bug fix tasks?
- Did any behavior constraint address API creation?
- Was there an execution policy that scoped permissible actions for this task type?

**Missing Decision Evidence**:
- What decision logic led to creating a new endpoint instead of modifying existing code?
- Was there a human approval for this structural change?
- Does the outcome scope match the authorized artifact scope?

Investigators can see the artifact. They cannot see the condition structure or the decision record that produced it.

This is not a documentation problem. Git provides excellent artifact documentation. The gap is **governance documentation**—records of:
- What behavior scope was defined (condition evidence)
- What execution policy applied to this task type (condition evidence)
- What decision logic was active (decision evidence)
- What outcome scope resulted (decision evidence)

Without this evidence, development decisions are forensically opaque. The code exists, but its governance legitimacy is indeterminate.

---

### 2.4 The Development-Specific Governance Challenge

Development decisions differ from runtime decisions in three ways that make governance uniquely challenging:

**1. Structural Permanence**
- Runtime decisions: transient (request handled, then forgotten)
- Development decisions: permanent (code persists in version control)

**2. Multiplicative Impact**
- Runtime decisions: affect individual transactions
- Development decisions: affect all future executions

**3. Pre-emptive Nature**
- Runtime decisions: can be validated after execution
- Development decisions: validation must occur during generation

This creates a governance paradox: **development decisions require the strongest governance (due to permanence and impact) but receive the weakest governance (due to inadequate tooling for condition evidence and decision evidence)**.

Current practice governs development through:
- Code review (post-hoc, artifact-based)
- Testing (validates behavior, not decision legitimacy)
- Style guides (syntax, not governance)

None of these capture decision governance: **whether the decision to generate this code was formed under reproducible, attributable, and auditable conditions**.

The result: every commit carries invisible governance debt. The code works, but its condition evidence and decision evidence cannot be reproduced. The system evolves, but decision legitimacy cannot be established. Governance becomes reactive rather than structural.

This structural gap reveals a governance challenge: development decisions cannot be evaluated once their condition evidence disappears. A mechanism is therefore required to make development decisions observable, reproducible, and attributable before they become embedded in artifacts.

This requirement motivates the concept of decision observability, which defines the conditions under which development decisions can be structurally examined and governed.

---

## 3 Decision Observability Premise

Chapter 2 established that development decisions in AI-assisted software engineering suffer from boundary loss, missing conditions, and absent evidence. These deficiencies share a common root: the decision, once formed, cannot be structurally examined. Before decision analysis can classify outcomes or risk models can assign severity, a prior question must be answered: *under what conditions is a development decision observable at all?*

This chapter defines **decision observability** as the structural premise for governance. Decision observability is not a binary property but a composite condition: a decision is observable when persistent evidence exists to reconstruct its formation context, verify its relationship to governing rules, and evaluate whether its outcome falls within permitted scope. This formulation draws on two companion studies. The decision analysis framework (Tsai, 2026a) provides the analytical method for classifying decision states from observable evidence. The decision boundary model (Tsai, 2026b) provides the structural vocabulary—visible scope, artifact scope, behavior scope—through which governance boundaries are expressed. Decision observability unifies these contributions: it defines the evidence threshold at which decision analysis becomes feasible and boundary compliance becomes verifiable.

Decision observability therefore serves as the bridge between the governance gap identified in Chapter 2 and the decision analysis framework introduced in Chapter 4. Without observability, decision analysis cannot operate—there is nothing to analyze. Without decision analysis, risk classification cannot proceed. Decision observability is a necessary precondition for the entire governance chain proposed in this paper.

A development decision is observable when the conditions under which it was formed can be reconstructed from persistent evidence. This requires two categories of evidence to be available: **condition evidence**, which records the governance context that existed before and during decision formation, and **decision evidence**, which records the reasoning and results produced by the decision itself.

**Condition evidence** captures the inputs, boundaries, and rules that governed the decision at the time it was formed. It comprises four components:

**Prompt** is the specific instruction that initiated the decision process. In AI-assisted development, this is the literal prompt or task description provided to the agent. The prompt serves as the primary intent carrier—the artifact that connects organizational intent to agent action. It is the entry point of every development decision and the first piece of evidence required for observability.

**Visible Scope** records what information was available to the decision-maker at the time of decision formation. This includes referenced specifications, codebase context, system instructions, and any governing rules provided as input. In AI-assisted development, visible scope is bounded by the prompt context and retrieved documents. If a governing rule was not included in the agent's context, it did not participate in decision formation—regardless of whether the rule existed elsewhere in the organization. Visible scope evidence answers: *what did the decision-maker know?*

**Artifact Scope** records the explicitly permitted modification boundary: which files, modules, and components the decision-maker was authorized to change. Artifact scope is often partially specified (e.g., "modify files in `src/auth/`") but rarely exhaustively defined. Unspecified artifact boundaries create ambiguity about whether the creation of new files or modification of adjacent modules constitutes scope violation. Artifact scope evidence answers: *where was the decision authorized to act?*

**Behavior Scope** records the types of actions permitted within the artifact boundary. As established in the decision boundary model (Tsai, 2026b), behavior scope cannot be inferred from artifact scope alone—knowing *where* to work does not determine *what kinds of work* are permitted. Behavior scope comprises three sub-dimensions:

- **Type**: what categories of change are allowed—structural changes (new files, new APIs), behavioral changes (modified logic, altered control flow), or cosmetic changes (formatting, renaming).
- **Policy**: what execution principles govern the decision—such as the minimal change principle, backward compatibility requirements, or single-responsibility constraints.
- **Constraint**: what explicit prohibitions apply—such as "do not create new API endpoints" or "do not modify test files."

Together, type, policy, and constraint define the behavioral boundary of the decision. Without behavior scope evidence, a decision's artifact scope may appear compliant while its behavioral scope is entirely ungoverned—the boundary loss problem described in Section 2.1.

**Decision evidence** captures what happened during and after the decision. It comprises two components:

**Decision Record** captures the reasoning, alternatives considered, constraints applied, and resolution logic during decision formation. This is the most frequently absent evidence component. Without a decision record, the rationale behind a specific choice—why approach A was selected over approach B, why a particular trade-off was accepted—remains forensically inaccessible. Decision record evidence answers: *how was the decision formed?*

**Outcome Scope** records the actual changes produced by the decision, including both intended modifications and unintended side effects. Outcome scope extends beyond artifact scope by capturing what *actually* changed rather than what was *permitted* to change. Comparing outcome scope against artifact scope and behavior scope reveals whether the decision remained within its authorized boundaries. Outcome scope evidence answers: *what did the decision produce?*

The completeness of condition evidence and decision evidence together determines the degree of decision observability. When all components are present, the decision is fully observable: its context can be reconstructed (visible scope), its boundaries can be verified (artifact scope, behavior scope), its initiation can be traced (prompt), its reasoning can be examined (decision record), and its outcome can be evaluated against governing rules (outcome scope). When components are missing, observability degrades proportionally, and specific governance operations—attribution, reproducibility assessment, or compliance verification—become infeasible.

This evidence framework provides the structural foundation for decision analysis. Chapter 4 introduces the analytical methods that operate on observable decision evidence to classify decision states, which in turn enable the risk model defined in Chapter 5.

---

## 4 Decision Analysis Framework

Chapter 3 established the observability conditions under which development decisions can be structurally examined. Observable evidence, however, does not interpret itself. A mechanism is required to classify the structural state of each decision based on the evidence available. This chapter introduces **Decision Analysis** (DA)—an effect-oriented analytical method that takes observable decision evidence as input and produces a decision state classification as output. Decision Analysis is the bridge between observability (Chapter 3) and risk (Chapter 5): it transforms raw evidence into structured classifications that the risk model can interpret.

The framework presented here summarizes the companion study (Tsai, 2026a), which defines Decision Analysis in full formal detail. This chapter focuses on the conceptual foundations and state definitions required for the risk model, omitting the diagnostic protocol and cumulative analysis mechanisms that are treated comprehensively in the companion work.

### 4.1 Decision Analysis Concept

Decision Analysis is a structural analytical method. It determines the relationship between what a development decision was authorized to produce and what it actually produced. The determination is based entirely on observable evidence—the condition evidence and decision evidence defined in Chapter 3—without requiring semantic understanding of the generated code, subjective judgment of code quality, or reconstruction of the decision-maker's intent.

**Input.** Decision Analysis operates on the evidence components established by decision observability: prompt, visible scope, artifact scope, behavior scope (condition evidence), and decision record, outcome scope (decision evidence). Not all components need be present; the absence of specific components produces specific analytical states rather than analytical failure.

**Output.** Decision Analysis produces a single classification from a set of five mutually exclusive states: DA-N (Normal), DA-O (Over Outcome), DA-I (Indeterminate), DA-V (Decision Vacancy), and DA-U (Unobservable). Each state describes a structural relationship between the authorized scope and the actual outcome. The same evidence always produces the same state—the classification is deterministic and repeatable.

**Non-claims.** Decision Analysis makes no risk judgment. A state of DA-O (scope exceedance) does not imply that the modification is harmful, unauthorized, or in need of remediation. Decision Analysis makes no correctness judgment—it does not evaluate whether the generated code functions properly. It makes no governance recommendation—it does not prescribe what action should follow from a given state. These interpretive functions belong to the Decision Risk model (Chapter 5). Decision Analysis provides the structural facts; Decision Risk provides the governance interpretation.

This separation is not a methodological preference but a structural requirement. Analytical determination must remain governance-neutral to ensure repeatability. The same observable evidence must produce the same DA state regardless of organizational context, risk appetite, or governance policy. Mixing analysis with interpretation would make the classification dependent on organizational variables, destroying its value as a stable analytical foundation.

### 4.2 Anchor-Based Trace Analysis

Decision Analysis classifies decision states by examining the structural relationships among three scopes. Chapter 3 defined these scopes as evidence components; here they serve as the analytical operands:

**Visible Scope** ($S_v$) corresponds to the condition evidence that records what information was available to the decision-maker. It represents the governing context—the specifications, constraints, and rules that defined the decision's authorized boundaries.

**Artifact Scope** ($S_a$) corresponds to the condition evidence that records the permitted modification boundary. It represents what the decision-maker was authorized to change—which files, modules, or components were within the declared scope of the task.

**Outcome Scope** ($S_o$) corresponds to the decision evidence that records the actual modifications produced. It represents what the decision actually changed—the factual record of modification, independent of what was intended or authorized.

The analytical method proceeds effect-first. Analysis begins with the outcome scope—what actually changed—rather than with intent or authorization. This ordering is a structural necessity in AI-assisted development, where the internal reasoning of the generation process is not introspectable. The decision-maker's intent cannot be recovered from the AI system; only the observable effect can be examined.

The analytical sequence operates as follows:

1. **Observe**: determine $S_o$—what was actually modified. If no modification is observable, analysis terminates immediately.
2. **Compare**: evaluate $S_o$ against $S_a$—did the actual modifications stay within the authorized boundary?
3. **Trace**: for any modifications outside $S_a$, trace their structural relationship back toward $S_v$—can the scope-exceeding modifications be attributed to a governing specification?
4. **Classify**: based on the results of observation, comparison, and trace, assign the appropriate decision state.

Each step is a structural comparison between evidence components. No semantic interpretation of the generated code is required. The classification depends solely on the set-relational conditions among $S_v$, $S_a$, and $S_o$.

### 4.3 Decision Analysis Result Space

Five mutually exclusive states partition all possible analytical situations. They are presented here in the diagnostic evaluation order—the sequence in which conditions are checked during analysis.

#### 4.3.1 DA-U — Unobservable

**Condition:** No observable modification exists ($S_o = \emptyset$).

Analysis terminates at the entry condition. No state deviation was detected, so no further determination is possible. DA-U may result from: no development action occurring, the action producing no modifications, or modifications occurring outside the observable evidence boundary (e.g., changes to artifacts not captured by the project's version control or anchoring infrastructure).

DA-U does not distinguish between these causes. It records the analytical fact that nothing observable happened. Whether unobservability constitutes a governance concern—for instance, whether the absence of expected modifications signals a problem—is a question for the risk model, not for analysis.

#### 4.3.2 DA-V — Decision Vacancy

**Condition:** Observable modifications exist outside the artifact scope, and those modifications cannot be traced to any known governing specification or decision source.

The decision produced effects, but the decision that produced them does not exist in any recoverable structural form. No specification element, no requirement, no task definition, no constraint record provides a plausible origin for the scope-exceeding modifications. The code exists, but its decision origin is structurally absent.

DA-V is the formal detection criterion for what the companion study terms *ghost intent*: executable artifacts whose originating decision cannot be recovered. In development terms, DA-V identifies code that entered the system without any traceable connection to an authorized decision—code that exists but cannot answer the question "why was this created?"

DA-V is the most analytically severe observable state. It indicates not merely scope exceedance but complete absence of structural origin for the exceedance.

#### 4.3.3 DA-O — Over Outcome

**Condition:** Observable modifications exist outside the artifact scope ($S_o \not\subseteq S_a$), and the scope-exceeding modifications can be traced to known specification sources.

The development decision produced more changes than it was authorized to produce. The AI agent—or the developer assisted by AI—modified files, functions, or modules beyond the declared task boundary. However, unlike DA-V, the excess modifications can be structurally linked to governing specifications, meaning the scope exceedance is attributable even though it was not authorized.

Two sub-conditions refine the classification:

- **DA-O within specification reach**: the scope-exceeding modifications trace back to components within the visible scope. The decision "did more than asked" but the additional work is structurally related to the governing context. Example: a bug fix task that also refactors related functions referenced in the same specification.
- **DA-O beyond specification reach**: the scope-exceeding modifications trace to specifications outside the visible scope. The decision reached beyond its authorized information boundary. Example: a bug fix task that modifies a module governed by a different specification not included in the task context.

DA-O does not evaluate whether the additional modifications are correct, beneficial, or harmful. It identifies the structural fact of scope exceedance and determines whether the exceedance is specification-related or specification-unrelated.

#### 4.3.4 DA-I — Indeterminate

**Condition:** Observable modifications exist outside the artifact scope, and those modifications can be traced to multiple governing specifications with no unique attribution.

The scope-exceeding modifications have structural connections to the specification layer, but the trace yields multiple plausible sources. No evidence distinguishes which specification element actually drove the modification. The decision is attributable in principle—it came from *somewhere* in the specification—but the specific origin cannot be uniquely determined.

DA-I arises characteristically when a development task references multiple governing contexts simultaneously. For example, when a task is governed by both a functional requirement ("add OAuth support") and an architectural constraint ("maintain single-responsibility principle"), a structural change in the generated code may be attributable to either. If no evidence resolves the ambiguity, the state is Indeterminate.

DA-I does not resolve attribution. It identifies the structural fact of attribution instability—a condition that limits the precision of subsequent governance actions.

#### 4.3.5 DA-N — Normal

**Condition:** Observable modifications exist, all modifications fall within the artifact scope ($S_o \subseteq S_a$), and the artifact scope is structurally reachable from the visible scope.

No analytical anomaly. The development decision stayed within its authorized scope at both the artifact level (it modified only what it was permitted to modify) and the specification level (the permitted modifications are traceable to governing specifications). The evidence chain is complete: what was authorized can be verified, and what was produced falls within that authorization.

DA-N is the only state that produces no input for the risk model. All other states—DA-U, DA-V, DA-O, DA-I—represent structural conditions that require governance interpretation.

---

## 5 Decision Risk Model

Chapter 4 introduced Decision Analysis as a governance-neutral analytical method: it classifies the structural state of a development decision without interpreting whether that state constitutes a problem. This neutrality is essential for analytical repeatability but insufficient for governance action. An organization that knows a decision is DA-O (scope exceedance) has a structural fact; it does not yet have a governance response. Transforming structural facts into actionable governance requires an interpretive layer—a model that assigns governance meaning to analytical states.

This chapter defines **Decision Risk** (DR)—governance risk that arises from structural deficiencies in the decision formation process rather than from probabilistic estimation of future events. Decision Risk is not conventional software risk. It does not predict what might go wrong with a code artifact. It identifies what is already structurally deficient in the decision that produced that artifact—missing rules, broken traceability, absent evidence, or ungoverned scope.

The Decision Risk model operates on the output of Decision Analysis and produces four contributions. First, it defines Decision Risk as a function of DA state and governance context, distinguishing it from probabilistic risk (Section 5.1). Second, it maps each non-normal DA state to a corresponding risk category with specific governance implications (Section 5.2). Third, it identifies the structural domains—rule definition, traceability, and lifecycle—from which Decision Risk originates (Section 5.3), and formalizes the specific conditions within those domains as threat types (Section 5.4). Fourth, it defines the manifestation levels through which latent risk becomes operationally visible (Section 5.5), and provides a simple assessment matrix that combines threat type with manifestation level to produce severity ratings for governance prioritization (Section 5.6).

Together, these components form a complete risk interpretation chain: Decision Analysis produces a state → the state maps to a risk category → the risk category traces to structural threats → the threats manifest at observable levels → the threat–manifestation intersection determines governance severity. This chain enables organizations to move from "we detected an anomaly" to "this anomaly requires this specific governance response at this priority level."

---

### 5.1 Decision Risk Definition

Decision Analysis classifies the structural state of a development decision. It does not evaluate whether that state constitutes a governance problem. A classification of DA-O (scope exceedance) is a structural fact—it records that modifications exceeded the artifact scope. Whether this exceedance matters, how urgently it should be addressed, and what governance response it requires are questions that belong to a different analytical layer.

**Decision Risk** is governance risk derived from a decision analysis result:

$$
\text{Decision Risk (DR)} = f(\text{DA state}, \text{governance context})
$$

Where the DA state is the structural classification produced by Decision Analysis, and governance context includes the organizational rules, policies, and risk tolerance that determine how a given structural state should be interpreted.

Decision Risk is not probabilistic risk. It does not estimate the likelihood of a future event. It describes the governance implication of a structural condition that already exists. When Decision Analysis identifies that a development decision was formed without governing rules (DA-V), Decision Risk does not predict what might go wrong. It states that the decision is currently ungoverned—a structural condition with immediate governance consequences regardless of whether adverse outcomes materialize.

This distinction separates Decision Risk from conventional software risk assessment. Traditional risk models ask: *What could go wrong, and how likely is it?* Decision Risk asks a structurally prior question: *Is the decision governable at all?* A decision that cannot be observed (DA-U) cannot be governed—not because governance has failed, but because the structural precondition for governance does not exist. A decision formed without rules (DA-V) is ungoverned by definition, not merely undergoverned. These are structural states, not probabilistic estimates.

Decision Risk therefore answers three governance questions for each non-normal DA state:

**Governability**: Can governance mechanisms operate on this decision? DA-U decisions cannot be governed because they cannot be observed. DA-V decisions cannot be governed because no rules exist to govern them. DA-O and DA-I decisions can be governed but require different governance responses.

**Attributability**: Can the decision be traced to a responsible source? DA-V decisions have no traceable origin. DA-I decisions have multiple plausible origins but no unique attribution. DA-O decisions are attributable—the scope exceedance can be linked to specific specifications. DA-U decisions have no evidence to attribute.

**Structural risk potential**: Does the decision state create conditions for downstream governance failures? A single DA-O event may be minor; cumulative DA-O events across sessions constitute Inference Creep—a systemic structural erosion. A single DA-V event may be an anomaly; persistent DA-V events indicate systematic absence of decision governance. The structural risk lies not in the individual state but in the pattern.

---

### 5.2 Decision Risk Categories

Each non-normal Decision Analysis state maps to a corresponding Decision Risk category. The mapping is direct: each DA state produces exactly one DR category. DA-N (Normal) produces no Decision Risk—it is the only analytical state that requires no governance interpretation.

| Decision Analysis | Decision Risk | Risk Name          | Governance Question                                    |
| ----------------- | ------------- | ------------------ | ------------------------------------------------------ |
| **DA-U**          | **DR-U**      | Unobservable Risk  | Can this decision be governed at all?                  |
| **DA-V**          | **DR-V**      | Vacancy Risk       | Does a governing rule exist for this decision?         |
| **DA-O**          | **DR-O**      | Over-Scope Risk    | Did this decision stay within its authorized boundary? |
| **DA-I**          | **DR-I**      | Indeterminate Risk | Can this decision be attributed to a unique source?    |

The four categories are ordered by governance severity—from the most structurally severe (DR-U) to the least (DR-I). This ordering reflects a principle: governance requires progressively more structural infrastructure as it moves from observation to attribution.

**DR-U — Unobservable Risk.** The decision cannot be observed. No outcome scope is available, so no comparison against artifact scope or visible scope is possible. Governance is structurally precluded: there is nothing to govern. DR-U represents the most fundamental governance failure—not a failure of rules, constraints, or processes, but a failure of the evidence infrastructure that makes governance possible. The governance response to DR-U is not to improve rules but to establish observability. Until the decision becomes observable, all other governance mechanisms are inoperative.

In development practice, DR-U manifests when AI-assisted code changes occur outside the project's anchoring infrastructure—modifications to files not tracked by version control, changes made in ephemeral environments without persistent records, or generation events whose outputs are manually copied into the codebase without preserving the generation context. The code enters the system, but the decision that produced it leaves no structural trace.

**DR-V — Vacancy Risk.** The decision is observable—modifications exist and can be detected—but no governing rule, specification, or decision source can be identified as the origin. The decision produced effects without structural authorization. DR-V is the governance interpretation of ghost intent: executable code whose decision origin is absent from the governance structure.

DR-V is more severe than DR-O because it indicates not merely that a boundary was exceeded, but that no boundary existed to be exceeded. An over-scope decision (DR-O) implies that governance was attempted but insufficient; a vacant decision (DR-V) implies that governance was never established for this decision space. The governance response to DR-V is to establish decision authority—to create the rules, specifications, or boundary definitions that should have governed the decision before it was formed.

In development practice, DR-V manifests when AI agents generate code in areas where no specification exists, no task definition covers the modified artifacts, and no constraint addresses the type of modification produced. The code may be functionally correct, well-structured, and useful—but its governance legitimacy is indeterminate because no rule structure exists against which to evaluate it.

**DR-O — Over-Scope Risk.** The decision is observable, governing rules exist, and the scope-exceeding modifications can be traced to specification sources—but the actual modifications exceeded the authorized artifact scope. The governance structure was in place, but the decision outcome extended beyond its boundary. DR-O is the governance interpretation of scope exceedance: the decision was governed but not contained.

DR-O admits two severity sub-levels inherited from Decision Analysis. When the scope exceedance traces to specifications within the visible scope (DA-O within specification reach), the risk is attributable and the governance response is typically constraint refinement—tightening the boundary definitions to prevent recurrence. When the scope exceedance traces to specifications outside the visible scope (DA-O beyond specification reach), the risk is more severe because the decision accessed governing context it was not authorized to see, suggesting a deeper structural gap in scope definition.

In development practice, DR-O is the most commonly observed Decision Risk category. It manifests whenever an AI agent "does more than asked"—fixing a bug while also refactoring adjacent code, implementing a feature while also creating new utility functions, or modifying test files while executing a task where test modification was not authorized. Each instance may be individually minor; cumulative instances constitute Inference Creep.

**DR-I — Indeterminate Risk.** The decision is observable, governing rules exist, and the scope-exceeding modifications can be traced to the specification layer—but the trace yields multiple plausible sources with no unique attribution. The governance structure is in place, the boundary was exceeded, and the exceedance is specification-related—but which specification drove the decision cannot be determined.

DR-I is the least severe category because the governance infrastructure is largely functional. Rules exist, traceability exists, and the scope exceedance is linked to known specifications. The deficiency is attributional precision: governance actions cannot target a specific rule or specification for improvement because the causal link is ambiguous. The governance response to DR-I is evidence enrichment—adding decision records, refining specification boundaries, or decomposing multi-viewpoint tasks into single-viewpoint tasks to eliminate attribution ambiguity.

In development practice, DR-I manifests when complex tasks reference multiple governing specifications simultaneously. A task governed by both a functional requirement and an architectural constraint may produce modifications attributable to either. Without a decision record disambiguating the driver, governance must treat the modification as ambiguously sourced—complicating root-cause analysis and targeted improvement.

---

### 5.3 Structural Sources of Decision Risk

Decision Risk does not arise from random events, implementation errors, or operational failures. It arises from **structural deficiencies in the development governance infrastructure**—gaps in the rules, traceability mechanisms, and lifecycle processes that should govern development decisions but do not.

This structural origin distinguishes Decision Risk from conventional software risk. A conventional software risk might be: "the authentication module may contain a vulnerability." Decision Risk asks a prior question: "was the decision to modify the authentication module formed under conditions where vulnerabilities could be detected?" The first is an outcome risk; the second is a governance risk. Decision Risk operates at the governance layer, not the artifact layer.

Three structural domains produce Decision Risk:

**Rule definition deficiencies.** Development decisions require governing rules—policies that define decision principles and constraints that define explicit prohibitions. When these rules are absent, incomplete, or ambiguously scoped, decisions are formed in ungoverned or partially governed space. Rule definition deficiencies include: rules that do not exist for a given decision type (producing DA-V), rules whose scope boundaries are unclear (contributing to DA-O), rules designed for one task type but applied uniformly to all task types (the execution policy gap described in Section 2.2), and rules whose records have been lost or were never persisted.

**Traceability deficiencies.** Governance requires the ability to trace from a decision's outcome back to its governing rules, and from those rules forward to the specifications that authorized the decision. When traceability is disrupted—when the chain from outcome to rule to specification is broken—decisions cannot be attributed, audited, or evaluated for compliance. Traceability deficiencies include: trace paths that terminate before reaching a governing rule (producing DA-V), trace paths that fork into multiple plausible sources without resolution (producing DA-I), rules that propagate from one context to another without explicit reference chains, and delegation structures where the original rule authority is no longer identifiable.

**Lifecycle deficiencies.** Development decisions occur within time-evolving systems. Rules that were adequate at one point may become inadequate as the system evolves. Scope boundaries that were appropriate for version $n$ may be insufficient for version $n{+}k$. Temporary rules introduced for specific circumstances may persist indefinitely. Lifecycle deficiencies include: scope expansion over successive development sessions (the structural mechanism of Inference Creep), temporary rules that become permanent due to undefined expiration, behavioral drift where actual development practices diverge from declared rules, and delayed impact where the consequences of a governance gap manifest only after multiple development cycles.

These three domains are not independent. A rule definition deficiency (missing constraint) may create a traceability deficiency (no trace target for attribution), which compounds over the lifecycle (scope expands unchecked across sessions). Decision Risk is often produced by the interaction of deficiencies across domains rather than by a single isolated gap.

The specific structural conditions within these domains are formalized as **Threat Types** in Section 5.4.

---

### 5.4 Threat Types

Section 5.3 identified three structural domains—rule definition, traceability, and lifecycle—as the sources of Decision Risk. Threat types formalize the specific structural conditions within these domains that produce governance failures. Each threat type describes a concrete, identifiable condition in which the governance infrastructure degrades in a way that creates or amplifies Decision Risk.

Development governance operates through two types of rules. **Policies** define decision principles—general statements of what should guide decision-making ("minimize structural changes during bug fixes," "maintain backward compatibility"). **Constraints** define explicit prohibitions—specific, enforceable boundaries that restrict the permissible action space ("do not modify test files," "do not create new API endpoints"). Threat types describe the ways in which policies, constraints, and their associated traceability structures degrade during the development lifecycle.

Three families of threats correspond to the three structural source domains.

**Structural Threats (ST)** arise from deficiencies in rule definition or governance structure—conditions where the rules themselves are absent, incomplete, or structurally inadequate.

| Threat Code | Name                      | Description                                                                                                                                                                                                                                        | Indicator                       |
| ----------- | ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| **ST-1**    | Missing Rule              | No policy or constraint exists for the decision type. The decision space is entirely ungoverned. This is the primary structural source of DR-V: the decision produces effects, but no rule exists against which to evaluate them.                  | Rule coverage = 0               |
| **ST-2**    | Lost Rule Record          | A rule was defined but its record has been lost or was never persisted. The rule may have existed in a meeting decision, a verbal agreement, or a configuration that was overwritten. The governance intent existed; the evidence does not.        | Rule defined but record missing |
| **ST-3**    | Implicit Rule Propagation | A rule propagates from one context to another without an explicit reference chain. For example, a constraint defined for module A is informally applied to module B because "they work the same way"—but no formal relationship links the two.     | Rule reference missing          |
| **ST-4**    | Rule Boundary Ambiguity   | A rule exists but its scope is unclear. A constraint states "do not modify configuration files" without defining what counts as a configuration file. Is `docker-compose.yml` a configuration file? Is `.env.example`? The boundary is unresolved. | Rule scope incomplete           |

ST-1 and ST-2 represent absence—of rules and of rule records, respectively. ST-3 and ST-4 represent degradation—rules that exist but whose structural integrity is insufficient for governance. In practice, ST-3 is particularly insidious because the rule appears to function (behavior is constrained) while its governance basis is structurally unsound (the constraint's authority chain is informal).

**Temporal Threats (TT)** arise from governance degradation over time—conditions where the governance structure was adequate at one point but has become inadequate through system evolution, repeated development cycles, or the passage of time.

| Threat Code | Name                      | Description                                                                                                                                                                                                                                                                                                                                                     | Indicator             |
| ----------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| **TT-1**    | Scope Expansion           | The effective decision scope expands over successive development sessions. Each session may remain within its locally defined scope, but the cumulative scope exceeds the original authorization. This is the threat mechanism underlying Inference Creep: individually compliant decisions that collectively violate the original boundary.                    | Scope(t1) < Scope(t2) |
| **TT-2**    | Persistent Temporary Rule | A rule introduced as a temporary measure becomes permanent because no expiration condition was defined. Emergency constraints ("do not deploy to production this week") persist beyond their intended validity period and distort ongoing governance without anyone recognizing the rule's temporal scope has expired.                                          | Expiry undefined      |
| **TT-3**    | Rule Drift                | Actual development behavior gradually diverges from the declared rule. The rule states "all structural changes require architecture review," but in practice, minor structural changes are routinely committed without review. The rule exists in the governance record; the behavior exists in the codebase. They no longer correspond.                        | Behavior $\neq$ rule  |
| **TT-4**    | Delayed Impact            | The consequences of a governance gap manifest only after multiple development cycles. A missing constraint on dependency introduction (ST-1) produces no visible effect in session 1. By session 10, the project has accumulated unauthorized dependencies that create security or compatibility issues. The risk was created at session 1; it manifests later. | Impact delay          |

TT-1 is the most structurally significant temporal threat because it compounds invisibly. Each individual session passes governance review (DA-N locally), but the cumulative effect constitutes scope exceedance (DA-O cumulatively). TT-4 amplifies all other threats by creating temporal separation between cause and consequence, making root-cause attribution difficult.

**Referential Threats (RT)** arise from traceability failures—conditions where the structural links between decisions, rules, and specifications are broken, incomplete, or ambiguous.

| Threat Code | Name                | Description                                                                                                                                                                                                                                                                                                                                  | Indicator                        |
| ----------- | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| **RT-1**    | Trace Discontinuity | The trace path from a decision outcome to its governing rule is broken. The outcome exists, the rule may exist, but the structural link between them is absent. This is the primary referential source of DA-V: the decision's effect is observable, but its origin cannot be traced.                                                        | Missing trace                    |
| **RT-2**    | Rule Chain Break    | A rule's authority chain—the lineage from rule to specification to organizational intent—is incomplete. The rule exists and is enforced, but its derivation from a higher-level specification cannot be verified. The rule may be legitimate or may be an artifact of historical practice with no current authorization.                     | Origin unknown                   |
| **RT-3**    | Delegation Cascade  | Rule authority propagates through multiple delegation levels without structural controls. An original specification delegates to a design document, which delegates to a task definition, which delegates to an AI prompt. By the third delegation, the connection to the original specification is tenuous and may be semantically altered. | Delegation depth > 1             |
| **RT-4**    | Outcome Masking     | A functionally correct outcome conceals a governance deficiency. The code works, tests pass, and review approves—but the rule structure that should have governed the decision is absent or broken. Correctness masks the governance gap. This is the most dangerous referential threat because it produces no visible signal.               | Outcome correct but rule unclear |

RT-4 deserves particular emphasis. In conventional engineering practice, defective outcomes signal governance failures—a bug prompts investigation, which reveals process gaps. RT-4 describes the opposite: the outcome is correct, so no investigation occurs, and the governance gap remains hidden. In AI-assisted development, this is common because AI agents frequently produce functionally correct code even when operating outside governed scope. The code quality conceals the governance deficiency.

**Decision Risk to Threat Mapping.** Each Decision Risk category is typically produced by characteristic threat combinations. This mapping is not deterministic—a given DR category may arise from various threat combinations—but it identifies the most common structural patterns.

| Decision Risk | Primary Threats | Secondary Threats | Characteristic Pattern                                                                                         |
| ------------- | --------------- | ----------------- | -------------------------------------------------------------------------------------------------------------- |
| **DR-U**      | ST-1, ST-2      | RT-1              | No rules exist (ST-1) or rule records are lost (ST-2), and no trace connects the decision to governance (RT-1) |
| **DR-V**      | ST-1, RT-1      | RT-2              | No rule governs the decision (ST-1), trace terminates before reaching any authority (RT-1, RT-2)               |
| **DR-O**      | ST-4, TT-1      | TT-3, ST-3        | Rule boundaries are ambiguous (ST-4), scope expands over time (TT-1), behavior drifts from rules (TT-3)        |
| **DR-I**      | RT-3, ST-3      | TT-2, RT-2        | Delegation cascades create attribution ambiguity (RT-3), implicit propagation blurs rule origins (ST-3)        |

This mapping serves two governance functions. First, it enables **diagnostic triage**: when a Decision Risk category is identified, the mapping directs investigation toward the most likely structural deficiencies. Second, it enables **targeted governance response**: rather than applying generic governance improvements, organizations can address the specific threat types that produce their most frequent Decision Risk categories.

---

### 5.5 Risk Manifestation Levels

Decision Risk does not necessarily manifest immediately. A structural governance deficiency may exist for months before producing visible consequences. The temporal gap between risk creation and risk manifestation is itself a governance challenge: risks that remain latent receive no governance attention, yet they accumulate structural debt that compounds over time.

Risk manifestation describes the degree to which a Decision Risk has become visible and impactful within the development process. Four levels capture the progression from invisible structural condition to system-wide governance failure.

| Level  | Name            | Description                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **L0** | **Latent**      | The risk exists as a structural condition but produces no visible signal. No analysis has been performed, no anomaly has been detected, and no development process has been affected. The governance deficiency is present but entirely invisible to all stakeholders.                                                                                                                                                               |
| **L1** | **Observable**  | The risk is detectable through Decision Analysis. A DA state classification has identified a non-normal condition (DA-U, DA-V, DA-O, or DA-I), and the corresponding DR category has been assigned. The risk is now structurally visible—it has been named and classified—but it has not yet affected any development process or system behavior.                                                                                    |
| **L2** | **Operational** | The risk impacts the development process. Code review identifies scope-exceeding modifications that require rework. Merge conflicts arise from uncoordinated scope expansions. Audit inquiries cannot establish decision legitimacy for specific commits. The governance deficiency is no longer abstract; it creates concrete friction in development operations.                                                                   |
| **L3** | **Systemic**    | The risk affects system behavior or organizational governance capacity. Unauthorized architectural changes alter system properties. Cumulative scope expansion (Inference Creep) has restructured modules beyond their original design intent. Security audit failures occur because decision evidence cannot be reconstructed. The governance deficiency has propagated from the decision layer into the artifact layer and beyond. |

The four levels describe a progression along two dimensions: **visibility** (is the risk detectable?) and **impact** (does the risk affect processes or systems?).

| Level  | Visibility | Impact                |
| ------ | ---------- | --------------------- |
| **L0** | Invisible  | None                  |
| **L1** | Detectable | None                  |
| **L2** | Detectable | Development process   |
| **L3** | Detectable | System and governance |

This progression is not deterministic. Not every L0 risk escalates to L3. Some latent risks are resolved before they manifest—a missing rule (ST-1) may be defined before it produces a DA-V event. Others remain latent indefinitely because the ungoverned decision space is never exercised. The manifestation levels describe the current state of a risk, not its inevitable trajectory.

However, the progression has a structural asymmetry: **escalation is passive while de-escalation requires active governance**. A risk at L0 can escalate to L1 simply because Decision Analysis is performed—the risk was always there; it is now visible. A risk at L1 can escalate to L2 because development continues in the presence of the governance deficiency. Escalation requires no action; it occurs through the normal operation of the development process. De-escalation, by contrast, requires deliberate governance intervention: defining missing rules, establishing traceability, refining scope boundaries. This asymmetry explains why Decision Risk accumulates: the default state of the development process is risk escalation, not risk resolution.

Manifestation levels serve a practical governance function: they enable **prioritization**. Organizations with limited governance capacity cannot address all Decision Risks simultaneously. Manifestation levels provide a triage criterion: L3 risks demand immediate structural intervention, L2 risks require process-level response, L1 risks should be monitored and scheduled for governance improvement, and L0 risks—by definition invisible—require that the organization invest in Decision Analysis capability to make them detectable.

---

### 5.6 Simple Risk Assessment Matrix

Sections 5.4 and 5.5 established two independent dimensions of Decision Risk: **threat type** (the structural condition that produces risk) and **manifestation level** (the degree to which that risk has become visible and impactful). Practical governance requires a method to combine these dimensions into a severity assessment that guides resource allocation and intervention priority.

This paper proposes a simple assessment matrix that crosses threat family with manifestation level to produce a four-level severity rating: **Low**, **Medium**, **High**, and **Critical**. The matrix is deliberately simple—it sacrifices quantitative precision for practical applicability. Organizations with mature governance infrastructure may refine the matrix with weighted scoring; the version presented here provides a baseline that requires no calibration data and can be applied immediately.

**Threat–Manifestation Matrix**

| Threat Family | L0 (Latent) | L1 (Observable) | L2 (Operational) | L3 (Systemic) |
| ------------- | ----------- | --------------- | ---------------- | ------------- |
| **ST**        | Low         | Medium          | High             | High          |
| **TT**        | Low         | Medium          | High             | Critical      |
| **RT**        | Medium      | High            | Critical         | Critical      |

The matrix encodes two principles derived from the structural analysis in Sections 5.3 and 5.4.

**Principle 1: Referential threats are more governance-damaging than structural or temporal threats at every manifestation level.** Structural threats (ST) describe absent or ambiguous rules—conditions that can be resolved by defining or clarifying rules. Temporal threats (TT) describe governance degradation over time—conditions that can be resolved by lifecycle management. Referential threats (RT) describe broken traceability—conditions that undermine the governance infrastructure's capacity to attribute, audit, and verify decisions. When traceability is broken, governance cannot determine *which* rule failed or *whose* decision produced the effect, rendering both rule improvement and lifecycle management ineffective. Referential threats therefore receive higher severity at every manifestation level: an RT threat at L0 (Latent) is rated Medium rather than Low, because even a latent traceability failure represents a condition where governance mechanisms cannot function if activated.

**Principle 2: Temporal threats escalate more severely at high manifestation levels than structural threats.** At L3 (Systemic), temporal threats are rated Critical while structural threats are rated High. This reflects the compounding nature of temporal threats: scope expansion (TT-1) and rule drift (TT-3) are cumulative processes that accelerate once they reach systemic manifestation. A structural threat at L3—such as a missing rule that has produced system-wide effects—is severe but bounded: the rule can be defined and the damage assessed. A temporal threat at L3—such as Inference Creep that has restructured multiple modules over dozens of development sessions—is both severe and structurally entrenched: the cumulative scope expansion has become the de facto system architecture, making remediation a restructuring effort rather than a rule definition.

**Severity Levels and Governance Response**

| Severity     | Governance Implication                                                                                                                                                                                                       |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Low**      | Monitor. The risk exists as a structural condition but has not manifested. Schedule governance improvement in the normal development cycle.                                                                                  |
| **Medium**   | Plan. The risk is detectable or involves latent traceability failure. Allocate governance resources for targeted intervention within the current cycle.                                                                      |
| **High**     | Act. The risk impacts development processes or represents a structural threat at systemic level. Governance intervention is required before further development proceeds in the affected scope.                              |
| **Critical** | Intervene immediately. The risk affects system governance capacity or involves traceability failure at operational or systemic level. Continued development without governance intervention compounds the risk structurally. |

**Assessment Example.** Consider a development project where Decision Analysis identifies a DA-V state for a code module: executable code exists but no governing rule or specification can be identified as its decision origin. The risk assessment proceeds:

1. **Decision Risk category**: DA-V maps to DR-V (Vacancy Risk).
2. **Threat identification**: DR-V is primarily associated with ST-1 (Missing Rule) and RT-1 (Trace Discontinuity). Investigation confirms RT-1: the trace path from the code artifact to any governing specification is broken.
3. **Manifestation level**: The untraced code has caused merge conflicts and review disputes—the risk is impacting the development process. Manifestation level: L2 (Operational).
4. **Severity assessment**: RT × L2 = **Critical**.
5. **Governance response**: Immediate intervention required. The governance team must reconstruct the trace—identifying or creating the specification that authorizes the code—and establish the rule structure (policy and constraints) that should govern future decisions in this scope. Continued development in the affected module without trace reconstruction compounds the referential threat with each additional commit.

This example illustrates the matrix's practical function: it translates an abstract structural condition (DA-V with RT-1 at L2) into a concrete severity level (Critical) with a specific governance response (trace reconstruction and rule establishment). The matrix does not replace detailed threat analysis—it provides the triage mechanism that determines which threats receive governance attention first.

---

## 6 Risk Governance Model

Chapter 5 defined the risk taxonomy: what Decision Risk is (Section 5.1), what categories it takes (Section 5.2), where it originates (Sections 5.3–5.4), how it manifests (Section 5.5), and how to assess its severity (Section 5.6). The taxonomy tells an organization *what risks exist* and *how severe they are*. It does not tell the organization *what to do about them*. A severity rating of Critical for an RT×L2 condition demands "immediate intervention"—but what form should that intervention take? At what organizational level should it operate? How does a single intervention connect to a sustained governance process?

This chapter defines the **Risk Governance Model**—the mechanism that translates risk assessments into governance actions. The model operates on three principles. First, governance responses must be proportional to risk severity—not every risk requires structural reform; some require only operational correction. Second, governance must be cyclic, not episodic—a single intervention addresses the current manifestation but does not prevent recurrence without systematic follow-through. Third, governance strategies must be risk-type-specific—the governance response to DR-V (missing rules) differs fundamentally from the response to DR-O (inadequate boundaries).

### 6.1 Governance Levels

Not all Decision Risks require the same depth of governance response. A scope exceedance detected during code review (DR-O at L2) may require only a targeted correction; a systemic traceability failure across multiple modules (DR-V at L3) demands structural reform. Applying structural governance to every risk instance is prohibitively expensive; applying only operational fixes to structural risks is ineffective.

Three governance levels define the depth of intervention, each corresponding to a different layer of the development governance infrastructure.

**Level 1: Operational Fix.** The governance response addresses the specific risk instance without modifying the underlying governance structure. The immediate anomaly is corrected: scope-exceeding code is reverted or reviewed, a missing decision record is retroactively created, or an untraced artifact is manually linked to its governing specification. Operational fixes are appropriate for isolated, low-severity risks—DA-O events within specification reach at L1 or L2 manifestation. They resolve the symptom without addressing the structural condition that produced it.

Operational fixes are necessary but insufficient as a sole governance mechanism. They treat each risk instance independently, creating no protection against recurrence. An organization that governs exclusively through operational fixes will resolve the same risk type repeatedly without reducing its frequency.

**Level 2: Process Adjustment.** The governance response modifies the development process to prevent recurrence of the identified risk pattern. If code review repeatedly identifies scope exceedance in a particular module, the process adjustment might introduce pre-generation scope verification for tasks affecting that module. If delegation cascades (RT-3) produce attribution ambiguity, the process adjustment might limit delegation depth for high-governance-impact specifications. Process adjustments are appropriate for recurring risks at Medium to High severity—patterns that indicate a systematic gap rather than an isolated event.

Process adjustments operate on the workflow layer: they change *how* development is conducted without changing the fundamental governance architecture. They add checkpoints, verification steps, or review gates that intercept risk before it manifests. Their limitation is that they depend on process compliance—if the adjusted process is not followed, the governance protection disappears.

**Level 3: Structural Governance.** The governance response modifies the governance architecture itself—the rule definitions, traceability infrastructure, or scope specification mechanisms that constitute the foundation of development governance. If DR-V events occur systematically because an entire decision domain lacks governing rules, structural governance creates the rule framework for that domain. If traceability failures (RT-1, RT-2) are endemic because the anchoring infrastructure does not capture decision evidence, structural governance establishes the infrastructure components required for trace persistence.

Structural governance is appropriate for Critical-severity risks and for risk patterns that persist despite process adjustments. It is the most resource-intensive governance level but produces the most durable protection: once the governance architecture is established, it governs all future decisions within its scope without requiring per-instance intervention.

The three levels are complementary, not exclusive. A Critical-severity risk may require all three: an operational fix to address the immediate instance, a process adjustment to prevent near-term recurrence, and structural governance to eliminate the root cause. The governance level selection is guided by the severity assessment from Section 5.6: Low and Medium severities typically require Level 1 or Level 2 responses; High severity requires Level 2 with Level 3 consideration; Critical severity requires Level 3 intervention.

### 6.2 PDCA Governance Cycle

Governance is not a single intervention but a continuous process. A risk identified today may be mitigated but not eliminated; the mitigation itself may introduce new governance conditions that require monitoring. The Risk Governance Model adopts the **Plan-Do-Check-Act** (PDCA) cycle as its operational framework, adapting the standard quality management cycle to the specific requirements of Decision Risk governance.

**Plan.** Identify and prioritize Decision Risks using the assessment framework from Chapter 5. For each prioritized risk, determine the appropriate governance level (Section 6.1) and select the risk-type-specific strategy (Section 6.3). Planning produces a governance action plan: which risks will be addressed, at what governance level, through what specific interventions, and with what expected outcomes. Planning also establishes the measurement criteria—the specific indicators (Appendix A) and risk load metrics (Appendix B) that will be used to evaluate governance effectiveness.

**Do.** Execute the governance action plan. At Level 1, this means applying operational fixes to specific risk instances. At Level 2, this means deploying process adjustments—adding scope verification steps, introducing decision record requirements, or establishing review gates. At Level 3, this means implementing structural changes—defining new rule frameworks, deploying traceability infrastructure, or restructuring specification mechanisms. Execution should be incremental: address the highest-severity risks first and validate each intervention before proceeding to the next.

**Check.** Re-evaluate the governance state after intervention. Perform Decision Analysis on development decisions produced under the new governance conditions. Compare the post-intervention DA state distribution against the pre-intervention baseline. Calculate the Governance Improvement Index (Appendix C) to quantify the change in risk load. The Check phase answers two questions: *Did the intervention reduce the targeted risk?* and *Did the intervention introduce new risks?* The second question is critical—a process adjustment that eliminates DR-O by restricting AI agent scope may inadvertently increase DR-U if the restriction prevents agents from producing observable modifications.

**Act.** Based on Check phase results, either standardize the successful intervention (incorporate it into the permanent governance structure) or revise the approach (return to Plan with updated risk assessment). The Act phase also identifies residual risks—governance gaps that remain after intervention—and feeds them back into the next Plan cycle. This creates the continuous improvement loop: each cycle reduces the overall Decision Risk load while the governance infrastructure matures incrementally.

The PDCA cycle operates at two temporal scales. **Short-term mitigation** cycles (days to weeks) address immediate risk instances through Level 1 and Level 2 responses. **Long-term governance** cycles (months to quarters) address structural deficiencies through Level 3 interventions and measure cumulative improvement across multiple development cycles.

### 6.3 Governance Strategy by Risk Type

Each Decision Risk category requires a different governance strategy because each originates from a different structural deficiency. Applying a generic "improve governance" response to all risk types is inefficient—it distributes governance resources uniformly rather than targeting the specific structural gap that produces the risk. The following strategies map each DR category to its primary governance intervention.

**DR-U → Establish Observability.** The decision cannot be governed because it cannot be observed. No rule improvement, process adjustment, or traceability mechanism can operate on an invisible decision. The governance strategy is to establish the evidence infrastructure that makes the decision observable: deploying anchoring mechanisms that capture prompt, visible scope, artifact scope, and outcome scope; integrating generation events into the project's version control and traceability systems; ensuring that AI-assisted development occurs within the observable boundary of the governance infrastructure. Once observability is established, the decision's DA state can be reclassified—likely to DA-V or DA-O—and the corresponding governance strategy applied.

**DR-V → Establish Decision Authority.** The decision is observable but no governing rule exists. The governance strategy is to create the rule structure that should govern the decision space: defining policies that establish decision principles for the relevant task type, defining constraints that establish explicit prohibitions, and linking both to the specifications that authorize development in the affected scope. Decision authority establishment is structural governance (Level 3): it creates governance infrastructure where none existed. Until decision authority is established, all decisions in the affected scope remain structurally ungoverned regardless of their functional correctness.

**DR-O → Refine Boundaries.** The decision is governed but the governance boundaries proved insufficient to contain the outcome. The governance strategy is to tighten the scope definitions that govern the decision: clarifying ambiguous rule boundaries (addressing ST-4), decomposing broad artifact scopes into more precise modification boundaries, and adding behavior constraints that address the specific types of scope exceedance observed. Boundary refinement is typically a Level 2 response (process adjustment) for isolated instances, escalating to Level 3 (structural governance) when cumulative scope expansion (TT-1) indicates systemic boundary inadequacy.

**DR-I → Enrich Evidence.** The decision is governed, the scope exceedance is specification-related, but the attribution is ambiguous. The governance strategy is to increase the precision of the evidence that connects decisions to their governing specifications: requiring decision records that document the specific specification element driving each structural change, decomposing multi-specification tasks into single-specification subtasks to eliminate attribution ambiguity, and refining delegation structures (addressing RT-3) to maintain traceable authority chains. Evidence enrichment is typically a Level 2 response that reduces attribution ambiguity incrementally across development cycles.

These four strategies are not mutually exclusive. A development project may simultaneously require observability establishment for one module (DR-U), decision authority creation for another (DR-V), boundary refinement for a third (DR-O), and evidence enrichment for a fourth (DR-I). The governance model supports concurrent strategy execution, prioritized by the severity assessment from Section 5.6.

---

## 7 Case Demonstrations

The preceding chapters defined the framework components in isolation: observability conditions (Chapter 3), analytical states (Chapter 4), risk taxonomy (Chapter 5), and governance model (Chapter 6). This chapter demonstrates how these components operate together through a single case that progresses through three governance stages. Each stage represents a PDCA cycle: the Check phase performs Decision Analysis and risk assessment; the Act phase introduces a governance intervention; the next stage operates under the improved governance conditions.

The case is deliberately simple—a single development task with a clear scope—to isolate the framework's analytical mechanism from the complexity of real-world projects. The purpose is not to demonstrate governance at scale but to show how the same development task produces different DA states, DR categories, and governance responses as the governance infrastructure matures.

### 7.1 Case Context

A development team maintains a web application with session-based authentication. The team decides to migrate the login system from session cookies to JSON Web Tokens (JWT). An AI agent is assigned to implement the migration.

The task—"modify the login system to support JWT"—is realistic, bounded, and structurally interesting. It involves modifying existing authentication logic (behavioral change), potentially creating new token management utilities (structural change), and possibly affecting adjacent systems such as session middleware, API endpoints, and test suites (scope expansion). The task's natural tendency toward scope expansion makes it a useful vehicle for demonstrating Decision Risk progression.

The case proceeds through three stages, each representing a governance maturity level. The stages are sequential: the governance intervention at the end of each stage creates the conditions for the next.

### 7.2 Stage 1 — Prompt Only (DA-U)

**Input.** The AI agent receives a single instruction: *"Modify login system to support JWT."* No software design document exists. No specification defines the migration scope. No policy governs the types of changes permitted. No constraint restricts the modification boundary. The prompt is the sole governance artifact.

**Decision Analysis.** The agent produces code changes, but the governance infrastructure captures none of the evidence components required for observability. No visible scope is recorded—the agent's context (which files it read, which specifications it referenced) is not persisted. No artifact scope is defined—the prompt does not specify which files may be modified. No behavior scope exists—no policy or constraint governs the types of changes permitted. No decision record captures the agent's reasoning. The outcome scope—what actually changed—is visible in the git diff, but without condition evidence, the diff cannot be evaluated against any governing standard.

Decision Analysis result: **DA-U** (Unobservable). Observable modifications exist in the git diff, but the governance evidence required to analyze them—visible scope, artifact scope, behavior scope—does not. The decision produced artifacts but left no governance trace.

**Risk Assessment.** DA-U maps to **DR-U** (Unobservable Risk). The decision cannot be governed because the evidence infrastructure required for governance does not exist. Threat identification: **ST-1** (Missing Rule)—no policy or constraint exists for any aspect of the task; **ST-2** (Lost Rule Record)—even the prompt context is not persisted after the generation session ends; **RT-1** (Trace Discontinuity)—no trace connects the code changes to any governing specification. Risk load: ST = 2, RT = 1, TT = 0; RL = 3 (Moderate risk). Manifestation level: L1 (Observable)—the risk is detectable through analysis but has not yet impacted development processes. Severity: ST × L1 = Medium; RT × L1 = High. The highest applicable severity is **High**.

**Governance Response.** DR-U requires establishing observability (Section 6.3). The governance intervention is to create a **Software Design Document (SDD)** that captures the migration intent, defines the affected components, and establishes a specification against which future decisions can be evaluated. This structural governance action (Level 3) creates the condition evidence infrastructure that was entirely absent.

### 7.3 Stage 2 — Specification Introduced (DA-V)

**Input.** The SDD now exists. It specifies: (1) the login module (`src/auth/login.js`) will be modified to issue JWT tokens instead of session cookies; (2) a token validation utility will be created; (3) the session middleware will be updated to accept JWT headers. The AI agent receives the SDD as context along with the implementation instruction.

**Decision Analysis.** The agent produces code changes. The governance infrastructure has improved: visible scope is now partially defined (the SDD establishes what the agent should know), and artifact scope is partially defined (the SDD names specific files and components). However, no policy governs *how* the migration should be conducted—whether the agent should use minimal changes or is permitted to restructure the authentication architecture. No constraint restricts what the agent must *not* do—no prohibition on creating new API endpoints, modifying test files, or introducing new dependencies.

The agent's output reveals modifications beyond the SDD's artifact scope: it created a new `/api/token/refresh` endpoint (not specified), modified the test suite to accommodate JWT (not authorized by the SDD), and introduced a new `jsonwebtoken` dependency (not addressed in the specification). These modifications are observable—the SDD provides a reference against which to compare—but they cannot be attributed to any governing rule because no rules exist.

Decision Analysis result: **DA-V** (Decision Vacancy). Observable modifications exist outside the artifact scope, and those modifications cannot be traced to any governing specification or decision source. The refresh endpoint, test modifications, and dependency introduction are structurally orphaned—they exist as code but have no decision authority.

**Risk Assessment.** DA-V maps to **DR-V** (Vacancy Risk). The decision is observable and its scope exceedance is detectable, but no rule exists against which to evaluate the exceedance. Threat identification: **ST-1** (Missing Rule)—no policy or constraint governs the agent's behavior types; **RT-1** (Trace Discontinuity)—the scope-exceeding modifications have no trace to any authorizing specification; **RT-4** (Outcome Masking)—the refresh endpoint and test modifications are functionally correct, concealing the governance gap. Risk load: ST = 1, RT = 2, TT = 0; RL = 3 (Moderate risk). Manifestation level: L1 (Observable)—the risk is detectable through DA comparison against the SDD. Severity: ST × L1 = Medium; RT × L1 = High. Highest applicable severity: **High**.

Compared to Stage 1: the risk load is unchanged (RL = 3), but the risk *composition* has shifted. ST decreased from 2 to 1 (the SDD resolved one rule absence), while RT increased from 1 to 2 (the now-observable scope exceedance reveals traceability gaps that were invisible in Stage 1). The governance intervention improved observability but exposed previously hidden referential threats.

**Governance Response.** DR-V requires establishing decision authority (Section 6.3). The governance intervention is to define **rules**—policies and constraints—that govern the development task:

- **Policy**: "Apply minimal change principle—modify only what is necessary to achieve the specified migration."
- **Constraint**: "Do not create new API endpoints unless explicitly specified in the SDD."
- **Constraint**: "Do not modify test files; test updates will be handled in a separate task."
- **Constraint**: "Do not introduce new dependencies without explicit approval."

These rules, combined with the existing SDD, create a complete condition evidence structure: visible scope (SDD + rules), artifact scope (SDD-specified files), and behavior scope (policy + constraints).

### 7.4 Stage 3 — Rule-Constrained Execution (DA-O)

**Input.** The AI agent now operates under comprehensive governance: the SDD defines the specification context (visible scope), the authorized modification targets (artifact scope), and the rules define permitted behavior types (policy), prohibited actions (constraints). The agent receives all of these as context for the implementation task.

**Decision Analysis.** The agent produces code changes. The governance infrastructure is now sufficient to evaluate every evidence component. The agent modified `src/auth/login.js` to issue JWT tokens (within artifact scope), created `src/auth/tokenValidator.js` as the validation utility (within artifact scope per SDD), and updated `src/middleware/session.js` to accept JWT headers (within artifact scope per SDD). These modifications are within the authorized boundary.

However, the agent also refactored the existing password hashing logic in `src/auth/login.js`—extracting it into a separate function for "better maintainability." This modification is *within* the artifact scope (the file was authorized for modification) but *outside* the behavior scope (the policy specified minimal changes; refactoring exceeds the minimal change principle). The refactoring can be structurally traced to the SDD—the password hashing function is part of the login module referenced in the specification—but it exceeds the authorized behavior boundary.

Decision Analysis result: **DA-O** (Over Outcome), within specification reach. Observable modifications exist outside the behavior scope, and the scope-exceeding modifications trace to a known specification source (the SDD's reference to the login module).

**Risk Assessment.** DA-O maps to **DR-O** (Over-Scope Risk). The decision was governed—rules existed and were partially effective—but the governance boundary proved insufficient to fully contain the outcome. Threat identification: **ST-4** (Rule Boundary Ambiguity)—the "minimal change principle" policy does not precisely define what constitutes "necessary" change, leaving the agent interpretive space to include refactoring; **TT-1** (Scope Expansion)—if this pattern recurs across sessions, the cumulative refactoring constitutes scope creep beyond the original migration intent. Risk load: ST = 1, RT = 0, TT = 1; RL = 2 (Moderate risk). Manifestation level: L1 (Observable). Severity: ST × L1 = Medium; TT × L1 = Medium. Highest applicable severity: **Medium**.

Compared to Stage 2: risk load decreased from 3 to 2, and referential threats were eliminated entirely (RT = 0). The governance intervention succeeded in establishing decision authority—every modification now traces to a governing specification or rule. The residual risk is a boundary precision issue (ST-4) and a potential temporal threat (TT-1), both more tractable than the vacancy and traceability failures of earlier stages.

**Governance Response.** DR-O requires boundary refinement (Section 6.3). The governance intervention is to tighten the behavior scope definitions: replacing the general "minimal change principle" with specific behavior type restrictions ("modify existing function signatures and control flow only; do not extract, inline, rename, or restructure functions") and adding a decision record requirement for any modification that the agent considers ambiguous relative to the policy.

### 7.5 Governance Implications

The three-stage progression demonstrates four properties of the Decision Risk framework.

**First, governance maturity shifts risk type rather than eliminating risk.** Stage 1 produced DR-U (unobservable); the governance intervention shifted it to DR-V (vacancy) in Stage 2; further intervention shifted it to DR-O (over-scope) in Stage 3. Each stage reduced risk severity—from High to High to Medium—but the risk did not disappear. It transformed from an infrastructure problem (no evidence) to an authority problem (no rules) to a precision problem (imprecise boundaries). This progression is characteristic: governance maturity does not eliminate Decision Risk; it converts severe, intractable risks into milder, addressable ones.

**Second, improved observability reveals previously hidden risks.** Stage 1's DR-U concealed the referential threats that became visible in Stage 2. The SDD did not create the traceability gap—it made an existing gap detectable. This is the L0-to-L1 transition described in Section 5.5: governance investment that increases observability will initially *increase* the number of detected risks. Organizations should expect this and interpret it as a sign of governance progress, not governance failure.

**Third, risk load provides a quantitative governance trajectory.** Across the three stages, risk load progressed from RL = 3 to RL = 3 to RL = 2. The unchanged load between Stages 1 and 2 reflects the risk composition shift—structural threats decreased while referential threats increased. The decrease from Stage 2 to Stage 3 reflects genuine risk reduction through rule establishment. The Governance Improvement Index (Appendix C) for the full progression: $GI = RL_{\text{Stage 1}} - RL_{\text{Stage 3}} = 3 - 2 = 1$, indicating partial improvement. Further PDCA cycles would target the residual ST-4 and TT-1 threats.

**Fourth, the PDCA cycle produces incremental, measurable governance improvement.** Each stage followed the same pattern: Check (perform DA and risk assessment) → Act (apply targeted governance intervention). The intervention at each stage was specific to the identified DR category: establish observability for DR-U, establish decision authority for DR-V, refine boundaries for DR-O. This targeted approach—enabled by the framework's risk-type-specific governance strategies (Section 6.3)—ensures that governance resources address the actual structural deficiency rather than applying generic improvements.

---

## 8 Discussion

The Decision Risk framework addresses a specific governance gap: development decisions in AI-assisted software engineering lack the structural evidence required for governance evaluation. The framework provides a complete analytical chain—from observability conditions through decision analysis states to risk categories, threat types, manifestation levels, and governance responses. The case demonstration in Chapter 7 illustrates this chain operating across governance maturity stages. However, the framework operates under assumptions and within boundaries that warrant explicit discussion.

### 8.1 Limitations

**Observability dependency.** The framework requires decision observability as its operational prerequisite. Decision Analysis cannot classify what it cannot observe; Decision Risk cannot assess what Decision Analysis cannot classify. Organizations that lack the infrastructure to capture condition evidence and decision evidence—prompt persistence, scope recording, outcome tracking—cannot apply the framework until that infrastructure exists. The framework acknowledges this dependency (DR-U identifies the condition and prescribes observability establishment as the governance response), but it cannot bootstrap itself: some minimum evidence infrastructure must exist before the first analysis cycle can operate.

**Manual analytical process.** The current framework is defined as a conceptual and procedural model, not as an automated tool. Decision Analysis requires a human analyst to identify the three scopes, evaluate set-relational conditions, and assign DA states. Threat identification requires structural judgment about which threat types apply to a given situation. Risk assessment follows a defined matrix but the inputs—threat family and manifestation level—require interpretation. This manual dependency limits scalability: applying the framework to every development decision in a large project would require substantial analytical effort. Automation of scope extraction from version control systems, specification repositories, and AI agent logs would significantly improve practical applicability but remains outside the scope of this paper.

**Single-decision granularity.** The framework analyzes individual development decisions. The case demonstration examined one task across three governance stages. Real development projects involve hundreds or thousands of decisions with complex interdependencies—a scope exceedance in one decision may create conditions that affect subsequent decisions. The cumulative analysis mechanisms defined in the companion study (Tsai, 2026a) address cross-decision patterns, but the risk model presented here does not formally incorporate decision interaction effects. The Inference Creep phenomenon (TT-1) is identified as a temporal threat, but the framework does not provide a formal method for detecting cumulative scope expansion across decision sequences.

**Severity calibration.** The Threat–Manifestation Matrix (Section 5.6) assigns severity levels based on structural principles rather than empirical calibration. The rating that RT threats are more governance-damaging than ST threats at every level is a theoretical claim derived from the framework's structural analysis. Empirical validation—measuring whether RT-classified risks actually produce worse governance outcomes than ST-classified risks in practice—would strengthen the matrix's authority but requires longitudinal field studies that are beyond the scope of this work.

### 8.2 Implications

**For AI development governance.** The framework reframes AI governance in software development from an outcome-oriented activity ("does the code work correctly?") to a structure-oriented activity ("was the decision that produced this code formed under governable conditions?"). This reframing has practical consequences: it shifts governance investment from post-hoc code review toward pre-generation evidence infrastructure. Organizations adopting this perspective would prioritize specification completeness, rule definition, and scope declaration before AI-assisted generation begins—not as bureaucratic overhead but as governance infrastructure that enables structural evaluation of every subsequent decision.

**For development tooling.** The evidence components defined in Chapter 3—prompt, visible scope, artifact scope, behavior scope, decision record, outcome scope—constitute a specification for development tooling. Current AI-assisted development tools persist prompts and code diffs but discard the governance-critical intermediate evidence: what context was available, what rules applied, what scope was authorized, and what reasoning connected input to output. The framework implies that development environments should treat governance evidence as a first-class artifact, persisted alongside code with the same rigor applied to version control.

**For organizational risk management.** Decision Risk introduces a risk category that existing frameworks do not address. ISO/IEC 42001 governs AI management systems; ISO/IEC 5338 addresses AI system lifecycle processes. Neither provides a mechanism for evaluating whether individual development decisions were formed under governable conditions. The Decision Risk taxonomy—with its threat types, manifestation levels, and severity matrix—offers a complementary assessment layer that organizations can integrate into existing AI governance frameworks without replacing them.

---

## 9 Conclusion

AI-assisted software development introduces a structural governance challenge: development decisions are produced by or with AI agents, but the conditions under which those decisions are formed—governing rules, authorized scope, decision reasoning—are rarely preserved as persistent evidence. The result is that code artifacts accumulate in version control while the governance legitimacy of the decisions that produced them remains indeterminate.

This paper addressed this challenge through a four-component framework. **Decision observability** (Chapter 3) defined the evidence conditions—condition evidence and decision evidence—under which a development decision can be structurally examined. **Decision Analysis** (Chapter 4) provided the analytical method that classifies observable decisions into five mutually exclusive states (DA-N, DA-O, DA-I, DA-V, DA-U) based on set-relational conditions among visible scope, artifact scope, and outcome scope. **Decision Risk** (Chapter 5) interpreted these analytical states as governance risks, defining four risk categories (DR-U, DR-V, DR-O, DR-I), twelve threat types across three families (ST, TT, RT), four manifestation levels (L0–L3), and a severity assessment matrix. **Risk Governance** (Chapter 6) translated risk assessments into governance actions through three intervention levels and a PDCA cycle with risk-type-specific strategies.

The case demonstration (Chapter 7) showed these components operating as an integrated chain: a single development task progressing through three governance stages produced a measurable trajectory from DR-U (High severity, RL = 3) to DR-O (Medium severity, RL = 2), with each governance intervention targeting the specific structural deficiency identified by the preceding analysis cycle.

The framework's central claim is structural: development decisions that cannot be observed cannot be governed, and decisions that can be observed but lack governing rules accumulate governance debt regardless of their functional correctness. Decision Risk is not a prediction of future failure but a diagnosis of present structural deficiency—a condition that exists now and compounds with each ungoverned decision.

---

## 10. Related Work

AI-assisted software development has attracted increasing attention since the widespread adoption of large language models for code generation (Chen et al., 2021; Tian et al., 2024). Existing research primarily focuses on three areas: code quality and correctness (Ziegler et al., 2022; Pearce et al., 2023), security vulnerabilities in generated code (Pearce et al., 2022; Siddiq et al., 2024), and developer productivity gains (Vaithilingam et al., 2022; Mozannar et al., 2023). While these studies document the functional benefits and risks of AI-generated code, they largely treat the output as a black-box artifact, with limited attention to the governance legitimacy of the underlying development decisions.

Governance frameworks for AI systems have advanced significantly in recent years, particularly in runtime and deployment contexts. The NIST AI Risk Management Framework (NIST, 2023) and ISO/IEC 42001 (ISO, 2023) provide structured approaches to identifying, assessing, and mitigating AI-related risks, emphasizing traceability, accountability, and human oversight. In the agentic AI domain, frameworks such as the MODEL AI Governance Framework for Agentic AI (IMDA, 2025) and Preparing for AI Agent Governance (Partnership on AI, 2025) address autonomy risks, delegation cascades, and behavioral drift during operation. However, these frameworks assume that decisions are formed within observable, rule-governed environments and focus primarily on post-deployment monitoring rather than the pre-commit decision formation process in development workflows.

Decision analysis and observability concepts appear in related domains. Tsai (2026a) introduced an anchor-based decision analysis method for classifying development decisions into five states (DA-N, DA-I, DA-O, DA-V, DA-U) based on set-relational conditions among scopes. Tsai (2026b) further formalized decision boundaries (visible scope, artifact scope, behavior scope) as necessary conditions for governance legitimacy. These works provide analytical foundations but stop short of interpreting analytical states as structured governance risks or proposing a corresponding risk taxonomy and intervention model.

Threat classification in software engineering has been explored in vulnerability taxonomies (MITRE CWE, 2024) and supply-chain risk models (NIST SP 800-161r1, 2022), but these focus on technical artifacts rather than the governance conditions under which decisions are formed. Temporal and referential threat concepts draw inspiration from software evolution studies (Mens & Tourwé, 2004; Lehman, 1980) and traceability research (Gotel & Finkelstein, 1997; Cleland-Huang et al., 2007), yet no prior work systematically maps traceability failures or temporal drift to governance-level decision risks in AI-assisted development.

Quantitative governance metrics are emerging in AI risk literature, including recovery metrics for self-correction (IBM, 2025) and observability scores in system monitoring (Google SRE, 2024). However, no existing metric directly measures the recoverability of development decision trajectories or penalizes only the absence of traceable evidence while preserving legitimate exploration.

In summary, while prior work has advanced code generation quality, runtime AI governance, and traceability techniques, no framework has yet addressed the structural governance debt created when AI agents produce development decisions without persistent condition evidence and decision records. This paper bridges that gap by extending decision analysis into a structural risk taxonomy, recoverability-based governance levels, and measurable improvement mechanisms tailored to the open development phase of agentic AI systems.

---

## References

*   Chen, M., Tworek, J., Jun, H., Yuan, Q., Ponde de Oliveira Pinto, H., ... & Zaremba, W. (2021). Evaluating large language models trained on code. _arXiv preprint arXiv:2107.03374_.
*   Cleland-Huang, J., Gotel, O., Hayes, J. H., Mäder, P., & Zisman, A. (2007). Software traceability: Trends and future directions. _Future of Software Engineering (FOSE'07)_, 55–69.
*   Gotel, O. C., & Finkelstein, A. C. (1997). An analysis of the requirements traceability problem. _Proceedings of IEEE International Conference on Requirements Engineering_, 94–101.
*   IBM. (2025). _AI governance metrics and observability in enterprise AI systems_. IBM Research Report.
*   ISO/IEC. (2023). _ISO/IEC 42001:2023 Artificial intelligence — Management system_. International Organization for Standardization.
*   Lehman, M. M. (1980). Programs, life cycles, and laws of software evolution. _Proceedings of the IEEE, 68_(9), 1060–1076.
*   Mens, T., & Tourwé, T. (2004). A survey of software refactoring. _IEEE Transactions on Software Engineering, 30_(2), 126–139.
*   MITRE. (2024). _Common Weakness Enumeration (CWE)_. MITRE Corporation. [https://cwe.mitre.org](https://cwe.mitre.org)
*   Mozannar, H., Delfanti, L., & Chilton, L. B. (2023). The impact of generative AI on software development productivity. _Proceedings of the ACM on Human-Computer Interaction, CSCW_, Article 123.
*   NIST. (2023). _AI Risk Management Framework 1.0_. National Institute of Standards and Technology.
*   NIST. (2022). _Cybersecurity supply chain risk management practices for systems and organizations (SP 800-161r1)_. National Institute of Standards and Technology.
*   Partnership on AI. (2025). _Preparing for AI agent governance: A policy and research agenda_. Partnership on AI.
*   Pearce, H., Ahmad, B., Tan, B., Dolan-Gavitt, B., & Karri, R. (2022). Asleep at the keyboard? Assessing the security of GitHub Copilot’s code contributions. _2022 IEEE Symposium on Security and Privacy (SP)_, 754–770.
*   Pearce, H., Tan, B., Ahmad, B., Karri, R., & Dolan-Gavitt, B. (2023). Examining zero-shot vulnerability repair with large language models. _2023 IEEE Symposium on Security and Privacy (SP)_, 2339–2356.
*   Siddiq, H., Santos, J. C. S., Tan, R., Majumdar, S., & Pradel, M. (2024). A systematic evaluation of large language models for code generation. _arXiv preprint arXiv:2402.14868_.
*   Tian, H., Lu, W., Li, T. O., Tang, X., Cheung, S. C., Klein, J., & Bissyandé, T. F. (2024). Is ChatGPT the ultimate programming assistant — how far is it? _arXiv preprint arXiv:2304.11938_.
*   Tsai, S. (2026a). Decision analysis: Effect-oriented structural scope audit for AI-assisted software development. _engrXiv_. https://doi.org/10.31224/6616
*   Tsai, S. (2026b). Boundary as an execution-time primitive for AI-assisted software development governance. _engrXiv_. https://doi.org/10.31224/6583
*   Vaithilingam, P., Zhang, T., & Glassman, E. L. (2022). Expectation vs. experience: Evaluating the usability of code generation tools powered by large language models. _CHI Conference on Human Factors in Computing Systems Extended Abstracts_, 1–7.
*   Ziegler, A., Kalliamvakou, E., Li, X., Rice, D., Guo, K., ... & Johnson, D. (2022). Productivity assessment of GitHub Copilot. _arXiv preprint arXiv:2206.08974_.

---

## Appendix A Decision Observability Indicators

This appendix provides a set of practical indicators for evaluating the degree to which development decisions are observable—that is, the degree to which the evidence infrastructure required for Decision Analysis (Chapter 4) and Decision Risk assessment (Chapter 5) is present. The indicators do not measure decision quality or governance effectiveness; they measure whether the structural prerequisites for governance evaluation exist.

### A.1 Decision Observability Score (DOS)

The Decision Observability Score classifies each development decision into one of three observability levels based on the available evidence infrastructure.

| DOS Level | DA State Correspondence | Observability Level | Description                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| --------- | ----------------------- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **DOS-0** | DA-U                    | None                | The decision produced observable artifacts (code changes exist in version control) but no governance evidence persists. No visible scope, no artifact scope, no behavior scope, and no decision record are available. The decision cannot be subjected to Decision Analysis.                                                                                                                                                                          |
| **DOS-1** | DA-V, DA-I              | Partial             | Some governance evidence exists but is incomplete. The decision is observable—its effects can be identified and its scope can be partially reconstructed—but the governing rules, specification authority, or trace linkage required for full governance evaluation are absent or ambiguous. Decision Analysis can classify the decision but the classification reveals governance gaps (vacancy or attribution ambiguity).                           |
| **DOS-2** | DA-N, DA-O              | Structured          | Comprehensive governance evidence exists. Condition evidence (visible scope, artifact scope, behavior scope) and decision evidence (decision record, outcome scope) are present and structurally linked. Decision Analysis can fully evaluate the decision against its governing rules and specifications. The evaluation may reveal scope exceedance (DA-O), but the governance infrastructure is sufficient to detect, classify, and respond to it. |

DOS is a per-decision metric. An organization's overall observability posture can be summarized as the distribution of DOS levels across its development decisions: what percentage are DOS-0, DOS-1, and DOS-2. A governance maturity progression moves the distribution rightward—reducing the proportion of DOS-0 decisions and increasing DOS-2 decisions.

**Application.** DOS serves two functions. First, it provides a **baseline measurement** before governance intervention: an organization that discovers 60% of its AI-assisted decisions are DOS-0 knows that observability infrastructure—not rule definition—is the priority. Second, it provides a **progress metric** across PDCA cycles: the shift in DOS distribution from one governance cycle to the next quantifies the improvement in evidence infrastructure.

### A.2 Observability Evidence Components

A development decision's observability depends on the presence or absence of specific evidence components. The following checklist enumerates the components defined in Chapter 3, organized by evidence category.

**Condition Evidence** (what the decision-maker knew and was authorized to do):

| Component              | Description                                                                                            | Required for DOS-1 | Required for DOS-2 |
| ---------------------- | ------------------------------------------------------------------------------------------------------ | ------------------ | ------------------ |
| Prompt                 | The instruction or request that initiated the development action                                       | Yes                | Yes                |
| Visible Scope ($S_v$)  | The specifications, documents, and context available to the decision-maker at the time of the decision | No                 | Yes                |
| Artifact Scope ($S_a$) | The files, modules, or components authorized for modification                                          | No                 | Yes                |
| Behavior Scope         | The rules—policies and constraints—that govern permitted and prohibited actions                        | No                 | Yes                |

**Decision Evidence** (what the decision produced and why):

| Component             | Description                                                                                        | Required for DOS-1 | Required for DOS-2 |
| --------------------- | -------------------------------------------------------------------------------------------------- | ------------------ | ------------------ |
| Decision Record       | Documentation of the reasoning that connected input conditions to output actions                   | No                 | Yes                |
| Outcome Scope ($S_o$) | The actual modifications produced by the decision, as recorded in version control                  | Yes                | Yes                |
| Execution Trace       | The sequence of actions taken during generation—files read, functions invoked, intermediate states | No                 | Recommended        |

The "Required for DOS-1" column indicates the minimum evidence needed to achieve partial observability: the prompt and outcome scope must be available so that the decision's existence and effects can be identified. The "Required for DOS-2" column indicates the full evidence set needed for structured observability: all scope components plus the decision record must be present for complete governance evaluation. Execution trace is recommended but not strictly required for DOS-2, as the three scope sets and the decision record provide sufficient structural evidence for Decision Analysis.

### A.3 Observability Assessment Checklist

The following checklist translates the evidence components into assessment questions that can be applied to any development decision. Each question is binary (yes/no). The total count of "yes" responses does not directly produce a DOS level—the DOS level depends on which specific components are present, as defined in Section A.2—but the checklist provides a systematic procedure for evidence inventory.

1. **Is there an identifiable development action?** Can the decision be isolated as a discrete event—a generation session, a commit, a code review unit—with a defined beginning and end?
2. **Is the initiating prompt preserved?** Does the instruction that triggered the development action persist in a retrievable form after the action concludes?
3. **Is the specification context documented?** Can the specifications, design documents, and reference materials available to the decision-maker be identified and retrieved?
4. **Is the modification boundary defined?** Was the set of files, modules, or components authorized for modification explicitly declared before the action began?
5. **Do governing rules exist?** Are there policies (permitted behavior types) and constraints (prohibited actions) that apply to the decision scope?
6. **Is a decision record available?** Does documentation exist that captures the reasoning connecting the input conditions to the output actions?
7. **Is the outcome scope recorded?** Are the actual modifications—files changed, lines added or removed, artifacts created—captured in version control or an equivalent persistence mechanism?
8. **Can the outcome be traced to a governing specification?** Does a structural link exist from each modification in the outcome scope to a specification element in the visible scope that authorizes or motivates it?

Questions 1–2 with "yes" establish the minimum for DOS-1. Questions 1–7 with "yes" establish the minimum for DOS-2. Question 8 addresses traceability completeness—a "no" answer at DOS-2 indicates that the decision may classify as DA-V or DA-I despite having comprehensive evidence components, because the structural links between components are absent.

The checklist is designed for manual application during governance audits or PDCA Check phases. Organizations with automated evidence capture may implement these questions as programmatic checks against their development infrastructure.

---

## Appendix B Risk Load Estimation

This appendix defines the procedure for estimating Risk Load (RL)—the quantitative measure of structural decision risk intensity introduced in Section 5.4 and applied throughout the case demonstration in Chapter 7. Risk Load provides a single numeric value that summarizes the threat exposure of a development decision, enabling comparison across decisions, across governance stages, and across PDCA cycles.

### B.1 Threat Counting Method

Risk Load estimation begins with threat identification: for each development decision that has been classified through Decision Analysis (Chapter 4) and assigned a Decision Risk category (Section 5.2), the analyst identifies which specific threat types from Section 5.4 are active.

Threat identification follows the DR-to-Threat mapping table (Section 5.4) as an initial guide, then confirms each threat through structural evidence:

**Structural Threats (ST).** For each ST type (ST-1 through ST-4), determine whether the structural condition exists for the decision under analysis. ST-1 (Missing Rule): does the decision scope lack a governing policy or constraint? ST-2 (Lost Rule Record): did a rule exist at some point but its record is no longer retrievable? ST-3 (Implicit Rule Propagation): is the decision governed by an unwritten convention rather than an explicit rule? ST-4 (Rule Boundary Ambiguity): does a rule exist but with undefined or ambiguous scope boundaries? Count the number of confirmed ST threats. This count is the ST component of Risk Load.

**Referential Threats (RT).** For each RT type (RT-1 through RT-4), determine whether the referential condition exists. RT-1 (Trace Discontinuity): is the trace path from the decision outcome to its governing rule broken? RT-2 (Rule Chain Break): is the rule's authority chain—from rule to specification to organizational intent—incomplete? RT-3 (Delegation Cascade): does rule authority propagate through multiple delegation levels without structural controls? RT-4 (Outcome Masking): does a correct functional outcome conceal a governance deficiency? Count the number of confirmed RT threats. This count is the RT component.

**Temporal Threats (TT).** For each TT type (TT-1 through TT-4), determine whether the temporal condition exists. TT-1 (Scope Expansion): has the effective decision scope expanded across successive development sessions? TT-2 (Persistent Temporary Rule): has a temporary rule persisted beyond its intended validity? TT-3 (Rule Drift): has actual behavior diverged from the declared rule? TT-4 (Delayed Impact): are consequences of a governance gap manifesting only after multiple development cycles? Count the number of confirmed TT threats. This count is the TT component.

Each threat type is counted at most once per decision: a decision either exhibits ST-1 or it does not. The counting method does not weight threats—each confirmed threat contributes equally to its family count. This simplification is deliberate: differential weighting would require empirical calibration data that is not yet available. The severity differentiation between threat families is handled by the Threat–Manifestation Matrix (Section 5.6), not by the Risk Load calculation.

### B.2 Risk Load Calculation

Risk Load is the sum of confirmed threat counts across all three families:

$$RL = ST + RT + TT$$

where $ST$ is the count of confirmed structural threats (0–4), $RT$ is the count of confirmed referential threats (0–4), and $TT$ is the count of confirmed temporal threats (0–4). The theoretical range of RL is 0–12.

**Worked example from Chapter 7:**

| Stage          | ST  | RT  | TT  | RL  | Explanation                                                              |
| -------------- | --- | --- | --- | --- | ------------------------------------------------------------------------ |
| Stage 1 (DA-U) | 2   | 1   | 0   | 3   | ST-1 (missing rule), ST-2 (lost rule record), RT-1 (trace discontinuity) |
| Stage 2 (DA-V) | 1   | 2   | 0   | 3   | ST-1 (missing rule), RT-1 (trace discontinuity), RT-4 (outcome masking)  |
| Stage 3 (DA-O) | 1   | 0   | 1   | 2   | ST-4 (rule boundary ambiguity), TT-1 (scope expansion)                   |

The example illustrates that RL alone does not capture risk composition shift: Stages 1 and 2 both have RL = 3, but their threat profiles differ significantly. RL provides a summary metric for triage and trend tracking; the per-family counts (ST, RT, TT) provide the diagnostic detail needed for governance strategy selection (Section 6.3).

### B.3 Risk Severity Interpretation

The following interpretation table maps Risk Load values to severity bands. These bands are calibrated against the theoretical RL range (0–12) and aligned with the four-level severity scheme used in the Threat–Manifestation Matrix (Section 5.6).

| Risk Load | Severity Band | Interpretation                                                                                                                                                                                                                                        |
| --------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **0–1**   | Low           | Minimal structural threat exposure. The decision operates under governance conditions that address most threat types. Residual risk, if any, is isolated and tractable.                                                                               |
| **2–3**   | Moderate      | Multiple threat types are active. The decision has identifiable governance gaps that, while not yet causing systemic effects, require targeted intervention to prevent escalation.                                                                    |
| **4–5**   | High          | Substantial threat exposure across multiple families. The governance infrastructure has significant gaps that likely produce recurring risk manifestation. Governance intervention should be prioritized.                                             |
| **>5**    | Critical      | Pervasive structural threat exposure. The decision operates under governance conditions where most threat families are active, indicating fundamental governance infrastructure deficiencies. Immediate structural governance (Level 3) is warranted. |

Risk Load and the Threat–Manifestation Matrix provide complementary assessments. RL quantifies *how many* threats are active; the matrix assesses *how severe* each threat is given its manifestation level. A decision with RL = 2 may still produce a Critical severity rating if one of its two threats is an RT threat at L2 or L3. Conversely, a decision with RL = 4 may produce only Medium severity if all threats are ST types at L1. Practitioners should use both metrics: RL for overall threat burden and triage, the matrix for per-threat severity and response prioritization.

---

## Appendix C Governance Improvement Metrics

This appendix defines the metrics for evaluating whether governance interventions—operational fixes, process adjustments, or structural governance changes—actually reduce Decision Risk. Without measurement, governance becomes an assertion ("we improved") rather than a demonstration ("risk load decreased from 5 to 2"). The metrics defined here provide the quantitative basis for the Check and Act phases of the PDCA governance cycle (Section 6.2).

### C.1 Governance Improvement Index (GI)

The Governance Improvement Index measures the change in Risk Load between two assessment points—typically before and after a governance intervention, or between two PDCA cycles.

$$GI = RL_{\text{before}} - RL_{\text{after}}$$

where $RL_{\text{before}}$ is the Risk Load calculated at the earlier assessment point and $RL_{\text{after}}$ is the Risk Load calculated at the later point, both using the procedure defined in Appendix B.

A positive GI indicates risk reduction: the governance intervention eliminated one or more active threats. A GI of zero indicates no net change: the intervention may have resolved some threats while new threats emerged, or it may have had no effect. A negative GI indicates risk increase: the governance intervention introduced new threats or the development process accumulated additional threats faster than the intervention resolved them.

**Per-family decomposition.** GI can be decomposed into family-specific components to identify which threat families improved and which did not:

$$GI_{ST} = ST_{\text{before}} - ST_{\text{after}}$$
$$GI_{RT} = RT_{\text{before}} - RT_{\text{after}}$$
$$GI_{TT} = TT_{\text{before}} - TT_{\text{after}}$$

This decomposition is essential for diagnosing governance effectiveness. A governance intervention that produces GI = 1 overall but $GI_{ST} = 2$ and $GI_{RT} = -1$ has successfully addressed structural threats while inadvertently introducing a referential threat—a pattern that requires a different follow-up strategy than an intervention that uniformly reduced all threat families.

**Worked example from Chapter 7.** The three-stage case progression:

| Transition                     | $RL_{\text{before}}$ | $RL_{\text{after}}$ | GI  | Interpretation                                                                 |
| ------------------------------ | -------------------- | ------------------- | --- | ------------------------------------------------------------------------------ |
| Stage 1 → Stage 2              | 3                    | 3                   | 0   | Risk composition shifted (ST decreased, RT increased) but total load unchanged |
| Stage 2 → Stage 3              | 3                    | 2                   | 1   | Net risk reduction through rule establishment                                  |
| Stage 1 → Stage 3 (cumulative) | 3                    | 2                   | 1   | Partial improvement across the full governance progression                     |

### C.2 Governance Effectiveness Levels

The following table provides interpretive guidance for GI values, calibrated against the theoretical RL range (0–12).

| GI Range | Effectiveness Level     | Interpretation                                                                                                                                                                                                                                                                                                                                                    |
| -------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **0**    | No improvement          | The governance intervention produced no net reduction in threat exposure. Re-evaluate the intervention strategy: the intervention may have targeted the wrong threat type, or new threats may have emerged concurrently.                                                                                                                                          |
| **1–2**  | Partial improvement     | The intervention resolved some active threats but significant threat exposure remains. This is the expected outcome for single PDCA cycles addressing moderate-risk decisions. Continue with additional cycles targeting residual threats.                                                                                                                        |
| **3–4**  | Significant improvement | The intervention substantially reduced threat exposure across multiple families. This typically indicates a Level 3 structural governance intervention that addressed root causes rather than symptoms. Validate that the improvement is durable by monitoring subsequent development cycles.                                                                     |
| **>4**   | Structural improvement  | The governance infrastructure has been fundamentally strengthened. This level of improvement is characteristic of organizations transitioning from no governance infrastructure (DOS-0 dominant) to structured governance (DOS-2 dominant). It is achievable in early governance maturity stages but becomes increasingly difficult as the baseline RL decreases. |

GI should be interpreted in context: a GI of 1 from RL = 2 to RL = 1 represents a 50% reduction in threat exposure, while a GI of 1 from RL = 8 to RL = 7 represents a 12.5% reduction. Organizations with high baseline RL should expect multiple PDCA cycles to achieve significant cumulative improvement.

### C.3 PDCA Integration

The governance improvement metrics integrate into the PDCA cycle as follows:

**Plan.** Establish the baseline: calculate $RL_{\text{before}}$ and record the per-family threat profile (ST, RT, TT counts) for prioritized decisions. Define the target: specify which threat types the planned intervention aims to resolve and what $RL_{\text{after}}$ is expected.

**Do.** Execute the governance intervention at the appropriate level (Section 6.1) using the risk-type-specific strategy (Section 6.3).

**Check.** Re-assess: perform Decision Analysis on decisions produced under the post-intervention governance conditions. Calculate $RL_{\text{after}}$, compute GI and its per-family decomposition, and compare against the target. Identify any newly introduced threats (negative per-family GI components).

**Act.** If GI meets or exceeds the target and no new threats emerged, standardize the intervention into the permanent governance structure. If GI is below target or new threats emerged, return to Plan with updated threat profiles and revised intervention strategies.

Each PDCA cycle produces a GI measurement. The sequence of GI values across cycles constitutes the organization's **governance improvement trajectory**—a longitudinal record that demonstrates whether governance investment produces measurable risk reduction over time.

---

## Appendix D Decision Risk Assessment Worksheet

This appendix provides a step-by-step procedure for assessing Decision Risk in a development context. The worksheet consolidates the analytical methods defined in Chapters 4–6 into a sequential workflow that can be applied to any individual development decision. It is designed for manual use during governance audits, PDCA Check phases, or ad hoc risk evaluation of specific development events.

### D.1 Step 1: Decision Analysis

Identify the development decision to be assessed. A decision is a discrete development action—a generation session, a commit, a code review unit—that produced observable artifacts.

**Inputs required:**
- **Intent artifact**: The specification, design document, or task description that authorized the development action. If no intent artifact exists, record its absence—this is itself a significant finding.
- **Code artifact**: The actual modifications produced by the decision, as recorded in version control (git diff, commit history, or equivalent).
- **Trace relationship**: The structural link—if any—between the code artifact and the intent artifact. Can each modification in the code artifact be traced to a specific element in the intent artifact?

**Procedure:**
1. Identify the three scopes: visible scope ($S_v$—what was available as context), artifact scope ($S_a$—what was authorized for modification), and outcome scope ($S_o$—what was actually modified).
2. Evaluate the set-relational conditions among the three scopes using the Decision Analysis framework (Chapter 4).
3. Assign the DA state: DA-N (normal), DA-O (over outcome), DA-I (indeterminate), DA-V (decision vacancy), or DA-U (unobservable).

**Output:** DA classification with supporting evidence for the assigned state.

### D.2 Step 2: Risk Identification

Map the DA state to its corresponding Decision Risk category using the mapping defined in Section 5.2.

| DA State | DR Category | Risk Name                                            |
| -------- | ----------- | ---------------------------------------------------- |
| DA-N     | —           | No Decision Risk (decision is within governed scope) |
| DA-U     | DR-U        | Unobservable Risk                                    |
| DA-V     | DR-V        | Vacancy Risk                                         |
| DA-O     | DR-O        | Over-Scope Risk                                      |
| DA-I     | DR-I        | Indeterminate Risk                                   |

If the DA state is DA-N, the decision does not require further risk assessment—it operates within the governed boundary. Record the result and proceed to the next decision. For all other DA states, continue to Step 3.

**Output:** DR classification.

### D.3 Step 3: Threat Identification

Identify which specific threat types from the three threat families (Section 5.4) are active for the identified Decision Risk. Use the DR-to-Threat mapping table (Section 5.4) as a starting guide, then confirm each threat through structural evidence examination.

**For each threat family, assess:**

- **Structural Threats (ST):** Is a governing rule absent (ST-1)? Has a rule record been lost (ST-2)? Is a rule enforced implicitly without formal authority (ST-3)? Is a rule's scope boundary ambiguous (ST-4)?
- **Referential Threats (RT):** Is the trace from outcome to rule broken (RT-1)? Is the rule's authority chain incomplete (RT-2)? Does delegation propagate through multiple uncontrolled levels (RT-3)? Does functional correctness conceal a governance gap (RT-4)?
- **Temporal Threats (TT):** Has the effective scope expanded across sessions (TT-1)? Has a temporary rule persisted beyond its validity (TT-2)? Has behavior diverged from the declared rule (TT-3)? Are consequences manifesting only after multiple cycles (TT-4)?

Record each confirmed threat with a brief evidence note explaining why the threat is considered active.

**Output:** List of confirmed threat types with evidence notes. Per-family counts: ST = ___, RT = ___, TT = ___.

### D.4 Step 4: Risk Assessment

Calculate Risk Load and determine severity using the quantitative methods from Section 5.6 and Appendix B.

1. **Calculate Risk Load:** $RL = ST + RT + TT$ (sum of per-family threat counts from Step 3).
2. **Determine manifestation level:** Assess whether the risk is L0 (Latent), L1 (Observable), L2 (Operational), or L3 (Systemic) using the criteria from Section 5.5.
3. **Determine severity:** For each confirmed threat, cross-reference its threat family with its manifestation level in the Threat–Manifestation Matrix (Section 5.6). The highest severity rating across all confirmed threats is the decision's overall severity.

**Output:** Risk Load value, manifestation level, per-threat severity ratings, and overall severity (Low / Medium / High / Critical).

### D.5 Step 5: Governance Action

Select the governance response based on the risk assessment results, using the governance level guidance (Section 6.1) and risk-type-specific strategies (Section 6.3).

| DR Category | Primary Strategy             | Typical Actions                                                                                                                                                                            |
| ----------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| DR-U        | Establish Observability      | Deploy evidence capture infrastructure; integrate generation events into version control; ensure prompt and scope persistence                                                              |
| DR-V        | Establish Decision Authority | Define policies and constraints for the ungoverned decision space; link rules to authorizing specifications; create the governance structure where none exists                             |
| DR-O        | Refine Boundaries            | Tighten scope definitions; clarify ambiguous rule boundaries; decompose broad artifact scopes into precise modification boundaries; add behavior constraints for observed exceedance types |
| DR-I        | Enrich Evidence              | Require decision records documenting specification-to-change linkage; decompose multi-specification tasks into single-specification subtasks; limit delegation depth                       |

Select the governance level appropriate to the severity:
- **Low / Medium severity:** Level 1 (Operational Fix) or Level 2 (Process Adjustment).
- **High severity:** Level 2 with Level 3 consideration.
- **Critical severity:** Level 3 (Structural Governance) required.

**Output:** Selected governance strategy, governance level, and specific planned actions.

### D.6 Step 6: PDCA Iteration

After the governance action (Step 5) has been executed, return to Step 1 and repeat the assessment for decisions produced under the post-intervention governance conditions.

**Iteration checklist:**
1. Re-perform Decision Analysis (Step 1) on new decisions within the affected scope.
2. Re-classify Decision Risk (Step 2) and re-identify threats (Step 3).
3. Re-calculate Risk Load and severity (Step 4).
4. Compute the Governance Improvement Index: $GI = RL_{\text{before}} - RL_{\text{after}}$ (Appendix C).
5. Evaluate whether the intervention achieved its target. If residual risks remain, return to Step 5 with updated risk assessment and plan the next intervention cycle.

Each iteration through the worksheet constitutes one PDCA cycle. The sequence of RL values and GI measurements across cycles documents the governance improvement trajectory, providing evidence that governance investment produces measurable structural risk reduction.
