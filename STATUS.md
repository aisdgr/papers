# Paper Status Definitions

This document defines the lifecycle states used in this repository.
Status changes are **structural events** and must be reflected by
directory movement and a corresponding commit.

Status labels describe **maturity and intent**, not quality or acceptance.

---

## Status Overview

| Status      | Meaning                        | Structural Location |
| ----------- | ------------------------------ | ------------------- |
| draft       | Exploratory, incomplete ideas  | `drafts/`           |
| in-progress | Structured, actively developed | `in-progress/`      |
| submitted   | Under formal review            | `submitted/`        |
| preprint    | Publicly available reference   | `preprints/`        |

---

## draft

### Definition
A **draft** represents early or exploratory work.
Arguments may be incomplete, unstable, or undergoing reframing.

### Characteristics
- Structure may change significantly
- Evaluation may be absent or undefined
- Target venue may be unknown or tentative
- Content is not citation-ready

### Allowed Artifacts
- Conceptual framing
- Partial arguments
- Open questions
- Notes and sketches

### Transition Criteria
A draft may be promoted to **in-progress** when:
- A stable core question is identified
- Overall structure is no longer experimental
- The paper has a clear direction

---

## in-progress

### Definition
An **in-progress** paper has a defined structure and scope,
but is still undergoing substantive development.

### Characteristics
- Core argument is stable
- Sections and flow are mostly fixed
- Evaluation, examples, or evidence may still be incomplete
- Target venue is identified

### Allowed Artifacts
- Full manuscript drafts
- Figures under refinement
- Preliminary evaluation or case material

### Transition Criteria
An in-progress paper may be promoted to **submitted** when:
- The manuscript is submission-complete
- All required sections for the target venue are present
- No major conceptual changes are expected

---

## submitted

### Definition
A **submitted** paper has been formally submitted to a conference,
journal, or archive and is under external review.

### Characteristics
- Manuscript content is frozen for the review cycle
- Only minor formatting or administrative changes may occur
- Review outcome is pending

### Required Artifacts
- Final submission version (PDF or source)
- `submission-info.md` documenting:
  - venue
  - submission date
  - paper identifier (if available)

### Transition Criteria
A submitted paper may transition to:
- **preprint**, if publicly released
- **in-progress**, if substantially revised after rejection
- **draft**, if reframed or restarted

---

## preprint

### Definition
A **preprint** is a publicly accessible version of a paper,
typically hosted on platforms such as arXiv or SSRN.

### Characteristics
- Stable reference point for citation
- Content corresponds to a specific submission version
- May coexist with an active in-progress revision

### Required Artifacts
- Public PDF
- `link.md` with external URL
- Identifier (e.g., arXiv ID)

### Notes
Preprints are **additive**, not replacements.
The corresponding `submitted/` or `in-progress/` history is preserved.

---

## Structural Rules

- Status changes **must** be reflected by moving the paper directory
- Status changes **must** include a commit explaining the transition
- Status is not inferred from commit messages alone
- Front-matter `status` must match directory placement

---

## Design Principle

> Status reflects **where the work is in its lifecycle**,  
> not whether the ideas are correct, accepted, or complete.

This repository treats status as an engineering signal,
not an academic judgment.
