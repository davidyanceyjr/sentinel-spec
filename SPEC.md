# Sentinel Specification

This document is the canonical entrypoint for the curated Sentinel specification.
It indexes the promoted specification sections under `core/`, `subsystems/`, and `reference/`.

## Status
- Phase 2 promotion status: complete first-draft structure populated from `archive/raw-heading-split/` per `PLANS.md`.
- Source archive status: preserved; no files were removed or rewritten in `archive/raw-heading-split/`.
- Phase 3 boundary status: duplicate-heading boundaries resolved with explicit canonical precedence in `DECISIONS.md`.
<<<<<<< HEAD
- Phase 4 normalization status: normative sections normalized with requirement IDs for existing normative statements.
=======
>>>>>>> docs/phase3-structural-review

## Core
- [00-sentinel-canonical-engineering-specification.md](core/00-sentinel-canonical-engineering-specification.md)
- [01-system-purpose.md](core/01-system-purpose.md)
- [02-canonical-architecture.md](core/02-canonical-architecture.md)
- [03-canonical-event-schema.md](core/03-canonical-event-schema.md)
- [04-parser-contract.md](core/04-parser-contract.md)
- [05-service-identification.md](core/05-service-identification.md)
- [06-temporal-segmentation.md](core/06-temporal-segmentation.md)
- [07-rule-definition-model.md](core/07-rule-definition-model.md)
- [08-evidence-model.md](core/08-evidence-model.md)
- [09-finding-output-schema.md](core/09-finding-output-schema.md)
- [10-cli-contract.md](core/10-cli-contract.md)
- [11-validation-requirements.md](core/11-validation-requirements.md)
- [12-versioning.md](core/12-versioning.md)

## Subsystems / SecObs
- [00-sentinel-secobs-canonical-engineering-specification.md](subsystems/secobs/00-sentinel-secobs-canonical-engineering-specification.md)
- [01-scope-and-objectives.md](subsystems/secobs/01-scope-and-objectives.md)
- [02-system-architecture.md](subsystems/secobs/02-system-architecture.md)
- [03-canonical-event-model.md](subsystems/secobs/03-canonical-event-model.md)
- [04-parser-requirements.md](subsystems/secobs/04-parser-requirements.md)
- [05-classification-and-normalization.md](subsystems/secobs/05-classification-and-normalization.md)
- [06-temporal-segmentation.md](subsystems/secobs/06-temporal-segmentation.md)
- [07-finding-engine.md](subsystems/secobs/07-finding-engine.md)
- [08-rule-catalog.md](subsystems/secobs/08-rule-catalog.md)
- [09-evidence-model.md](subsystems/secobs/09-evidence-model.md)
- [10-finding-output-schema.md](subsystems/secobs/10-finding-output-schema.md)
- [11-cli-interface.md](subsystems/secobs/11-cli-interface.md)
- [12-error-handling-and-warnings.md](subsystems/secobs/12-error-handling-and-warnings.md)
- [13-testing-and-validation.md](subsystems/secobs/13-testing-and-validation.md)
- [14-versioning.md](subsystems/secobs/14-versioning.md)
- [appendix.md](subsystems/secobs/appendix.md)

## Subsystems / Journald Findings Engine
- [00-journald-security-findings-engine.md](subsystems/journald-findings-engine/00-journald-security-findings-engine.md)
- [01-journald-security-findings-engine-overview.md](subsystems/journald-findings-engine/01-journald-security-findings-engine-overview.md)
- [02-purpose.md](subsystems/journald-findings-engine/02-purpose.md)
- [03-architectural-principle.md](subsystems/journald-findings-engine/03-architectural-principle.md)
- [04-stage-definitions.md](subsystems/journald-findings-engine/04-stage-definitions.md)
- [05-evidence-references.md](subsystems/journald-findings-engine/05-evidence-references.md)
- [06-memory-ownership-and-lifetime.md](subsystems/journald-findings-engine/06-memory-ownership-and-lifetime.md)
- [07-error-and-warning-propagation.md](subsystems/journald-findings-engine/07-error-and-warning-propagation.md)
- [08-determinism-requirements.md](subsystems/journald-findings-engine/08-determinism-requirements.md)
- [09-scalability-and-extensibility.md](subsystems/journald-findings-engine/09-scalability-and-extensibility.md)
- [10-testing-strategy-by-stage.md](subsystems/journald-findings-engine/10-testing-strategy-by-stage.md)
- [11-non-goals-of-this-spec.md](subsystems/journald-findings-engine/11-non-goals-of-this-spec.md)
- [12-design-goals.md](subsystems/journald-findings-engine/12-design-goals.md)
- [13-v1-summary.md](subsystems/journald-findings-engine/13-v1-summary.md)

## Subsystems / Journald Parser
- [00-journald-security-findings-engine.md](subsystems/journald-parser/00-journald-security-findings-engine.md)
- [01-purpose.md](subsystems/journald-parser/01-purpose.md)
- [02-supported-input.md](subsystems/journald-parser/02-supported-input.md)
- [03-parser-design-requirements.md](subsystems/journald-parser/03-parser-design-requirements.md)
- [04-export-record-structure.md](subsystems/journald-parser/04-export-record-structure.md)
- [05-field-format.md](subsystems/journald-parser/05-field-format.md)
- [06-field-name-rules.md](subsystems/journald-parser/06-field-name-rules.md)
- [07-field-value-handling.md](subsystems/journald-parser/07-field-value-handling.md)
- [08-binary-fields.md](subsystems/journald-parser/08-binary-fields.md)
- [09-record-boundaries.md](subsystems/journald-parser/09-record-boundaries.md)
- [10-duplicate-fields.md](subsystems/journald-parser/10-duplicate-fields.md)
- [11-error-categories.md](subsystems/journald-parser/11-error-categories.md)
- [12-recovery-rules.md](subsystems/journald-parser/12-recovery-rules.md)
- [13-raw-record-output-contract.md](subsystems/journald-parser/13-raw-record-output-contract.md)
- [14-parser-limits.md](subsystems/journald-parser/14-parser-limits.md)
- [15-security-requirements.md](subsystems/journald-parser/15-security-requirements.md)
- [16-parser-test-corpus.md](subsystems/journald-parser/16-parser-test-corpus.md)
- [17-complexity-guarantees.md](subsystems/journald-parser/17-complexity-guarantees.md)
- [18-output-guarantees.md](subsystems/journald-parser/18-output-guarantees.md)

## Reference
- [global-threshold-summary.md](reference/global-threshold-summary.md)
- [journald-security-findings-engine-reference.md](reference/journald-security-findings-engine-reference.md)
- [original-rule-catalog-and-reference-material.md](reference/original-rule-catalog-and-reference-material.md)
- [rule-catalog.md](reference/rule-catalog.md)

## Validation and Repo Control
- [acceptance-criteria.md](validation/acceptance-criteria.md)
- [traceability-matrix.md](validation/traceability-matrix.md)
- [PLANS.md](PLANS.md)
- [DECISIONS.md](DECISIONS.md)
- [CHANGELOG.md](CHANGELOG.md)
- [STYLE.md](STYLE.md)
- [glossary.md](glossary.md)

## Archive
- [Raw heading split index](archive/raw-heading-split/README.md)

## Structural Boundary Notes
- Canonical precedence for overlapping sections is defined in `DECISIONS.md` (Phase 3 entry).
<<<<<<< HEAD
- Requirement ID scheme and normalization scope are defined in `DECISIONS.md` (Phase 4 entry).
- `subsystems/secobs/08-rule-catalog.md` is a canonical bridge pointer; detailed rule catalog content is reference-only.
- `subsystems/secobs/01-scope-and-objectives.md` is restored from upstream reconciled source with scope/objective-relevant content.
=======
- `subsystems/secobs/08-rule-catalog.md` is a canonical bridge pointer; detailed rule catalog content is reference-only.
- `subsystems/secobs/01-scope-and-objectives.md` remains a canonical structural placeholder from a heading-only source fragment.
>>>>>>> docs/phase3-structural-review
- Reference-only files intentionally excluded from canonical spec body:
  - `archive/raw-heading-split/sentinel-spec-14-13-original-rule-catalog-and-reference-material.md`
  - `archive/raw-heading-split/sentinel-spec-57-journald-security-findings-engine.md`
  - `archive/raw-heading-split/sentinel-spec-58-rule-catalog.md`
  - `archive/raw-heading-split/sentinel-spec-59-global-threshold-summary.md`
