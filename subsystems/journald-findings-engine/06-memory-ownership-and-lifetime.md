# 5. Memory Ownership and Lifetime

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

