# AI Knowledge Architecture for Enterprise Knowledge Management

## From Semantic Units to Persistent Attribute and Relation States

**Spark Tsai**

Independent Researcher

Email: spark.tsai@gmail.com

ORCID: 0009-0006-8847-4703

---

## Abstract

Retrieval-augmented generation improves access to enterprise information but typically leaves query-time semantic interpretations dependent on each model invocation. This conceptual study applies AI Knowledge Architecture (AIKA) to enterprise knowledge management through two persistence responsibilities. First, semantic distinctions that have been explicitly established and accepted are externalized as Attributes. Second, accepted relationships among semantic units are externalized as persistent Relations rather than repeatedly inferred. Claims identify semantic units, while Qualifiers, Grounding, Viewpoints, and derived Domains make the resulting knowledge state bounded, inspectable, and reusable. An enterprise case demonstrates how this architecture converts transient interpretation into governed organizational knowledge across multiple functions. The paper defines a semantic unit as a meaningful assertion available for inference.

**Keywords:** Enterprise AI; Knowledge Management; Retrieval-Augmented Generation; Semantic Persistence; Relational Knowledge

---

# 1. Introduction

## 1.1 From Enterprise Repositories to RAG-Based Knowledge Access

Organizations have accumulated large bodies of internal information in requirements repositories, policy documents, contracts, specifications, operating procedures, technical records, databases, meeting records, issue histories, and other enterprise systems. Knowledge management technologies have long attempted to make these materials available for organizational use. More recently, large language models and retrieval-augmented generation (RAG) have substantially changed the way employees interact with such material.

Instead of requiring users to know where a document is stored, how it is classified, or which keywords it contains, a RAG-based system can retrieve relevant material and place it into the context of a generative model. The model can then summarize the retrieved information, compare multiple sources, answer questions, identify apparent dependencies, or explain implications in natural language (Lewis et al., 2020; Gao et al., 2023). Graph-based retrieval approaches extend this capability by organizing entities and relationships to support broader query-time synthesis and sensemaking (Edge et al., 2024).

This development addresses an important organizational problem: **access to information**.

Yet access to information and possession of organizational knowledge are not equivalent.

Consider an enterprise AI assistant working over a software requirements repository. A requirement states:

> The production transaction service shall sustain 10,000 transactions per second.

A RAG system can retrieve this statement. A language model can interpret it competently. It may determine that the statement is a requirement rather than an observation, that *production* identifies an applicability environment, that 10,000 is a target rather than a historical measurement, that transactions per second is the relevant metric, and that *sustain* distinguishes continuous load from a temporary burst.

The answer may be useful. A design decision may follow from it.

Three weeks later, however, another employee asks a related question. The same source statement is retrieved again, and the model interprets it again. The interpretation may be identical. It may be slightly different. A different model may emphasize different semantics. A later model version may reach another conclusion.

Nothing in the ordinary RAG cycle requires the organization to retain which parts of that semantic interpretation it has accepted as stable Attributes.

The source information persists.

The interpretation does not necessarily persist as an explicit enterprise state.

## 1.2 The Missing Transition from Semantic Interpretation to Organizational Knowledge

This problem becomes clearer when the unit represented by many AI-enabled knowledge systems is examined.

A contemporary RAG workflow may operate on documents, passages, chunks, embeddings, extracted entities, facts, propositions, summaries, or other semantic units. Such units are useful and often necessary. They allow a system to identify meaningful material rather than treat an enterprise repository as an undifferentiated body of text. In the bounded comparison developed in this paper, this is the **semantic layer**: the system has produced or retrieved a meaningful unit that can participate in inference.

Many RAG-oriented implementations effectively stop at this layer. A semantic unit is made retrievable and is then treated as the knowledge element supplied to the model. Any finer meaning within the unit, and any relationship between that unit and another, may still be reconstructed at query time.

AI Knowledge Architecture introduces two additional persistence steps for enterprise knowledge management.

First, when a semantic distinction within a unit has been explicitly established and accepted, it is represented as an **Attribute**. For example, *production* may be persisted as an environment, 10,000 as a target, and *sustain* as a sustained-load condition. The accepted meaning no longer exists only as an interpretation that a later model must reproduce.

Second, when a relationship between two semantic units has been explicitly established and accepted, it is represented as a persistent **Relation**. The relationship becomes part of the enterprise knowledge state rather than a conclusion that must be inferred again whenever the two units are retrieved together.

The operational contrast can be summarized as follows:

| Dimension                           | RAG-oriented workflow                                                      | AIKA-enabled workflow                                                          |
| ----------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Primary persistent object           | Source, chunk, embedding, extracted entity, or graph index                 | Identified Claim with governed knowledge state                                 |
| Meaning within a semantic unit      | May be reconstructed for the present query                                 | Accepted meaning is persisted as Attributes                                    |
| Relationship between semantic units | May be extracted or inferred for retrieval and response generation         | Accepted relationship is persisted as a Relation with Qualifiers and Grounding |
| Repeated query                      | The model may reinterpret the same units and regenerate their connection   | Routine reuse reads the accepted Attribute and Relation state                  |
| Governance status                   | Relevance or retrieval does not itself establish organizational acceptance | Admission distinguishes candidate interpretation from accepted commitment      |

The comparison is architectural rather than universal: particular RAG implementations may persist entities, edges, summaries, or memory records. AIKA asks the additional question of whether their meaning and relationships have been explicitly admitted as organizational commitments.

A semantic unit should therefore not automatically be equated with complete organizational knowledge.

The statement that a service must sustain 10,000 transactions per second conveys meaningful information. Representing that statement as an identifiable semantic assertion improves machine use. Nevertheless, an organization frequently needs to know considerably more:

- whether another system constraint limits the requirement;
- under which environment and operating conditions that limitation applies;
- what evidence established the limitation;
- whether the relationship has been accepted or remains speculative;
- how architecture, business, product, and operations functions organize the same information;
- and whether the organization has subsequently revised its earlier interpretation.

The organizationally consequential knowledge is therefore not contained only in an isolated semantic unit. It also exists in the relationships among semantic units, the conditions delimiting those relationships, the evidence supporting them, and the recurring organizational perspectives through which they are interpreted.

This paper adopts a deliberately bounded position:

> **RAG can supply semantic units as knowledge elements for query-time reasoning. AI Knowledge Architecture persists the accepted meaning within those units as Attributes and the accepted relationships among those units as Relations. Organizational knowledge is therefore represented not as semantic units alone, but as a governed persistent state of accepted semantics and accepted relational structure.**

The claim is architectural rather than philosophical. It does not propose a universal definition of knowledge. Knowledge has been treated in the knowledge management literature as an object, a process, a state of knowing, a capability, and a condition of access, among other perspectives (Alavi & Leidner, 2001). The present paper addresses a narrower systems question: **what must an enterprise AI system persist if an organization expects the results of AI-assisted interpretation to remain reusable organizational knowledge rather than transient model output?**

## 1.3 From Retrieval to Organizational Knowledge

Traditional knowledge management research has treated organizational knowledge as something that must be created, retained, transferred, applied, and embedded in organizational structures and processes (Nonaka, 1994; Alavi & Leidner, 2001). Organizational memory research similarly emphasizes the problem of storing and retrieving information from an organization's history in forms that can influence subsequent decisions (Walsh & Ungson, 1991).

RAG contributes powerfully to this tradition by improving access to recorded organizational material. But the RAG cycle primarily answers:

> **What information should be brought into the present inference context?**

A language model may then answer:

> **What might this information mean in the context of the present question?**

For enterprise knowledge management, another question follows:

> **What interpretation has the organization actually accepted, and how can that interpretation persist independently of the model invocation that produced it?**

This distinction matters because organizationally meaningful work often occurs between retrieval and final action.

Locating a requirement is retrieval.

Determining that another capacity statement constrains that requirement is interpretation.

Determining that the constraint applies only in production, under sustained load, is qualified interpretation.

Determining that the relationship rests on a particular measurement is grounding.

Accepting that interpretation for subsequent organizational use is a governance act.

If all of those results remain only inside a generated response, the organization possesses the source materials and perhaps the conversation transcript, but not an explicit knowledge structure representing what it decided those materials mean.

## 1.4 Organizational Ownership

As used in this paper, **organizational ownership of knowledge** does not refer to intellectual-property ownership.

In this paper, **organizational ownership of knowledge** is used operationally. An organization can be said to hold an accepted interpretation as an organizational knowledge asset when it can:

1. identify the interpretation independently of a past model response;
2. inspect what semantic commitments were accepted;
3. identify the relationships among those commitments;
4. determine the conditions under which those relationships apply;
5. inspect the basis on which they were accepted;
6. reuse them without requiring routine probabilistic reconstruction;
7. revise them explicitly when evidence or conditions change; and
8. account for the distinction between what is accepted, proposed, revised, or rejected.

A generated answer may contribute to organizational knowledge without itself satisfying these conditions.

This distinction separates **having access to previous AI output** from **possessing governed organizational knowledge**.

## 1.5 Research Question

The paper addresses the following research question:

> **RQ: How can enterprise AI systems extend RAG semantic units by persisting accepted semantic distinctions as Attributes and accepted relationships among semantic units as Relations, so established knowledge does not require repeated inference?**

The proposed answer is **AI Knowledge Architecture (AIKA) for enterprise knowledge management**.

AIKA operates downstream of retrieval. It does not replace RAG, knowledge graphs, provenance models, ontology views, or language-model reasoning. Instead, it defines an architectural boundary between interpretations that remain candidates and interpretations that have become accepted organizational commitments.

Once accepted, semantic distinctions are externalized as Attributes and relational interpretations are externalized as Relations rather than left to be reconstructed from source text and retrieval context at every later use.

## 1.6 Contributions

The paper makes three primary contributions.

**First, it distinguishes semantic availability from semantic persistence.** RAG can retrieve or produce a semantic unit, but the meanings resolved within that unit may still remain implicit. AIKA externalizes the accepted portion of those meanings as Attributes that can be reused directly.

**Second, it distinguishes semantic units from persistent relational knowledge.** The availability of two semantic units does not preserve an accepted relationship between them. AIKA externalizes established semantic-to-semantic relationships as persistent Relations, with Qualifiers and Grounding preserving where they apply and why they were accepted.

**Third, it positions AIKA as a knowledge-management layer downstream of RAG.** RAG supplies semantic material for present inference. AI reasoning proposes Attributes and Relations. An admission process determines which proposals become organizational commitments. AIKA preserves the accepted Attribute and Relation state for reuse.

The contribution is therefore not a new graph syntax or a claim that semantic units, relations, provenance, qualifiers, or views are individually novel. These mechanisms have substantial prior art. The contribution lies in assigning them a common organizational responsibility:

> **accepted semantics should become persistent Attributes, and accepted semantic relationships should become persistent Relations, rather than return unnecessarily to probabilistic reconstruction.**

---

# 2. Literature Review and Conceptual Positioning

## 2.1 Organizational Knowledge and Knowledge Creation

Knowledge management research has long distinguished knowledge from the mere possession of information. Nonaka (1994) describes organizational knowledge creation as a process through which individually held knowledge is articulated, amplified, and incorporated into organizational knowledge. In this view, organizations do not passively accumulate information; they participate in processes through which meaning becomes shared and operationally consequential.

Alavi and Leidner (2001) similarly describe knowledge as a multifaceted concept and identify knowledge creation, storage and retrieval, transfer, and application as central organizational knowledge-management processes. Their treatment is especially relevant to information systems because it positions knowledge management systems not simply as repositories but as technological support for a wider organizational knowledge lifecycle.

Davenport and Prusak (1998) likewise emphasize that knowledge management involves making knowledge visible, developing environments in which knowledge can be shared, and building knowledge infrastructures connecting people, processes, and technology.

These perspectives differ in theoretical orientation, but they share an important implication for AI-enabled knowledge management: **organizational knowledge cannot be reduced to the existence of source information alone.**

The introduction of generative AI makes this distinction more consequential. AI systems increasingly perform interpretive work that previously occurred primarily in human cognition and communication. They classify, compare, infer, summarize, connect, and contextualize organizational material. The outputs of those activities may shape decisions even when the interpretations themselves are not subsequently represented as organizational knowledge.

The problem examined in this paper therefore concerns not whether AI can generate useful interpretations, but whether an organization can subsequently identify which interpretations it has accepted.

## 2.2 Organizational Memory and Knowledge Retention

Organizational memory provides a second relevant foundation.

Walsh and Ungson (1991) conceptualize organizational memory in terms of information from an organization's history that can be stored and later brought to bear on present decisions. The broader organizational-memory literature therefore draws attention to the persistence problem: organizational learning has limited value if knowledge developed through prior activity cannot influence later activity.

Generative AI creates a new variant of this issue.

An enterprise may retain every source document consulted by an AI system. It may retain every user prompt and every model response. Yet neither guarantees that the organization can identify which interpretation became an accepted organizational position.

A transcript records that an interpretation occurred.

It does not necessarily establish that the interpretation was accepted.

Nor does it necessarily express the interpretation in a form suitable for deterministic reuse, comparison, qualification, or revision.

This distinction is important because an organization may possess excellent conversational memory while still having weak organizational knowledge memory.

AIKA therefore focuses not on preserving conversation as conversation, but on externalizing accepted semantic commitments into persistent structures.

## 2.3 Knowledge Management Systems and the Role of IT

Knowledge management systems have historically supported a range of processes including knowledge creation, storage, retrieval, transfer, and application (Alavi & Leidner, 2001). Different technological generations have emphasized different parts of this lifecycle.

Document repositories emphasize storage.

Enterprise search emphasizes retrieval.

Knowledge graphs emphasize explicit semantic structure.

Collaboration tools support sharing and collective interpretation.

Workflow systems embed knowledge in operational activity.

Generative AI expands the interpretive capacity of these systems. Instead of merely locating or displaying stored information, an AI system can infer structure from unstructured material, compare multiple sources, generate candidate explanations, identify possible contradictions, and adapt its response to the needs of different organizational roles.

This increased interpretive power creates a corresponding architectural requirement.

When an information system only retrieves a document, the retrieved document remains available for later use.

When an AI system derives an interpretation from that document and the interpretation influences organizational action, retaining only the document does not retain all of the knowledge produced during the interaction.

This paper therefore treats generative AI not merely as another interface to a repository, but as a participant in knowledge work whose accepted outputs may require explicit incorporation into organizational memory.

## 2.4 Retrieval-Augmented Generation and Query-Time Interpretation

RAG integrates external non-parametric information with model inference (Lewis et al., 2020). Its importance in enterprise contexts follows directly from a central weakness of standalone language models: organizations require answers grounded in information that may be private, current, domain-specific, or too extensive to encode reliably in model parameters.

A standard RAG workflow can be represented conceptually as:

**Source Material → Indexing → Retrieval → Context → Model Inference → Response**

The architecture is effective because it allows the model to reason over enterprise information at query time.

Graph-based RAG architectures further organize source material into graph structures that improve global summarization, relational retrieval, and sensemaking over large collections (Edge et al., 2024).

Agent-memory architectures address a related but different problem. MemGPT, for example, manages information across memory tiers to extend the effective context available to a language model during long-document analysis and multi-session interaction (Packer et al., 2023). GraphRAG constructs graph-based indexes and community summaries so a model can retrieve and synthesize corpus-level information more effectively (Edge et al., 2024). These approaches improve what information can be retained, selected, or brought into an inference context.

AIKA assigns a different responsibility to persistence. A memory record can remain useful without being an accepted organizational commitment, and a graph edge can support retrieval without recording that the organization has accepted the relationship it represents. AIKA therefore does not compete with agent memory or GraphRAG. Those systems can supply semantic material and candidate structure; AIKA records which meanings and relationships have crossed an explicit Admission boundary, under what conditions, and on what basis. The distinction is between **context continuity** and **governed commitment continuity**.

These systems improve access and query-time synthesis. In the comparison used here, their durable unit may remain the retrievable semantic element, while resolved properties of that element and conclusions about its relationships remain products of the current inference cycle. They do not necessarily require either result to become a governed organizational commitment for the next cycle.

That distinction is central.

Suppose a model concludes, using retrieved requirements and load-test evidence, that a connection-pool configuration constrains a throughput requirement only under sustained production load.

Several things may happen:

- the answer may be accepted by a user;
- a design decision may be made;
- the decision may enter implementation;
- the original documents may remain available;
- the model response may remain in a conversation log.

Nevertheless, a later RAG query may again retrieve the same semantic units and ask the model to reconstruct both levels of meaning: what each unit means for the present use and whether a relationship exists between the units, what that relationship means, and where its applicability boundary lies.

The system has retained the **materials** from which the conclusion was derived.

It has not necessarily retained the accepted semantics as **Attributes** or the accepted conclusion as a persistent **Relation**.

AIKA therefore positions RAG upstream of persistent organizational knowledge rather than as a competing architecture.

Retrieval supplies semantic material.

Interpretation proposes Attributes and Relations.

Admission establishes commitment.

Persistent knowledge structure preserves the accepted Attribute and Relation state.

## 2.5 Semantic Units and Persistent Knowledge Representation

Several established research areas provide representation mechanisms relevant to this problem.

Nanopublications provide identifiable units containing assertions and provenance information (Groth et al., 2010). Semantic-unit approaches structure knowledge graphs into bounded semantically meaningful units (Vogt et al., 2024). Trusty URIs demonstrate mechanisms for persistent and verifiable digital identity (Kuhn & Dumontier, 2014). Wikidata provides practical statement qualification mechanisms (Vrandečić & Krötzsch, 2014), while RDF-star supports statements about statements and therefore enables richer relational representation (Hartig, 2017). Provenance-aware approaches preserve lineage and contextual evidence associated with represented knowledge (Sikos & Philp, 2020).

These mechanisms demonstrate that persistent semantic identity, qualification, higher-order relations, and provenance are established capabilities.

AIKA claims novelty for none of them individually.

Instead, it draws an architectural distinction among three states:

1. a semantic unit is available for retrieval;
2. accepted meanings within that unit are persisted as Attributes; and
3. accepted relationships among semantic units are persisted as Relations.

A semantic assertion may identify that:

> The production transaction service shall sustain 10,000 TPS.

A second semantic assertion may identify that:

> The connection pool supports 500 concurrent connections under configuration X.

Persisting both assertions does not establish that one constrains the other.

That relationship is itself an interpretation.

Accepting the two Claims therefore does not imply acceptance of a Relation between them.

The Relation requires its own grounding and applicability boundary.

This is the point at which isolated semantic representation becomes persistent relational knowledge representation. The relationship no longer has to be regenerated whenever both semantic units appear in a new retrieval context.

## 2.6 From Semantic Units to Governed Semantic Networks

For the purposes of AIKA, an isolated semantic unit supplied by the semantic layer is given persistent identity as a **Claim**.

A Claim provides stable identity to an assertion. Semantic distinctions that have been explicitly resolved and accepted are persisted as its **Attributes**.

Organizational knowledge, however, frequently depends on structures of the form:

**Claim A — Relation R → Claim B**

subject to:

**Qualifier Q**

supported by:

**Grounding G**

and organized for recurring purposes through:

**Viewpoint V**

The resulting knowledge is relational and stateful.

This distinction has several implications.

First, the existence of two accepted semantic units does not entail that the organization accepts any relationship between them.

Second, a Relation that is accepted without its applicability boundary risks being interpreted too broadly.

Third, a Relation whose grounding cannot be inspected creates an accountability gap even if the relation itself is stored.

Fourth, different organizational functions may organize the same shared Claims and Relations differently without requiring separate knowledge copies.

Knowledge is therefore represented in AIKA not as a flat collection of independently retrievable semantic elements but as a governed persistent state: accepted Attributes preserve established meaning within Claims, while accepted Relations preserve established meaning between Claims.

## 2.7 Ontology Views and Perspective-Aware Representation

Prior work also addresses views over shared semantic structures.

Noy and Musen (2004) define ontology views through traversal specifications involving concepts, relationships, and constraints. Brinkley et al. (2006) describe architectures in which shared reference ontologies support application-specific views. Such work provides direct prior art for deriving subsets of a shared knowledge structure without maintaining independent copies.

AIKA builds on these ideas but assigns a specific organizational role to a **Viewpoint**.

A Viewpoint does not merely select knowledge. It persists an interpretive organization over shared knowledge identities. The same accepted Relation may function as a *bottleneck* from an architecture viewpoint and as a *scaling boundary* from an operations viewpoint.

The underlying Relation is shared.

The interpretive structural role differs.

This design allows organizational functions to maintain recurring perspectives without fragmenting the underlying knowledge state.

## 2.8 Research Gap

The literature reviewed above provides substantial foundations.

Knowledge management explains why organizations create, retain, transfer, and apply knowledge.

Organizational memory explains why persistence matters.

RAG provides powerful access to source information at inference time.

Knowledge representation provides semantic identity, relations, qualification, provenance, and graph structures.

Ontology and perspective research provide mechanisms for deriving and organizing alternative views.

What remains insufficiently explicit in common RAG-based enterprise AI architectures is the transition:

**from retrieved organizational information**

to

**retrieved or generated semantic units**

to

**accepted semantic distinctions persisted as Attributes**

to

**accepted semantic relationships persisted as Relations**

to

**persistent relational reuse without routine re-inference**.

The gap is therefore not the absence of semantic representation mechanisms or the inability of a model to infer relationships.

It is the absence of an architectural responsibility assigning persistent state to **accepted meaning within semantic units and accepted relationships among them**.

AIKA addresses this gap.

---

# 3. Methodology: Conceptual Architecture Development

## 3.1 Research Design

This study is a conceptual architecture study rather than an empirical hypothesis-testing study.

Conceptual research can contribute by integrating existing theoretical elements, clarifying distinctions, and constructing models through explicit analytical reasoning when the research problem concerns the organization and relationship of concepts rather than the measurement of a pre-existing causal model (Jabareen, 2009; Jaakkola, 2020).

The purpose of this paper is therefore not to estimate the performance of a particular implementation of AIKA.

It asks a prior architectural question:

> What must be represented persistently so that accepted meaning within semantic units and accepted relationships among semantic units can function as reusable organizational knowledge rather than transient query-time inference?

The architecture is derived through problem decomposition.

Repeated inference tasks within and between semantic units are identified first.

Each repeated interpretive responsibility is then mapped to a corresponding persistent knowledge structure.

The resulting structures are compared with established representation mechanisms to distinguish architectural responsibility from representational novelty.

Finally, an illustrative enterprise case is used to demonstrate internal operation and cross-role consequences.

## 3.2 Analytical Units

The analysis distinguishes five levels.

### Source Information

Source information includes documents, database records, measurements, configuration records, policies, requirements, contracts, transcripts, external evidence, and other enterprise materials.

Source information may contain knowledge, but AIKA does not assume that every source unit is already expressed at the semantic granularity needed for downstream reasoning.

### Semantic Unit

A semantic unit is a meaningful assertion retrieved, extracted, or generated from source information for use in inference.

For example, interpreting *production* as an environment, 10,000 as a target, or *sustain* as a sustained-load requirement involves interpretation rather than retrieval.

A Claim provides persistent identity to such a semantic assertion within AIKA. Identity makes the semantic unit addressable, but does not by itself preserve all meaning resolved within the unit or any relationship to another unit.

### Accepted Attribute State

Accepted Attribute state consists of semantic distinctions within a Claim that have been explicitly established and admitted for reuse.

For example, `environment = production`, `target = 10,000`, and `load mode = sustained` preserve resolved meaning that would otherwise remain dependent on repeated interpretation.

### Accepted Relation State

Accepted Relation state consists of explicitly established and admitted relationships among Claims.

It preserves what the organization has accepted about how semantic units are connected, including the relationship's applicability and grounding, so routine use does not require the connection to be inferred again.

### Governed Organizational Knowledge

Governed organizational knowledge consists of accepted Claims whose established semantic distinctions are represented as explicit Attributes, together with accepted Relations that preserve established semantic-to-semantic relationships. Applicability Qualifiers, inspectable Grounding, and persistent Viewpoints make that state bounded, accountable, and reusable for recurring purposes.

In simplified form:

**Organizational Knowledge in AIKA = Identified Semantic Claims + Accepted Attributes + Accepted Relations + Qualifiers + Grounding + Viewpoints**

This expression is not offered as a universal epistemological definition. It states the minimum persistent structure required by the architecture developed here.

## 3.3 Problem Decomposition

The architecture begins by identifying two classes of semantic questions that otherwise return repeatedly to inference: questions about meaning within a semantic unit and questions about relationships between semantic units.

### Assertion identity

Which knowledge assertion is being referenced?

Text identity is insufficient because different sentences may express equivalent propositions and a single sentence may contain multiple assertions.

### Resolved meaning within a semantic unit

Which meanings implicit in the source have already been established?

If *production* has already been accepted as the relevant environment, routine reuse should not require every model invocation to rediscover that fact.

### Resolved relationships between semantic units

How are two accepted assertions related?

The existence of two Claims does not establish a Relation between them.

### Applicability

Under which conditions does an accepted Relation hold?

A constraint valid under one environment, version, time period, jurisdiction, authority, or operational condition should not silently expand beyond that boundary.

### Grounding

Why was a Relation accepted?

Persistent relationships without inspectable basis weaken accountability and make later review difficult.

### Interpretive organization

How does a recurring organizational perspective select and organize shared knowledge?

Architecture, business, product, operations, compliance, and other functions may work over the same accepted knowledge while emphasizing different structures.

### View-specific membership

Which part of the shared knowledge state belongs to a recurring perspective at a particular point in time?

Maintaining separate copies for every organizational function introduces synchronization and identity problems.

## 3.4 Architecture Derivation

The decomposition leads to the following mapping:

| Repeated interpretive problem             | Persistent structure | Architectural responsibility                            |
| ----------------------------------------- | -------------------- | ------------------------------------------------------- |
| Semantic-unit identity                    | Claim                | Preserve the identity of a semantic element             |
| Repeated inference within a semantic unit | Attribute            | Preserve accepted semantic meaning                      |
| Repeated inference between semantic units | Relation             | Preserve an accepted semantic relationship as state     |
| Implicit applicability                    | Qualifier            | Preserve boundary conditions                            |
| Uninspectable justification               | Grounding Basis      | Preserve basis of acceptance                            |
| Repeated perspective reconstruction       | Viewpoint            | Preserve interpretive organization                      |
| Duplicated role-specific stores           | Derived Domain       | Reuse shared knowledge through deterministic derivation |

The architecture therefore follows one construction principle:

> **accepted meaning within a semantic unit is externalized as Attribute state, while accepted meaning between semantic units is externalized as Relation state.**

## 3.5 Determinacy as a Design Principle

The architecture applies a determinacy-oriented design principle:

> **Once an interpretation has been explicitly established and accepted, routine use should not require that interpretation to be re-inferred.**

This principle does not imply that probabilistic AI should be eliminated.

Probabilistic interpretation remains necessary where knowledge is new, ambiguous, incomplete, disputed, or insufficiently represented.

The principle distinguishes:

**discovery from reuse**

and

**revision from routine reinterpretation**.

It also does not claim that accepted knowledge is objectively true.

Persistence records organizational commitment, not epistemic infallibility.

An accepted interpretation may later prove wrong.

The architecture therefore requires revision to occur explicitly rather than through silent replacement during ordinary inference.

## 3.6 Conceptual Demonstration and Evaluation Boundary

The architecture is demonstrated using a single enterprise performance requirement and several related assertions.

The demonstration examines whether the architecture can represent:

1. stable semantic identity;
2. explicit resolved semantics;
3. relational commitments;
4. applicability boundaries;
5. inspectable grounding;
6. multiple organizational perspectives over shared knowledge;
7. cross-perspective comparison.

The case is illustrative rather than empirical.

It does not establish that AIKA improves organizational performance, reduces inference cost, increases model accuracy, or produces better decisions in deployed enterprises.

Those questions require implementation and empirical evaluation.

The purpose of the present analysis is narrower: to evaluate whether the proposed architecture provides a coherent persistent representation for the organizational knowledge problem identified.

---

# 4. AI Knowledge Architecture: Conceptual Framework

## 4.1 From RAG to Persistent Organizational Knowledge

AIKA can be positioned as a layer downstream of RAG-based enterprise AI:

**Enterprise Sources**

↓

**RAG — retrieve or produce relevant semantic units**

↓

**AI Reasoning — propose semantic Attributes and semantic-to-semantic Relations**

↓

**Admission — determine which interpretations become accepted commitments**

↓

**AI Knowledge Architecture — persist accepted Attribute and Relation state**

↓

**Organizational Reuse**

This separation prevents two common conflations.

First, retrieval is not acceptance.

A document returned by RAG does not automatically become an organizational commitment merely because it was relevant to a query.

Second, model generation is not acceptance.

A plausible interpretation generated by a language model remains a candidate unless the applicable organizational process allows it to become accepted knowledge.

The architecture therefore distinguishes a **probabilistic interpretation zone** from a **governed knowledge zone**.

Before admission, AI may retrieve, interpret, compare, hypothesize, and propose.

After admission, accepted meaning within semantic units becomes explicit Attribute state, and accepted meaning between semantic units becomes explicit Relation state.

The distinction is not between AI and non-AI processing.

It is between unresolved interpretation and accepted knowledge.

## 4.2 Admission: From Candidate Interpretation to Organizational Commitment

Admission is the boundary through which candidate semantic structures become accepted organizational knowledge.

AIKA deliberately does not prescribe a universal admission algorithm.

Different organizations and domains may use:

- designated human approval;
- authoritative source policies;
- deterministic validation;
- schema validation;
- evidence requirements;
- consistency checks;
- agreement across independent systems;
- risk-sensitive governance rules;
- or combinations of these mechanisms.

One practical instantiation is a hybrid Admission workflow. An AI system first proposes a candidate Claim, Attribute, or Relation together with Qualifiers and a Grounding Basis. Automated controls then verify schema completeness, identifier integrity, required evidence, and consistency with already accepted knowledge. A policy layer may admit low-risk candidates derived from designated authoritative sources, while routing ambiguous, cross-domain, or high-impact candidates to a domain expert. Successful Admission records the responsible authority, applicable policy, supporting evidence, timestamp, and version. Rejection or deferral preserves the candidate status rather than silently discarding or accepting the proposal.

This workflow is illustrative rather than mandatory. Its purpose is to show that Admission can combine AI proposal, deterministic validation, policy-based routing, and accountable human judgment without assigning acceptance to any one mechanism universally.

The architecture requires only that acceptance be explicit.

This is essential because generation and commitment carry different organizational consequences.

A language model can produce a well-formed semantic assertion that remains uncertain.

A rule engine can produce a deterministic output based on an invalid input.

A human expert can make an incorrect judgment.

Acceptance therefore does not guarantee truth.

It identifies what the organization has decided to rely upon under its applicable governance process.

## 4.3 Claim: Persistent Semantic Identity

A **Claim** is the persistent identity of a semantic assertion supplied to or established by the enterprise knowledge process.

For example:

**Claim C-001**

> The production transaction service shall sustain 10,000 transactions per second.

The Claim allows downstream processes to refer to a stable semantic object rather than repeatedly locate or reinterpret a passage of text.

This distinction is important because textual representation and semantic identity are not equivalent.

Two differently worded requirements may express the same underlying commitment.

A single paragraph may contain several distinct commitments.

A later version of a document may restate an existing commitment without creating a new knowledge identity.

Persistent Claim identity therefore separates the semantics being managed from the exact linguistic form in which those semantics originally appeared.

A Claim identifies a semantic unit.

It is not, by itself, the full organizational knowledge network.

## 4.4 Attributes: Externalized Semantic Meaning

Attributes externalize semantic distinctions that have already been resolved and accepted about a Claim. They are the first extension beyond a RAG semantic unit: instead of leaving the unit's operational meaning to be reconstructed from its text or embedding, AIKA records the parts that the organization has determined it can rely on.

For C-001, the following semantics might be represented:

- type = requirement
- subject = transaction service
- environment = production
- metric = transactions per second
- target = 10,000
- load mode = sustained
- priority = high
- business goal = enterprise service-level commitment

Before externalization, these distinctions remain dependent on natural-language interpretation in the current retrieval and inference context.

After externalization, routine downstream use can consult the accepted Attribute value directly. This does not prohibit later revision; it prevents ordinary reuse from silently becoming a new interpretation event.

The architecture does not require a universal attribute schema.

Which semantics are worth externalizing depends on organizational use.

Consider a supplier clause:

> Replacement units for the enterprise controller are dispatched within five business days for customers on the Premium plan.

A procurement process may require:

- supplier;
- contractual obligation;
- committed lead time;
- contract term;
- renewal date;
- breach exposure.

A customer-service process may require:

- entitlement tier;
- covered product;
- promised service window;
- escalation trigger;
- exception conditions.

The source sentence is identical.

The semantic distinctions required for action differ.

AIKA therefore treats Attribute requirements as use-dependent.

Where multiple applications operate over the same Claim, the Claim may accumulate accepted semantic Attributes established for different purposes. Each application can consume the subset relevant to its decision.

This allows accepted semantic meaning to compound across organizational uses without requiring every application to rebuild interpretation independently.

## 4.5 Relations: From Semantic Units to Knowledge Structure

A **Relation** externalizes an accepted relational interpretation between Claims as persistent enterprise state. It is the second extension beyond a RAG semantic unit: a relationship that has already been established no longer needs to be inferred again merely because a later query retrieves the same units.

Suppose a second Claim states:

**Claim C-002**

> Under deployment configuration X, the connection pool supports 500 concurrent connections.

The existence of C-001 and C-002 does not establish that the connection-pool capacity constrains the throughput requirement.

That proposition is a new semantic commitment:

**Relation R-001**

C-001 **constrainedBy** C-002

This distinction is central to AIKA.

Accepting Claim A and Claim B does not entail accepting Relation R between them.

A Relation must therefore possess its own identity, applicability conditions, and grounding. Its persistence records an organizational commitment to the relationship, not merely the fact that a model once predicted an edge.

This is also the point at which the architecture distinguishes a collection of semantic units from a semantic network.

A set of isolated Claims may be useful for retrieval and query-time reasoning.

A network of accepted Relations among Claims records what the organization has established about how those semantic units interact. The network is a state that later processes can read, inspect, challenge, or revise without first regenerating every accepted connection.

## 4.6 Qualifiers: Boundary of Organizational Meaning

A Relation without explicit applicability conditions may invite silent generalization.

Suppose R-001 was established using evidence from:

- the production environment;
- sustained traffic;
- deployment version 2026.09;
- autoscaling disabled.

If those conditions remain implicit, a later system may reuse the Relation under a different environment or operating configuration.

The Relation may then appear stable while its meaning expands.

A **Qualifier** externalizes the boundary within which a Relation is accepted.

Candidate dimensions include:

- environment;
- scope;
- time;
- condition;
- jurisdiction;
- authority;
- version;
- modality;
- evidence class.

For R-001:

**environment = production**  
**load mode = sustained**  
**version = 2026.09**

The purpose is not to define every possible semantic boundary in advance.

No finite qualifier vocabulary can guarantee complete representation of all future distinctions.

The architectural requirement is narrower:

> where an applicability boundary is organizationally consequential, it should become explicit rather than remain dependent on repeated inference.

## 4.7 Grounding Basis: Inspectable Justification

A **Grounding Basis** records why a Relation was proposed and accepted.

Grounding may reference:

- Claim Attributes;
- other Claims;
- other Relations;
- measurements;
- test evidence;
- authoritative policies;
- external sources;
- deterministic calculations;
- provenance records;
- human judgments.

For R-001, the grounding might include:

- C-001.target;
- C-001.load_mode;
- C-002.max_connections;
- load-test evidence E-003;
- deployment configuration X.

Grounding performs a different function from provenance alone.

Provenance can establish where information came from.

Grounding establishes which information formed the basis for the accepted relational commitment.

The distinction becomes important when a Relation is later challenged.

The relevant question is not merely:

> Where did these Claims originate?

but:

> Why did the organization accept this relationship between them?

The architecture therefore requires accepted Relations to remain inspectable with respect to their basis.

## 4.8 Viewpoints: Persistent Organizational Interpretation

Claims, Attributes, Relations, Qualifiers, and Grounding describe shared accepted knowledge.

Organizations, however, rarely use that knowledge through a single perspective.

Architecture, business analysis, product management, operations, compliance, security, finance, and other functions ask different questions of the same shared knowledge state.

AIKA represents recurring interpretive organization through a **Viewpoint**.

A Viewpoint is not merely a user role, tag, saved query, or arbitrary subset of Claims.

Four properties distinguish it.

### Interpretive coherence

A Viewpoint concerns a recognizable interpretive dimension.

An architecture Viewpoint may emphasize dependency, interfaces, capacity, constraints, and bottlenecks.

### Structural organization

A Viewpoint organizes knowledge relationally rather than simply selecting records.

Elements may occupy structural roles such as driver, dependency, bottleneck, risk, obligation, or boundary.

### Selective relevance

A Viewpoint identifies which Claims, Attributes, Relations, Qualifiers, and patterns matter for the interpretive purpose.

### Reusability

A Viewpoint represents a recurring organizational perspective rather than a one-off query result.

This distinction enables the same accepted Relation to occupy different interpretive roles without being duplicated.

A connection-pool constraint can function as a *bottleneck* in an architecture Viewpoint and as a *scaling boundary* in an operations Viewpoint.

The shared Relation remains the same.

The organizational interpretation differs.

## 4.9 Derived Domains

A **Viewpoint Domain** is the knowledge organization derived by applying a persistent Viewpoint to the shared governed knowledge state.

AIKA separates:

- persistent Viewpoint definition;
- shared accepted knowledge;
- derived Domain content.

This avoids maintaining independent knowledge copies for each organizational function.

If the governed state changes, the relevant Domain can be re-derived.

If the Viewpoint definition changes, the Domain changes accordingly.

A change to accepted knowledge should also propagate explicitly. When **Reconstruction**, the explicit reopening of previously accepted knowledge, revises or supersedes a Claim, Attribute, or Relation, the system can use derivation dependencies to identify affected Viewpoint Domains. Those Domains should be marked stale or invalidated until they are re-derived from the newly accepted state. If the changed element previously occupied a material structural role, such as *bottleneck*, *obligation*, or *risk*, affected consumers can be notified that the prior Domain no longer represents the current governed state. Once Reconstruction and Admission complete, deterministic derivation produces the updated Domain and preserves the earlier version for provenance. This connects Viewpoint reuse to the controlled-change operations developed in the companion AI Knowledge Evolution paper (Tsai, 2026a).

The desirable property is reproducibility:

> if the governed knowledge state and Viewpoint definition are unchanged, the derived Domain should also remain unchanged.

That property requires reproducible derivation semantics.

If an unconstrained language model decides Domain membership from scratch every time, the architecture has merely relocated repeated interpretation rather than externalized it.

AI may assist in designing or revising a Viewpoint.

Routine Domain derivation should rely on explicit, stable selection and organizational semantics.

## 4.10 The Integrated AIKA Structure

The resulting architecture can be summarized as follows:

| Element         | What it persists                    | Knowledge-management role         |
| --------------- | ----------------------------------- | --------------------------------- |
| Claim           | Semantic assertion identity         | Persistent semantic unit          |
| Attribute       | Resolved meaning                    | Explicit organizational semantics |
| Relation        | Accepted connection among Claims    | Relational knowledge              |
| Qualifier       | Applicability conditions            | Boundary of meaning               |
| Grounding Basis | Basis of acceptance                 | Inspectable justification         |
| Viewpoint       | Recurring interpretive organization | Organizational perspective        |
| Domain          | View-specific derived structure     | Reusable contextual knowledge     |

The elements are not independent inventions.

Together they establish a governed semantic network in which accepted interpretations can survive the inference event that produced them.

---

# 5. Results and Discussion

## 5.1 Conceptual Demonstration: One Requirement, Four Organizational Perspectives

Consider again:

> The production transaction service shall sustain 10,000 transactions per second.

After semantic interpretation and admission, the requirement becomes Claim C-001 with explicit Attributes.

Four further Claims are accepted:

**C-002:** the connection-pool configuration supports 500 concurrent connections.

**C-003:** increasing connection-pool capacity increases infrastructure cost.

**C-004:** the service is positioned for enterprise high-volume workloads.

**C-005:** infrastructure spending for the service must remain within the approved annual operating budget.

Four Relations are accepted.

**R-001:** C-001 is constrained by C-002 under production sustained-load conditions.

**R-002:** increasing the capacity represented by C-002 increases the cost represented by C-003.

**R-003:** the performance commitment represented by C-001 supports the market positioning represented by C-004.

**R-004:** the infrastructure cost represented by C-003 is constrained by the budget represented by C-005 during the current fiscal period.

The first Relation is grounded in the target throughput, load mode, configured capacity, and load-test evidence.

The second is grounded in infrastructure pricing and configuration data.

The third is grounded in the approved product positioning and service-level commitment.

The fourth is grounded in the approved operating budget and fiscal-period controls.

These elements form a shared governed knowledge state.

They do not initially belong to architecture, business, product, or operations.

The organizational perspectives are applied afterward.

### Architecture Viewpoint

The architecture Viewpoint emphasizes:

- dependency;
- capacity;
- technical constraints;
- structural bottlenecks.

C-001 and C-002 are central.

R-001 is interpreted structurally as a bottleneck relationship.

### Business Viewpoint

The business Viewpoint emphasizes:

- objectives;
- economic impact;
- cost;
- prioritization.

C-001, C-002, C-003, and C-005 become relevant.

R-002 and R-004 become central because satisfying the technical commitment may create economic consequences that must remain within the approved budget.

### Product Viewpoint

The product Viewpoint emphasizes:

- customer expectations;
- market positioning;
- service commitments;
- customer value.

C-001 and C-004 become prominent.

R-003 makes their accepted connection explicit: the technical performance commitment supports the enterprise high-volume market position. The Product Viewpoint therefore does not merely place two disconnected Claims together; it organizes an accepted Relation as part of a product promise rather than primarily as an engineering constraint.

### Operations Viewpoint

The operations Viewpoint emphasizes:

- capacity;
- sustained load;
- scaling;
- thresholds;
- operating conditions.

C-001 and C-002 again become central.

However, R-001 is interpreted as a scaling boundary rather than an architecture bottleneck.

The underlying accepted Claims and Relation have not changed.

The interpretive organization has.

## 5.2 What Becomes Visible Across Viewpoints

Because all four Viewpoints derive from shared knowledge identities, they can be compared without first reconciling separately constructed knowledge stores.

The architecture and operations Viewpoints share C-001, C-002, and R-001.

Their difference lies primarily in structural interpretation.

Architecture sees a bottleneck.

Operations sees a scaling boundary.

This difference can itself become organizationally informative.

A stronger interaction appears between operations and business.

Operations concludes that satisfying the performance target may require capacity expansion.

Business holds that capacity expansion increases infrastructure cost and that the resulting cost remains subject to C-005, the approved annual operating budget.

Because C-005 and R-004 are represented in the shared state, the network exposes a cross-functional chain:

**Performance Target**

→ constrained by

**Connection-Pool Capacity**

→ capacity expansion increases

**Infrastructure Cost**

→ constrained by

**Budget Constraint**

This chain corresponds to C-001, C-002 through R-001, C-003 through R-002, and C-005 through R-004. Every endpoint and relationship is therefore represented in the shared governed knowledge state rather than introduced only in the Viewpoint narrative.

No single source statement necessarily contains that chain.

The knowledge exists through the network of accepted semantic commitments.

This demonstrates why AIKA does not treat a single semantic unit as equivalent to the full organizational knowledge structure.

## 5.3 Why RAG Alone Does Not Complete the Knowledge Lifecycle

The demonstration also clarifies the relationship between AIKA and RAG.

RAG remains essential.

Without retrieval, the model may not have access to C-001, C-002, C-003, or the evidence grounding their relationships.

But retrieval and knowledge persistence answer different questions.

At the semantic layer, RAG asks:

> Which semantic material is relevant now?

AIKA asks:

> Which meanings within that semantic material have already been accepted as Attributes, and which relationships among semantic units have already been accepted as Relations?

The two therefore compose naturally.

**Retrieval supplies semantic units.**

**AI reasoning proposes Attributes and Relations.**

**Admission determines commitment.**

**The knowledge architecture retains accepted Attribute and Relation state.**

This division avoids requiring every enterprise question to begin from epistemic zero.

An AI system can still retrieve source material when additional context, validation, or revision is required.

But routine downstream work can read accepted Attributes and Relations without repeatedly reconstructing semantic commitments already established.

## 5.4 Semantic Unit Versus Organizational Knowledge

One of the most important distinctions emerging from the architecture is:

**Semantic Unit ≠ Persistent Enterprise Knowledge State**

A Claim may be accurate, persistent, identifiable, and useful.

Yet many organizational decisions depend on relationships among Claims.

Consider:

**Claim A:** Production throughput must reach 10,000 TPS.

**Claim B:** The connection pool has capacity X.

Without a persistent Relation, the system holds two semantic units and may infer a connection between them at query time.

With an accepted Relation:

**A constrainedBy B**

the system retains something additional: an accepted relationship that can be reused without repeating the inference.

With Qualifiers:

**only under production sustained load**

it knows where that relationship applies.

With Grounding:

**supported by test E-003**

it knows why the relationship was accepted.

With a Viewpoint:

**architecture: bottleneck**  
**operations: scaling boundary**

the system knows how recurring organizational perspectives structure the same accepted relation.

The resulting knowledge is therefore not simply the sum of semantic statements.

Its organizational meaning emerges partly through governed relational structure.

A concise representation is:

**Semantic Units → Accepted Attributes → Accepted Relations → Qualified Persistent State → Organizational Knowledge Structure**

This distinction also helps clarify why knowledge graphs alone do not automatically solve the problem.

A graph can contain predicted, extracted, imported, disputed, outdated, or speculative edges.

AIKA is concerned not merely with graph connectivity but with **governed relational commitment**.

The question is not:

> Is there an edge?

It is:

> Has the organization accepted this relationship, under what conditions, and on what basis?

## 5.5 From AI Answers to Organizational Knowledge Assets

The architecture also reframes what it means for an organization to “own” the knowledge generated through AI-assisted work.

Suppose an employee asks an AI assistant whether a technical capacity limitation threatens a contractual commitment.

The assistant retrieves several sources, performs a technically sound analysis, and produces a conclusion.

If the conclusion disappears into a conversation log, the organization has received value from the model but has not necessarily converted that value into a reusable organizational asset.

A later employee may pay for the same interpretive work again.

A later model may reinterpret the same evidence.

A vendor change may alter the reasoning behavior.

A dispute may arise with no inspectable representation of what the organization had previously accepted.

AIKA changes the persistence boundary.

Once an interpretation is accepted, it becomes independently identifiable.

Its semantics become explicit.

Its Relations become addressable.

Its applicability becomes bounded.

Its grounding becomes inspectable.

Its organizational uses can be represented through Viewpoints.

These mechanisms close the eight ownership conditions introduced in Section 1.4:

| Organizational ownership condition   | AIKA mechanism                                                                  |
| ------------------------------------ | ------------------------------------------------------------------------------- |
| Independent identification           | Stable Claim and Relation identities                                            |
| Inspectable semantic commitments     | Explicit accepted Attributes                                                    |
| Identifiable relationships           | Addressable accepted Relations                                                  |
| Explicit applicability               | Relation Qualifiers                                                             |
| Inspectable basis of acceptance      | Grounding Basis                                                                 |
| Reuse without routine reconstruction | Shared persistent Attribute and Relation state                                  |
| Explicit revision                    | Versioned replacement, supersession, or reopening of accepted elements          |
| Distinguishable epistemic status     | Admission status separating candidate, accepted, revised, and rejected elements |

AIKA therefore satisfies organizational ownership structurally rather than by retaining a conversation transcript. The architecture does not guarantee that every condition is implemented correctly, but it assigns each condition an explicit representational or governance responsibility.

The knowledge therefore becomes less dependent on:

- a particular model;
- a particular prompt;
- a particular conversation;
- a particular employee;
- or a particular moment of inference.

This is the operational sense in which the organization begins to hold the knowledge produced through AI-assisted work.

## 5.6 Implications for Enterprise Knowledge Management

The architecture suggests several broader implications for enterprise AI knowledge management.

### From question answering to cumulative knowledge work

RAG-based assistants are frequently evaluated by the quality of individual answers.

AIKA shifts attention toward cumulative organizational effects.

A useful answer may be temporary.

An accepted interpretation represented persistently can become input to later work.

The unit of value therefore changes from:

**answer quality**

toward:

**knowledge accumulation and reuse**.

### From model memory to organizational memory

Conversation history and model memory can improve continuity, but they remain different from governed organizational memory.

Organizational knowledge should survive changes in:

- session;
- user;
- workflow;
- model;
- vendor;
- deployment architecture.

Persistent knowledge structure creates this independence.

### From siloed knowledge systems to shared knowledge with multiple interpretations

Different departments often construct independent repositories or AI assistants around the same organizational material.

This can duplicate identity and create conflicting interpretations.

AIKA instead allows shared Claim and Relation identities to support multiple Viewpoints.

Functional differentiation therefore occurs in interpretive organization rather than through unnecessary duplication of underlying knowledge.

### From implicit reasoning to inspectable commitment

Generative AI can produce convincing conclusions whose inferential basis is difficult to reconstruct later.

AIKA does not require the internal reasoning process of a model to become deterministic or fully exposed.

It requires the **basis of accepted organizational commitment** to remain inspectable.

This is a more practical governance target.

The organization need not preserve every intermediate token of model reasoning.

It must preserve enough explicit structure to answer:

> What did we accept, under what conditions, and why?

## 5.7 Engineering Determinacy Reconsidered

Engineering Determinacy remains useful as a design principle but should not be interpreted as a claim that organizational knowledge can become permanently deterministic (Tsai, 2026b).

The principle is:

> once an interpretation has been explicitly established and accepted, routine reuse should not require that interpretation to be re-inferred.

This creates two zones.

The **probabilistic zone** is where unresolved semantics are interpreted, hypotheses are generated, candidate Relations are proposed, and conflicting meanings may coexist.

The **governed knowledge zone** is where accepted semantic commitments are represented explicitly enough for routine reuse.

The boundary between them is Admission.

The deterministic property therefore concerns reuse of accepted representation.

It does not concern permanent truth.

This distinction is particularly important because knowledge changes.

A Relation accepted today may require revision tomorrow.

Persistent knowledge must therefore support explicit change rather than prevent change.

## 5.8 Limitations

The conceptual architecture has several important limitations.

### Persistence does not establish truth

An incorrect interpretation can be accepted.

Persistence may then propagate the error more consistently than repeated inference would.

The architecture therefore transfers part of the risk from repeated interpretation to admission quality.

This is intentional but consequential.

### Admission governance patterns require domain-specific instantiation

AIKA intentionally does not prescribe a universal Admission mechanism. Admission is domain-specific because evidential thresholds, authority, validation, and risk controls differ across organizational settings.

The limitation is therefore not the absence of one universal algorithm. It is that the present conceptual study does not instantiate or evaluate reusable Admission governance patterns for different domains. Implementation research must show how particular combinations of human approval, authoritative-source policy, deterministic validation, evidence requirements, and risk-sensitive controls perform in practice.

### Explicit semantics cannot be complete

No finite schema can capture every semantic distinction relevant to all future organizational decisions.

AIKA therefore reduces unnecessary inference rather than eliminating interpretation.

### Viewpoint formalization remains incomplete

The paper proposes conditions distinguishing a persistent Viewpoint from a saved query or arbitrary relation set, but it does not provide a complete formal logic for Viewpoint discovery, validation, split, merge, or collapse.

### Cross-viewpoint comparison requires empirical validation

The illustrative case shows how shared identities can expose cross-functional relationships, but it does not establish that such comparison consistently improves enterprise decision making.

### The architecture is representation-agnostic

AIKA does not specify whether implementations should use RDF, RDF-star, labeled property graphs, relational databases, document stores, hybrid representations, or another storage technology.

The contribution concerns semantic responsibility rather than a particular storage platform.

### No empirical performance claim is made

The present study does not demonstrate reduced cost, higher retrieval accuracy, improved answer faithfulness, improved employee productivity, or improved decision outcomes.

Such claims require implementation and empirical study. A prototype evaluation should compare a conventional RAG workflow with an AIKA-enabled workflow over matched repeated-query and knowledge-change tasks. Relevant measures include:

- the number of accepted semantic distinctions and relationships that must be re-inferred;
- token consumption and latency across repeated uses;
- consistency of recovered Attributes and Relations across sessions, models, and prompt variants;
- frequency of stale or invalid accepted knowledge being reused;
- human and automated effort required for Admission;
- propagation time from Reconstruction to affected Viewpoint Domains;
- and the accuracy with which the system distinguishes candidate from accepted knowledge.

The expected benefit is not cost reduction under every workload. Persisting, validating, versioning, and revising governed knowledge introduces its own operational cost. Empirical evaluation must therefore identify the conditions under which reduced repeated inference and improved consistency outweigh the overhead of Admission and knowledge maintenance.

## 5.9 From Persistent Knowledge to Knowledge Evolution

A persistent knowledge structure creates a subsequent question already recognized in ontology-evolution research: represented knowledge must support controlled change, versioning, and the propagation of revisions rather than remain static (Zablith et al., 2015).

Knowledge cannot remain static.

Requirements change.

Policies expire.

Evidence accumulates.

New Claims appear.

Existing relationships may cease to hold.

Previously disconnected Claims may become plausibly related.

AIKA defines the persistent state on which such change can operate.

A companion paper, **AI Knowledge Evolution**, develops this question through four operations (Tsai, 2026a):

**Construction** establishes explicit Claims and resolved semantic Attributes.

**Integration** establishes Relations among existing Claims.

**Reconstruction** explicitly reopens previously accepted Relations when evidence or conditions change.

**Exploration** identifies candidate Relations among Claims not currently connected by an accepted relationship.

These operations do not form a mandatory sequence, and Admission remains orthogonal to them.

The distinction is important because persistence and evolution solve different problems.

AIKA asks:

> **What does accepted organizational knowledge look like when it persists?**

AI Knowledge Evolution asks:

> **How can that accepted knowledge change without allowing every new probabilistic inference to silently redefine what the organization previously accepted?**

Together, they establish a progression from information retrieval to persistent and evolvable enterprise knowledge.

---

# 6. Conclusion

Retrieval-augmented generation has transformed organizational access to internal information.

Documents, requirements, contracts, operational records, and other enterprise materials can now be retrieved and interpreted through natural-language interaction with unprecedented flexibility.

Yet improved access to semantic material does not by itself establish persistent organizational knowledge.

A central limitation appears when resolved meaning within semantic units and established relationships between semantic units remain transient.

A source statement may persist.

The model may retrieve it repeatedly.

The organization may repeatedly pay for its interpretation.

But unless accepted meaning becomes Attribute state and accepted relationships become Relation state, the system cannot reliably distinguish a previously established organizational position from a newly generated interpretation.

This paper therefore distinguishes five levels:

**information**

**semantic interpretation**

**accepted Attributes**

**accepted Relations**

**governed organizational knowledge**

AI Knowledge Architecture combines the latter levels as a persistent semantic network for enterprise knowledge management.

Claims provide stable identity to semantic assertions.

Attributes externalize resolved meaning.

Relations preserve accepted connections among Claims.

Qualifiers delimit applicability.

Grounding preserves the basis of acceptance.

Viewpoints represent recurring organizational interpretation.

Derived Domains organize shared knowledge for particular purposes without duplicating the underlying state.

The contribution is not that any of these representation mechanisms is individually new.

The contribution is their assignment to a common knowledge-management responsibility:

> **accepted meaning within semantic units should become persistent Attribute state, and accepted relationships among semantic units should become persistent Relation state, rather than disappear as transient inference.**

The resulting division of responsibility is straightforward.

**RAG retrieves or produces semantic units relevant to the present question.**

**AI reasoning proposes what those units mean and how they may be related.**

**Admission determines which proposed Attributes and Relations the organization is prepared to accept.**

**AI Knowledge Architecture preserves the accepted Attribute and Relation state.**

In this architecture, a semantic unit is not treated as the complete knowledge asset.

It becomes an identified Claim whose accepted meaning is represented through Attributes and whose accepted connections to other Claims are represented through Relations.

That network allows both semantic meaning and semantic relationships to persist across queries, sessions, roles, models, and vendors while remaining open to explicit revision when evidence changes.

Enterprise AI knowledge management can therefore move beyond repeatedly answering questions over stored information.

It can begin to accumulate, govern, and evolve the interpretations produced through organizational AI-assisted work.

---

# Appendix A. Structural Specification

## A.1 Shared Knowledge State

The shared knowledge state contains accepted Claims and accepted shared Relations.

Attributes are attached to Claims.

Qualifiers and Grounding Basis are attached to Relations where applicable.

Persistent Viewpoints operate over this shared state.

Viewpoint Domains are derived rather than maintained as independent copies.

## A.2 Claim

A Claim contains:

- persistent identifier;
- proposition;
- explicit semantic Attributes;
- provenance;
- epistemic status where required by the implementation.

Example:

**Claim C-001**

**Proposition:**  
The production transaction service shall sustain 10,000 transactions per second.

**Attributes:**

- type = requirement
- subject = transaction-service
- environment = production
- metric = TPS
- target = 10000
- load_mode = sustained
- priority = high
- business_goal = enterprise-SLA

The architecture distinguishes three Attribute selections:

1. Attributes available on the Claim;
2. Attributes used as grounding for a Relation;
3. Attributes treated as relevant by a Viewpoint.

These sets may overlap but are not equivalent.

## A.3 Relation

A Relation contains:

- persistent identifier;
- source Claim;
- target Claim;
- relation type;
- Qualifiers;
- Grounding Basis;
- epistemic status where required.

Example:

**Relation R-001**

**Source:** C-001  
**Target:** C-002  
**Type:** constrainedBy

**Qualifiers:**

- environment = production
- load_mode = sustained
- valid_from = 2026-09-01

**Grounding Basis:**

- C-001.target
- C-001.load_mode
- C-002.max_connections
- Evidence E-003

A shared Relation belongs to the governed shared knowledge state.

A Viewpoint may assign additional structural meaning to the Relation without changing the identity of the underlying Relation.

## A.4 Qualifier Dimensions

Candidate Qualifier dimensions include:

- scope;
- environment;
- time;
- condition;
- modality;
- authority;
- jurisdiction;
- evidence;
- version.

The list is not exhaustive.

Qualifier dimensions should be expanded where organizational decisions depend on semantic boundaries not already represented.

## A.5 Grounding Basis

Grounding may reference:

- Claim Attributes;
- Claims;
- accepted Relations;
- measurements;
- policies;
- specifications;
- external evidence;
- rules;
- provenance;
- human authority.

Grounding identifies why a semantic commitment was accepted.

It does not imply that the commitment is permanently correct.

## A.6 Viewpoint

A Viewpoint contains:

- an interpretive dimension;
- relevant Claim and Attribute criteria;
- relevant Relation types;
- applicable constraints;
- structural organization;
- structural roles;
- explicit selection or derivation criteria.

Illustrative structural roles might include:

**Requirement Constraint → driver**

**Architecture Dependency → dependency**

**Capacity Limitation → bottleneck**

The same shared Relation may occupy different structural roles under different Viewpoints.

## A.7 Viewpoint Domain

A Viewpoint Domain is obtained by applying a persistent Viewpoint to the shared governed knowledge state.

The Viewpoint definition persists.

The Domain content is derived.

The desirable reproducibility condition is:

> if the governed state and Viewpoint definition remain unchanged, the derived Domain also remains unchanged.

This condition requires reproducible derivation semantics.

## A.8 Cross-Viewpoint Comparison

Cross-Viewpoint comparison operates over shared knowledge identities.

Candidate comparison dimensions include:

- shared Claims;
- shared Relations;
- different selected Attributes;
- different Qualifiers;
- different Grounding dependencies;
- different structural roles;
- different relational paths;
- different constraints;
- missing Relations.

Because Viewpoints operate over a shared knowledge state, comparison does not require prior reconciliation of independently maintained semantic copies.

---

# Declarations

## Funding

The author received no specific funding for this work.

## Conflicts of Interest

The author declares no conflicts of interest.

## Data Availability

No empirical dataset was generated or analyzed for this conceptual architecture study.

## Declaration of Generative AI and AI-Assisted Technologies

Generative AI tools were used during preparation of the manuscript to support literature discovery, organization of arguments, language drafting, editing, and manuscript refinement. The research problem, conceptual distinctions, architecture design, interpretation of prior work, scholarly positioning, and final claims were directed, evaluated, revised, and approved by the author. The author reviewed generated material, verified cited sources and their characterization, and takes responsibility for the content of the manuscript.

---

# References

Alavi, M., & Leidner, D. E. (2001). Review: Knowledge management and knowledge management systems: Conceptual foundations and research issues. *MIS Quarterly, 25*(1), 107–136. https://doi.org/10.2307/3250961

Brinkley, J. F., Suciu, D., Detwiler, L. T., Gennari, J. H., & Rosse, C. (2006). A framework for using reference ontologies as a foundation for the Semantic Web. *AMIA Annual Symposium Proceedings, 2006*, 96–100.

Davenport, T. H., & Prusak, L. (1998). *Working knowledge: How organizations manage what they know*. Harvard Business School Press.

Edge, D., Trinh, H., Cheng, N., Bradley, J., Chao, A., Mody, A., Truitt, S., Metropolitansky, D., Ness, R. O., & Larson, J. (2024). *From local to global: A Graph RAG approach to query-focused summarization* [Preprint]. arXiv. https://doi.org/10.48550/arXiv.2404.16130

Gao, Y., Xiong, Y., Gao, X., Jia, K., Pan, J., Bi, Y., Dai, Y., Sun, J., Wang, M., & Wang, H. (2023). *Retrieval-augmented generation for large language models: A survey* [Preprint]. arXiv. https://doi.org/10.48550/arXiv.2312.10997

Groth, P., Gibson, A., & Velterop, J. (2010). The anatomy of a nanopublication. *Information Services & Use, 30*(1–2), 51–56. https://doi.org/10.3233/ISU-2010-0613

Hartig, O. (2017). Foundations of RDF\* and SPARQL\*: An alternative approach to statement-level metadata in RDF. *CEUR Workshop Proceedings, 1912*, 1–12.

Jaakkola, E. (2020). Designing conceptual articles: Four approaches. *AMS Review, 10*(1–2), 18–26. https://doi.org/10.1007/s13162-020-00161-0

Jabareen, Y. (2009). Building a conceptual framework: Philosophy, definitions, and procedure. *International Journal of Qualitative Methods, 8*(4), 49–62. https://doi.org/10.1177/160940690900800406

Kuhn, T., & Dumontier, M. (2014). Trusty URIs: Verifiable, immutable, and permanent digital artifacts for Linked Data. In *Proceedings of the 11th Extended Semantic Web Conference* (pp. 395–410). Springer. https://doi.org/10.1007/978-3-319-07443-6_27

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-t., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. *Advances in Neural Information Processing Systems, 33*, 9459–9474.

Nonaka, I. (1994). A dynamic theory of organizational knowledge creation. *Organization Science, 5*(1), 14–37. https://doi.org/10.1287/orsc.5.1.14

Noy, N. F., & Musen, M. A. (2004). Specifying ontology views by traversal. In *Proceedings of the 3rd International Semantic Web Conference* (pp. 713–725). Springer. https://doi.org/10.1007/978-3-540-30475-3_49

Packer, C., Wooders, S., Lin, K., Fang, V., Patil, S. G., Stoica, I., & Gonzalez, J. E. (2023). *MemGPT: Towards LLMs as operating systems* [Preprint]. arXiv. https://doi.org/10.48550/arXiv.2310.08560

Sikos, L. F., & Philp, D. (2020). Provenance-aware knowledge representation: A survey of data models and contextualized knowledge graphs. *Data Science and Engineering, 5*(3), 293–316. https://doi.org/10.1007/s41019-020-00118-0

Tsai, S. (2026a). *AI knowledge evolution: From persistent knowledge structure to controlled knowledge change* [Preprint]. Zenodo. https://doi.org/10.5281/zenodo.22892257

Tsai, S. (2026b). *Engineering determinacy: Structuring established knowledge so that it need not be reinterpreted* [Preprint]. Zenodo. https://doi.org/10.5281/zenodo.22718019

Vogt, L., Kuhn, T., & Hoehndorf, R. (2024). Semantic units: Organizing knowledge graphs into semantically meaningful units of representation. *Journal of Biomedical Semantics, 15*, Article 7. https://doi.org/10.1186/s13326-024-00310-5

Vrandečić, D., & Krötzsch, M. (2014). Wikidata: A free collaborative knowledgebase. *Communications of the ACM, 57*(10), 78–85. https://doi.org/10.1145/2629489

Walsh, J. P., & Ungson, G. R. (1991). Organizational memory. *Academy of Management Review, 16*(1), 57–91. https://doi.org/10.5465/amr.1991.4278992

Zablith, F., Antoniou, G., d'Aquin, M., Flouris, G., Kondylakis, H., Motta, E., Plexousakis, D., & Sabou, M. (2015). Ontology evolution: A process-centric survey. *The Knowledge Engineering Review, 30*(1), 45–75. https://doi.org/10.1017/S0269888913000349
