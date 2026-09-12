# AI Knowledge Evolution: From Persistent Knowledge Structure to Controlled Knowledge Change

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  

---

## Abstract

The companion paper *AI Knowledge Architecture* proposed a persistent knowledge architecture in which accepted AI interpretations are externalized as Claim Objects, qualified Relations, Viewpoint structures, and derived Domains. That architecture defines how accepted knowledge is represented. It does not define how such knowledge comes into existence, how it becomes connected to other knowledge, how previously accepted relationships are reconsidered, or how a system identifies relationships that have not yet been established.

This paper addresses those questions through four knowledge operations with distinct epistemic responsibilities.

**Knowledge Construction** establishes what knowledge assertions exist. It transforms source material into explicit Claim Objects together with semantic Attributes that have been resolved for subsequent use. Construction does not determine how those Claims relate to other Claims. A Claim or Attribute produced through probabilistic AI interpretation remains a candidate unless the applicable governance process accepts it.

**Knowledge Integration** establishes how existing Claims are related. It creates explicit Relations whose type, applicability conditions, and grounding can be inspected. Accepting that two Claims exist is not equivalent to accepting that a particular relationship holds between them; relational interpretation is therefore treated as a separate knowledge commitment.

**Knowledge Reconstruction** asks whether Relations that have already been accepted still hold. New Claims, evidence, conditions, or contextual distinctions may alter the basis or applicability of an existing Relation. Reconstruction may retain the Relation, narrow or revise its applicability, supersede it, remove it, or establish additional Relations. Knowledge can therefore change even when graph topology does not: a Relation may remain structurally present while the conditions under which it is accepted change materially.

**Knowledge Exploration** asks whether Claims currently treated as unrelated may plausibly be related. It uses existing Attributes, qualified Relations, structural patterns, and persistent Viewpoints to produce candidate Relations. These candidates carry proposed applicability conditions, an inspectable grounding basis, and an evidence profile describing why the relationship merits examination. Exploration does not create a knowledge commitment; it creates a structured reason for asking whether one should exist.

The four operations interact without forming a mandatory sequential pipeline. Construction creates Claims, Integration relates them, Reconstruction revisits accepted relational commitments, and Exploration identifies relational possibilities that have not yet entered the accepted knowledge state. Admission remains orthogonal to all four operations: it governs when a candidate knowledge element becomes an accepted commitment.

The paper extends Engineering Determinacy from persistent representation to controlled knowledge change. Engineering Determinacy does not require knowledge to remain static. It requires changes in accepted knowledge to be explicit, inspectable, and distinguishable from routine probabilistic reinterpretation.

**Keywords:** AI Knowledge Evolution; Engineering Determinacy; Knowledge Representation; Knowledge Graph; Knowledge Revision; Ontology Evolution; Knowledge Graph Completion; Literature-Based Discovery; Large Language Models; AI Governance

---

# 1. Introduction

A knowledge system that never changes is not useful for long. Requirements are revised, policies expire, technical constraints change, evidence accumulates, organizational assumptions are challenged, and relationships that appeared valid under one set of conditions may cease to hold under another. At the same time, unconstrained change creates a different problem. If every interaction with an AI system is permitted to reinterpret previously accepted knowledge, persistence loses much of its value: the organization may store information while repeatedly renegotiating what that information means.

The companion paper *AI Knowledge Architecture* addresses the static side of this problem. It proposes that interpretations which have been explicitly established and accepted should be externalized into persistent knowledge structures rather than reconstructed through probabilistic inference whenever they are used [1]. Claim Objects provide stable identity to knowledge assertions; Attributes externalize resolved semantics; Relations persist accepted relational interpretations; Qualifiers express applicability conditions; Grounding Basis preserves why a Relation was accepted; Viewpoints preserve recurring interpretive organization; and Domains derive role- or purpose-specific knowledge organizations from a shared state.

That architecture establishes what accepted knowledge looks like. It deliberately leaves a different question open: how does that knowledge change?

The proposed operations concern persistent knowledge structure rather than retrieval indexing. They are intended to govern how interpreted knowledge is constructed, related, reconsidered, and explored after it becomes a candidate for persistent organizational use.

The problem cannot be reduced to adding and deleting graph edges. Before a relation can exist, the assertions that participate in it must first have been identified. When a new assertion is introduced, a system must determine whether it relates to existing assertions. When new evidence appears, relationships already accepted may need to be reconsidered. When the current state contains Claims that have no known relationship, the structure itself may provide reasons to investigate whether a relationship has been overlooked. These are different activities. Treating all of them as generic “AI reasoning” obscures important differences in what is being asserted, what is already accepted, what is being challenged, and what remains speculative.

This paper distinguishes four operations.

**Construction asks what Claims exist.** It converts source material into explicit knowledge assertions and resolved semantic properties.

**Integration asks how known Claims are related.** It establishes relational commitments among Claims that already exist.

**Reconstruction asks whether Relations already accepted still hold.** It re-examines existing relational structure under changed evidence, conditions, or context.

**Exploration asks whether Claims currently treated as unrelated may in fact be related.** It produces candidate relationships that remain outside the accepted state until evaluated.

These four operations are not proposed as an exhaustive taxonomy of all possible knowledge operations. Archival, deprecation, synchronization, cross-state merging, projection, and other operations may also be necessary in practical systems. The purpose here is narrower: to identify the minimum operational distinctions required to explain how the persistent knowledge architecture developed in the companion paper can be formed, connected, revised, and expanded.

The distinction matters for Engineering Determinacy. Its governing principle is that once an interpretation has been explicitly established and accepted, routine use should not require that interpretation to be reconstructed. This does not imply that accepted knowledge is permanent. It implies that a change to accepted knowledge should itself be recognizable as a change.

A newly generated interpretation and a previously accepted commitment should therefore not occupy the same epistemic position. Nor should the system silently overwrite the latter with the former. New knowledge may be proposed probabilistically, but the transition from proposal to commitment remains governed.

This paper makes three contributions.

First, it develops an operational model of persistent knowledge evolution based on four distinct epistemic responsibilities: assertion construction, relation establishment, accepted-relation review, and candidate-relation discovery.

Second, it distinguishes the epistemic state of knowledge from its content. A semantically plausible Claim or Relation produced by an AI system is not accepted merely because it is well formed. Its status depends on how it was established and on the governance mechanism through which it was admitted.

Third, it connects knowledge evolution to Engineering Determinacy by separating accepted knowledge from candidate knowledge throughout the change process. Exploration produces candidates rather than commitments; Reconstruction makes reconsideration explicit rather than silently replacing accepted knowledge; and Admission remains an independent governance mechanism that determines when proposed knowledge becomes part of the governed state.

The result is an account of knowledge evolution in which persistence and change are not opposing goals. Persistent structure provides continuity. Explicit operations provide controlled change.

---

# 2. Preconditions for Knowledge Evolution

The four operations described later do not act on an undifferentiated graph. They depend on two prior conditions: the system must distinguish the epistemic status of knowledge elements, and the structures on which runtime operations operate must have been designed deliberately.

## 2.1 Epistemic State

The epistemic state of a knowledge element is determined by how that element was established and confirmed, not merely by what it says.

This distinction is particularly important in AI-assisted knowledge systems because semantically similar objects may have very different evidential status. Consider two identical Attributes indicating that a service operates in a production environment. One may have been imported from an authoritative configuration-management system. The other may have been inferred by a language model from an ambiguous paragraph. Although their values are identical, it does not follow that the organization should treat them identically.

The architecture therefore separates content from epistemic status.

Knowledge imported from a governed source may, according to an organization's source policy, enter the knowledge state as accepted. Human-entered information may similarly be accepted when the person supplying it is acting as the designated authority. By contrast, a Claim, Attribute, Relation, or Qualifier generated through probabilistic inference should normally remain a candidate until it satisfies the applicable validation and admission requirements.

This does not mean that governed systems are infallible or that human assertions are necessarily correct. Accepted status is not a declaration of objective truth. It is a declaration that the organization has decided to rely on that element under a defined governance process.

The distinction applies at a finer level than an entire Claim. A Claim may be accepted while one newly inferred Attribute remains candidate. A Relation may already be accepted while a proposed additional Qualifier is still under review. This matters because AI-assisted enrichment often occurs incrementally. Treating the epistemic status of an entire object as indivisible would force organizations either to reject useful accepted knowledge whenever one uncertain property is added or to treat speculative enrichment as though it had already been confirmed.

For the purposes of this paper, four broad states are sufficient. A **candidate** has been proposed but not accepted. An **accepted** element belongs to the governed knowledge state. An element **under review** has previously been accepted but has been explicitly reopened because new information may affect it. A **superseded** or rejected element no longer functions as the current accepted commitment, although its historical existence may still matter for provenance and accountability.

Admission governs transitions into the accepted state. It is not itself one of the four knowledge operations. Construction can generate a candidate Claim; Integration can generate a candidate Relation; Reconstruction can reopen an accepted Relation; Exploration can generate a speculative relational candidate. Admission determines whether any candidate satisfies the evidential, structural, and governance requirements for acceptance.

Importantly, admission does not guarantee truth. Its purpose is to make commitment explicit.

## 2.2 Design Before Operation

Runtime operations also presuppose structural design.

Before a system can construct Claims, designers must decide what counts as a knowledge assertion and at what granularity assertions should be represented. Before Attributes can be populated, the system must know which semantic distinctions matter for its applications. Before Integration can establish Relations, some relation vocabulary or extensible taxonomy must exist. Before Qualifiers can delimit applicability, the system must know which boundary dimensions—such as environment, time, scope, jurisdiction, version, authority, or condition—are relevant. Before Viewpoints can be used to organize knowledge, the recurring interpretive perspectives that matter to the organization must be identified.

Two design operations are particularly important: **Extraction** and **Attachment**.

Extraction makes semantics already contained in source material explicit. A sentence stating that a production service must sustain ten thousand transactions per second may yield Attributes identifying the statement as a requirement, the environment as production, the metric as transactions per second, the value as ten thousand, and the load mode as sustained.

Attachment adds semantics required by the knowledge system but not expressed directly in the source. An organization may attach an accountable owner, an external requirement identifier, a governance classification, a review date, or an internal priority. Such properties can be essential to later operations even though they are not recoverable from the source sentence itself.

The distinction matters because the two forms of information have different provenance. An extracted Attribute claims to represent meaning found in the source. An attached Attribute represents an additional organizational decision or governance requirement.

The relevant structures are not necessarily fixed once for all applications. The companion paper argues that Attribute requirements emerge from the decisions that depend on them rather than from a universal schema [1]. The same principle applies here. Relation types, Qualifier dimensions, and Viewpoints may expand as new uses appear.

Design evolution has operational consequences. Adding a new Qualifier dimension, for example, may expose that previously accepted Relations were recorded too broadly. Introducing a new Viewpoint may reveal that existing Relations need additional structural roles or contextual distinctions. Structural design therefore precedes runtime operation, but design changes may themselves trigger Reconstruction.

The purpose of this section is not to specify a development methodology for knowledge systems. It establishes only that runtime operations do not define their own semantics opportunistically. Determinacy requires the structures through which knowledge is changed to remain explicit enough that the same operation does not invent a different representation every time it runs.

---

# 3. Four Knowledge Operations

The four operations differ primarily in the epistemic question each asks.

Construction asks whether an assertion should exist as an explicit knowledge object. Integration asks whether a relationship should be established among existing assertions. Reconstruction reopens relationships that the organization has already accepted. Exploration considers relationships that the organization has not yet accepted and may never have considered.

Separating these questions prevents the entire knowledge lifecycle from collapsing into one opaque process of model inference.

## 3.1 Knowledge Construction

Knowledge Construction establishes what knowledge assertions exist.

Its input may be a document, a retrieved passage, an event record, a database row, an API response, a human statement, a transcript, or another source from which knowledge assertions can be identified. Its output is one or more explicit Claim Objects together with the semantic Attributes resolved during interpretation.

Construction deliberately stops before relational interpretation.

Consider the statement:

> The production transaction service shall sustain 10,000 transactions per second.

Construction may identify this as a single requirement Claim and externalize several semantics: the subject is the transaction service, the environment is production, the metric is transactions per second, the target is ten thousand, and the required load mode is sustained.

At this point the architecture has established an assertion identity. It has not yet established that the requirement is constrained by a connection pool, supports a business objective, depends on a database, or conflicts with an infrastructure budget. Those are relational commitments and belong to Integration.

This separation is epistemically important. A system may be highly confident that two Claims accurately represent statements found in two authoritative sources while having no justified basis for connecting them. Conversely, uncertainty about a proposed Relation should not force the system to treat the existence of the underlying Claims as uncertain.

Construction therefore answers a narrower question than many end-to-end extraction pipelines. It asks: *what should exist as an explicit Claim, and which semantics of that Claim have already been resolved?*

The process may be automated, manual, or hybrid. A language model may identify propositions and infer candidate Attributes. A parser may extract structured values. A source connector may map fields deterministically. A human may create a Claim directly. The architecture does not prescribe a single construction algorithm.

What matters is that the resulting knowledge element retains epistemic status.

A Claim produced by model interpretation is not accepted merely because its representation is syntactically valid. It remains candidate until it satisfies the applicable admission requirements. A Claim imported from a source declared authoritative under the organization's governance policy may enter accepted state directly. The same distinction applies to individual Attributes.

Construction quality therefore cannot be reduced to extraction accuracy alone. Accuracy remains important: an incorrectly interpreted source can produce a wrong Claim. But the architecture adds another requirement. Resolved semantics and unresolved uncertainty should be represented in a form that can be inspected before the organization commits to them.

This requirement becomes increasingly important as AI systems perform richer extraction. A model that converts a paragraph into ten highly structured fields may appear more useful than one that extracts only three. Yet if seven of those fields are speculative, the added structure can increase rather than reduce semantic risk if all ten are stored without distinction.

Construction under Engineering Determinacy is therefore not the elimination of uncertainty. It is the conversion of interpretation into explicit objects whose certainty, provenance, and admission status can be governed.

## 3.2 Knowledge Integration

Knowledge Integration establishes relational structure among Claims that already exist.

Given two or more existing Claims, Integration may establish one or more Relations among them. Each Relation identifies the Claims it connects, the type of relationship asserted, the conditions under which the relationship holds, and the basis supporting the assertion.

Consider an accepted performance requirement and an accepted capacity statement. The first states that a production transaction service must sustain ten thousand transactions per second. The second states that a particular connection-pool configuration supports a defined level of concurrency under a measured deployment configuration.

Those Claims can exist independently. Integration begins only when the system proposes that the capacity represented by the second Claim constrains fulfillment of the first.

That proposal is a new epistemic commitment.

This distinction is fundamental. Accepting Claim A and accepting Claim B does not entail accepting Relation R between A and B. Relation R needs its own basis.

The Grounding Basis may refer to the Attributes of the Claims, measured evidence, another accepted Relation, an external specification, a rule, a human judgment, or some combination. Qualifiers then delimit the context in which the Relation is intended to hold. A constraint established from a production load test, for example, should not automatically be interpreted as applying to development environments, different deployment topologies, or later software versions.

Integration therefore produces more than connectivity. It produces *qualified connectivity with inspectable justification*.

This is one point at which the architecture differs from a simplistic view of graph growth. Adding an edge is technically trivial. Accepting the edge as organizational knowledge is not.

Knowledge graph research already covers entity and relation extraction, graph population, representation learning, and the inference of missing relations at significant depth [2, 3]. The present architecture does not introduce a new extraction or link-estimation algorithm. Its concern is the epistemic responsibility of an established Relation: why does this relationship exist in the governed state, and under what conditions may downstream work rely on it?

Integration can also alter the organization of existing knowledge without changing the Claims themselves. A previously isolated Claim may satisfy the selection criteria of a Viewpoint once it acquires a relevant Relation. A Domain derived from that Viewpoint may therefore expand automatically. The content has not been duplicated into a new store; the relational state has changed, causing a different derived organization to become valid.

Integration can occur at different times from Construction. A newly constructed Claim may immediately participate in candidate Relations, but it need not. Some Claims may remain isolated for long periods. Their lack of a current Relation is not itself an error. It becomes significant only when there is a reason to expect connectivity or when later Exploration identifies a plausible relational opportunity.

This distinction becomes important for the fourth operation. Integration establishes Relations for which there is already a specific proposed basis. Exploration asks whether a basis worth investigating might exist where no accepted Relation currently does.

## 3.3 Knowledge Reconstruction

Knowledge Reconstruction reviews relational commitments already present in the accepted knowledge state.

This operation addresses a consequence of persistence that can otherwise become dangerous. Once a Relation is accepted and routinely reused, downstream systems may stop questioning it. That is precisely what Engineering Determinacy intends for normal reuse: accepted meaning should not need to be probabilistically reconstructed on every query. But the same stability becomes harmful if changed evidence can never reopen the commitment.

Reconstruction provides that reopening mechanism.

A Reconstruction trigger may be a newly accepted Claim, new evidence, withdrawal of previous evidence, a change in environmental conditions, a new version of a system, an updated policy, a changed authority, or the discovery that a previous applicability boundary was incomplete.

The question is no longer *could these Claims be related?* The system already believes they are related. The question is:

> Does the Relation we have already accepted still hold in the way we currently represent it?

Several outcomes are possible.

The Relation may be retained unchanged because the new information does not materially affect its basis or applicability.

Its Qualifiers may be revised. A Relation previously treated as generally applicable may become restricted to a particular environment, version, region, authority, or operating condition.

The Relation may be superseded by another Relation that better represents the new state while preserving the historical relationship between the old commitment and its replacement.

It may be removed from current accepted knowledge when its basis has failed and no replacement is justified.

Reconstruction may also reveal a previously omitted Relation, causing new Integration work.

A significant implication follows: **knowledge evolution is not equivalent to graph-topology evolution**.

Suppose an accepted Relation states that a throughput requirement is constrained by a particular capacity limitation. New evidence shows that the limitation applies only when autoscaling is disabled. The same two Claims remain connected by the same general relation type. A topology-only comparison may show no change at all. Yet the organization's commitment has changed substantially. What was previously understood as a broad constraint is now accepted only under a narrower condition.

The knowledge change exists in the Qualifier.

This is one reason qualified Relations are central to the architecture. If applicability remains implicit, Reconstruction cannot distinguish changing a relationship from changing the conditions under which it holds.

Reconstruction also applies beyond individual base Relations.

A persistent Viewpoint organizes Relations into a recurring interpretive structure. If one of the Relations essential to that structure is invalidated or substantially narrowed, the Viewpoint may no longer organize the relevant knowledge coherently. A derived Domain may therefore change even when many underlying Claims remain untouched.

Conversely, newly established Relations may create a structural pattern that supports a Viewpoint that did not previously exist. This paper does not attempt to formalize automatic Viewpoint emergence or collapse, but the possibility follows from treating Viewpoints as persistent relational structures rather than labels.

Reconstruction must preserve history where accountability matters. Silent overwrite would defeat the purpose of persistent accepted knowledge. When a Relation changes, the system should be able to distinguish the prior accepted commitment from its successor and identify why the transition occurred.

This does not imply that every implementation must retain every historical state forever. Retention policy is a separate governance problem. The architectural principle is simply that revision should be represented as revision rather than masquerading as though the new interpretation had always been the accepted one.

Ontology evolution and ontology change research already provide mature accounts of change detection, consistency management, versioning, propagation, and process-oriented change [6, 7]. Reconstruction is therefore not presented as a new general theory of ontology evolution. Its role in this architecture is more specific: it ensures that the stability created by Engineering Determinacy does not prevent accepted relational commitments from being explicitly reopened when their grounding or applicability changes.

## 3.4 Knowledge Exploration

Knowledge Exploration examines whether Claims currently lacking an accepted Relation may plausibly be related.

This is the most speculative of the four operations and therefore requires the clearest separation between candidate and accepted knowledge.

Exploration begins from an existing governed knowledge state. It does not begin from an empty prompt asking an AI system to invent possible associations. Instead, it uses structure already present in the state to direct attention toward relational possibilities that may be worth investigating.

Several kinds of structure can provide such direction.

Two Claims may share relevant Attributes or contextual dimensions.

Existing Relations may form a pattern with a missing connection.

Qualified Relations in one part of the knowledge state may resemble a structure appearing elsewhere.

Different Viewpoints may select the same Claims but assign them different structural roles, exposing tensions or missing explanations.

A pattern established in one Domain may suggest a question worth testing in another Domain.

None of these signals establishes that a new Relation is true.

Their role is to make the question less arbitrary.

Consider an accepted throughput requirement and an accepted statement describing capacity limits in a regional data service. Suppose no accepted Relation currently connects them. Exploration may notice that both apply to the same production environment, that the capacity Claim resembles another Claim already known to constrain the throughput requirement, and that the same Viewpoint pattern places capacity limits in a bottleneck role.

This structure provides a reason to ask whether the regional capacity may also constrain the requirement.

The output is a candidate Relation, not an accepted Relation.

The candidate should identify the proposed relation type, the Claims involved, the conditions under which the relationship might hold, and the basis for proposing it. If the candidate arose partly because of analogy to an existing structural pattern, that pattern should remain inspectable. If apparent compatibility depends on particular Attributes or Qualifiers, those dependencies should remain visible.

A candidate may also carry an evidence profile.

This paper deliberately avoids reducing that profile to a universal confidence score. A number such as 0.73 is difficult to interpret unless the mechanism and calibration producing it are known. Instead, the profile can preserve dimensions relevant to evaluation: how many independent accepted structures support the candidate, whether those supports ultimately depend on the same evidence, how much Attribute correspondence exists, whether proposed Qualifiers are compatible with existing conditions, whether existing paths provide structural support, and whether the current state contains contradiction.

The Grounding Basis and evidence profile serve different purposes.

Grounding explains why the candidate was proposed.

The evidence profile describes how strongly the currently available structure supports continued consideration of that candidate.

Independence matters. Five Relations derived from the same source should not automatically be treated as five independent confirmations. Conversely, a smaller number of Relations supported by genuinely independent evidence may provide a more diverse basis for investigation. This paper does not define an aggregation function, weighting scheme, or calibration rule. Those questions require empirical work.

Exploration remains distinct from Integration even when both use similar inference techniques. A link-prediction model, an LLM, a rule engine, or an analogical mapping system might participate in either operation. The difference lies in epistemic purpose.

Integration evaluates a particular relational commitment for incorporation into governed knowledge.

Exploration searches for relational possibilities that are not yet commitments.

This distinction prevents hypothesis generation from silently becoming knowledge insertion.

It also allows unsuccessful Exploration to remain useful. A candidate that is evaluated and rejected may be retained as a historical exploration record if doing so prevents repeated investigation of the same unsupported relationship. The record should not appear as an accepted Relation, but its existence can still reduce redundant reasoning.

Knowledge Exploration overlaps substantially with knowledge graph completion, link prediction, literature-based discovery, abductive reasoning, and analogical reasoning. The architecture does not claim that discovering previously unstated relationships is new. Its contribution lies in placing relational discovery inside a governed knowledge lifecycle where candidate status, proposed applicability, grounding, and possible admission remain explicit.

---

# 4. Interaction Among the Operations

The four operations are easier to understand as interacting responsibilities than as stages of a fixed pipeline.

Construction produces explicit Claims. Integration establishes relationships among Claims. Reconstruction revisits relationships the organization already accepts. Exploration proposes relationships the organization has not yet accepted.

A typical lifecycle may pass through all four, but it does not have to do so in a fixed sequence.

A new document may trigger Construction. The resulting Claim may immediately participate in Integration, or it may remain isolated.

A newly accepted Relation may affect other accepted Relations and therefore trigger Reconstruction.

Reconstruction may identify the need for an additional Relation, leading back to Integration.

Exploration may produce a candidate Relation that later enters Integration for evaluation.

A newly constructed Claim may create a structural pattern that triggers Exploration before any new accepted Relation has been added.

The operations are therefore event-driven rather than sequential.

Admission remains orthogonal to this interaction.

Construction can generate a candidate Claim without admitting it.

Integration can generate a candidate Relation whose structural form is complete but whose evidence is insufficient.

Reconstruction can move a previously accepted Relation into an explicit review state without immediately replacing it.

Exploration can generate many candidates, most of which may never become accepted.

This separation is important because otherwise the architecture would conflate *producing a structured object* with *authorizing downstream reliance on that object*.

The same distinction applies to probabilistic and deterministic mechanisms. None of the four operations is inherently “AI” or “non-AI.” Construction may be deterministic when mapping a governed database field and probabilistic when extracting an assertion from natural language. Integration may follow a deterministic rule or depend on model reasoning. Reconstruction may be triggered by a temporal rule but require human adjudication. Exploration is likely to use probabilistic methods frequently, but rule-based structural gap detection may also participate.

Engineering Determinacy therefore does not classify entire operations as deterministic or probabilistic. It classifies individual knowledge commitments according to whether their meaning and status are already established.

Once an accepted Relation exists, routine downstream use can rely on it. When the Relation becomes subject to Reconstruction, uncertainty is reintroduced explicitly. When Exploration proposes a new relationship, uncertainty remains explicit from the start.

This gives knowledge change a recognizable boundary.

An organization can distinguish:

- what it currently accepts,
- what it is reconsidering,
- what it is merely exploring,
- and what has been rejected or superseded.

The four operations are not claimed to cover every possible manipulation of persistent knowledge. Deprecation policies, archival, cross-repository merging, projection, synchronization, access control, retention, and deletion may all require additional mechanisms. The claim is narrower: Construction, Integration, Reconstruction, and Exploration are sufficient to explain the formation and relational evolution addressed in this paper.

---

# 5. Illustrative Scenario: Evolution of a Performance Requirement

The following scenario extends the example used in the companion architecture paper. It is illustrative rather than empirical. Its purpose is to show how the four operations change the epistemic status and relational organization of the same knowledge over time.

A requirements repository contains the statement:

> The production transaction service shall sustain 10,000 transactions per second.

A separate configuration and test record describes the connection-pool configuration used during production load testing. Later records describe autoscaling behavior and a regional database capacity constraint.

## Construction

The requirements statement is interpreted as a Claim representing a performance requirement. Its relevant Attributes identify the subject as the transaction service, the environment as production, the metric as transactions per second, the target as ten thousand, and the load mode as sustained.

A second Claim represents the connection-pool capacity under a specified deployment configuration. Its Attributes identify the relevant capacity value, deployment version, and test environment.

If the first Claim is produced through AI-assisted interpretation of natural language, it initially carries candidate status unless the relevant process admits it. If the second Claim is imported from a governed configuration or measurement system, source policy may permit it to enter as accepted. Their epistemic states need not be identical merely because both are represented as Claims.

At this stage, no relationship between the two Claims is required.

## Integration

Load-test evidence and configuration analysis indicate that, under the tested production conditions, the connection-pool configuration limits the system's ability to satisfy the sustained throughput requirement.

Integration therefore proposes a `constrainedBy` Relation between the requirement Claim and the capacity Claim.

The Relation is not accepted merely because both Claims are accepted. Its Grounding Basis references the measured capacity evidence, the target throughput, the relevant deployment configuration, and the test result. Its Qualifiers delimit the relationship to the production environment and sustained-load condition represented in the evidence.

Once admitted, the Relation becomes part of the governed knowledge state.

An architecture Viewpoint may treat the Relation as identifying a bottleneck. An operations Viewpoint may treat the same Relation as a scaling boundary. The underlying Relation remains shared.

## Reconstruction

A later Claim states that autoscaling has been introduced for the transaction service.

This new Claim does not automatically invalidate the existing `constrainedBy` Relation. It triggers a question: does the previously accepted constraint still hold under the new operating condition?

The Relation enters review.

Further evidence shows that the specific connection-pool constraint remains relevant only when autoscaling is disabled or when scaling has not yet crossed a defined threshold. The accepted relationship therefore requires a narrower applicability boundary.

The relation type and connected Claims may remain unchanged. The Qualifier changes.

From the perspective of graph topology, the knowledge appears stable: the same Claim is still related to the same other Claim by the same general relationship. From the perspective of organizational commitment, the knowledge has changed materially. The organization no longer accepts the constraint as generally applicable to the production service.

This is Qualifier-induced Reconstruction.

The prior version of the Relation may be retained as superseded history, together with the evidence and event that caused the revision.

## Exploration

A later system inventory introduces another accepted Claim describing a capacity limitation in an EU regional database service.

No accepted Relation currently connects that Claim to the throughput requirement.

Exploration identifies several reasons that the relationship may be worth investigating. Both Claims apply to the production environment. The database Claim describes a capacity boundary. Existing accepted knowledge already contains a pattern in which another capacity limitation constrains the same throughput requirement. Under the architecture Viewpoint, capacity-limiting structures commonly occupy a bottleneck role.

These observations do not justify directly adding a new constraint Relation.

Instead, Exploration produces a candidate: the throughput requirement *may be constrained by* the regional database capacity under particular operating conditions.

The candidate records why it was proposed. Its proposed Qualifiers identify the relevant region and production context. Its evidence profile notes structural support from the existing capacity-constraint pattern, partial Attribute correspondence, and the current absence of a known contradiction.

The candidate then becomes eligible for further evidence collection and Integration.

If evaluation supports the relationship and admission requirements are satisfied, Integration establishes an accepted Relation. If not, the candidate remains rejected or unresolved rather than entering the governed knowledge state.

The scenario illustrates the central distinction of the paper.

Construction made assertions explicit.

Integration created an accepted relationship.

Reconstruction changed what the organization was prepared to say about that relationship.

Exploration produced a reason to investigate a relationship that had not previously been accepted.

At no point does the architecture require an AI system to treat every plausible inference as knowledge.

---

# 6. Related Work and Positioning

The four operations overlap with established bodies of research. The purpose of this section is therefore not to search for terminological novelty, but to compare architectural responsibilities.

## 6.1 Knowledge Acquisition and Knowledge Graph Construction

Conventional RAG pipelines primarily prepare source material for retrieval through operations such as cleaning, segmentation, enrichment, embedding, and indexing [10]. The operations defined here are not an alternative indexing pipeline; they concern the construction and evolution of explicit knowledge structures under Engineering Determinacy, after semantic interpretations have become candidates for persistent organizational knowledge.

Knowledge graphs provide structured representations in which entities, properties, and relations can be acquired from heterogeneous sources and used for querying, reasoning, and downstream applications [2]. Surveys of knowledge graph research cover representation learning, entity and relation extraction, knowledge acquisition, completion, and knowledge-aware applications [3].

These areas directly overlap with Construction and Integration.

Information extraction systems identify entities, attributes, events, and relations from text. Knowledge graph construction pipelines transform extracted information into persistent graph structures. Existing systems may combine deterministic mapping, ontology alignment, rule-based extraction, statistical models, or neural models.

This paper does not claim novelty for converting source material into structured statements or for creating graph relations.

The architectural distinction lies in separating two epistemic commitments that end-to-end pipelines may operationally combine.

Construction establishes that a Claim exists as an explicit assertion.

Integration establishes that a specific Relation among Claims is accepted.

The distinction allows a Claim to remain useful without requiring speculative relationships to be accepted, and it allows the evidential basis of a Relation to be evaluated independently from the provenance of its Claims.

Admission adds a further separation between successful structural generation and organizational acceptance. A model may correctly produce a syntactically valid Claim or Relation without the organization yet being prepared to rely on it.

The proposed operations therefore sit above particular extraction algorithms. They classify what kind of knowledge commitment is being made rather than how a model computes it.

## 6.2 Knowledge Revision and Ontology Evolution

Ontology evolution and ontology change provide the closest established research base for Reconstruction.

Flouris et al. survey multiple forms of ontology change and the relationships among fields dealing with modification, versioning, inconsistency, and evolution [7]. Zablith et al. provide a process-centric account of ontology evolution, emphasizing that change involves multiple stages including detection, representation, implementation, validation, and propagation [6].

Reconstruction should not be interpreted as replacing this literature.

Its purpose is to express how change operates within the particular knowledge architecture defined by the companion paper.

Two aspects are especially important.

First, Reconstruction treats the Grounding Basis and Qualifiers of accepted Relations as first-class targets of review. A Relation can change epistemically without disappearing structurally. Narrowing its applicability from a general production condition to a condition valid only when autoscaling is disabled changes what the organization accepts even though the connected Claims and relation type remain the same.

Second, Reconstruction extends to persistent Viewpoint structures. Because Viewpoints organize shared Relations into recurring interpretive structures, changes to the underlying Relations can alter the validity of derived Domains or the coherence of the Viewpoint itself.

These observations are compatible with ontology evolution rather than alternatives to it. The contribution is to position such change relative to the determinacy boundary between routine reuse and explicit reconsideration.

## 6.3 Knowledge Graph Completion and Link Prediction

Knowledge graph refinement research includes both correcting erroneous knowledge and adding missing knowledge [4]. Knowledge graph completion and link prediction methods estimate plausible relations that are not already represented. Embedding approaches such as TransE model relational structure in vector spaces and evaluate candidate links based on learned patterns [5].

This is direct prior art for parts of Knowledge Exploration.

The novelty claim cannot therefore be that a system may infer a missing relationship from existing graph structure.

The distinction proposed here is architectural.

Exploration produces a governed candidate rather than treating predicted linkage as accepted knowledge. The candidate retains its proposed applicability boundary, grounding, epistemic status, and evidence profile. It can be rejected, retained for later review, or passed into Integration for possible admission.

This distinction becomes particularly important when link-prediction machinery is combined with language models. A plausible generated explanation can easily create the appearance that an inferred relation has already been established. Candidate status prevents plausibility from becoming commitment by default.

Likewise, confidence in the candidate is not assumed to be fully represented by a model probability. A model score may be one element of the evidence profile, but downstream governance may also care about evidence independence, qualifier compatibility, contradiction, authoritative sources, or structural support from accepted Relations.

Exploration therefore treats prediction as an input to a governed knowledge-change process rather than as the process itself.

## 6.4 Literature-Based Discovery and Analogical Reasoning

Knowledge Exploration also relates to research that seeks novel connections across previously disconnected bodies of information.

Swanson's work on literature-based discovery demonstrated that independently published literatures can contain complementary relationships whose combination suggests a novel hypothesis even when the source communities have not made the connection explicitly [8]. The well-known ABC pattern behind literature-based discovery illustrates that structural relationships can direct attention toward an unrecognized connection.

Gentner's structure-mapping theory similarly emphasizes relational structure in analogy. Rather than relying only on surface similarity between objects, structure mapping focuses on systems of relations and higher-order organization transferred from a base domain to a target domain [9].

Both lines of work are relevant to cross-domain Exploration.

A persistent knowledge architecture can expose relational patterns that recur across Viewpoint Domains or across otherwise disconnected collections of Claims. Those patterns may provide reasons to test a candidate Relation in a new context.

Again, structural correspondence does not establish truth.

The proposed distinction is that analogical or cross-domain discovery feeds a persistent governed knowledge state through an explicit candidate lifecycle. A relational hypothesis is represented with proposed conditions and grounding, remains epistemically distinct from accepted Relations, and can later be evaluated through Integration.

The value of this architecture is therefore not that it generates hypotheses where earlier methods could not. It is that it places hypothesis generation, accepted knowledge, revision, and reuse inside one explicit lifecycle.

## 6.5 Architectural Positioning

The relationship among the main research areas can be summarized conceptually.

Knowledge acquisition and graph construction provide methods for producing structured assertions and Relations. They form the closest prior art for Construction and Integration.

Ontology evolution and knowledge revision provide mature mechanisms for changing accepted representations. They form the closest prior art for Reconstruction.

Knowledge graph completion, link prediction, literature-based discovery, and analogical reasoning provide methods for identifying relational possibilities not currently represented. They form the closest prior art for Exploration.

The contribution of the present work lies in assigning these activities distinct epistemic responsibilities within the architecture established by *AI Knowledge Architecture*.

Construction does not imply Integration.

Integration does not imply truth.

Reconstruction is not routine reinterpretation.

Exploration does not imply acceptance.

Admission does not imply permanence.

Admission remains the control point separating candidate structures from governed commitments.

This separation is the operational counterpart of Engineering Determinacy.

---

# 7. Discussion and Limitations

The proposed distinction among Construction, Integration, Reconstruction, and Exploration clarifies responsibilities but leaves important technical and empirical questions unresolved.

## 7.1 Admission Remains Underspecified

Admission is central to the architecture but is not formalized here.

Different organizations may require human adjudication, authoritative source validation, schema constraints, deterministic tests, model agreement, evidence thresholds, approval workflows, or combinations of these mechanisms.

The architecture requires only that the transition into accepted knowledge be explicit.

This leaves substantial future work in defining risk-sensitive admission policies. A low-risk internal classification may justifiably use automatic rule-based admission, while a Relation affecting contractual, safety, financial, or regulatory commitments may require designated human authority.

The appropriate mechanism is domain-dependent.

## 7.2 Structural Compatibility Does Not Establish Truth

A candidate Relation may fit the existing knowledge structure well and still be wrong.

Two Claims may have compatible Attributes, matching Qualifiers, and a familiar relational pattern without sharing the causal, logical, or institutional relationship being proposed.

Integration therefore cannot rely on structural fit as a sufficient acceptance criterion.

This limitation is particularly important for Exploration. Pattern similarity is useful for directing attention, but it can also reproduce existing biases or create attractive but unsupported analogies.

The architecture separates these stages precisely because discovery evidence and acceptance evidence need not be the same.

## 7.3 Reconstruction Triggers and Propagation Require Further Work

This paper explains why accepted Relations must sometimes be reopened but does not define a complete triggering model.

Some triggers are direct. The authoritative source grounding a Relation may be withdrawn or superseded.

Others are indirect. A Claim referenced by a Relation may change, creating a possible effect on downstream Relations. A revised Qualifier may alter the Domain derived under a Viewpoint. One reconstructed Relation may therefore require review of additional structures.

Determining the appropriate propagation scope is difficult.

Too little propagation leaves dependent knowledge stale. Too much propagation causes expensive and unnecessary review.

A mature implementation will require explicit dependency analysis, impact rules, and possibly risk-based propagation policies.

## 7.4 Exploration Has a Search-Space Problem

If every pair of currently unrelated Claims is considered a possible Exploration target, the candidate space grows rapidly.

Attributes, Qualifiers, Viewpoints, and existing relational patterns can constrain that space, but this paper does not specify a complete search strategy or stopping condition.

Candidate ranking is similarly unresolved.

An evidence profile provides inspectable dimensions, but the paper deliberately avoids assigning universal weights or reducing them to a single score. Whether particular dimensions predict useful discoveries must be evaluated empirically.

The architecture therefore defines what an Exploration candidate should preserve, not how to optimize large-scale Exploration.

## 7.5 Evidence Profiles Are Not Yet Calibrated

The distinction between Grounding Basis and evidence profile is conceptual.

Grounding records why a Relation or candidate was proposed. The evidence profile describes aspects of the available support.

The dimensions suggested here—supporting relations, evidence independence, Attribute coverage, Qualifier compatibility, structural support, and contradiction—have not been calibrated as a predictive model.

Independent grounding is intuitively more informative than repeated evidence derived from the same source, but the appropriate representation of independence may vary considerably across domains.

Future empirical work is required before such profiles should be interpreted quantitatively.

## 7.6 Viewpoint-Level Evolution Requires Stronger Formalization

The companion architecture defines Viewpoints as persistent interpretive relational structures [1]. The present paper observes that changed Relations may cause Viewpoints to lose or gain structural coherence.

However, no complete formal criterion for Viewpoint collapse, emergence, split, or merge is provided.

This is significant because Viewpoints may become one of the mechanisms through which Exploration is constrained. A weak Viewpoint formalization would weaken cross-domain pattern transfer and make candidate generation overly dependent on subjective design.

Viewpoint evolution therefore remains a separate research problem.

## 7.7 The Four Operations Are Not Exhaustive

Construction, Integration, Reconstruction, and Exploration are deliberately limited.

A complete operational architecture may also require archival, expiration, deletion, retention, synchronization, migration, state merging, source reconciliation, projection, access-control transformation, and other operations.

Some may be expressible as special cases of Reconstruction or Integration. Others may deserve independent status.

The paper makes no completeness claim.

Its purpose is to isolate four operations necessary for reasoning about the transition from persistent representation to controlled knowledge evolution.

## 7.8 Design Quality Constrains Runtime Quality

Finally, runtime operations cannot compensate fully for poor structural design.

If important semantic distinctions were never extracted or attached, later Integration may establish relationships with incomplete context.

If Qualifier dimensions omit a relevant boundary, Reconstruction may fail to detect that a Relation has been generalized too broadly.

If Relation types are ambiguous, Exploration may produce candidates that cannot be meaningfully compared.

Engineering Determinacy therefore shifts some responsibility upstream. Making interpretation explicit creates governance opportunities, but it also makes representational design consequential.

The benefit is not automatic correctness. It is that the assumptions on which correctness depends become increasingly inspectable.

---

# 8. Conclusion

Persistent AI knowledge requires more than a durable representation.

Claims must first be constructed. Relationships among those Claims must be established. Relationships already accepted must sometimes be reconsidered. And persistent structure should be able to direct attention toward relationships that have not yet been considered.

This paper distinguished these responsibilities as four knowledge operations.

**Construction** identifies what Claims exist and externalizes the semantics already resolved about them.

**Integration** establishes explicit relational commitments among existing Claims.

**Reconstruction** revisits Relations the organization has already accepted when new evidence, conditions, or context may change their grounding or applicability.

**Exploration** identifies relationships that may be worth investigating but have not yet become knowledge commitments.

The distinction is epistemic rather than algorithmic. The same language model, rule engine, graph algorithm, human reviewer, or hybrid workflow may participate in several operations. What differs is the status of the knowledge being handled.

Construction concerns assertion identity.

Integration concerns relational commitment.

Reconstruction concerns revision of prior commitment.

Exploration concerns structured speculation.

Admission remains orthogonal to all four. A candidate structure does not become accepted merely because it has been generated, predicted, or represented successfully.

This distinction extends Engineering Determinacy beyond persistent representation.

The companion architecture argues that accepted interpretations should not need to be repeatedly reconstructed through probabilistic inference. The present paper adds the corresponding requirement for change: when accepted interpretation does need to change, that change should be explicit.

Engineering Determinacy therefore does not require knowledge to stop changing.

It requires changes in knowledge to become visible as changes.

**Persistent structure preserves knowledge; explicit operations govern how that knowledge changes.**

---

# Declarations

## Funding

The author received no specific funding for this work.

## Conflicts of Interest

The author declares no conflicts of interest.

## Data Availability

No empirical dataset was generated or analyzed for this conceptual architecture paper.

## Declaration of Generative AI and AI-Assisted Technologies

Generative AI tools were used during the preparation of this manuscript to support literature discovery, organization of arguments, language drafting, editing, and manuscript refinement. The research problem, Engineering Determinacy concept, operational model, conceptual distinctions, interpretation of prior work, and final scholarly claims were directed, evaluated, revised, and approved by the author. The author reviewed the generated material, verified cited sources and their characterization, and takes full responsibility for the content of the manuscript.

---

# References

[1] Tsai, S. (2026). *AI Knowledge Architecture: Why Organizations Do Not Yet Own the Knowledge Their AI Systems Produce*. Working paper.

[2] Hogan, A., Blomqvist, E., Cochez, M., d'Amato, C., de Melo, G., Gutierrez, C., Kirrane, S., Labra Gayo, J. E., Navigli, R., Neumaier, S., Ngonga Ngomo, A.-C., Polleres, A., Rashid, S. M., Rula, A., Schmelzeisen, L., Sequeda, J., Staab, S., & Zimmermann, A. (2021). Knowledge graphs. *ACM Computing Surveys*, 54(4), Article 71, 1–37. DOI: 10.1145/3447772.

[3] Ji, S., Pan, S., Cambria, E., Marttinen, P., & Yu, P. S. (2022). A survey on knowledge graphs: Representation, acquisition, and applications. *IEEE Transactions on Neural Networks and Learning Systems*, 33(2), 494–514. DOI: 10.1109/TNNLS.2021.3070843.

[4] Paulheim, H. (2017). Knowledge graph refinement: A survey of approaches and evaluation methods. *Semantic Web*, 8(3), 489–508. DOI: 10.3233/SW-160218.

[5] Bordes, A., Usunier, N., Garcia-Duran, A., Weston, J., & Yakhnenko, O. (2013). Translating embeddings for modeling multi-relational data. In *Advances in Neural Information Processing Systems*, 26, 2787–2795.

[6] Zablith, F., Antoniou, G., d'Aquin, M., Flouris, G., Kondylakis, H., Motta, E., Plexousakis, D., & Sabou, M. (2015). Ontology evolution: A process-centric survey. *The Knowledge Engineering Review*, 30(1), 45–75. DOI: 10.1017/S0269888913000349.

[7] Flouris, G., Manakanatas, D., Kondylakis, H., Plexousakis, D., & Antoniou, G. (2008). Ontology change: Classification and survey. *The Knowledge Engineering Review*, 23(2), 117–152. DOI: 10.1017/S0269888908001367.

[8] Swanson, D. R. (1986). Fish oil, Raynaud's syndrome, and undiscovered public knowledge. *Perspectives in Biology and Medicine*, 30(1), 7–18. DOI: 10.1353/pbm.1986.0087.

[9] Gentner, D. (1983). Structure-mapping: A theoretical framework for analogy. *Cognitive Science*, 7(2), 155–170.

[10] Gao, Y., Xiong, Y., Gao, X., Jia, K., Pan, J., Bi, Y., Dai, Y., Sun, J., & Wang, H. (2023). Retrieval-augmented generation for large language models: A survey. *arXiv preprint arXiv:2312.10997*.
