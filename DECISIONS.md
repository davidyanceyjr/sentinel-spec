# Decisions Log

Record major architectural or specification decisions.

## 2026-03-08 - Phase 2 Promotion Baseline

### Decision
Promote raw heading-split content into curated destinations exactly per `PLANS.md` mapping without semantic rewrite.

### Outcome
- Curated files in `core/`, `subsystems/secobs/`, `subsystems/journald-findings-engine/`, `subsystems/journald-parser/`, and `reference/` are populated from `archive/raw-heading-split/`.
- `SPEC.md` is the canonical entrypoint for curated navigation.
- `archive/raw-heading-split/` remains intact.

### Unresolved Items Carried Forward
- Duplicate-classified item:
  - `archive/raw-heading-split/sentinel-spec-56-8-rule-catalog.md`
- Uncertain item requiring human judgment on source completeness:
  - `archive/raw-heading-split/sentinel-spec-16-1-scope-and-objectives.md`
- Reference-only (intentionally non-canonical) items:
  - `archive/raw-heading-split/sentinel-spec-14-13-original-rule-catalog-and-reference-material.md`
  - `archive/raw-heading-split/sentinel-spec-57-journald-security-findings-engine.md`
  - `archive/raw-heading-split/sentinel-spec-58-rule-catalog.md`
  - `archive/raw-heading-split/sentinel-spec-59-global-threshold-summary.md`

## 2026-03-08 - Phase 3 Structural Boundary Resolution

### Decision
Resolve duplicate-heading boundary ambiguity by defining canonical precedence and section scope without changing normative intent.

### Duplicate Group Dispositions
- `Journald Security Findings Engine`:
  - `subsystems/journald-findings-engine/00-journald-security-findings-engine.md` is canonical for findings-engine V1 draft behavior.
  - `subsystems/journald-findings-engine/01-journald-security-findings-engine-overview.md` is canonical overview context.
  - `subsystems/journald-parser/00-journald-security-findings-engine.md` is canonical parser-scope preface.
  - `reference/journald-security-findings-engine-reference.md` is reference-only.
- `1. Purpose`:
  - `subsystems/journald-findings-engine/02-purpose.md` and `subsystems/journald-parser/01-purpose.md` are both canonical within their subsystem scope.
- `6. Temporal Segmentation`:
  - `core/06-temporal-segmentation.md` is canonical authority.
  - `subsystems/secobs/06-temporal-segmentation.md` is canonical bridge text that defers to core.
- `8. Rule Catalog` / `Rule Catalog`:
  - `subsystems/secobs/08-rule-catalog.md` is retained as canonical bridge pointer only (no detailed rule definitions).
  - `reference/rule-catalog.md` remains reference-only detail.
- `Evidence Model`:
  - `core/08-evidence-model.md` is canonical authority.
  - `subsystems/secobs/09-evidence-model.md` is retained with explicit precedence note to core.
- `Finding Output Schema`:
  - `core/09-finding-output-schema.md` is canonical authority.
  - `subsystems/secobs/10-finding-output-schema.md` is retained with explicit precedence note to core.
- `Versioning`:
  - `core/12-versioning.md` is canonical authority.
  - `subsystems/secobs/14-versioning.md` is retained with explicit precedence note to core.

### Uncertain Placement Disposition
- `archive/raw-heading-split/sentinel-spec-16-1-scope-and-objectives.md` is retained in
  `subsystems/secobs/01-scope-and-objectives.md` as canonical structural placeholder with an explicit note that the source fragment is heading-only.
<<<<<<< HEAD
- Follow-up status superseded by the Phase 4 Normalization Policy Lock disposition.
=======
- Human follow-up is still required only to determine whether upstream source recovery is needed for missing body text.
>>>>>>> docs/phase3-structural-review

### File Movement Summary
- No curated file was moved between canonical and reference directories in Phase 3.
- No archive file was modified.
<<<<<<< HEAD

## 2026-03-08 - Phase 4 Normalization Baseline

### Decision
Normalize requirement formatting in-place for canonical files with existing normative language by adding explicit `Normative Requirements` sections and stable requirement identifiers.

### Requirement ID Scheme
- Core architecture: `CORE-ARCH-###`
- Core event schema: `CORE-EVENT-###`
- Core parser contract: `CORE-PARSER-###`
- Core service identification: `CORE-SVC-###`
- Core rule definition model: `CORE-RULE-###`
- Core evidence model: `CORE-EVID-###`
- Core finding schema: `CORE-FIND-###`
- CLI contract: `CLI-###`
- Core validation: `CORE-VAL-###`
- SecObs canonical event model: `SECOBS-EVENT-###`

### Scope of Normalization
- Applied to existing normative statements only.
- No requirements were added, removed, or broadened.
- No canonical content was moved to `reference/`, `architecture/`, or `decisions/` during this pass because no clearly separable non-normative block was identified that could be moved without fragmenting section context.

### Follow-up
- Remaining canonical files without explicit IDs are descriptive/bridge content in this pass and can be evaluated in Phase 5 if additional normative statements are introduced or clarified.

## 2026-03-08 - Phase 4 Normalization Policy Lock

### Decision
Adopt explicit normalization policy for requirement IDs and missing-source handling as documented in `STYLE.md`.

### Policy Applied
- Requirement IDs are mandatory for explicit normative statements in canonical files.
- Descriptive/bridge text does not receive requirement IDs unless it contains explicit normative requirements.
- Missing-source or heading-only sections are retained as placeholders with explicit source-gap notes and tracked decisions.

### Disposition Applied
- Upstream source file `sentinel_canonical_spec_v1.1_reconciled.md` was identified and reviewed.
- `subsystems/secobs/01-scope-and-objectives.md` is updated with source-derived scope/objective content from the upstream `# 1. Scope and Objectives` section.
- The recovered text is limited to scope/objective-relevant subsections (`Product Definition`, `Mission`, `Non-Goals`, `Target Use Cases`) to avoid duplicating detailed downstream section content already curated elsewhere.
=======
>>>>>>> docs/phase3-structural-review
