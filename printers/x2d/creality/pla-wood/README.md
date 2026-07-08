# X2D / Creality / PLA Wood

Recommended starting profile for **Creality PLA Wood** on **Bambu Lab X2D**.

This profile is intended as a safe baseline for decorative wood-filled PLA prints. It prioritizes reliability, reduced clogging risk, and surface quality over speed.

## Use case

- Printer: Bambu Lab X2D
- Filament vendor: Creality
- Filament type: PLA Wood / wood-filled PLA
- Slicer: Bambu Studio
- Suggested nozzle: 0.4 mm hardened steel minimum; 0.6 mm hardened steel preferred for best clog resistance
- Suggested plate: Textured PEI

## Key tuning strategy

Wood-filled PLA should not be printed with aggressive high-speed PLA settings. Use a custom filament profile based on Generic PLA and reduce volumetric flow, wall speed, top surface speed, and acceleration.

Most important baseline values:

```text
Nozzle temperature: 215°C first layer / 210°C other layers
Textured PEI bed: 60°C first layer / 55°C other layers
Max volumetric speed: 8 mm³/s
Outer wall speed: 45–50 mm/s
Top surface speed: 40–45 mm/s
Auxiliary part cooling fan: 0%
Normal printing acceleration: 1000 mm/s²
```

## Recommended print order for tuning

1. Create or copy a Generic PLA filament profile.
2. Apply the filament settings from `profile.yaml`.
3. Run a small 20–30 minute test print.
4. Check for under-extrusion, stringing, blobs, rough top layers, and corner quality.
5. Add main nozzle and AUX nozzle calibration values later in `calibration-values.yaml`.

## Notes for AUX nozzle use

For X2D, the AUX nozzle has a different extrusion path than the main nozzle. Treat AUX nozzle calibration separately where Bambu Studio supports it.

Recommended order for AUX tuning:

1. Manual Flow Dynamics calibration for AUX nozzle.
2. Manual Flow Rate calibration for AUX nozzle.
3. Small real-world test print using AUX nozzle.
4. Update `calibration-values.yaml` with the final K-factor and flow rate values.

For wood PLA, keep AUX nozzle print speed conservative and avoid high acceleration.
