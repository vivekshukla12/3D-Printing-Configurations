# ADR 0011: Read-Only Filament Profile Website

## Status
Accepted

## Date
2026-08-04

## Context
The repository contains structured filament settings that should be easier to browse without weakening Git history, schema validation, source precedence, or the append-only validation model.

## Decision
Publish a static, read-only website from this repository using GitHub Pages.

The website must:

- treat committed repository files as the only source of truth,
- use `metadata.yaml` as the discovery entry point,
- display available profile files without inventing missing values,
- keep profile updates exclusively in Git commits and pull requests,
- provide links back to the authoritative GitHub source,
- avoid forms, databases, or any other website write path.

The initial implementation may read the public repository tree and raw files at runtime. Deployment remains version-controlled through the GitHub Actions workflow stored in the repository.

## Consequences

- Users can search and read filament settings through a browser.
- Manufacturer, calibrated, speed, calibration, notes, and validation data remain independently represented.
- Repository review, attribution, rollback, semantic versioning, and schema validation remain unchanged.
- GitHub API availability and rate limits may affect initial page loading; a future build-time index may replace runtime discovery without changing the read-only decision.
