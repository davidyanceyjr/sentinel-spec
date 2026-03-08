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

