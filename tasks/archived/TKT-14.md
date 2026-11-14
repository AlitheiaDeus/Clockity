# TKT-14: CRT Glass Bulb Curvature & Interlaced Clock Scanlines

## 1. Problem Statement
The CRT effect currently only barrel-warps scanlines in the background canvas behind the clock. The clock digits sit flat on top with zero raster interaction, while viewport edges remain square.

## 2. Proposed Architecture
- **Interlaced Scanline Layer (`#crt-scanlines`)**:
  - Full-screen fixed overlay at $z=15$ (directly over `#clock-wrapper` at $z=10$, beneath HUD/Drawer at $z=50$).
  - Slices horizontal raster beam gaps across the clock digits via repeating linear gradient.
  - Keeps phosphor snow/noise strictly on the background canvas so time legibility is never obscured.
- **Glass Bulb Curvature**:
  - Flex border radius to 44px on widescreen with deep radial vignette and spherical specular glare.

## 3. Acceptance Criteria
- [x] Scanline raster lines cleanly slice through clock digits.
- [x] Static noise remains in the background behind digits.
- [x] Viewport edges and corners reflect vintage CRT tube curvature.
