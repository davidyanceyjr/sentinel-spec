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

