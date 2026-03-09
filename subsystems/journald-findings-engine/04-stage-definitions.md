# 3. Stage Definitions

## Normative Requirements

- `[JFE-STAGE-001]` The stream reader MUST NOT interpret record structure or field semantics.
- `[JFE-STAGE-002]` The format decoder MUST NOT classify security-relevant behavior.
- `[JFE-STAGE-003]` The record normalizer MAY ignore unknown fields unless later stages explicitly require them.
- `[JFE-STAGE-004]` Absent canonical-event fields MUST be represented explicitly and MUST NOT be guessed.
- `[JFE-STAGE-005]` The event classifier MUST be deterministic and conservative.
- `[JFE-STAGE-006]` The classified-event `context` object MUST remain bounded.
- `[JFE-STAGE-007]` The classified-event `context` object MUST NOT contain arbitrary whole-record dumps.
- `[JFE-STAGE-008]` The finding engine MUST NOT depend on parser internals.
- `[JFE-STAGE-009]` Evidence references in findings MUST point to parsed dataset records.
- `[JFE-STAGE-010]` Overlapping findings MAY merge only according to rule-specific policies.
- `[JFE-STAGE-011]` Output renderers MUST NOT perform classification or rule logic.

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
