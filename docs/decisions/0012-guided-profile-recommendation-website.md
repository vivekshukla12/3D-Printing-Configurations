# ADR 0012: Guided Profile Recommendation Website

## Status
Accepted

## Date
2026-08-05

## Context
The first website exposed repository files directly. Although accurate, it required users to understand the repository structure and open individual configuration files. The intended audience should be able to begin with the filament they plan to print and then select their printer.

## Decision
The public website will use a guided selection flow:

1. Select filament.
2. Select printer.
3. Optionally select an exact nozzle or process configuration.
4. Present one assembled recommendation view containing the best available calibrated profile, calibration results, speed profile, manufacturer defaults, and print notes.

Profile selection must remain repository-driven. The website may rank exact matching profiles by repository status, but it must not invent settings, merge incompatible hardware configurations, or claim validation where none exists. Missing profile categories must be shown as unavailable. Raw source files and GitHub links remain available for traceability.

## Consequences
- Users do not need to understand YAML file responsibilities before retrieving settings.
- Repository metadata remains the discovery mechanism.
- Calibrated settings, speed settings, and calibration results remain stored independently even though the website presents them together.
- Main and Auxiliary nozzle configurations remain independent.
- The website remains read-only and GitHub remains the exclusive write path and source of truth.
