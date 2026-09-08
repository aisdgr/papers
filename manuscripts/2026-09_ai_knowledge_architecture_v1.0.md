# AI Knowledge Architecture
> Why Organizations Do Not Yet Own the Knowledge Their AI Systems Produce

**Author:** Spark Tsai
**ORCID:** https://orcid.org/0009-0006-8847-4703
**Email:** spark.tsai@gmail.com

---

## Abstract

Organizations increasingly rely on large language models to interpret their own documents: requirements, policies, contracts, specifications, and operational records. Retrieval-augmented generation, knowledge graphs, and memory systems have made the underlying material far easier to reach. But reaching information is not the same as keeping what was concluded about it. When an AI system determines what a requirement means, which conditions it applies under, and how it relates to another commitment, that determination typically exists only inside the response it produced. The next interaction begins from the source text again.

The information persists. The interpretation does not.

This paper argues that the consequence is organizational rather than merely technical. If an accepted interpretation is never represented as anything other than a past model output, the organization cannot say which interpretations it has committed to, cannot distinguish an established position from a newly generated one, and cannot demonstrate afterwards why a particular reading was adopted. Interpretive work is performed repeatedly, paid for repeatedly, and owned by no one.

**AI Knowledge Architecture** addresses this by applying a governing principle: *once an interpretation has been explicitly established and accepted, it should not be re-inferred.* The architecture places an explicit admission boundary between interpretations an AI system proposes and interpretations an organization has accepted, and it externalizes accepted interpretations into persistent, inspectable structures — a stable identity for each knowledge assertion, explicit representation of the semantics that were resolved, the relationships that were accepted, the conditions under which those relationships hold, the basis on which they were accepted, and the recurring perspectives through which the same knowledge is organized for different roles.

The architecture does not attempt to make probabilistic AI deterministic, and it does not replace retrieval, knowledge graphs, provenance models, or ontology views. Retrieval locates material; AI reasoning proposes interpretations; admission determines which of them become governed knowledge; persistent structure allows later work to use accepted meaning without rebuilding it. An illustrative case — a single performance requirement read by architecture, business, product, and operations roles — shows how one shared knowledge state can support genuinely different interpretive organizations without fragmenting into separate stores, and how a cost-versus-capacity conflict becomes visible only when those organizations are compared.

**Keywords:** AI Governance; Enterprise AI; Knowledge Management; Organizational Knowledge; Accountability; Engineering Determinacy; Knowledge Representation; Large Language Models; Retrieval-Augmented Generation; Knowledge Graph

---

# 1. Introduction

An enterprise adopts an AI assistant to work over its requirements repository. Asked what a performance requirement means, the assistant answers well: it identifies the statement as a requirement rather than an observation, recognizes that *production* names an applicability environment, treats the stated figure as a target rather than a measurement, and distinguishes sustained load from transient burst capacity. The answer is used. A decision follows.

Three weeks later the same question arises in a different context, and the assistant is asked again. It may answer the same way. It may not. Nothing in the system requires the second answer to match the first, because nothing recorded that the first answer had been accepted.

This is the situation the present paper addresses. Retrieval-Augmented Generation (RAG) retrieves external information and supplies it as context during inference [1, 2]. Graph-based retrieval architectures additionally extract entities and relationships and organize corpus information into structures supporting summarization and query answering [3]. Knowledge graphs, memory systems, and external tools extend the informational environment further. All of these substantially improve **access to information**.

None of them makes the **persistence of interpretation** an architectural requirement.

The distinction matters because interpretation is where the organizationally meaningful work happens. Locating a requirement is retrieval. Deciding that it constrains another commitment, that the constraint holds only under sustained production load, and that this conclusion rests on a specific measurement — that is knowledge the organization has produced. If it exists only inside a past conversation, the organization has paid for it without acquiring it.

The problem compounds at three levels. At the level of a single assertion, resolved semantics stay implicit in the original sentence. At the relational level, an accepted conclusion that one commitment constrains another is rediscovered on each occasion, and the conditions limiting it, if never stated, quietly widen. At the level of perspective, a request to *analyze these requirements from an architecture perspective* obliges the model to reconstruct what an architecture perspective consists of, which knowledge belongs to it, and how that knowledge should be organized — every time it is asked.

This paper approaches all three through **Engineering Determinacy**, with the governing principle:

> **Once an interpretation has been explicitly established and accepted, it should not be re-inferred.**

The principle does not reject probabilistic reasoning. Probabilistic inference remains necessary wherever knowledge is ambiguous, incomplete, novel, contested, or not yet represented. What the principle separates is *discovering or revising an interpretation* from *reusing an interpretation that has already been accepted*. The first may require a model. The second should not.

> **A note on scope.** Engineering Determinacy is a general principle concerning the form in which established information exists; it is not specific to knowledge representation, and it is developed separately. The present paper applies it to one domain — the knowledge an AI system produces about an organization's own material — and proposes an architecture on that basis.

Based on this principle, the paper proposes **AI Knowledge Architecture**, a persistent knowledge architecture organized around a shared knowledge state, in which different structures externalize different classes of semantic uncertainty:

| Element         | Question otherwise repeatedly inferred                  | Determinacy role         |
| --------------- | ------------------------------------------------------- | ------------------------ |
| Claim Object    | Which knowledge assertion is this?                      | Semantic Identity        |
| Attribute       | What semantics are implicit in this assertion?          | Semantic Determinacy     |
| Relation        | Are these Claims related, and how?                      | Relational Determinacy   |
| Qualifier       | Under what conditions does this Relation hold?          | Boundary Determinacy     |
| Grounding Basis | Why was this Relation accepted?                         | Inspectable Basis        |
| Viewpoint       | How should this knowledge be interpreted and organized? | Interpretive Determinacy |
| Domain          | Which knowledge belongs to this Viewpoint?              | Deterministic Derivation |

The paper makes three contributions.

**C1 — Determinacy-driven architecture.** It proposes an architectural model in which Engineering Determinacy governs the transition from transient AI interpretation to persistent knowledge structure, with acceptance represented as an explicit organizational act rather than an implicit consequence of generation.

**C2 — Unified determinacy responsibilities.** Claim identity, semantic attributes, relations, qualifiers, grounding basis, viewpoints, and derived domains are not introduced as independent representation inventions. Each is well established as a representation mechanism. They are brought together here under a single architectural objective: externalizing different forms of already-resolved semantic uncertainty so that they no longer depend on repeated probabilistic reconstruction.

**C3 — Persistent interpretive structure over shared knowledge.** The architecture defines a Viewpoint as a persistent interpretive relational structure over a shared knowledge substrate, with Domains derived rather than independently maintained. This preserves common knowledge identity while allowing the different interpretive organizations that different organizational roles genuinely require.

The scope of the paper is architectural. It defines the persistent knowledge state and the structures through which accepted interpretation becomes reusable. It does not define complete algorithms for automatically constructing claims, resolving identity, accepting candidate relations, discovering viewpoints, reconciling conflicting evidence, or revising accepted knowledge. Those operations are identified as future work.

---

# 2. The Problem: Interpretation Does Not Persist

## 2.1 Retrieved Material Is Not Persistent Interpretation

Consider a source statement in a requirements repository:

> The production transaction service shall sustain 10,000 transactions per second.

Retrieval can locate this statement reliably. A language model can interpret it competently, deriving that it is a requirement rather than an observation, that *production* identifies an applicability environment, that ten thousand is a target rather than a historical measurement, that transactions per second is the operative metric, and that *sustain* distinguishes sustained load from transient burst capacity.

If those interpretations remain only inside a generated answer, a prompt context, or a temporary reasoning process, the next invocation begins from the original sentence again. The second interpretation may closely resemble the first. Nothing in the architecture requires it to be identical.

The problem is not that the second interpretation must be wrong. The problem is that a semantic question which had already been resolved has been returned, unnecessarily, to probabilistic inference.

## 2.2 Where Repeated Interpretation Occurs

**Assertion identity.** The system repeatedly asks which knowledge assertion a piece of material expresses. Text identity is a poor substitute for knowledge identity: different sentences may express the same proposition, and one sentence may contain several assertions. Without persistent assertion identity, downstream operations reason over textual artifacts rather than stable knowledge objects.

**Resolved semantics.** The system repeatedly asks which semantics are implicit in an assertion. In the example above, *production* functions as an environment, ten thousand as a target, transactions per second as a metric, and *sustain* as a load mode. Left embedded in natural language, each of these must be recovered again later.

**Relational interpretation.** The system repeatedly asks whether two assertions are related and how. That a connection pool supporting five hundred concurrent connections constrains a ten-thousand-transaction throughput requirement may be inferable, but if it is never persisted, every subsequent reasoning cycle may rediscover it.

**Applicability.** Even an explicit relation can leave the conditions of its validity unresolved. A capacity relationship valid under sustained production traffic may not hold under development traffic, batch processing, a different deployment topology, or a different software version. Implicit applicability invites silent generalization.

**Interpretive organization.** Finally, the system repeatedly asks which knowledge matters from a given perspective and how it should be arranged. An architect, a business analyst, a product manager, and an operations engineer may reason over the same assertions while selecting different semantics, emphasizing different relationships, and assigning different structural roles. If the perspective itself exists only in a prompt, it is reconstructed probabilistically whenever it is used.

## 2.3 Organizational Consequences

The consequences of repeated interpretation are usually discussed in technical terms. They are more consequential in organizational ones.

**The organization cannot say what it has concluded.** An interpretation that exists only as a past model output has no status. Asked which reading of a requirement the organization has adopted, there is no place to look — only a history of conversations, each internally plausible, none authoritative. The organization possesses the source documents and the transcripts, but not the conclusions drawn between them.

**An established position has no precedence over a new one.** Unless acceptance is itself represented, a freshly generated interpretation carries exactly the same weight as one that was carefully reviewed and adopted six months ago. The system offers no way to prefer the second over the first, because it holds no record that the second ever occurred. In practice this means that a decision reached with deliberation can be silently displaced by one reached in passing.

**Accountability has nothing to attach to.** When an interpretation later proves consequential — a commitment misread, a constraint applied too broadly, a dependency overlooked — the reconstruction question is *why was this understood this way, and on what basis*. If the reasoning existed only in an inference context that no longer exists, the question cannot be answered. Responsibility is not thereby removed; it is merely made undemonstrable, which is a worse position for an organization than either accepting or rejecting it.

**Conditional commitments widen without anyone deciding to widen them.** A relationship accepted under specific conditions, whose conditions were never written down, tends to be applied more generally each time it is recovered. No single step in that drift is a decision. The organization ends up holding a broader commitment than it ever agreed to, with no point at which the broadening can be located.

**The same interpretive work is bought repeatedly.** Semantic questions whose answers were already settled continue to consume inference resources on every occasion they arise. This is the least serious consequence, but it is the one most easily measured, and it is often the only one that surfaces in budget discussions.

**Continuity depends on the model.** Because interpretation is produced at the moment of use, changing the model — a version upgrade, a different vendor, a locally hosted alternative — can change what the organization's own knowledge is taken to mean. Knowledge that ought to be an organizational asset is in practice contingent on a supplier's product decisions.

Taken together, these consequences describe an organization that has adopted AI to work with its knowledge and has, as a result, ended up holding rather less of it than before.

## 2.4 Relationship to Retrieval

AI Knowledge Architecture does not replace RAG. The two answer different questions.

Retrieval asks what information should be brought into context. This architecture asks which accepted interpretations should persist after inference has finished.

They compose naturally. Sources are retrieved; AI proposes interpretations of them; an admission step determines which proposals become governed knowledge; the knowledge architecture preserves what was accepted for subsequent reuse. Retrieval supplies the material. The architecture retains the conclusions.

---

# 3. Engineering Determinacy Applied to Knowledge

## 3.1 The Governing Principle

Engineering Determinacy is applied here as a design principle governing where probabilistic interpretation remains necessary and where explicit structure can take its place. Applied to knowledge, it reads:

> **Once an interpretation has been explicitly established and accepted, it should not be re-inferred.**

Three terms carry weight.

*Established* means the interpretation has been made explicit. It does not mean the interpretation is objectively correct.

*Accepted* means the interpretation has crossed an admission boundary and become part of the governed knowledge state. Generation by a model does not by itself constitute acceptance — this is the point at which most current systems make no distinction at all.

*Not re-inferred* means routine reuse should consume the accepted representation rather than reconstruct its meaning from the original source. It does not prevent later revision.

The principle therefore separates two pairs of activities that are commonly conflated: discovery is not reuse, and revision is not reinterpretation on every query.

## 3.2 Two Zones and the Boundary Between Them

The architecture distinguishes a probabilistic zone from a deterministic knowledge zone.

The **probabilistic zone** handles unresolved interpretation: material is read, meanings are proposed, candidate knowledge is produced. This zone may contain ambiguity, competing interpretations, incomplete evidence, disagreement between models, disagreement between people, and unverified relationships. AI reasoning is expected here, and nothing in this architecture seeks to reduce it.

The **deterministic knowledge zone** begins after admission. Once a semantic commitment has been accepted, it becomes explicitly addressable. Instead of asking whether a requirement appears to apply to production, a downstream operation can consult the recorded environment. Instead of asking whether connection-pool capacity constrains throughput, it can check whether that relation exists in the accepted state. The architecture changes the default location of semantic interpretation, not the capability of the model.

**Admission** is the boundary between the two. The architecture deliberately does not prescribe a single universal admission procedure. Admission may rest on human adjudication, deterministic validation, authoritative sources, evidence requirements, schema validation, agreement across models, domain rules, or combinations of these — and the appropriate mechanism differs by organization, by risk, and by regulatory context.

What matters is that persistence is not truth. Persisting an incorrect interpretation does not correct it. The purpose of admission is not to guarantee truth but to establish an explicit transition between a proposed interpretation and an accepted knowledge commitment — and, in doing so, to give the organization a place where that commitment can be located, reviewed, and, if necessary, revised.

Determinacy in this architecture therefore does not arise from model certainty. It arises from explicit representation, persistence, and controlled admission. The deterministic zone governs reuse, not permanent truth.

---

# 4. An Illustrative Case: One Requirement, Four Roles

Before describing the architecture in detail, it is worth seeing the problem it addresses in a form that has nothing to do with representation formalism.

## 4.1 The Shared Knowledge State

Consider again:

> The production transaction service shall sustain 10,000 transactions per second.

After interpretation and admission, this becomes an identified assertion with resolved semantics recorded explicitly: it is a requirement, its subject is the transaction service, its environment is production, its metric is transactions per second, its target is ten thousand, its load mode is sustained, its priority is high, and it serves an enterprise service-level commitment.

Three further assertions are accepted alongside it: that the connection pool supports five hundred concurrent connections; that increasing the connection pool increases infrastructure cost; and that the service is marketed for enterprise high-volume workloads.

Two relationships are also accepted. The throughput requirement is constrained by the connection-pool capacity, and that constraint is recorded as holding specifically in production and specifically under sustained load, on the basis of the stated target, the load mode, and the pool's maximum connections. Separately, satisfying the requirement increases cost, grounded in the third assertion.

All of this belongs to a shared state. None of it belongs to any particular role.

## 4.2 Four Readings of the Same Knowledge

An **architecture** reading emphasizes dependency, capacity, and structural constraint. It draws on the requirement and the connection pool, and it reads the constraint relationship as identifying a bottleneck.

A **business analysis** reading emphasizes objectives, economic justification, and cost impact. It draws on the requirement, the connection pool, and the cost assertion. Different semantics of the same requirement become salient — priority, business goal, target — and the cost relationship becomes structurally central, because meeting the performance commitment has economic consequences.

A **product** reading emphasizes customer expectation and market positioning. It draws on the requirement and the market-segment assertion, and it places the same requirement in a structure connecting technical performance to customer value.

An **operations** reading emphasizes capacity, sustained load, scaling, and thresholds. It draws on the same two assertions as the architecture reading, but interprets the same constraint relationship as a scaling boundary rather than a bottleneck.

Nothing in the underlying knowledge has changed across these four readings. The same assertion, the same relationship, the same recorded conditions. What differs is which knowledge is relevant, how it is organized, and what structural role each element plays.

Two observations follow. First, the same relationship can carry different structural roles under different readings without the relationship itself being duplicated. Second, and more consequentially, these readings are recurring: an organization does not invent its architecture perspective afresh each time it needs one. If the perspective is stable, it can be represented; if it is represented, it need not be reconstructed.

## 4.3 What Becomes Visible Only Across Readings

Because all four readings derive from one shared state, they can be compared.

The architecture and operations readings share the same requirement, the same connection pool, and the same constraint — but assign it different roles. That difference is itself informative: the two functions are looking at one limitation and treating it as two different kinds of problem.

The comparison between operations and business is sharper. Operations holds that meeting the performance target requires a capacity increase. Business holds that a capacity increase creates infrastructure cost, which meets a budget constraint. Chained together, these produce a conflict — performance target, capacity increase, infrastructure cost, budget limit — that is not structurally visible within either reading alone.

The significance here is not the comparison operation itself, which is elementary. It is that the comparison operates over shared knowledge identities. Where each function maintains its own separately constructed knowledge store, a comparison of this kind must first reconcile two independently built representations, and the conflict is usually discovered instead through a failed delivery.

---

# 5. The Architecture

This section describes each structure in terms of the interpretive question it removes from repeated inference. Structural specifications and worked representations appear in Appendix A.

## 5.1 Claim Object — Semantic Identity

A **Claim Object** is the persistent identity of an identified knowledge assertion: an identifier, the proposition it expresses, and a set of explicit attributes. It transforms a textual expression into a persistent semantic identity, so that downstream work references a stable knowledge object rather than a passage of text.

Identifiable knowledge statements are not novel. Nanopublications already represent assertions as identifiable publishing units with associated provenance [4]. Semantic-unit architectures organize knowledge graphs into persistent, semantically meaningful units and compound structures [5], and Trusty URIs provide mechanisms for verifiable persistent digital identity [6]. Claim Objects use these established capabilities toward a determinacy objective.

## 5.2 Attribute — Semantic Determinacy

Attributes externalize semantics that would otherwise remain implicit in natural language. That *production* denotes an environment is, before externalization, something a model must infer whenever it matters; afterwards it is something the system holds.

Attributes serve several purposes without collapsing them into one mechanism. They describe resolved claim semantics; a selected subset may form part of the basis supporting a relationship; and different perspectives may treat different attributes as relevant. The attributes available on a claim, the attributes grounding a relation, and the attributes a viewpoint selects are three distinct selections and should not be conflated.

Which semantics are worth externalizing is not a property of the source material. It is a property of the decisions that depend on it.

Consider a single clause in a supplier agreement:

> Replacement units for the enterprise controller are dispatched within five business days for customers on the Premium plan.

A procurement system and a customer-service system may both retrieve this clause, and both must resolve what *five business days* means before acting on it. They do not resolve it into the same thing. For procurement, the clause states a supplier obligation: what matters is which supplier is bound, what the committed lead time is, which contract term and renewal date govern it, what penalty exposure attaches to a breach, and what sourcing risk follows if the supplier cannot meet it. For customer service, the same clause states a customer entitlement: what matters is which entitlement tier it applies to, which product is covered, what response window has been promised, what condition triggers escalation, and which exceptions apply.

The phrase is identical. The resolved semantics are not, because the two systems are answering different questions — *are we exposed if this supplier slips* versus *what is this customer owed today*. An attribute set designed for one will not serve the other, and a schema built to serve both by union will hold, for each system, a majority of fields that no decision in that system consults.

The architecture therefore does not require applications to adopt a universal attribute schema, and does not treat the absence of one as a deficiency. Its requirement is narrower: once an application repeatedly depends on a resolved semantic distinction, that distinction should become explicit rather than being reconstructed from source text on every query. Attribute sets accordingly accumulate from use rather than being designed in advance, and they differ between applications because the decisions differ.

Two consequences follow for shared deployments. Where several applications operate over the same Claim Objects, their attribute requirements may overlap without coinciding; the shared claim carries the union of what has been established, and each application consults the subset its decisions require. And where an established attribute happens to serve a second application, that application inherits it without re-establishing it — which is the point at which persisting semantics begins to compound across an organization rather than accruing to one system.

Property-bearing knowledge representation is established prior art. The determinacy role lies in *why* a semantic property is persisted: so that a resolved interpretation stops depending on repeated inference.

## 5.3 Relation — Relational Determinacy

A **Relation** externalizes an accepted relational interpretation between claims: source, target, relation type, applicability conditions, and grounding. Once accepted, the existence of the relationship becomes an explicit property of the knowledge state rather than something rediscovered on demand.

The architecture also distinguishes relations belonging to the shared state from relations induced by a particular perspective. The shared state may hold that a connection pool limits throughput, while an architecture perspective organizes the same knowledge as the pool acting as a bottleneck for a requirement. A perspective-induced relation must remain anchored to the shared state — to a shared claim, a shared relation, or another explicitly referenced shared object. Without that requirement, a perspective can quietly become an isolated private knowledge universe, which is precisely the fragmentation the shared substrate exists to prevent.

## 5.4 Grounding Basis — Inspectable Basis

The **Grounding Basis** records why a relation was asserted and accepted. It may reference claim attributes, other claims, other relations, evidence, measurements, external sources, deterministic rules, provenance records, or authoritative assertions. A relation may originate from human assertion, model inference, a rule engine, deterministic computation, an external knowledge graph, or imported authoritative knowledge.

The architecture does not define a universal relation-inference algorithm. Its requirement is narrower and more durable:

> **Whenever a relation becomes an accepted knowledge commitment, its relevant grounding remains inspectable.**

This is the structure that answers the accountability question raised in Section 2.3. Provenance-aware knowledge representation already provides mechanisms for preserving lineage and contextual evidence [7]; the contribution here is not provenance syntax but its assignment to the basis of accepted interpretation.

## 5.5 Qualifier — Boundary Determinacy

An unqualified relation invites over-generalization. A constraint that actually holds only in production, under sustained load, from a particular date, will be applied more broadly than intended if those conditions are never written down.

A **Qualifier** externalizes that applicability boundary, along dimensions that may include scope, environment, time, condition, modality, authority, evidence, and version. The design principle is direct: unqualified semantics invite inference expansion; explicit boundaries constrain interpretation.

Statement-level qualification is established prior art. Wikidata demonstrates practical qualifier mechanisms [8], and RDF-star supports higher-order statements in which statements themselves become objects of further assertions [9]. The architectural purpose here is to use qualification to prevent accepted conditional meanings from being repeatedly reconstructed or silently generalized.

## 5.6 Viewpoint — Interpretive Determinacy

The structures above externalize interpretation at the assertion and relational levels. A different problem appears when recurring groups of knowledge must be interpreted through a stable perspective — the situation illustrated in Section 4.

A **Viewpoint** externalizes that recurring interpretive structure. It is not a user role, a category, a tag, a saved query, a claim set, a relation set, or a traversal rule. Four conditions distinguish it.

*Interpretive coherence.* Its components must share an identifiable interpretive dimension. An architecture viewpoint may emphasize dependency, capacity, structural constraint, interface, and bottleneck; an arbitrary collection of relations does not constitute a viewpoint.

*Structural organization and role semantics.* A viewpoint organizes relations rather than merely selecting them, and elements within it may occupy explicit structural roles — driver, dependency, bottleneck. The organization itself carries interpretive meaning, and a role is a position within that structure rather than a viewpoint in miniature.

*Selective relevance.* A viewpoint defines what knowledge is relevant under its interpretive structure, drawing on claim identity, attributes, relation types, qualifiers, grounding, relational patterns, or structural roles. Selection determines membership; interpretive structure determines organization. These are different functions.

*Abstractability.* A viewpoint must be reusable beyond one concrete case. A one-off arrangement of relations that cannot be abstracted into a recurring pattern is not a viewpoint.

The falsification boundary is explicit and worth stating plainly: **if a viewpoint can be completely replaced by a saved query without information loss, the mechanism reduces to ontology-view prior art.** The distinction claimed here is substantive, not terminological, and it can be tested.

> *Terminology note.* The term *viewpoint* also appears in ISO/IEC/IEEE 42010:2022 in the context of architecture description [10]. The present work uses the term independently, to denote a persistent interpretive structure over an AI knowledge state.

## 5.7 Domain — Deterministic Derivation

A **Viewpoint Domain** is the knowledge organization obtained by applying a persistent viewpoint to the shared knowledge state.

The architecture separates a persistent domain *definition* from derived domain *content*. The viewpoint and its selection criteria persist; the claims and relations constituting the domain are derived from the shared state each time. The shared knowledge state remains the single source of truth, the viewpoint remains a persistent interpretive definition, and the domain remains a derived organization rather than another maintained copy of the knowledge base.

The property this yields is reproducibility: the same governed state combined with the same explicit viewpoint definition produces the same derived organization. That property holds only if the derivation itself is reproducible. If unconstrained model interpretation determines domain membership on every derivation, the architecture has merely relocated repeated semantic inference rather than removing it. Routine derivation must therefore rest on stable, explicit, reproducible selection semantics.

## 5.8 The Determinacy Stack

| Element         | Externalized uncertainty           | Determinacy role         |
| --------------- | ---------------------------------- | ------------------------ |
| Claim Object    | Assertion identity                 | Semantic Identity        |
| Attribute       | Implicit claim semantics           | Semantic Determinacy     |
| Relation        | Relational interpretation          | Relational Determinacy   |
| Qualifier       | Applicability conditions           | Boundary Determinacy     |
| Grounding Basis | Basis for accepted relation        | Inspectable Basis        |
| Viewpoint       | Interpretive organization          | Interpretive Determinacy |
| Domain          | View-specific knowledge membership | Deterministic Derivation |

The architecture follows one construction principle: different forms of semantic uncertainty are externalized into different forms of explicit structure. It is not a collection of unrelated representation features.

---

# 6. Related Work and Positioning

This section compares prior work by **architectural responsibility** rather than by terminology or representation mechanism. The relevant question is not whether prior work contains statements, properties, qualifiers, provenance, perspectives, or views — most of these mechanisms are well established. The relevant question is what responsibility is assigned to persistent structure, and where semantic interpretation remains after inference.

## 6.1 Retrieval and Graph-Based Retrieval

RAG integrates external non-parametric knowledge into model inference [1, 2]. Graph-based architectures such as GraphRAG extract entities and relationships and organize corpus information into structures supporting summarization and query answering [3]. These substantially improve retrieval, context construction, and query-time synthesis.

The distinction is not retrieval versus knowledge graph. It is query-time interpretation versus persistent accepted interpretation. Standard retrieval does not require semantic interpretations established during one inference cycle to become governed commitments for the next. This architecture therefore operates downstream of retrieval rather than replacing it.

## 6.2 Persistent Knowledge Units and Qualified Representation

Persistent, referable knowledge units are established prior art. Nanopublications combine assertions with provenance and publication information [4]; Trusty URIs provide verifiable persistent identification [6]; semantic-unit architectures organize knowledge graphs into bounded, semantically meaningful structures, including statements about statements and multiple frames of reference [5]. Wikidata demonstrates statement-level qualifiers [8], RDF-star provides higher-order statements [9], and provenance-aware representation preserves lineage and evidential context [7].

This paper claims novelty for none of these. Persistent statement identity, semantic modularization, statements about statements, qualifier syntax, and provenance models form its representation substrate. The distinction lies in the responsibility assigned to them: to mark accepted semantic commitments as distinct from questions still requiring probabilistic inference, to make applicability explicit rather than implicit, and to keep the basis of acceptance inspectable.

## 6.3 Ontology Views and Perspective-Aware Architectures

Derived views over shared knowledge are also established. Noy and Musen define ontology views through traversal specifications involving focus concepts, relationships, and constraints [11]. Brinkley et al. describe an architecture in which reference ontologies serve as shared foundations while application ontologies are expressed as views over them, with persistent view definitions and derived, possibly non-materialized, contents [12]. This is structurally close to the domain derivation described in Section 5.7, and no novelty is claimed for persistent view definitions, shared source ontologies, dynamic derivation, non-materialized views, or query-based selection.

The proposed distinction depends entirely on what a viewpoint contains. An ontology view can be characterized as a query or traversal over a knowledge base. A viewpoint here requires selection *and* interpretive structure: it persists not only which knowledge is selected but how the selected relations are organized and what structural roles they occupy. As stated in Section 5.6, this claim is falsifiable — if the structure can be fully replaced by a saved query, it collapses into this prior art.

Perspective-aware extraction offers a closer comparison. Miranda and Nalepa [13] propose an architecture in which ontology-orchestrated agents extract perspective-conditioned facts while preserving stakeholder interpretations as epistemically separable, queryable knowledge graphs — directly addressing the preservation of multiple interpretations rather than collapsing them into one decontextualized representation.

The distinction concerns *where perspective enters the architecture*. Perspective-conditioned extraction moves from source to perspective-conditioned knowledge. This architecture moves from source to a shared knowledge state, and then to viewpoint-derived domains. Persistent claims and base relations form a shared governed substrate before perspective is applied; perspectives then assign relevance, organization, and structural roles to the same knowledge identities. Perspective changes the organization of shared knowledge without requiring the underlying assertions to be reconstructed separately for each perspective — which is what makes the cross-perspective comparison in Section 4.3 possible.

## 6.4 Ontology Evolution

Ontology evolution provides mature process models for detecting, representing, propagating, validating, and managing change in ontological knowledge as domains and requirements evolve [14, 15]. This literature is directly relevant to future reconstruction mechanisms.

Knowledge revision is not claimed as novel. What the present architecture adds is a distinction between routine reuse, which consumes accepted structures, and epistemic revision, which requires an explicit transition from an accepted commitment through a candidate to a new accepted commitment. This paper defines the persistent state and determinacy boundary on which such processes can operate; detailed evolution mechanisms are outside its scope.

## 6.5 Positioning Summary

| Architecture family               | Primary responsibility                                                        | Relationship to this work                                                                  |
| --------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| RAG                               | Retrieve relevant information                                                 | Upstream source of material                                                                |
| GraphRAG                          | Graph-supported retrieval and sensemaking                                     | Structured retrieval substrate                                                             |
| Nanopublications / Semantic Units | Persistent identifiable semantic units                                        | Persistent knowledge substrate                                                             |
| Qualified / Provenance KR         | Contextual and evidential representation                                      | Qualifier and grounding substrate                                                          |
| Ontology Views                    | Derived views over shared knowledge                                           | Direct prior art for domain derivation                                                     |
| Perspective-Aware KG              | Preserve perspective-conditioned knowledge                                    | Direct prior art for multi-perspective knowledge                                           |
| Ontology Evolution                | Govern knowledge change                                                       | Foundation for future reconstruction                                                       |
| **AI Knowledge Architecture**     | **Externalize accepted AI interpretation into governed persistent structure** | **Determinacy boundary between probabilistic interpretation and structure-governed reuse** |

The architecture-level proposition is therefore that accepted interpretation becomes persistent explicit structure, and persistent explicit structure enables structure-governed reuse.

---

# 7. Discussion and Limitations

## 7.1 Determinacy Does Not Mean Truth

The architecture creates explicit semantic commitments. It does not guarantee that those commitments are correct. If an interpretation is wrong and passes admission, persistence does not repair it — and may amplify its consequences, because downstream work will reuse the accepted structure.

Engineering Determinacy therefore moves part of the problem from repeated interpretation to **admission quality**. This trade-off is intentional. Repeated probabilistic interpretation hides semantic instability by distributing it across occasions where no one is watching. Persistent accepted knowledge makes semantic commitments inspectable, which means they can be wrong in a way that someone can find.

## 7.2 Deterministic Does Not Mean Immutable

Suppose an accepted target of ten thousand transactions per second is later superseded by an authoritative requirement of fifteen thousand. The architecture does not require the old value to persist indefinitely — nor should each model invocation independently decide which value is currently valid. The knowledge must undergo an explicit state transition.

Persistent is not immutable, and deterministic reuse is not permanent truth. Knowledge reconstruction is a necessary operational complement to this architecture, not a contradiction of it.

## 7.3 Explicit Semantics Cannot Be Complete

Attributes reduce repeated interpretation only for semantics that have actually been externalized. No finite schema can guarantee that every future semantic question has already been represented. A claim may record environment and target while a later task requires a dimension never modeled, at which point the system must return to probabilistic interpretation.

The architecture is therefore progressive rather than total: implicit semantics become candidate semantics, and candidate semantics become accepted explicit semantics, incrementally and only where the organization has reason to invest. Engineering Determinacy reduces unnecessary inference. It does not eliminate interpretation.

The same caution applies to qualifier dimensions. Scope, time, environment, condition, authority, modality, and evidence cannot be assumed complete across domains, and an omitted boundary may still permit inference expansion. Qualifier schema design, domain-specific discovery, missing-boundary detection, conflict handling, and boundary inheritance all require further work.

## 7.4 Viewpoint Formalization Remains Incomplete

The viewpoint is the component requiring the strongest additional validation. The conditions proposed in Section 5.6 distinguish viewpoints from arbitrary relation sets and saved queries, but this paper does not provide a complete formal logic for determining whether a candidate structure satisfies them, nor does it define automatic viewpoint discovery.

Viewpoints may originate from human design, organizational roles, recurring structural patterns, ontology structures, model-assisted induction, historical analysis, or combinations of these. The architecture requires accepted viewpoints to become explicit and persistent. It does not prescribe how they are found.

Likewise, the cross-perspective comparison illustrated in Section 4.3 has no complete comparison algebra here. Candidate dimensions include shared claims and relations, differences in selected attributes, qualifiers, grounding, structural roles, structural paths, constraints, and missing relations. Whether such comparison reliably identifies meaningful conflicts remains to be evaluated empirically.

## 7.5 Reproducibility Depends on the Derivation Mechanism

The reproducibility property of Section 5.7 holds only when derivation is itself reproducible. If domain membership is decided by unconstrained model interpretation on each derivation, repeated semantic inference has been relocated rather than removed. Routine derivation should rest on explicit rules, stable queries, deterministic traversal, validated structural patterns, or comparable semantics. AI may assist in constructing or revising those mechanisms; it should not silently redefine them during routine reuse.

## 7.6 Architecture Rather Than Storage Technology

The architecture is representation-agnostic. Labeled property graphs, RDF and RDF-star, relational databases, document stores, hybrid systems, and dedicated knowledge infrastructures are all plausible implementations. No claim is made that one storage technology is optimal. The contribution concerns the semantic responsibilities assigned to persistent structures, not the technology that holds them.

---

# 8. Future Work: Toward Knowledge Evolution

This paper defines a persistent knowledge architecture. A subsequent problem concerns how that knowledge state changes. Four operation classes follow.

**Construction** moves from source material to candidate knowledge: claim extraction, semantic attribute extraction, candidate relation discovery, candidate qualifier generation, evidence collection, and provenance capture. It operates primarily in the probabilistic zone.

**Integration** moves from an existing state plus new candidates to a revised state, raising claim identity resolution, duplicate detection, equivalence, conflicting attributes, relation reconciliation, qualifier compatibility, provenance conflicts, and admission decisions. Integration is the principal transition between candidate interpretation and governed knowledge.

**Reconstruction** changes accepted structures when new evidence or changed conditions invalidate existing commitments. Reconstruction may occur at the claim level (split, merge, replacement, specialization, generalization), the relation level (insertion, deletion, type change, grounding change), the qualifier level (narrowing, expansion, temporal or authority revision), the viewpoint level (role change, topology revision, split, merge), or the scope level (domain expansion, contraction, changed intersection). A general process moves from local change through dependency propagation and reconstruction to revalidation. Ontology evolution research provides important foundations here [14, 15].

**Exploration** concerns semantics and relationships not yet made explicit. Where an architecture perspective holds a capacity constraint and a business perspective holds a cost constraint, the absence of an accepted relation connecting capacity expansion to business feasibility is itself a structural gap — and a structural gap is an exploration question, which returns to the probabilistic zone as a candidate for later admission.

Together these form a cycle in which probabilistic discovery and deterministic knowledge structure alternate rather than compete. The present paper defines the structural side of that cycle; the operational theory remains future work.

---

# 9. Conclusion

AI systems now retrieve, generate, and organize information with considerable sophistication. Information availability, however, does not guarantee that interpretation persists. When established semantic decisions remain encoded only in source text, prompts, temporary context, or transient reasoning, the same meaning is reconstructed repeatedly — and the organization that paid for the interpretation does not hold it.

This paper proposed **AI Knowledge Architecture**, derived from the principle of **Engineering Determinacy**:

> **Once an interpretation has been explicitly established and accepted, it should not be re-inferred.**

The architecture does not attempt to eliminate probabilistic AI. It establishes a boundary between unresolved interpretation and accepted knowledge. Before that boundary, AI retrieves, infers, compares, and proposes. After it, accepted interpretation becomes persistent explicit structure: a claim object establishing semantic identity, attributes externalizing resolved semantics, relations persisting accepted relational interpretations, qualifiers externalizing applicability boundaries, grounding basis preserving inspectable justification, viewpoints externalizing reusable interpretive organization, and domains derived reproducibly from a shared state.

The contribution is not a new graph representation, property mechanism, qualifier syntax, provenance model, virtual view, or the existence of multiple perspectives. Prior work provides substantial foundations for each. The architectural contribution lies in assigning them a common responsibility: *do not repeatedly infer what has already been explicitly established, accepted, and represented.*

This reframes persistent AI knowledge as more than stored information. It becomes a governed record of accepted interpretation — something an organization can point to, review, revise, and be held to.

The resulting division of responsibility is simple: **inference discovers interpretation; structure preserves what has been accepted.**

---

# Appendix A. Structural Specification

This appendix records the structural detail omitted from the main text. It is intended for readers implementing or evaluating the architecture.

## A.1 Shared Knowledge State

The shared knowledge state consists of a set of accepted Claim Objects and a set of accepted shared Relations. Viewpoints and derived Domains are defined over this state.

## A.2 Claim Object

A Claim Object comprises a persistent identifier, a proposition, and a set of explicit attributes.

```
Claim C-001

proposition:
  "The production transaction service
   shall sustain 10,000 TPS."

attributes:
  type          = requirement
  subject       = transaction-service
  environment   = production
  metric        = TPS
  target        = 10000
  load_mode     = sustained
  priority      = high
  business_goal = enterprise-SLA
```

Three attribute selections must be kept distinct: the attributes available on a claim; the subset forming the grounding of a relation; and the subset a viewpoint treats as relevant. These are not the same selection and should not be represented as one.

The attribute set is not fixed by a schema defined in advance. Following Section 5.2, the same claim accumulates whatever semantics the applications operating over it have needed to establish. For the supplier clause discussed there:

```
Claim C-112

proposition:
  "Replacement units for the enterprise
   controller are dispatched within five
   business days for customers on the
   Premium plan."

attributes established for procurement:
  supplier            = northgate-components
  obligation_type     = lead_time_commitment
  committed_lead_time = 5d
  contract_term       = MSA-2026-04
  penalty_exposure    = service_credit
  renewal_date        = 2027-04-01

attributes established for customer service:
  entitlement_tier    = premium
  covered_product     = enterprise-controller
  promised_window     = 5d
  escalation_trigger  = window_exceeded
  exception_condition = stock_unavailable
```

The two sets share a knowledge identity and one value, and diverge everywhere else. Neither is a subset of the other, and neither system consults the other's fields during routine operation.

## A.3 Relation

A Relation comprises an identifier, a source claim, a target claim, a relation type, qualifiers, and a grounding basis.

```
Relation R-001

source:  C-001
target:  C-002
type:    constrainedBy

qualifiers:
  environment = production
  load_mode   = sustained
  valid_from  = 2026-09-01

basis:
  C-001.target
  C-001.load_mode
  C-002.max_connections
  Evidence E-003
```

A shared base relation belongs to the shared state. A viewpoint-induced relation exists as part of an interpretive structure under a viewpoint and must remain anchored to a shared claim, a shared base relation, or another explicitly referenced shared object.

## A.4 Qualifier Dimensions

Candidate dimensions include scope, environment, time, condition, modality, authority, evidence, and version. No claim of completeness is made; see Section 7.3.

## A.5 Viewpoint

A viewpoint comprises an interpretive dimension, an organized relational structure, applicable constraints, and explicit selection criteria. Structural roles are assigned to elements within the structure:

```
Requirement Constraint  → driver
Architecture Dependency → dependency
Capacity Limitation     → bottleneck
```

The same shared relation may carry different roles under different viewpoints — for example, `bottleneck` under an architecture viewpoint and `scaling_boundary` under an operations viewpoint — without duplication of the underlying assertion.

## A.6 Domain Derivation

A Viewpoint Domain is obtained by applying a persistent viewpoint to the shared knowledge state, yielding a subset of claims together with the relevant shared and viewpoint-induced relations. The definition persists; the content is derived.

Reproducibility condition: if the governed state and the viewpoint definition are both unchanged between two derivations, the derived domain is identical. This holds only where the derivation function is itself reproducible (Section 7.5).

## A.7 Cross-Viewpoint Comparison

Comparison across viewpoints operates over shared knowledge identities. Candidate comparison dimensions include the intersection of claims, the intersection of relations, and differences in selected attributes, qualifiers, grounding basis, structural roles, structural paths, constraints, and missing relations. In the illustrative case, the architecture and operations viewpoints intersect on claims C-001 and C-002 and on relation R-001, differing only in the structural role assigned.

---


# Declarations

## Funding

The author received no specific funding for this work.

## Conflicts of Interest

The author declares no conflicts of interest.

## Data Availability

No empirical dataset was generated or analyzed for this conceptual architecture paper.

## Declaration of Generative AI and AI-Assisted Technologies

Generative AI tools were used during the preparation of this manuscript to support literature discovery, organization of arguments, language drafting, editing, and manuscript refinement. The research problem, Engineering Determinacy concept, architectural design, conceptual distinctions, interpretation of prior work, and final scholarly claims were directed, evaluated, revised, and approved by the author. The author reviewed the generated material, verified cited sources and their characterization, and takes full responsibility for the content of the manuscript.


# References

[1] Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. In *Advances in Neural Information Processing Systems*, 33, 9459–9474.

[2] Gao, Y., Xiong, Y., Gao, X., Jia, K., Pan, J., Bi, Y., Dai, Y., Sun, J., & Wang, H. (2023). Retrieval-augmented generation for large language models: A survey. *arXiv preprint arXiv:2312.10997*.

[3] Edge, D., Trinh, H., Cheng, X., Bradley, J., Chao, A., Mody, A., Truitt, S., & Larson, J. (2024). From local to global: A Graph RAG approach to query-focused summarization. *arXiv preprint arXiv:2404.16130*.

[4] Groth, P., Gibson, A., & Velterop, J. (2010). The anatomy of a nanopublication. *Information Services & Use*, 30(1–2), 51–56. DOI: 10.3233/ISU-2010-0613.

[5] Vogt, L., Kuhn, T., & Hoehndorf, R. (2024). Semantic units: organizing knowledge graphs into semantically meaningful units of representation. *Journal of Biomedical Semantics*, 15, Article 7. DOI: 10.1186/s13326-024-00310-5.

[6] Kuhn, T., & Dumontier, M. (2014). Trusty URIs: Verifiable, immutable, and permanent digital assets for the semantic web. In *Proceedings of the 11th Extended Semantic Web Conference (ESWC)* (pp. 395–410). Springer. DOI: 10.1007/978-3-319-07443-6_27.

[7] Sikos, L. F., & Philp, D. (2020). Provenance-aware knowledge representation: A survey of data models and contextualized knowledge graphs. *Data Science and Engineering*, 5, 293–316.

[8] Vrandečić, D., & Krötzsch, M. (2014). Wikidata: A free collaborative knowledgebase. *Communications of the ACM*, 57(10), 78–85. DOI: 10.1145/2629489.

[9] Hartig, O. (2017). Foundations of RDF* and SPARQL*—An approach for statements about statements. *CEUR Workshop Proceedings*, 1912, 1–12.

[10] ISO/IEC/IEEE. (2022). *ISO/IEC/IEEE 42010:2022 — Software, systems and enterprise — Architecture description*. ISO/IEC/IEEE.

[11] Noy, N. F., & Musen, M. A. (2004). Specifying ontology views by traversal. In *Proceedings of the 3rd International Semantic Web Conference (ISWC 2004)* (pp. 713–725). Springer. DOI: 10.1007/978-3-540-30475-3_49.

[12] Brinkley, J. F., Suciu, D., Detwiler, L. T., & Rosse, C. (2006). A framework for using reference ontologies as a foundation for the Semantic Web. *AMIA Annual Symposium Proceedings*, 2006, 86–90.

[13] Miranda, L. D. V., & Nalepa, G. J. (2026). Thesis proposal: A multi-agent system for ontology-based perspective-aware knowledge extraction. In *Proceedings of the 19th Conference of the European Chapter of the Association for Computational Linguistics (Volume 4: Student Research Workshop)* (pp. 604–611). Association for Computational Linguistics. DOI: 10.18653/v1/2026.eacl-srw.46.

[14] Zablith, F., Antoniou, G., d'Aquin, M., Flouris, G., Kondylakis, H., Motta, E., Plexousakis, D., & Sabou, M. (2015). Ontology evolution: A process-centric survey. *The Knowledge Engineering Review*, 30(1), 45–75. DOI: 10.1017/S0269888913000349.

[15] Flouris, G., Manakanatas, D., Kondylakis, H., Plexousakis, D., & Antoniou, G. (2008). Ontology change: Classification and survey. *ACM Computing Surveys*, 40(2), Article 7. DOI: 10.1145/1330311.1330314.
