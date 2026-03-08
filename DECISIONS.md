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
- Human follow-up is still required only to determine whether upstream source recovery is needed for missing body text.

### File Movement Summary
- No curated file was moved between canonical and reference directories in Phase 3.
- No archive file was modified.
