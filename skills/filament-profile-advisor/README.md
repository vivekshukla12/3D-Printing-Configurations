# Filament Profile Advisor

Reusable repository-first AI-agent skill for filament, calibration, and Bambu Studio speed-setting recommendations.

## Entry point

`SKILL.md`

## Supporting references

- `references/bambu-studio-speed-output-standard.md`

## Authority model

This skill is workflow guidance only. It does not replace repository profile data.

The authoritative sources remain:

1. exact validation records under `printers/.../test-history/`
2. `calibrated-profile.yaml`
3. `speed-profile.yaml`
4. `calibration-results.yaml`
5. `manufacturer-profile.yaml`
6. accepted repository documentation and ADRs

When an exact repository value is unavailable, the skill may research current manufacturer and web sources and provide a clearly labelled proposed baseline. Such a baseline must not be represented as validated repository data.
