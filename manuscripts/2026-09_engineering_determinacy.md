# Engineering Determinacy: Structuring Established Knowledge So That It Need Not Be Reinterpreted

**Author:** Spark Tsai
**ORCID:** https://orcid.org/0009-0006-8847-4703
**Email:** spark.tsai@gmail.com

## Abstract

Engineering work continuously produces information that becomes established: what a task covers, which behaviors are permitted, which artifact a requirement refers to, where a decision came from, and what state must survive a handoff. Yet established information often remains expressed in the same semantic form as information that is still unresolved. As long as it exists only in natural language, a later consumer must read, understand, and interpret it before use. What engineering settled previously can therefore become subject to interpretation again.

This paper introduces **Engineering Determinacy** as a principle concerning the form in which established engineering information exists. Rather than remaining accessible only through semantic reconstruction, established information can be given an explicit engineering representation. Two conceptual operations are distinguished. **Extraction** makes explicit information already contained in semantic material, such as turning an implied scope into an enumerated set. **Attachment** assigns engineering information that the semantics did not originally contain, such as an identifier, anchor, or trace. Because explicit structure can still be incomplete, stale, or wrong, the principle also requires **bounded engineering treatment** sufficient to maintain the representation for its intended purpose.

A further consequence is model independence. When an established engineering fact remains available only as semantic content, its operational interpretation may vary with the model, context, or interaction in which it is reconstructed. Once it has an explicit engineering representation, preserving that fact no longer has to depend on the semantic capability of the model consuming it.

The principle was recognized retrospectively across a series of previously published mechanisms addressing different engineering problems. Scope sets, behavior states, identifiers, trace links, specification structures, decision classifications, and continuation fields were developed independently, yet repeatedly performed the same function: they gave established engineering information an existence independent of the semantics through which it was originally expressed. This paper names that shared property and positions it in relation to requirements traceability, formal specification, context engineering, knowledge representation, and AI governance.

**Keywords:** Engineering Determinacy; AI-Assisted Software Engineering; Established Engineering Knowledge; Semantic Interpretation; Structured Representation; Requirements Traceability; Model Independence; AI Governance; Large Language Models; Software Engineering Practice

---

## 1. Introduction

### 1.1 Established information can remain semantically unresolved in form

Engineering processes continuously transform uncertainty into decisions, constraints, references, classifications, and accepted states. A requirement discussion may establish the scope of a task. A design review may establish which interface is authoritative. A policy decision may determine whether an action is permitted. A workflow handoff may determine what must continue into the next stage.

What changes during these activities is the epistemic status of the information: something that was previously open becomes established. Yet the representation of that information often does not change with it. Established and unresolved information may continue to coexist in specifications, issue descriptions, design documents, meeting notes, comments, and conversational history as ordinary natural language.

The engineering process may therefore have resolved a question while leaving the result in a form that requires a later consumer to resolve it again through interpretation.

### 1.2 Why the problem has become more visible

This condition predates artificial intelligence. Human engineering practice has long relied on memory, organizational continuity, domain familiarity, conversation, and clarification to reconstruct the operational meaning of prior decisions. Much of the cost of reinterpretation was absorbed informally by people.

Large language models make the problem more visible because semantic reconstruction can now occur repeatedly across sessions, models, agents, prompts, and workflow stages. A model may reasonably interpret the same wording differently under different surrounding contexts, and another model may reconstruct a different operational meaning without either model necessarily malfunctioning. The issue is therefore not simply that AI sometimes makes errors; it is that information engineering already regarded as settled may still be represented in a form that invites settlement again.

### 1.3 Scope of the principle

Engineering Determinacy concerns the form in which engineering information exists, not the type of system that consumes it. Large language models make the distinction especially consequential, but they do not define its boundary of applicability.

Once established information has been represented explicitly, it may be used by deterministic software, an AI model or agent, or a human. A CI process may evaluate a scope set, an execution environment may act on an assigned boundary state, a traceability tool may follow an identifier, and a human may inspect the same information directly. The principle is therefore about engineering representation rather than model context.

### 1.4 Contributions

This paper makes six conceptual contributions.

First, it identifies **repeated reinterpretation of established engineering information** as a distinct problem and separates it from hallucination. The problem arises not because a model necessarily produces unsupported output, but because information that should no longer require interpretation remains represented in an interpretation-dependent form.

Second, it introduces **Engineering Determinacy** as a principle for preserving established engineering information independently of repeated semantic reconstruction.

Third, it distinguishes **Extraction** and **Attachment** as two conceptual operations through which semantic material can acquire an explicit engineering representation, and introduces **bounded engineering treatment** to recognize that explicit structure must still be maintained for its intended purpose.

Fourth, it identifies three recurring forms observed across prior work—**Identification, Enumeration, and State Assignment**—without claiming that they constitute an exhaustive taxonomy.

Fifth, it develops the consequence of **model-independent determinacy**: changing the model may alter how unresolved information is inferred without requiring established engineering facts to be reconstructed again.

Finally, it provides a retrospective synthesis of independently developed prior mechanisms and shows that each can be understood as moving some part of engineering information away from repeated semantic reinterpretation.

### 1.5 Core proposition

The central proposition of this paper is:

> **Established engineering knowledge should have an existence independent of the semantic interpretation required to discover it.**

The remainder of the paper develops this proposition, explains how such independence may be obtained, and positions it against adjacent engineering and AI practices.

---

## 2. The Problem of Reinterpretation

### 2.1 Semantic information must be understood before it can be used

Natural language carries engineering meaning through interpretation. A statement describing a permitted action, task boundary, artifact relationship, decision rationale, or workflow condition cannot generally be acted upon merely because its text is available. A consumer must first determine what that text means for the engineering purpose at hand.

This property is useful while information remains unresolved. Interpretation allows ambiguity to be examined, alternatives to be compared, and meaning to be negotiated. The difficulty begins when the same interpretive process continues to be required after engineering has already treated the relevant meaning as established.

### 2.2 Interpretation is not guaranteed to reproduce itself

The same semantic material can lead to different operational interpretations across readers, sessions, models, surrounding contexts, and points in time. A requirement may remain textually unchanged while its inferred scope differs. A behavioral restriction may remain unchanged while different consumers infer different permissible actions. A reference may remain linguistically stable while different artifacts are assumed to be its target.

In each case, the text persists, but the operational meaning is reconstructed. The previous engineering resolution is therefore not obtained directly; it is re-created from semantic material. A later consumer may reproduce the intended interpretation exactly, but successful reproduction is still different from direct access to an explicit representation of what had already been established.

### 2.3 Why this is not hallucination

Repeated reinterpretation is distinct from hallucination. Hallucination concerns unsupported, fabricated, or otherwise erroneous model output. Reinterpretation can occur even when a model behaves entirely as requested.

If a scope is supplied only as prose, interpreting that prose is precisely what the model has been asked to do. If the interpretation differs from an earlier human or model interpretation, the relevant failure may not lie in model competence at all. It may lie in the decision to keep an already established scope available only through semantic reconstruction.

The problem addressed here is therefore not interpretation itself. Engineering necessarily depends on interpretation where uncertainty remains. The problem is continuing to require interpretation where engineering has already resolved what that interpretation was intended to establish.

---

## 3. Engineering Determinacy

### 3.1 Definition

> **Engineering information is determinate when obtaining what has already been established requires access rather than reinterpretation.**

The criterion is intentionally simple: **does obtaining this information require understanding it again?**

Engineering Determinacy does not require all engineering information to become structured. It concerns information whose relevant engineering meaning has already been established and is expected to remain available as such.

### 3.2 Extraction

**Extraction** makes explicit engineering information already contained within semantic material. A requirement may, for example, imply a particular scope of change. As long as that scope exists only within the requirement prose, a later consumer must reconstruct it by interpreting the text. Extracting that scope into an explicit set gives the established information an independently accessible representation.

A short illustration makes the difference concrete. Suppose a task states:

> Only files related to authentication may be modified.

Even where a team has already agreed what that scope covers, the operative boundary still depends on how each consumer interprets *related to authentication*. Whether a shared session utility, a middleware registration, or a payment module that calls an authentication service falls inside the scope remains an interpretive judgment, and different consumers may answer differently without any of them behaving unreasonably.

Extracting the agreed scope into an explicit set changes what obtaining it requires:

```
scope:
  src/auth/*
  tests/auth/*
```

Whether `src/payment/payment.ts` lies within scope is now a membership question rather than an interpretive one. The prose may remain in place as explanation, but the established boundary no longer depends on it.

Extraction does not create information that was absent from the source semantics. Its limits are therefore defined by what the semantic material actually contains. If a requirement never established a boundary, extracting one from it would instead introduce a new judgment.

### 3.3 Attachment

**Attachment** applies where the engineering information required for determinacy was never contained in the original semantics. A rule may receive a Rule ID, an artifact may receive an Anchor ID, or a derivation may receive a Trace ID linking it to its source. These identifiers are not hidden meanings to be recovered from the prose; they are engineering information assigned to it.

Extraction and Attachment therefore address different conditions, but they serve the same conceptual purpose: **to make established engineering information independently accessible from the semantic content through which it was originally expressed.**

### 3.4 Bounded Engineering Treatment

Explicit structure does not guarantee correctness. A Scope Set may be clear but incomplete, an assigned `DENY` state may be based on an obsolete policy, and a Trace ID may exist while pointing to the wrong artifact. Engineering Determinacy therefore requires engineering treatment sufficient to maintain the resulting representation for its intended purpose.

Such treatment may involve review, validation, versioning, invalidation, conflict detection, or other engineering practices. The paper deliberately does not prescribe a universal level of treatment. A personal development tool, an enterprise workflow, and a regulated system may require very different levels of assurance.

> **The concept is universal; the sufficient degree of engineering treatment is not, and is determined by the purpose of the system that applies it.**

### 3.5 Determinacy is not correctness

Engineering Determinacy does not claim that structured information is true merely because it has been made explicit. Correctness concerns whether the established information is right. Determinacy concerns whether what has been established remains directly obtainable as established rather than repeatedly reconstructed from its semantic origin.

This distinction matters because a wrong state can still be explicit, stable, and consistently accessible. Such a state is determinate but incorrect. The engineering problem then becomes validation or revision, not semantic reconstruction.

### 3.6 Consumer Independence

Once established information has an explicit engineering representation, it is not inherently model context. A CI script may evaluate a Scope Set, a runtime environment may act on an assigned boundary state, a traceability tool may traverse an identifier, a human may inspect the information directly, and an AI model may consume the same representation while performing a larger task.

The relevant property is not that every consumer internally understands the representation in an identical way. It is that each consumer can operate against the same explicit engineering reference rather than independently reconstructing what engineering had previously established from semantic material.

---

## 4. Established and Unresolved Information

The distinction between established and unresolved information is familiar to engineering practice. Teams distinguish accepted requirements from open questions, approved decisions from alternatives, and active constraints from proposals. Engineering Determinacy does not introduce that distinction. It argues that the difference in epistemic status should, where appropriate, be reflected in the form in which the information exists.

Information that remains unresolved may legitimately continue to depend on interpretation. Design, negotiation, diagnosis, comparison, and trade-off analysis all involve questions whose meaning, consequence, or preferred resolution is still open. Engineering Determinacy does not seek to remove those activities from engineering.

Established information is different. Once a relevant question has been settled for an engineering purpose, repeated reconstruction of that settlement adds uncertainty without adding new knowledge. The principle can therefore be expressed simply:

> **Inference belongs to the unresolved. Access belongs to the established.**

This does not imply that established information is immutable. New evidence, changed requirements, revised authority, or altered context may justify reopening it. Engineering Determinacy concerns how a resolution exists while it is treated as established, not whether that resolution can ever change.

---

## 5. Model-Independent Determinacy

A significant consequence of Engineering Determinacy appears when established information is consumed by AI systems. If an engineering fact remains available only through semantic content, its operational meaning remains partly dependent on the model asked to reconstruct that meaning. Model substitution, version changes, prompt changes, and context changes can therefore affect not only how unresolved questions are reasoned about, but also how supposedly settled facts are recovered.

Engineering Determinacy separates these two concerns. A new model may propose a different implementation, identify different risks, or reason differently about an unresolved trade-off. Those differences are legitimate consequences of changing inference capability. They should not automatically redefine an already established scope, reference, boundary, or state.

Capability provides a particularly useful test. The preservation of an established boundary should not become more reliable merely because a more capable model is used. If moving from a weaker model to a stronger one substantially improves the consistency with which the same boundary is recovered, then the boundary itself has remained dependent on semantic inference. Engineering may have decided it, but engineering has not yet given that decision an independent representation.

The claim is therefore not that AI systems can become independent of models. Models remain necessary where interpretation, generation, comparison, and inference are required. The narrower claim is that **determinacy need not remain model-dependent merely because AI is one of the consumers of the information.**

---

## 6. Retrospective Synthesis of Prior Work

### 6.1 Retrospective recognition

Engineering Determinacy was not the starting assumption from which the author's previous mechanisms were designed. Those mechanisms addressed different engineering problems independently: behavioral rules, scope, boundaries, anchoring, traceability, specification structure, decision analysis, decision risk, workflow continuation, and knowledge architecture.

Only in retrospect did a recurring property become visible. In each case, some piece of engineering information that would otherwise remain dependent on semantic reconstruction was given an identifier, explicit set, relationship, category, or assigned state. Engineering Determinacy names that shared property after the fact.

### 6.2 Semantic and engineering components

The mechanisms below were published between February and September 2026, each with an independent digital object identifier. Full citations appear in the references.

| Prior work                                  | Semantic component         | Engineering construct                       | Recurring form         | Operation  |
| ------------------------------------------- | -------------------------- | ------------------------------------------- | ---------------------- | ---------- |
| Behavior Rule Architecture [1]              | Rule content and rationale | Rule ID; MUST / MUST NOT                    | Identification + State | Attachment |
| Scope as a Governance Primitive [2]         | Task description           | Scope Set                                   | Enumeration            | Extraction |
| Boundary as an Execution-Time Primitive [3] | Restriction rationale      | Allow / Deny / Undefined                    | State Assignment       | Extraction |
| Anchor Architecture [4]                     | Artifact content           | Anchor ID and spatiotemporal coordinates    | Identification         | Attachment |
| Ghost Intent / Traceability Collapse [5]    | Intent description         | Trace ID links                              | Identification         | Attachment |
| Viewpoint-Structured Specification [6]      | Specification text         | Viewpoint structure; sufficiency conditions | Enumeration + State    | Extraction |
| Decision Analysis [7]                       | Decision rationale         | DA states; A1–A5 evidence types             | State Assignment       | Extraction |
| Decision Risk [8]                           | Risk rationale             | DR-V / DR-O / DR-I                          | State Assignment       | Extraction |
| Continuation Readiness [9]                  | Handoff explanation        | Continuation Package fields                 | Enumeration            | Extraction |
| AI Knowledge Architecture [10]              | Knowledge content          | Claim Object / Relation types               | Identification + State | Attachment |

### 6.3 Recurring forms

Three forms recur across these mechanisms. They are not proposed as an ontology or exhaustive taxonomy; they are empirical patterns observed across the author's prior work.

**Identification** answers *which one?* An identifier allows an engineering object, rule, artifact, decision, or relationship to be referenced without rediscovering its identity through semantic matching. Rule IDs, Anchor IDs, and Trace IDs are examples.

**Enumeration** answers *what is included?* An explicit set makes membership accessible without requiring a consumer to reconstruct a boundary from descriptive prose. Scope Sets and structured continuation fields illustrate this form.

**State Assignment** answers *which recognized condition applies?* An assigned state replaces repeated interpretation of the currently applicable category or condition. `Allow / Deny / Undefined`, Decision Analysis categories, and Decision Risk classifications are examples.

None of these constructs is novel in software engineering. Their relevance here lies in recognizing their shared function: each removes a piece of established engineering information from repeated semantic reconstruction.

### 6.4 Non-model uses

The engineering nature of these constructs is particularly visible in uses that involve no language model at all. A Scope Set can be evaluated by CI tooling to detect whether a change crosses an established boundary. An assigned Boundary state can be acted upon by an execution environment. A Trace ID can be traversed by a traceability or impact-analysis tool. Decision Analysis states can be aggregated in an audit report or dashboard. Continuation fields can be consumed by a workflow engine.

These examples matter because they show that the resulting structures are not merely prompt material. The same information may later be exposed to an AI system, but its existence and operational use do not depend on AI consumption.

### 6.5 Why this is not a constructed retrospective pattern

The mechanisms discussed above were developed and published independently before Engineering Determinacy was articulated as a shared principle. The earliest [4, 3] appeared in March 2026 and the latest [2, 9] in August 2026, each carrying its own registered identifier and publication date [1–10]. That record is externally verifiable and precedes the present paper, which establishes that these mechanisms were not constructed as examples to fit the abstraction proposed here.

This does not prove that Engineering Determinacy is the only possible interpretation of these mechanisms, nor does recurrence itself constitute empirical validation of the principle. It provides the historical basis for a retrospective synthesis: mechanisms developed for different engineering problems repeatedly introduced explicit constructs that reduced dependence on semantic reinterpretation.

The prior mechanisms therefore remain valid within their original problem domains. The present paper does not redefine them; it identifies a common function that had not previously been stated explicitly.

---

## 7. Positioning and Related Work

### 7.1 Retrieval and Grounding

Retrieval-augmented generation [11, 12] and graph-based retrieval architectures [13] reduce the likelihood that a model must operate without relevant external information. They address whether information can be retrieved and made available to a model.

Retrieved information, however, may still remain semantic material that must be interpreted before its engineering meaning can be used. Engineering Determinacy addresses a different question: whether information that has already been established should remain interpretation-dependent at all. Retrieval and determinacy are therefore complementary rather than competing concerns.

### 7.2 Requirements Engineering and Traceability

Requirements engineering and traceability provide the closest established precedent for several mechanisms discussed in this paper [14, 15, 16]. Identifiers, structured requirements, explicit trace links, dependency relationships, and impact paths have long been used to preserve connections across engineering artifacts and lifecycle stages, and ISO/IEC/IEEE 29148 codifies much of this practice [16].

Engineering Determinacy does not claim these constructs as new. Their existence is instead evidence that software engineering has long recognized practical situations in which semantic descriptions alone are insufficient for reliable engineering work.

The distinction proposed here is one of function. Traceability traditionally asks whether a requirement, design element, implementation artifact, or test can be followed across explicit relationships. Engineering Determinacy asks what happens to the engineering meaning of such relationships when semantic interpretation is repeatedly delegated to new consumers. A trace link does more than support navigation in that setting: it prevents an already established relationship from having to be rediscovered through semantic matching.

The same observation applies beyond trace links. A requirement identifier prevents identity from being repeatedly inferred from wording. An explicit scope prevents task membership from being reconstructed each time from prose. A recorded state prevents a previously resolved classification from becoming an open interpretive question again.

Engineering Determinacy therefore does not compete with traceability. It generalizes one property visible within traceability and related engineering practices: explicit engineering structure can preserve something that natural-language persistence alone does not necessarily preserve—the previously established operational resolution of an engineering question.

### 7.3 Formal Specification and Model-Driven Engineering

Formal specification and model-driven engineering provide a stronger precedent for making requirements, states, constraints, interfaces, and system behavior explicit through formally defined representations and semantics. They therefore demonstrate that engineering information need not remain dependent on informal interpretation.

Engineering Determinacy differs in ambition rather than object. Formal specification and model-driven engineering [17, 18, 19] make requirements, states, constraints, and behavior explicit through formally defined semantics, and therefore constitute the strongest existing precedent for reducing reliance on informal interpretation. Engineering Determinacy does not require complete formal semantics, exhaustive system specification, mathematically defined behavior, or proof obligations. Its concern is narrower: when particular engineering information is already treated as established, that information should be independently accessible from the semantic content through which it was originally expressed.

The word **bounded** is important for this reason. The appropriate degree of structure, validation, and formality is determined by the purpose for which the information will be used. Some cases may justify strong formal treatment; others may require only an explicit identifier, set, relationship, or state together with ordinary engineering validation.

Engineering Determinacy therefore does not replace formal methods. It states a weaker and more broadly applicable principle that can be satisfied without requiring the surrounding engineering system to become fully formal.

### 7.4 Context Engineering and Agent Memory

Context engineering and agent memory increasingly rely on structured state, schemas, summaries, retrieval mechanisms, persistent stores, and other techniques intended to improve continuity and task performance across model interactions [20, 21]. These practices approach part of the problem addressed here, and their outputs may also be consumable by conventional software.

The distinction therefore does not rest on whether a representation can technically be used outside a model. It rests on why the representation exists.

Context engineering and agent memory are primarily concerned with preserving, selecting, organizing, or retrieving information so that a model can perform a task more effectively. Engineering Determinacy asks a prior question: whether particular information that engineering already regards as established should remain dependent on semantic reinterpretation at all.

A structured memory record may improve the probability that a model reconstructs prior intent correctly. A determinate engineering representation instead seeks to remove the need to reconstruct the established part of that intent in the first place. The distinction is therefore between improving access to semantic context and giving selected established information an independent engineering existence.

### 7.5 Knowledge Representation

Knowledge representation provides extensive methods for making entities, concepts, relations, properties, and categories explicit and computationally accessible [22, 23, 24]. Engineering Determinacy shares its interest in structure, but it does not seek a comprehensive representation of a domain or complete computational semantics.

The principle deliberately permits large parts of engineering knowledge to remain semantic, incomplete, and open to interpretation. Its concern is limited to information already treated as established for a particular engineering purpose. The resulting structure therefore need not become an ontology or a complete knowledge model.

### 7.6 AI Governance and Controllability

AI alignment, guardrails, policy enforcement, and controllability mechanisms generally address how model outputs or actions should be constrained, evaluated, or governed [25, 26]. Engineering Determinacy operates earlier. It concerns the representation of engineering information against which such behavior may later be assessed.

An AI system may consume determinate scopes, policies, states, or relationships, but those representations need not have been created specifically for the model. Their role is to preserve engineering meaning independently of repeated semantic reconstruction.

### 7.7 Positioning within the author's prior work

Engineering Determinacy is not introduced as another framework layered on top of the author's earlier mechanisms. Scope, Boundary, Anchor, Trace, Decision Analysis, Decision Risk, specification structures, and continuation mechanisms continue to address their own engineering problems.

The contribution of the present paper is conceptual synthesis. It identifies a property repeatedly produced by those mechanisms: established engineering information became less dependent on semantic reinterpretation through explicit engineering constructs.

---

## 8. Discussion

### 8.1 Why this matters now

Engineering has always combined semantic reasoning with structured artifacts. Identifiers, enumerations, states, schemas, databases, trace links, and formal representations are not inventions of AI-assisted development.

What has changed is the scale and frequency at which semantic interpretation can be delegated to systems without the continuity traditionally supplied by human engineering teams. Models and agents can repeatedly encounter the same specifications, decisions, and constraints under different contexts. This makes it increasingly expensive to treat every piece of engineering information as if it were still open to interpretation.

Engineering Determinacy therefore articulates a distinction that traditional practice often handled implicitly: some engineering information exists to be reasoned about, while some exists because the reasoning has already produced a result that must persist.

### 8.2 When not to structure

Engineering Determinacy does not imply that every semantic statement should be converted into explicit structure. Structure creates maintenance obligations. Identifiers must remain valid, sets must remain synchronized with engineering reality, assigned states can become stale, and relationships can require versioning or invalidation. The cost of preserving a determinate representation may exceed the value of avoiding reinterpretation.

A related risk is **premature determinacy**. Ambiguity sometimes reflects incomplete knowledge rather than poor engineering. Forcing unresolved information into an identifier, set, or state can conceal uncertainty instead of resolving it. A provisional design choice may look authoritative once expressed as a fixed state even though the engineering process never intended it to be final.

The relevant question is therefore not whether information *can* be structured, but whether engineering has established enough of its meaning that repeated interpretation no longer contributes useful uncertainty resolution.

### 8.3 Who decides what is established?

Engineering Determinacy does not define a universal authority model for deciding when information becomes established. That decision depends on the engineering process and purpose involved.

A developer may establish a local implementation choice, a team may establish an interface contract, an organization may establish a policy, and a regulator may establish a compliance constraint. Different authorities can therefore establish different kinds of engineering information at different levels.

The principle begins after such an engineering process has treated information as established. Its concern is what form that information should take if later consumers are expected to rely on the established result rather than reconstruct it.

---

## 9. Limitations

This paper is conceptual and does not provide empirical evidence that applying Engineering Determinacy improves reliability, consistency, development speed, token efficiency, model portability, or engineering quality. Those effects remain hypotheses that require later evaluation.

The paper also does not establish a general cost-benefit threshold for determining when explicit engineering structure is worthwhile. Maintaining structured representations introduces engineering overhead, and the point at which that overhead exceeds the cost of repeated reinterpretation will vary across systems, domains, risks, and lifecycle stages.

---

## 10. Future Work

Three directions follow from the limitations above.

**Empirical evaluation.** The principle predicts that established engineering information supplied as explicit structure should be preserved more consistently than the same information supplied as prose, across model versions, vendors, session boundaries, and context perturbations. That prediction is testable. A suitable study would hold the underlying engineering facts constant, vary only their representation, and measure how often the operational result diverges. The present paper deliberately does not report such a study, but the prediction is stated here in falsifiable form so that it can be evaluated independently.

**Determining the threshold.** The conditions under which structuring is worth its maintenance cost remain unresolved. Candidate factors include how often the information is consumed, how many independent consumers exist, how severe the consequences of divergent interpretation are, and how frequently the underlying engineering fact changes. A practical decision procedure built on such factors would make the principle applicable without requiring case-by-case judgment.

**Completeness of the recurring forms.** Identification, Enumeration, and State Assignment were derived inductively from a limited set of mechanisms developed by one author. Whether other classes of established engineering information require a further form — ordering, quantity, or conditional dependency are plausible candidates — remains open. Examining mechanisms developed independently of the present research line would be the appropriate test.

---

## 11. Conclusion

Engineering work does not consist only of discovering new information. It continuously establishes identities, scopes, relationships, constraints, decisions, states, and conditions that later engineering activities are expected to reuse.

When those results remain available only through semantic content, future consumers must repeatedly reconstruct what engineering has already established. The text may persist while the operational meaning remains dependent on interpretation.

> **Engineering information is determinate when obtaining what has already been established requires access rather than reinterpretation.**

Extraction makes explicit information already contained in semantics. Attachment supplies engineering information that semantics did not contain. Bounded engineering treatment maintains the resulting structure sufficiently for its intended purpose. None of these operations requires all engineering knowledge to become formal or structured; unresolved information may and often should remain open to interpretation.

The principle is also independent of its consumer. Explicit engineering information may be evaluated by software, inspected by humans, or used by AI systems. Large language models make this distinction urgent because they repeatedly expose how easily established meaning can become interpretation-dependent again, but they do not define the principle's scope.

One consequence is especially important for AI-assisted engineering:

> **Engineering facts that have already been established should not change merely because the model used to consume them changes.**

The objective is not to eliminate inference or to make language models deterministic. It is to ensure that inference is used where engineering still needs it, rather than merely to recover what engineering has already established.
---

# Declarations

## Funding

This research received no external funding. It was conducted independently by the author.

## Conflicts of Interest

The author declares no conflicts of interest. The author develops open and commercial tooling related to AI-assisted software development, and the mechanisms cited in Section 6 are the author's own prior publications.

## Data Availability

No datasets were generated or analyzed. The paper is conceptual, and all prior mechanisms discussed in Section 6 are publicly available through the identifiers listed in the references.

## Declaration of Generative AI and AI-Assisted Technologies

The author used generative AI tools during drafting and editing to assist with language, organization, and consistency. All conceptual claims, analytical positions, and the synthesis presented here are the author's own. The author reviewed and edited all content and takes full responsibility for the final manuscript.

---

# References

## Prior work by the author

[1] Tsai, S. (2026). Behavior Rule Architecture: Rule-Based Governance of AI System Behavior. *engrXiv*. DOI: 10.31224/6681. Zenodo DOI: 10.5281/zenodo.19174636. Published 25 March 2026.

[2] Tsai, S. (2026). Scope as a Governance Primitive. *SSRN Electronic Journal*, 7353398. Zenodo DOI: 10.5281/zenodo.22108234. Published 28 August 2026.

[3] Tsai, S. (2026). Boundary as an Execution-Time Primitive for AI-Assisted Software Development Governance. *engrXiv*. DOI: 10.31224/6583. Zenodo DOI: 10.5281/zenodo.18883242. Published 9 March 2026.

[4] Tsai, S. (2026). Anchor Architecture. *engrXiv*. DOI: 10.31224/6580. Zenodo DOI: 10.5281/zenodo.18856781. Published 9 March 2026.

[5] Tsai, S. (2026). Ghost Intent: An Effect of Traceability Collapse in GenAI-Assisted SDLCs. *SSRN Electronic Journal*, 6348599. Zenodo DOI: 10.5281/zenodo.18872540. Published 23 April 2026.

[6] Tsai, S. (2026). Viewpoint-Structured Specification. *engrXiv*. DOI: 10.31224/6612. Zenodo DOI: 10.5281/zenodo.18930951. Published 10 March 2026.

[7] Tsai, S. (2026). Decision Analysis: Effect-Oriented Structural Scope Audit for AI-Assisted Software Development. *engrXiv*. DOI: 10.31224/6616. Zenodo DOI: 10.5281/zenodo.18934765. Published 10 March 2026.

[8] Tsai, S. (2026). Decision Risk: A Structural Governance Framework for AI-Assisted Software Development. *SSRN Electronic Journal*, 6655398. Zenodo DOI: 10.5281/zenodo.19025533. Published 7 May 2026.

[9] Tsai, S. (2026). Beyond HITL: Continuation Readiness as a Governance Requirement for Enterprise AI Workflows. *SSRN Electronic Journal*, 7252878. Zenodo DOI: 10.5281/zenodo.21856291. Published 13 August 2026.

[10] Tsai, S. (2026). AI Knowledge Architecture: From Repeated Semantic Inference to Persistent Knowledge Structure. *engrXiv*. Zenodo DOI: 10.5281/zenodo.20781734.

## Retrieval and grounding

[11] Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. In *Advances in Neural Information Processing Systems*, 33, 9459–9474.

[12] Gao, Y., Xiong, Y., Gao, X., Jia, K., Pan, J., Bi, Y., Dai, Y., Sun, J., & Wang, H. (2023). Retrieval-augmented generation for large language models: A survey. *arXiv preprint arXiv:2312.10997*.

[13] Edge, D., Trinh, H., Cheng, X., Bradley, J., Chao, A., Mody, A., Truitt, S., & Larson, J. (2024). From local to global: A Graph RAG approach to query-focused summarization. *arXiv preprint arXiv:2404.16130*.

## Requirements engineering and traceability

[14] Gotel, O. C. Z., & Finkelstein, A. C. W. (1994). An analysis of the requirements traceability problem. In *Proceedings of the First International Conference on Requirements Engineering* (pp. 94–101). IEEE. DOI: 10.1109/ICRE.1994.292398.

[15] Cleland-Huang, J., Gotel, O. C. Z., Huffman Hayes, J., Mäder, P., & Zisman, A. (2014). Software traceability: Trends and future directions. In *Proceedings of the Future of Software Engineering (FOSE 2014)* (pp. 55–69). ACM. DOI: 10.1145/2593882.2593891.

[16] ISO/IEC/IEEE. (2018). *ISO/IEC/IEEE 29148:2018 — Systems and software engineering — Life cycle processes — Requirements engineering*. ISO/IEC/IEEE.

## Formal specification and model-driven engineering

[17] Woodcock, J., Larsen, P. G., Bicarregui, J., & Fitzgerald, J. (2009). Formal methods: Practice and experience. *ACM Computing Surveys*, 41(4), Article 19. DOI: 10.1145/1592434.1592436.

[18] Schmidt, D. C. (2006). Guest editor's introduction: Model-driven engineering. *Computer*, 39(2), 25–31. DOI: 10.1109/MC.2006.58.

[19] Abrial, J.-R. (2010). *Modeling in Event-B: System and Software Engineering*. Cambridge University Press.

## Context engineering and agent memory

[20] Packer, C., Wooders, S., Lin, K., Fang, V., Patil, S. G., Stoica, I., & Gonzalez, J. E. (2023). MemGPT: Towards LLMs as operating systems. *arXiv preprint arXiv:2310.08560*.

[21] Park, J. S., O'Brien, J. C., Cai, C. J., Morris, M. R., Liang, P., & Bernstein, M. S. (2023). Generative agents: Interactive simulacra of human behavior. In *Proceedings of the 36th Annual ACM Symposium on User Interface Software and Technology (UIST '23)*. ACM. DOI: 10.1145/3586183.3606763.

## Knowledge representation

[22] Hogan, A., Blomqvist, E., Cochez, M., d'Amato, C., de Melo, G., Gutierrez, C., Kirrane, S., Labra Gayo, J. E., Navigli, R., Neumaier, S., Ngonga Ngomo, A.-C., Polleres, A., Rashid, S. M., Rula, A., Schmelzeisen, L., Sequeda, J., Staab, S., & Zimmermann, A. (2021). Knowledge graphs. *ACM Computing Surveys*, 54(4), Article 71. DOI: 10.1145/3447772.

[23] Vrandečić, D., & Krötzsch, M. (2014). Wikidata: A free collaborative knowledgebase. *Communications of the ACM*, 57(10), 78–85. DOI: 10.1145/2629489.

[24] Studer, R., Benjamins, V. R., & Fensel, D. (1998). Knowledge engineering: Principles and methods. *Data & Knowledge Engineering*, 25(1–2), 161–197. DOI: 10.1016/S0169-023X(97)00056-6.

## AI governance and controllability

[25] ISO/IEC. (2023). *ISO/IEC 42001:2023 — Information technology — Artificial intelligence — Management system*. ISO/IEC.

[26] National Institute of Standards and Technology. (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0)*. NIST AI 100-1. DOI: 10.6028/NIST.AI.100-1.
