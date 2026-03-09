# 8. Binary Fields

## Normative Requirements

- `[JPARSER-BIN-001]` Binary field decoding MUST read the declared length.
- `[JPARSER-BIN-002]` Binary field decoding MUST verify the declared length is within limits.
- `[JPARSER-BIN-003]` Binary field decoding MUST read the exact declared byte count.
- `[JPARSER-BIN-004]` On malformed binary length, the parser MUST abort the record.
- `[JPARSER-BIN-005]` On malformed binary length, the parser MUST emit a warning.
- `[JPARSER-BIN-006]` On malformed binary length, the parser MUST resume at the next record boundary.

Binary fields may appear as:

FIELD_NAME`\n`{=tex} \<8‑byte length\> `<binary payload>`{=html}

Parser rules:

-   read length
-   verify within limits
-   read exact byte count

Malformed length:

-   abort record
-   warn
-   resume at next boundary

------------------------------------------------------------------------
