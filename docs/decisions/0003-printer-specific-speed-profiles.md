# ADR 0003: Printer-Specific Speed Profiles

## Status
Accepted

## Date
2026-08-04

## Context
Print speed depends on printer mechanics, cooling, acceleration limits, hotend capacity, nozzle configuration, and process profile.

## Decision
Store speed profiles per printer and exact nozzle/process configuration. Do not treat one filament's speed settings as universal across printers.

## Consequences
- The same filament may have separate speed profiles for A1 Mini, X2D Main nozzle, X2D Auxiliary nozzle, and future printers.
- Maximum volumetric speed remains tied to the tested filament-hotend-nozzle combination.
