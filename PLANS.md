# Phase 1 Placement Plan

| source file | classification | destination path | notes |
| --- | --- | --- | --- |
| archive/raw-heading-split/README.md | obsolete-fragment | N/A | Index of archive files only; should remain archival metadata, not canonical spec content. |
| archive/raw-heading-split/sentinel-spec-01-sentinel-canonical-engineering-specification.md | canonical-core | core/00-sentinel-canonical-engineering-specification.md | Core root specification preface. |
| archive/raw-heading-split/sentinel-spec-02-1-system-purpose.md | canonical-core | core/01-system-purpose.md | Core purpose section. |
| archive/raw-heading-split/sentinel-spec-03-2-canonical-architecture.md | canonical-core | core/02-canonical-architecture.md | Core architecture section. |
| archive/raw-heading-split/sentinel-spec-04-3-canonical-event-schema.md | canonical-core | core/03-canonical-event-schema.md | Core event schema definition. |
| archive/raw-heading-split/sentinel-spec-05-4-parser-contract.md | canonical-core | core/04-parser-contract.md | Core parser contract. |
| archive/raw-heading-split/sentinel-spec-06-5-service-identification.md | canonical-core | core/05-service-identification.md | Core service identification rules. |
| archive/raw-heading-split/sentinel-spec-07-6-temporal-segmentation.md | canonical-core | core/06-temporal-segmentation.md | Normative core temporal segmentation. |
| archive/raw-heading-split/sentinel-spec-08-7-rule-definition-model.md | canonical-core | core/07-rule-definition-model.md | Core rule model. |
| archive/raw-heading-split/sentinel-spec-09-8-evidence-model.md | canonical-core | core/08-evidence-model.md | Core normative evidence model. |
| archive/raw-heading-split/sentinel-spec-10-9-finding-output-schema.md | canonical-core | core/09-finding-output-schema.md | Core normative finding schema. |
| archive/raw-heading-split/sentinel-spec-11-10-cli-contract.md | canonical-core | core/10-cli-contract.md | Core CLI contract. |
| archive/raw-heading-split/sentinel-spec-12-11-validation-requirements.md | canonical-core | core/11-validation-requirements.md | Core validation requirements. |
| archive/raw-heading-split/sentinel-spec-13-12-versioning.md | canonical-core | core/12-versioning.md | Core versioning policy. |
| archive/raw-heading-split/sentinel-spec-14-13-original-rule-catalog-and-reference-material.md | reference | reference/original-rule-catalog-and-reference-material.md | Explicitly retained as reference material. |
| archive/raw-heading-split/sentinel-spec-15-sentinel-secobs-canonical-engineering-specification.md | canonical-subsystem | subsystems/secobs/00-sentinel-secobs-canonical-engineering-specification.md | SecObs subsystem root. |
| archive/raw-heading-split/sentinel-spec-16-1-scope-and-objectives.md | uncertain | subsystems/secobs/01-scope-and-objectives.md | Heading-only fragment; likely intended canonical section but content appears missing in source split. |
| archive/raw-heading-split/sentinel-spec-17-journald-security-findings-engine.md | canonical-subsystem | subsystems/journald-findings-engine/00-journald-security-findings-engine.md | Full findings-engine V1 draft. |
| archive/raw-heading-split/sentinel-spec-18-2-system-architecture.md | canonical-subsystem | subsystems/secobs/02-system-architecture.md | SecObs architecture reconciliation section. |
| archive/raw-heading-split/sentinel-spec-19-journald-security-findings-engine.md | canonical-subsystem | subsystems/journald-findings-engine/01-journald-security-findings-engine-overview.md | Findings-engine pipeline overview preface. |
| archive/raw-heading-split/sentinel-spec-20-1-purpose.md | canonical-subsystem | subsystems/journald-findings-engine/02-purpose.md | Findings-engine purpose section. |
| archive/raw-heading-split/sentinel-spec-21-2-architectural-principle.md | canonical-subsystem | subsystems/journald-findings-engine/03-architectural-principle.md | Findings-engine architectural principle section. |
| archive/raw-heading-split/sentinel-spec-22-3-stage-definitions.md | canonical-subsystem | subsystems/journald-findings-engine/04-stage-definitions.md | Findings-engine stage contracts and boundaries. |
| archive/raw-heading-split/sentinel-spec-23-4-evidence-references.md | canonical-subsystem | subsystems/journald-findings-engine/05-evidence-references.md | Findings-engine evidence reference behavior. |
| archive/raw-heading-split/sentinel-spec-24-5-memory-ownership-and-lifetime.md | canonical-subsystem | subsystems/journald-findings-engine/06-memory-ownership-and-lifetime.md | Findings-engine ownership/lifetime rules. |
| archive/raw-heading-split/sentinel-spec-25-6-error-and-warning-propagation.md | canonical-subsystem | subsystems/journald-findings-engine/07-error-and-warning-propagation.md | Findings-engine warning/error propagation model. |
| archive/raw-heading-split/sentinel-spec-26-7-determinism-requirements.md | canonical-subsystem | subsystems/journald-findings-engine/08-determinism-requirements.md | Findings-engine determinism requirements. |
| archive/raw-heading-split/sentinel-spec-27-8-scalability-and-extensibility.md | canonical-subsystem | subsystems/journald-findings-engine/09-scalability-and-extensibility.md | Findings-engine scope/scaling constraints. |
| archive/raw-heading-split/sentinel-spec-28-9-testing-strategy-by-stage.md | canonical-subsystem | subsystems/journald-findings-engine/10-testing-strategy-by-stage.md | Findings-engine testing strategy. |
| archive/raw-heading-split/sentinel-spec-29-10-non-goals-of-this-spec.md | canonical-subsystem | subsystems/journald-findings-engine/11-non-goals-of-this-spec.md | Findings-engine non-goals. |
| archive/raw-heading-split/sentinel-spec-30-11-design-goals.md | canonical-subsystem | subsystems/journald-findings-engine/12-design-goals.md | Findings-engine design goals. |
| archive/raw-heading-split/sentinel-spec-31-12-v1-summary.md | canonical-subsystem | subsystems/journald-findings-engine/13-v1-summary.md | Findings-engine summary section. |
| archive/raw-heading-split/sentinel-spec-32-3-canonical-event-model.md | canonical-subsystem | subsystems/secobs/03-canonical-event-model.md | SecObs canonical event model. |
| archive/raw-heading-split/sentinel-spec-33-4-parser-requirements.md | canonical-subsystem | subsystems/secobs/04-parser-requirements.md | SecObs parser requirements section. |
| archive/raw-heading-split/sentinel-spec-34-journald-security-findings-engine.md | canonical-subsystem | subsystems/journald-parser/00-journald-security-findings-engine.md | Parser subsystem root preface. |
| archive/raw-heading-split/sentinel-spec-35-1-purpose.md | canonical-subsystem | subsystems/journald-parser/01-purpose.md | Parser purpose section. |
| archive/raw-heading-split/sentinel-spec-36-2-supported-input.md | canonical-subsystem | subsystems/journald-parser/02-supported-input.md | Parser supported input section. |
| archive/raw-heading-split/sentinel-spec-37-3-parser-design-requirements.md | canonical-subsystem | subsystems/journald-parser/03-parser-design-requirements.md | Parser design requirements. |
| archive/raw-heading-split/sentinel-spec-38-4-export-record-structure.md | canonical-subsystem | subsystems/journald-parser/04-export-record-structure.md | Parser export record structure section. |
| archive/raw-heading-split/sentinel-spec-39-5-field-format.md | canonical-subsystem | subsystems/journald-parser/05-field-format.md | Parser field format constraints. |
| archive/raw-heading-split/sentinel-spec-40-6-field-name-rules.md | canonical-subsystem | subsystems/journald-parser/06-field-name-rules.md | Parser field name constraints. |
| archive/raw-heading-split/sentinel-spec-41-7-field-value-handling.md | canonical-subsystem | subsystems/journald-parser/07-field-value-handling.md | Parser field value handling rules. |
| archive/raw-heading-split/sentinel-spec-42-8-binary-fields.md | canonical-subsystem | subsystems/journald-parser/08-binary-fields.md | Parser binary field handling. |
| archive/raw-heading-split/sentinel-spec-43-9-record-boundaries.md | canonical-subsystem | subsystems/journald-parser/09-record-boundaries.md | Parser record boundary rules. |
| archive/raw-heading-split/sentinel-spec-44-10-duplicate-fields.md | canonical-subsystem | subsystems/journald-parser/10-duplicate-fields.md | Parser duplicate-field handling. |
| archive/raw-heading-split/sentinel-spec-45-11-error-categories.md | canonical-subsystem | subsystems/journald-parser/11-error-categories.md | Parser error categorization. |
| archive/raw-heading-split/sentinel-spec-46-12-recovery-rules.md | canonical-subsystem | subsystems/journald-parser/12-recovery-rules.md | Parser recovery behavior. |
| archive/raw-heading-split/sentinel-spec-47-13-raw-record-output-contract.md | canonical-subsystem | subsystems/journald-parser/13-raw-record-output-contract.md | Parser raw record output contract. |
| archive/raw-heading-split/sentinel-spec-48-14-parser-limits.md | canonical-subsystem | subsystems/journald-parser/14-parser-limits.md | Parser limits and bounds. |
| archive/raw-heading-split/sentinel-spec-49-15-security-requirements.md | canonical-subsystem | subsystems/journald-parser/15-security-requirements.md | Parser security requirements. |
| archive/raw-heading-split/sentinel-spec-50-16-parser-test-corpus.md | canonical-subsystem | subsystems/journald-parser/16-parser-test-corpus.md | Parser test corpus section. |
| archive/raw-heading-split/sentinel-spec-51-17-complexity-guarantees.md | canonical-subsystem | subsystems/journald-parser/17-complexity-guarantees.md | Parser complexity guarantees. |
| archive/raw-heading-split/sentinel-spec-52-18-output-guarantees.md | canonical-subsystem | subsystems/journald-parser/18-output-guarantees.md | Parser output guarantees. |
| archive/raw-heading-split/sentinel-spec-53-5-classification-and-normalization.md | canonical-subsystem | subsystems/secobs/05-classification-and-normalization.md | SecObs bridge section that defers to pipeline spec. |
| archive/raw-heading-split/sentinel-spec-54-6-temporal-segmentation.md | canonical-subsystem | subsystems/secobs/06-temporal-segmentation.md | SecObs bridge section deferring to core temporal model. |
| archive/raw-heading-split/sentinel-spec-55-7-finding-engine.md | canonical-subsystem | subsystems/secobs/07-finding-engine.md | SecObs high-level finding engine summary. |
| archive/raw-heading-split/sentinel-spec-56-8-rule-catalog.md | duplicate | subsystems/secobs/08-rule-catalog.md | Placeholder parent heading only; detailed rules are in `sentinel-spec-58-rule-catalog.md`. |
| archive/raw-heading-split/sentinel-spec-57-journald-security-findings-engine.md | reference | reference/journald-security-findings-engine-reference.md | Rule-catalog preface retained as reference document. |
| archive/raw-heading-split/sentinel-spec-58-rule-catalog.md | reference | reference/rule-catalog.md | Full detailed rule catalog (non-canonical reference detail). |
| archive/raw-heading-split/sentinel-spec-59-global-threshold-summary.md | reference | reference/global-threshold-summary.md | Threshold quick-reference table. |
| archive/raw-heading-split/sentinel-spec-60-9-evidence-model.md | canonical-subsystem | subsystems/secobs/09-evidence-model.md | SecObs normalized evidence schema (overlaps with core model). |
| archive/raw-heading-split/sentinel-spec-61-10-finding-output-schema.md | canonical-subsystem | subsystems/secobs/10-finding-output-schema.md | SecObs finding schema restatement (overlaps with core schema). |
| archive/raw-heading-split/sentinel-spec-62-11-cli-interface.md | canonical-subsystem | subsystems/secobs/11-cli-interface.md | SecObs CLI section defers to core CLI contract. |
| archive/raw-heading-split/sentinel-spec-63-12-error-handling-and-warnings.md | canonical-subsystem | subsystems/secobs/12-error-handling-and-warnings.md | SecObs warning/error summary defers to pipeline spec. |
| archive/raw-heading-split/sentinel-spec-64-13-testing-and-validation.md | canonical-subsystem | subsystems/secobs/13-testing-and-validation.md | SecObs testing expectations section. |
| archive/raw-heading-split/sentinel-spec-65-14-versioning.md | canonical-subsystem | subsystems/secobs/14-versioning.md | SecObs versioning restatement. |
| archive/raw-heading-split/sentinel-spec-66-appendix.md | canonical-subsystem | subsystems/secobs/appendix.md | SecObs appendix controlling precedence against legacy text. |

## Ambiguities and structural conflicts

### Duplicate headings
- `Journald Security Findings Engine`: appears in `sentinel-spec-17`, `sentinel-spec-19`, `sentinel-spec-34`, `sentinel-spec-57` with different scopes.
- `1. Purpose`: appears in `sentinel-spec-20` (findings engine) and `sentinel-spec-35` (parser).
- `6. Temporal Segmentation`: appears in `sentinel-spec-07` (core normative) and `sentinel-spec-54` (SecObs deferral).
- `8. Rule Catalog` / `Rule Catalog`: appears in `sentinel-spec-56` (placeholder) and `sentinel-spec-58` (full catalog).
- `Evidence Model`: appears in `sentinel-spec-09` (core) and `sentinel-spec-60` (SecObs restatement).
- `Finding Output Schema`: appears in `sentinel-spec-10` (core) and `sentinel-spec-61` (SecObs restatement).
- `Versioning`: appears in `sentinel-spec-13` (core) and `sentinel-spec-65` (SecObs restatement).

### Overlapping sections
- `sentinel-spec-53`, `54`, `62`, `63` are bridge/deferral sections that point to other subsystem/core specs rather than define independent normative detail.
- `sentinel-spec-60`, `61`, `65` restate core concepts with slight wording differences; drift risk exists if both are treated as normative without precedence rules.
- `sentinel-spec-56` overlaps structurally with `sentinel-spec-58` and provides no standalone rule detail.

### Possible subsystem boundaries
- `subsystems/journald-parser`: byte-level decode, input format, field/value handling, record construction, parser guarantees (`sentinel-spec-34` to `52`).
- `subsystems/journald-findings-engine`: post-parse pipeline, stage contracts, evidence propagation, deterministic findings behavior (`sentinel-spec-17`, `19` to `31`).
- `subsystems/secobs`: reconciled/canonical integration layer and normalized cross-cutting summaries (`sentinel-spec-15`, `18`, `32`, `33`, `53` to `66`).
- `reference`: historical or detailed non-canonical rule materials (`sentinel-spec-14`, `57`, `58`, `59`).

### Files that do not belong in the canonical spec
- `archive/raw-heading-split/README.md` (archive index only).
- `archive/raw-heading-split/sentinel-spec-14-13-original-rule-catalog-and-reference-material.md` (explicit reference retention marker).
- `archive/raw-heading-split/sentinel-spec-57-journald-security-findings-engine.md` (reference preface for detailed catalog material).
- `archive/raw-heading-split/sentinel-spec-58-rule-catalog.md` (detailed historical rule catalog in reference domain).
- `archive/raw-heading-split/sentinel-spec-59-global-threshold-summary.md` (reference summary table).

## Summary

- Files classified: **67**
- Duplicate headings detected: **7 groups**
- Uncertain classifications: **1** (`sentinel-spec-16-1-scope-and-objectives.md`)
