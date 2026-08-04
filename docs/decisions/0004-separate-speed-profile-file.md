# ADR 0004: Separate Speed Profile File

## Status
Accepted

## Date
2026-08-04

## Context
Speed and acceleration settings evolve independently from filament temperature, cooling, and extrusion settings. One filament may also need multiple purpose-specific process profiles.

## Decision
Store Bambu Studio speed and acceleration settings in `speed-profile.yaml` rather than embedding them in `calibrated-profile.yaml`.

## Consequences
- Speed settings can be versioned independently.
- Quality, standard, fast, and draft profiles can be added without duplicating the full filament configuration.
- Consumers know which file contains Bambu Studio Speed page values.
