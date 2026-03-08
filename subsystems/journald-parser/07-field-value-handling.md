# 7. Field Value Handling

Values are **raw byte sequences**.

Parser stores:

pointer + length

Do not assume UTF‑8.

Limits:

max value size: 1 MB\
max record size: 2 MB\
max fields per record: 256

If limits exceeded:

-   discard record
-   emit warning

------------------------------------------------------------------------

