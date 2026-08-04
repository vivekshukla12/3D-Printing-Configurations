# Repository Architecture

## Purpose

This repository stores structured 3D-printing configuration data in a form that is readable by humans, version-controllable in Git, and reliably consumable by AI tools.

## Canonical layout

```text
printers/
└── <printer>/
    └── <vendor>/
        └── <filament>/
            ├── metadata.yaml
            ├── README.md
            ├── manufacturer-profile.yaml
            ├── calibrated-profile.yaml
            ├── speed-profile.yaml
            ├── calibration-results.yaml
            ├── print-notes.md
            └── test-history/
```

Not every profile must contain every file. Missing files indicate that no authoritative data is available for that category.

## File responsibilities

### `metadata.yaml`
Repository index and discovery entry point. Records printer, filament, profile status, version, contributors, profile references, tags, and supported configurations.

### `manufacturer-profile.yaml`
Immutable source record for manufacturer or slicer defaults. Never overwrite values merely because a calibrated profile differs.

### `calibrated-profile.yaml`
Current recommended filament configuration after tuning. This may evolve through semantic versioning.

### `speed-profile.yaml`
Bambu Studio process-speed and acceleration overrides for one exact printer, nozzle configuration, process profile, and intended use.

### `calibration-results.yaml`
Structured results for independent calibration modules such as flow dynamics, flow rate, temperature, maximum volumetric speed, retraction, bridging, ironing, and dimensional accuracy.

### `print-notes.md`
Human-readable operational observations, limitations, troubleshooting notes, and practical guidance.

### `test-history/`
Append-only, dated validation and calibration records. Existing successful records must not be deleted when new hardware or software configurations are tested.

## Configuration specificity

Profiles may depend on:

- printer model
- nozzle role: Main or Auxiliary
- nozzle diameter
- nozzle material
- nozzle flow type
- process profile or layer height
- build plate
- filament feed method
- dryer usage
- enclosure state
- firmware version
- slicer version

Main and Auxiliary nozzle calibration data must remain separate.

## Precedence

When retrieving settings, use this order:

1. Exact validated configuration
2. `calibrated-profile.yaml`
3. `speed-profile.yaml` for process speeds
4. `calibration-results.yaml` for calibration values
5. `manufacturer-profile.yaml`
6. Closest partial match, clearly labelled as such

Never invent missing values.

## Status model

Profiles and records may use:

- `manufacturer-default`
- `proposed`
- `baseline`
- `calibrated`
- `tested`
- `verified`
- `deprecated`

`verified` should represent confirmation beyond a single isolated print or contributor.

## Versioning

Use semantic versioning:

- patch: small correction or tuning change
- minor: new compatible calibration or capability
- major: incompatible profile redesign or schema-breaking change

## Schemas

JSON Schemas are stored under `schemas/`. New or updated YAML files should conform to the applicable schema before being committed.
