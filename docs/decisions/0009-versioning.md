# ADR 0009: Semantic Versioning

## Status
Accepted

## Date
2026-08-04

## Context
Profiles and schemas evolve over time. Consumers need to distinguish minor tuning from incompatible redesigns.

## Decision
Use semantic versioning for maintained profiles and schemas.

## Consequences
- Patch releases represent small corrections or tuning changes.
- Minor releases add compatible calibration data or capabilities.
- Major releases represent incompatible redesigns or schema-breaking changes.
- Version history complements Git history rather than replacing it.
