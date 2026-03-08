# 3. Canonical Event Model

The CanonicalEvent schema is the authoritative data model used between all pipeline stages.

The normalized CanonicalEvent structure for V1 is:

```text
CanonicalEvent {
    record_index
    timestamp
    has_timestamp
    boot_id
    has_boot_id
    host
    source
    message
    has_message
    priority
    has_priority
    process_id
    has_process_id
    user_id
    has_user_id
    group_id
    has_group_id
    command
    executable
    transport
    systemd_unit
    syslog_identifier
    structured_fields
    normalization_warnings[]
}
```

Field normalization rules:

- `host` is the normalized hostname field
- `source` is the normalized primary source identifier
- `process_id` normalizes `_PID`
- `user_id` normalizes `_UID`
- `group_id` normalizes `_GID`
- `command` normalizes `_COMM`
- `executable` normalizes `_EXE`
- `priority` normalizes `PRIORITY` as an integer when valid
- `structured_fields` contains bounded canonicalized key/value data required downstream

## Normative Requirements

- `[SECOBS-EVENT-001]` Parser and normalization stages MUST produce this schema exactly for downstream stages.

---
