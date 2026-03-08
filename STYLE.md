# Specification Style Guide

Rules for formatting requirements and normative language.

## Requirement Statements

- Normative requirements MUST use explicit normative keywords: `MUST`, `MUST NOT`, `SHOULD`, `SHOULD NOT`, `MAY`.
- Non-normative explanatory text SHOULD avoid normative keywords unless it is intentionally a requirement.
- Where practical, files SHOULD separate normative requirements from descriptive notes using a `Normative Requirements` section.

## Requirement IDs

- Requirement IDs are required for explicit normative statements in canonical specification files.
- Descriptive, contextual, and bridge text MUST NOT receive requirement IDs unless it contains an explicit normative requirement.
- Requirement IDs MUST be stable, readable, and prefix-scoped by domain (for example: `CORE-*`, `CLI-*`, `SECOBS-*`, `JPARSER-*`).
- New IDs MUST append within the relevant domain prefix and MUST NOT trigger broad repository renumbering.

## Source Gaps and Placeholder Sections

- If source material is missing or heading-only, the section MUST be marked with a short `source-gap` style note.
- Missing-source sections MUST NOT be expanded with invented requirements.
- A missing-source section MAY remain as a structural placeholder when canonical placement is known.
- Every missing-source placeholder MUST have an associated decision record in `DECISIONS.md` that tracks the recovery/disposition status.
