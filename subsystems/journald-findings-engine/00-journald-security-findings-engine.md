# Journald Security Findings Engine

## V1 Specification --- First Draft

### Status

**Draft status:** First Draft\
**Scope:** V1 implementation specification

------------------------------------------------------------------------

## Normative Requirements

- `[JFE-BASE-001]` Each event MUST maintain a stable evidence reference.
- `[JFE-BASE-002]` Each finding MUST reference evidence records.
- `[JFE-BASE-003]` Rules MUST define explicit time windows.
- `[JFE-BASE-004]` Boot boundaries SHOULD segment analysis by default.
- `[JFE-BASE-005]` JSON output structure MUST include `schema_version`, tool metadata, dataset summary, findings, and warnings.
- `[JFE-BASE-006]` JSON schema MUST be versioned and stable.
- `[JFE-BASE-007]` The parser MUST tolerate missing fields.
- `[JFE-BASE-008]` The parser MUST skip malformed records safely.
- `[JFE-BASE-009]` The parser MUST enforce size limits.
- `[JFE-BASE-010]` The parser MUST never crash on bad input.
- `[JFE-BASE-011]` Skipped records MUST be reported.
- `[JFE-BASE-012]` The analyzer MUST process input in streaming fashion.
- `[JFE-BASE-013]` The analyzer MUST use bounded memory.
- `[JFE-BASE-014]` The analyzer MUST handle large exports safely.
- `[JFE-BASE-015]` The tool MUST avoid storing entire datasets in memory when possible.
- `[JFE-BASE-016]` Implementations MUST use strict bounds checking, safe string handling, avoid format-string vulnerabilities, enforce field size limits, and preserve predictable memory ownership.
- `[JFE-BASE-017]` Evidence previews MUST be safely truncated.
- `[JFE-BASE-018]` Dependencies SHOULD remain minimal (POSIX + libc).
- `[JFE-BASE-019]` Corpus fixtures MUST include SSH brute force patterns, authentication failures, service restart loops, SELinux/AppArmor denials, and malformed exports.
- `[JFE-BASE-020]` Identical inputs MUST produce identical findings.

## 1. Product Definition

V1 is a deterministic command-line analyzer written in **pure C17** that
performs **static security analysis of bounded `systemd-journald`
evidence** and produces **structured findings** plus a human‑readable
report.

V1 is **not** a daemon, not a live monitor, and not a Prometheus
exporter.

Its purpose is to:

-   ingest journald evidence
-   normalize records
-   apply a small, high‑value set of security rules
-   emit explainable findings backed by evidence

------------------------------------------------------------------------

## 2. Mission

Convert bounded journald evidence into **deterministic, evidence‑backed
security findings** for incident triage and operational review.

Key principles:

-   signal quality
-   explainability
-   deterministic behavior
-   tight scope
-   minimal dependencies
-   auditable codebase

------------------------------------------------------------------------

## 3. Non‑Goals

V1 explicitly excludes:

-   live journald following
-   long‑running agent mode
-   HTTP server
-   Prometheus exporter
-   alerting
-   remote collection
-   EDR‑style telemetry
-   network monitoring
-   plugin systems
-   regex rule DSL

The system is strictly an **offline journald evidence analyzer**.

------------------------------------------------------------------------

## 4. Target Use Cases

Primary users:

-   Linux operators
-   SREs
-   security engineers
-   incident responders

Typical uses:

-   analyze an exported journal dataset
-   review authentication and privilege activity
-   identify restart loops or policy denials
-   attach analysis results to incident reports

------------------------------------------------------------------------

## 5. Supported Input

### Primary format

`journalctl -o export`

Example workflow:

``` bash
journalctl -o export > journal.export
secobs analyze journal.export
```

### Input methods

Supported sources:

-   file path
-   stdin

Examples:

``` bash
secobs analyze journal.export
journalctl -o export | secobs analyze -
```

Deferred formats:

-   native `.journal` files
-   JSON journal output
-   syslog text files

------------------------------------------------------------------------

## 6. CLI Interface

Primary command:

``` bash
secobs analyze <input>
```

Flags (initial set):

    --report
    --json
    --output <path>
    --severity-threshold <level>
    --max-records <n>
    --quiet
    --version
    --help

Exit codes:

  Code       Meaning
  ---------- ------------------------
  0          successful analysis
  non‑zero   runtime or input error

Findings **do not** cause non‑zero exit codes.

------------------------------------------------------------------------

## 7. Processing Pipeline

Internal architecture:

1.  Input reader
2.  Export record parser
3.  Event normalization
4.  Event classification
5.  Rule engine
6.  Evidence correlation
7.  Finding generation
8.  Report / JSON output

------------------------------------------------------------------------

## 8. Event Model

Normalized event fields:

-   timestamp
-   boot ID
-   hostname
-   MESSAGE
-   \_SYSTEMD_UNIT
-   SYSLOG_IDENTIFIER
-   PRIORITY
-   \_PID
-   \_UID
-   \_GID
-   \_COMM
-   \_EXE
-   \_TRANSPORT
-   dataset record index

Each event must maintain a stable **evidence reference**.

------------------------------------------------------------------------

## 9. Finding Model

Every finding contains:

-   id (unique identifier for the specific finding instance)
-   rule_id (identifier of the rule that generated the finding; corresponds to the rule catalog ID)
-   category
-   severity
-   confidence
-   summary
-   description
-   time_first
-   time_last
-   evidence_count
-   evidence_refs
-   context object

### Severity Levels

-   informational
-   low
-   medium
-   high

### Confidence Levels

-   low
-   medium
-   high

A finding **must always reference evidence records**.

------------------------------------------------------------------------

## 10. V1 Finding Categories

### Authentication

-   AUTH_FAILURE_BURST
-   INVALID_USER_ATTEMPTS
-   AUTH_FAILURE_THEN_SUCCESS
-   AUTH_LOCKOUT_OR_ACCOUNT_DENIAL

### SSH

-   SSH_BRUTE_FORCE_PATTERN
-   SSH_LOGIN_AFTER_FAILURES
-   SSH_INVALID_USER_PATTERN

### Privilege Escalation

-   SUDO_FAILURE_BURST
-   SUDO_FAILURE_THEN_SUCCESS
-   SU_ATTEMPT_PATTERN

### Service Behavior

-   SERVICE_RESTART_LOOP
-   CRITICAL_SERVICE_FAILURE
-   SECURITY_SERVICE_UNAVAILABLE

### Policy Enforcement

-   SELINUX_DENIAL_CLUSTER
-   APPARMOR_DENIAL_CLUSTER

### Dataset Integrity

-   LOGGING_GAP
-   RAPID_REBOOT_SEQUENCE

------------------------------------------------------------------------

## 11. Rule Model

Rules are compiled into the program.

Types:

1.  **Atomic rules** --- triggered by single events\
2.  **Aggregate rules** --- triggered by event clusters\
3.  **Context rules** --- triggered by event sequences

Preference order for matching:

1.  structured fields
2.  stable identifiers
3.  message text patterns

------------------------------------------------------------------------

## 12. Time Window Handling

Many findings depend on event windows.

Rules must define explicit windows such as:

-   30 seconds
-   1 minute
-   5 minutes

Boot boundaries should segment analysis by default.

------------------------------------------------------------------------

## 13. Human Report Output

Report sections:

1.  Dataset summary
2.  Findings summary
3.  Detailed findings
4.  Analysis warnings

Dataset summary includes:

-   total records
-   parsed records
-   skipped records
-   time span
-   boot segments

------------------------------------------------------------------------

## 14. JSON Output

JSON structure must include:

-   schema_version
-   tool metadata
-   dataset summary
-   findings
-   warnings

Example structure:

``` json
{
  "schema_version": "1",
  "tool": {"name":"secobs"},
  "dataset": {},
  "findings": [],
  "warnings": []
}
```

JSON schema must be **versioned and stable**.

------------------------------------------------------------------------

## 15. Parsing Requirements

Parser must:

-   tolerate missing fields
-   skip malformed records safely
-   enforce size limits
-   never crash on bad input

Skipped records must be reported.

All input is treated as **untrusted**.

------------------------------------------------------------------------

## 16. Performance Requirements

The analyzer must:

-   process input in streaming fashion
-   use bounded memory
-   handle large exports safely

The tool must avoid storing entire datasets in memory when possible.

------------------------------------------------------------------------

## 17. Error Handling

Fatal errors:

-   unreadable input
-   unrecoverable parsing
-   output failure

Warnings:

-   malformed records
-   truncated input
-   unsupported field patterns

Warnings appear in both report and JSON output.

------------------------------------------------------------------------

## 18. Configuration

V1 configuration is minimal.

Prefer CLI flags over configuration files.

Possible tunables:

-   severity threshold
-   max records processed
-   max evidence references per finding

------------------------------------------------------------------------

## 19. Security Requirements

Required safeguards:

-   strict bounds checking
-   safe string handling
-   no format‑string vulnerabilities
-   field size limits
-   predictable memory ownership

Evidence previews must be safely truncated.

------------------------------------------------------------------------

## 20. Build Requirements

Language:

-   **C17**
-   **no C++**

Build systems:

-   Make
-   CMake

Build modes:

-   release: `-O2`
-   debug: `-O0 -g`

Dependencies should remain minimal (POSIX + libc).

------------------------------------------------------------------------

## 21. Testing Requirements

### Unit tests

-   parser
-   normalization
-   rule logic
-   finding generation
-   JSON serialization

### Corpus tests

Fixtures must include:

-   SSH brute force patterns
-   authentication failures
-   service restart loops
-   SELinux/AppArmor denials
-   malformed exports

### Regression tests

Identical inputs must produce identical findings.

------------------------------------------------------------------------

## 22. Acceptance Criteria

V1 is considered complete when it can:

-   parse `journalctl -o export`
-   generate defined findings
-   emit human report
-   emit stable JSON output
-   survive malformed input
-   operate with bounded memory
-   compile via Make and CMake

------------------------------------------------------------------------

## 23. Product Definition (V1)

**A pure C17 CLI tool that statically analyzes journald export evidence
and produces deterministic, evidence‑backed security findings.**


---
