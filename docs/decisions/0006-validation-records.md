# ADR 0006: Append-Only Validation Records

## Status
Accepted

## Date
2026-08-04

## Context
A profile may be proven to work with multiple nozzle materials, nozzle diameters, build plates, feed methods, firmware versions, or slicer versions. Replacing old evidence would hide compatibility history.

## Decision
Never delete or overwrite a successful validated configuration. Append a new dated validation record under `test-history/` whenever the same profile is confirmed under a materially different configuration.

## Consequences
- Hardened-steel and stainless-steel nozzle validations can coexist.
- Compatibility claims are evidence-based.
- Historical records remain available for future comparison and confidence scoring.
