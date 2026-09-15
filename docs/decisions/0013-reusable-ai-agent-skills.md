# ADR 0013: Reusable AI Agent Skills

## Status
Accepted

## Date
2026-09-15

## Context

The repository is intentionally AI-friendly and already serves as long-term memory for printer profiles, calibration evidence, schemas, and design decisions. Repeated AI-assisted workflows such as repository-first filament lookup, current manufacturer research, Bambu Studio output formatting, calibration guidance, and safe repository maintenance would otherwise depend on chat history or be reimplemented inconsistently in every session.

Workflow instructions are different from filament-profile data: they describe how an AI agent should retrieve, interpret, research, present, and maintain repository information. Storing those instructions inside individual printer or filament directories would mix behavior with authoritative configuration data.

## Decision

Add a top-level `skills/` directory for reusable AI-agent workflow instructions.

Canonical skill layout:

```text
skills/
└── <skill-name>/
    ├── SKILL.md
    ├── README.md
    └── references/
```

Rules:

- `SKILL.md` is the reusable skill entry point.
- `README.md` and `references/` are optional supporting material.
- Skills may define retrieval procedures, research fallbacks, response formats, calibration guidance, and repository-maintenance workflows.
- Skills are workflow guidance only. They must not become a second source of truth for mutable printer or filament settings.
- Authoritative profile files under `printers/`, repository schemas, documentation, and accepted ADRs take precedence over skill instructions when conflicts occur.
- Skills must preserve exact hardware/configuration specificity and must not weaken existing source-precedence or validation rules.
- Web-researched or inferred values may be used as clearly labelled proposed baselines when an exact repository value is unavailable, but must not be represented as repository-validated data.
- Repository writes remain explicit user-authorized actions. A skill must not silently commit researched baseline values as validated or verified profiles.
- Reusable skills are version-controlled in Git so future AI sessions can reconstruct workflow behavior without relying on prior chat history.

The first skill is `skills/filament-profile-advisor/`.

## Consequences

- Future AI sessions can reuse a consistent repository-aware workflow.
- Filament/profile data remains cleanly separated from agent behavior.
- The repository becomes the long-term source for both configuration knowledge and the approved procedures used to consume that knowledge.
- Skills can evolve independently without duplicating mutable profile values.
- Adding or revising a skill does not require changing profile schemas unless the skill introduces new structured repository data.
- Future repository-wide changes to the skill architecture require a new ADR rather than rewriting this decision.
