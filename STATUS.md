# Paper Status Definitions

This document defines the lifecycle states used in this repository.

Status reflects **the role of a document in the research workflow**,
not academic quality, acceptance, or endorsement.

Status changes are **organizational signals**, expressed by
directory placement and index updates — not embedded in document content.

---

## Status Overview

| Status      | Meaning                                      | Location       |
| ----------- | -------------------------------------------- | -------------- |
| manuscripts | Authoritative working manuscripts (Markdown) | `manuscripts/` |
| in-progress | Submission-ready artifacts not yet submitted | `in-progress/` |
| submitted   | Formally submitted versions under review     | `submitted/`   |
| preprints   | Publicly accessible reference versions       | `preprints/`   |

---

## manuscripts

### Definition
**Manuscripts** are the canonical writing surface of this repository.

They represent the author's current thinking in Markdown form,
regardless of whether the content is finalized or still evolving.

### Characteristics
- Written in Markdown
- May include:
  - early drafts
  - refined but unpublished manuscripts
  - post-submission revisions
- Content may continue evolving even after submission

### Design Intent
Manuscripts are **not tied to submission state**.

They answer:
> “What does the author currently think?”

Not:
> “What has been submitted?”

---

## in-progress

### Definition
**In-progress** contains artifacts that are structurally complete
and prepared for submission, but **not yet formally submitted**.

### Characteristics
- PDF, TeX, or other submission-format artifacts
- Correspond to a specific manuscript snapshot
- Awaiting submission timing or venue decision

### Typical Use
- Final PDF prepared but not uploaded
- TeX package ready for arXiv but held back
- Internal consistency check stage

---

## submitted

### Definition
**Submitted** contains artifacts that have been formally submitted
to external platforms (SSRN, arXiv, conferences, journals).

### Characteristics
- Content is frozen for that review cycle
- Files represent an exact submission snapshot
- External review or processing is ongoing

### Required Context (via index.md)
- Submission platform (e.g., SSRN, arXiv)
- Submission date
- Identifier (if available)

---

## preprints

### Definition
**Preprints** are publicly accessible reference versions of papers.

### Characteristics
- Public URL exists
- Stable citation target
- Corresponds to a specific submitted version

### Notes
Preprints are **additive**, not replacements.

A manuscript may:
- exist in `manuscripts/`
- have a submitted snapshot in `submitted/`
- and a public reference in `preprints/`

All simultaneously.

---

## Structural Rules

- Documents **do not carry status internally**
- Status is expressed by:
  - directory placement
  - index.md entries
- Content edits and status changes should be **separate commits**

---

## Design Principle

> Manuscripts express thinking.  
> Submissions express timing.  
> Preprints express visibility.

Status is a **workflow signal**, not an academic judgment.
