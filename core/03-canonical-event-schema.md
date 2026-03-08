# 3. Canonical Event Schema

The earlier abbreviated CanonicalEvent definition is hereby **removed** and is non-normative.
This full schema is the single authoritative V1 CanonicalEvent definition.

## Normative Requirements

- `[CORE-EVENT-001]` All pipeline components that exchange normalized events MUST use the **CanonicalEvent** structure below.
- `[CORE-EVENT-002]` Fields with `has_*` companions MUST use explicit presence semantics; downstream stages MUST NOT infer presence from placeholder values.
- `[CORE-EVENT-003]` `priority`, `process_id`, `user_id`, and `group_id` are typed normalized fields and MUST only be populated when conversion succeeds.
- `[CORE-EVENT-004]` Downstream stages MUST NOT alter `record_index`, `timestamp`, `has_timestamp`, `boot_id`, or `has_boot_id`.

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

## Schema Notes

- `record_index` is the stable dataset-local event identity used for evidence references.
- `host`, `source`, `systemd_unit`, `syslog_identifier`, `command`, `executable`, `transport`, and `message` are nullable/string-like normalized fields.
- `structured_fields` contains bounded canonicalized key/value data retained for downstream analysis.
- `normalization_warnings[]` contains non-fatal normalization diagnostics attached to the event.

---
