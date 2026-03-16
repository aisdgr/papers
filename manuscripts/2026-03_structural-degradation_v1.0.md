# Structural Degradation: From Stateless Generation to Layered Software Decay in AI-Generated Code
> A Three-Layer Taxonomy of Software Decay and Its Governance Implications

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Date:** March 2026  

---

## Abstract

Generative AI introduces a fundamental structural mismatch into software engineering: code is produced through stateless probabilistic generation, yet integrated into systems that evolve through stateful, temporally constrained architectures. While existing discourse concentrates on hallucinations, isolated defects, and productivity gains, it lacks a unified account of the degradation mechanisms unique to AI-assisted development—mechanisms that are neither reducible to individual bugs nor adequately captured by traditional notions of technical debt.

This paper proposes a three-layer taxonomy of structural degradation in AI-generated code, organized across the Intent, Structural, and Behavioral layers. We first establish the root cause model: a three-dimensional discontinuity—temporal, authorial, and state-based—arising from the interaction between stateless generation and stateful system evolution. We then define and differentiate eighteen distinct degradation phenomena distributed across the three layers, each characterized by its definition, distinction from adjacent concepts, illustrative examples, and degradation path logic. Finally, we demonstrate that these phenomena propagate across layers through identifiable causal mechanisms, and articulate the Visibility Inversion Principle: detection probability is inversely proportional to origination layer depth, while damage magnitude is directly proportional to failure layer depth.

The contribution of this paper is foundational. It establishes a coherent ontology of degradation patterns and their cross-layer propagation dynamics, providing a necessary conceptual foundation for future analytical, governance, and architectural research in AI-assisted software engineering.

---

**Keywords:** AI-Generated Code, Structural Degradation, Stateless Generation, Stateful Evolution, Three-Layer Taxonomy, Cross-Layer Dynamics, AI-Assisted Software Engineering

---

**JEL Classification:**  
- C88 — Design of Experiments: Software Engineering  
- O33 — Technological Change: Choices and Consequences  
- M15 — IT Management  

---

## 1. Introduction

The integration of generative AI into software development represents a paradigm shift in how code artifacts are produced, reviewed, and maintained. Large language models (LLMs) and AI-assisted coding tools now routinely generate functions, modules, and even architectural scaffolding from natural language prompts, code completion contexts, and iterative conversational refinement. The productivity implications of this shift have been widely discussed, with studies documenting acceleration in code production, reduction in boilerplate effort, and expansion of developer capabilities across unfamiliar domains.

Yet beneath the productivity narrative lies a structural tension that the current discourse has largely failed to articulate. AI-generated code is produced through **stateless probabilistic generation**: each generation event operates as an isolated completion, without persistent memory of prior iterations, without cumulative awareness of architectural evolution, and without recoverable authorial continuity. The resulting artifacts, however, are inserted into **stateful systems**—systems that have evolved over time through incremental modification, that carry implicit architectural constraints and accumulated invariants, and that depend on persistent authorship chains for interpretability and maintenance.

This mismatch between the stateless nature of generation and the stateful nature of the receiving system introduces degradation patterns that are qualitatively distinct from those addressed by traditional software engineering concepts. These patterns are not hallucinations—they may be syntactically and semantically valid. They are not isolated bugs—they emerge from structural interactions rather than localized errors. They are not conventional technical debt—they arise without conscious trade-off decisions. And they are not dead code—they may execute, produce output, and appear functional.

Despite their distinctive character, these degradation phenomena **remain under-theorized** in current software engineering discourse. Existing discussions tend to classify AI-related code quality issues under pre-existing categories—hallucination, defect density, code smell—without recognizing that AI-assisted development introduces novel degradation mechanisms with their own causal logic, propagation dynamics, and remediation requirements.

This paper addresses this gap by making four contributions:

1. **Root Cause Model.** We identify the fundamental cause of AI-generated code degradation as a three-dimensional discontinuity—temporal, authorial, and state-based—arising from the interaction between stateless generation and stateful evolution (Section 3).

2. **Three-Layer Taxonomy.** We construct a systematic taxonomy of eighteen degradation phenomena organized across three abstraction layers: Intent, Structural, and Behavioral. Each phenomenon is defined, differentiated from adjacent concepts, illustrated where appropriate, and situated within a degradation path logic (Section 4).

3. **Cross-Layer Propagation Model.** We demonstrate that degradation propagates primarily downward—from Intent through Structural to Behavioral—through identifiable causal mechanisms, and that behavioral failures serve as diagnostic signals rather than causal origins (Section 5).

4. **Visibility Inversion Principle.** We articulate a governing principle: the ease of detecting degradation is inversely proportional to its origination depth, while the magnitude of damage is directly proportional to the depth at which failure manifests. This principle carries direct implications for governance strategy, architectural design, and process optimization (Section 6).

The remainder of this paper is organized as follows. Section 2 defines the concept of structural degradation and establishes its boundaries. Section 3 analyzes the root cause through the three-dimensional discontinuity model. Section 4 presents the three-layer taxonomy in full. Sections 5 and 6 address cross-layer dynamics and the Visibility Inversion Principle, respectively. Section 7 discusses implications for software engineering practice. Section 8 acknowledges limitations and future directions. Section 9 concludes. Section 10 surveys related work.

---

## 2. Structural Degradation

Before presenting the taxonomy, it is necessary to define the central concept of this paper and to delineate its boundaries with precision.

### 2.1 Definition

**Structural degradation** refers to the progressive decay of software architecture that arises when AI-generated artifacts are integrated into stateful, evolving systems. It is not a single event or a localized defect, but a systemic condition that manifests across multiple abstraction layers and propagates through identifiable causal mechanisms.

### 2.2 Nature

The essential nature of structural degradation is **architectural decay induced by structural mismatch**. AI-generated code is produced under assumptions that diverge from the assumptions governing the receiving system. When such code is integrated—whether through direct insertion, iterative refinement, or regeneration—the resulting mismatch does not merely introduce an isolated anomaly. It destabilizes the structural coherence of the system across intent, topology, and behavior.

### 2.3 Manifestation

Structural degradation manifests across three abstraction layers:

- **Intent Layer:** Instability in the decision origins, semantic boundaries, and directional coherence of generated artifacts.
- **Structural Layer:** Degradation of architectural topology, module boundaries, dependency relationships, and structural interpretability.
- **Behavioral Layer:** Runtime instability, systematic omission patterns, hidden state violations, and suppressed error signals.

These manifestations are not independent. They are connected through cross-layer propagation dynamics that form the subject of Section 5.

### 2.4 Root Cause

Structural degradation originates from the **three-dimensional discontinuity** between stateless generation and stateful evolution. This discontinuity operates along temporal, authorial, and state dimensions simultaneously. The detailed causal model is presented in Section 3.

### 2.5 Distinction from Adjacent Concepts

Structural degradation is conceptually distinct from several established software engineering concepts:

- **Distinguished from bugs.** A bug is a localized, identifiable defect—an incorrect computation, a logic error, a boundary violation. Structural degradation may not manifest as any single identifiable defect; it emerges from the interaction between structurally mismatched artifacts and an evolving system context.

- **Distinguished from technical debt.** Technical debt, as introduced by Cunningham (1992), presupposes a conscious trade-off: developers knowingly accept suboptimal solutions in exchange for short-term benefit. Structural degradation involves no such conscious decision. It arises from the generative process itself, without deliberate human trade-off.

- **Distinguished from dead code.** Dead code is unreachable and non-executing. Structural degradation frequently involves code that executes, produces output, and appears functional—yet whose origin, purpose, or architectural alignment cannot be recovered.

- **Distinguished from hallucination.** Hallucination refers to the generation of factually incorrect or nonsensical content. Structural degradation phenomena may be syntactically valid, semantically plausible, and locally correct—yet structurally misaligned with the system they inhabit.

### 2.6 Propagation Mechanism

Structural degradation propagates through **cross-layer cascading dynamics**. Degradation at the intent layer embeds into structural artifacts, which in turn produce behavioral instabilities. This propagation is predominantly downward (Intent → Structural → Behavioral), and the difficulty of reversal increases with each layer transition. The full propagation model is developed in Section 5.

---

## 3. Root Cause: Stateless Generation vs. Stateful Evolution

### 3.1 The Assumptions of Traditional Software Development

Traditional software development life cycles (SDLC) rest upon three foundational assumptions that, while rarely stated explicitly, underpin the coherence and evolvability of software systems:

1. **Persistent Authorship.** Code is written by identifiable authors who carry contextual memory of design decisions, architectural rationale, and implementation history. This memory enables future maintainers to reconstruct intent from artifact.

2. **Incremental Structural Evolution.** Systems evolve through modifications that build upon prior structure. Each change extends, refines, or deliberately restructures what exists, rather than reinitializing it.

3. **Boundary-Respecting Modification.** Changes observe established module boundaries, interface contracts, and architectural constraints—whether explicit (documented APIs) or implicit (accumulated invariants).

Together, these assumptions support **cumulative system growth**: the property that each modification contributes to a coherent, evolving whole whose structural integrity can be maintained over time.

### 3.2 How AI Generation Violates These Assumptions

AI-assisted code generation systematically violates all three assumptions. The resulting violation is not incidental or occasional; it is inherent in the generative mechanism itself.

We conceptualize this violation as a **three-dimensional discontinuity**:

#### 3.2.1 Temporal Discontinuity

Generation occurs as isolated completion events. Each invocation of an AI code generator operates within a bounded context window, producing output based on the immediate prompt and available context, without persistent awareness of the historical sequence of iterations, regenerations, and modifications that have shaped the current system state.

**Consequence:** Each regeneration event partially resets local structure rather than cumulatively extending it. The system accumulates layers of partially reinitialized code, each reflecting the snapshot available at its moment of generation rather than the full evolutionary trajectory.

#### 3.2.2 Authorial Discontinuity

Traditional systems assume persistent authorship chains: code is written by authors whose identity, expertise, and decision-making rationale can be recovered—if not from documentation, then from organizational memory, version control attribution, or direct inquiry. AI generation disperses authorship across probabilistic outputs conditioned on transient prompts. The "author" of AI-generated code is neither the human who prompted it (who may not understand its internals) nor the model that produced it (which retains no memory of having done so).

**Consequence:** Artifacts lack recoverable authorial continuity. When questions arise about why a particular implementation choice was made, no persistent author exists to provide the answer. The decision origin is structurally absent.

#### 3.2.3 State Discontinuity

Generation treats the system as a snapshot—a static context provided to the model at generation time—rather than as an evolving stateful organism carrying implicit constraints, accumulated invariants, and dynamic dependencies. The model has no awareness of which architectural assumptions are load-bearing, which interface contracts are fragile, or which implicit dependencies have accumulated through prior evolution.

**Consequence:** Integration may violate accumulated architectural assumptions without producing immediate errors. The violation is silent, structural, and may remain latent until downstream conditions expose it.

### 3.3 Mechanistic Consequence: Non-Cumulative Integration

When temporal, authorial, and state discontinuities co-exist—as they inherently do in AI-assisted generation—the fundamental property of cumulative system growth breaks down. Integration becomes **non-cumulative**.

Instead of extending prior structure, each generation event partially reinitializes local structure. The system accumulates not coherent evolutionary layers, but a patchwork of structurally independent fragments, each optimized for its local generation context but blind to the global system trajectory.

Degradation thus emerges not from isolated defects, but from **repeated structural resets embedded into an evolving system**. Each reset is locally reasonable; the accumulated effect is systemic decay.

This is the causal foundation of all subsequent degradation phenomena defined in this paper.

![Figure 3.2: Triple discontinuities in state, time, and authorship root AI-generated non-cumulative integration, driving repeated structural resets and systemic decay.](../images/structural-degradation-02.png)

*Figure 3.2: Triple discontinuities in state, time, and authorship root AI-generated non-cumulative integration, driving repeated structural resets and systemic decay.*

---

## 4. A Three-Layer Taxonomy of Structural Degradation

This section presents the core contribution: a systematic taxonomy of eighteen degradation phenomena organized across three abstraction layers. For each phenomenon, we provide: (1) a definition, (2) a distinction from related concepts, (3) an illustrative example where appropriate, and (4) the degradation path logic characterizing its mode of emergence.

### 4.1 Intent Layer Degradation

The intent layer concerns the stability, recoverability, and coherence of decision intent—the originating rationale that should govern what code does and why. Intent-layer degradation arises when the link between generative output and originating human decision is severed, distorted, or fragmented.

#### 4.1.1 Ghost Intent

**Definition.** Ghost Intent denotes executable artifacts whose originating decision cannot be recovered. The code exists and functions, but no specification, requirement, prompt, or design record can be identified as its authoritative source.

**Distinction.** Ghost Intent is not undocumented code (where implicit intent may exist within organizational memory) and not a missing requirement (a specification gap that can be identified as such). Ghost Intent concerns the **absence of origin**: no recoverable decision trail connects the artifact to any human authorization.

**Example.** An AI generates caching logic within a data access module. No requirement specifies performance optimization; no prompt requests caching; no design document mentions it. The caching logic executes correctly, but its presence cannot be traced to any originating decision. It is a ghost—functional but unanchored.

**Path Logic.** Static absence. The degradation is present from the moment of generation; it does not develop over time but persists as a permanent gap in the decision record.

#### 4.1.2 Inference Creep

**Definition.** Inference Creep occurs when generation exceeds explicit instruction boundaries, producing functionality, structure, or behavior that was not requested and cannot be justified by the stated prompt or context.

**Distinction.** Inference Creep is not hallucination (factually incorrect generation), not a bug (a localized error), and not traditional scope creep (which involves deliberate negotiation and conscious expansion of project scope). Inference Creep is **probabilistic overreach**: the model's distributional tendencies lead it to generate beyond the boundary of explicit instruction, without any deliberate decision to expand scope.

**Example.** A developer prompts the AI to generate a user authentication function. The generated code includes not only authentication but also session management, role-based access scaffolding, and audit logging—none of which were requested. Each addition is plausible and syntactically valid, but collectively they represent scope that was never authorized.

**Path Logic.** Probabilistic overreach. The model's training distribution favors patterns that co-occur with the requested functionality, leading to implicit expansion beyond declared boundaries.

#### 4.1.3 Semantic Expansion

**Definition.** Semantic Expansion occurs when the conceptual meaning of a term or instruction broadens during the generation process, producing output whose scope exceeds the declared semantic boundary of the original directive.

**Distinction.** Semantic Expansion is not prompt drift (gradual shift in conversational context) and not misunderstanding (failure to parse intent). It is a **reinterpretation that extends beyond declared meaning**: the model treats the instructed concept as a seed from which to generate a broader conceptual scope.

**Example.** Prompted to "validate input," the AI generates code that not only validates format and type constraints but also sanitizes against injection attacks, normalizes Unicode representations, trims whitespace, and transforms data types. The original concept of "validation" has been semantically expanded to encompass sanitization, normalization, and transformation—each a distinct concern.

**Path Logic.** Beyond declared meaning. The boundary of the instructed concept is implicitly widened during generation, embedding additional responsibilities without explicit authorization.

#### 4.1.4 Intent Fragmentation

**Definition.** Intent Fragmentation occurs when a coherent intent exists but becomes structurally dispersed across generated artifacts, such that no single location preserves the complete, cohesive expression of the original decision.

**Distinction.** Intent Fragmentation differs from Ghost Intent ontologically: Ghost Intent concerns the **absence** of origin, while Fragmentation concerns the **loss of cohesion** despite the origin being present. The intent can be reconstructed in principle, but only by assembling scattered pieces from multiple locations—a reconstruction that may be infeasible in practice.

**Example.** A requirement specifies a unified error-handling strategy. Through multiple generation iterations, error handling logic is distributed across twelve different modules, each implementing a slightly different variant. The original intent—unified error handling—exists in the requirement document, but its structural realization is fragmented beyond practical cohesion.

**Path Logic.** Origin present, cohesion absent. The degradation lies not in the disappearance of intent but in its structural scattering.

#### 4.1.5 Scope Absorption

**Definition.** Scope Absorption occurs when generated code implicitly absorbs adjacent concerns without explicit declaration, effectively swallowing neighboring responsibilities into its own boundary.

**Distinction.** Scope Absorption involves **boundary swallowing rather than boundary crossing**. The absorbed concern does not appear as a separate, visible dependency or integration point; it is silently incorporated into the generated artifact, making it invisible to architectural analysis.

**Example.** An AI generates a logging module that silently absorbs responsibility for metrics collection, health-check reporting, and configuration validation. These concerns are not declared as part of the logging module's interface or responsibility; they are embedded within its implementation, invisible to module-level analysis.

**Path Logic.** Implicit inclusion. Adjacent concerns are drawn into the generated artifact's scope by distributional proximity in the model's training data, without any explicit decision to include them.

#### 4.1.6 Intent Drift

**Definition.** Intent Drift is the gradual deviation of generated artifacts from their original intent across multiple iterations of generation, regeneration, or refinement.

**Distinction.** Intent Drift is not deliberate modification (conscious redesign). Each local regeneration or iterative refinement optimizes for local coherence without reference to the original anchor—the initial intent that governed the first generation. Over successive iterations, the cumulative effect is a progressive departure from the original direction.

**Example.** A data transformation pipeline is initially generated to convert CSV input to JSON output with specific field mappings. Through five iterations of regeneration to fix edge cases, the pipeline gradually acquires data enrichment logic, conditional filtering, and format-specific optimizations. The original intent—simple format conversion—has drifted into a complex ETL process without any explicit decision to change scope.

**Path Logic.** Gradual deviation. Each iteration is locally reasonable; the cumulative trajectory diverges from the original anchor.

#### 4.1.7 Intent Collision

**Definition.** Intent Collision occurs when conflicting intents from different agents, iterations, or generation sessions coexist within the same system, producing contradictory directives that cannot be simultaneously satisfied.

**Distinction.** Intent Collision is a multi-source conflict. It arises in environments where multiple developers use AI generation independently, or where successive generation sessions produce artifacts guided by incompatible assumptions about system behavior, architecture, or requirements.

**Example.** Developer A prompts an AI to generate a module following an event-driven architecture. Developer B independently prompts an AI to generate an adjacent module assuming synchronous request-response communication. Both modules are integrated into the same system. The conflicting architectural assumptions produce subtle integration failures that neither developer anticipated, because each module is internally consistent with its own generative context.

**Path Logic.** Conflicting direction. Multiple generation sources introduce incompatible intent vectors into a shared system.

#### 4.1.8 Intent Degradation Path

The seven intent-layer phenomena are not independent. They form a causal degradation path:

Ghost Intent creates unanchored implementation conditions—artifacts whose purpose cannot be verified or challenged. Unanchored implementation provides fertile ground for Inference Creep, which expands scope without authorization, and for Semantic Expansion, which broadens meaning without declaration. These expansions accelerate Intent Fragmentation as the now-expanded scope scatters across modules. Fragmented intent enables Scope Absorption, as boundaries become unclear enough for adjacent concerns to be silently incorporated. Across iterations, the accumulated effect manifests as Intent Drift. When multiple agents or sessions contribute drifting artifacts, Intent Collision becomes inevitable.

The path logic is: **absence → overreach → scattering → absorption → drift → collision**.

---

### 4.2 Structural Layer Degradation

The structural layer concerns the topology and architecture of the software system: its module boundaries, dependency relationships, interface contracts, and pattern consistency. Structural-layer degradation arises when AI-generated artifacts introduce architectural anomalies that erode the system's structural coherence and evolvability.

#### 4.2.1 Ghost Code

**Definition.** Ghost Code is code whose purpose is indeterminate. It exists in the codebase, may be syntactically valid and executable, but its intended function, design rationale, or architectural role cannot be recovered from any available source.

**Distinction.** Ghost Code is distinct from dead code. Dead code is **unreachable**—it will never execute regardless of system state. Ghost Code may execute, produce output, and affect system behavior, but its **interpretability is indeterminate**: no available information can establish what it is meant to do or why it exists.

In human-authored systems, the interpretability of ambiguous code can often be reconstructed through authorship memory—asking the original developer, consulting design documents, or reviewing commit messages. In AI-generated systems, that reconstruction pathway is structurally absent. The code exists without recoverable origin, purpose, or justification.

**Example.** An AI-generated module contains a helper function that performs a series of string manipulations on configuration values before passing them to the main logic. The manipulations are syntactically correct and the function executes without error, but no documentation, test, requirement, or prompt explains what the manipulations accomplish or why they are necessary. The function is a ghost: present, active, and opaque.

**Path Logic.** Interpretability indeterminate. The degradation lies not in incorrectness but in the impossibility of confirming correctness.

#### 4.2.2 Architectural Amnesia

**Definition.** Architectural Amnesia occurs when conflicting implicit architectural models coexist within the same system, each reflecting the assumptions of a different generation context.

**Distinction.** In traditional development, architectural inconsistency typically results from deliberate (if ill-advised) design decisions or gradual erosion over time with awareness of the divergence. Architectural Amnesia is distinctive because the conflicting models are introduced simultaneously and unconsciously—each generation session produces artifacts consistent with its own implicit architectural model, without awareness that other sessions have embedded different models into the same system.

**Example.** One generation session produces data access code following the Repository pattern. A subsequent session generates data access code for a related entity using the Active Record pattern. Both coexist in the same codebase. Neither is "wrong" in isolation, but their coexistence introduces conflicting assumptions about data access architecture that confuse future maintenance and impede refactoring.

**Path Logic.** Conflicting mental models. Multiple implicit architectural assumptions are embedded without reconciliation.

#### 4.2.3 Rigidity Calcification

**Definition.** Rigidity Calcification is the unconscious standardization of structural patterns that progressively reduces the system's capacity for evolutionary adaptation.

**Distinction.** Rigidity Calcification differs from technical debt in a critical dimension: technical debt involves **conscious** trade-offs where developers knowingly accept suboptimal solutions. Calcification emerges from **unconscious** cumulative pattern uniformity—the model's tendency to reproduce similar structural templates across different generation events, regardless of whether the template is appropriate for each specific context.

**Example.** An AI generates CRUD (Create, Read, Update, Delete) scaffolding for every data entity in a system, even for entities that require specialized processing, event-driven workflows, or read-only access patterns. Over time, the uniform CRUD pattern becomes so deeply embedded that introducing a different access pattern for any entity requires fighting the structural assumptions of the entire codebase.

**Path Logic.** Cumulative pattern uniformity. Repeated application of the same structural template, regardless of contextual appropriateness, progressively reduces the system's capacity to accommodate structural variation.

#### 4.2.4 Shadow Coupling

**Definition.** Shadow Coupling refers to undeclared dependency paths between components—dependencies that are not expressed through formal interfaces, import statements, or architectural documentation but exist through implicit channels such as shared global state, assumed execution order, or convention-based naming.

**Distinction.** Shadow Coupling is distinct from known coupling that is merely poorly documented. In Shadow Coupling, the dependency path is **structurally invisible**: it does not appear in dependency graphs, import analysis, or interface inspection. It exists only in the runtime behavior of the system, mediated by implicit assumptions embedded during generation.

**Example.** Module A, generated in one session, writes to a shared in-memory cache using a specific key naming convention. Module B, generated in a different session, reads from the same cache using the same naming convention. No interface, API contract, or documented dependency connects A and B. The coupling exists solely through the coincidence of naming conventions embedded by the model's distributional patterns.

**Path Logic.** Undeclared dependencies. The coupling is real but architecturally invisible.

#### 4.2.5 Interface Erosion

**Definition.** Interface Erosion is the incremental blurring of module boundaries and interface contracts through successive generation events, each of which slightly expands, overlaps, or reinterprets the responsibilities defined by the original interface.

**Distinction.** Interface Erosion is a gradual process, not a sudden break. Each individual generation event may respect the interface to a reasonable approximation, but the cumulative effect of multiple events is a progressive loss of boundary clarity.

**Example.** A service interface initially exposes three methods with clearly defined input/output contracts. Through successive iterations of AI-assisted feature addition, the interface grows to twelve methods, several of which overlap in functionality, accept inconsistent parameter formats, and return differently shaped response objects. The original boundary clarity has eroded into an amorphous surface.

**Path Logic.** Incremental boundary blurring. Each generation event contributes a small boundary violation; the accumulated effect is architectural ambiguity.

#### 4.2.6 Dependency Blindness

**Definition.** Dependency Blindness occurs when AI-generated code incorporates implicit assumptions about external dependencies—APIs, libraries, services, runtime environments—that remain hidden until the assumed conditions change and the dependency fails.

**Distinction.** Dependency Blindness is not simply poor documentation of known dependencies. It concerns dependencies whose very existence is not recognized until failure reveals them. The generated code embeds assumptions about external behavior that are never made explicit, tested in isolation, or documented as preconditions.

**Example.** AI-generated code assumes that a third-party API returns results in a specific order—an undocumented behavior of the current API version. When the API provider releases a new version that returns results in a different order, the generated code fails silently, producing incorrect results without error signals. The dependency on result ordering was never declared, tested, or documented; it existed only as an implicit assumption embedded during generation.

**Path Logic.** Fragile implicit assumptions. Dependencies exist as embedded assumptions rather than declared contracts, surfacing only upon failure.

#### 4.2.7 Structural Degradation Path

The six structural-layer phenomena form a causal chain:

Architectural Amnesia introduces conflicting implicit models into the codebase. These conflicting models resist reconciliation through refactoring, and over time the path of least resistance—regenerating similar patterns—leads to Rigidity Calcification. Calcified structures force workarounds that bypass formal interfaces, creating Shadow Coupling. Shadow Coupling blurs the boundaries between modules, accelerating Interface Erosion. Eroded interfaces expose the system to external fragilities that were previously contained, manifesting as Dependency Blindness. Throughout this chain, Ghost Code accumulates as the structural byproduct of repeated generation events whose artifacts cannot be fully interpreted.

The path logic is: **conflicting models → calcification → undeclared coupling → boundary erosion → exposed fragility**.

---

### 4.3 Behavioral Layer Degradation

The behavioral layer is a **manifestation layer**: runtime instabilities that are often symptomatic of upstream degradation in the intent or structural layers. Behavioral-layer phenomena are typically the first to be observed, but the last to be properly diagnosed, because their root causes lie in deeper layers.

#### 4.3.1 Conditional Blindspot

**Definition.** Conditional Blindspot is the systematic omission of rare boundary cases, edge conditions, and exceptional paths in AI-generated code.

**Distinction.** Conditional Blindspot is not a random bug that happens to miss an edge case. The omission is **systematic**: it correlates with the generative distribution. Cases that are underrepresented in training data—rare error conditions, unusual input combinations, platform-specific edge cases—are systematically less likely to be generated. The bias is structural, not accidental.

**Example.** AI-generated form validation handles standard inputs correctly but consistently omits handling for: inputs at exact boundary lengths, Unicode edge cases, concurrent submission scenarios, and browser-specific parsing differences. Each omission individually could be an oversight; their systematic co-occurrence reveals a distributional bias.

**Path Logic.** Omission bias. The generation distribution systematically underweights conditions that are rare in training data, regardless of their importance in the target system.

#### 4.3.2 State Assumption Leak

**Definition.** State Assumption Leak occurs when AI-generated code embeds implicit assumptions about system state that hold under typical execution sequences but fail under specific, non-obvious sequences.

**Distinction.** State Assumption Leak is not a simple concurrency bug or race condition (which can be identified through standard concurrency analysis). It concerns **hidden state assumptions that are invisible until a specific execution sequence violates them**. The assumed state invariant is never declared, never tested, and may hold for the vast majority of executions—failing only under conditions that are difficult to anticipate or reproduce.

**Example.** AI-generated code for a payment processing workflow assumes that the user profile has been loaded into a cache by a prior step in the workflow. Under normal sequential execution, this assumption holds. Under a specific sequence—where a timeout triggers a retry that skips the cache-loading step—the assumption fails, producing a null reference that corrupts the transaction state. The assumption was never declared; the failure sequence was never tested.

**Path Logic.** Sequence-dependent violation. The degradation lies dormant under typical sequences and activates under specific, non-obvious execution paths.

#### 4.3.3 Observation Bias

**Definition.** Observation Bias occurs when AI-generated monitoring, logging, and observability code is systematically aligned with expected behaviors while neglecting anomalous or unexpected conditions.

**Distinction.** Observation Bias is not incomplete logging (a random gap in coverage) and not a monitoring configuration error (a known deficiency). It is **directional**: the generated observability infrastructure is shaped by the same distributional tendencies that shape the code itself. Expected paths are thoroughly monitored; unexpected paths are systematically invisible.

**Example.** AI-generated observability code for a microservice logs response times, success counts, and standard error codes. It does not log: partial failures, degraded responses that still return 200 status codes, silent data truncation, or latency spikes in downstream dependencies. The monitoring creates an illusion of system health by observing only the dimensions that confirm expected behavior.

**Path Logic.** Expectation-driven monitoring. The observability infrastructure mirrors the generation distribution's bias toward common paths, systematically excluding the anomalous conditions that most need observation.

#### 4.3.4 Non-Deterministic Degradation

**Definition.** Non-Deterministic Degradation is a pattern of behavioral instability in which system behavior is neither consistently correct nor consistently incorrect, but varies depending on load, timing, execution sequence, and environmental conditions.

**Distinction.** Non-Deterministic Degradation is not a localized bug (which produces consistent failure under consistent conditions). It is a **systemic instability** that defies deterministic reproduction. The system appears to work correctly under test conditions but fails intermittently under production conditions, without a single identifiable cause.

**Example.** A system integrating multiple AI-generated microservices exhibits intermittent data inconsistencies. Under normal load, all services return consistent results. Under elevated load, subtle timing differences between services cause race conditions in shared state access, producing inconsistencies that appear randomly and cannot be reliably reproduced in isolation. The root cause is not any single service but the interaction between multiple services, each carrying hidden state assumptions from its generation context.

**Path Logic.** Load and sequence dependent instability. The degradation manifests as a property of the system's dynamic behavior rather than its static structure.

#### 4.3.5 Confidence Propagation

**Definition.** Confidence Propagation occurs when a system continues to express certainty—returning definitive results, asserting success, suppressing error signals—despite the progressive degradation of its underlying assumptions.

**Distinction.** Confidence Propagation is the most insidious form of behavioral degradation because it **suppresses the signals that would otherwise trigger detection and remediation**. The system does not fail; it continues to operate with apparent confidence, masking the degradation that is accumulating beneath.

**Example.** An AI-generated recommendation engine incorporates multiple data sources, each accessed through generated integration code. As upstream data quality degrades—one source returns stale data, another silently drops fields—the recommendation engine continues to produce results with unchanged confidence scores. No error is raised, no confidence metric degrades, and no alert fires. The system's expressed certainty is inversely correlated with its actual reliability.

**Path Logic.** Suppressed error signals. Degradation in upstream assumptions does not propagate as reduced confidence in downstream outputs; instead, the system's error-signaling mechanisms are too weak—or too narrowly scoped—to detect the degradation.

#### 4.3.6 Behavioral Degradation Path

The five behavioral-layer phenomena form a terminal degradation path:

Conditional Blindspot creates systematic gaps in coverage. These gaps expose hidden State Assumption Leaks that would otherwise remain dormant. The failure to observe these leaks—due to Observation Bias in the monitoring infrastructure—allows them to recur and accumulate. Accumulated, unobserved state violations produce Non-Deterministic Degradation: intermittent, irreproducible instability. Finally, Confidence Propagation ensures that even as the system's behavior becomes increasingly unreliable, its outputs continue to express certainty, suppressing the detection signals that would trigger intervention.

Confidence Propagation is the terminal node in this path because it creates a **feedback suppression loop**: the worse the degradation, the more critical detection becomes, yet the system's expressed confidence actively prevents detection.

The path logic is: **systematic omission → hidden violation → biased observation → intermittent instability → false certainty**.

---

### 4.4 Taxonomy Summary

Table 1 summarizes all eighteen degradation phenomena across the three layers:

| Layer      | Phenomenon                    | Definition                                                         | Path Logic                            |
| ---------- | ----------------------------- | ------------------------------------------------------------------ | ------------------------------------- |
| Intent     | Ghost Intent                  | Executable artifact whose originating decision cannot be recovered | Static Absence                        |
| Intent     | Inference Creep               | Generation exceeds explicit instruction boundaries                 | Probabilistic Overreach               |
| Intent     | Semantic Expansion            | Conceptual meaning broadens during generation                      | Beyond Declared Meaning               |
| Intent     | Intent Fragmentation          | Intent exists but is structurally dispersed                        | Origin Present, Cohesion Absent       |
| Intent     | Scope Absorption              | Adjacent concerns absorbed without explicit declaration            | Implicit Inclusion                    |
| Intent     | Intent Drift                  | Gradual deviation across iterations                                | Gradual Deviation                     |
| Intent     | Intent Collision              | Conflicting intents across agents or iterations                    | Conflicting Direction                 |
| Structural | Ghost Code                    | Code whose purpose is indeterminate                                | Interpretability Indeterminate        |
| Structural | Architectural Amnesia         | Conflicting implicit architectural models coexist                  | Conflicting Mental Models             |
| Structural | Rigidity Calcification        | Unconscious pattern standardization reduces evolvability           | Cumulative Pattern Uniformity         |
| Structural | Shadow Coupling               | Undeclared dependency paths                                        | Undeclared Dependencies               |
| Structural | Interface Erosion             | Incremental boundary blurring                                      | Incremental Boundary Blurring         |
| Structural | Dependency Blindness          | Implicit external assumptions surface only upon failure            | Fragile Implicit Assumptions          |
| Behavioral | Conditional Blindspot         | Systematic omission of rare boundary cases                         | Omission Bias                         |
| Behavioral | State Assumption Leak         | Hidden state assumptions violated under specific sequences         | Sequence-Dependent Violation          |
| Behavioral | Observation Bias              | Monitoring aligned with expected behaviors, ignoring anomalies     | Expectation-Driven Monitoring         |
| Behavioral | Non-Deterministic Degradation | Behavior neither consistently correct nor incorrect                | Load & Sequence Dependent Instability |
| Behavioral | Confidence Propagation        | System expresses certainty despite degraded assumptions            | Suppressed Error Signals              |

*Table 1: Three-Layer Taxonomy of Structural Degradation Phenomena*

![Figure 4.1: Structural degradation propagates downward through intent, structural, and behavioral layers. Rooted in Stateless Generation vs Stateful Evolution.](../images/structural-degradation-01.png)

*Figure 4.1: Structural degradation propagates downward through intent, structural, and behavioral layers. Rooted in Stateless Generation vs Stateful Evolution.*

---

## 5. Cross-Layer Degradation Dynamics

The eighteen phenomena defined in Section 4 do not exist in isolation. They propagate across layers through identifiable causal mechanisms. Understanding these cross-layer dynamics is essential for diagnosing root causes, designing effective interventions, and avoiding the common error of treating symptoms while leaving causes intact.

### 5.1 Primary Direction: Downward Propagation

Degradation propagates primarily **downward**: from Intent through Structural to Behavioral layers.

This directionality is not incidental. It reflects a fundamental asymmetry: **abstraction loss is easier than abstraction reconstruction**. When intent-layer instability embeds into structural artifacts—through code generation, pattern replication, and iterative refinement—the original intent context is progressively lost. Recovering that context from the resulting structure requires reconstruction of information that was never explicitly encoded, a task whose difficulty grows exponentially with each layer transition.

The downward propagation principle has a critical practical implication: **interventions at the behavioral layer cannot reverse upstream degradation**. Fixing a runtime symptom does not repair the structural anomaly that produced it, nor does it recover the intent instability that enabled the structural anomaly. Effective remediation must target the originating layer.

![Figure 5.1: Degradation propagates from the Intent Layer to the Behavioral Layer.](../images/structural-degradation-03.png)

*Figure 5.1: Degradation propagates from the Intent Layer to the Behavioral Layer.*

### 5.2 Intent → Structural Propagation

The mechanism by which intent-layer degradation propagates into the structural layer can be illustrated through a characteristic pathway:

1. **Inference Creep** generates functionality beyond instruction boundaries, which through **Scope Absorption** silently incorporates adjacent concerns.
2. The absorbed logic, having been generated once, serves as a template for future generation events. Through repeated regeneration, the absorbed patterns standardize into structural templates, producing **Rigidity Calcification**.
3. Calcified structures resist adaptation. When the system must accommodate new requirements that conflict with the calcified patterns, the rigidity prevents structural accommodation, creating conditions for later behavioral instability.

This pathway demonstrates how a seemingly minor intent-layer phenomenon (scope expansion) can, through structural embedding and calcification, produce systemic evolvability loss.

### 5.3 Structural → Behavioral Propagation

The mechanism by which structural-layer degradation propagates into behavioral instability follows a characteristic pattern:

1. **Shadow Coupling** creates hidden state dependencies between components connected through undeclared channels.
2. Under stress—increased load, unusual execution sequences, environmental variation—these hidden dependencies trigger **State Assumption Leaks**: implicit state invariants are violated because the coupling path was never designed to handle the stress condition.
3. Repeated state assumption leaks, each occurring under slightly different conditions, accumulate into **Non-Deterministic Degradation**: the system exhibits intermittent failures that cannot be traced to any single cause because the cause is distributed across multiple shadow coupling paths.

This pathway demonstrates how structurally invisible coupling can produce behaviorally visible instability that defies conventional debugging approaches.

### 5.4 Behavioral → Intent/Structural: Diagnostic Pathway

While the primary propagation direction is downward, behavioral failures frequently **reveal** upstream degradation in the structural and intent layers. A runtime failure may be the first observable signal that an architectural anomaly exists, or that an intent-layer instability has embedded into the system.

However, this upward signal is **diagnostic, not causal**. The behavioral failure does not cause the structural or intent-layer issue; it makes it visible. This distinction is critical for remediation strategy:

- Behavioral intervention (fixing the runtime symptom) provides immediate relief but does not address the cause.
- Structural intervention (repairing the architectural anomaly) prevents recurrence of the specific symptom but may leave the intent-layer instability intact.
- Intent-layer intervention (recovering, clarifying, or re-establishing the originating decision) addresses the root cause but requires the most effort and the deepest understanding.

Effective governance must support **cross-layer traceability**: the ability to follow a behavioral signal upward through structural conditions to its intent-layer origin.

---

## 6. Visibility Inversion Principle

The cross-layer dynamics described in Section 5 give rise to a governing principle that we term the **Visibility Inversion Principle**:

> The probability of detecting degradation is inversely proportional to the depth of the layer at which it originates.  
> The magnitude of damage caused by degradation is directly proportional to the depth of the layer at which it manifests as failure.

### 6.1 Detection Difficulty

Behavioral-layer phenomena are the easiest to detect: they produce observable symptoms—runtime errors, performance degradation, inconsistent outputs—that trigger alerts and attract attention. Structural-layer phenomena are harder to detect: they require architectural analysis, dependency inspection, and pattern recognition that go beyond standard testing. Intent-layer phenomena are the hardest to detect: they require recovery of originating decisions, comparison against specifications, and evaluation of conceptual coherence—activities that are rarely automated and difficult to perform at scale.

Detection difficulty is thus **inversely proportional to origination layer depth**: the deeper the origin, the harder the detection.

### 6.2 Damage Magnitude

Paradoxically, the damage relationship runs in the opposite direction. Intent-layer degradation, if caught early, is cheap to remediate: clarifying a requirement, constraining a prompt, or re-establishing a design boundary may suffice. Structural-layer degradation requires more extensive intervention: refactoring modules, rebuilding interfaces, or restructuring dependencies. Behavioral-layer failures, especially those arising from accumulated cross-layer degradation, can be the most costly: they may require simultaneous intervention across multiple layers, emergency response under production conditions, and extensive regression testing.

Damage magnitude is thus **directly proportional to failure layer depth**: the deeper the failure manifests, the greater the damage.

![Figure 6.1: As system layer depth increases, detection difficulty decreases while damage potential increases, illustrating the Visibility Inversion Principle.](../images/structural-degradation-04.png)

*Figure 6.1: As system layer depth increases, detection difficulty decreases while damage potential increases, illustrating the Visibility Inversion Principle.*

### 6.3 Governance Implications

The Visibility Inversion Principle implies that **governance cost increases with layer depth**. The most cost-effective governance strategy is to invest in early detection at the intent layer, where degradation is hardest to see but cheapest to fix. Conversely, relying on behavioral-layer detection—the easiest approach—is the most expensive, because by the time degradation manifests as behavioral failure, it has already propagated through structural layers and accumulated compound effects.

Effective governance requires:
- **Cross-layer root cause tracing**: the ability to follow behavioral symptoms back through structural conditions to intent-layer origins.
- **Intent-layer early detection**: mechanisms that identify ghost intent, inference creep, semantic expansion, and other intent-layer phenomena before they embed into structure.
- **Proactive rather than reactive monitoring**: observability that looks for absence (missing intent, undeclared dependencies) rather than only presence (runtime errors, performance thresholds).

### 6.4 Architectural Implications

From an architectural perspective, the Visibility Inversion Principle demands:
- **Explicit state mechanisms**: architectures must make deep-layer states visible. Intent assumptions, architectural decisions, and generation contexts must be captured in machine-readable form, not left implicit.
- **Cross-layer tracking infrastructure**: the architecture must support traceability from behavioral outputs through structural topology to intent origins. This requires instrumentation that spans all three layers.
- **Generation context preservation**: the conditions under which AI generates code—the prompt, the context window, the model version, the system snapshot—must be recorded as first-class architectural metadata.

### 6.5 Process Implications

For software development processes, the Visibility Inversion Principle implies:
- **Shallow-layer verification**: verification activities must be introduced at the intent layer—not merely at the testing (behavioral) layer. Prompt review, generation scope validation, and intent consistency checking must become standard process activities.
- **Degradation-aware CI/CD**: continuous integration and deployment pipelines must incorporate degradation monitoring beyond functional testing. Structural analysis (dependency drift, boundary clarity, pattern diversity) and intent analysis (scope consistency, decision traceability) must be embedded in automated pipelines.
- **Periodic degradation assessment**: teams must periodically assess the structural health of systems that incorporate AI-generated code, looking specifically for the phenomena defined in this taxonomy.

---

## 7. Implications for Software Engineering

The root cause model, three-layer taxonomy, and cross-layer dynamics presented in this paper carry broad implications for software engineering research and practice.

### 7.1 Toward a Unified Ontology

The three-layer taxonomy provides a **coherent conceptual framework** for describing AI-generated code degradation. By organizing degradation phenomena across intent, structural, and behavioral layers, and by defining each phenomenon with precision, the taxonomy enables consistent communication about problems that have previously been described using ad hoc terminology.

More importantly, the taxonomy reveals the **limitations of traditional defect taxonomies** when applied to AI-generated code. Concepts such as "bug," "code smell," or "technical debt" were developed for human-authored systems with persistent authorship and cumulative evolution. Applying these concepts to AI-generated code degradation leads to systematic misclassification: intent-layer phenomena are misclassified as specification gaps; structural-layer phenomena are misclassified as refactoring opportunities; behavioral-layer phenomena are misclassified as isolated bugs. Each misclassification leads to misaligned remediation—interventions that address the wrong layer, at the wrong time, with predictable ineffectiveness.

### 7.2 Diagnostic Orientation

The three-dimensional discontinuity model (temporal, authorial, state) provides a **diagnostic lens** for identifying and preventing degradation root causes. When a development team observes degradation symptoms, the discontinuity model directs inquiry to specific questions:

- **Temporal**: Has the generation process been isolated from the system's evolutionary history? Are regeneration events cumulatively coherent or independently optimized?
- **Authorial**: Can the originating decisions for generated artifacts be recovered? Is there a traceable chain from requirement to prompt to artifact?
- **State**: Was the system's full state—including implicit constraints and accumulated invariants—accessible to the generation context? Or was generation performed against a partial snapshot?

These diagnostic questions guide root cause analysis toward the actual origin of degradation, rather than its symptomatic manifestation.

### 7.3 Architectural Innovation

The taxonomy implies the need for new architectural principles adapted to the realities of AI-generated artifact integration:

- **Isolate Non-Cumulative Integration.** AI-generated artifacts should be integrated through isolation boundaries that prevent cumulative structural corruption. Generated code should be treated as provisional until architecturally validated.
- **Explicit Evolution Constraint.** Architectural constraints that are currently implicit—module boundaries, interface contracts, dependency rules—must be made explicit and machine-enforceable, because the generative process cannot infer implicit constraints from context alone.
- **Dynamic Authorial Traceability.** The conventional assumption that authorship can be reconstructed from version control must be supplemented with explicit generation context records: what was prompted, what was generated, under what context, and with what model.

### 7.4 Governance Transformation

The cross-layer propagation model and Visibility Inversion Principle demand a transformation in how AI-assisted development is governed:

- **Cross-layer degradation tracing** must become a core governance capability, enabling teams to follow behavioral signals through structural conditions to intent origins.
- **Combined static and dynamic analysis** must be deployed: static analysis to detect structural anomalies (ghost code, shadow coupling, interface erosion) and dynamic analysis to detect behavioral instabilities (state assumption leaks, non-deterministic degradation, confidence propagation).
- **Observability must be redefined** to include degradation-awareness. Current observability focuses on system health metrics (uptime, latency, error rates). Degradation-aware observability must additionally monitor structural health (boundary clarity, dependency stability, pattern diversity) and intent health (decision traceability, scope coherence).
- **Intent-layer early detection** must be prioritized, as the Visibility Inversion Principle demonstrates that governance investment at the intent layer yields the highest return.

### 7.5 Process Optimization

The taxonomy implies the need for new activities within the software development life cycle:

- **Generated Artifact Consistency Audit**: periodic review of AI-generated artifacts for internal consistency, architectural alignment, and intent traceability.
- **Explicit Architecture Assumption Validation**: verification that generated code respects declared (and implicit) architectural constraints, conducted as part of the integration process rather than deferred to testing.
- **Periodic Degradation Assessment**: scheduled evaluation of the system's structural health across all three layers, using the taxonomy as a diagnostic checklist. This assessment should be conducted at regular intervals, not only in response to observed failures.

---

## 8. Limitations

This paper presents a conceptual taxonomy, not an empirical study. Several limitations must be acknowledged.

**Conceptual rather than empirical foundation.** The taxonomy is constructed through theoretical analysis and conceptual reasoning, not through systematic empirical observation. While the phenomena described are grounded in observable patterns of AI-assisted development, no formal empirical validation has been conducted. Future work must subject the taxonomy to empirical testing through case studies, controlled experiments, and longitudinal observation of AI-assisted software projects.

**Boundary ambiguity at the intent layer.** Some intent-layer phenomena—particularly the boundaries between Inference Creep, Semantic Expansion, and Scope Absorption—may overlap in practice. While they are conceptually distinct (as argued in Section 4.1), their operational differentiation in specific cases may require further refinement. Future work should develop more precise operational criteria for distinguishing these phenomena.

**Assumption of long-lived evolving systems.** The taxonomy assumes that AI-generated artifacts are integrated into long-lived systems that undergo sustained evolution. For short-lived, disposable, or prototype systems—where long-term structural coherence is not a design goal—the full degradation dynamics may not manifest. The applicability of this taxonomy to such systems remains an open question.

**Absence of quantitative measurement.** This paper defines and categorizes degradation phenomena but does not propose metrics for measuring their severity, prevalence, or rate of accumulation. The development of a quantitative measurement framework for structural degradation is a necessary next step for making the taxonomy practically actionable.

**No prevention or mitigation mechanisms.** The scope of this paper is diagnostic, not prescriptive. We identify and categorize degradation phenomena but do not design prevention strategies, mitigation mechanisms, or governance frameworks. These are essential directions for future research, which can build upon the conceptual foundation established here.

---

## 9. Conclusion

This paper has addressed a gap in the current understanding of AI-assisted software engineering: the absence of a unified, systematic account of the degradation mechanisms unique to AI-generated code.

We have made the following contributions:

1. **Root Cause Model.** We identified the fundamental cause of structural degradation as a three-dimensional discontinuity—temporal, authorial, and state-based—arising from the interaction between stateless generation and stateful system evolution. This model explains why AI-generated code degradation is qualitatively distinct from traditional software decay.

2. **Three-Layer Taxonomy.** We constructed a systematic taxonomy of eighteen degradation phenomena organized across Intent, Structural, and Behavioral layers. Each phenomenon is defined with precision, differentiated from adjacent concepts, and situated within a causal degradation path.

3. **Cross-Layer Propagation Model.** We demonstrated that degradation propagates primarily downward through the layer stack via identifiable causal mechanisms, and that behavioral failures serve as diagnostic signals of upstream degradation rather than independent causes.

4. **Visibility Inversion Principle.** We articulated the principle that detection ease and damage magnitude are inversely related across layers: intent-layer degradation is hardest to detect but cheapest to remediate, while behavioral-layer failure is easiest to observe but most expensive to address.

5. **Conceptual Differentiation.** We established that structural degradation is a distinct concept, not reducible to bugs, technical debt, dead code, or hallucination—each of which addresses a different phenomenon under different assumptions.

The central argument of this paper is that without a **layered ontology**, AI-generated code degradation will be systematically misclassified under traditional defect categories, leading to misaligned remediation strategies that address symptoms rather than causes. The taxonomy presented here provides the conceptual vocabulary necessary for accurate classification, enabling future work in governance, architecture, process design, and empirical analysis.

Future research directions include:

- **Empirical validation**: systematic case studies and controlled experiments to test the taxonomy's descriptive accuracy and diagnostic utility.
- **Phenomenon expansion**: identification of additional degradation phenomena as AI-assisted development practices evolve.
- **Governance framework design**: development of actionable governance frameworks that operationalize the Visibility Inversion Principle.
- **Process integration**: design of SDLC activities, tools, and automated checks that embed degradation awareness into standard development workflows.
- **Measurement framework**: development of quantitative metrics for assessing degradation severity, prevalence, and progression across the three layers.

---

## 10. Related Work

This section situates the present work within the broader landscape of relevant research and identifies the specific contributions that distinguish it from prior work.

### 10.1 AI-Assisted Software Engineering

The growing body of research on AI-assisted software engineering has primarily focused on productivity, code correctness, and developer experience. Studies have examined the effectiveness of LLM-based code generation tools in producing functionally correct code (Chen et al., 2021; Vaithilingam et al., 2022), the quality characteristics of AI-generated code (Yetiştiren et al., 2023), and the integration of AI tools into developer workflows. This literature provides valuable insights into the capabilities and limitations of generative AI for code production, but it does not address the **structural degradation dynamics** that emerge when AI-generated artifacts are integrated into evolving systems over time. The present work complements this literature by shifting focus from individual artifact quality to systemic degradation patterns.

### 10.2 Software Architecture Decay

Software architecture decay—also termed architecture erosion, drift, or degradation—has been studied extensively in the context of human-authored systems (Perry & Wolf, 1992; Hochstein et al., 2005; de Silva & Balasubramaniam, 2012). Classical models describe how architectural constraints are progressively violated through human decision-making over time, and how to detect and remediate such violations. This paper introduces an **AI-generated code perspective** to the architecture decay literature, identifying decay mechanisms that are specific to the stateless generation / stateful evolution mismatch and that are not accounted for in existing models of architecture erosion.

### 10.3 Technical Debt Management

Technical debt, as conceptualized by Cunningham (1992) and elaborated by subsequent researchers (Li et al., 2015; Coplien, 1996), presupposes conscious trade-off decisions by human developers. The management of technical debt focuses on making these trade-offs visible, quantifiable, and manageable over time. The structural degradation phenomena identified in this paper differ in a fundamental way: they arise **without conscious human trade-off**. The taxonomy goes beyond the single concept of technical debt to articulate **multi-layer degradation dynamics** in which unconscious structural decay accumulates across intent, structure, and behavior simultaneously.

### 10.4 Software Evolution Governance

Research on software evolution governance, including Lehman's Laws of Software Evolution (Belady & Lehman, 1976) and subsequent work on managing long-term system sustainability, addresses how systems change over time and how governance can maintain quality through change. This literature assumes human-directed evolution with recoverable decision trails. The present work proposes a **stateless-aware governance framework** that specifically addresses the governance challenges introduced by AI-generated artifacts: the absence of recoverable authorship, the non-cumulative nature of generation-driven integration, and the need for cross-layer degradation tracing.

### 10.5 AI Testing and Verification

Recent work on testing and verifying AI-generated code (Shumailov et al., 2023; Shukla et al., 2025; Abbassi et al., 2025) has explored security vulnerabilities, inefficiency patterns, and correctness deficiencies in LLM-generated code. These contributions identify important quality issues at the artifact level. The present work extends this line of inquiry by revealing **new testing and verification requirements** that arise from structural degradation: the need to test for cross-layer propagation effects, the need to verify intent consistency across generation iterations, and the need to assess behavioral stability under conditions that expose hidden state assumptions.

### 10.6 Software Modularity and Decomposition

The foundational work on software modularity (Parnas, 1972) established information hiding as a principle for managing complexity through boundary preservation. Brooks (1975) articulated the essential difficulties of software development, including conceptual integrity. The structural degradation phenomena described in this paper—particularly Interface Erosion, Shadow Coupling, and Architectural Amnesia—represent new threats to the modularity principles established by this classical literature, threats that arise specifically from the AI generation context.

### 10.7 Ontological Approaches to Software Engineering

Gruber's (1993) foundational work on portable ontologies provides the methodological grounding for this paper's taxonomic approach. By constructing a coherent ontology of degradation phenomena—with precise definitions, explicit distinctions, and identified relationships—the present work follows the ontological tradition of building shared conceptual frameworks that enable consistent communication and cumulative knowledge building within a domain.

---

## References

[1] Abbassi, A., et al. (2025). A Taxonomy of Inefficiencies in LLM-Generated Code. *arXiv preprint*.

[2] Belady, L. A., & Lehman, M. M. (1976). A Model of Large Program Development. *IBM Systems Journal*, 15(3), 225–252.

[3] Brooks, F. P. (1975). *The Mythical Man-Month: Essays on Software Engineering*. Addison-Wesley.

[4] Chen, M., et al. (2021). Evaluating Large Language Models Trained on Code. *arXiv preprint arXiv:2107.03374*.

[5] Coplien, J. O. (1996). Software Patterns: Gardening and the Concept of Design Debt. *Bell Labs Technical Journal*, 1(2), 156–169.

[6] Cunningham, W. (1992). The WyCash Portfolio Management System. *ACM SIGPLAN OOPS Messenger*, 4(2), 29–30.

[7] de Silva, L., & Balasubramaniam, D. (2012). Controlling Software Architecture Erosion: A Survey. *Journal of Systems and Software*, 85(1), 132–151.

[8] Gruber, T. R. (1993). A Translation Approach to Portable Ontologies. *Knowledge Acquisition*, 5(2), 199–220.

[9] Hochstein, L., Lindvall, M., & Basili, V. R. (2005). Detecting Architectural Degradation Patterns During Software Evolution. *Proceedings of the IEEE International Conference on Software Maintenance (ICSM)*, 193–202.

[10] Li, Z., Avgeriou, P., & Liang, P. (2015). A Systematic Mapping Study on Technical Debt and Its Management. *Journal of Systems and Software*, 101, 193–220.

[11] Parnas, D. L. (1972). On the Criteria To Be Used in Decomposing Systems into Modules. *Communications of the ACM*, 15(12), 1053–1058.

[12] Perry, D. E., & Wolf, A. L. (1992). Foundations for the Study of Software Architecture. *ACM SIGSOFT Software Engineering Notes*, 17(4), 40–52.

[13] Shukla, A., et al. (2025). Security Degradation in AI Code Generation: Patterns, Prevalence, and Implications. *arXiv preprint*.

[14] Shumailov, I., et al. (2023). The Curse of Recursion: Training on Generated Data Makes Models Forget. *arXiv preprint arXiv:2305.17493*.

[15] Vaithilingam, P., Zhang, T., & Glassman, E. L. (2022). Expectation vs. Experience: Evaluating the Usability of Code Generation Tools Powered by Large Language Models. *Proceedings of the CHI Conference on Human Factors in Computing Systems*.

[16] Yetiştiren, B., et al. (2023). Evaluating the Code Quality of AI-Assisted Code Generation Tools: An Empirical Study on GitHub Copilot, Amazon CodeWhisperer, and ChatGPT. *arXiv preprint*.
