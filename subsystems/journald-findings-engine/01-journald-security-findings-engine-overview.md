# Journald Security Findings Engine

## Processing Pipeline Specification (V1) --- First Draft

Status: Draft\
Scope: Defines the internal data flow and stage contracts for the
offline analyzer.

This document specifies **how parsed records move through the system and
become findings**.\
It does **not** define the byte-level decoding rules of
`journalctl -o export`.

------------------------------------------------------------------------

