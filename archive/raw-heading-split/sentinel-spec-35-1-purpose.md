# 1. Purpose

The parser converts a byte stream containing `journalctl -o export` data
into **Raw Records**.

Responsibilities:

-   decode export format
-   identify record boundaries
-   decode field name/value pairs
-   enforce structural validity
-   attach parse warnings
-   emit raw records

No semantic interpretation occurs here.

------------------------------------------------------------------------

