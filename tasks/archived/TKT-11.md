# TKT-11: CRT Barrel Lens Distortion & Phosphor Snow Calibration

## 1. Problem Statement
The CRT Static background animation features 240p co-rasterized scanlines and edge vignetting, but lacks the iconic **barrel curvature / curved glass lens distortion** seen on vintage cathode-ray tube television screens. Additionally, the raw snow intensity can blend too closely with foreground clock digits on certain themes.

## 2. Proposed Architecture
1. **CRT Glass Barrel Curvature**:
   - Apply subtle radial barrel distortion / pincushion transformation shader or CSS spherical lens warp to curve the raster grid outward toward the center, authentically mimicking a curved spherical glass picture tube.
2. **Phosphor Snow Contrast Calibration**:
   - Cap the maximum snow luminance factor so `bgAccent` noise remains an atmospheric ambient backdrop rather than competing with foreground digital clock legibility.

## 3. Acceptance Criteria
- [x] Subtle curved bulb distortion visible along CRT raster edges.
- [x] Foreground digits maintain sharp contrast over the calibrated static floor.
