# Papers

**Author:** Spark Tsai  
**ORCID:** https://orcid.org/0009-0006-8847-4703

This repository documents an original and ongoing research program
examining how **software engineering must structurally adapt to
AI-assisted development**, and what this implies for making
**AI governance technically realizable rather than purely declarative**.

The work presented here develops a coherent conceptual system,
including (but not limited to) **Engineering Decision Behavior Governance (EDBG)**
and **Engineering Decision Behavior Framework (EDBF)**,
along with related constructs such as *Inference Creep*, *Ghost Intent*,
*Decision Risk*, *Viewpoint-Driven Specification (VDS)*,
and *Intent-Governed Execution Framework (IGEF)*.

**First publicly articulated in early 2026**, these concepts are developed
as part of a unified research trajectory rather than isolated papers.

All core formulations are timestamped via Git history and
cross-referenced across manuscripts to preserve conceptual lineage
and internal consistency.

---

## Scope

This repository treats **software engineering as the primary locus of inquiry**.

Discussions of AI governance appear only insofar as they arise from
engineering structures, development workflows, execution boundaries,
and decision traceability within AI-assisted systems.

Key scope characteristics:

- Focus on the **development phase**, not deployment-time compliance or policy enforcement
- Emphasis on **engineering-detectable phenomena**, rather than model internals
- Governance framed as an **engineering problem of decision behavior**, not institutional control

Topics intentionally **out of scope** include:
- Model alignment techniques
- Runtime content moderation
- Organizational policy frameworks detached from engineering artifacts

---

## Repository Structure

This repository is organized by **manuscript maturity**, not by topic silos.

- `manuscripts/`  
  Early conceptual drafts and exploratory arguments.
  These documents capture problem formulation and theoretical scaffolding
  and should not be cited as final positions.

- `in-progress/`  
  Actively developed papers with a stabilized direction
  but not yet submitted or finalized.

- `submitted/`  
  Manuscripts that have been submitted to conferences, journals,
  or public archives.

- `published/`  
  Publicly accessible preprints (e.g., arXiv) corresponding
  to submitted manuscripts.

- `history/`  
  Conceptual and structural evolution records for each paper,
  documenting key decision points, terminological shifts,
  and explicit exclusions.
  These files provide provenance rather than draft recovery.

- `index.md`  
  A chronological and thematic index of all manuscripts,
  indicating status, relationships, and conceptual dependencies.

---

## Reading Guide

For readers encountering this work for the first time:

1. Begin with `index.md` to understand the overall research landscape
   and how individual papers relate to the broader framework.
2. Refer to `GLOSSARY.md` to familiarize yourself with the controlled
   vocabulary used throughout this repository.
   Core terms are system-defined and may not align with informal or
   industry usage.
3. Consult `preprints/` for stable, citable reference points.
4. Read materials in `in-progress/` or `manuscripts/` only if you are
   interested in ideas under active formation or theoretical evolution.


---

## Methodological Note

This repository follows a **traceable manuscript methodology**.

Individual papers are developed on dedicated topic branches and
merged into `main` only upon conceptual stabilization.
Early drafts are intentionally excluded from `main`,
while each finalized manuscript is accompanied by a concise
conceptual history documenting its evolution.

This structure is designed to support:
- intellectual provenance
- terminological precision
- and defensible priority of formulation

---

## Relationship to Other Repositories

This repository is part of a broader research workspace that includes:

- narrative and reflective explorations (e.g., essays, blogs)
- formalized schemas, constraints, and specification artifacts

Repositories are separated by **artifact type**, not by research domain,
to preserve clarity between conceptual analysis, formal structure,
and narrative interpretation.

---

## License

Unless otherwise noted, all materials in this repository are released under
the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license.
Attribution is required for any reuse of concepts, terminology, or text.
