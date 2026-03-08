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

