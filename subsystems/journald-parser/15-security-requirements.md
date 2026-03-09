# 15. Security Requirements

## Normative Requirements

- `[JPARSER-SEC-001]` The parser MUST defend against integer overflow.
- `[JPARSER-SEC-002]` The parser MUST defend against malicious binary lengths.
- `[JPARSER-SEC-003]` The parser MUST defend against malformed records.
- `[JPARSER-SEC-004]` The parser MUST defend against unsafe string assumptions.
- `[JPARSER-SEC-005]` All parsing MUST be bounds-checked.

Parser must defend against:

-   integer overflow
-   malicious binary lengths
-   malformed records
-   unsafe string assumptions

All parsing must be bounds-checked.

------------------------------------------------------------------------
