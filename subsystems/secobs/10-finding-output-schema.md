# 10. Finding Output Schema

Structural note: on conflict, `core/09-finding-output-schema.md` controls.

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
