# 13. Raw Record Output Contract

## Normative Requirements

- `[JPARSER-RAW-001]` Downstream components MUST NOT modify parser buffers.

Each parsed record emits:

RawRecord - record_index - field_count - fields\[\] - parse_warnings\[\]

Each field:

Field - name_ptr - name_len - value_ptr - value_len

Downstream components must not modify parser buffers.

------------------------------------------------------------------------
