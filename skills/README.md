# Reusable AI Agent Skills

This directory contains reusable AI-agent workflow instructions that operate on the repository without becoming a second source of truth for printer or filament settings.

## Rules

- Each skill lives under `skills/<skill-name>/`.
- Each skill must contain a `SKILL.md` entry point.
- Optional supporting material may live under `references/`.
- Skills may define retrieval, research, response-format, calibration, and repository-maintenance workflows.
- Skills must treat `printers/`, repository documentation, schemas, and accepted ADRs as authoritative.
- Skills must not embed mutable filament-profile values as a replacement for repository profile files.
- If a skill conflicts with an accepted ADR or authoritative profile data, the ADR/profile data wins.
- Repository writes remain explicit user actions; a skill must not silently write researched baseline values into validated profile data.

## Available skills

### `filament-profile-advisor`

Repository-first filament and Bambu Studio settings advisor. It retrieves the best matching repository profile, preserves exact hardware specificity, and falls back to current manufacturer/web research only when an exact repository value is unavailable.

Entry point: `skills/filament-profile-advisor/SKILL.md`
