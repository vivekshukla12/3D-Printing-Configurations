# ADR 0007: JSON Schema Validation

## Status
Accepted

## Date
2026-08-04

## Context
Structured YAML files require consistent fields, units, versions, and value types to remain reliable for humans, automation, and AI consumers.

## Decision
Maintain Draft 2020-12 JSON Schemas under `schemas/` and validate structured repository files against the applicable schema.

## Consequences
- Invalid contributions can be detected automatically.
- Field names and units remain consistent.
- Future GitHub Actions can enforce repository integrity.
