# 6. Error and Warning Propagation

The pipeline distinguishes between:

-   parser warnings
-   normalization warnings
-   classification warnings
-   analysis warnings
-   fatal processing errors

## 6.1 Parser warnings

Attached to `RawRecord`.

Examples:

-   duplicate field
-   ignored invalid field name
-   record-level salvage note

## 6.2 Normalization warnings

Attached to `CanonicalEvent`.

Examples:

-   missing canonical timestamp
-   invalid numeric conversion
-   truncated message representation

## 6.3 Classification warnings

Attached to `ClassifiedEvent`.

Examples:

-   weak message-based inference
-   ambiguous source family

## 6.4 Analysis warnings

Emitted globally in final output.

Examples:

-   large number of skipped records
-   dataset too sparse for some time-based findings
-   evidence list clipping due to configured limits

## 6.5 Fatal errors

Fatal errors abort processing.

Examples:

-   unreadable input
-   unrecoverable parser desynchronization
-   output write failure

------------------------------------------------------------------------

