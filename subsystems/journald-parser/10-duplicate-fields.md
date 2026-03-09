# 10. Duplicate Fields

## Normative Requirements

- `[JPARSER-DUP-001]` Duplicate-field handling MUST follow a first-occurrence-wins policy.
- `[JPARSER-DUP-002]` The parser MUST retain the first value for a duplicated field.
- `[JPARSER-DUP-003]` The parser MUST emit a duplicate-field warning when duplicate fields are present.

Policy:

first occurrence wins

Parser must:

-   retain first value
-   emit duplicate-field warning

------------------------------------------------------------------------
