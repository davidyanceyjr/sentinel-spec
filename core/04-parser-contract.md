# 4. Parser Contract

The parser decodes `journalctl -o export` input into `RawRecord` objects.
The normalizer converts each `RawRecord` into a `CanonicalEvent`.

### Canonical Field Mapping

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

Additional contract rules:

- `source` is derived during normalization from the best available stable source identifier, preferring `systemd_unit` and otherwise `syslog_identifier`.
- Fatal parser errors are limited to unreadable input, unrecoverable desynchronization, or other explicitly fatal conditions defined by the parser specification.

## Normative Requirements

- `[CORE-PARSER-001]` The parser MUST preserve monotonic `record_index` assignment for each decoded record.
- `[CORE-PARSER-002]` The parser MUST tolerate malformed records according to recovery requirements `JPARSER-RECOVERY-001` through `JPARSER-RECOVERY-003`; malformed records may be discarded with warnings, but non-fatal record defects MUST NOT force whole-dataset failure.

---
