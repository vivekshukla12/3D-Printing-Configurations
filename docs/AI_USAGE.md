# AI Usage Guide

## Purpose

This repository is designed to be read and maintained by both humans and AI assistants. AI systems must treat repository files as the primary source of truth for stored printer and filament settings.

Reusable AI-agent workflows may be stored under `skills/`, but those skills are execution guidance rather than a second profile-data source.

## Retrieval procedure

1. Identify the exact printer, filament vendor, filament product, nozzle role, nozzle diameter, nozzle material, process profile, and requested setting category.
2. Read `metadata.yaml` first when an exact profile exists.
3. Read only the profile files relevant to the request.
4. Prefer exact validated records over general profiles.
5. Keep Main and Auxiliary nozzle values separate.
6. Preserve units and field names.
7. List the source paths used.
8. If a relevant reusable skill exists under `skills/`, use it for workflow and response-format guidance without allowing it to override authoritative repository evidence.

## Source precedence

Use the following order for profile values:

1. Exact validation record under `test-history/`
2. `calibrated-profile.yaml`
3. `speed-profile.yaml`
4. `calibration-results.yaml`
5. `manufacturer-profile.yaml`
6. Closest available profile, explicitly marked as a partial match

## Reusable AI agent skills

Reusable skills live under `skills/<skill-name>/` and use `SKILL.md` as their entry point.

Skills may define:

- repository lookup procedures
- external research fallback when repository data is missing
- response/output standards
- calibration guidance
- safe repository-maintenance workflow

Skills must not:

- replace `metadata.yaml` as the profile discovery index,
- duplicate mutable profile values as an alternate source of truth,
- override accepted ADRs,
- merge incompatible printer or nozzle configurations,
- weaken validation or schema requirements,
- silently convert researched/inferred baseline values into validated repository data.

If a skill conflicts with profile data, repository documentation, schemas, or an accepted ADR, the authoritative repository source wins.

## External research fallback

A skill may direct the AI to research current manufacturer or other reputable sources when an exact repository value is unavailable.

When doing so:

- clearly state that no exact repository value exists,
- distinguish manufacturer facts from engineering inference,
- label inferred or researched starting values as proposed/baseline rather than validated,
- do not write those values into validated profile data unless the user explicitly requests repository maintenance and the stored status accurately reflects the evidence.

## Maintenance rules

- Never invent missing repository values.
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
- Keep reusable skill files under `skills/`; do not store skill instructions inside individual printer profiles unless they are profile-specific human notes.

## Handling ambiguity

If an exact combination does not exist:

- state which attributes match,
- state which attributes differ or are missing,
- present the closest profile only as a reference,
- do not claim compatibility without a validation record.

## Updating architecture

When a new architectural decision is accepted, add a new numbered ADR. Do not rewrite an old ADR to hide earlier reasoning. Superseded ADRs should remain in the repository and link to the replacing decision.

Changes to the top-level `skills/` architecture or its authority model are repository-wide design changes and require a new ADR. Adding a new skill that follows the accepted structure does not by itself require another ADR.
