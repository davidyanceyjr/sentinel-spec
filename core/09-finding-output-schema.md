# 9. Finding Output Schema

The authoritative V1 finding schema is:

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

## Normative Requirements

- `[CORE-FIND-001]` `evidence_refs[]` MUST contain `EvidenceRef` objects.
- `[CORE-FIND-002]` `evidence_count` MUST equal the number of retained `evidence_refs[]`.
- `[CORE-FIND-003]` `context` MUST be JSON-serializable and MUST serialize to no more than 4096 bytes in UTF-8 JSON encoding.

## Schema Notes

- `severity` enum: `informational | low | medium | high`
- `confidence` enum: `low | medium | high`
- The earlier abbreviated finding schema using a single `timestamp` field and inline `evidence` object is non-normative and removed.

---
