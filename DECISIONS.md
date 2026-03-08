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
