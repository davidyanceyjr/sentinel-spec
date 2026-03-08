# 3. Canonical Event Schema

All pipeline components that exchange normalized events MUST use the **CanonicalEvent** structure below.

The earlier abbreviated CanonicalEvent definition is hereby **removed** and is non-normative.
This full schema is the single authoritative V1 CanonicalEvent definition.

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

Rules:

- `record_index` is the stable dataset-local event identity used for evidence references.
- Fields with `has_*` companions MUST use explicit presence semantics; downstream stages MUST NOT infer presence from placeholder values.
- `host`, `source`, `systemd_unit`, `syslog_identifier`, `command`, `executable`, `transport`, and `message` are nullable/string-like normalized fields.
- `priority`, `process_id`, `user_id`, and `group_id` are typed normalized fields and MUST only be populated when conversion succeeds.
- `structured_fields` contains bounded canonicalized key/value data retained for downstream analysis.
- `normalization_warnings[]` contains non-fatal normalization diagnostics attached to the event.
- Downstream stages MUST NOT alter `record_index`, `timestamp`, `has_timestamp`, `boot_id`, or `has_boot_id`.

---

