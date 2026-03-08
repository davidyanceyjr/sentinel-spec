# Sentinel Specification Development Roadmap

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

Objective:
Classify mechanically split sections and determine canonical placement.

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

Objective:
Promote raw split files into curated repository directories.

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

Objective:
Resolve duplicate sections and clarify canonical boundaries.

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