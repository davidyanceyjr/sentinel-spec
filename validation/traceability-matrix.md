# Traceability Matrix

This matrix maps requirement IDs to source documents and acceptance criteria.

| Requirement ID | Source | Acceptance ID | Verification Method | Status | Notes |
| --- | --- | --- | --- | --- | --- |
| CORE-ARCH-001 | `core/02-canonical-architecture.md` | AC-CORE-ARCH-001 | Integration pipeline-order test | Ready | Top-level stage order only. |
| CORE-EVENT-001 | `core/03-canonical-event-schema.md` | AC-CORE-EVENT-001 | Schema conformance tests at stage boundaries | Ready | CanonicalEvent authority is core schema. |
| CORE-EVENT-002 | `core/03-canonical-event-schema.md` | AC-CORE-EVENT-002 | Negative/edge fixture tests for `has_*` semantics | Ready | Placeholder-driven inference prohibited. |
| CORE-EVENT-003 | `core/03-canonical-event-schema.md` | AC-CORE-EVENT-003 | Typed-field conversion tests | Ready | Success/failure conversion paths required. |
| CORE-EVENT-004 | `core/03-canonical-event-schema.md` | AC-CORE-EVENT-004 | Immutability regression tests across downstream stages | Ready | Applies after normalization. |
| CORE-PARSER-001 | `core/04-parser-contract.md` | AC-CORE-PARSER-001 | Parser sequence-index tests | Ready | Monotonic assignment required. |
| CORE-PARSER-002 | `core/04-parser-contract.md` | AC-CORE-PARSER-002 | Parser recovery and non-fatal-malformed-input tests | Ready | Recovery behavior is now mapped to JPARSER recovery requirements. |
| CORE-SVC-001 | `core/05-service-identification.md` | AC-CORE-SVC-001 | Service-name format conformance tests | Ready | Uses explicit `<unit-name>.<unit-type>` shape. |
| CORE-RULE-001 | `core/07-rule-definition-model.md` | AC-CORE-RULE-001 | Rule schema validation tests | Ready | Required top-level fields explicitly defined. |
| CORE-RULE-002 | `core/07-rule-definition-model.md` | AC-CORE-RULE-002 | Rule top-level strictness and extension-container tests | Ready | Optional extension data is constrained to top-level `extensions`. |
| CORE-EVID-001 | `core/08-evidence-model.md` | AC-CORE-EVID-001 | Referential integrity tests | Ready | `record_index` must resolve to CanonicalEvent set. |
| CORE-EVID-002 | `core/08-evidence-model.md` | AC-CORE-EVID-002 | Evidence schema compliance tests | Ready | `event_id` identity dependency disallowed in V1. |
| CORE-EVID-003 | `core/08-evidence-model.md` | AC-CORE-EVID-003 | Output schema separation tests | Ready | Derived presentation fields are non-identity. |
| CORE-EVID-004 | `core/08-evidence-model.md` | AC-CORE-EVID-004 | Evidence clipping limit tests | Ready | Truncation required when limit exceeded. |
| CORE-EVID-005 | `core/08-evidence-model.md` | AC-CORE-EVID-005 | Warning emission tests | Ready | `evidence_clipped` warning required on truncation. |
| CORE-FIND-001 | `core/09-finding-output-schema.md` | AC-CORE-FIND-001 | Finding schema validation tests | Ready | `evidence_refs[]` element typing enforced. |
| CORE-FIND-002 | `core/09-finding-output-schema.md` | AC-CORE-FIND-002 | Finding count-consistency tests | Ready | `evidence_count` equality to retained refs required. |
| CORE-FIND-003 | `core/09-finding-output-schema.md` | AC-CORE-FIND-003 | JSON serialization and size-bound tests | Ready | UTF-8 JSON serialization bound is 4096 bytes. |
| CLI-001 | `core/10-cli-contract.md` | AC-CLI-001 | CLI fatal-parser-failure exit-code tests | Ready | Non-zero status required. |
| CLI-002 | `core/10-cli-contract.md` | AC-CLI-002 | CLI warning-only execution tests | Ready | Warnings alone cannot terminate execution. |
| CLI-003 | `core/10-cli-contract.md` | AC-CLI-003 | CLI required-argument validation tests | Ready | `--input`, `--output`, and `--rules` are required. |
| CORE-VAL-001 | `core/11-validation-requirements.md` | AC-CORE-VAL-001 | Test-plan coverage audit | Ready | Presence of listed test categories required. |
| SECOBS-EVENT-001 | `subsystems/secobs/03-canonical-event-model.md` | AC-SECOBS-EVENT-001 | Parser/normalizer output schema conformance tests | Ready | Overlaps core event schema requirements by design. |
| JPARSER-RECOVERY-001 | `subsystems/journald-parser/12-recovery-rules.md` | AC-JPARSER-RECOVERY-001 | Parser field-error recovery tests | Ready | Field-level errors continue current record processing. |
| JPARSER-RECOVERY-002 | `subsystems/journald-parser/12-recovery-rules.md` | AC-JPARSER-RECOVERY-002 | Parser record-structural-error recovery tests | Ready | Record is discarded and parser resynchronizes at next boundary. |
| JPARSER-RECOVERY-003 | `subsystems/journald-parser/12-recovery-rules.md` | AC-JPARSER-RECOVERY-003 | Parser stream-structural-error fatal tests | Ready | Stream structural error causes parser abort. |
| JFE-BASE-001..020 | `subsystems/journald-findings-engine/00-journald-security-findings-engine.md` | AC-JFE-BASE-001-020 | Findings-engine baseline behavior tests | Ready | Added in VG-005 narrow normalization pass. |
| JFE-STAGE-001..011 | `subsystems/journald-findings-engine/04-stage-definitions.md` | AC-JFE-STAGE-001-011 | Stage contract and boundary tests | Ready | Added in VG-005 narrow normalization pass. |
| JFE-MEM-001..004 | `subsystems/journald-findings-engine/06-memory-ownership-and-lifetime.md` | AC-JFE-MEM-001-004 | Memory ownership/lifetime tests | Ready | Added in VG-005 narrow normalization pass. |
| JFE-DET-001..006 | `subsystems/journald-findings-engine/08-determinism-requirements.md` | AC-JFE-DET-001-006 | Determinism/non-env-dependence tests | Ready | Added in VG-005 narrow normalization pass. |
| JPARSER-DESIGN-001..007 | `subsystems/journald-parser/03-parser-design-requirements.md` | AC-JPARSER-DESIGN-001-007 | Parser design-contract tests | Ready | Added in VG-005 narrow normalization pass. |
| JPARSER-BOUNDARY-001..004 | `subsystems/journald-parser/09-record-boundaries.md` | AC-JPARSER-BOUNDARY-001-004 | Record boundary and EOF handling tests | Ready | Added in VG-005 narrow normalization pass. |
| JPARSER-DUP-001..003 | `subsystems/journald-parser/10-duplicate-fields.md` | AC-JPARSER-DUP-001-003 | Duplicate-field policy tests | Ready | Added in VG-005 narrow normalization pass. |
| JPARSER-RAW-001 | `subsystems/journald-parser/13-raw-record-output-contract.md` | AC-JPARSER-RAW-001 | Parser buffer immutability tests | Ready | Added in VG-005 narrow normalization pass. |
| JPARSER-SEC-001..005 | `subsystems/journald-parser/15-security-requirements.md` | AC-JPARSER-SEC-001-005 | Parser security hardening tests | Ready | Added in VG-005 narrow normalization pass. |
| JPARSER-CPLX-001..004 | `subsystems/journald-parser/17-complexity-guarantees.md` | AC-JPARSER-CPLX-001-004 | Parser complexity/regression tests | Ready | Added in VG-005 narrow normalization pass. |
| JFE-EVID-001..003 | `subsystems/journald-findings-engine/05-evidence-references.md` | AC-JFE-EVID-001-003 | Evidence-reference schema and monotonic-index tests | Ready | Added in VG-005 second narrow pass. |
| JFE-TEST-001..007 | `subsystems/journald-findings-engine/10-testing-strategy-by-stage.md` | AC-JFE-TEST-001-007 | Test-strategy coverage audit | Ready | Added in VG-005 second narrow pass. |
| JFE-GOAL-001..006 | `subsystems/journald-findings-engine/12-design-goals.md` | AC-JFE-GOAL-001-006 | Design-goal conformance checks | Ready | Added in VG-005 second narrow pass. |
| JPARSER-EXPORT-001..003 | `subsystems/journald-parser/04-export-record-structure.md` | AC-JPARSER-EXPORT-001-003 | Export-record structure parsing tests | Ready | Added in VG-005 second narrow pass. |
| JPARSER-BIN-001..006 | `subsystems/journald-parser/08-binary-fields.md` | AC-JPARSER-BIN-001-006 | Binary-field parsing and recovery tests | Ready | Added in VG-005 second narrow pass. |
| JPARSER-CORPUS-001..011 | `subsystems/journald-parser/16-parser-test-corpus.md` | AC-JPARSER-CORPUS-001-011 | Parser corpus inventory checks | Ready | Added in VG-005 second narrow pass. |
| JPARSER-OUT-001..004 | `subsystems/journald-parser/18-output-guarantees.md` | AC-JPARSER-OUT-001-004 | Parser output contract tests | Ready | Added in VG-005 second narrow pass. |

## Open Traceability Gaps

No open traceability gaps are currently tracked for the normalized requirement set in scope.
