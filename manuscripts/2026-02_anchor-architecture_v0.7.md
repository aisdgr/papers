# Anchor Architecture

*A Minimal Structural Foundation for Software Traceability*

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703
**Email:** spark.tsai@gmail.com
**Date:** February 2026  

---

## Abstract

As software development increasingly incorporates AI assistance and autonomous systems, relationships between specifications, code, executions, and governance artifacts often degrade into post-hoc interpretation and speculation.

This paper presents **Anchor Architecture**, a model-independent and pre-analytical framework for structural traceability. The framework does not depend on AI models, prompts, inference transparency, or tool-specific metadata schemas. Instead, it defines traceability as a property that emerges from **spatiotemporal anchoring**.

Anchor Architecture is intentionally minimal and consists of two primitives:

- **Anchor** — a spatiotemporal coordinate
- **Relationship** — a directed structural connection

All structural views (linear, net, set, timeline) and all operations (trace, impact, diff, version) are derived from these primitives.

The central claim is that traceability failures are not caused by opaque reasoning, but by missing structural anchors. Once entities are bound to persistent locations and temporal indices at creation time, relationships become structurally examinable rather than interpretively reconstructed.

---

## Keywords

Anchor Architecture, Structural Traceability, Spatiotemporal Coordinate, Pre-Analytical Structure, Implicit Traceability, Software Engineering

---

## 1. Introduction

### 1.1 Motivation

Modern software systems are no longer produced solely through direct human authorship. AI-assisted tools and autonomous agents increasingly generate, modify, and deploy artifacts across the development lifecycle.

However, regardless of whether changes are produced by humans or AI systems, one structural problem persists:

> Relationships between artifacts are often reconstructed after the fact.

When identifiers, locations, and time states are not structurally bound at creation, later analysis becomes speculative. Logs, narratives, and inferred histories cannot guarantee structural certainty.

### 1.2 Core Claim

Traceability failures are not caused by opaque reasoning.

They are caused by missing anchors.

Without spatiotemporal anchoring, relationships cannot be examined structurally and must instead be guessed.

### 1.3 Contributions

This paper makes the following contributions:

1. Defines **Anchor** as a minimal spatiotemporal coordinate.
2. Defines **Relationship** as a directed structural connection between anchors.
3. Establishes four structural views: Linear, Net, Set, Timeline.
4. Formalizes structural operations: trace(), impact(), diff(), version().
5. Demonstrates that traceability is a structural property, not an annotation practice.
6. Establishes pre-analytical anchoring as a necessary condition for examinability.

### 1.4 Scope

This paper focuses on structural foundations.

It does not:

- Propose a tool
- Define a schema
- Bind to CI/CD systems
- Depend on AI models
- Prescribe governance frameworks

It defines only the minimal structural condition required for traceability.

---

## 2. Anchor Architecture Primitives

Anchor Architecture consists of two primitives:

1. **Anchor**
2. **Relationship**

Everything else is derived.

---

## 3. Anchor

An **Anchor** is a spatiotemporal coordinate that binds identity to a persistent location and a temporal state.

An anchor does not contain content.  
It defines where and when content exists.

### 3.1 Progressive Anchoring

Anchoring is defined as progressive structural binding:

1. Identifier (ID)
2. Spatial Anchor
3. Spatiotemporal Anchor

This progression is structural, not semantic.

---

### 3.2 Identifier (ID)

An **Identifier (ID)** establishes a persistent logical reference to a structural entity.

Formally:

$$
ID = f_{id}(Entity)
$$

---

#### Structural Entity

A **Structural Entity** is an independently referenceable unit within a system.

Examples:

- A requirement paragraph
- A function or class
- A test case
- A transaction
- A deployment event

A structural entity is:

- Atomic for reference
- Independently identifiable
- Bound by single responsibility
- Capable of being versioned

This definition is conceptual and not limited to data models.

---

#### Properties:

* Entity Naming — uniquely labels a structural entity
* Location Neutral — does not imply storage location
* Temporal Neutral — does not imply version or time
* Structural Necessity — identity must exist before spatial binding

An ID alone is insufficient for examinability.
It establishes existence, not decidability.

---

#### Example

$$
ID = FR\text{-}091
$$

---

#### Implementation Snippet (Specification)

```markdown
### FR-091
Password length must be ≥ 12 characters.
```

No location or time is implied here.

---

### 3.3 Spatial Anchor

A Spatial Anchor binds identity to a persistent location.

$$
A_s = \langle ID, L \rangle
$$

Where:

* $L$  = persistent locator
* Locator must satisfy **Resolvability**

---

#### Resolvability Property

A locator must provide deterministic resolution within its context.

$$
resolve(\langle ID, L \rangle) \to Content
$$

---

#### Example

$$
A_s = \langle FR\text{-}091,\; srs/auth.md \rangle
$$

---

#### Implementation Snippet

```markdown
<!-- Anchor: FR-091 | srs/auth.md -->

### FR-091
Password length must be ≥ 12 characters.
```

---

### 3.4 Spatiotemporal Anchor

A Spatiotemporal Anchor binds identity, location, and time.

$$
A = \langle ID,\; L,\; \tau \rangle
$$

Where:

* $\tau$  = temporal index
  * version number
  * timestamp

An anchor is a coordinate — not a container.

$$
resolve(A) \to Content
$$

---

#### Example

$$
A_{req} = \langle FR\text{-}091,\; srs/auth.md,\; v1.2 \rangle
$$
 
$$
A_{log} = \langle TEST\text{-}AUTH\text{-}RESULT,\; logs/auth-test.log,\; 2026-02-11T09:58:47.540Z \rangle
$$

---

#### Implementation Snippet (Specification)

```markdown
<!-- Anchor: FR-091 | srs/auth.md | v1.2 -->

### FR-091
Password length must be ≥ 12 characters.
```

---

#### Implementation Snippet (Code)

```python
# Anchor: FUNC-validate | src/auth.py | v1.2

def validate_password(password: str) -> bool:
    return len(password) >= 12
```

---

### 3.5 Progressive Expansion Principle

Anchoring proceeds monotonically:

$$
ID \rightarrow \langle ID, L \rangle \rightarrow \langle ID, L, \tau \rangle
$$

Each expansion increases structural determinacy.

* ID → existence
* Spatial → resolvability
* Spatiotemporal → examinability

---

### 3.6 Spatial Uniqueness

Two spatial anchors are equal if and only if both identity and location match.

$$
\langle ID, L \rangle = \langle ID', L' \rangle \iff ID = ID' \land L = L'
$$

---

#### Example

Same ID but different location:

$$
\langle FR\text{-}091,\; srs/auth.md \rangle \neq \langle FR\text{-}091,\; srs/security.md \rangle
$$

Even though the identifier is the same (`FR-091`),  
the locator differs. Therefore they are **distinct spatial anchors**.

---

#### Implementation Snippet

Two different documents referencing similarly named sections:

```markdown
<!-- Anchor: FR-091 | srs/auth.md -->

### FR-091
Password must support OAuth authentication.
```

```markdown
<!-- Anchor: FR-091 | srs/security.md -->

### FR-091
Password must be stored using bcrypt hashing.
```

Although both use the same symbolic ID,  
they reside in different persistent locations.

Therefore:

* Identity alone is insufficient.
* Location participates in spatial uniqueness.

Only when both `ID` and `L` match does a spatial anchor remain identical.

---

### 3.7 Spatiotemporal Uniqueness

Two anchors are equal if and only if all three components match.

$$
A = A' \iff ID = ID' \land L = L' \land \tau = \tau'
$$

This guarantees coordinate-level uniqueness.

---

#### Example

$$
\langle FR\text{-}091,\; srs/auth.md,\; v1.2 \rangle \neq \langle FR\text{-}091,\; srs/auth.md,\; v1.3 \rangle
$$

---

#### Implementation Snippet

```markdown
<!-- Anchor: FR-091 | srs/auth.md | v1.3 -->

### FR-091
Password length must be ≥ 16 characters.
```

Different temporal coordinate → different anchor.

---

## 4. Core Principles

### 4.1 Pre-Analytical Existence

Anchors must be committed at creation time.

If an anchor does not exist prior to analysis, analysis becomes speculative.

Traceability cannot be reconstructed post-hoc with certainty.

---

### 4.2 Spatiotemporal Coordinates

An anchor is a coordinate system.

It separates identity from state.

It allows:

- Deterministic resolution
- Historical query
- Time travel analysis

---

### 4.3 Implicit Traceability

Relationships can be inferred structurally.

Given:

$$
A_1 = \langle ID_1, L_1, \tau_1 \rangle
$$
 
$$
A_2 = \langle ID_2, L_2, \tau_2 \rangle
$$

If:

- A structural relation exists
-  $\tau_1 < \tau_2$ 

Then causal direction is structurally constrained.

Explicit annotation is not required for every semantic link.

---

### 4.4 Non-Reconstructibility

If temporal index is not recorded at creation:

It cannot be reconstructed uniquely later.

Multiple histories can produce identical present states.

Therefore:

Anchoring must occur at source.

---

## 5. Relationship

### 5.1 Formal Definition

A **Relationship** is a directed structural connection between anchors.

$$
R \subseteq A \times A
$$
 
$$
(A_i, A_j) \in R
$$

Where:

- $A$ : the set of all Anchors
- $A_i$ : source anchor
- $A_j$ : target anchor
- $R$ : a set of ordered anchor pairs

A relationship contains **no embedded semantics**.  
It expresses only structural adjacency between two anchors.

---

#### Structural Adjacency

By defining relationships as ordered pairs of anchors,  
the architecture replaces **semantic inference**  
(guessing how artifacts relate)  
with **structural adjacency**  
(recording that two anchors are connected).

In this manifold:

> A relationship is a directed vector between two points in spatiotemporal coordinates.

Traceability therefore becomes geometric rather than interpretive.

---

#### Example (Formula)

Let:

$$
A_{req} = \langle FR\text{-}091,\; srs/auth.md,\; v1.2 \rangle
$$
 
$$
A_{code1} = \langle FUNC\text{-}validate\text{-}password,\; src/auth/password.py,\; 1.4.0 \rangle
$$
 
$$
A_{code2} = \langle FUNC\text{-}oauth\text{-}fallback,\; src/auth/oauth.py,\; 2.1.3 \rangle
$$

Then:

$$
R = \{ (A_{req}, A_{code1}), (A_{req}, A_{code2}) \}
$$

---

#### Implementation Snippet (Specification)

```markdown
ID: FR-091
Location: srs/auth.md
Version: v1.2

Requirement:
Password length must be >= 12 characters.
```

---

#### Implementation Snippet (Code)

```python
# ID: FUNC-validate-password
# TRACE: FR-091
# Version: 1.4.0

def validate_password(pwd: str) -> bool:
    return len(pwd) >= 12
```

```python
# ID: FUNC-oauth-fallback
# TRACE: FR-091
# Version: 2.1.3

def oauth_password_policy(pwd: str) -> bool:
    if external_provider():
        return True
    return len(pwd) >= 12
```

These fragments instantiate the formal structural relation above.

---

### 5.2 Multiplicity Property

Relationship is structurally **many-to-many**.

The architecture imposes no cardinality constraint.
No uniqueness, hierarchy, or tree assumption is embedded in the primitive.

Formally:

$$
\forall A_i \in A,\;
|\{ A_j \mid (A_i, A_j) \in R \}| \ge 0
$$

$$
\forall A_j \in A,\;
|\{ A_i \mid (A_i, A_j) \in R \}| \ge 0
$$

This implies:

- One anchor may relate to zero, one, or many anchors.
- Multiple anchors may relate to the same anchor.
- Absence of relation is permitted.
- Symmetry is not assumed:
  $$
  (A_i, A_j) \in R \nRightarrow (A_j, A_i) \in R
  $$

All mapping patterns are structural special cases:

- one-to-one
- one-to-many
- many-to-one
- many-to-many

The architecture therefore supports general directed graphs.

---

#### Many-to-One Example

Suppose `validate_password()` also implements `FR-102`.

$$
R =
\{
(A_{FR091}, A_{code}),
(A_{FR102}, A_{code})
\}
$$

No hierarchy is required.

A tree structure is merely a constrained special case of a directed graph.

---

#### Evolutionary Relation (Temporal Projection)

Multiplicity also includes temporal multiplicity.

Given two anchors sharing identity and location:

$$
A_{\tau_1} = \langle ID, L, \tau_1 \rangle
$$

$$
A_{\tau_2} = \langle ID, L, \tau_2 \rangle
$$

where:

$$
\tau_1 < \tau_2
$$

Define the timeline projection as a constrained subset of the general relation:

$$
R_{timeline} =
\{
(A_i, A_j)
\in R
\mid
ID_i = ID_j
\land L_i = L_j
\land \tau_i < \tau_j
\}
$$

Timeline introduces **no additional primitive**.

It is a **view over relationship space** —
a projection of $R$ constrained by identity equality and temporal ordering.

Version history therefore emerges structurally,
not architecturally.

---

### 5.3 Graph Nature

Because:

$$
R \subseteq A \times A
$$

the structure formed by anchors and relationships is a 
**directed graph**:

$$
G = (A, R)
$$

Under temporal constraint, it becomes a 
**Directed Acyclic Graph (DAG)**.

---

#### Temporal Monotonicity Constraint

For every structural relation:

$$
(A_i, A_j) \in R
$$

the temporal index must satisfy:

$$
\tau(A_i) \le \tau(A_j)
$$

In most engineering contexts:

$$
\tau(A_i) < \tau(A_j)
$$

Therefore, structural cycles that violate temporal ordering are disallowed.

---

#### Structural Properties

- Relationship is temporally monotonic  
  → Structural cycles are disallowed
- Multiple incoming and outgoing edges are permitted
- No implicit parent constraint
- No enforced tree structure
- Trees are special cases of DAGs

---

#### Operational Consequences

Graph traversal yields:

- `trace()` → reachable nodes
- `impact()` → reachable subgraph
- `version()` → temporal projection
- `diff()` → anchor comparison

Relationship defines geometry.  
Operations explore it.

---

### 5.4 No Embedded Semantics

Relationship expresses structural connectivity only.

Semantic labels such as:

- implements
- tests
- governs
- depends\on

are **not architectural primitives**.

They are application-layer interpretations derived from:

- structural patterns
- domain rules
- operational queries

---

#### Semantic Delegation

The architecture delegates semantic interpretation to the application layer.

While the architecture records:

$$
(A_i, A_j) \in R
$$

a governance tool may interpret this as **“violates”**,  
while a development tool interprets it as **“implements.”**

Both interpretations operate on the same invariant structural geometry.

The structure is fixed.  
Meaning is delegated.

This preserves minimality and prevents semantic coupling at the foundational layer.

---

### 5.5 Structural Validity Principle

A relationship is structurally valid **only if both participating anchors exist and are resolvable**.

Formally:

$$
(A_i, A_j) \in R \Rightarrow A_i \in A \land A_j \in A
$$

Additionally:

$$
resolve(A_i) \neq \varnothing \land resolve(A_j) \neq \varnothing
$$

If:

$$
resolve(A_k) = \varnothing
$$

then:

$$
(A_i, A_k) \notin R_{valid}
$$

---

#### Interpretation

A relationship cannot exist independently of anchors.

If an anchor:

- was never created
- was deleted
- lacks a temporal index
- cannot be resolved

then any relation referencing it is structurally void.

This is not an application-layer error.  
It is a geometric invalidity.

---

#### Example (Broken Relation)

Let:

$$
A_{ghost} = \langle FR\text{-}999,\; srs/auth.md,\; v1.0 \rangle
$$

But `FR-999` does not exist in `srs/auth.md@v1.0`.

$$
resolve(A_{ghost}) = \varnothing
$$

Therefore:

$$
(A_{ghost}, A_{code}) \notin R_{valid}
$$

The relationship collapses.

---

#### Example (Code Annotation Case)

```python
# ID: FUNC-reset-password
# TRACE: FR-999
# Version: 1.2.0
```

If `FR-999` has no corresponding anchor:

- The annotation exists
- The structural anchor does not
- The relationship is invalid

---

### 5.6 Structural Implication

Because anchors must be established pre-analytically,  
relationships become structurally examinable rather than interpretively reconstructed.

Meaning:

- Trace is graph traversal
- Impact is reachability
- Diff is anchor comparison
- Version is temporal query

Traceability is not documentation.  
It is coordinate geometry.

---

### 5.7 Structural Determinism vs. AI Hallucination

Because relationship validity depends strictly on anchor resolvability,  
an AI agent cannot hallucinate a **structurally valid** traceability link.

Even if a large language model generates a tag such as:

```python
# TRACE: FR-999
```

the architecture evaluates validity exclusively through anchor existence.

A relationship is valid **if and only if** both anchors are resolvable at their full spatiotemporal coordinates:

$$
(A_i, A_j) \in R_{valid} \iff resolve(A_i) \neq \varnothing \land resolve(A_j) \neq \varnothing
$$

Where each anchor is defined as:

$$
A = \langle ID, L, \tau \rangle
$$

Thus, resolvability requires:

$$
resolve(\langle ID, L, \tau \rangle) \neq \varnothing
$$

This condition simultaneously requires:

- The **Identifier** exists.
- The **Locator** resolves to a persistent structural position.
- The **Temporal Index** corresponds to a committed state.

All three coordinates must be present and consistent.

If any component is missing:

$$
resolve(\langle ID, L, \tau \rangle) = \varnothing
$$

then:

$$
(A_i, A_j) \notin R_{valid}
$$

The relationship collapses geometrically.

---

#### Structural Consequence

The architecture enforces:

1.  No anchor → no relation
2.  No resolvability → no validity
3.  No temporal commitment → no examinability

A language model may generate symbolic references,  
but symbolic references do not constitute structural anchors.

Validity is not derived from plausibility.  
It is derived from coordinate existence.

---

#### Deterministic Shift

This shifts the burden of proof:

> From model transparency  
> to structural existence.

AI reasoning may speculate.  
Structure cannot.

---

## 6. Structural Views

Structural Views are constrained projections of the general relation:

$$
R \subseteq A \times A
$$

They introduce no new primitives.  
Each view is a restriction or projection over the same anchor set $A$ and relation set $R$.

---

### 6.1 Linear View

A Linear View is a total ordered path derived from $R$.

Formally, a linear chain is a sequence of anchors:

$$
L = [A_1, A_2, \dots, A_n]
$$

such that:

$$
(A_i, A_{i+1}) \in R
$$

and:

$$
\tau_1 < \tau_2 < \dots < \tau_n
$$

This represents sequential structural progression.

---

#### Example (Formula)

Let:

$$
A_{req} = \langle FR\text{-}091,\; srs/auth.md,\; v1.2 \rangle
$$

$$
A_{code} = \langle FUNC\text{-}validate\text{-}password,\; src/auth/password.py,\; 1.4.0 \rangle
$$

$$
A_{test} = \langle TEST\text{-}auth,\; tests/test_auth.py,\; 1.0.1 \rangle
$$

If:

$$
(A_{req}, A_{code}) \in R
$$

$$
(A_{code}, A_{test}) \in R
$$

Then:

$$
L = [A_{req}, A_{code}, A_{test}]
$$

---

#### Implementation Snippet

```markdown
<!-- srs/auth.md -->
ID: FR-091
Version: v1.2
Password must be >= 12 characters.
````

```python
# src/auth/password.py
# ID: FUNC-validate-password
# TRACE: FR-091
# Version: 1.4.0
```

```python
# tests/test_auth.py
# ID: TEST-auth
# TRACE: FUNC-validate-password
# Version: 1.0.1
```

---

### 6.2 Net View

The Net View represents the full directed relationship space.

It is a projection of:

$$
G = (A, R)
$$

subject only to temporal monotonicity:

$$
(A_i, A_j) \in R \Rightarrow \tau(A_i) \le \tau(A_j)
$$

Characteristics:

- Arbitrary branching permitted
- Multiple incoming and outgoing edges allowed
- No hierarchy enforced
- No tree constraint imposed
- No cardinality restriction

The Net View represents the complete structural manifold.

---

#### Example (Formula)

$$
R = \{ (A_{req}, A_{code1}), (A_{req}, A_{code2}), (A_{code1}, A_{test}), (A_{code2}, A_{test}) \}
$$

This yields a branching graph:

```
FR-091
  |    \
code1  code2
   \    /
   TEST-auth
```

---

#### Implementation Snippet

```markdown
<!-- srs/auth.md -->
ID: FR-091
Version: v1.2
Password must be >= 12 characters.
````

```python
# FUNC-validate-password
# TRACE: FR-091
```

```python
# FUNC-oauth-fallback
# TRACE: FR-091
```

```python
# TEST-auth
# TRACE: FUNC-validate-password
# TRACE: FUNC-oauth-fallback
```

Net View captures dependency propagation and impact reachability.

---

### 6.3 Set View

A Set View is a membership projection over anchors.

Formally, define:

$$
S \subseteq A
$$

Membership:

$$
A_i \in S
$$

Set membership does not imply structural adjacency:

$$
A_i \in S \land A_j \in S
\nRightarrow
(A_i, A_j) \in R
$$

Set expresses **semantic grouping**, not structural dependency.

---

#### Example (Scope Boundary)

Define an authentication scope:

$$
S_{scope-auth} =
\{
\langle FR\text{-}091,\; srs/auth.md,\; v1.2 \rangle,
\langle FUNC\text{-}validate\text{-}password,\; src/auth/password.py,\; 1.4.0 \rangle,
\langle LOG\text{-}auth-success,\; logs/auth.log,\; 2026-02-11T10:12:05Z \rangle,
\langle POLICY\text{-}password-strength,\; governance/policy.md,\; v2.0 \rangle
\}
$$

These anchors:

- may not be directly connected by $R$
- may belong to different domains (spec, code, log, governance)
- may have no structural adjacency

They are grouped because they share a **semantic boundary**.

---

#### Implementation Snippet

```markdown
# Scope: Authentication

Includes:
- FR-091
- FUNC-validate-password
- LOG-auth-success
- POLICY-password-strength
```

Set View defines:

- boundary
- scope
- compliance grouping
- evidence aggregation

It does not require adjacency.

---

### 6.4 Timeline View

Timeline is a constrained projection of $R$ over identical identity and location.

Given anchors:

$$
A_{\tau_1} = \langle ID, L, \tau_1 \rangle
$$
 
$$
A_{\tau_2} = \langle ID, L, \tau_2 \rangle
$$

where:

$$
\tau_1 < \tau_2
$$

Define:

$$
R_{timeline} = \{ (A_i, A_j) \in R \mid ID_i = ID_j \land L_i = L_j \land \tau_i < \tau_j \}
$$

Timeline is therefore a constrained subset of $R$.

---

#### Example (Formula)

$$
T(FR\text{-}091) = \{ \langle FR\text{-}091,\; srs/auth.md,\; v1.0 \rangle, \langle FR\text{-}091,\; srs/auth.md,\; v1.1 \rangle, \langle FR\text{-}091,\; srs/auth.md,\; v1.2 \rangle \}
$$

---

#### Implementation Snippet

```markdown
<!-- srs/auth.md -->
ID: FR-091
Version: v1.0
Password >= 8

ID: FR-091
Version: v1.1
Password >= 10

ID: FR-091
Version: v1.2
Password >= 12
```

Timeline emerges from:

- identical ID
- identical location
- ordered temporal index

No additional primitive is introduced.

---

### 6.5 Structural Consistency

All views are derived from:

$$
R \subseteq A \times A
$$

They differ only by constraint:

| View     | Constraint Over R             | Analytical Value       | Example Application       |
| -------- | ----------------------------- | ---------------------- | ------------------------- |
| Linear   | Total temporal order          | Causal Path            | Step-by-step verification |
| Net      | No constraint                 | Impact Propagation     | Blast radius analysis     |
| Set      | Membership only               | Governance Boundary    | Compliance scope          |
| Timeline | Same (ID, L) + temporal order | Evolutionary Integrity | Change rationale          |

Thus:

- Views are projections.
- Geometry is invariant.
- Interpretation is delegated.

---

## 7. Structural Operations

Structural operations are **queries over relation and coordinate space**.

They introduce no new primitives.

All operations derive exclusively from:

- Anchor set  $\mathcal{A}$
- Relation     $R \subseteq \mathcal{A} \times \mathcal{A}$

Let:

$$
R^+
$$

denote the transitive closure of $R$.

All structural analysis reduces to:

- Traversal over $R$ or $R^+$
- Projection over $\mathcal{A}$
- Content resolution via coordinate

No semantic inference is required at this layer.

---

### 7.1 Base Structural Capabilities

Anchor Architecture provides exactly two primitive capabilities.

---

#### 7.1.1 Relation Traversal

Traversal computes structural reachability.

$$
R^+(a) = \{ b \in \mathcal{A} \mid (a,b) \in R^+ \}
$$

This expresses structural propagation without semantic interpretation.

Traversal does not assume:

- hierarchy
- tree structure
- unique parent
- semantic meaning

It is pure relation expansion.

---

#### 7.1.2 Content Resolution

Resolution retrieves content from a coordinate.

Given:

$$
a = \langle ID, L, \tau \rangle
$$

$$
resolve(a) \rightarrow \text{Content}
$$

Resolution is deterministic.

If resolution fails:

Structural examinability at that coordinate cannot be guaranteed.

Resolution failure does not invalidate the anchor definition,  
but prevents structural verification at that moment.

---

### 7.2 Derived Operations (Application Layer)

The following operations are projections over base capabilities.

They are named usage patterns — not new primitives.

---

#### 7.2.1 trace()

##### Definition

trace is **goal-oriented traversal with path preservation**.

Given:

- source anchor $a$
- predicate $P$ over anchors

$$
trace(a, P) = \{ \text{ordered sequences } (a \rightarrow \dots \rightarrow b) \mid b \in R^+(a) \land P(b) \}
$$

##### Properties

- Requires a termination condition $P$
- Returns complete causal chains
- If no reachable anchor satisfies $P$, result is empty
- Preserves structural ordering

trace answers:

> "Through what structural chain does a reach a target?"

---

##### Example

If:

$$
P(x) := \text{x is a Test anchor}
$$

Then:

$$
trace(A_{FR091}, P) = \{ (A_{FR091}, A_{code1}, A_{test}), (A_{FR091}, A_{code2}, A_{test}) \}
$$

---

##### Implementation Illustration

```python
# ID: FUNC-validate-password
# TRACE: FR-091
# Version: 1.4.0
def validate_password(pwd):
    return len(pwd) >= 12
```

trace reconstructs the structural chain,  
not the semantic meaning of "implements".

---

#### 7.2.2 impact()

##### Definition

impact is **unconstrained structural expansion**.

$$
impact(a) = R^+(a)
$$

##### Properties

- No termination predicate
- No path preservation
- Returns reachable anchor set
- Order irrelevant

impact answers:

> "If a changes, which anchors are structurally downstream?"

---

##### Example

Using the same structure:

$$
impact(A_{FR091}) = \{ A_{code1}, A_{code2}, A_{test} \}
$$

Note:

trace returns paths.  
impact returns reachable anchors.

They share traversal basis but differ in:

- objective
- return structure
- analytical meaning

---

#### 7.2.3 diff()

##### Definition

diff compares the resolved content of **two distinct anchors**.

Given:

$$
a_1, a_2 \in \mathcal{A}
$$

$$
diff(a_1, a_2)
=
resolve(a_2) \setminus resolve(a_1)
$$

No identity or location equality is required.

The two anchors may:

- share the same ID but differ in temporal index
- share the same location but differ in ID
- differ in all three coordinates

diff is therefore a **content-level comparison**,  
not a version-control operation.

Precondition:

$$
resolve(a_1) \neq \varnothing \land resolve(a_2) \neq \varnothing
$$

If resolution fails, structural comparison cannot be performed.

---

##### Example

Anchors:

$$
\langle FR-091, srs/auth.md, v1.1 \rangle
$$
 
$$
\langle FR-091, srs/auth.md, v1.2 \rangle
$$

diff returns structural content difference,  
not semantic interpretation.

---

##### Implementation Illustration

diff answers:

> How does the resolved content of one anchor differ from another?

Meaning is not embedded in the operation.  
Semantic interpretation of the difference belongs to the application layer.

---

#### 7.2.4 version()

##### Definition

version projects anchors sharing identity and location across temporal indices.

Given fixed:

$$
ID^*, L^*
$$

$$
version(ID^*, L^*) = \{ a \in \mathcal{A} \mid ID_a = ID^* \land L_a = L^* \}
$$

ordered by:

$$
\tau_1 < \tau_2 < \dots < \tau_n
$$

version is therefore a **temporal projection** over a fixed spatial anchor.


---

##### Example

$$
version(FR-091, srs/auth.md) = [ \langle FR-091, srs/auth.md, v1.0 \rangle, \langle FR-091, srs/auth.md, v1.1 \rangle, \langle FR-091, srs/auth.md, v1.2 \rangle ]
$$

---

##### Interpretation

version answers:

> What is the structural evolution of this anchor across time?

The result is an ordered sequence of anchors:

$$
[
\langle ID^*, L^*, \tau_1 \rangle,
\langle ID^*, L^*, \tau_2 \rangle,
\dots,
\langle ID^*, L^*, \tau_n \rangle
]
$$

version does not compute differences.

It returns the immutable structural timeline.

Diff operates across anchors.  
Version organizes anchors along the temporal axis.

---

### 7.3 Structural Summary

All structural analysis reduces to two base capabilities:

- Relation traversal over $R$ and $R^+$
- Content resolution via coordinate

Derived operations are projections:

| Operation | Structural Basis     | Return Structure    | Core Question                           |
| --------- | -------------------- | ------------------- | --------------------------------------- |
| trace()   | Traversal over $R^+$ | Path set            | Through what chain does this propagate? |
| impact()  | Traversal over $R^+$ | Anchor set          | What is downstream?                     |
| diff()    | Content resolution   | Content difference  | What changed?                           |
| version() | Temporal projection  | Ordered anchor list | What is history?                        |

Operations do not introduce semantics.

They operate on coordinates and relations.

Meaning emerges only at application layer.

---

## 8. Comprehensive Example

This section demonstrates Anchor Architecture through a realistic failure scenario.

The goal is not to demonstrate functionality,  
but to demonstrate structural examinability.

---

### 8.1 Scenario

System: Authentication Module

Evolution:

1. Initial requirement: Password ≥ 8
2. Strengthened: Password ≥ 10
3. Further strengthened: Password ≥ 12
4. OAuth introduced
5. After deployment, some users cannot log in

Engineering Question:

- Which requirement version introduced the issue?
- Which code artifacts are affected?
- Has any related code changed after the policy update?

Anchor Architecture answers these structurally.

---

### 8.2 Anchors

#### Requirement Anchors

```markdown
<!-- (FR-091, srs/auth.md, v1.0) -->
Password length must be ≥ 8 characters.
```

```markdown
<!-- (FR-091, srs/auth.md, v1.1) -->
Password length must be ≥ 10 characters.
```

```markdown
<!-- (FR-091, srs/auth.md, v1.2) -->
Password length must be ≥ 12 characters.
```

Formal anchors:

$$
A_{r1} = \langle FR\text{-}091,\; srs/auth.md,\; v1.0 \rangle
$$
 
$$
A_{r2} = \langle FR\text{-}091,\; srs/auth.md,\; v1.1 \rangle
$$
 
$$
A_{r3} = \langle FR\text{-}091,\; srs/auth.md,\; v1.2 \rangle
$$

---

#### Code Anchors

Password validation:

```python
# (FUNC-validate-password, src/auth/password.py, 1.4.0)
# TRACE: FR-091
```

OAuth fallback:

```python
# (FUNC-oauth-fallback, src/auth/oauth.py, 2.1.3)
# TRACE: FR-091
```

Login entry point:

```python
# (FUNC-login, src/auth/login.py, 3.0.1)
# TRACE: FUNC-validate-password
# TRACE: FUNC-oauth-fallback
```

Test anchor:

```python
# (TEST-auth, tests/test_auth.py, 0.9.2)
# TRACE: FUNC-login
```

Formal anchors:

$$
A_{c1} = \langle FUNC\text{-}validate\text{-}password,\; src/auth/password.py,\; 1.4.0 \rangle
$$
 
$$
A_{c2} = \langle FUNC\text{-}oauth\text{-}fallback,\; src/auth/oauth.py,\; 2.1.3 \rangle
$$
 
$$
A_{c3} = \langle FUNC\text{-}login,\; src/auth/login.py,\; 3.0.1 \rangle
$$
 
$$
A_t = \langle TEST\text{-}auth,\; tests/test_auth.py,\; 0.9.2 \rangle
$$

---

### 8.3 Relationship Set

Declared structural relation:

$$
R = \{ (A_{r3}, A_{c1}), (A_{r3}, A_{c2}), (A_{c1}, A_{c3}), (A_{c2}, A_{c3}), (A_{c3}, A_t) \}
$$

Pure ordered-pair relation:

$$
R \subseteq \mathcal{A} \times \mathcal{A}
$$

No embedded semantics.

---

### 8.4 Structural Investigation

Now assume:

Users report login failure after deployment.

We perform structural queries.

---

#### 8.4.1 trace()

**Purpose**

trace() answers:

> Through which structural chain does the requirement reach the failing test?

Targeted traversal:

$$
trace(A_{r3}, A_t)
$$

Result:

$$
\{ (A_{r3}, A_{c1}, A_{c3}, A_t), (A_{r3}, A_{c2}, A_{c3}, A_t) \}
$$

Interpretation:

- Requirement v1.2 affects both password validator and OAuth fallback
- Both feed into login
- Login feeds into test

trace returns **paths**.

It helps:

- Identify the structural chain
- Locate the problematic segment

---

#### 8.4.2 diff()

**Purpose**

diff() answers:

> What changed between requirement versions?

Compare:

$$
diff(A_{r2}, A_{r3}) = resolve(A_{r3}) \setminus resolve(A_{r2})
$$

Structural output:

Change in minimum length from 10 → 12

diff does not assume identity equivalence across arbitrary anchors.  
It compares resolved content of two anchors.

Engineering use:

- Identify the exact policy shift
- Determine whether the failure coincides with that change

---

#### 8.4.3 impact()

**Purpose**

impact() answers:

> Which artifacts are structurally downstream of this requirement version?

$$
impact(A_{r3})
$$

Result (closure over R):

$$
\{ A_{c1}, A_{c2}, A_{c3}, A_t \}
$$

Interpretation:

Requirement v1.2 influences:

- password validator
- OAuth fallback
- login function
- test

impact returns a **set**, not paths.

Use:

- Change propagation analysis
- Inference creep detection
- Blast radius estimation

---

#### 8.4.4 version()

**Purpose**

version() answers:

> What is the structural evolution of this requirement?

$$
version(FR\text{-}091,\; srs/auth.md)
$$

Result:

$$
[ \langle FR\text{-}091,\; srs/auth.md,\; v1.0 \rangle, \langle FR\text{-}091,\; srs/auth.md,\; v1.1 \rangle, \langle FR\text{-}091,\; srs/auth.md,\; v1.2 \rangle ]
$$

Ordered by version.

Engineering use:

- Determine when policy changed
- Check alignment between policy version and deployment version
- Audit structural consistency

---

### 8.5 Investigative Flow

Given login failure:

1. trace()  
   → reveals structural path from requirement to failing test
2. diff()  
   → reveals policy tightened from 10 → 12
3. impact()  
   → reveals OAuth path also affected
4. version()  
   → reveals v1.2 is first appearance of stricter constraint

Conclusion:

Failure coincides with FR-091 v1.2 change.  
Structural evidence confirms propagation chain.

No semantic guessing required.

---

### 8.6 Structural Integrity Demonstration

Suppose someone writes:

```python
# TRACE: FR-999
```

But no anchor:

$$
\langle FR\text{-}999,\; srs/auth.md,\; v1.0 \rangle
$$

exists.

Then:

$$
resolve(\langle FR\text{-}999,\; srs/auth.md,\; v1.0 \rangle) = \varnothing
$$

Therefore:

$$
(A_{ghost}, A_{code}) \notin R_{valid}
$$

The relationship collapses structurally.

---

### 8.7 What This Example Proves

This example demonstrates:

- Anchor as coordinate
- R as relation
- trace() → path discovery
- impact() → affected set
- diff() → content change detection
- version() → structural timeline
- Structural determinism against invalid reference

No graph vocabulary required.  
No tool binding required.  
No AI introspection required.

Traceability becomes coordinate geometry over declared relations.

---

## 9. Related Work

### 9.1 Provenance Models (PROV-DM)

Focus on recording activity provenance.

Anchor Architecture focuses on minimal coordinate determinism.

### 9.2 Version Control

Git tracks file state.

Anchor Architecture generalizes spatiotemporal binding beyond file diffs.

### 9.3 Traceability Matrices

Require manual annotation.

Anchor Architecture enables structural inference.

### 9.4 Supply Chain Attestations

Record artifact integrity.

Anchor Architecture addresses structural examinability.

### 9.5 AI-Generated Code Traceability

Most approaches rely on model transparency.

Anchor Architecture does not.

### 9.6 Differentiation

This architecture defines:

- Minimal primitives
- No tool binding
- No schema dependency
- No semantic enforcement

It defines structural necessity.

---

## 10. Conclusion

Anchor Architecture defines traceability as a structural property.

It consists of:

- Two primitives (Anchor, Relationship)
- Four structural views (Linear, Net, Set, Timeline)
- Four operations (trace, impact, diff, version)

It is:

- Model-independent
- Tool-independent
- Pre-analytical
- Minimal

The core insight:

> Examinability requires structure prior to analysis.

Traceability is not documentation.

It is geometry.

---

## References

- [1] Abhishek Rath et al. "Agent Drift: Quantifying Behavioral Degradation in Multi-Agent LLM Systems Over Extended Interactions." arXiv:2601.04170, 2026. 
- [2] Lin Chen et al. "AI Agent Behavioral Science." arXiv:2506.06366v2, 2025.
- [3] Technical Report: "Evaluating Goal Drift in Language Model Agents." arXiv:2505.02709, 2025.
- [4] Adnan Masood. "Agent Drift: the reliability blind spot in multi-agent LLM systems." Medium, 2026.
- [5] Various authors. Studies on context degradation and user behavior/data drift in LLMs (e.g., Deepchecks reports, 2024–2025). 
- [6] Y. Dong et al. "Safeguarding Large Language Models: A Survey." arXiv:2406.02622, 2024. (Also published in Artificial Intelligence Review, 2025). 
- [7] "Building Guardrails for Large Language Models." arXiv:2402.01822, 2024. 
- [8] "SoK: Evaluating Jailbreak Guardrails for Large Language Models." arXiv:2506.10597, 2025. [9] "A Flexible Large Language Models Guardrail Development Methodology Applied to Off-Topic Prompt Detection." arXiv:2411.12946, 2024 (v2 2025). 
- [10] "When Developer Aid Becomes Security Debt: A Systematic Analysis of Insecure Behaviors in LLM Coding Agents." arXiv:2507.09329, 2025. 
- [11] Junwei Liu et al. "Large Language Model-Based Agents for Software Engineering: A Survey." arXiv:2409.02977, 2024. (Accepted by TOSEM). 
- [12] "From LLMs to LLM-based Agents for Software Engineering: A Survey of Current, Challenges and Future." arXiv:2408.02479v2. 
- [13] "A Survey on Code Generation with LLM-based Agents." arXiv:2508.00083, 2025. 
- [14] Anthropic. "Introducing the Model Context Protocol (MCP)." Anthropic Announcements, November 2024. https://www.anthropic.com/news/model-context-protocol 
- [15] Model Context Protocol official documentation and subsequent engineering blogs (Anthropic, 2024–2025). https://modelcontextprotocol.io/
