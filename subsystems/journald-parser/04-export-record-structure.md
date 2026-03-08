# 4. Export Record Structure

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

