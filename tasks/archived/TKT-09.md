# TKT-09: Off-Screen Horizon Perspective for Cyber Grid and Deep Water

## 1. Problem Statement
When a perspective horizon / vanishing point sits inside the visible screen (`horizonY = h * 0.44`):
- All converging lines crowd toward a single focal zone, presenting a burn-in / image-retention risk for OLEDs and LCDs.
- The viewport is split into two disjointed halves (an empty upper sky and a bottom road/surface).

## 2. Proposed Architecture
- Elevate the virtual vanishing point off-screen above the top viewport boundary (`horizonY = -h * 0.25` or `0.00`).
- **Cyber Grid**: Perspective road/warp grid sweeps across 100% of the screen height from top to bottom with zero convergence hotspot inside the visible area.
- **Deep Water**: Ripples span the entire viewport with continuous perspective elliptical foreshortening based on full screen height.

## 3. Acceptance Criteria
- [x] No focal line convergence hotspot exists inside the visible viewport.
- [x] Grid and ripples cover full screen height smoothly and safely.
