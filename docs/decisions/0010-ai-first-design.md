# ADR 0010: AI-Friendly Repository Design

## Status
Accepted

## Date
2026-08-04

## Context
The repository is intended to be queried and maintained through AI-assisted workflows as well as by human contributors.

## Decision
Use predictable paths, explicit units, structured YAML, metadata indexes, schemas, source-precedence rules, and documented architectural decisions so AI systems can retrieve and update data without relying on prior chat history.

## Consequences
- New conversations can reconstruct repository context from the repository itself.
- AI outputs must cite or list the exact files used.
- Missing values must remain missing rather than being silently inferred.
- Repository documentation becomes the long-term memory for maintenance decisions.
