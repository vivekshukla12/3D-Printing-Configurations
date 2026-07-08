# 3D Printing Configurations

Community-friendly 3D printing configuration repository for storing and comparing real-world slicer settings, calibration values, and tuning notes by printer, filament vendor, and filament type.

## Repository structure

```text
printers/
  <printer-model>/
    <vendor>/
      <filament-type>/
        README.md
        profile.yaml
        calibration-values.yaml
```

Example:

```text
printers/x2d/creality/pla-wood/
  README.md
  profile.yaml
  calibration-values.yaml
```

## Naming convention

Use lowercase folder names and hyphens:

- Printer model: `x2d`, `a1-mini`, `p1s`, etc.
- Vendor: `creality`, `bambu-lab`, `esun`, `sunlu`, etc.
- Filament type: `pla-wood`, `pla-basic`, `petg`, `petg-hf`, etc.

## What each profile should contain

Each filament profile should capture:

- Printer and nozzle context
- Filament vendor and material type
- Plate type
- Nozzle and bed temperatures
- Flow ratio and volumetric speed
- Cooling settings
- Speed and acceleration settings
- Calibration values for main and auxiliary nozzles where applicable
- Known issues, observations, and tuning history

## Important note

These settings are practical starting points, not guaranteed final values. Always validate with a small test print before running a long print, especially with filled filaments such as wood PLA, carbon-fiber blends, or glow-in-the-dark materials.
