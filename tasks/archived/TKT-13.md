# TKT-13: Cyber Grid Option C (Hybrid Synthwave Breather)

## 1. Problem Statement
The Cyber Grid background has forward-moving crossbars, but its perspective fan lines are straight rigid rays. This produces a flat runway appearance rather than an organic, breathing retro-wave grid.

## 2. Proposed Architecture
- Implement **Option C: Hybrid Synthwave Breather**:
  1. **Breathing Perspective Ribs**: Perspective fan lines flex laterally with a harmonic sinusoidal wave (`quadraticCurveTo`).
  2. **Rolling Elevation Crossbars**: Crossbars are segmented into 12-16 points across screen width, with $Y$ displaced by a traveling elevation wave.
- Ensure zero dynamic heap allocations and freeze to 0.00% CPU when in Eco Mode or when another mode is selected.

## 3. Acceptance Criteria
- [x] Perspective ribs breathe laterally.
- [x] Crossbars roll with traveling wave elevation.
- [x] 30 FPS target maintained without garbage generation.
