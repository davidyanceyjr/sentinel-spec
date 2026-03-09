# 4. Evidence References

## Normative Requirements

- `[JFE-EVID-001]` `EvidenceRef` MUST include `record_index` as the stable dataset-local record identifier.
- `[JFE-EVID-002]` Record indexes in evidence references MUST be non-negative and monotonic across the dataset.
- `[JFE-EVID-003]` Later versions MAY extend `EvidenceRef` with additional fields such as file offsets, boot IDs, or timestamps, but V1 MUST use stable dataset-local record identity.

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
