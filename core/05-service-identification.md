# 5. Service Identification

Service detection follows this rule:

1. If `systemd_unit` exists, use it.
2. Otherwise use `syslog_identifier`.

## Normative Requirements

- `[CORE-SVC-001]` Canonical service names MUST match the systemd unit naming shape `<unit-name>.<unit-type>`, where `<unit-name>` is non-empty and `<unit-type>` is lowercase alphabetic.

Examples:

sshd.service  
systemd-journald.service  
auditd.service

---
