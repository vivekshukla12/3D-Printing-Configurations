# Bambu Lab Studio Speed Settings — Output Standard

## Purpose

Whenever the agent recommends Bambu Lab Studio speed settings for a filament, use the same sequence and hierarchy as the Bambu Lab Studio Speed page.

The field order is fixed. Numerical values must come from the repository when available or from a clearly labelled proposed baseline when no exact repository value exists.

## Response rules

1. Use the exact Bambu Lab Studio field names and order below.
2. Include every listed field, even when the recommendation is to retain the profile default.
3. Show units beside numerical values:
   - speed: `mm/s`
   - distance: `mm`
   - acceleration: `mm/s²`
   - percentages: `%`
4. Show checkbox settings as `Enabled` or `Disabled`.
5. For **Small perimeters** and **Vertical shell speed**, use either `mm/s` or `%` as appropriate.
6. For **Sparse infill acceleration**, use either `mm/s²` or `%` as appropriate.
7. List all five **Overhang speed** values individually in this order: `10%`, `25%`, `50%`, `75%`, `100%`.
8. When the request concerns only one nozzle, identify Main or Auxiliary once in the header. Do not duplicate the full list.
9. State any required assumptions rather than silently guessing.
10. Put explanation, tuning advice, and warnings after the complete ordered settings list.
11. Write `Use profile default` when no override is recommended.
12. Account for printer model, nozzle role, nozzle diameter/material, filament product, process profile, geometry/purpose, cooling limits, and maximum volumetric speed.

## Required response format

# Bambu Lab Studio — Speed Settings

**Printer:** [printer model]  
**Nozzle:** [Main/Auxiliary, diameter, and nozzle material]  
**Filament:** [brand and material]  
**Process profile:** [layer height or preset]  
**Purpose:** [general, quality, strong part, fast prototype, flexible part, etc.]  
**Status:** [Repository validated / Repository calibrated / Partial repository match / Proposed baseline]

## Initial layer speed

- **Initial layer:** [value] mm/s
- **Initial layer infill:** [value] mm/s

## Other layers speed

- **Outer wall:** [value] mm/s
- **Inner wall:** [value] mm/s
- **Small perimeters:** [value] mm/s or [value]%
- **Small perimeter threshold:** [value] mm
- **Sparse infill:** [value] mm/s
- **Internal solid infill:** [value] mm/s
- **Vertical shell speed:** [value] mm/s or [value]%
- **Top surface:** [value] mm/s
- **Slow down for overhangs:** Enabled/Disabled

### Overhang speed

- **10%:** [value] mm/s
- **25%:** [value] mm/s
- **50%:** [value] mm/s
- **75%:** [value] mm/s
- **100%:** [value] mm/s

- **Slow down by height:** Enabled/Disabled
- **Bridge:** [value] mm/s
- **Gap infill:** [value] mm/s
- **Support:** [value] mm/s
- **Support interface:** [value] mm/s

## Travel speed

- **Travel:** [value] mm/s or `Use profile default`

## Acceleration

- **Normal printing:** [value] mm/s²
- **Travel:** [value] mm/s² or `Use profile default`
- **Initial layer travel:** [value] mm/s²
- **Initial layer:** [value] mm/s²
- **Outer wall:** [value] mm/s²
- **Inner wall:** [value] mm/s²
- **Top surface:** [value] mm/s²
- **Sparse infill:** [value] mm/s² or [value]%

## Notes

After the ordered settings, add only information that materially affects the recommendation, such as maximum volumetric speed, cooling, drying, first-print validation/calibration, or geometry-specific reductions.
