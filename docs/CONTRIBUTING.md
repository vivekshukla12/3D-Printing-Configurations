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

## Design changes

Repository-wide design changes require a new Architecture Decision Record under `docs/decisions/`.
