# 4. Parser Requirements

Parser requirements, log format handling, and field extraction rules.

Normalized parser-to-canonical field mapping:

```text
__REALTIME_TIMESTAMP -> timestamp
_BOOT_ID              -> boot_id
_HOSTNAME             -> host
MESSAGE               -> message
PRIORITY              -> priority
_PID                  -> process_id
_UID                  -> user_id
_GID                  -> group_id
_COMM                 -> command
_EXE                  -> executable
_TRANSPORT            -> transport
_SYSTEMD_UNIT         -> systemd_unit
SYSLOG_IDENTIFIER     -> syslog_identifier
```

`source` is derived during normalization from the best available stable source identifier, preferring `systemd_unit` and otherwise `syslog_identifier`.

