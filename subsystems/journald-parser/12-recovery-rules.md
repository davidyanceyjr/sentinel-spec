# 12. Recovery Rules

## Normative Requirements

- `[JPARSER-RECOVERY-001]` On field-level decode error, the parser MUST continue processing the current record.
- `[JPARSER-RECOVERY-002]` On record structural error, the parser MUST discard the current record and resume scanning for the next record boundary.
- `[JPARSER-RECOVERY-003]` On stream structural error, the parser MUST abort parsing.

## Recovery Summary

Field error:
continue record

Record structural error:
discard record scan for next boundary

Stream structural error:
abort parsing

------------------------------------------------------------------------
