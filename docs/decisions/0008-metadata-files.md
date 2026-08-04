# ADR 0008: Metadata as the Discovery Index

## Status
Accepted

## Date
2026-08-04

## Context
Humans, websites, scripts, and AI assistants need a predictable entry point for discovering profile identity, status, versions, supported hardware, and related files.

## Decision
Every maintained filament profile should use `metadata.yaml` as its discovery and indexing document.

## Consequences
- Consumers can identify a profile without parsing every file.
- A future compatibility matrix or static website can be generated from metadata.
- File references, tags, contributors, and validation status remain centralized.
