# ADR 0005: Independent Calibration Modules

## Status
Accepted

## Date
2026-08-04

## Context
Temperature, flow dynamics, flow rate, maximum volumetric speed, retraction, bridging, ironing, and dimensional accuracy can change independently and may require different retest conditions.

## Decision
Store calibration results as independent modules within `calibration-results.yaml`, with sufficient hardware and process context for each result.

## Consequences
- One calibration can be updated without invalidating unrelated results.
- Nozzle changes can trigger only the relevant recalibrations.
- Calibration provenance remains visible.
