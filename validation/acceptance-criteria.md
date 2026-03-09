# Acceptance Criteria

This document defines objective acceptance checks for currently identified
normative requirement IDs in canonical specification files.

## Requirement Acceptance Criteria

| Acceptance ID | Requirement ID | Acceptance Condition (pass/fail) |
| --- | --- | --- |
| AC-CORE-ARCH-001 | CORE-ARCH-001 | Execution traces show top-level stages run in order: Parser -> Classifier -> Finding Engine -> Output Generator. |
| AC-CORE-EVENT-001 | CORE-EVENT-001 | At each normalized-event handoff, exchanged payloads conform to the CanonicalEvent field set defined in `core/03-canonical-event-schema.md`. |
| AC-CORE-EVENT-002 | CORE-EVENT-002 | Tests with placeholder field values and `has_* = false` confirm downstream logic treats the field as absent and does not infer presence from placeholders. |
| AC-CORE-EVENT-003 | CORE-EVENT-003 | For `priority`, `process_id`, `user_id`, and `group_id`, successful conversion yields typed values; failed conversion does not populate typed values. |
| AC-CORE-EVENT-004 | CORE-EVENT-004 | After normalization, downstream stages do not modify `record_index`, `timestamp`, `has_timestamp`, `boot_id`, or `has_boot_id`. |
| AC-CORE-PARSER-001 | CORE-PARSER-001 | Decoded records receive monotonic `record_index` assignments across a dataset. |
| AC-CORE-PARSER-002 | CORE-PARSER-002 | Non-fatal malformed records are tolerated per recovery requirements `JPARSER-RECOVERY-001` to `JPARSER-RECOVERY-003` and do not force whole-dataset failure; discarded malformed records are surfaced as warnings. |
| AC-CORE-SVC-001 | CORE-SVC-001 | Canonical service names match `<unit-name>.<unit-type>`, with non-empty `<unit-name>` and lowercase alphabetic `<unit-type>`. |
| AC-CORE-RULE-001 | CORE-RULE-001 | Rule objects include the required fields listed by the rule definition model (`rule_id`, `description`, `severity`, `confidence`, `trigger_conditions`, `context_fields`, `evidence_fields`). |
| AC-CORE-RULE-002 | CORE-RULE-002 | No unknown top-level rule fields are present; optional extension fields, when present, are contained only within top-level `extensions`. |
| AC-CORE-EVID-001 | CORE-EVID-001 | Every `EvidenceRef.record_index` resolves to an existing CanonicalEvent `record_index` in the analyzed dataset. |
| AC-CORE-EVID-002 | CORE-EVID-002 | V1 evidence identity does not rely on any `event_id` field. |
| AC-CORE-EVID-003 | CORE-EVID-003 | Optional evidence presentation fields, when present in rendered output, are treated as derived fields and not as EvidenceRef identity fields. |
| AC-CORE-EVID-004 | CORE-EVID-004 | If retained evidence exceeds the active evidence limit, output evidence references are truncated to that limit. |
| AC-CORE-EVID-005 | CORE-EVID-005 | If evidence is truncated, warning `evidence_clipped` is emitted. |
| AC-CORE-FIND-001 | CORE-FIND-001 | `Finding.evidence_refs[]` elements validate as `EvidenceRef` objects. |
| AC-CORE-FIND-002 | CORE-FIND-002 | `Finding.evidence_count` equals the count of retained `evidence_refs[]`. |
| AC-CORE-FIND-003 | CORE-FIND-003 | `context` is JSON-serializable and serialized UTF-8 JSON size is `<= 4096` bytes. |
| AC-CLI-001 | CLI-001 | Fatal parser processing failure causes CLI exit status to be non-zero. |
| AC-CLI-002 | CLI-002 | Presence of warnings alone does not terminate execution. |
| AC-CLI-003 | CLI-003 | CLI invocation without any one of `--input`, `--output`, or `--rules` fails argument validation. |
| AC-CORE-VAL-001 | CORE-VAL-001 | Test suite includes explicit coverage for parser validation, CanonicalEvent schema validation, rule trigger behavior, evidence clipping behavior, and full pipeline execution. |
| AC-SECOBS-EVENT-001 | SECOBS-EVENT-001 | Parser and normalization outputs conform exactly to the SecObs CanonicalEvent schema and remain compatible with core CanonicalEvent requirements. |
| AC-JPARSER-RECOVERY-001 | JPARSER-RECOVERY-001 | Field-level decode errors do not terminate record parsing; parser continues processing current record. |
| AC-JPARSER-RECOVERY-002 | JPARSER-RECOVERY-002 | Record structural errors cause current record discard and resynchronization at next record boundary. |
| AC-JPARSER-RECOVERY-003 | JPARSER-RECOVERY-003 | Stream structural errors cause parser abort. |
| AC-JFE-BASE-001-020 | JFE-BASE-001..020 | The findings-engine baseline behaviors formalized in `JFE-BASE-001` through `JFE-BASE-020` are each verified by focused subsystem tests and/or schema/contract checks. |
| AC-JFE-STAGE-001-011 | JFE-STAGE-001..011 | Stage-boundary and stage-behavior tests verify each requirement `JFE-STAGE-001` through `JFE-STAGE-011`. |
| AC-JFE-MEM-001-004 | JFE-MEM-001..004 | Ownership/lifetime tests verify parser buffer immutability and owned-data retention constraints in `JFE-MEM-001` through `JFE-MEM-004`. |
| AC-JFE-DET-001-006 | JFE-DET-001..006 | Determinism tests verify constraints in `JFE-DET-001` through `JFE-DET-006`, including identical-input output stability. |
| AC-JPARSER-DESIGN-001-007 | JPARSER-DESIGN-001..007 | Parser architecture tests verify single-pass, byte-oriented, bounded-memory, and bounded-byte-inspection behavior. |
| AC-JPARSER-BOUNDARY-001-004 | JPARSER-BOUNDARY-001..004 | Record-boundary tests verify emit/reset/index increment behavior and EOF final-record handling. |
| AC-JPARSER-DUP-001-003 | JPARSER-DUP-001..003 | Duplicate-field tests verify first-occurrence-wins retention and duplicate warning emission. |
| AC-JPARSER-RAW-001 | JPARSER-RAW-001 | Downstream integration tests verify parser buffers remain immutable after parser emission. |
| AC-JPARSER-SEC-001-005 | JPARSER-SEC-001..005 | Security tests verify overflow, length, malformed-input, and bounds-check defenses. |
| AC-JPARSER-CPLX-001-004 | JPARSER-CPLX-001..004 | Complexity tests verify linear/single-pass/bounded-memory behavior and no superlinear degradation on malformed inputs. |
| AC-JFE-EVID-001-003 | JFE-EVID-001..003 | Evidence-reference tests verify required V1 identity shape and monotonic/non-negative record-index constraints, and permit only documented future extensibility semantics. |
| AC-JFE-TEST-001-007 | JFE-TEST-001..007 | Stage-specific test suites verify parser, normalization, classification, rule, renderer, and end-to-end coverage, with independent stage testability. |
| AC-JFE-GOAL-001-006 | JFE-GOAL-001..006 | Design-goal conformance checks verify offline-first operation, determinism, bounded resources, separation of concerns, fixture testability, and forward compatibility intent. |
| AC-JPARSER-EXPORT-001-003 | JPARSER-EXPORT-001..003 | Export-structure tests verify `FIELD=VALUE` lines, blank-line record termination, and EOF final-record allowance. |
| AC-JPARSER-BIN-001-006 | JPARSER-BIN-001..006 | Binary-field decoding tests verify length read/limit enforcement/exact-byte consumption and malformed-length recovery behavior. |
| AC-JPARSER-CORPUS-001-011 | JPARSER-CORPUS-001..011 | Corpus inventory audit verifies all required parser test cases are present. |
| AC-JPARSER-OUT-001-004 | JPARSER-OUT-001..004 | Output-contract tests verify monotonic record indices, structural field validity, warning anomaly signaling, and field-order non-reliance. |

## Validation Gaps

No open validation gaps are currently tracked for the normalized requirement set in scope.
