# 8. Evidence Model

Evidence references link findings to the source records that triggered them.

The authoritative V1 evidence reference schema is:

```text
EvidenceRef {
    record_index
}
```

## Normative Requirements

- `[CORE-EVID-001]` `record_index` MUST refer to the CanonicalEvent `record_index` value.
- `[CORE-EVID-002]` V1 evidence references MUST NOT rely on a separate `event_id` field.
- `[CORE-EVID-003]` Additional evidence presentation fields such as timestamp, source, or message excerpts MAY be rendered in reports, but they are derived output fields and are not part of the normative EvidenceRef identity schema.
- `[CORE-EVID-004]` If the evidence limit is exceeded, the evidence list MUST be truncated.
- `[CORE-EVID-005]` If the evidence limit is exceeded, warning `evidence_clipped` MUST be emitted.

## Schema Notes

- Evidence identity is dataset-local and monotonic in input order.

Evidence limits:

default max_evidence_per_finding = 25

CLI override:

--max-evidence N

If the limit is exceeded:

- evidence list is truncated
- warning `evidence_clipped` is emitted

---
