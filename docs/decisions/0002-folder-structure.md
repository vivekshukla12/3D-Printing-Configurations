# ADR 0002: Per-Printer Filament Folder Structure

## Status
Accepted

## Date
2026-08-04

## Context
The same filament can require different settings on different printers and nozzle configurations.

## Decision
Store profiles under `printers/<printer>/<vendor>/<filament>/` with separate metadata, manufacturer, calibrated, speed, calibration, notes, and history files.

## Consequences
- Printer-specific differences remain explicit.
- Duplicate filament entries across printers are intentional.
- Consumers can navigate by printer first and avoid unsafe cross-printer assumptions.
