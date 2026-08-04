# Schema Reference

## Schema files

Structured YAML documents are validated by JSON Schemas under `schemas/`.

Current schemas:

- `metadata.schema.json`
- `profile.schema.json`
- `speed-profile.schema.json`
- `calibration-results.schema.json`

## Common conventions

- Temperatures use `_c` and values in degrees Celsius.
- Speeds use `_mm_s`.
- Acceleration uses `_mm_s2`.
- Distances use `_mm`.
- Volumetric speed uses `_mm3_s`.
- Percentages use `_percent`.
- Flow ratio and K-factor are unitless decimals.
- Dates use ISO `YYYY-MM-DD`.
- Profile versions use semantic versioning.

## Metadata

`metadata.yaml` should identify:

- profile ID
- printer manufacturer and model
- filament vendor, material, and product or variant
- profile status and version
- contributors
- file references
- tags
- supported or validated configurations

## Profiles

Profile files should record the exact hardware and process context for which values apply. Unknown values should be omitted or explicitly represented as unavailable when allowed by the schema; they must not be guessed.

## Speed profiles

`speed-profile.yaml` contains Bambu Studio speed-page values in the same field order used by the UI. It must bind settings to an exact printer, nozzle role, nozzle diameter, nozzle material, process profile, and purpose.

## Calibration results

`calibration-results.yaml` stores independent modules. Each module should include status and sufficient context to interpret the result. Values for different nozzle roles or hardware configurations must not be merged without evidence.

## Validation records

Dated test records under `test-history/` are append-only evidence. A future dedicated validation schema may extend the current schema set.
