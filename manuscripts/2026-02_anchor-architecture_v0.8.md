# Anchor Architecture

*A Minimal Structural Foundation for Software Traceability*

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703  
**Email:** spark.tsai@gmail.com  
**Date:** February 2026  

---

## Abstract

As software development increasingly involves AI-assisted tools and autonomous agents, structural relationships between specifications, code, tests, and governance artifacts degrade into post-hoc reconstruction. Existing traceability approaches — provenance models, version control, traceability matrices, and supply chain attestation — address this problem at various levels but share a common assumption: that the entities being traced are already structurally identifiable. When identifiers, locations, and temporal states are not bound to artifacts at creation time, all subsequent traceability analysis becomes speculative regardless of the sophistication of the tools employed.

This paper presents **Anchor Architecture**, a minimal, model-independent, and pre-analytical framework that defines the structural conditions under which traceability becomes deterministic. The framework consists of exactly two primitives: **Anchor**, a spatiotemporal coordinate $\langle ID, L, \tau \rangle$ that binds identity to a persistent location and temporal index; and **Relationship**, a directed binary relation $R \subseteq \mathcal{A} \times \mathcal{A}$ over the anchor set. From these primitives, four structural views (Linear, Net, Set, Timeline) and four operations (trace, impact, diff, version) are derived without additional axioms, grounded in relation theory and set theory.

The central claim is that traceability failures are caused not by opaque reasoning or insufficient documentation, but by missing structural anchors. The paper formalizes pre-analytical anchoring as a necessary and non-reconstructible condition for structural examinability, and demonstrates through a comprehensive worked example that failure diagnosis, impact analysis, change detection, and integrity validation each reduce to coordinate operations over the relational structure $(\mathcal{A}, R)$. Anchor Architecture is independent of AI models, tooling, and semantic interpretation — it defines the coordinate system upon which provenance, versioning, and governance systems implicitly depend.

---

## Keywords

Anchor Architecture, Structural Traceability, Spatiotemporal Coordinate, Pre-Analytical Anchoring, Relation Theory, Software Engineering, AI-Assisted Development

---

## 1. Introduction

Software artifacts — specifications, code, tests, configurations — are increasingly produced through hybrid authorship involving human developers and AI agents [6][8]. Regardless of the author, a recurring structural problem persists: relationships between artifacts are reconstructed after the fact. Provenance models [1] assume entities are already identifiable; version control tracks file-level states but not arbitrary structural entities; traceability matrices [2] collapse under annotation overhead; supply chain frameworks [4][5] presuppose well-defined artifact boundaries. None address the foundational question: what minimal structural condition must hold *before* any traceability mechanism can operate?

This paper argues that traceability failures are caused by **missing structural anchors** — not by opaque reasoning, insufficient documentation, or inadequate tooling. When identifiers, locations, and temporal states are not bound to artifacts at creation time, all subsequent analysis becomes reconstructive and therefore speculative. This condition is non-reconstructible: structure absent at creation cannot be recovered with certainty post-hoc.

To address this, the paper presents **Anchor Architecture**, a minimal, model-independent framework consisting of exactly two primitives: **Anchor**, a spatiotemporal coordinate $\langle ID, L, \tau \rangle$ that binds identity to a persistent location and temporal index; and **Relationship**, a directed binary relation $R \subseteq \mathcal{A} \times \mathcal{A}$ over the anchor set. From these primitives, the framework derives four structural views — Linear, Net, Set, and Timeline — as projections over the relational structure $(\mathcal{A}, R)$, and four operations — trace(), impact(), diff(), version() — as compositions over the primitive relation, without additional axioms.

The contributions of this paper are: (1) a minimal primitive foundation grounded in relation theory and set theory; (2) derived structural views and operations that reduce failure diagnosis, impact analysis, change detection, and integrity validation to coordinate operations; and (3) a formal characterization of pre-analytical anchoring as a necessary condition for structural examinability. A comprehensive worked example demonstrating these operations over a concrete development scenario is provided in Appendix.

---

## 2. Anchor

An **Anchor** is a spatiotemporal coordinate that binds identity to a persistent location and a temporal state. An anchor does not contain content. It defines where and when content exists.

### 2.1 Definition

#### 2.1 Identifier (ID)

An **Identifier (ID)** establishes a persistent logical reference to a structural entity.

Formally:

$$
ID = f_{id}(Entity)
$$

A **Structural Entity** is independently referenceable:

- Requirement paragraph
- Function
- Test
- Transaction
- Deployment event

Properties:

- Entity Naming
- Location Neutral
- Temporal Neutral
- Structural Necessity

---

#### 2.1.2 Spatial Anchor

A Spatial Anchor binds identity to a persistent location.

$$
A_s = \langle ID, L \rangle
$$

Locator must satisfy **Resolvability**:

$$
resolve(\langle ID, L \rangle) \to Content
$$

---

#### 2.1.3 Spatiotemporal Anchor

A Spatiotemporal Anchor binds identity, location, and time.

$$
\mathcal{A} = \langle ID, L, \tau \rangle
$$

where $\tau$ is a temporal index that establishes when the anchor state was committed.

In practice, $\tau$ is most commonly represented as a **version identifier**
(e.g., `v1.2`, `v2.0`) that corresponds to a specific git commit timestamp.
The version provides human-readable temporal semantics;
the underlying commit timestamp provides strict temporal ordering
across artifacts.

$$
\tau = v1.2 \;\mapsto\; \text{commit } \texttt{a3f7c2d} \;\mapsto\; \text{2026-02-15T10:30:00Z}
$$

The requirement is not a specific format, but **resolvability to a unique temporal position**.
All representations that satisfy this condition are structurally equivalent as $\tau$.

---

### 2.2 Coordinate Structure

Anchoring proceeds as monotonic expansion:

$$
ID \rightarrow \langle ID, L \rangle \rightarrow \langle ID, L, \tau \rangle
$$

Each expansion increases structural determinacy:

| Coordinate                    | Establishes   | Enables                               |
| ----------------------------- | ------------- | ------------------------------------- |
| $ID$                          | Existence     | Identity reference                    |
| $\langle ID, L \rangle$       | Resolvability | Deterministic resolution              |
| $\langle ID, L, \tau \rangle$ | Examinability | Historical query, temporal comparison |

Identity is separated from state.
The same $ID$ at the same $L$ may exist at multiple $\tau$,
and each $\langle ID, L, \tau \rangle$ is a distinct coordinate.

---

### 2.3 Structural Properties

Two anchors are identical if and only if all coordinate components match.

Spatial identity:

$$
\langle ID, L \rangle = \langle ID', L' \rangle \iff ID = ID' \land L = L'
$$

Spatiotemporal identity:

$$
A = A' \iff ID = ID' \land L = L' \land \tau = \tau'
$$

Consequently, the same $ID$ at the same $L$ with different $\tau$ 
yields distinct anchors — this is what makes versioning structurally 
expressible rather than conventionally imposed.

---

### 2.4 Existence and Determinacy

Anchors must be committed at creation time.
If an anchor does not exist prior to analysis, all subsequent analysis becomes speculative.

This condition is non-reconstructible:
multiple histories can produce identical present states.
A temporal index not recorded at creation cannot be uniquely recovered post-hoc.

$$
\neg \exists\, \tau_{\text{created}} \;\Rightarrow\; \neg \exists\, \text{unique reconstruction of } \tau
$$

Pre-analytical anchoring is therefore a necessary condition
for structural examinability — not a best practice,
but a prerequisite.

---

## 3 Relationship

### 3.1 Definition

A **Relationship** is a binary relation over the set of anchors 𝓐:

$$
R \subseteq \mathcal{A} \times \mathcal{A}
$$

An instance of relationship is an ordered pair:

$$
(a_i, a_j) \in R
$$

It expresses **structural adjacency only**.

No embedded semantics are carried at the architectural layer.

Terms such as _implements_, _tests_, _validates_, _depends-on_, or _governs_ are not primitives of the architecture.  
They are interpretations applied externally by domain-specific rules.

The architecture is defined entirely in relational terms.  
No additional structural primitives are required.

---

### 3.2 Validity

A relationship is structurally valid if and only if both participating anchors are resolvable:

$$
(a_i, a_j) \in R_{\text{valid}}
\iff
\operatorname{resolve}(a_i) \neq \varnothing
\land
\operatorname{resolve}(a_j) \neq \varnothing
$$

Validity is therefore determined by coordinate existence, not symbolic declaration.

If

$$
\operatorname{resolve}(a_i) = \varnothing
$$

then no valid relationship involving $a_i$ can exist.

Structural validity is binary.
It is not inferred, repaired, or interpreted.
It is decided by resolvability.

---

### 3.3 Closure and Reachability

Define the transitive closure:

$$
R^{+} = \bigcup_{n=1}^{\infty} R^n
$$

where $R^1 = R$ and $R^{n+1} = \{(a_i, a_k) \mid \exists\, a_j : (a_i, a_j) \in R^n \land (a_j, a_k) \in R\}$.

Traceability is reachability over $R^{+}$.
Impact analysis, dependency chains, and evidence paths
reduce to membership queries in $R^{+}$.

Reachability is determined by declared relations, not temporal ordering.
Given $(a_1, a_2) \in R$, temporal consistency may require:

$$
\tau_1 \le \tau_2
$$

But temporal precedence alone does not generate relation:

$$
\tau_1 < \tau_2 \;\not\Rightarrow\; (a_1, a_2) \in R
$$

Time constrains admissible direction; relation must be declared independently.
If $(a_1, a_2) \in R \land \tau_1 > \tau_2$,
the relation is temporally inconsistent — a structural violation detectable through coordinate comparison, not semantic inspection.

---

### 3.4 Structural Constraints

The relation $R$ is intentionally minimally constrained:

$$
\begin{aligned}
&(a_1, a_2) \in R \land (a_1, a_3) \in R &&\text{is permitted (not a function)} \\
&(a_1, a_2) \in R \nRightarrow (a_2, a_1) \in R &&\text{(not symmetric)} \\
&(a_1, a_2) \in R \land (a_2, a_3) \in R \nRightarrow (a_1, a_3) \in R &&\text{(not transitive)} \\
\end{aligned}
$$

No cardinality, hierarchy, acyclicity, or reflexivity constraints are imposed.

**Semantic neutrality.**
Relationship types such as *implements*, *tests*, *governs*, or *constrains*
are not architectural primitives.
They are application-layer interpretations imposed over structural adjacency.
The relation is invariant; meaning is delegated.

**Temporal independence.**
Temporal precedence does not generate relation:

$$
\tau(a_i) < \tau(a_j) \;\not\Rightarrow\; (a_i, a_j) \in R
$$

Relation must be declared independently.
Application-layer policies may optionally impose
$\tau(a_i) \le \tau(a_j)$ to enforce causal or lifecycle consistency,
but such constraints are governance-layer rules, not structural necessities.

---

## 4. Relational Views

Structural views are derived subrelations of the global relation $R$.

### 4.1 Formal Definition

The global relation is defined as:

$$
R \subseteq A \times A
$$

A structural view is defined by a predicate $C$:

$$
R_{view} = \{ (a_i, a_j) \in R \mid C(a_i, a_j) \}
$$

Thus:

$$
R_{view} \subseteq R
$$

Structural views introduce no new primitives.
They operate over the same anchor set $A$ and relation set $R$.
No structural elements are added or modified.

---

### 4.2 View Categories (Predicate Families)

Different engineering concerns correspond to different predicates.

The following view categories are illustrative, not exhaustive.
Any predicate over anchors or their coordinates may define a valid structural view.

#### 4.2.1 Causal View

Define the causal subrelation of $R$ as:

$$
R_{causal}
=
\{ (a_i, a_j) \in R \mid \tau(a_i) \le \tau(a_j) \}
$$

This is a derived subrelation obtained by restricting $R$ 
under temporal monotonicity.

Causal View does not modify $R$.
It filters $R$ according to a temporal predicate.

Backward references may remain structurally valid in $R$,
but are excluded from causal analysis.

---

#### 6.2.2 Cross-Artifact View

$$
C_{cross}(a_i, a_j)
\iff
L_{a_i} \neq L_{a_j}
$$

This isolates inter-artifact relationships.

---

**Example:**

Given anchors:
$$
A_1 = \langle FR\text{-}091, srs/auth.md, v1.2 \rangle
$$
$$
A_2 = \langle FR\text{-}095, srs/auth.md, v1.2 \rangle
$$

```markdown
---
location: srs/auth.md
version: v1.2
---

### FR-091
Password length must be ≥ 12 characters.

### FR-095
Passwords must be stored using a secure hashing algorithm.
```

$$
A_3 = \langle FUNC\text{-}validate, src/auth.py, v2.1 \rangle
$$

$$
A_4 = \langle TEST\text{-}length\text{-}too\text{-}short, tests/auth.py, v1.1 \rangle
$$
$$
A_5 = \langle TEST\text{-}length\text{-}eligible, tests/auth.py, v1.1 \rangle
$$

```python
# file: tests/auth.py
# version: v1.1

# ID: TEST-length-too-short
# TRACE: STS-091
def test_length_too_short():

# ID: TEST-eligible
# TRACE: STS-091
def test_length_eligible():
```

And relations:
$$
R = \{ (A_1, A_2), (A_1, A_3), (A_3, A_4), (A_4, A_5) \}
$$

Cross-Artifact View filtering:

$(A_1, A_2) \notin C_{cross}$ because both in $srs/auth.md$ ✗

$(A_1, A_3) \in C_{cross}$ because $srs/auth.md \neq src/auth.py$ ✓

$(A_3, A_4) \in C_{cross}$ because $src/auth.py \neq tests/auth.py$ ✓

$(A_4, A_5) \notin C_{cross}$ because both in $tests/auth.py$ ✗

---

**Interpretation:**

Included relations (cross-artifact):
- Requirement → Implementation
- Implementation → Test

Excluded relations (intra-artifact):
- Requirement → Requirement (specification refinement)
- Test → Test (test case dependency)

This view isolates structural dependencies that cross artifact boundaries,
useful for:
- Requirement traceability to implementation
- Cross-repository impact analysis
- Governance boundary verification

---

#### 6.2.3 Identity Consistency View

$$
C_{id}(a_i, a_j)
\iff
ID_{a_i} = ID_{a_j}
$$

This traces evolution of a logical component across
location or time.

ID equality does not imply coordinate equality.

---

**Example:**

Given anchors representing a refactored function:
$$
A_1 = \langle FUNC\text{-}validate, src/auth.py, v1.0 \rangle
$$
$$
A_2 = \langle FUNC\text{-}validate, src/auth.py, v2.0 \rangle
$$
$$
A_3 = \langle FUNC\text{-}validate, src/utils/validation.py, v3.0 \rangle
$$

$$
A_4 = \langle UTILS\text{-}hash, src/hash.py, v1.0 \rangle
$$

```python
# file: src/hash.py
# version: v1.0

# ID: UTILS-hash
# TRACE: FR-095@v1.2, STS-091@v1.0
def hash_password(password: str) -> str:
```

And relations:
$$
R = \{ (A_1, A_2), (A_2, A_3), (A_2, A_4) \}
$$

Identity Consistency View filtering:

$(A_1, A_2) \in C_{id}$ because $FUNC\text{-}validate = FUNC\text{-}validate$ ✓

$(A_2, A_3) \in C_{id}$ because $FUNC\text{-}validate = FUNC\text{-}validate$ ✓

$(A_2, A_4) \notin C_{id}$ because $FUNC\text{-}validate \neq UTILS\text{-}hash$ ✗

---

**Interpretation:**

Included relations trace the evolution of FUNC-validate:
- $A_1 \to A_2$: Same location, version upgrade
- $A_2 \to A_3$: Location changed (refactored to utils/), ID persists

Excluded relation crosses component boundaries:
- $A_2 \to A_4$: Different logical components (validation vs hashing)

This view reveals logical continuity across refactoring,
where the same component migrates between files.

---

**Contrast with Timeline View:**

Timeline View:
$$
Timeline(FUNC\text{-}validate, src/auth.py) = [A_1, A_2]
$$

Timeline excludes $A_3$ because location changed.
Identity Consistency includes $A_3$ because ID persists.

**Relationship to Other Views:**

Identity Consistency View:
- Requires: Same ID only
- Tracks: Logical component across migrations
- Use case: Refactoring traceability

Timeline View:
- Requires: Same ID AND same L
- Tracks: Temporal evolution at fixed location
- Use case: Version history of a file

Both views operate on the same R.
The difference is constraint strictness.

---

### 6.3 Structural Forms (Induced Structures)

Structural forms describe the geometric patterns that emerge
from particular predicate-restricted subrelations.

They do not introduce new primitives.
They characterize the shape of derived subrelations
under specific constraints.

These forms describe recurring geometric patterns observed in predicate-restricted subrelations.
Other forms may arise under different predicates.

#### 6.3.1 Linear View

A Linear View is a total ordered path derived from R.

Formally, a linear chain is a sequence of anchors:

$$
L = [A_1, A_2, \dots, A_n]
$$

such that:

$$
(A_i, A_{i+1}) \in R \quad \text{for all } i \in [1, n-1]
$$

In valid causal chains, temporal ordering typically follows:

$$
\tau_1 < \tau_2 < \dots < \tau_n
$$

This represents sequential structural progression.

**Example:**

Given anchors:
$$
A_{req} = \langle FR\text{-}091, srs/auth.md, v1.2 \rangle
$$

$$
A_{sts} = \langle STS\text{-}091, sts/auth-status.md, v1.0 \rangle
$$

```markdown
<!-- sts/auth-status.md -->
<!-- version: v1.0 -->

### STS-091
Password validation strategy defined.
```

$$
A_{code} = \langle FUNC\text{-}validate, src/auth.py, v2.1 \rangle
$$

$$
A_{log} = \langle TEST\text{-}LOG\text{-}auth, logs/test-auth.log, 2026\text{-}02\text{-}15T10:30:00Z \rangle
$$

```json
// Test Execution Log
// ID: TEST-LOG-auth
// File: logs/test−auth.log
// Timestamp: 2026-02-15T10:30:00Z⟩
{
  "test": "test_password_length",
  "result": "pass"
}
```

And relations:
$$
R = \{ (A_{req}, A_{sts}), (A_{sts}, A_{code}), (A_{code}, A_{log}) \}
$$

Then:
$$
L = [A_{req}, A_{sts}, A_{code}, A_{log}]
$$

forms a linear chain representing the trace from:
- Requirement specification
- Status/design document  
- Implementation
- Test execution log

**Cross-Domain Traceability:**

This chain spans multiple artifact types and uses mixed temporal 
representations (versions for documents/code, timestamp for execution logs).
All are valid temporal indices in the architecture.

This linear chain demonstrates that Anchor Architecture supports 
heterogeneous artifacts without requiring schema alignment. 
Each anchor maintains its own temporal semantics while participating 
in the same structural relation.

---

#### 6.3.2 Net View

The Net View represents the complete relation R without additional constraints.

$$
Net = R
$$

Characteristics:

- Arbitrary branching permitted
- Many-to-many relational structure permitted
- No hierarchy enforced
- No tree constraint imposed
- No cardinality restriction

The Net View is the unfiltered relational substrate.

---

**Example:**

Given anchors:
$$
A_{req} = \langle FR\text{-}091, srs/auth.md, v1.2 \rangle
$$
$$
A_{sts1} = \langle STS\text{-}091, sts/length\text{-}validation.md, v1.0 \rangle
$$
$$
A_{sts2} = \langle STS\text{-}095, sts/hash\text{-}policy.md, v1.0 \rangle
$$
$$
A_{code1} = \langle FUNC\text{-}validate, src/auth.py, v2.1 \rangle
$$
$$
A_{code2} = \langle Utils\text{-}hash, src/utils/hash.py, v1.3 \rangle
$$
$$
A_{log} = \langle TEST\text{-}LOG, logs/test\text{-}auth.log, 2026\text{-}02\text{-}15T14:00:00Z \rangle
$$

And relations:
$$
R = \{ 
  (A_{req}, A_{sts1}), 
  (A_{req}, A_{sts2}), 
  (A_{sts1}, A_{code1}), 
  (A_{sts2}, A_{code2}),
  (A_{code1}, A_{log}),
  (A_{code2}, A_{log})
\}
$$

Relational structure:
```
              FR-091
             /      \
        STS-091    STS-095
         (Length)   (Hash)
            |          |
      FUNC-validate Utils-hash
            \        /
            TEST-LOG
```

This demonstrates:
- **First-level branching**: One requirement decomposes into two design aspects
- **Parallel implementation**: Each design aspect maps to distinct code modules
- **Convergence**: Both implementations contribute to unified test evidence
- **Multi-domain trace**: From specification → design → code → execution

Net View captures the complete structural adjacency space,
enabling full impact propagation and dependency analysis.

**Structural Analysis:**

Forward impact from FR-091:
$$
impact(A_{req}) = \{ A_{sts1}, A_{sts2}, A_{code1}, A_{code2}, A_{log} \}
$$

Backward trace from TEST-LOG:
$$
trace^{-1}(A_{log}) = \{ A_{code1}, A_{code2}, A_{sts1}, A_{sts2}, A_{req} \}
$$

Both queries operate over the same relational foundation.

---

#### 6.3.3 Set View

A **Set View** is a membership-based selection over anchors.

Formally:

$$
S \subseteq \mathcal{A}
$$

Membership is defined as:

$$
a \in S
$$

A Set View introduces **no structural relations**.  
It does not modify R.  
It does not imply adjacency, causality, or reachability.

Set membership is independent of:

$$
(a_i, a_j) \in R
$$

That is:

$$
a_i \in S \land a_j \in S \nRightarrow (a_i, a_j) \in R
$$

A Set View restricts analysis to a subset of anchors.  
It is a projection over $\mathcal{A}$, not a transformation of R.

**Example:**

Define a compliance boundary for authentication subsystem:

$$
S_{\text{auth-boundary}} = \{ 
  a \in \mathcal{A} \mid L_a \in \{srs/auth.md, sts/auth.md, src/auth.py, tests/auth.py\}
\}
$$

Given complete anchor set:
$$
\mathcal{A} = \{
  \langle FR\text{-}091, srs/auth.md, v1.2 \rangle,
  \langle STS\text{-}091, sts/auth.md, v1.0 \rangle,
  \langle FUNC\text{-}validate, src/auth.py, v2.1 \rangle,
  \langle UTILS\text{-}hash, src/hash.py, v1.0 \rangle,
  \langle TEST\text{-}auth, tests/auth.py, v1.1 \rangle,
  \langle LOG\text{-}deploy, logs/deploy.log, 2026\text{-}02\text{-}15T10:00:00Z \rangle
\}
$$

Set View result:

$$
S_{\text{auth-boundary}} = \{
  \langle FR\text{-}091, srs/auth.md, v1.2 \rangle,
  \langle STS\text{-}091, sts/auth.md, v1.0 \rangle,
  \langle FUNC\text{-}validate, src/auth.py, v2.1 \rangle,
  \langle TEST\text{-}auth, tests/auth.py, v1.1 \rangle
\}
$$

Excluded anchors:
- UTILS-hash (src/hash.py) — outside auth boundary
- LOG-deploy (logs/deploy.log) — deployment artifact, not auth subsystem

**Structural Independence:**

Even if relations exist:
$$
R = \{ 
  (FR\text{-}091, FUNC\text{-}validate),
  (FUNC\text{-}validate, UTILS\text{-}hash),
  (UTILS\text{-}hash, TEST\text{-}auth)
\}
$$

The relation $(FUNC\text{-}validate, UTILS\text{-}hash) \in R$ crosses the boundary.

Set View only defines membership:
- FUNC-validate ∈ S_auth-boundary ✓
- UTILS-hash ∉ S_auth-boundary ✗

It does not alter R.  
Boundary-crossing relations remain in R but are excluded from scoped analysis.

**Practical Applications:**

**Compliance auditing:**
"Verify all anchors in auth boundary have required approvals"
→ Query over S_auth-boundary, not entire 𝓐

**Impact analysis with scope:**
"What auth components are affected by FR-091 changes?"
→ Compute impact(FR-091) ∩ S_auth-boundary

**Evidence aggregation:**
"Collect all test logs from regression suite X"
→ Define S_regression-X by test execution context

**Governance boundary verification:**
"Ensure no unauthorized changes to production artifacts"
→ Define S_production and verify all modifications have anchors in S_approved

All realized through membership over 𝓐,  
without introducing new primitives or altering R.

Structural adjacency remains defined exclusively by R.

---

#### 6.3.4 Timeline View

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

Timeline emerges from:

- identical ID
- identical location
- ordered temporal index

No additional primitive is introduced.

**Example**

$$
T(FR\text{-}091) = \{ \langle FR\text{-}091,\; srs/auth.md,\; v1.0 \rangle, 
                      \langle FR\text{-}091,\; srs/auth.md,\; v1.1 \rangle, 
                      \langle FR\text{-}091,\; srs/auth.md,\; v1.2 \rangle \}
$$

```markdown
---
location: srs/auth.md
version: v1.0
---

### FR-091
Password length must be ≥ 4 characters.
```

```markdown
---
location: srs/auth.md
version: v1.1
---

### FR-091
Password length must be ≥ 8 characters.
```

```markdown
---
location: srs/auth.md
version: v1.2
---

### FR-091
Password length must be ≥ 12 characters.
```

---

### 6.4 Structural Consistency

All views are derived from the same relational foundation:

$$
(𝓐, R) \quad \text{where} \quad R ⊆ 𝓐 × 𝓐
$$

They differ only by projection or constraint:

---

#### 6.4.1 Primary Structural Views

| View     | Projection Base | Constraint                    | Analytical Value       | Example Application       |
| -------- | --------------- | ----------------------------- | ---------------------- | ------------------------- |
| Linear   | R               | Total temporal order          | Causal Path            | Step-by-step verification |
| Net      | R               | No constraint                 | Impact Propagation     | Blast radius analysis     |
| Set      | 𝓐               | Membership predicate          | Governance Boundary    | Compliance scope          |
| Timeline | R               | Same (ID, L) + temporal order | Evolutionary Integrity | Version history           |

---

#### 6.4.2 Derived Relational Views

These are constraint-based subrelations of R:

| View                 | Constraint Formula        | Purpose                |
| -------------------- | ------------------------- | ---------------------- |
| Causal               | $\tau(a_i) \le \tau(a_j)$ | Temporal causality     |
| Cross-Artifact       | $L_{a_i} \neq L_{a_j}$    | Inter-artifact tracing |
| Identity Consistency | $ID_{a_i} = ID_{a_j}$     | Component evolution    |

---

#### 6.4.3 Invariance Principle

**All views operate on the same geometric substrate:**

$$
(𝓐, R)
$$

**Differences are purely operational:**

- **Linear**: Ordered sequence extraction
- **Net**: Complete relation
- **Set**: Membership selection over 𝓐
- **Timeline**: Same-location temporal sequence
- **Causal**: Temporal filter
- **Cross-Artifact**: Spatial filter  
- **Identity Consistency**: Identity filter

**Three fundamental principles:**

1. **Views are projections*-
   No new primitives are introduced

2. **Geometry is invariant*-
   R and 𝓐 remain unchanged

3. **Interpretation is delegated*-
   Views provide lenses, not semantics

All structural analysis reduces to queries over:
$$
(𝓐, R)
$$

---

## 7. Structural Operations

Structural operations are **queries over relation and coordinate space**.

They introduce no new primitives.

All operations derive exclusively from:

- Anchor set $\mathcal{A}$
- Relation $R \subseteq \mathcal{A} \times \mathcal{A}$

**Transitive Closure**

Let $R^+$ denote the transitive closure of R:

$$
R^+ = \bigcup_{n=1}^{\infty} R^n
$$

where:
$$
R^1 = R
$$
$$
R^{n+1} = R^n \circ R = \{ (a, c) \mid \exists b: (a,b) \in R^n \land (b,c) \in R \}
$$

Equivalently, $(a_i, a_j) \in R^+$ if and only if  
there exists a relational path from $a_i$ to $a_j$.

---

All structural analysis reduces to:

- **Traversal** over R or R⁺
- **Projection** over 𝓐
- **Content resolution** via coordinate

No semantic inference is required at this layer.

---

### 7.1 Base Structural Operations

The architecture defines two structural primitives:
- Anchor (coordinate)
- Relationship (binary relation)

At the operational layer, two base capabilities emerge from these primitives:
- Relation Traversal
- Content Resolution

All higher-level operations compose these two capabilities.

---

#### 7.1.1 Relation Traversal

Traversal computes structural reachability from an anchor.

Given anchor $a$, the image set under R⁺ is:

$$
image_{R^+}(a) = \{ b \in \mathcal{A} \mid (a,b) \in R^+ \}
$$

This expresses structural propagation without semantic interpretation.

Traversal does not assume:
- Hierarchy
- Tree structure
- Unique parent
- Semantic meaning

It is pure relational expansion.

---

#### 7.1.2 Content Resolution

Resolution retrieves content from a spatiotemporal coordinate.

Given:

$$
a = \langle ID, L, \tau \rangle
$$

$$
resolve(a) \rightarrow Content
$$

where Content represents the artifact state at the specified coordinate.

This may be:
- Text (documents, code)
- Binary data (compiled artifacts, images)
- Metadata (structural descriptors)

The architecture does not constrain content type.

---

**Resolution Determinism**

Resolution is deterministic:
- Same coordinate → Same content
- Different $\tau$ at same $(ID, L)$ → Different content

**Resolution Failure**

If $resolve(a) = \varnothing$:

Structural examinability at that coordinate cannot be guaranteed.

Resolution failure does not invalidate the anchor definition,  
but prevents structural verification at that coordinate.

This may occur when:
- Artifact was deleted
- Version control history is incomplete  
- Temporal index references non-existent state

---

### 7.2 Derived Operations (Application Layer)

The following operations are projections over the base structural capabilities.

They are named usage patterns — not new primitives.

They do not extend the architecture.  
They compose existing structural elements:

- anchor membership over  $A$ 
- relation traversal over  $R$ 
- reachability over  $R^{+}$ 
- coordinate resolution via `resolve()`

The operations listed below represent **common application patterns**,  
but they are **not exhaustive**.

Any application-layer behavior reducible to:

- selection over  $A$ ,
- traversal over  $R$ ,
- closure over  $R^{+}$ , or
- coordinate comparison,

is admissible within the architecture.

The architecture imposes no restriction on higher-level operational naming.  
It defines only structural capabilities.

---

#### 7.2.1 trace()

**Definition**

trace is **goal-oriented path traversal with structural preservation**.

Given:
- Source anchor $a$
- Target predicate $P: \mathcal{A} \to \{\text{true}, \text{false}\}$

$$
trace(a, P) = \{ [a_0, a_1, \dots, a_n] \mid a_0 = a \land P(a_n) \land \forall i: (a_i, a_{i+1}) \in R \}
$$

where each result is an ordered sequence of anchors forming a path in R.

**Properties**

- **Requires termination condition**: Predicate $P$ defines target anchors
- **Returns structural paths**: Complete ordered sequences, not just endpoints
- **Empty if unreachable**: If no reachable anchor satisfies $P$, result is $\emptyset$
- **Preserves ordering**: Each path maintains relational sequence

trace answers:

> "Through what structural chain does $a$ reach a target satisfying $P$?"

**Example:**

Given anchors:
$$
A_{req} = \langle FR\text{-}091, srs/auth.md, v1.2 \rangle
$$
$$
A_{code1} = \langle FUNC\text{-}validate, src/auth.py, v2.1 \rangle
$$
$$
A_{code2} = \langle UTILS\text{-}hash, src/hash.py, v1.0 \rangle
$$
$$
A_{test} = \langle TEST\text{-}auth, tests/auth.py, v1.1 \rangle
$$

And relations:
$$
R = \{ (A_{req}, A_{code1}), 
       (A_{req}, A_{code2}), 
       (A_{code1}, A_{test}), 
       (A_{code2}, A_{test}) 
    \}
$$

Define target predicate:
$$
P_{test}(x) := ID_x \in \{\text{TEST-*}\}
$$

Then:
$$
trace(A_{req}, P_{test}) = \{
  [A_{req}, A_{code1}, A_{test}],
  [A_{req}, A_{code2}, A_{test}]
\}
$$

**Interpretation:**

Two distinct structural paths exist from requirement to test:
- Via FUNC-validate
- Via UTILS-hash

trace reconstructs the structural chains,  
not the semantic meaning of "implements" or "tests".

If test fails, trace reveals which implementation paths may be responsible.

---

#### 7.2.2 impact()

**Definition**

impact returns the set of anchors reachable from a given anchor under transitive closure.

$$
impact(a) = \{ b \in \mathcal{A} \mid (a, b) \in R^{+} \}
$$

Equivalently:
$$
impact(a) = image_{R^{+}}(a)
$$

It is a reachability projection over R⁺.

**Properties**

- Derived from transitive closure R⁺
- Returns a **set**, not paths
- Does not preserve traversal structure
- Order-independent
- May be restricted by external predicate (e.g., Set View boundary)

impact answers:

> "If anchor $a$ changes, which anchors are structurally downstream?"

**Example:**

Given anchors:
$$
A_{req} = \langle FR\text{-}091, srs/auth.md, v1.2 \rangle
$$
$$
A_{code1} = \langle FUNC\text{-}validate, src/auth.py, v2.1 \rangle
$$
$$
A_{code2} = \langle UTILS\text{-}hash, src/hash.py, v1.0 \rangle
$$
$$
A_{test} = \langle TEST\text{-}auth, tests/auth.py, v1.1 \rangle
$$

And relations:

$$
R = \{ (A_{req}, A_{code1}), 
       (A_{req}, A_{code2}), 
       (A_{code1}, A_{test}), 
       (A_{code2}, A_{test}) 
    \}
$$

Then:

$$
impact(A_{req}) = \{ A_{code1}, A_{code2}, A_{test} \}
$$

**Interpretation:**

If FR-091 changes, three anchors are structurally downstream:
- Two implementations (FUNC-validate, UTILS-hash)
- One test (TEST-auth)

impact computes the blast radius without revealing causality.

To understand *how* the impact propagates, use trace().

**Distinction from trace()**

Both operations rely on traversal over R, but differ structurally and analytically:

| Aspect            | trace(a, P)                    | impact(a)                    |
| ----------------- | ------------------------------ | ---------------------------- |
| **Return Type*-   | Paths (ordered sequences)      | Anchor set (unordered)       |
| **Structure*-     | Preserves relational causality | Discards path information    |
| **Query*-         | "How does a reach targets?"    | "What is affected by a?"     |
| **Use Case*-      | Root cause analysis            | Blast radius estimation      |
| **Predicate*-     | Required (target filter)       | Optional (scope filter)      |
| **Computational** | Path enumeration               | Reachability set computation |

**Scoped Impact Analysis**

impact() may be combined with Set View for governance-bounded analysis:

$$
impact(a) \cap S_{boundary}
$$

Example:
$$
impact(A_{req}) \cap S_{auth\text{-}subsystem} = \{ A_{code1}, A_{test} \}
$$

This excludes UTILS-hash if it falls outside the auth subsystem boundary.

**Implementation Note:**

impact() is more efficient than trace() when:
- Only the affected anchor set is needed
- Path causality is irrelevant
- Large relational spaces require optimization

Both share the same relational substrate (𝓐, R)  
but serve different analytical roles.

---

#### 7.2.3 diff()

**Definition**

diff compares the resolved content of two anchors.

Given:

$$
a_1, a_2 \in \mathcal{A}
$$

Let a content-difference operator be defined as:

$$
\Delta : Content \times Content \rightarrow DiffResult
$$

where $DiffResult$ represents the structural difference between two content states.

Then:

$$
diff(a_1, a_2) = \Delta\big(resolve(a_1),\; resolve(a_2)\big)
$$

diff operates at the **content level**, not at the structural level.

**Precondition**

$$
resolve(a_1) \neq \varnothing
\;\land\;
resolve(a_2) \neq \varnothing
$$

If resolution fails, content comparison cannot be performed.

**Properties**

- **No coordinate constraints**: 
  - No requirement of identity equality  
  - No requirement of location equality  
  - No requirement of temporal adjacency  

- **Non-relational**:
  - Does not modify R  
  - Does not imply structural connection
  - Does not assert version-control semantics  

The two anchors may:
- Share the same ID but differ in temporal index (version comparison)
- Share the same location but differ in ID (different components in same file)
- Differ in all coordinates (arbitrary comparison)

diff compares resolved states only.

**Difference Representation**

The architecture does not prescribe diff format.

$DiffResult$ may be:
- **Text-level**: Line additions/deletions (unified diff, context diff)
- **Structural**: AST node changes, schema modifications
- **Binary**: Byte-level differences
- **Semantic**: Constraint changes, policy updates

Interpretation belongs to the application layer.

**Example:**

Given anchors representing requirement evolution:
$$
a_{v1.1} = \langle FR\text{-}091, srs/auth.md, v1.1 \rangle
$$
$$
a_{v1.2} = \langle FR\text{-}091, srs/auth.md, v1.2 \rangle
$$

Content resolution:
$$
resolve(a_{v1.1}) = \text{"Password length must be } \ge \text{ 8 characters."}
$$
$$
resolve(a_{v1.2}) = \text{"Password length must be } \ge \text{ 12 characters."}
$$

Then:
$$
diff(a_{v1.1}, a_{v1.2}) = \Delta(resolve(a_{v1.1}), resolve(a_{v1.2}))
$$

Example diff result (non-normative):

```diff
- Password length must be ≥ 8 characters.
+ Password length must be ≥ 12 characters.
```

**Interpretation:**

The operation detects a constraint strengthening (10 → 12).

However, interpreting this as:
- Requirement refinement
- Policy tightening  
- Breaking change

belongs to the application layer.

diff provides structural difference.  
Semantic meaning is delegated.

**Analytical Role**

diff answers:

> "How does one committed anchor state differ from another?"

It is a coordinate-based content comparison.  
It does not assert structural relation, causality, or semantic meaning.

---

#### 7.2.4 version()

**Definition**

version projects anchors sharing identity and location across temporal indices.

Given fixed coordinates:
$$
ID^*, L^*
$$

Define:
$$
version(ID^*, L^*) =
\{ a \in \mathcal{A} \mid ID_a = ID^* \land L_a = L^* \}
$$

where $ID_a$ and $L_a$ denote the identity and location components of anchor $a$.

version returns the subset of anchors that share identity and spatial coordinate.

**Optional Temporal Ordering**

The architecture does not mandate global temporal ordering.

However, when temporal comparability is available within $(ID^*, L^*)$:

$$
\tau_1 < \tau_2 < \dots < \tau_n
$$

the projection may be represented as an ordered sequence:

$$
version(ID^*, L^*) = [
\langle ID^*, L^*, \tau_1 \rangle,
\langle ID^*, L^*, \tau_2 \rangle,
\dots,
\langle ID^*, L^*, \tau_n \rangle
]
$$

Ordering semantics are delegated to the underlying version-control  
or temporal indexing system.

**Example:**

Given anchors:
$$
\mathcal{A} = \{
  \langle FR\text{-}091, srs/auth.md, v1.0 \rangle,
  \langle FR\text{-}091, srs/auth.md, v1.1 \rangle,
  \langle FR\text{-}091, srs/auth.md, v1.2 \rangle,
  \langle FR\text{-}095, srs/auth.md, v1.2 \rangle,
  \langle FR\text{-}091, sts/auth.md, v2.0 \rangle
\}
$$

Then:
$$
version(FR\text{-}091, srs/auth.md) = [
  \langle FR\text{-}091, srs/auth.md, v1.0 \rangle,
  \langle FR\text{-}091, srs/auth.md, v1.1 \rangle,
  \langle FR\text{-}091, srs/auth.md, v1.2 \rangle
]
$$

Note:
- FR-095 is excluded (different ID)
- FR-091 @ sts/auth.md is excluded (different location)

With content resolution (non-normative):
```
v1.0: "Password length must be ≥ 8 characters."
v1.1: "Password length must be ≥ 10 characters."  
v1.2: "Password length must be ≥ 12 characters."
```

**Interpretation**

version answers:

> "What anchor states share the same identity and location across time?"

It returns structural states organized by temporal coordinate.  
It does not compute content differences.

**Structural Role**

version() enables:
- **Change history**: Track evolution of a component at fixed location
- **Temporal navigation**: Select specific version for analysis
- **Diff preparation**: Identify anchors to compare
- **Rollback analysis**: Locate previous states

All without requiring structural relations.

---

### 7.3 Structural Summary

All structural analysis reduces to two base capabilities:

- **Relation traversal** over R and R⁺
- **Content resolution** via coordinate

Derived operations are projections over $(𝓐, R)$:

| Operation | Operates On | Structural Basis    | Return Structure     | Core Question                           |
| --------- | ----------- | ------------------- | -------------------- | --------------------------------------- |
| trace()   | R⁺          | Path enumeration    | Set of ordered paths | Through what chain does this propagate? |
| impact()  | R⁺          | Reachability set    | Anchor set           | What is downstream?                     |
| diff()    | 𝓐           | Content resolution  | Content difference   | What changed between two states?        |
| version() | 𝓐           | Identity + Location | Ordered anchor list  | What is the temporal sequence?          |

**Operational Characteristics:**

**trace() and impact()**
- Both traverse R⁺
- trace() preserves paths
- impact() discards path structure
- Complementary views of structural propagation

**diff() and version()**
- Both operate on resolved content
- version() organizes by coordinate
- diff() compares content
- Sequential: version() → diff()

**Architectural Properties:**

Operations do not introduce semantics.  
They operate on coordinates and relations.

**No operation assumes:**
- Semantic labels (implements, tests, validates)
- Hierarchical structure (tree, parent-child)
- Domain knowledge (requirements, code, tests)

**All operations are:**
- Domain-agnostic
- Tool-independent
- Model-independent

Meaning emerges only at application layer.

**Composability:**

Operations compose to answer complex queries:

**"Which tests are affected by requirement changes?"**
$$
impact(A_{req}) \cap \{ a \in \mathcal{A} \mid ID_a \in \text{TEST-*} \}
$$

**"What changed in the latest version of this component?"**
$$
\text{Let } [a_1, \dots, a_n] = version(ID^*, L^*) \\
diff(a_{n-1}, a_n)
$$

**"Trace how a specific version reached test failures"**
$$
\text{Let } a_v = \langle ID, L, v_{specific} \rangle \\
trace(a_v, \lambda x. ID_x \in \text{TEST-*} \land failed(x))
$$

All composed from the same two base capabilities.

**Invariance Principle:**

The relational substrate $(𝓐, R)$ is invariant.  
Operations provide lenses, not transformations.

Traceability is not documentation.  
It is coordinate geometry.

---

## 8. Comprehensive Example

This section demonstrates Anchor Architecture through a realistic failure scenario.

The goal is not to demonstrate functionality,  
but to demonstrate structural examinability.

---

### 8.1 Scenario

System: Authentication Module

Evolution:

1. Initial requirement: Password ≥ 4
2. Strengthened: Password ≥ 8
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
---
location: srs/auth.md
version: v1.0
---

### FR-091
Password length must be ≥ 4 characters.
```

```markdown
---
location: srs/auth.md
version: v1.1
---

### FR-091
Password length must be ≥ 8 characters.
```

```markdown
---
location: srs/auth.md
version: v1.2
---

### FR-091
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
# file: src/auth/password.py
# version: 1.4

# ID: FUNC-validate-password
# TRACE: FR-091@v1.2, STS-091@v1.0
def validate_password(password: str) -> bool:
```

OAuth fallback:

```python
# file: src/auth/oauth.py
# version: 2.1

# ID: FUNC-oauth-fallback
# TRACE: FR-091@v1.1, STS-091@v1.0
def oauth_password_policy(user: object) -> bool:
```

Login entry point:

```python
# file: src/auth/login.py
# version: 3.0

# ID: FUNC-login
# TRACE: FUNC-validate-password@v1.2, FUNC-oauth-fallback@v2.1

def login(user, pwd):
```

Test anchor:

```python
# file: tests/auth.py
# version: v1.1

# ID: TEST-length-too-short
# TRACE: STS-091
def test_length_too_short():

# ID: TEST-eligible
# TRACE: STS-091
def test_length_eligible():
```

Formal anchors:

$$
A_{c1} = \langle FUNC\text{-}validate\text{-}password,\; src/auth/password.py,\; 1.4 \rangle
$$
 
$$
A_{c2} = \langle FUNC\text{-}oauth\text{-}fallback,\; src/auth/oauth.py,\; 2.1 \rangle
$$
 
$$
A_{c3} = \langle FUNC\text{-}login,\; src/auth/login.py,\; 3.0 \rangle
$$
 
$$
A_t = \langle TEST\text{-}length\text{-}too\text{-}short,\; tests/test_auth.py,\; 1.1 \rangle
$$

$$
A_t = \langle TEST\text{-}length\text{-}eligible,\; tests/test_auth.py,\; 1.1 \rangle
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

Define target predicate:

$$
P_{target}(x) := (x = A_t)
$$

Targeted traversal:

$$
trace(A_{r3}, P_{target})
$$

Result:

$$
\{
  [A_{r3}, A_{c1}, A_{c3}, A_t],
  [A_{r3}, A_{c2}, A_{c3}, A_t]
\}
$$

**Implementation Snippet (Illustrative)**

```markdown
### FR-091
Password length must be ≥ 12 characters.
````

```python
# ID: FUNC-validate-password
# TRACE: FR-091
def validate_password(pwd: str) -> bool:
    return len(pwd) >= 12
```

```python
# ID: FUNC-oauth-fallback
# TRACE: FR-091
def oauth_password_policy(pwd: str) -> bool:
    if external_provider():
        return True
    return len(pwd) >= 12
```

```python
# ID: FUNC-login
# TRACE: FUNC-validate-password, FUNC-oauth-fallback
def login(user, pwd):
    if not oauth_password_policy(pwd):
        raise ValueError("Invalid password")
```

```python
# ID: TEST-login-length
# TRACE: FUNC-login
def test_length_too_short():
    assert login("u", "short")  # expected failure
```

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
diff(A_{r2}, A_{r3}) = \Delta(resolve(A_{r2}), resolve(A_{r3}))
$$

where $\Delta$ is a content-difference operator.

**Implementation Snippet (Illustrative)**

Version v1.1:

```markdown
<!-- (FR-091, srs/auth.md, v1.1) -->
### FR-091
Password length must be ≥ 8 characters.
```

Version v1.2:

```markdown
<!-- (FR-091, srs/auth.md, v1.2) -->
### FR-091
Password length must be ≥ 12 characters.
```

Structural diff result (non-normative):

```diff
  ### FR-091
- Password length must be ≥ 8 characters.
+ Password length must be ≥ 12 characters.
```

Structural output:

Change in minimum length from 8 → 12

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

---

**Implementation Snippet (Illustrative)**

Requirement anchor:
```markdown
<!-- (FR-091, srs/auth.md, v1.2) -->
### FR-091
Password length must be ≥ 12 characters.
```

Affected artifacts (impact set):

1. **Password Validator** (A_c1):
```python
# ID: FUNC-validate-password
# TRACE: FR-091
def validate_password(pwd: str) -> bool:
    return len(pwd) >= 12  # ← constraint from v1.2
```

2. **OAuth Fallback** (A_c2):
```python
# ID: FUNC-oauth-fallback
# TRACE: FR-091
def oauth_password_policy(pwd: str) -> bool:
    if external_provider():
        return True
    return len(pwd) >= 12  # ← constraint from v1.2
```

3. **Login Function** (A_c3):
```python
# ID: FUNC-login
# TRACE: FUNC-validate-password, FUNC-oauth-fallback
def login(user, pwd):
    if not oauth_password_policy(pwd):
        raise ValueError("Invalid password")
```

4. **Test** (A_t):
```python
# ID: TEST-auth
# TRACE: FUNC-login
def test_length_too_short():
    assert login("u", "short")  # fails due to v1.2
```

---

**Visual Impact Propagation:**
```
FR-091 (v1.2)
    ↓
    ├─→ FUNC-validate-password
    │        ↓
    └─→ FUNC-oauth-fallback
             ↓
        FUNC-login
             ↓
        TEST-auth
```

All four downstream anchors are structurally reachable from the requirement change.

---

**Interpretation:**

Requirement v1.2 influences:
- **2 implementations** (password validator, OAuth fallback)
- **1 integration point** (login function)
- **1 test** (authentication test)

impact returns a **set**, not paths.

Contrast with trace():
- trace() reveals **how** the impact propagates (two distinct paths)
- impact() reveals **what** is affected (four anchors)

---

**Engineering Use:**

**Change Propagation Analysis**
- Before modifying FR-091, run impact(A_r3)
- Identify all affected code modules
- Plan coordinated updates

**Blast Radius Estimation**
- If FR-091 has a defect, four artifacts need review
- Prioritize testing based on criticality

**Inference Creep Detection**
- Verify all four anchors explicitly reference FR-091
- Detect implicit dependencies not in R

**Scope Validation**
- Combine with Set View for bounded analysis:
  $$impact(A_{r3}) \cap S_{auth\text{-}subsystem}$$
- Exclude artifacts outside governance boundary

In this investigation:
- impact() immediately reveals all potentially affected code
- No need to manually trace through call chains
- Structural reachability is deterministic

---

#### 8.4.4 version()

**Purpose**

version() answers:

> What is the structural evolution of this requirement?

$$
version(FR\text{-}091, srs/auth.md)
$$

Result:

$$
[
  \langle FR\text{-}091, srs/auth.md, v1.0 \rangle,
  \langle FR\text{-}091, srs/auth.md, v1.1 \rangle,
  \langle FR\text{-}091, srs/auth.md, v1.2 \rangle
]
$$

Ordered by temporal index.

**Implementation Snippet (Illustrative)**

Evolution timeline:

**Version 1.0** (Initial):

```markdown
---
location: srs/auth.md
version: v1.0
---
### FR-091
Password length must be ≥ 4 characters.
```

**Version 1.1** (First Strengthening):

```markdown
---
location: srs/auth.md
version: v1.1
---
### FR-091
Password length must be ≥ 8 characters.
```

**Version 1.2** (Second Strengthening):

```markdown
---
location: srs/auth.md
version: v1.2
---
### FR-091
Password length must be ≥ 12 characters.
```

**Temporal Evolution:**

```
Timeline of FR-091 @ srs/auth.md

v1.0 ────────→ v1.1 ────────→ v1.2
(≥ 4 chars)   (≥ 8 chars)   (≥ 12 chars)
   │              │              │
   │              │              └─→ Current (failure point)
   │              └─→ Intermediate
   └─→ Initial
```

**Interpretation:**

version() returns the temporal sequence of a requirement at fixed location.

Each version represents a distinct structural state.

To understand what changed between versions, use diff():
$$
diff(A_{r1}, A_{r2}), diff(A_{r2}, A_{r3})
$$

**Engineering Use:**

- Identify all historical states of a component
- Select specific version for analysis
- Support rollback decisions
- Provide temporal context for changes

version() organizes anchors by temporal coordinate.  
It does not determine causality or diagnose failures.

---

### 8.5 Investigative Flow

Given login failure reported after deployment, we apply the four structural operations sequentially.

#### 8.5.1 Step

**Step 1: Identify Structural Paths** — trace()

$$
trace(A_{r3}, P_{test}) = \{
  [A_{r3}, A_{c1}, A_{c3}, A_t],
  [A_{r3}, A_{c2}, A_{c3}, A_t]
\}
$$

**Finding:**
- Requirement v1.2 propagates through two distinct paths
- Both paths converge at login function
- Login connects to failing test

**Step 2: Analyze Content Change** — diff()

$$
diff(A_{r2}, A_{r3}) = \Delta(resolve(A_{r2}), resolve(A_{r3}))
$$

Result:
```diff
- Password length must be ≥ 8 characters.
+ Password length must be ≥ 12 characters.
```

**Finding:**
- Constraint tightened from 8 → 12 characters
- This is a breaking change
- Previously valid passwords (8-11 chars) now invalid

**Step 3: Determine Blast Radius** — impact()

$$
impact(A_{r3}) = \{ A_{c1}, A_{c2}, A_{c3}, A_t \}
$$

**Finding:**
- Four artifacts structurally downstream
- All implementations reference FR-091 v1.2
- Both password validator and OAuth fallback affected

**Step 4: Correlate with Timeline** — version()

$$
version(FR\text{-}091, srs/auth.md) = [A_{r1}, A_{r2}, A_{r3}]
$$

Timeline:
```
v1.0 (4 chars) → v1.1 (8 chars) → v1.2 (12 chars)
```

Cross-reference with deployment log:
- **Deployment timestamp**: 2026-02-15T09:00:00Z
- **Deployed version**: FR-091 v1.2
- **Failure reports started**: 2026-02-15T10:30:00Z (90 minutes after deployment)

---

#### 8.5.2 Synthesis

Four operations converge on the same structural coordinate:

| Evidence           | Source           | Finding                                   |
| ------------------ | ---------------- | ----------------------------------------- |
| Propagation paths  | trace()          | v1.2 → code → test                        |
| Content change     | diff()           | 8 → 12 chars (breaking)                   |
| Affected artifacts | impact()         | 4 downstream anchors                      |
| Temporal alignment | version() + logs | Deployed v1.2 at T+0, failures at T+90min |

**Conclusion:**

Login failures are structurally attributable to FR-091 v1.2:
1. Constraint strengthening (8 → 12) is a breaking change
2. Change propagated to all authentication paths
3. Deployment and failure timeline align
4. No other structural changes in same window

**No semantic guessing required.**  
The diagnosis emerges from coordinate geometry over (𝓐, R).

**Step 5: Validate Structural Integrity** (Optional)

During investigation, engineer discovers a reference in legacy code:
```python
# TRACE: FR-999
# Legacy authentication bypass
```

Structural validation:
$$
resolve(\langle FR\text{-}999, srs/auth.md, * \rangle) = \varnothing
$$

No anchor exists → relationship is structurally void.

This demonstrates **Ghost Reference detection**:
- AI or developer may generate symbolic references
- Without pre-analytical anchoring, references cannot be validated
- Structural examinability fails at that coordinate

---

### 8.6 Ghost Reference Detection

During the investigation in Section 8.5, structural validation revealed a secondary issue.

#### 8.6.1 Discovery

While examining authentication code, engineer finds a reference in legacy module:
```python
# file: src/auth/legacy.py
# version: 0.8 (deprecated)

# ID: FUNC-legacy-auth
# TRACE: FR-999
def legacy_authentication(user):
    # Bypass for admin accounts
    if user.is_admin:
        return True
```

---

#### 8.6.2 Structural Validation

Query for referenced anchor:
$$
resolve(\langle FR\text{-}999, srs/auth.md, * \rangle)
$$

Result:
$$
\varnothing
$$

No anchor FR-999 exists in any version of srs/auth.md.

Therefore:
$$
(A_{ghost}, A_{legacy}) \notin R_{valid}
$$

The reference is **structurally void**.

---

#### 8.6.3 Analysis

This demonstrates a fundamental failure mode:  
**Symbolic references without structural anchors.**

**Possible Origins:**

1. **AI Hallucination:**
   - LLM infers requirement from context
   - Generates plausible-looking identifier FR-999
   - Reference appears valid but lacks structural foundation

2. **Human Error:**
   - Developer invents requirement placeholder
   - Forgets to create actual anchor
   - Reference survives code review

3. **Documentation Drift:**
   - Original requirement FR-999 existed
   - Was deleted or renumbered
   - Code reference not updated

---

#### 8.6.4 Structural Consequence

Without anchor:
- Cannot trace requirement origin
- Cannot validate policy alignment
- Cannot assess change impact
- Cannot perform governance audit

The relationship exists **syntactically** but not **structurally**.

---

### 8.7 Synthesis: Traceability as Solvable Geometry

This comprehensive example demonstrates the complete operational mechanics  
of Anchor Architecture applied to a realistic failure scenario.

#### 8.7.1 What Was Demonstrated

**Primitives:**

- Anchors as spatiotemporal coordinates: $\langle ID, L, \tau \rangle$
- Relationships as binary relation: $R \subseteq \mathcal{A} \times \mathcal{A}$

**Structural Views:**

- Net View: Complete relational structure
- Timeline View: Temporal evolution of FR-091

**Operations:**

- trace(A, P) → Path discovery through R⁺
- impact(A) → Reachable anchor set
- diff(A₁, A₂) → Content comparison via resolution
- version(ID, L) → Temporal sequence projection

**Validation:**

- Ghost Reference detection through coordinate resolution
- Structural integrity verification without semantic interpretation

---

#### 8.7.2 What Was Not Required

**No Graph-Theoretic Concepts:**

- No vertices, edges, or graph traversal terminology
- Pure relational operations over ordered pairs

**No Semantic Inference:**

- No interpretation of "implements", "tests", "validates"
- Pure coordinate and relation operations

**No Tool-Specific Metadata:**

- No Git-specific assumptions
- No JIRA/Confluence integration
- No schema dependencies

**No AI Model Introspection:**

- No prompt inspection
- No reasoning chain analysis
- No model confidence scores

---

#### 8.7.3 What Was Sufficient

$$
(\mathcal{A}, R)
$$

Two primitives.  
Four operations.  
Pure coordinate geometry.

**The Central Claim Validated:**

**Claim (from Section 1):**

> Traceability failures are not caused by opaque reasoning.  
> They are caused by missing structural anchors.

**Evidence (from this example):Login failure diagnosis:**

- Not discovered through heuristic debugging
- Derived through coordinate operations over (𝓐, R)
- Root cause: FR-091 v1.2 constraint change (8 → 12 chars)

Both failures were **geometrically determined**, not interpretively inferred.

---

#### 8.7.4 Architectural Implications

**Examinability emerges from structure:**

- If anchors exist at creation → relationships are examinable
- If anchors are missing → relationships collapse geometrically

**Determinism replaces heuristics:**

- Traditional: "Does this code implement that requirement?" (semantic guess)
- Anchor Architecture: "Does (req, code) ∈ R?" (coordinate query)

**Governance becomes verification:**

- Traditional: "Did the developer document the rationale?" (hope)
- Anchor Architecture: "Does resolve(a) ≠ ∅?" (proof)

---

#### 8.7.5 From Abstract to Proof

**Abstract stated:**

> Traceability is not documentation. It is coordinate geometry.

**This example proved:**

- Failure diagnosis reduced to path enumeration (trace)
- Impact analysis reduced to reachability (impact)
- Change detection reduced to content comparison (diff)
- History reconstruction reduced to temporal projection (version)
- Integrity validation reduced to coordinate resolution (resolve)

All operations over the same geometric substrate: (𝓐, R)

**Conclusion:**

The failure was not *discovered* through expert judgment.  
It was *derived* through coordinate operations.

The invalid reference was not *suspected* through code smell.  
It was *proven void* through geometric resolution.

**Traceability is not documentation.**  
**It is coordinate geometry over declared relations.**

The architecture requires minimal primitives  
but provides deterministic examinability.

---

## 9. Related Work

Anchor Architecture positions itself as a **minimal structural foundation** for traceability, distinct from existing provenance, attestation, and traceability approaches. We categorize related work into four clusters and highlight key differences.

### 9.1 Provenance Models (Activity-Centric)

The W3C PROV-DM framework formalizes provenance through entities, activities, and agents connected by derivation relations. It excels at recording "what happened" after execution.

**Key Difference**  

PROV-DM is post-hoc and activity-centric — it assumes entities are already identifiable and focuses on causal history. Anchor Architecture operates at a more fundamental layer: defining pre-analytical coordinates (ID, L, τ) before any provenance relation can be meaningfully asserted. Without such coordinates, PROV-DM's entities remain ambiguous in AI-generated artifacts.

---

### 9.2 Version Control and Artifact Tracking

Version control systems (Git, Mercurial) track file states through commits and diffs, while tools like DVC extend this to data artifacts.

**Key Difference**  

These systems track temporal changes at the file level but do not generalize to arbitrary structural entities or enforce pre-analytical binding. Anchor Architecture abstracts beyond files: any entity (requirement, function, test, log) receives a spatiotemporal coordinate, enabling cross-artifact traceability without file-centric assumptions.

---

### 9.3 Manual Traceability Matrices and Tools

Classical requirements traceability (e.g., traceability matrices in DOORS, Polarion, Jama) links requirements to design, code, and tests through manual annotations or tooling conventions.

**Key Difference**  

These approaches collapse under scale due to annotation overhead and implicit assumptions about artifact identity. Anchor Architecture eliminates the annotation tax: traceability emerges implicitly from structural relations over pre-bound coordinates, not from manual links.

---

### 9.4 Supply Chain Attestation and Build Provenance

Frameworks like SLSA and in-toto focus on build integrity, artifact provenance, and secure pipelines through attestations and cryptographic hashes.

**Key Difference**  

SLSA/in-toto assume well-defined build steps and artifact boundaries. Anchor Architecture generalizes beyond builds: it defines structural examinability for any artifact type (spec, code, log, governance) through coordinate binding, independent of pipeline or security objectives.

---

### 9.5 AI-Generated Code Traceability and Agentic SE

Recent work on LLM-based agents in software engineering (e.g., surveys on agent drift, behavioral degradation, and code generation) highlights traceability collapse, ghost intent, and inference creep in AI-assisted workflows.

**Key Difference**  

Most approaches rely on model transparency, prompt engineering, or runtime guardrails. Anchor Architecture is model-independent: it enforces pre-analytical coordinates as a structural prerequisite, mitigating hallucination and drift through geometric validity rather than probabilistic filtering.

### 9.6 Positioning Summary

Anchor Architecture differs from existing work in three fundamental ways:

1. **Pre-analytical vs. post-hoc** — It defines coordinates before analysis, not after execution.
2. **Minimal relational core** — Two primitives (Anchor, Relation) suffice; all views and operations are projections.
3. **Semantic neutrality** — No embedded meaning; interpretation is delegated to application layer.

This relational foundation fills a gap in AI-assisted SE: traceability as a deterministic coordinate geometry, rather than heuristic or model-dependent reconstruction.

---

## 10. Conclusion

### 10.1 Summary

This paper presented Anchor Architecture, a minimal structural foundation for software traceability. The framework reduces traceability to two primitives — Anchor as a spatiotemporal coordinate $\langle ID, L, \tau \rangle$ and Relationship as a directed binary relation $R \subseteq \mathcal{A} \times \mathcal{A}$ — from which four structural views (Linear, Net, Set, Timeline) and four operations (trace, impact, diff, version) are derived without additional axioms. The framework is model-independent, tool-independent, semantically neutral, and pre-analytical: it defines the structural conditions under which traceability becomes deterministic, regardless of whether artifacts are produced by human developers or AI systems.

The central claim — that traceability failures are caused by missing structural anchors, not by opaque reasoning — was substantiated through formal analysis and a comprehensive worked example (Section 8). Failure diagnosis, impact analysis, change detection, and history reconstruction were each reduced to coordinate operations over the relational structure $(\mathcal{A}, R)$. Ghost references were detected not through semantic inspection but through geometric resolution failure: $resolve(a) = \emptyset$. These results demonstrate that pre-analytical anchoring transforms traceability from a documentation practice into a structurally examinable property.

---

### 10.2 Limitations

Anchor Architecture, as a structural foundation, deliberately defers several concerns that are essential for practical deployment.

**Adoption cost.** The framework requires spatiotemporal binding at creation time. Retrofitting pre-analytical anchors onto existing artifact ecosystems — particularly legacy codebases and unstructured documents — presents integration challenges that this paper does not address.

**Semantic layer.** The framework is semantically neutral by design: it defines *where* and *when* artifacts exist, not *what* relationships mean. Practical traceability systems require semantic interpretation (e.g., "implements", "tests", "deprecates") that must be supplied by application layers consuming the structural substrate.

**Empirical validation.** The worked example in Section 8 demonstrates operational mechanics on a representative scenario, but large-scale empirical evaluation across diverse software projects and organizational contexts remains to be conducted.

**Scalability characteristics.** While the relational formalization is well-defined, the computational behavior of operations such as $trace()$ and $impact()$ over large anchor sets — particularly under transitive closure $R^+$ — requires further analysis with respect to practical performance bounds.

---

### 10.3 Future Directions

The structural foundation established by Anchor Architecture opens several avenues for further investigation.

**Intent preservation.** When AI agents generate or modify artifacts, the reasoning behind structural decisions is often lost — a phenomenon we term *ghost intent*. Extending the coordinate system to capture decision provenance without requiring model introspection is a natural next step.

**Structural decision analysis.** Software development involves recurring structural decisions (technology selection, architectural trade-offs, constraint resolution) whose rationale degrades over time. Formalizing decision structures over the anchor substrate could enable deterministic decision traceability.

**Constraint enforcement in agentic pipelines.** As autonomous AI agents increasingly participate in software development workflows, enforcing pre-analytical anchor generation as a pipeline constraint — rather than relying on post-hoc annotation — becomes a practical imperative.

**Boundary monitoring.** The structural views defined in this paper (particularly Net View and Set View) suggest the possibility of continuous monitoring for structural integrity violations, enabling proactive detection of traceability degradation rather than reactive diagnosis.

Each of these directions builds upon the coordinate system and relational structure established here, extending rather than replacing the foundational primitives.

---

### 10.4 Closing Remarks

Anchor Architecture occupies a layer beneath provenance models, version control systems, and traceability tooling — defining the coordinate system upon which these systems implicitly depend. Its contribution is not a new tool or methodology, but a clarification of structural prerequisites: the minimal conditions under which traceability ceases to be speculative and becomes examinable.

The architecture requires minimal primitives but provides deterministic examinability. Examinability requires structure prior to analysis. And structure, once absent at creation, cannot be reconstructed with certainty.

Traceability is not documentation. It is coordinate geometry over declared relations.

---

## References

### 1. Provenance and Traceability Foundations

[1] W3C. *PROV-DM: The PROV Data Model*. W3C Recommendation, 2013.  
[2] Gotel, O., Finkelstein, A. *An Analysis of the Requirements Traceability Problem*. IEEE International Conference on Requirements Engineering, 1994.  
[3] Mens, T., Demeyer, S. *Software Evolution*. Springer, 2008.

### 2. Supply Chain and Attestation Frameworks

[4] SLSA Working Group. *Supply-chain Levels for Software Artifacts (SLSA)*. OpenSSF, 2021–2025.  
[5] in-toto. *A Framework to Secure the Integrity of Software Supply Chains*. Linux Foundation, 2020–2025.

### 3. AI Agent and LLM in Software Engineering

[6] Junwei Liu et al. *Large Language Model-Based Agents for Software Engineering: A Survey*. arXiv:2409.02977, 2024 (accepted by TOSEM).  
[7] Lin Chen et al. *AI Agent Behavioral Science*. arXiv:2506.06366v2, 2025.  
[8] Abhishek Rath et al. *Agent Drift: Quantifying Behavioral Degradation in Multi-Agent LLM Systems*. arXiv:2601.04170, 2026.  
[9] Adnan Masood. *Agent Drift: the reliability blind spot in multi-agent LLM systems*. Medium, 2026.  
[10] Y. Dong et al. *Safeguarding Large Language Models: A Survey*. arXiv:2406.02622, 2024 (published in Artificial Intelligence Review, 2025).

### 4. Governance and Decision Frameworks

[11] ISO/IEC 42001:2023. *Information technology — Artificial intelligence — Management system*. International Organization for Standardization, 2023.  
[12] Weidinger, L. et al. *Taxonomy of risks posed by language models*. Proceedings of the 2022 ACM Conference on Fairness, Accountability, and Transparency (FAccT), 2022.

---

## Appendix A — Comprehensive Structural Demonstration

This appendix demonstrates Anchor Architecture through a realistic failure scenario.
The flow for each operation follows:
code example → formal expression → operation → result → derivation → finding.

The objective is structural examinability under realistic engineering conditions.

---

### A.1 Scenario Description

**System:** Authentication Module

Evolution:

1. Initial requirement: Password ≥ 4 characters
2. Strengthened: Password ≥ 8 characters
3. Further strengthened: Password ≥ 12 characters
4. OAuth fallback introduced
5. After deployment, some users cannot log in

Engineering questions:

- Which requirement version introduced the issue?
- Which code artifacts are affected?
- Has any related code changed after the policy update?
- Is there any structurally invalid reference?

All answers must derive from $(\mathcal{A}, R)$.

---

### A.2 Anchor Set Construction

#### A.2.1 Requirement Anchors

```markdown
---
location: srs/auth.md
version: v1.0
---

### FR-091
Password length must be ≥ 4 characters.
```

```markdown
---
location: srs/auth.md
version: v1.1
---

### FR-091
Password length must be ≥ 8 characters.
```

```markdown
---
location: srs/auth.md
version: v1.2
---

### FR-091
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

#### A.2.2 Implementation Anchors

Password validation:

```python
# file: src/auth/password.py
# version: 1.4
# ID: FUNC-validate-password
# TRACE: FR-091@v1.2

def validate_password(password: str) -> bool:
    return len(password) >= 12
```

OAuth fallback:

```python
# file: src/auth/oauth.py
# version: 2.1
# ID: FUNC-oauth-fallback
# TRACE: FR-091@v1.1

def oauth_password_policy(user: object) -> bool:
    if external_provider():
        return True
    return len(user.password) >= 12
```

Login entry point:

```python
# file: src/auth/login.py
# version: 3.0
# ID: FUNC-login
# TRACE: FUNC-validate-password@v1.4, FUNC-oauth-fallback@v2.1

def login(user, pwd):
    if not validate_password(pwd):
        if not oauth_password_policy(user):
            raise ValueError("Invalid password")
```

Formal anchors:

$$
A_{c1} = \langle FUNC\text{-}validate\text{-}password,\; src/auth/password.py,\; 1.4 \rangle
$$

$$
A_{c2} = \langle FUNC\text{-}oauth\text{-}fallback,\; src/auth/oauth.py,\; 2.1 \rangle
$$

$$
A_{c3} = \langle FUNC\text{-}login,\; src/auth/login.py,\; 3.0 \rangle
$$

---

#### A.2.3 Test Anchors

```python
# file: tests/test_auth.py
# version: v1.1
# ID: TEST-auth
# TRACE: FUNC-login@v3.0

def test_length_too_short():
    with pytest.raises(ValueError):
        login("user", "short")

def test_length_eligible():
    assert login("user", "validpassword1")
```

Formal anchor:

$$
A_{t} = \langle TEST\text{-}auth,\; tests/test\_auth.py,\; 1.1 \rangle
$$

---

### A.3 Relationship Declaration

The `TRACE` annotations in the code above instantiate the following relation:

$$
R = \{ (A_{r3}, A_{c1}),\; (A_{r3}, A_{c2}),\; (A_{c1}, A_{c3}),\; (A_{c2}, A_{c3}),\; (A_{c3}, A_{t}) \}
$$

$$
R \subseteq \mathcal{A} \times \mathcal{A}
$$

No semantic labels (implements, tests, validates) are embedded.
The label `TRACE` is application-layer vocabulary, not architectural semantics.

---

### A.4 Issue Investigative Flow

Users report login failure after deployment.
The investigation proceeds entirely through coordinate operations over $(\mathcal{A}, R)$.

---

#### A.4.1 trace()

**Question:** Through which structural chain does the requirement reach the failing test?

**Code path:**

```
FR-091 (srs/auth.md, v1.2)
  → FUNC-validate-password (src/auth/password.py, v1.4)
    → FUNC-login (src/auth/login.py, v3.0)
      → TEST-auth (tests/test_auth.py, v1.1)

FR-091 (srs/auth.md, v1.2)
  → FUNC-oauth-fallback (src/auth/oauth.py, v2.1)
    → FUNC-login (src/auth/login.py, v3.0)
      → TEST-auth (tests/test_auth.py, v1.1)
```

**Operation:**

$$
trace(A_{r3},\; P(x) := x = A_t)
$$

**Result:**

$$
\{ [A_{r3}, A_{c1}, A_{c3}, A_t],\; [A_{r3}, A_{c2}, A_{c3}, A_t] \}
$$

**Derivation:**
trace() enumerates all paths in $R^{+}$ from source anchor to target predicate.
Two paths exist because $A_{r3}$ connects to $A_{c3}$ through two independent intermediaries.

**Finding:**
Requirement v1.2 propagates to the failing test through two distinct structural paths —
both the password validator and the OAuth fallback are in the failure chain.

---

#### A.4.2 diff()

**Question:** What changed between requirement versions?

**Code comparison:**

```markdown
<!-- v1.1 -->
### FR-091
Password length must be ≥ 8 characters.
```

```markdown
<!-- v1.2 -->
### FR-091
Password length must be ≥ 12 characters.
```

**Operation:**

$$
diff(A_{r2}, A_{r3}) = \Delta(resolve(A_{r2}),\; resolve(A_{r3}))
$$

**Result:**

```diff
  ### FR-091
- Password length must be ≥ 8 characters.
+ Password length must be ≥ 12 characters.
```

**Derivation:**
diff() resolves both anchors to content via $resolve(\langle ID, L, \tau \rangle) \to Content$,
then applies content-difference operator $\Delta$.
Both anchors share $ID$ and $L$; only $\tau$ differs.

**Finding:**
Constraint tightened from 8 → 12 characters.
Previously valid passwords (length 8–11) are now rejected — this is a breaking change.

---

#### A.4.3 impact()

**Question:** Which artifacts are structurally downstream of this requirement version?

**Affected code:**

```python
# FUNC-validate-password — directly references FR-091@v1.2
def validate_password(password: str) -> bool:
    return len(password) >= 12  # ← constraint from v1.2
```

```python
# FUNC-oauth-fallback — directly references FR-091
def oauth_password_policy(user: object) -> bool:
    if external_provider():
        return True
    return len(user.password) >= 12  # ← constraint from v1.2
```

```python
# FUNC-login — references both implementations
def login(user, pwd):
    ...
```

```python
# TEST-auth — references FUNC-login
def test_length_too_short():
    ...
```

**Operation:**

$$
impact(A_{r3})
$$

**Result:**

$$
\{ A_{c1},\; A_{c2},\; A_{c3},\; A_t \}
$$

**Derivation:**
impact() computes forward reachability over $R^{+}$ from source anchor:

$$
impact(a) = \{ a' \in \mathcal{A} \mid (a, a') \in R^{+} \}
$$

**Finding:**
Blast radius is four artifacts: two implementations, one integration point, one test.
All authentication-related code is structurally downstream of the requirement change.

Contrast with trace(): trace() reveals **how** impact propagates (paths);
impact() reveals **what** is affected (set).

---

#### A.4.4 version()

**Question:** What is the structural evolution of this requirement?

**Version history:**

```markdown
v1.0 — Password length must be ≥ 4 characters.
v1.1 — Password length must be ≥ 8 characters.
v1.2 — Password length must be ≥ 12 characters.
```

**Operation:**

$$
version(FR\text{-}091,\; srs/auth.md)
$$

**Result:**

$$
[ A_{r1},\; A_{r2},\; A_{r3} ]
$$

$$
v1.0 \rightarrow v1.1 \rightarrow v1.2
$$

**Derivation:**
version() projects all anchors sharing $(ID, L)$ and orders by $\tau$:

$$
version(ID, L) = sort_{\tau}(\{ a \in \mathcal{A} \mid a.ID = ID \land a.L = L \})
$$

**Finding:**
Three progressive constraint strengthenings.
Deployment corresponds to v1.2; failure reports begin 90 minutes after deployment.
Temporal alignment confirms v1.2 as the structurally correlated change.

---

### A.5 Ghost Reference Detection

During investigation, engineer discovers a reference in legacy code:

```python
# file: src/auth/legacy.py
# version: 0.8 (deprecated)
# ID: FUNC-legacy-auth
# TRACE: FR-999

def legacy_authentication(user):
    if user.is_admin:
        return True
```

**Structural validation:**

$$
resolve(\langle FR\text{-}999,\; srs/auth.md,\; * \rangle) = \varnothing
$$

No anchor FR-999 exists at any version.

$$
(A_{ghost}, A_{legacy}) \notin R_{\text{valid}}
$$

The reference is syntactically present but structurally void.

**Finding:**
Detection requires no model introspection or code review heuristics —
only coordinate resolution.
Whether the origin is AI hallucination, developer error, or documentation drift,
the structural consequence is identical:
the relationship is geometrically invalid and cannot participate in
trace(), impact(), or any operation over $(\mathcal{A}, R)$.

---

### A.6 Synthesis Conclusion

The failure was diagnosed entirely through coordinate operations:

| Operation | Question                            | Result                                          |
| --------- | ----------------------------------- | ----------------------------------------------- |
| trace()   | How does the change reach the test? | Two propagation paths via $A_{c1}$ and $A_{c2}$ |
| diff()    | What changed?                       | Constraint 8 → 12 (breaking)                    |
| impact()  | What is affected?                   | 4 downstream anchors                            |
| version() | When did it change?                 | v1.2 deployed, failures at T+90min              |
| resolve() | Is FR-999 valid?                    | $\varnothing$ — structurally void               |

No semantic interpretation, model introspection,
or narrative reconstruction was required.
The diagnosis was not *discovered* through expert judgment —
it was *derived* through coordinate geometry over $(\mathcal{A}, R)$.
