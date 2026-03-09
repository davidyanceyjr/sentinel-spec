# Sentinel Specification Development Roadmap

<<<<<<< HEAD
This document tracks the phases used to build and refine the Sentinel specification.

---

## Phase 1 — Raw Section Classification

Status: complete  
Branch: docs/phase1-classification  
Issue: not tracked in Github
=======
This document tracks the phases required to evolve the Sentinel specification
from raw extracted material into a stable canonical specification.

Each phase corresponds to:

- a Git branch
- a GitHub issue
- a Codex CLI prompt
- a milestone deliverable

---

# Phase 1 — Raw Section Classification

Status: complete  
Branch: docs/phase1-classification  
>>>>>>> docs/phase3-structural-review

Objective:
Classify mechanically split sections and determine canonical placement.

<<<<<<< HEAD
---

## Phase 2 — Curated Promotion

Status: complete  
Branch: docs/phase2-promote-curated-draft  
Issue: not tracke in Github
=======
Deliverables:
- mapping plan recorded in PLANS.md
- duplicate heading groups identified
- uncertain classifications recorded

Prompt summary:
Classify files under `archive/raw-heading-split/` and generate a placement plan.

---

# Phase 2 — Curated Promotion

Status: complete  
Branch: docs/phase2-promote-curated-draft  
>>>>>>> docs/phase3-structural-review

Objective:
Promote raw split files into curated repository directories.

<<<<<<< HEAD
---

## Phase 3 — Structural Resolution

Status: complete  
Branch: docs/phase3-structural-review  
Issue: not tracke in Github

=======
Deliverables:
- `core/`, `subsystems/`, and `reference/` populated
- `SPEC.md` updated as canonical entrypoint
- archive preserved as raw source

Prompt summary:
Promote files from archive into curated structure according to PLANS.md.

---

# Phase 3 — Structural Resolution

Status: active  
Branch: docs/phase3-structural-review  
>>>>>>> docs/phase3-structural-review

Objective:
Resolve duplicate sections and clarify canonical boundaries.

<<<<<<< HEAD
---

## Phase 4 — Specification Normalization

Status: complete  
Branch: docs/phase4-normalize-spec  
Issue: #1

Objective:
Normalize canonical specification structure and introduce requirement identifiers.

Outcome:
- Canonical requirement formatting normalized with stable requirement IDs.
- SecObs `1. Scope and Objectives` restored from upstream reconciled source (`sentinel_canonical_spec_v1.1_reconciled.md`).

---

## Phase 5 — Requirement Validation

Status: active  
Issue: #2

Objective:
Ensure all normative requirements are testable.

---

## Phase 6 — Consistency Review

Status: pending  
Issue: #6

Objective:
Detect contradictions across specification sections.

---

## Phase 7 — Final Canonicalization

Status: pending  
Issue: #7

Objective:
Produce the final canonical Sentinel specification.
=======
Inputs:
- duplicate heading groups recorded in PLANS.md
- unresolved items recorded in DECISIONS.md

Deliverables:
- canonical vs reference classification finalized
- duplicate sections resolved or archived
- uncertain placements decided

Prompt summary:
Review duplicate sections and resolve canonical placement without rewriting content.

---

# Phase 4 — Specification Normalization

Status: pending

Objective:
Normalize structure and terminology across the specification.

Tasks:
- introduce requirement identifiers
- normalize headings and section ordering
- separate normative requirements from rationale

Prompt summary:
Normalize specification structure while preserving meaning.

---

# Phase 5 — Requirement Validation Pass

Status: pending

Objective:
Ensure all normative requirements are verifiable.

Tasks:
- identify vague wording
- introduce acceptance criteria
- populate validation/traceability mapping

Prompt summary:
Review requirements for testability and clarity.

---

# Phase 6 — Consistency and Contradiction Review

Status: pending

Objective:
Detect conflicting requirements and duplicated semantics.

Tasks:
- cross-check subsystem requirements
- verify CLI contract consistency
- detect contradictory guarantees

Prompt summary:
Analyze specification for contradictions and overlapping definitions.

---

# Phase 7 — Final Canonicalization

Status: pending

Objective:
Produce the final canonical Sentinel specification.

Deliverables:
- clean canonical spec
- resolved structural duplication
- finalized SPEC.md navigation
- validated acceptance criteria
>>>>>>> docs/phase3-structural-review
