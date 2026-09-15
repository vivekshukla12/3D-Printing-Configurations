---
name: filament-profile-advisor
description: Repository-first filament profile and Bambu Studio speed-settings advisor for vivekshukla12/3D-Printing-Configurations. Use when a user asks for print settings, filament settings, speed settings, calibration guidance, or a baseline profile for a filament. Check the repository first; if the exact filament/configuration is unavailable, research authoritative manufacturer sources and current web sources and clearly label the result as a proposed baseline.
---

# Filament Profile Advisor

## Purpose

Provide reproducible filament and Bambu Studio printing recommendations while treating `vivekshukla12/3D-Printing-Configurations` as the authoritative long-term source of truth.

Use this skill for:

- filament settings
- print settings
- Bambu Studio speed settings
- temperature, cooling, flow, and maximum-volumetric-speed recommendations
- calibration guidance
- baseline settings for a new filament
- repository profile lookups
- settings for a specific printer, nozzle, material, or process profile

## Authority and precedence

A reusable skill defines workflow, not profile truth. Accepted repository ADRs and authoritative repository data always override this skill if they conflict.

Use this source order:

1. Exact validated repository configuration under `test-history/`
2. `calibrated-profile.yaml`
3. `speed-profile.yaml` for Bambu Studio process speed and acceleration settings
4. `calibration-results.yaml` for measured calibration values
5. `manufacturer-profile.yaml`
6. Closest partial repository match, explicitly labelled as a partial match
7. Current authoritative manufacturer information from the web
8. Broader reputable web research for missing values
9. Engineering inference only when necessary, explicitly labelled as a proposed baseline

Never present a web-derived or inferred value as repository-validated.

## Repository bootstrap

Before repository maintenance or profile creation, read:

- `docs/REPOSITORY_ARCHITECTURE.md`
- `docs/AI_USAGE.md`
- `docs/SCHEMA_REFERENCE.md`
- `docs/CONTRIBUTING.md`
- `docs/ROADMAP.md`
- every file under `docs/decisions/`

Accepted ADRs are authoritative. Do not contradict an accepted ADR unless the user explicitly requests a design change.

For a settings-only lookup, read enough repository documentation to apply the current source precedence and hardware-specificity rules.

## Repository discovery workflow

### 1. Resolve request context

Determine, when available:

- printer model
- filament vendor
- filament product or product line
- material
- nozzle role: Main or Auxiliary
- nozzle diameter
- nozzle material
- nozzle flow type if relevant
- process profile or layer height
- build plate
- feed method
- enclosure state
- intended purpose: quality, standard, strong part, fast prototype, flexible part, support, support interface, etc.

Do not silently guess missing attributes.

If the user supplies only a filament type:

- search the repository for that exact vendor/product/material first;
- use established project context when available;
- state any remaining assumptions in the output header;
- do not require clarification if a safe, useful baseline can be produced with explicit assumptions.

### 2. Search metadata first

Use `metadata.yaml` as the discovery/index entry point whenever it exists.

Canonical profile path:

`printers/<printer>/<vendor>/<filament>/`

Do not conclude that a profile is absent only because code search returns no result. Inspect the relevant printer/vendor directory or repository tree when necessary.

### 3. Retrieve exact evidence

For an exact repository match, inspect only the files relevant to the request:

- `metadata.yaml`
- exact records under `test-history/`
- `calibrated-profile.yaml`
- `speed-profile.yaml`
- `calibration-results.yaml`
- `manufacturer-profile.yaml`
- `print-notes.md`

List or cite the exact repository paths used.

### 4. Keep configurations independent

Never merge incompatible hardware configurations.

- Main and Auxiliary nozzle values remain separate.
- Never reuse one printer's speed profile as an exact profile for another printer.
- Do not treat nozzle materials or diameters as interchangeable without validation.
- Maximum volumetric speed is tied to the tested filament/hotend/nozzle combination.
- A validation for one feed path, build plate, firmware version, or slicer version does not automatically validate another.

## When no exact repository profile exists

If the filament or exact configuration is missing:

1. State clearly that no exact repository profile was found.
2. State the closest repository match if useful, but do not claim compatibility.
3. Search the manufacturer's current official product page, datasheet, technical documentation, or slicer profile.
4. Prefer manufacturer values for nozzle-temperature range, bed-temperature range, drying, recommended speed range, cooling, and handling.
5. Use reputable current sources for values the manufacturer does not publish.
6. Derive only the missing operational values required for a usable baseline.
7. Label non-authoritative engineering estimates as `Proposed baseline`.
8. Explain material inferred values, especially maximum volumetric speed.

Web-source priority:

1. manufacturer or official documentation
2. Bambu Lab documentation where relevant
3. established slicer/project documentation
4. reputable technical communities/issues for practical corroboration

Do not copy a community value blindly.

## Status language

Use these labels precisely:

- `Repository validated` — supported by an exact validation record
- `Repository calibrated` — from the current calibrated profile but not necessarily independently validated
- `Repository manufacturer default` — stored manufacturer or slicer default
- `Partial repository match` — some attributes differ or are missing
- `Proposed baseline` — researched or inferred starting point not yet validated by the repository

Do not call a proposed baseline tested, calibrated, or validated.

## Filament-setting output

When the user asks generally for filament or print settings, provide a concise profile summary with the fields that are actually supported or materially useful, including where applicable:

- nozzle temperature, first layer / other layers
- bed temperature, first layer / other layers
- flow ratio
- maximum volumetric speed
- cooling
- chamber/enclosure guidance
- drying recommendation
- retraction only when relevant and supported
- material-specific warnings
- calibration recommendation

Preserve repository values exactly when they exist. Do not replace calibrated values with generic internet values.

## Bambu Lab Studio speed-settings format

When speed settings are requested, or when a complete baseline speed profile is part of the answer, follow `references/bambu-studio-speed-output-standard.md` exactly.

Required header:

# Bambu Lab Studio — Speed Settings

**Printer:** [printer model]  
**Nozzle:** [Main/Auxiliary, diameter, and nozzle material]  
**Filament:** [brand and material]  
**Process profile:** [layer height or preset]  
**Purpose:** [general, quality, strong part, fast prototype, flexible part, etc.]  
**Status:** [Repository validated / Repository calibrated / Partial repository match / Proposed baseline]

Do not omit listed Speed-page fields. Use `Use profile default` where no override is recommended.

Account for cooling capacity and maximum volumetric speed; do not recommend nominal linear speeds that the configured MVS cannot sustain.

## Calibration guidance

Do not automatically recommend every calibration. Evaluate modules independently:

- flow dynamics
- flow rate
- temperature
- maximum volumetric speed
- retraction
- bridging
- ironing
- dimensional accuracy

For a new unvalidated filament baseline:

- recommend a small first-print validation;
- recommend only calibrations likely to materially improve the result;
- avoid wasting filament on a full calibration suite when a smaller test is sufficient.

When the user supplies successful print feedback or measured results, distinguish that evidence from generic advice.

## Repository maintenance rules

When the user explicitly asks to save, add, or update a profile:

- preserve manufacturer profiles;
- never overwrite validated configurations;
- append validation records under `test-history/`;
- keep Main and Auxiliary nozzle calibration independent;
- store process speeds in `speed-profile.yaml`;
- store calibration measurements in `calibration-results.yaml`;
- use `metadata.yaml` as the repository index;
- follow semantic versioning;
- validate structured YAML against the applicable JSON Schema before committing;
- create a new ADR for a new architectural decision instead of rewriting accepted ADR history.

A proposed baseline must never be stored as `validated` or `verified` without validation evidence.

## Final response pattern

1. Start with a short source/status statement: exact repository match, partial match, or researched baseline.
2. Provide the requested settings.
3. For speed settings, use the exact ordered reference format.
4. Add only material notes such as MVS, cooling, drying, calibration/validation, or geometry limitations.
5. Mention repository source paths when repository values were used.
6. Cite current web sources when internet research supplied values.

Keep repository-derived facts, manufacturer facts, community evidence, and engineering inference clearly distinguishable.
