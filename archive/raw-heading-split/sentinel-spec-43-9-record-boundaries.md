# 9. Record Boundaries

Record termination occurs on:

```{=tex}
\n\n
```
Parser must:

1.  emit record
2.  reset field list
3.  increment record_index

EOF may end the final record.

------------------------------------------------------------------------

