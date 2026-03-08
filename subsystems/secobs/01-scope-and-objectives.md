# 1. Scope and Objectives

<<<<<<< HEAD
Source note: recovered from `sentinel_canonical_spec_v1.1_reconciled.md` section
`# 1. Scope and Objectives`. This section captures the upstream scope/objective
material; detailed processing and interface requirements remain in later sections.

## 1. Product Definition

V1 is a deterministic command-line analyzer written in **pure C17** that
performs **static security analysis of bounded `systemd-journald`
evidence** and produces **structured findings** plus a human-readable
report.

V1 is **not** a daemon, not a live monitor, and not a Prometheus
exporter.

Its purpose is to:

- ingest journald evidence
- normalize records
- apply a small, high-value set of security rules
- emit explainable findings backed by evidence

## 2. Mission

Convert bounded journald evidence into **deterministic, evidence-backed
security findings** for incident triage and operational review.

Key principles:

- signal quality
- explainability
- deterministic behavior
- tight scope
- minimal dependencies
- auditable codebase

## 3. Non-Goals

V1 explicitly excludes:

- live journald following
- long-running agent mode
- HTTP server
- Prometheus exporter
- alerting
- remote collection
- EDR-style telemetry
- network monitoring
- plugin systems
- regex rule DSL

The system is strictly an **offline journald evidence analyzer**.

## 4. Target Use Cases

Primary users:

- Linux operators
- SREs
- security engineers
- incident responders

Typical uses:

- analyze an exported journal dataset
- review authentication and privilege activity
- identify restart loops or policy denials
- attach analysis results to incident reports
=======
Structural note: the source fragment for this section is heading-only.
Normative scope and objectives are defined in `subsystems/secobs/00-sentinel-secobs-canonical-engineering-specification.md`
and `core/01-system-purpose.md`.
>>>>>>> docs/phase3-structural-review
