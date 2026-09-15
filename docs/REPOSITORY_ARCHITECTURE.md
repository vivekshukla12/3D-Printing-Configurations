# Repository Architecture

## Purpose

This repository stores structured 3D-printing configuration data and reusable AI-agent workflows in a form that is readable by humans, version-controllable in Git, and reliably consumable by AI tools.

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

skills/
└── <skill-name>/
    ├── SKILL.md
    ├── README.md
    └── references/

docs/
└── ...

schemas/
└── ...
```

Not every profile or skill must contain every optional file. Missing profile files indicate that no authoritative data is available for that category.

## Profile file responsibilities

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

## Reusable AI agent skills

Reusable AI-agent workflow instructions live under `skills/`.

### `SKILL.md`
Required skill entry point. Defines the reusable workflow an AI agent should follow for a specific repository task.

### `README.md`
Optional human-readable overview, scope, and authority model for the skill.

### `references/`
Optional supporting instructions, output standards, examples, or stable reference material used by the skill.

Skills describe behavior, retrieval procedure, research fallback, output formatting, calibration guidance, or maintenance workflow. They are not authoritative storage for mutable printer or filament profile values.

If a skill conflicts with authoritative profile data, repository documentation, schemas, or an accepted ADR, those authoritative repository sources take precedence.

The first reusable skill is `skills/filament-profile-advisor/`.

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

## Profile source precedence

When retrieving settings, use this order:

1. Exact validated configuration
2. `calibrated-profile.yaml`
3. `speed-profile.yaml` for process speeds
4. `calibration-results.yaml` for calibration values
5. `manufacturer-profile.yaml`
6. Closest partial match, clearly labelled as such

Never invent missing repository values.

A reusable skill may define an external research fallback when an exact repository value is unavailable, but externally researched or inferred values must remain clearly distinguished from repository-validated data.

## Skill authority

The authority order for workflow and architecture is:

1. Accepted ADRs and repository-wide architectural documentation
2. Authoritative repository profile data and schemas
3. Reusable skill instructions under `skills/`
4. Chat-local assumptions or generic model knowledge

A skill must not weaken source precedence, hardware specificity, schema requirements, semantic versioning, or append-only validation history.

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

Use semantic versioning for maintained profiles and schemas:

- patch: small correction or tuning change
- minor: new compatible calibration or capability
- major: incompatible profile redesign or schema-breaking change

Reusable skills are version-controlled through Git history. If a future skill requires its own explicit semantic version field, that should be introduced through a documented repository decision rather than inferred ad hoc.

## Schemas

JSON Schemas are stored under `schemas/`. New or updated YAML files should conform to the applicable schema before being committed.

Markdown skill files do not require a profile JSON Schema unless a future skill introduces structured machine-readable skill metadata beyond the current `SKILL.md` convention.
