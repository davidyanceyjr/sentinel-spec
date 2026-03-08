# 3. Parser Design Requirements

The parser must:

-   operate in a **single forward pass**
-   be **byte-oriented**
-   enforce **strict structural decoding**
-   tolerate **missing fields**
-   implement **explicit skip/abort rules**
-   maintain **bounded memory usage**

Time complexity target:

O(n)

Each byte should be examined a bounded number of times.

------------------------------------------------------------------------

