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
- Follow-up status superseded by the Phase 4 Normalization Policy Lock disposition.

### File Movement Summary
- No curated file was moved between canonical and reference directories in Phase 3.
- No archive file was modified.

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

## 2026-03-09 - Phase 5 Requirement Validation and Testability Baseline

### Decision
Establish a first-pass validation baseline by mapping all currently ID-backed
canonical requirements to explicit acceptance criteria and a traceability matrix,
while recording unresolved ambiguity as validation gaps instead of introducing
new behavioral assumptions.

### Outcome
- `validation/acceptance-criteria.md` now contains acceptance checks for all
  currently identified requirement IDs in `core/` and `subsystems/secobs/`.
- `validation/traceability-matrix.md` now maps requirement IDs to source files,
  acceptance criteria IDs, verification methods, and readiness status.
- `core/02-canonical-architecture.md` wording is tightened for `CORE-ARCH-001`
  to make the required top-level stage order explicit.
- `core/10-cli-contract.md` wording is tightened for `CLI-001`, and `CLI-003`
  is added to formalize already-declared required flags (`--input`, `--output`,
  `--rules`) as a testable requirement.

### Validation Gaps Recorded
- `VG-001`: `CORE-SVC-001` does not define a formal conformance rule for
  "systemd unit format".
- `VG-002`: `CORE-RULE-001` does not explicitly define strictness for extra
  fields/cardinality in rule objects.
- `VG-003`: `CORE-FIND-003` requires bounded `context`, but no concrete bound
  is defined.
- `VG-004`: `CORE-PARSER-002` references parser recovery behavior that exists
  in parser subsystem documents but is not fully normalized into requirement IDs.
- `VG-005`: Multiple subsystem files in
  `subsystems/journald-findings-engine/` and `subsystems/journald-parser/`
  contain normative-style statements without requirement IDs, reducing
  validation traceability coverage.

## 2026-03-09 - Phase 5 Validation Gap Resolution Update

### Decision
Apply explicit requirement-level resolutions for validation gaps `VG-001`
through `VG-004` using narrowly scoped normative wording updates.

### Outcome
- `VG-001` resolved:
  - `CORE-SVC-001` now defines systemd unit naming shape as
    `<unit-name>.<unit-type>` with non-empty `<unit-name>` and lowercase
    alphabetic `<unit-type>`.
- `VG-002` resolved:
  - `CORE-RULE-001` now explicitly defines required top-level rule fields.
  - New requirement `CORE-RULE-002` constrains optional extension data to a
    top-level `extensions` object and disallows unknown top-level fields.
- `VG-003` resolved:
  - `CORE-FIND-003` now defines bounded `context` as UTF-8 JSON serialized
    size of no more than 4096 bytes.
- `VG-004` resolved:
  - `subsystems/journald-parser/12-recovery-rules.md` now includes
    `JPARSER-RECOVERY-001` through `JPARSER-RECOVERY-003`.
  - `CORE-PARSER-002` now explicitly references those recovery requirements.

### Remaining Open Gap
- `VG-005` remains open for subsystem documents containing normative-style
  statements without requirement IDs.

## 2026-03-09 - Phase 5 VG-005 Narrow Normalization Pass

### Decision
Execute a narrow requirement-ID normalization pass for the 10 files explicitly
listed under `VG-005`, without broad structural rewrite or semantic expansion.

### Outcome
- Added requirement-ID backed normative sections to:
  - `subsystems/journald-findings-engine/00-journald-security-findings-engine.md`
  - `subsystems/journald-findings-engine/04-stage-definitions.md`
  - `subsystems/journald-findings-engine/06-memory-ownership-and-lifetime.md`
  - `subsystems/journald-findings-engine/08-determinism-requirements.md`
  - `subsystems/journald-parser/03-parser-design-requirements.md`
  - `subsystems/journald-parser/09-record-boundaries.md`
  - `subsystems/journald-parser/10-duplicate-fields.md`
  - `subsystems/journald-parser/13-raw-record-output-contract.md`
  - `subsystems/journald-parser/15-security-requirements.md`
  - `subsystems/journald-parser/17-complexity-guarantees.md`
- Added validation coverage rows for new requirement-ID ranges in:
  - `validation/acceptance-criteria.md`
  - `validation/traceability-matrix.md`

### Residual Gap Status
- `VG-005` is narrowed but not fully closed.
- Remaining non-ID normative-style statements are currently tracked in:
  - `subsystems/journald-findings-engine/05-evidence-references.md`
  - `subsystems/journald-findings-engine/10-testing-strategy-by-stage.md`
  - `subsystems/journald-findings-engine/12-design-goals.md`
  - `subsystems/journald-parser/04-export-record-structure.md`
  - `subsystems/journald-parser/08-binary-fields.md`
  - `subsystems/journald-parser/16-parser-test-corpus.md`
  - `subsystems/journald-parser/18-output-guarantees.md`

## 2026-03-09 - Phase 5 VG-005 Second Narrow Pass and Closure

### Decision
Execute a second narrow requirement-ID normalization pass for the residual
`VG-005` file set and close `VG-005` if no in-scope subsystem file with
normative language remains without requirement IDs.

### Outcome
- Added requirement-ID backed normative sections to:
  - `subsystems/journald-findings-engine/05-evidence-references.md`
  - `subsystems/journald-findings-engine/10-testing-strategy-by-stage.md`
  - `subsystems/journald-findings-engine/12-design-goals.md`
  - `subsystems/journald-parser/04-export-record-structure.md`
  - `subsystems/journald-parser/08-binary-fields.md`
  - `subsystems/journald-parser/16-parser-test-corpus.md`
  - `subsystems/journald-parser/18-output-guarantees.md`
- Added corresponding acceptance and traceability coverage rows in:
  - `validation/acceptance-criteria.md`
  - `validation/traceability-matrix.md`

### Verification and Disposition
- Verification scan result: no file in
  `subsystems/journald-findings-engine/` or `subsystems/journald-parser/`
  containing normative language (`MUST/SHOULD/MAY` forms) is currently without
  at least one requirement ID.
- `VG-005` is closed for the normalized scope.
