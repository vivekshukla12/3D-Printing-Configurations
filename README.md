# 3D Printing Configurations

Community-friendly, AI-readable 3D-printing knowledge base for storing and comparing real-world slicer settings, calibration values, speed profiles, validation history, tuning notes, and reusable AI-agent workflows.

## Repository structure

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
├── REPOSITORY_ARCHITECTURE.md
├── AI_USAGE.md
├── CONTRIBUTING.md
├── SCHEMA_REFERENCE.md
├── ROADMAP.md
└── decisions/

schemas/
└── *.schema.json
```

Not every filament profile must contain every optional profile file. Missing files mean no authoritative data is available for that category.

## Profile authority

For printer and filament settings, use repository evidence in this order:

1. exact validation record under `test-history/`
2. `calibrated-profile.yaml`
3. `speed-profile.yaml`
4. `calibration-results.yaml`
5. `manufacturer-profile.yaml`
6. closest partial match, explicitly labelled as such

`metadata.yaml` is the profile discovery/index entry point.

## Reusable AI agent skills

Reusable AI-agent workflow instructions live under `skills/`.

Skills define how an agent should retrieve, research, format, validate, and maintain repository information. They are not a second source of truth for filament settings. Authoritative profile data, repository documentation, schemas, and accepted ADRs take precedence if a conflict occurs.

Available skill:

- `skills/filament-profile-advisor/` — repository-first filament settings, Bambu Studio speed settings, web fallback, and calibration guidance

See `skills/README.md` and ADR `docs/decisions/0013-reusable-ai-agent-skills.md`.

## Naming convention

Use lowercase folder names and hyphens:

- Printer model: `x2d`, `a1-mini`, `p1s`, etc.
- Vendor: `creality`, `bambu-lab`, `esun`, `sunlu`, etc.
- Filament type: `pla-wood`, `pla-basic`, `petg`, `petg-hf`, etc.
- Skill: descriptive kebab-case such as `filament-profile-advisor`

## Important note

These settings are practical, configuration-specific records and starting points, not universal guarantees. Always verify that the selected profile matches the printer, nozzle role, nozzle diameter/material, process profile, and relevant hardware context. Validate proposed or baseline values with a small test print before relying on them for a long print.

Repository architecture and maintenance rules are defined under `docs/`. Accepted decisions under `docs/decisions/` must not be silently contradicted.
