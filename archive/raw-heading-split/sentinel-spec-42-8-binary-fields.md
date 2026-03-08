# 8. Binary Fields

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

