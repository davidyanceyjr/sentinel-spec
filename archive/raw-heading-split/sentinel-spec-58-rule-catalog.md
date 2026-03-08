# Rule Catalog

## AUTH_FAILURE_BURST

Category: Authentication

Trigger: - ≥5 authentication failures - within 5 minutes - same boot
segment

Inputs: - events classified as auth_failure

Severity: medium Confidence: high

Context: - failure_count - window_seconds - boot_id

------------------------------------------------------------------------

## INVALID_USER_ATTEMPTS

Category: Authentication

Trigger: - ≥1 invalid user authentication attempt

Escalation: - ≥3 attempts within 5 minutes → medium severity

Inputs: - events classified as invalid_user

Severity: - low (single) - medium (cluster)

Confidence: high

Context: - attempt_count - boot_id

------------------------------------------------------------------------

## AUTH_FAILURE_THEN_SUCCESS

Category: Authentication

Trigger: - ≥3 auth failures followed by ≥1 success - within 15 minutes -
same boot segment

Severity: high Confidence: high

Context: - failure_count - sequence_duration_seconds - boot_id

------------------------------------------------------------------------

## AUTH_LOCKOUT_OR_ACCOUNT_DENIAL

Category: Authentication

Trigger: - explicit account lockout or denial event

Inputs: - PAM/login/SSHD denial messages

Severity: low Confidence: medium

------------------------------------------------------------------------

## SSH_BRUTE_FORCE_PATTERN

Category: SSH

Trigger: - ≥10 SSH failures within 1 minute OR - ≥25 failures within 5
minutes

Inputs: - sshd auth_failure events

Severity: high Confidence: high

Context: - failure_count - window_seconds - boot_id

------------------------------------------------------------------------

## SSH_LOGIN_AFTER_FAILURES

Category: SSH

Trigger: - ≥5 SSH failures followed by ≥1 success - within 15 minutes

Severity: high Confidence: high

------------------------------------------------------------------------

## SSH_INVALID_USER_PATTERN

Category: SSH

Trigger: - ≥3 invalid-user SSH attempts - within 5 minutes

Severity: medium Confidence: high

------------------------------------------------------------------------

## SUDO_FAILURE_BURST

Category: Privilege Escalation

Trigger: - ≥3 sudo failures - within 5 minutes

Severity: medium Confidence: high

------------------------------------------------------------------------

## SUDO_FAILURE_THEN_SUCCESS

Category: Privilege Escalation

Trigger: - ≥2 sudo failures followed by ≥1 success - within 15 minutes

Severity: medium Confidence: high

------------------------------------------------------------------------

## SU_ATTEMPT_PATTERN

Category: Privilege Escalation

Trigger: - single su attempt OR - ≥2 attempts within 15 minutes

Severity: - low (single) - medium (cluster)

Confidence: medium

------------------------------------------------------------------------

## SERVICE_RESTART_LOOP

Category: Service Behavior

Trigger: - same systemd unit restarts ≥3 times - within 5 minutes

Severity: medium Confidence: high

Context: - unit - restart_count

------------------------------------------------------------------------

## CRITICAL_SERVICE_FAILURE

Category: Service Behavior

Trigger: - failure or abnormal exit of a critical service

Default critical services: - sshd.service - systemd-journald.service -
auditd.service

Severity: high Confidence: high

------------------------------------------------------------------------

## SECURITY_SERVICE_UNAVAILABLE

Category: Service Behavior

Trigger: - security service enters failed or stopped state

Services: - sshd - journald - auditd

Severity: high Confidence: high

------------------------------------------------------------------------

## SELINUX_DENIAL_CLUSTER

Category: Policy Enforcement

Trigger: - ≥3 SELinux denial events - within 5 minutes

Severity: medium Confidence: high

------------------------------------------------------------------------

## APPARMOR_DENIAL_CLUSTER

Category: Policy Enforcement

Trigger: - ≥3 AppArmor denial events - within 5 minutes

Severity: medium Confidence: high

------------------------------------------------------------------------

## LOGGING_GAP

Category: Dataset Integrity

Trigger: - adjacent timestamp gap \> 30 minutes - same boot segment

Severity: low Confidence: high

Context: - gap_seconds

------------------------------------------------------------------------

## RAPID_REBOOT_SEQUENCE

Category: Dataset Integrity

Trigger: - ≥3 boot segments - within 1 hour

Severity: medium Confidence: high

Context: - boot_count - window_seconds

------------------------------------------------------------------------

