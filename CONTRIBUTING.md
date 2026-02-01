# Contributing Guide

This repository documents research work at different stages of maturity.
Its contribution model prioritizes **clarity of intent, traceability of state,
and separation between content evolution and lifecycle transitions**.

Contributions are governed by the following principles.

---

## Core Principles

### 1. Content and Status Are Separate

- **Content** lives inside files.
- **Status** is expressed by directory placement and commit history.

Files do **not** encode status metadata.
Status changes must be structural.

---

### 2. Artifact Types and Expectations

This repository contains research papers in multiple lifecycle states:

- `drafts/`  
  Exploratory work written primarily in Markdown.

- `in-progress/`  
  Structured manuscripts under active development.

- `submitted/`  
  Submission-ready manuscripts under formal review.

- `preprints/`  
  Publicly available reference versions (e.g., arXiv, SSRN).

Each directory reflects a **distinct lifecycle stage**, not content quality.

---

## Contribution Types

All contributions fall into one of two categories.
These categories must **never be mixed in a single commit**.

---

### A. Content Changes

Content changes modify the substance of a paper without altering its lifecycle state.

**Examples**
- Revising arguments
- Adding or removing sections
- Editing figures or notes
- Refining language or structure

**Rules**
- Do not move directories
- Do not change paper status
- `index.md` is not updated unless a new paper is introduced

**Commit Message Format**

```
Draft: refine argument on decision vacancy  
Paper: revise evaluation section  
Paper: clarify scope and terminology
```

Use `Draft:` only for papers under `drafts/`.  
Use `Paper:` for all other content changes.

---

### B. Status Changes

Status changes represent lifecycle transitions and are treated as **structural events**.

**Examples**
- Draft → In-progress
- In-progress → Submitted
- Submitted → Preprint

**Required Actions**
- Move the paper directory to the appropriate status folder
- Update `index.md` to reflect the new status and location
- Do not make substantive content changes in the same commit

**Commit Message Format**

```
Status -> in-progress: adapting-se-for-ai  
Status -> submitted: decision-vacancy (arXiv)  
Status -> preprint: decision-vacancy (arXiv:2601.xxxxx)
```

---

## Updating `index.md`

`index.md` serves as the **single source of truth** for paper status and location.

Update `index.md` only when:
- A new paper is added
- A paper changes lifecycle status
- A public reference (preprint) becomes available

Do **not** update `index.md` for routine content edits.

---

## File Formats

- Drafts are expected to be written in Markdown.
- Submitted and preprint versions retain their original submission formats
  (e.g., PDF, LaTeX).
- No file is required to encode lifecycle status internally.

---

## Design Rationale

This repository treats lifecycle state as an **engineering signal**, not an editorial judgment.

Separating content evolution from status transitions ensures:
- Clear commit history
- Auditable research progression
- Minimal friction during active writing

---

## Summary

- Content changes and status changes are intentionally separated.
- Status is determined by directory placement, not file metadata.
- Each commit should communicate **one kind of intent** clearly.

This structure reflects how research evolves in practice,
not how it is finalized for publication.
