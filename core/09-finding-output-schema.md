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

Rules:

- `severity` enum: `informational | low | medium | high`
- `confidence` enum: `low | medium | high`
- `evidence_refs[]` MUST contain `EvidenceRef` objects.
- `evidence_count` MUST equal the number of retained `evidence_refs[]`.
- `context` MUST be JSON-serializable and bounded.
- The earlier abbreviated finding schema using a single `timestamp` field and inline `evidence` object is non-normative and removed.

---

