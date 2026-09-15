# Contributing

## General principles

Contributions should improve reproducibility without erasing historical evidence.

## Adding a new profile

1. Create the profile under `printers/<printer>/<vendor>/<filament>/`.
2. Add `metadata.yaml`.
3. Add only the configuration files supported by available data.
4. Record exact printer, nozzle, process, accessory, and filament context.
5. Use explicit units in field names.
6. Mark the profile status accurately.
7. Validate YAML files against the applicable schema.

## Updating an existing profile

- Do not modify manufacturer defaults to match calibrated values.
- Do not delete successful validation records.
- Append a new record for a new tested configuration.
- Increment the semantic version when the recommended profile changes.
- Explain material changes in the commit message.

## Calibration data

Keep calibration modules independent where possible:

- flow dynamics
- flow rate
- temperature
- maximum volumetric speed
- retraction
- bridging
- ironing
- dimensional accuracy

Main and Auxiliary nozzle data must be stored separately.

## Speed data

Speed profiles are printer-specific and must include:

- printer model
- nozzle role
- nozzle diameter
- nozzle material
- process profile
- intended purpose
- maximum volumetric speed

Do not reuse one printer's speed profile as an exact profile for another printer.

## Validation records

Each validation should record enough context to reproduce the result, including the nozzle, plate, feed method, software versions when known, and outcome.

## Reusable AI agent skills

Reusable skills live under `skills/<skill-name>/`.

When adding a skill:

1. Create a descriptive kebab-case directory under `skills/`.
2. Add a required `SKILL.md` entry point.
3. Add `README.md` and `references/` only when they provide useful supporting context.
4. State the skill's scope and trigger conditions clearly.
5. Treat repository profile data, schemas, documentation, and accepted ADRs as authoritative.
6. Do not copy mutable filament/profile values into the skill as a replacement for the canonical profile files.
7. Preserve exact printer/nozzle/process specificity and existing source-precedence rules.
8. Label web-researched or inferred values as proposed/baseline when repository evidence is unavailable.
9. Keep repository writes explicit; a skill must not silently store inferred values as validated or verified data.

When updating a skill:

- keep the workflow compatible with accepted ADRs,
- update supporting references when output requirements change,
- explain material behavioral changes in the commit message,
- do not use skill changes to bypass profile validation, schemas, or append-only history.

Markdown-only skill changes do not require JSON Schema validation unless structured machine-readable skill data is introduced.

## Design changes

Repository-wide design changes require a new Architecture Decision Record under `docs/decisions/`.

Adding a new skill within the accepted `skills/<skill-name>/` structure is not itself a new architecture decision. Changing the top-level skill structure, authority model, or relationship between skills and profile data requires a new ADR.
