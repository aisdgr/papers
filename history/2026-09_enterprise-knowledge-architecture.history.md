# AI Knowledge Architecture — Version History

This document records the conceptual development of the paper
**“AI Knowledge Architecture for Enterprise Knowledge Management: From
Semantic Units to Persistent Attribute and Relation States.”**

The paper developed from an earlier investigation into Knowledge Evolution and
the limits of retrieval-centric enterprise AI. It subsequently narrowed its
focus to a specific architectural problem: how an organization can preserve
accepted semantic interpretations as reusable organizational knowledge.

The architecture retains the established name **AI Knowledge Architecture
(AIKA)**. *Enterprise* identifies the application and scholarly positioning of
the current paper; it does not introduce a separate EAIKA architecture.

The stages below describe the development of the paper's argument and
architecture. References to precursor work identify conceptual lineage; they
do not retroactively redefine separate papers as versions of this manuscript.

---

## v0.1 — Beyond Retrieval-Centric Enterprise AI

**Status:** Conceptual Precursor

### Purpose

- Identify the limitation of enterprise AI systems centered primarily on
  retrieval, summarization, and question answering.
- Distinguish stored information and knowledge materials from organizational
  knowledge that can be reused and developed over time.
- Explore how AI-assisted work might contribute to continuing organizational
  learning rather than isolated responses.

### Key Contributions

- Established the distinction between access to information and the evolution
  of organizational knowledge.
- Proposed that documents, decisions, actions, issues, and outcomes should be
  treated as inputs to knowledge formation rather than as complete knowledge
  by themselves.
- Identified validation, traceability, governance, and stewardship as necessary
  conditions for enterprise knowledge use.

### Limitations

- The knowledge representation layer remained abstract.
- No persistent unit of semantic identity was defined.
- The transition from AI-generated interpretation to accepted organizational
  knowledge was not architecturally specified.
- Knowledge Evolution combined representation, change, decision support, and
  governance within one broad framing.

### Historical Significance

This stage established the motivating problem: retrieval can repeatedly expose
source information without preserving what an organization has already
interpreted and accepted about that information.

---

## v0.2 — Persistence of Accepted Interpretation

**Status:** Problem Definition

### Purpose

- Narrow the earlier Knowledge Evolution thesis to the persistence problem.
- Explain why useful AI interpretations remain organizationally transient even
  when their source documents remain available.
- Define a boundary between probabilistic interpretation and accepted semantic
  commitment.

### Key Contributions

- Introduced the governing principle:

  > Once an interpretation has been explicitly established and accepted, it
  > should not need to be re-inferred during routine use.

- Distinguished three responsibilities:
  - retrieval locates source material;
  - AI reasoning proposes interpretations;
  - persistent architecture preserves accepted interpretations.
- Positioned repeated semantic inference as an architectural issue rather than
  only a model-consistency or prompt-quality issue.
- Applied Engineering Determinacy to organizational knowledge representation.

### Deliberate Non-Goals

- No attempt to make probabilistic model reasoning deterministic.
- No replacement of RAG, knowledge graphs, ontology views, provenance models,
  or enterprise source systems.
- No claim that persistence establishes truth.

### Historical Significance

This stage transformed a broad claim about Knowledge Evolution into a bounded
architectural question: what must persist when an organization decides to rely
on an interpretation produced during AI-assisted work?

---

## v0.3 — AI Knowledge Architecture Formation

**Status:** Architecture Definition

### Purpose

- Define the minimum persistent structures needed to externalize accepted
  semantic interpretation.
- Preserve both knowledge assertions and the relational conditions under which
  those assertions become meaningful to an organization.
- Support multiple organizational perspectives over a shared knowledge state.

### Key Contributions

#### 1. Claim Identity

Introduced the **Claim** as a persistent semantic unit with stable identity.
The architecture no longer depended on a document fragment being reinterpreted
whenever its meaning was needed.

#### 2. Externalized Semantics

Introduced **Attributes** to record semantic distinctions that had already been
resolved and accepted for subsequent use.

#### 3. Qualified Relational Structure

Introduced **Relations** and **Qualifiers** to represent accepted connections
among Claims together with the conditions under which those connections hold.

#### 4. Inspectable Basis

Introduced **Grounding Basis** so a Relation could preserve why it had been
accepted rather than storing connectivity without justification.

#### 5. Persistent Interpretive Organization

Introduced **Viewpoints** and derived **Domains** so architecture, business,
product, operations, and other roles could organize a shared knowledge state
without maintaining disconnected semantic copies.

### Integrated Structure

The architecture stabilized around:

`Claim → Attribute → Relation → Qualifier → Grounding → Viewpoint → Domain`

These elements are complementary responsibilities rather than a mandatory
processing sequence.

### Limitations

- Admission was identified but not yet fully positioned as an independent
  transition into organizational commitment.
- The relationship to established knowledge-management and organizational-
  memory literature required stronger development.
- The illustrative enterprise case required a more explicit analytical role.
- The distinction between an isolated semantic unit and organizational
  knowledge required further qualification.

---

## v0.4 — Governed Semantic Network and Enterprise Positioning

**Status:** Scholarly Consolidation

### Purpose

- Position AI Knowledge Architecture within enterprise knowledge management
  rather than only within AI systems architecture.
- Clarify the transition from candidate interpretation to governed
  organizational commitment.
- Demonstrate why organizational knowledge requires more than isolated
  semantic units.
- Strengthen the architecture's relationship to prior work and state its
  novelty conservatively.

### Key Contributions

#### 1. Admission Becomes Explicit

**Admission** is defined as the governance transition through which a candidate
interpretation becomes an accepted organizational commitment.

The architecture therefore distinguishes:

- source information;
- semantic interpretation;
- candidate knowledge;
- admitted organizational knowledge.

Admission does not guarantee objective truth. It records that the organization
has decided to rely on an interpretation under an applicable governance
process.

#### 2. Organizational Knowledge Becomes Relational

The paper no longer treats an isolated semantic unit as the complete knowledge
structure. Within AIKA, organizational knowledge is represented as a governed
semantic network of:

- accepted Claims;
- resolved Attributes;
- explicit Relations;
- applicability Qualifiers;
- inspectable Grounding;
- persistent Viewpoints;
- and derived Domains.

#### 3. Enterprise Knowledge Management Positioning

AIKA is positioned downstream of RAG:

`Enterprise Sources → Retrieval → AI Interpretation → Admission → AIKA`

RAG improves access to information. AIKA preserves accepted semantic
commitments so later work can reuse them without reconstructing their meaning
from source material alone.

#### 4. Organizational Ownership

The paper defines ownership in operational rather than proprietary terms. An
organization owns AI-assisted knowledge when accepted interpretations are
represented independently of a transient model response and can be inspected,
reused, governed, revised, and attributed.

#### 5. Shared State and Multiple Viewpoints

The enterprise example was expanded to show how architecture, business,
product, and operations Viewpoints can derive different organizations from one
shared knowledge state. Cross-viewpoint comparison can expose relationships
that remain invisible within any single role-specific reading.

#### 6. Conservative Novelty Boundary

The paper does not claim that graphs, semantic units, provenance, qualifiers,
or ontology views are individually novel. Its contribution is the assignment
of these mechanisms to a common organizational responsibility: preserving
accepted AI-assisted interpretations as governed and reusable knowledge.

---

## v0.5 — Attribute and Relation State Clarification

**Status:** Conceptual Refocusing

### Purpose

- Define more precisely where RAG ends and AIKA begins.
- Separate persistence of accepted meaning within a semantic unit from
  persistence of accepted relationships between semantic units.
- Make repeated relational inference an explicit architectural problem.
- Preserve the established AIKA name while strengthening its enterprise
  knowledge-management positioning.

### Key Contributions

#### 1. RAG Is Positioned as the Semantic Layer

The current paper treats a RAG-oriented system as supplying retrieved or
generated semantic units for query-time reasoning.

A semantic unit may function as the knowledge element presented to the model,
but meanings required for a particular use and relationships to other semantic
units may still be reconstructed during each inference cycle.

This is an analytical boundary rather than a claim that every RAG
implementation uses the same internal representation.

#### 2. Accepted Meaning Becomes Attribute State

Semantic distinctions within a Claim that have been explicitly established and
accepted are externalized as **Attributes**.

Examples include:

- `environment = production`;
- `target = 10,000`;
- `load mode = sustained`.

The Attribute layer preserves the accepted portion of semantic interpretation
so routine downstream use does not need to reconstruct it from source text,
embeddings, or the current prompt context.

#### 3. Accepted Relationships Become Relation State

The existence of two semantic units does not establish an accepted connection
between them.

When a relationship has been explicitly established and accepted, AIKA
externalizes it as a persistent **Relation** with its own identity,
applicability Qualifiers, and Grounding Basis.

The relationship becomes enterprise knowledge state rather than a conclusion
that must be inferred again whenever the same semantic units are retrieved.

#### 4. Two-Level Persistence

The central architectural distinction becomes:

`Semantic Unit → Accepted Attribute State → Accepted Relation State`

- **Attribute state** preserves accepted meaning within semantic units.
- **Relation state** preserves accepted meaning between semantic units.

Claims provide identity. Qualifiers bound applicability. Grounding preserves
the basis of acceptance. Viewpoints and derived Domains organize the shared
state for recurring enterprise purposes.

#### 5. Naming Continuity

The formal architecture name remains **AI Knowledge Architecture (AIKA)** to
preserve continuity with the SSRN publication and existing citations.

The paper title changes to:

> **AI Knowledge Architecture for Enterprise Knowledge Management: From
> Semantic Units to Persistent Attribute and Relation States**

The phrase *for Enterprise Knowledge Management* describes the present paper's
scope and application rather than renaming the architecture.

---

## v0.6 — Submission Structure and Argument Closure

**Status:** Submission Readiness Revision

### Purpose

- Separate the proposed conceptual framework from the paper's Results and
  Discussion section.
- Ensure that every Claim used in the enterprise demonstration participates in
  an explicit relational structure.
- Close the Organizational Ownership argument against the eight conditions
  introduced in the paper.
- Strengthen citation support for Engineering Determinacy and Knowledge
  Evolution.
- Reframe intentionally domain-specific design choices without presenting them
  as unresolved universal mechanisms.

### Structural Revisions

#### 1. Framework and Results Are Separated

The former dual-Results structure is removed.

Section 4 becomes:

> **AI Knowledge Architecture: Conceptual Framework**

Section 5 remains:

> **Results and Discussion**

The architecture definition is therefore presented as the proposed framework,
while the conceptual demonstration and its implications remain the analytical
results.

#### 2. Demonstration Becomes a Closed Relational Network

The enterprise case is expanded from four Claims and two Relations to five
Claims and four Relations.

The accepted Claims now include:

- C-001 — performance target;
- C-002 — connection-pool capacity;
- C-003 — infrastructure-cost consequence;
- C-004 — enterprise high-volume market position;
- C-005 — approved annual operating-budget constraint.

Two Relations are added:

- R-003 connects C-001 to C-004, making the Product Viewpoint's market-
  positioning interpretation explicit.
- R-004 connects C-003 to C-005, representing the budget constraint as part of
  the governed shared state.

The cross-Viewpoint chain now contains only defined Claims and Relations:

`Performance Target → Connection-Pool Capacity → Infrastructure Cost → Budget Constraint`

This removes unconnected and narratively introduced elements from the
demonstration.

#### 3. Organizational Ownership Is Evaluated Explicitly

Section 5.5 now maps the eight conditions introduced in Section 1.4 to AIKA
mechanisms:

| Ownership Condition | AIKA Responsibility |
|---|---|
| Independent identification | Claim and Relation identity |
| Inspectable semantics | Attributes |
| Identifiable relationships | Relations |
| Explicit applicability | Qualifiers |
| Inspectable basis | Grounding Basis |
| Reuse without reconstruction | Persistent shared state |
| Explicit revision | Replacement, supersession, or reopening |
| Distinguishable status | Admission state |

Organizational Ownership is therefore used as an evaluative closure rather
than appearing only as an introductory framing device.

#### 4. Admission Limitation Is Reclassified

The absence of a universal Admission algorithm is retained as a deliberate
architectural decision because authority, evidence, validation, and risk
thresholds differ by domain.

The actual limitation is narrowed to the lack of instantiated and empirically
evaluated Admission governance patterns for different organizational settings.

#### 5. Citation Support Is Strengthened

- Engineering Determinacy is linked to its Zenodo publication.
- AI Knowledge Evolution is identified as a companion paper and linked to its
  Zenodo publication.
- Zablith et al. (2015) is cited in the Knowledge Evolution discussion to
  establish the ontology-evolution context.
- The Miranda and Nalepa thesis-proposal citation is removed from its prior
  supporting role; established ontology-view literature remains the primary
  foundation for Viewpoints.

#### 6. Semantic Unit Is Defined Earlier

The Abstract now defines a semantic unit as a meaningful assertion available
for inference. This prevents the central term from remaining undefined until
the methodology section.

#### 7. Target-Journal Format Is Aligned

The manuscript is prepared against the Research Paper requirements of **The
IUP Journal of Knowledge Management**, whose subject scope covers knowledge
creation, capture, dissemination, and management processes.

The submission-facing changes include:

- reducing the Abstract to 113 words, below the 120-word limit;
- reducing the keyword list to five entries;
- retaining the required Introduction, Literature Review, Methodology, Results
  and Discussion, and Conclusion structure;
- adding author email and Independent Researcher affiliation below the title;
- retaining an alphabetical APA-style reference list;
- and identifying both Zenodo self-citations explicitly as `[Preprint]`.

The journal's published Author Guidelines and Publication Ethics pages do not
state a specific policy accepting or prohibiting preprint citations. Editorial
confirmation therefore remains necessary before final submission if those two
self-citations are retained.

---

## v0.7 — Peer-Review Response and Operational Deepening

**Status:** Major Revision Response

### Purpose

- Make the value difference between a RAG-oriented workflow and AIKA visible
  at the beginning of the paper.
- Demonstrate how Admission can operate without imposing one universal
  governance algorithm.
- Specify how changes to accepted knowledge propagate into Viewpoint Domains.
- Distinguish governed commitment persistence from agent memory and GraphRAG
  context management.
- Turn the empirical limitation into a concrete prototype evaluation agenda.

### Key Revisions

#### 1. RAG and AIKA Are Compared Directly

The Introduction now compares the two workflows across persistent objects,
meaning within semantic units, relationships between semantic units, repeated
queries, and governance status.

The comparison explicitly avoids a universal claim about RAG implementations.
RAG systems may persist entities, edges, summaries, or memory records; AIKA
adds the question of whether represented meaning has been admitted as an
organizational commitment.

#### 2. Admission Receives an Illustrative Hybrid Workflow

The conceptual framework now describes a practical sequence in which:

1. AI proposes a candidate Claim, Attribute, or Relation with Qualifiers and
   Grounding;
2. automated controls validate schema, identifiers, evidence, and consistency;
3. policy admits eligible low-risk candidates from authoritative sources;
4. ambiguous or high-impact candidates are routed to a domain expert; and
5. the resulting decision records authority, policy, evidence, time, and
   version.

This example demonstrates operational feasibility while preserving the
architecture's domain-specific Admission boundary.

#### 3. Viewpoint Domains Gain Change-Propagation Semantics

When Reconstruction reopens, revises, or supersedes accepted knowledge,
derivation dependencies identify affected Viewpoint Domains. Those Domains can
be marked stale or invalidated, relevant consumers can be notified, and the
Domains can be re-derived after the revised state passes Admission.

Earlier Domain versions remain available for provenance.

#### 4. Agent Memory and GraphRAG Are Distinguished

MemGPT and GraphRAG are incorporated into the literature discussion as systems
that improve context continuity, retrieval, and synthesis.

AIKA is positioned as complementary: its concern is **governed commitment
continuity**, not merely the retention or selection of information for model
inference.

#### 5. Prototype Evaluation Is Specified

Future empirical work should compare matched RAG and AIKA-enabled workflows on:

- repeated-inference frequency;
- token consumption and latency;
- cross-session and cross-model consistency;
- stale-knowledge reuse;
- Admission effort;
- Reconstruction-to-Domain propagation time;
- and candidate-versus-accepted status accuracy.

The paper also recognizes that persistence and governance create maintenance
cost. The empirical question is therefore when reduced repeated inference and
greater consistency outweigh Admission and lifecycle overhead.

---

## Current Status — Persistent Attribute and Relation States

**Status:** Current Manuscript

The current paper presents AI Knowledge Architecture as a representation-
agnostic conceptual architecture for converting accepted semantic meaning and
accepted semantic relationships into persistent enterprise knowledge state.

Its central thesis is:

> RAG can supply semantic units for query-time reasoning. Durable enterprise
> knowledge requires accepted meaning within those units to be externalized as
> Attributes and accepted relationships among those units to be externalized
> as Relations.

The current manuscript emphasizes seven principles:

1. **RAG supplies the semantic layer.**
   Retrieved or generated semantic units provide meaningful material for
   present inference but do not necessarily preserve accepted interpretation.

2. **Interpretation and acceptance are distinct.**
   A plausible AI interpretation remains a candidate until an admission
   process accepts it for organizational use.

3. **Accepted intra-unit meaning becomes Attribute state.**
   Semantic distinctions that the organization has determined it can rely on
   are persisted as Attributes rather than repeatedly reconstructed.

4. **Accepted inter-unit meaning becomes Relation state.**
   Established relationships among semantic units are persisted as Relations
   rather than repeatedly inferred from retrieved material.

5. **Persistent Relations remain qualified and grounded.**
   Persistence records an accepted relationship together with where it applies
   and why it was accepted; it does not merely store a predicted edge.

6. **Multiple Viewpoints should share one knowledge state.**
   Role-specific organization should not require fragmented and independently
   maintained copies of the same semantic commitments.

7. **Persistence does not imply immutability or truth.**
   Accepted knowledge may be revised, superseded, or rejected through explicit
   governance processes.

The manuscript now includes a closed five-Claim, four-Relation conceptual
demonstration; an explicit evaluation of Organizational Ownership; literature
positioning; scoped limitations; declarations; and a structural appendix
specifying the principal AIKA elements and their relationships.

---

## Superseded or Narrowed Formulations

| Earlier Formulation | Current Position |
|---|---|
| Enterprise AI should evolve beyond retrieval | AIKA addresses the narrower persistence layer downstream of retrieval |
| Documents and records are merely knowledge materials | Source material may contain knowledge, but AIKA distinguishes source information from the semantic commitments it governs |
| A semantic unit can stand for organizational knowledge | A semantic unit becomes an identified Claim; accepted meaning is persisted as Attributes and accepted connections as Relations |
| Persistent interpretation is one undifferentiated state | AIKA separates accepted meaning within semantic units from accepted relationships between semantic units |
| A retrievable relationship is sufficient | An accepted Relation must persist as governed state with applicability and grounding |
| Determinacy means fixed knowledge | Determinacy means accepted meaning is explicit and reusable; governed revision remains possible |
| Viewpoints are separate role models | Viewpoints organize one shared knowledge state and derive role-relevant Domains |
| The architecture defines a storage model | AIKA defines semantic responsibilities and remains representation-agnostic |
| Enterprise AI Knowledge Architecture is a renamed architecture | The architecture remains AI Knowledge Architecture; enterprise knowledge management is the current application scope |

---

## Continuing Research Directions

Future work may examine:

- operational admission criteria and approval workflows;
- empirical evaluation of repeated-inference reduction;
- implementation using RDF-star, property graphs, relational models, document
  stores, or hybrid representations;
- formalization and validation of Viewpoint derivation;
- cross-viewpoint conflict and dependency detection;
- provenance, authority, confidence, and temporal semantics;
- organizational ownership and stewardship practices;
- integration with RAG, agent workflows, enterprise search, and knowledge
  management systems;
- and controlled knowledge change through Knowledge Construction, Integration,
  Reconstruction, and Exploration.

No earlier conceptual stage is treated as erased. Each stage records the
progression from a broad Knowledge Evolution thesis to a bounded architecture
for preserving accepted semantic meaning as Attribute state and accepted
semantic relationships as Relation state within governed organizational
knowledge.
