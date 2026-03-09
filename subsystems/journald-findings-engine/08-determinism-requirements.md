# 7. Determinism Requirements

## Normative Requirements

- `[JFE-DET-001]` All pipeline stages MUST be deterministic.
- `[JFE-DET-002]` Pipeline stages MUST NOT depend on wall-clock time.
- `[JFE-DET-003]` Pipeline stages MUST NOT depend on random numbers.
- `[JFE-DET-004]` Pipeline stages MUST NOT perform external network access.
- `[JFE-DET-005]` Pipeline stages MUST NOT branch on environment-dependent inputs except explicitly documented CLI/config inputs.
- `[JFE-DET-006]` Identical inputs and options MUST produce identical outputs.

All pipeline stages must be deterministic.

Requirements:

-   no wall-clock time
-   no random numbers
-   no external network access
-   no environment-dependent branching except explicitly documented
    CLI/config input

Identical inputs and options must produce identical outputs.

------------------------------------------------------------------------
