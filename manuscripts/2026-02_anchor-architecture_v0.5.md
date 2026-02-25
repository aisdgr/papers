# Anchor Architecture
## Spatiotemporal Anchors for Structural Traceability

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Date:** February 2026  
**Version:** v0.41

---

## Abstract

As software development increasingly incorporates AI assistance and autonomous
agents, relationships between specifications, code, executions, and governance
artifacts often degrade into post-hoc interpretation and speculation.

This paper presents **Anchor Architecture**, a model-agnostic and pre-analytical
framework for structural traceability. The framework does not depend on AI
models, prompts, or inference transparency. Instead, it defines traceability
as a property that emerges from **spatiotemporal anchoring**: progressively
binding identifiers to persistent carriers and indexing them along time or
version axes.

Anchor Architecture formalizes Trace IDs, spatial anchors, and spatiotemporal
anchors; distinguishes software, execution, and governance carriers; and
introduces trace chains, trace nets, and trace timelines as first-class
structural relations. The result is a unified foundation for impact analysis,
auditability, and governance across heterogeneous development contexts.

---

## Keywords

Anchor Architecture, Traceability, Spatiotemporal Anchors,  
Software Artifacts, Execution Evidence, Impact Analysis

---

## Introduction

Modern software systems are no longer produced solely through direct human
authorship. AI-assisted tools and agentic systems increasingly generate,
modify, and deploy artifacts across the development lifecycle.

This paper intentionally **does not depend on any AI model**. The structural
problems addressed here exist regardless of whether changes are produced by
humans, AI assistants, or fully autonomous agents.

The core claim is:

> Traceability failures are not caused by opaque reasoning,  
> but by missing structural anchors.

When identifiers, artifacts, executions, and governance constraints are not
anchored in space and time, analysis becomes speculative. Anchor Architecture
defines the minimal structural conditions required for relationships to be
**examinable rather than inferred**.

---

## Identifiers and Anchoring Primitives

### Identifier (ID)

An **Identifier (ID)** is a symbolic label assigned to a specific **Item** (artifact, entity, or event) within the system. Formally, we define the identifier through an assignment function $f_{id}$:

$$
ID = f_{id}(\text{Item})
$$

For example, a requirement item in a specification might be assigned:
$$
ID = \texttt{FR-091}
$$

**Properties of the Identifier**

It is critical to distinguish the **Identity** of an anchor from its **State** or **Context**. An ID in isolation satisfies the following structural properties:
* **Entity Naming**: It provides a unique handle to reference a specific Item.
* **Locational Neutrality**: The ID does not imply the physical or logical location of the carrier.
* **Temporal Neutrality**: The ID does not, by itself, imply a specific point in time or version.
* **Traceability Constraint**: While necessary, an ID alone is **insufficient** for traceability. Full structural examinability is only achieved when the ID is bound to a time index $\tau$ and a persistent carrier $C$.

---

### Spatial Anchor

A **Spatial Anchor** ($A_s$) is a structural commitment formed by binding a unique **Identifier (ID)** to a persistent **Carrier (C)**. This binding defines the "where" of an entity, establishing its location within the system's artifact space.

**Definition**
Formally, a spatial anchor is represented as a tuple:

$$
A_s := \langle ID, \; C \rangle
$$

For instance, when a functional requirement identifier is bound to a specific Software Requirements Specification (SRS) document:

$$
A_s = \langle \texttt{FR-091}, \; \texttt{SRS-FR-001} \rangle
$$

**Structural Significance**
The creation of a spatial anchor serves as a prerequisite for spatial decidability:
* **Locational Fixity**: It transforms an abstract ID into a locatable entity within a persistent carrier.
* **Contextual Boundary**: It defines the scope within which the entity's properties are contained.
* **Static Traceability**: A spatial anchor allows for the examination of *what* is where, but remains incomplete without a temporal index $\tau$ to determine *which version* or *which instance* of that entity is being referenced.

---

### Time Anchor

To ensure the **uniqueness** and **decidability** of the Anchor Architecture, we formalize the relationship between anchors, carriers, and their temporal or versioned indices.

**The Time Index $\tau$**

The time index $\tau$ is an element of the reference set $\mathcal{R}$, where its domain is conditioned by the type of the carrier $C$. We define the indexing logic as follows:

$$
\tau =
\begin{cases}
t \in \mathbb{T} & \text{timestamp} \\
v \in \mathbb{V} & \text{version}
\end{cases}
$$

**Anchor Instantiation**

An anchor instance $a_{\tau}$ is a structural commitment that maps a unique identifier to a specific state or point in time within its carrier's domain. Formally, an anchor instance is represented as a tuple:

$$
a_{\tau} := \langle \text{ID}, \text{Val} \rangle
$$

Where:
* **ID**: A unique, non-reconstructible identifier (e.g., a cryptographic hash or a GUID).
* **Val**: The concrete value (state) retrieved from the carrier at index $\tau$.

**Concrete Examples**
The architecture supports varying granularities of indexing depending on the carrier axis:

* **Version-based Anchor:**
    $$a_{\tau} \mid_{\tau \in \mathbb{V}} \implies \text{Val} = \texttt{"1.1.0"}$$
    
* **Time-based Anchor:**
    $$a_{\tau} \mid_{\tau \in \mathbb{T}} \implies \text{Val} = \texttt{"2026-02-11T09:58:47.540Z"}$$

---

### Spatiotemporal Anchor

A **Spatiotemporal Anchor** ($A_{st}$) is the primary structural primitive that extends a spatial anchor by incorporating a specific time index $\tau$. This synthesis establishes a multidimensional reference point, defining not only the location of an entity but its specific state at a discrete point in time or version.

**Formal Definition**
A spatiotemporal anchor is formalized as a triple:

$$
A_{st} := \langle ID, \; C, \; \tau \rangle
$$

Where the time index $\tau$ is strictly **carrier-dependent**, ensuring that the temporal reference aligns with the structural nature of the carrier $C$.

**Concrete Example**
For a requirement entity bound to a specific version of a specification document:

$$
A_{st} = \langle \texttt{FR-091}, \; \texttt{SRS-FR-001}, \; \texttt{v1.1.0} \rangle
$$

**Structural Implication**
The spatiotemporal anchor transforms an abstract identifier into a **decidable entity state**. By binding $ID$ to both $C$ and $\tau$, the architecture prevents "drift" in AI-assisted analysis: any examination of the entity $\texttt{FR-091}$ is now structurally constrained to its manifestation in $\texttt{SRS-FR-001}$ at version $\texttt{v1.1.0}$, eliminating ambiguity across different iterations or execution instances.

---

### Progressive Expansion Principle

The construction of an anchor follows a **Progressive Expansion Principle**, where each stage of binding introduces a new dimension of structural certainty. The progression is defined as follows:

$$
ID 
\quad \xrightarrow{\text{Location}} \quad 
\langle ID, \; C \rangle 
\quad \xrightarrow{\text{State}} \quad 
\langle ID, \; C, \; \tau \rangle
$$

Each step in this progression strictly increases the **structural information** available for analysis, transforming an abstract reference into a decidable entity:

* **Identity ($ID$):** Establishing **Existence**. At this stage, the entity is a "floating" reference. It names a concept (e.g., a specific requirement or a function) but lacks a tether to any physical or logical container.
* **Spatial Binding ($\langle ID, \; C \rangle$):** Establishing **Location**. This step fixes the entity within a persistent **Carrier** ($C$). It transforms a symbolic name into a locatable artifact, answering the question of *where* the entity resides.
* **Temporal Binding ($\langle ID, \; C, \; \tau \rangle$):** Establishing **State**. By incorporating the index $\tau$, the anchor captures a specific manifestation or version of the entity. This completes the structural requirement for tracking evolution and execution.

**Structural Implication**
This principle dictates that traceability is not a binary property but a layered structural state. Any analysis performed on a lower-level construct (e.g., using only an $ID$) is inherently **interpretive** and prone to speculation. Conversely, analysis performed on the full spatiotemporal triple is **structurally decidable**, providing the necessary ground truth for agentic governance.

---

### Spatial Uniqueness

To ensure that every identity-carrier binding is structurally distinct within the system, we define the uniqueness of spatial anchors through the following formal logic:

**1. Definition of Spatial Anchor Instances**
Let $A_c$ and $A_c'$ be two spatial anchor instances defined as tuples of an identifier and a carrier:
* $A_c = \langle ID, \; C \rangle$
* $A_c' = \langle ID', \; C' \rangle$

**2. Condition of Divergence**
The uniqueness of an anchor is predicated on the distinctness of its components. We consider a state of divergence where:
* $(ID \neq ID') \lor (C \neq C')$

**3. Spatial Inequality Conclusion**
Based on the principle of locational fixity, the following implication holds true:
* $A_c \neq A_c'$.

This formalization prevents semantic collision by ensuring that no two different entities share the same spatial coordinate, and conversely, no single entity can exist in multiple locations without generating distinct structural references.

### Spatiotemporal Uniqueness

To ensure that every state of an entity is uniquely resolvable across time or versions, we extend the uniqueness constraint to the spatiotemporal dimension.

**1. Definition of Spatiotemporal Anchor Instances**
Let $A_{st}$ and $A_{st}'$ be two spatiotemporal anchor instances associated with the same spatial coordinate, but indexed at different temporal points:
* $A_{st} = \langle ID, \; C, \; \tau \rangle$
* $A_{st}' = \langle ID', \; C', \; \tau' \rangle$

**2. Condition of Temporal Divergence**
Uniqueness is maintained even when the identifier and carrier remain constant, provided there is a divergence in the temporal or versioned index $\tau$:
* $(ID \neq ID') \lor (C \neq C') \lor (\tau \neq \tau')$

**3. Spatiotemporal Inequality Conclusion**
Based on the principle of progressive expansion, the following implication holds true for any resolved state:
* $A_{st} \neq A_{st}'$

This property guarantees that any reference to an entity's history is non-ambiguous. By enforcing spatiotemporal uniqueness, the framework ensures that a specific version of a policy or a specific timestamp of an execution evidence can be isolated and verified without risk of state-overlap or semantic drift.

---

## Core Principles

The effectiveness of the Anchor Architecture is predicated on four foundational principles that distinguish structural examination from traditional interpretive analysis.

### Pre-Analytical Existence
Anchors must exist **prior to** the analysis process, not as a dynamic result of it.

* **The Problem of Post-hoc Analysis**: Attempting to reconstruct relationships from outputs, logs, or narratives after an event has occurred yields **speculation**, not structural truth.
* **The Principle**: For an entity to be decidable, its anchor must be committed at the moment of creation or transition. This ensures the examiner is observing a recorded fact rather than an inferred history.

### Spatiotemporal Coordinates as Content Index
An anchor functions strictly as a **coordinate**, not a container for semantic content.

Given a spatiotemporal anchor $A = \langle ID, \; C, \; \tau \rangle$, the content is accessed through a resolution function:
$$\text{resolve}(A) \to \text{Content}$$

* **Lightweight Storage**: Anchors remain structurally minimal (approx. 50 bytes), regardless of the size of the referenced data.
* **Deterministic Resolution**: The same coordinate will always resolve to the exact same content, enabling **Time Travel** (the ability to query and verify any historical state without ambiguity).

### Implicit Traceability
Traceability relationships can be **inferred from spatiotemporal structure** without the need for explicit, manual annotation.

Given two anchors $A_1 = \langle ID_1, \; C_1, \; \tau_1 \rangle$ and $A_2 = \langle ID_2, \; C_2, \; \tau_2 \rangle$:
* **If**:
    1. They share the same **Trace ID** (Work Unit).
    2. $\tau_1 < \tau_2$ (Temporal ordering).
    3. $\text{Category}(C_1) = \text{Software}$ and $\text{Category}(C_2) = \text{Execution}$.
* **Then**: The framework infers that $A_2$ is a manifestation or evidence of $A_1$.

This eliminates the "annotation tax"—the need to explicitly tag every code artifact with "implements REQ-X"—by leveraging the inherent geometry of the engineering process.

### Non-Reconstructibility
The temporal dimension of an anchor is an irreversible record.

* **Principle**: If the temporal index $\tau$ is not captured at the moment of the entity's commitment to the carrier, it cannot be reconstructed later with absolute certainty. 
* **Implication**: This principle enforces a **"capture-at-source"** requirement, which is essential for maintaining a closed-loop digital twin and preventing the corruption of historical truth.

---

## Carrier Model

A **Carrier** ($C$) is a persistent and referenceable substrate that acts as the physical or logical container for an entity's state. It provides the **locational fixity** required for an anchor to resolve from a symbolic ID to a concrete manifestation.

### Carrier Substrate

Carriers must be persistent and addressable. Ephemeral artifacts are excluded.

Carriers may be stored in:
- Filesystems
- Version control systems
- Databases
- Registries

Beyond these types, the carrier accommodates **any identifiable data substrate** that satisfies the core requirements of **persistence** and **referencability**, ensuring that anchors remain resolvable throughout the engineering lifecycle.

---

### Carrier Categories

A **Carrier Instance** is classified into one of the following three categories based on the nature of its **Content**. This categorization provides a systematic way to handle different types of information within any engineering lifecycle, independent of specific frameworks or implementations:

**Software** (examples, non-exhaustive)
- Functional specifications
- Source code
- Architectural models
- Environment configurations

**Governance** (examples, non-exhaustive)
- Policies
- Constraints
- Rulesets
- Compliance standards
- Ethical guidelines

**Execution** (examples, non-exhaustive)
- Execution directives
- Execution Evidence
- Logs and rejports

The classification of a carrier instance is determined by its **functional contribution** to the system’s traceability. By categorizing carriers in this manner, the framework ensures that any **Anchor** can resolve to a specific semantic domain, allowing for a structured and decidable examination of the entire system state.

---

## Anchor Relationships

Anchors form four fundamental structural patterns:

- **Linear**
- **Net**
- **Set**
- **Time**

These are not storage formats, but structural constraints over anchors.

Let a basic anchor be defined as:

$$
A = \langle ID, C, \tau \rangle
$$

Where:

- $ID$ : Logical identifier
- $C$ : Carrier (artifact base)
- $\tau$ : Temporal coordinate (timestamp or version)

---

### Linear Anchor Relationship (Chain)

**Definition**

A **linear anchor relationship** is a totally ordered sequence of anchors representing a single progression.

$$
L = [A_1, A_2, ..., A_n]
$$
 
$$
\tau(A_i) < \tau(A_{i+1}) \quad \forall i
$$

**Structural Constraint**

- Each anchor has at most one predecessor and one successor.
- Total temporal ordering is preserved.
- No branching.
    
$$
A_i \rightarrow A_{i+1}
$$

**Semantic Meaning**

Represents:

- Requirement → Implementation → Test → Evidence
- Sequential workflow
- Causal progression
- Pipeline stages

**Example (Chain Notation)**

```
REQ-AUTH-091@v1.2@2026-02-10T14:30
        ↓
Code-Auth@v2.1@2026-02-11T09:00
        ↓
Test-Auth@v1.5@2026-02-11T10:00
        ↓
Evidence@2026-02-11T10:05
```

This expresses a **single deterministic path**.

---

### Net Anchor Relationship (Directed Graph)

**Definition**

A **net anchor relationship** is a directed graph allowing branching and merging.

$$
N = (V, E)
$$

Where:

$$
V = \{A_1, A_2, ..., A_n\}
$$
 
$$
E \subseteq V \times V
$$

Each edge:

$$
(A_i, A_j) \in E
$$

**Structural Constraint**

- Partial ordering (not total)
- Multiple incoming/outgoing edges allowed
- Directed relationships

**Semantic Meaning**

Represents:

- Multiple implementations
- Parallel development
- Dependency networks
- Impact propagation

**Example (Graph Mapping Notation)**

```yaml
net:
  REQ-091:
    - Code-Auth
    - Code-OAuth

  Code-Auth:
    - Test-Auth

  Code-OAuth:
    - Test-Auth

  Test-Auth:
    - Evidence
```

Visual interpretation:

```less
      REQ-091
       /    \
   Code-A  Code-O
       \    /
      Test-Auth
          |
      Evidence
```

Unlike Linear, this structure allows branching and merging.

---

### Set Anchor Relationship (Membership Structure)

**Definition**

An **anchor set** is a named collection of anchors with no inherent ordering.

$$
S = \langle S_{id}, M, \tau_s \rangle
$$

Where:

-  $S_{id}$  : Unique set identifier
-  $M \subseteq V$  : Member anchors
-  $\tau_s$  : Time when the set was defined

Membership condition:

$$
A \in S \iff A \in M
$$

**Structural Constraint**

- No ordering
- No directional edges
- Pure membership relation

**Semantic Meaning**

Represents:

- Scope
- Boundary
- Constraint grouping
- Directive grouping
- Compliance target definition

**Example (Set Notation)**

```
SCOPE-Auth-001 = {
  REQ-AUTH-091@v1.2,
  Code-Auth-Password@v2.1,
  Code-Auth-OAuth@v1.0,
  Test-Auth@v1.5
}
```

Membership evaluation:

```
Code-Auth-Password ∈ SCOPE-Auth-001  ✓
Code-Core           ∈ SCOPE-Auth-001  ✗
```

**Set Operations**

$$
S_1 \cap S_2
$$
 
$$
S_1 \cup S_2
$$
 
$$
S_1 \setminus S_2
$$
 
$$
S_1 \subseteq S_2
$$

These operations enable:

- Conflict detection
- Scope compliance
- Boundary enforcement

---

### Time Anchor Relationship (Evolution Structure)

**Definition**

A **time anchor relationship** tracks the evolution of the same spatial anchor across temporal coordinates.

Let spatial anchor be:

$$
A_{spatial} = \langle ID, C \rangle
$$

Timeline:

$$
T(A_{spatial}) = \{ A@\tau_1, A@\tau_2, ..., A@\tau_n \}
$$

Where:

$$
\tau_1 < \tau_2 < ... < \tau_n
$$

**Structural Constraint**

- Total temporal ordering
- Same spatial anchor (same ID + Carrier)
- Multiple temporal versions

**Semantic Meaning**

Represents:

- Version history
- Artifact evolution
- Temporal queries
- Change tracking

**Example (Timeline Notation)**

```
Timeline(REQ-AUTH-091)

2025-12-01 ── v1.0
2026-01-15 ── v1.1
2026-02-10 ── v1.2
```

Equivalent formal query:

$$
version\_at(A, t) = A@\tau
$$

Where:

$$
\tau = \max\{\tau' \mid \tau' \le t\}
$$

---

## Structural Properties and Composition

The four anchor relationship forms — Linear, Net, Set, and Time —
define structural constraints rather than storage formats.

- Linear → total order constraint
- Net → partial order constraint
- Set → membership constraint
- Time → temporal ordering over identical spatial anchors

These structures are composable rather than independent:

- A Linear relationship is a constrained form of Net (no branching).
- Nets may evolve over Time.
- Sets may group anchors participating in Linear or Net structures.
- Time applies orthogonally to all other structures.

No additional structural primitive is required.

All higher-level software engineering operations 
(trace, impact, diff, scope validation, version query) 
are reducible to standard graph and set operations 
over these four structural forms.

---

## Applications

This section demonstrates how Anchor definitions and relationships manifest in practical software development scenarios.  
All examples use engineering-readable formats (document headers, code comments, YAML blocks), while remaining formally grounded.

---

### From Identifier to Spatiotemporal Anchor

**Logical Identifier (ID)**

```text
FR-001
```

This is only a logical identifier.  
It has no carrier and no temporal coordinate.

---

**Spatial Anchor (Carrier-bound)**

```markdown
SRS-FR-001:
The system shall enforce password length ≥ 12.
```

Formal definition:

$$
A_{spatial} = \langle ID, C \rangle
$$

Where:

- ID = FR-001
- C = SRS document

Now the anchor is tied to a persistent carrier.

---

**Spatiotemporal Anchor**

```markdown
SRS-FR-001@v1.2.0:
The system shall enforce password length ≥ 12.
```

Formal definition:

$$
A = \langle ID, C, \tau \rangle
$$

Where:

- τ = version or timestamp

Now the anchor is fully examinable in space and time.

---

### Anchor Relationships in Engineering Context

---

#### Linear Relationship — Sequential Implementation

**Scenario: Requirement → Code → Test → Evidence**

```markdown
SRS-FR-001@v1.2.0
```

```python
# SPEC: SRS-FR-001
def validate_password(pw):
    return len(pw) >= 12
```

```python
# TEST: SRS-FR-001
def test_password_length():
    assert validate_password("123456789012") == True
```

```text
EVIDENCE-TEST-RESULT@2026-02-11T10:05: PASS
```

Formal structure:

$$
L = [A_1, A_2, A_3, A_4]
$$
 
$$
\tau(A_i) < \tau(A_{i+1})
$$

This represents a **single-path progression** from specification to execution evidence.

---

#### Net Relationship — Branching Dependencies

**Scenario: One Requirement → Multiple Implementations**

```markdown
SRS-FR-002:
The system shall support both password and OAuth authentication.
```

```python
# SPEC: SRS-FR-002
def password_auth():
    ...

# SPEC: SRS-FR-002
def oauth_auth():
    ...
```

```python
# TEST: SRS-FR-002
def test_authentication():
    ...
```

Formal structure:

$$
N = (V, E)
$$

Where:

- V = {anchors}
- E = directed edges

Graph:

```
         SRS-FR-002
         ↓        ↓
password_auth  oauth_auth
              ↓
      test_authentication
```

This structure models:

- Branching implementation
- Merging validation
- Dependency propagation

---

#### Set Relationship — Scope / Constraint Definition

**Scenario: Prescriptive Scope Before Implementation**

```yaml
SCOPE-AUTH-001:
  defined_at: 2026-02-11T08:00
  sources:
    - SRS-FR-002@v1.0
  targets:
    - auth/password.py
    - auth/oauth.py
  forbidden:
    - core/system.py
```

After execution:

```text
Changed files:
- auth/password.py
- auth/oauth.py
- core/system.py   ❌
```

Formal validation:

$$
S_{actual} \subseteq S_{prescriptive} ?
$$

Result: FALSE → Scope violation.

Set relationships represent:

- Boundary definition
- Membership constraints
- Compliance validation

---

#### Time Relationship — Version Evolution

**Scenario: Requirement Evolution**

```markdown
SRS-FR-001@v1.0:
Password length ≥ 8

SRS-FR-001@v1.1:
Password length ≥ 8 + OAuth support

SRS-FR-001@v1.2:
Password length ≥ 12 + OAuth + 2FA
```

Formal:

$$
T(\langle ID, C \rangle) = [A@\tau_1, A@\tau_2, ..., A@\tau_n]
$$

Temporal query:

$$
version\_at(\langle ID, C \rangle, t) = \max\{\tau \mid \tau \leq t\}
$$

Example:

```text
version_at(SRS-FR-001, 2026-01-20) → SRS-FR-001@v1.1
```

Time relationship enables:

- Historical reconstruction
- Version lookup
- Change impact over time

---

### Derived Engineering Operations

All higher-level software engineering analyses derive from the four structural relationships.

---

#### Trace

**Forward Trace**

Given:

```markdown
SRS-FR-001@v1.2.0
```

Find:

- Code referencing `# SPEC: SRS-FR-001`
- Tests referencing it
- Execution evidence generated

Formal:

$$
forward(A) = \{A' \mid A \leadsto A'\}
$$

Graph traversal over Net.

---

#### Impact Analysis

Modify:

```python
# SPEC: SRS-FR-001
def validate_password(pw):
```

Impact includes:

- All tests referencing it
- All scopes containing it
- All evidence linked to it

Formal:

$$
impact(A) = forward(A)
$$

Optionally include Set membership:

$$
impact(A) = forward(A) \cup \{S \mid A \in S\}
$$

---

#### (Temporal Comparison)

```text
diff(SRS-FR-001@v1.1, SRS-FR-001@v1.2)
```

Result:

```diff
- Password ≥ 8
+ Password ≥ 12
+ Added 2FA support
```

Formal:

$$
diff(A@\tau_1, A@\tau_2) = \Delta(resolve(A@\tau_1), resolve(A@\tau_2))
$$

---

#### Scope Validation

Before execution:

```yaml
targets:
  - auth/password.py
  - auth/oauth.py
```

After execution:

```text
Modified:
- auth/password.py
- auth/oauth.py
- core/system.py
```

Formal check:

$$
S_{actual} \subseteq S_{declared}
$$

If not, violation detected.

---

#### Version Reconstruction

Extract timeline:

$$
timeline(\langle ID, C \rangle) = \{A@\tau_1, ..., A@\tau_n\}
$$

Allows:

- Historical audit
- Evolution tracing
- Change propagation analysis

---

### Integrated Scenario

**Question:**

Did implementation of SRS-FR-002 respect declared scope and produce valid evidence?

Steps:

1. Extract Net from requirement
2. Extract Linear path to evidence
3. Compare Set (prescriptive vs actual)
4. Verify Time consistency

All operations are:

- Graph traversal
- Set operations
- Temporal ordering queries

No specialized reasoning engine required.

---

### Structural Principle Demonstrated

Applications illustrate that:

- Trace = graph traversal
- Impact = reachability
- Diff = temporal comparison
- Scope validation = set inclusion
- Version query = ordered selection

All derive from:

- Linear (total order)
- Net (partial order)
- Set (membership constraint)
- Time (temporal order over identical spatial anchors)

---

## Related Work

### Provenance Models

The W3C PROV-DM framework formalizes provenance as entities, activities, and
agents connected through derivation relations. While PROV-DM captures *what
happened*, it assumes that entities and activities are already identifiable
and does not define how artifacts become structurally anchorable prior to
provenance recording.

Anchor Architecture operates at a more fundamental layer by defining how
identifiers are bound to carriers and time before provenance relations can
be meaningfully asserted.

### Software Supply Chain Attestation

Frameworks such as SLSA and in-toto focus on build integrity, artifact
attestation, and secure pipelines. These systems assume well-defined build
steps and artifact boundaries.

Anchor Architecture does not assume a pipeline or security objective. It
generalizes the notion of artifact reference and execution evidence to any
software, execution, or governance carrier.

### Requirements Traceability

Classical requirements traceability approaches link requirements to design,
code, and tests through matrices or tooling conventions. These approaches
often collapse under scale due to implicit assumptions about artifact identity
and versioning.

Anchor Architecture reframes traceability as a spatiotemporal anchoring problem,
independent of tooling or lifecycle phase.

### Program Analysis and Change Impact

Static and dynamic program analysis techniques infer dependencies and impact
through code structure and execution behavior. Such methods are inherently
inferential and incomplete when artifacts are missing or ambiguous.

Anchor Architecture does not infer relationships; it makes them structurally
examinable by construction.

---

## Conclusion

Anchor Architecture defines traceability as a structural property rather than
an inferential outcome. By progressively anchoring identifiers to carriers and
time, systems gain examinable relationships across software, execution, and
governance—independent of AI models, tools, or human memory.

---

## References

[1] W3C. *PROV-DM: The PROV Data Model*. W3C Recommendation, 2013.  
[2] SLSA Working Group. *Supply-chain Levels for Software Artifacts*. OpenSSF, 2021.  
[3] in-toto. *A Framework to Secure the Integrity of Software Supply Chains*.  
[4] Gotel, O., Finkelstein, A. *An Analysis of the Requirements Traceability Problem*. IEEE, 1994.  
[5] Mens, T., Demeyer, S. *Software Evolution*. Springer, 2008.  
[6] Kitchenham, B. et al. *Evidence-Based Software Engineering*. IEEE Software, 2004.
