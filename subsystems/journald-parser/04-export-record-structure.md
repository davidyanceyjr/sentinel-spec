# 4. Export Record Structure

## Normative Requirements

- `[JPARSER-EXPORT-001]` Each export record MUST contain field lines in `FIELD=VALUE` form.
- `[JPARSER-EXPORT-002]` Records MUST terminate with a blank line (`\n\n`).
- `[JPARSER-EXPORT-003]` EOF MAY terminate the final record.

Each record contains field lines:

FIELD=VALUE`\n`{=tex}

Records terminate with a blank line:

```{=tex}
\n\n
```
Example:

\_\_REALTIME_TIMESTAMP=1710500000000000 \_BOOT_ID=abcd1234
SYSLOG_IDENTIFIER=sshd MESSAGE=Failed password

`<blank line>`{=html}

EOF may terminate the final record.

------------------------------------------------------------------------
