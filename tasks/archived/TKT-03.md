# TKT-03: Theme Palette Contrast Calibration for Ambient Backgrounds

## 1. Problem Statement
Most built-in preset themes configured in `THEMES` feature extremely dark `bgAccentColor` values (e.g. `< 10%` luminance). Consequently, background ambient effects (Stars, Matrix rain, Water, Fire, Grid) are rendered too dark to be comfortably visible across many presets.

## 2. Proposed Architecture
- Audit all preset themes in `THEMES` (Cyberpunk, Matrix, Amber CRT, Midnight Blue, Vaporwave, Minimal, etc.).
- Recalibrate `bgAccentColor` and ambient shader luminance so procedural background particles and geometries are aesthetically balanced, perceptible, yet non-distracting behind foreground digits.
- Maintain decoupled palette invariant (foreground colors remain independent from background accent).

## 3. Acceptance Criteria
- [ ] Procedural background effects are clearly discernible across all default preset themes.
- [ ] Foreground digital clock maintains high-contrast legibility over the calibrated backgrounds.
