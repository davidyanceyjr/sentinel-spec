# 5. Memory Ownership and Lifetime

## Normative Requirements

- `[JFE-MEM-001]` The normalizer MUST copy or safely materialize field data that is needed after parser buffer reuse.
- `[JFE-MEM-002]` Downstream stages MUST NOT mutate parser buffers.
- `[JFE-MEM-003]` Downstream stages MUST NOT retain borrowed parser pointers beyond their valid lifetime.
- `[JFE-MEM-004]` Downstream stages MUST retain only owned canonicalized data.

## 5.1 Parser-owned memory

The parser owns the byte buffers that back `RawRecord` field slices.

## 5.2 RawRecord lifetime

A `RawRecord` is valid only until the normalizer finishes consuming it,
unless explicitly copied.

## 5.3 CanonicalEvent ownership

The normalizer must copy or safely materialize any field data needed
after parser buffer reuse.

## 5.4 Downstream restrictions

Downstream stages:

-   must not mutate parser buffers
-   must not retain borrowed parser pointers beyond the valid lifetime
-   must only retain owned canonicalized data

These rules are mandatory because the implementation is in C.

------------------------------------------------------------------------
