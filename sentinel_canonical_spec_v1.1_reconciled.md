
# Sentinel Canonical Engineering Specification
Version: 1.1 (Reconciled Canonical Draft)

This document is the **single normative engineering specification** for the Sentinel / SecObs
journald security findings engine.

Legacy documents merged into this specification are considered **deprecated references**.

Normative requirement keywords:

MUST, MUST NOT, SHOULD, SHOULD NOT, MAY

---

# 1. System Purpose

Sentinel is a deterministic command‑line analyzer written in C17 that performs
static security analysis of bounded journald evidence and produces structured findings.

The system is:

- deterministic
- explainable
- evidence‑backed
- scoped to offline analysis

Sentinel is **not**:

- a daemon
- a live monitoring agent
- an alerting system
- a network monitoring platform

---

# 2. Canonical Architecture

The system pipeline consists of four stages:

Parser  
Classifier  
Finding Engine  
Output Generator

### Finding Engine internal stages

rule evaluation  
temporal correlation  
evidence aggregation  
finding generation

All implementations MUST follow this pipeline order.

---

# 3. Canonical Event Schema

All pipeline components exchange events using the **CanonicalEvent** structure.

```json
CanonicalEvent {
  timestamp
  host
  source
  message
  boot_id
  priority
  process_id
  systemd_unit
  syslog_identifier
  structured_fields
}
```

Rules:

- Parsers MUST emit CanonicalEvent objects.
- Downstream stages MUST NOT alter timestamp or host values.
- Missing optional fields MUST be represented as null.

---

# 4. Parser Contract

The parser converts journald input into CanonicalEvent objects.

### Field Mapping

timestamp → timestamp  
hostname → host  
program → source  
pid → process_id  
message → message  
priority → priority  
boot_id → boot_id  

Parser MUST fail fast on malformed input records.

---

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

# 6. Temporal Segmentation

All correlation rules operate within a **single boot segment**.

Boot segments are determined using the `boot_id` field.

Cross‑boot correlation is not supported in V1.

---

# 7. Rule Definition Model

All rules MUST follow this structure.

```
rule_id
description
severity
confidence
trigger_conditions
context_fields
evidence_fields
```

### Confidence Enum

low  
medium  
high

Values outside this enum are invalid.

---

# 8. Evidence Model

Evidence references link findings to the source events that triggered them.

Evidence structure:

```
event_id
timestamp
source
message_excerpt
```

Evidence limits:

default max_evidence_per_finding = 25

CLI override:

--max-evidence N

If the limit is exceeded:

- evidence list MUST be truncated
- warning `evidence_clipped` MUST be emitted

---

# 9. Finding Output Schema

Findings represent rule detections.

```json
Finding {
  id
  rule_id
  severity
  confidence
  timestamp
  context
  evidence
}
```

Context objects MUST be JSON serializable.

---

# 10. CLI Contract

Required flags:

--input  
--output  
--rules  

Optional flags:

--max-evidence  
--verbose  
--format  

CLI MUST exit non‑zero on parser failure.

Warnings MUST NOT terminate execution.

---

# 11. Validation Requirements

Implementations MUST include tests for:

- parser validation
- CanonicalEvent schema validation
- rule trigger behavior
- evidence clipping behavior
- full pipeline execution

---

# 12. Versioning

Versioning model:

MAJOR – breaking schema or rule changes  
MINOR – new rules or optional fields  
PATCH – documentation updates

---

# 13. Original Rule Catalog and Reference Material

The following content from the original merged specification is retained
for reference and rule detail.

---

# Sentinel / SecObs Canonical Engineering Specification
Version: 1.0 (First-pass merged draft)

This document consolidates the following project specifications into a single canonical specification:

- secobs_v1_spec_v1_corrected.md
- secobs_pipeline_spec_v1_corrected.md
- secobs_parser_spec_v1_first_draft.md
- secobs_rule_catalog_v1_first_draft.md

The goal is to provide a single normative engineering reference for system behavior, data models,
processing stages, rule definitions, and output structures.

---

# 1. Scope and Objectives

# Journald Security Findings Engine

## V1 Specification --- First Draft

### Status

**Draft status:** First Draft\
**Scope:** V1 implementation specification

------------------------------------------------------------------------

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

# 2. System Architecture

This section reconciles the architectural descriptions from the core spec and the pipeline spec.

## 2.1 Canonical V1 Processing Model

The canonical V1 architecture is:

```text
Input Stream
      │
      ▼
Stream Reader
      │
      ▼
Format Decoder (Parser)
      │
      ▼
Raw Record
      │
      ▼
Record Normalizer
      │
      ▼
Canonical Event
      │
      ▼
Event Classifier
      │
      ▼
Classified Event
      │
      ▼
Finding Engine
      │
      ▼
Findings
      │
      ▼
Output Renderer
```

For section-level shorthand elsewhere in this specification, the same architecture may be referred to as:

```text
Parser
Classifier
Finding Engine
Output Generator
```

## 2.2 Reconciliation Rule

The following stages from the core spec are treated as internal responsibilities of the Finding Engine and are not separate top-level pipeline stages in V1:

- Rule engine
- Evidence correlation
- Finding generation

The Finding Engine therefore performs:

- rule evaluation
- temporal correlation
- evidence aggregation
- finding generation

## 2.3 Stage Boundary Interpretation

The parser remains responsible only for decoding input and emitting parsed records.

Normalization remains responsible only for converting raw records into canonical events.

Classification remains responsible only for assigning stable event classes and bounded context.

The Finding Engine consumes classified events and emits immutable findings.

Output rendering remains responsible only for report and JSON generation and must not reinterpret rule logic.

## 2.4 Source Material Retained for Reference

The original pipeline specification text is retained below for reference.

# Journald Security Findings Engine

## Processing Pipeline Specification (V1) --- First Draft

Status: Draft\
Scope: Defines the internal data flow and stage contracts for the
offline analyzer.

This document specifies **how parsed records move through the system and
become findings**.\
It does **not** define the byte-level decoding rules of
`journalctl -o export`.

------------------------------------------------------------------------

# 1. Purpose

The pipeline specification defines:

-   processing stages
-   stage responsibilities
-   data contracts between stages
-   memory ownership rules
-   error propagation behavior

This document exists to keep parsing, normalization, classification,
analysis, and rendering separated.

------------------------------------------------------------------------

# 2. Architectural Principle

The analyzer is an **offline, deterministic, one-shot processing
pipeline**.

``` text
Input Stream
      │
      ▼
Stream Reader
      │
      ▼
Format Decoder (Parser)
      │
      ▼
Raw Record
      │
      ▼
Record Normalizer
      │
      ▼
Canonical Event
      │
      ▼
Event Classifier
      │
      ▼
Classified Event
      │
      ▼
Finding Engine
      │
      ▼
Findings
      │
      ▼
Output Renderer
```

Each stage has a narrow contract and a single primary responsibility.

------------------------------------------------------------------------

# 3. Stage Definitions

## 3.1 Stream Reader

Purpose:

Read bytes from an input source.

Supported V1 sources:

-   file
-   stdin

Responsibilities:

-   buffered reading
-   EOF detection
-   read error reporting
-   enforcing input size limits if configured

Output:

-   raw byte stream

The reader must not interpret record structure or field semantics.

------------------------------------------------------------------------

## 3.2 Format Decoder (Parser)

Defined by the Parser Specification.

Responsibilities:

-   decode `journalctl -o export`
-   identify record boundaries
-   decode field name/value pairs
-   enforce structural parsing rules
-   attach parser warnings
-   emit `RawRecord`

Output:

-   `RawRecord`

The decoder must not classify security-relevant behavior.

------------------------------------------------------------------------

## 3.3 Raw Record

Represents one decoded journal entry before semantic interpretation.

Structure:

``` text
RawRecord {
    record_index
    field_count
    fields[]
    parse_warnings[]
}
```

Field structure:

``` text
Field {
    name_ptr
    name_len
    value_ptr
    value_len
}
```

Properties:

-   fields are byte-oriented
-   field ordering is not semantically meaningful
-   duplicate and malformed-field warnings may be attached
-   values are not assumed to be UTF-8

------------------------------------------------------------------------

## 3.4 Record Normalizer

Purpose:

Convert `RawRecord` into a stable canonical structure used by the rest
of the system.

Responsibilities:

-   extract known fields
-   determine canonical timestamp
-   normalize boot ID
-   normalize source identifiers
-   normalize selected numeric fields
-   produce safe bounded message representation for downstream analysis
-   attach normalization warnings

Output:

-   `CanonicalEvent`

The normalizer may ignore unknown fields unless later stages explicitly
need them.

------------------------------------------------------------------------

## 3.5 Canonical Event

Canonical representation used by classification and rules.

Structure:

``` text
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

Properties:

-   fields may be absent
-   absent fields must be represented explicitly, not guessed
-   canonical event ordering follows input record order unless later
    design explicitly introduces a stable sort

------------------------------------------------------------------------

## 3.6 Event Classifier

Purpose:

Assign stable semantic classes to canonical events.

Responsibilities:

-   derive `source_family`
-   derive event class
-   derive event subtypes if needed
-   attach classification warnings when interpretation is weak

Examples of event classes:

-   `auth_failure`
-   `auth_success`
-   `invalid_user`
-   `sudo_failure`
-   `sudo_success`
-   `su_attempt`
-   `service_restart`
-   `service_start_failure`
-   `service_stopped`
-   `service_abnormal_exit`
-   `selinux_denial`
-   `apparmor_denial`
-   `boot_boundary`

Output:

-   `ClassifiedEvent`

The classifier must be deterministic and conservative.

------------------------------------------------------------------------

## 3.7 Classified Event

Structure:

``` text
ClassifiedEvent {
    record_index
    timestamp
    has_timestamp
    boot_id
    has_boot_id
    source_family
    event_class
    context
    classification_warnings[]
}
```

Where `context` is a bounded structured object that may contain selected
fields such as:

-   `systemd_unit`
-   `principal`
-   `message_excerpt`
-   `failure_reason`

The context object must remain bounded and must not contain arbitrary
whole-record dumps.

------------------------------------------------------------------------

## 3.8 Finding Engine

Purpose:

Consume classified events and emit evidence-backed findings.

Responsibilities:

-   maintain rule-local sliding windows
-   maintain sequence trackers
-   segment by boot boundary where required
-   apply the V1 Rule Catalog
-   merge overlapping findings where specified
-   emit immutable findings

Output:

-   `Finding`

The finding engine must not depend on parser internals.

------------------------------------------------------------------------

## 3.9 Finding Object

Structure:

``` text
Finding {
    id
    rule_id
    category
    severity
    confidence
    summary
    description
    time_first
    time_last
    evidence_count
    evidence_refs[]
    context
}
```

Schema constraints:

-   `severity` enum: `informational | low | medium | high`
-   `confidence` enum: `low | medium | high`
-   `evidence_refs[]` contains `EvidenceRef` objects
-   `context` is a bounded JSON-serializable object

Properties:

-   evidence references must point to parsed dataset records
-   findings are immutable after creation
-   overlapping findings may merge only according to rule-specific
    policies

------------------------------------------------------------------------

## 3.10 Output Renderers

Purpose:

Convert findings into user-visible or machine-readable output.

V1 outputs:

-   human-readable report
-   JSON

Responsibilities:

-   render dataset summary
-   render warnings
-   render findings
-   avoid semantic reinterpretation

Renderers must not perform classification or rule logic.

------------------------------------------------------------------------

# 4. Evidence References

Evidence references connect findings back to source records.

V1 minimum structure:

``` text
EvidenceRef {
    record_index
}
```

Schema constraints:

-   `record_index` is the stable dataset-local record identifier
-   record indexes are non-negative and monotonic across the dataset

Later versions may extend this with file offsets, boot IDs, or
timestamps, but V1 only requires stable dataset-local record identity.

------------------------------------------------------------------------

# 5. Memory Ownership and Lifetime

## 5.1 Parser-owned memory

The parser owns the byte buffers that back `RawRecord` field slices.

## 5.2 RawRecord lifetime

A `RawRecord` is valid only until the normalizer finishes consuming it,
unless explicitly copied.

## 5.3 CanonicalEvent ownership

The normalizer must copy or safely materialize any field data needed
after parser buffer reuse.

## 5.4 Downstream restrictions

Downstream stages:

-   must not mutate parser buffers
-   must not retain borrowed parser pointers beyond the valid lifetime
-   must only retain owned canonicalized data

These rules are mandatory because the implementation is in C.

------------------------------------------------------------------------

# 6. Error and Warning Propagation

The pipeline distinguishes between:

-   parser warnings
-   normalization warnings
-   classification warnings
-   analysis warnings
-   fatal processing errors

## 6.1 Parser warnings

Attached to `RawRecord`.

Examples:

-   duplicate field
-   ignored invalid field name
-   record-level salvage note

## 6.2 Normalization warnings

Attached to `CanonicalEvent`.

Examples:

-   missing canonical timestamp
-   invalid numeric conversion
-   truncated message representation

## 6.3 Classification warnings

Attached to `ClassifiedEvent`.

Examples:

-   weak message-based inference
-   ambiguous source family

## 6.4 Analysis warnings

Emitted globally in final output.

Examples:

-   large number of skipped records
-   dataset too sparse for some time-based findings
-   evidence list clipping due to configured limits

## 6.5 Fatal errors

Fatal errors abort processing.

Examples:

-   unreadable input
-   unrecoverable parser desynchronization
-   output write failure

------------------------------------------------------------------------

# 7. Determinism Requirements

All pipeline stages must be deterministic.

Requirements:

-   no wall-clock time
-   no random numbers
-   no external network access
-   no environment-dependent branching except explicitly documented
    CLI/config input

Identical inputs and options must produce identical outputs.

------------------------------------------------------------------------

# 8. Scalability and Extensibility

The pipeline is designed so V2 can add features without rewriting the
core analysis engine.

Examples:

  -----------------------------------------------------------------------
  Future feature                      Primary change
  ----------------------------------- -----------------------------------
  native `.journal` support           new decoder

  `journalctl -o json` support        new decoder

  compressed evidence bundles         new stream reader / input adapter

  additional rule families            finding engine and classifier
                                      updates

  timeline or SARIF output            new renderer

  systemd unit snapshot analysis      new decoder and/or additional
                                      normalization path
  -----------------------------------------------------------------------

The canonical event and finding contracts are intended to remain stable
across such changes.

------------------------------------------------------------------------

# 9. Testing Strategy by Stage

## Parser tests

Validate byte decoding and raw-record emission.

## Normalization tests

Validate known-field extraction and typed conversion.

## Classification tests

Validate event-class assignment.

## Rule tests

Validate finding emission against fixture corpora.

## Renderer tests

Validate stable textual and JSON output.

## End-to-end tests

Validate complete pipeline behavior for representative datasets.

Each stage should be testable independently.

------------------------------------------------------------------------

# 10. Non-Goals of This Spec

This document does not define:

-   byte-level export grammar
-   parser size limits in detail
-   specific rule thresholds
-   JSON schema
-   repository layout

Those belong to separate specifications.

------------------------------------------------------------------------

# 11. Design Goals

The pipeline must preserve these properties:

-   offline-first
-   deterministic behavior
-   bounded resource usage
-   strict separation of concerns
-   easy fixture-based testing
-   compatibility with future decoders and renderers

------------------------------------------------------------------------

# 12. V1 Summary

V1 treats the analyzer as a staged offline processing system:

-   one-shot input
-   parsed into raw records
-   normalized into canonical events
-   classified into event types
-   analyzed into findings
-   rendered as report and JSON

That structure is the foundation for V2 extensibility without turning
the parser into the entire architecture.


---

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

Parser and normalization stages MUST produce this schema exactly for downstream stages.

---

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

# Journald Security Findings Engine

## Parser Specification (V1) --- First Draft

Status: Draft\
Scope: Defines decoding rules for `journalctl -o export` input.

This document specifies **how bytes become parsed records**.\
It does **not** define classification or findings logic.

------------------------------------------------------------------------

# 1. Purpose

The parser converts a byte stream containing `journalctl -o export` data
into **Raw Records**.

Responsibilities:

-   decode export format
-   identify record boundaries
-   decode field name/value pairs
-   enforce structural validity
-   attach parse warnings
-   emit raw records

No semantic interpretation occurs here.

------------------------------------------------------------------------

# 2. Supported Input

Supported format:

`journalctl -o export`

Input sources:

-   file
-   stdin

Input is treated as **untrusted**.

------------------------------------------------------------------------

# 3. Parser Design Requirements

The parser must:

-   operate in a **single forward pass**
-   be **byte-oriented**
-   enforce **strict structural decoding**
-   tolerate **missing fields**
-   implement **explicit skip/abort rules**
-   maintain **bounded memory usage**

Time complexity target:

O(n)

Each byte should be examined a bounded number of times.

------------------------------------------------------------------------

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

# 5. Field Format

Each field line:

FIELD_NAME=VALUE

Parser behavior:

-   locate first '='
-   left side = field name
-   right side until newline = value

------------------------------------------------------------------------

# 6. Field Name Rules

Field names:

-   ASCII printable
-   cannot contain '=' or newline

Limit:

max field name length: 128 bytes

If exceeded:

-   ignore field
-   emit warning

------------------------------------------------------------------------

# 7. Field Value Handling

Values are **raw byte sequences**.

Parser stores:

pointer + length

Do not assume UTF‑8.

Limits:

max value size: 1 MB\
max record size: 2 MB\
max fields per record: 256

If limits exceeded:

-   discard record
-   emit warning

------------------------------------------------------------------------

# 8. Binary Fields

Binary fields may appear as:

FIELD_NAME`\n`{=tex} \<8‑byte length\> `<binary payload>`{=html}

Parser rules:

-   read length
-   verify within limits
-   read exact byte count

Malformed length:

-   abort record
-   warn
-   resume at next boundary

------------------------------------------------------------------------

# 9. Record Boundaries

Record termination occurs on:

```{=tex}
\n\n
```
Parser must:

1.  emit record
2.  reset field list
3.  increment record_index

EOF may end the final record.

------------------------------------------------------------------------

# 10. Duplicate Fields

Policy:

first occurrence wins

Parser must:

-   retain first value
-   emit duplicate-field warning

------------------------------------------------------------------------

# 11. Error Categories

Fatal Stream Error\
→ stop parsing

Record Structural Error\
→ discard record, continue

Field Validation Warning\
→ ignore field but keep record

------------------------------------------------------------------------

# 12. Recovery Rules

Field error:

continue record

Record structural error:

discard record scan for next boundary

Stream structural error:

abort parsing

------------------------------------------------------------------------

# 13. Raw Record Output Contract

Each parsed record emits:

RawRecord - record_index - field_count - fields\[\] - parse_warnings\[\]

Each field:

Field - name_ptr - name_len - value_ptr - value_len

Downstream components must not modify parser buffers.

------------------------------------------------------------------------

# 14. Parser Limits

  Parameter         Limit
  ----------------- -----------
  max field name    128 bytes
  max field value   1 MB
  max record size   2 MB
  max fields        256

------------------------------------------------------------------------

# 15. Security Requirements

Parser must defend against:

-   integer overflow
-   malicious binary lengths
-   malformed records
-   unsafe string assumptions

All parsing must be bounds-checked.

------------------------------------------------------------------------

# 16. Parser Test Corpus

Required tests:

-   empty input
-   single record
-   multiple records
-   missing final newline
-   duplicate fields
-   oversized field
-   oversized record
-   malformed binary field
-   truncated binary payload
-   invalid field name
-   non‑UTF‑8 message bytes

------------------------------------------------------------------------

# 17. Complexity Guarantees

The parser must guarantee:

-   linear time complexity
-   single-pass parsing
-   bounded memory

Malformed inputs must not cause superlinear behavior.

------------------------------------------------------------------------

# 18. Output Guarantees

For each record:

-   record_index increases monotonically
-   fields are structurally valid
-   warnings describe anomalies

Field order must not be relied upon.


---

# 5. Classification and Normalization

Event classification and normalized attributes are defined in the pipeline specification above.

---

# 6. Temporal Segmentation

Boot segmentation rules and time correlation logic originate from the core specification.

---

# 7. Finding Engine

The finding engine performs:

- rule evaluation
- temporal correlation
- evidence aggregation
- finding generation

Detailed behavior is described in the pipeline specification above.

---

# 8. Rule Catalog

All rule definitions are included below.

# Journald Security Findings Engine

## Rule Catalog (V1) --- First Draft

This document defines the exact trigger conditions for all V1 findings.

The rules are deterministic, compiled into the program, and designed for
explainability and bounded analysis over `journalctl -o export`
datasets.

------------------------------------------------------------------------

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

# Global Threshold Summary

  Rule                        Threshold              Window
  --------------------------- ---------------------- --------
  AUTH_FAILURE_BURST          5 failures             5 min
  INVALID_USER_ATTEMPTS       1 / 3 events           5 min
  AUTH_FAILURE_THEN_SUCCESS   3 failures + success   15 min
  SSH_BRUTE_FORCE_PATTERN     10/1m or 25/5m         dual
  SSH_LOGIN_AFTER_FAILURES    5 failures + success   15 min
  SSH_INVALID_USER_PATTERN    3 events               5 min
  SUDO_FAILURE_BURST          3 failures             5 min
  SUDO_FAILURE_THEN_SUCCESS   2 failures + success   15 min
  SU_ATTEMPT_PATTERN          1 / 2 attempts         15 min
  SERVICE_RESTART_LOOP        3 restarts             5 min
  SELINUX_DENIAL_CLUSTER      3 denials              5 min
  APPARMOR_DENIAL_CLUSTER     3 denials              5 min
  LOGGING_GAP                 \>30 min gap           n/a
  RAPID_REBOOT_SEQUENCE       3 boots                1 hr

------------------------------------------------------------------------

This catalog intentionally favors explainable, conservative rules over
broad heuristics. Findings indicate notable behavior observed in
journald evidence; they do not assert compromise.


---

# 9. Evidence Model

The normalized evidence reference schema for V1 is:

```text
EvidenceRef {
    record_index
}
```

Evidence references and aggregation behavior otherwise follow the core and pipeline specifications.

---

# 10. Finding Output Schema

The finding output schema for V1 is:

```text
Finding {
    id
    rule_id
    category
    severity
    confidence
    summary
    description
    time_first
    time_last
    evidence_count
    evidence_refs[]
    context
}
```

Normalized schema constraints:

- `severity` enum: `informational | low | medium | high`
- `confidence` enum: `low | medium | high`
- `evidence_count` equals the number of retained `evidence_refs[]`
- `context` must be JSON-serializable

---

# 11. CLI Interface

Command-line interface behavior and configuration options originate from the core specification.

---

# 12. Error Handling and Warnings

Pipeline warnings, parser failures, and analysis warnings are defined in the pipeline specification.

---

# 13. Testing and Validation

Testing expectations should include:

- parser validation tests
- schema validation tests
- rule trigger tests
- integration tests

---

# 14. Versioning

Specification versioning policy should follow:

MAJOR – breaking schema or rule changes  
MINOR – new rules or new optional fields  
PATCH – documentation fixes

---

# Appendix

Original documents included above remain the authoritative source for detailed implementation rules
until this canonical specification is finalized.

