# 5. Service Identification

Service detection follows this rule:

1. If `systemd_unit` exists, use it.
2. Otherwise use `syslog_identifier`.

Canonical service names MUST use systemd unit format.

Examples:

sshd.service  
systemd-journald.service  
auditd.service

---

