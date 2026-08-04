# AI Usage Guide

## Purpose

This repository is designed to be read and maintained by both humans and AI assistants. AI systems must treat repository files as the primary source of truth for stored printer and filament settings.

## Retrieval procedure

1. Identify the exact printer, filament vendor, filament product, nozzle role, nozzle diameter, nozzle material, process profile, and requested setting category.
2. Read `metadata.yaml` first.
3. Read only the files relevant to the request.
4. Prefer exact validated records over general profiles.
5. Keep Main and Auxiliary nozzle values separate.
6. Preserve units and field names.
7. List the source paths used.

## Source precedence

Use the following order:

1. Exact validation record under `test-history/`
2. `calibrated-profile.yaml`
3. `speed-profile.yaml`
4. `calibration-results.yaml`
5. `manufacturer-profile.yaml`
6. Closest available profile, explicitly marked as a partial match

## Maintenance rules

- Never invent missing values.
- Never silently reuse speed settings from another printer.
- Never overwrite manufacturer defaults.
- Never replace a validated configuration with a newer one.
- Append validation records for new nozzle materials, diameters, build plates, firmware versions, slicer versions, or feed methods.
- Record Main and Auxiliary nozzle calibrations independently.
- Store Bambu Studio speed settings in `speed-profile.yaml`.
- Store measured calibration values in `calibration-results.yaml`.
- Use `metadata.yaml` as the profile discovery index.
- Follow accepted ADRs under `docs/decisions/`.
- Follow semantic versioning.
- Validate structured files against the applicable JSON Schema.

## Handling ambiguity

If an exact combination does not exist:

- state which attributes match,
- state which attributes differ or are missing,
- present the closest profile only as a reference,
- do not claim compatibility without a validation record.

## Updating architecture

When a new architectural decision is accepted, add a new numbered ADR. Do not rewrite an old ADR to hide earlier reasoning. Superseded ADRs should remain in the repository and link to the replacing decision.
