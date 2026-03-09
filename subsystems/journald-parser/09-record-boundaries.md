# 9. Record Boundaries

## Normative Requirements

- `[JPARSER-BOUNDARY-001]` On record termination, the parser MUST emit the current record.
- `[JPARSER-BOUNDARY-002]` On record termination, the parser MUST reset the field list for the next record.
- `[JPARSER-BOUNDARY-003]` On record termination, the parser MUST increment `record_index`.
- `[JPARSER-BOUNDARY-004]` EOF MAY terminate the final record.

Record termination occurs on:

```{=tex}
\n\n
```
Parser must:

1.  emit record
2.  reset field list
3.  increment record_index

EOF may end the final record.

------------------------------------------------------------------------
