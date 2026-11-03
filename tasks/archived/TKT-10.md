# TKT-10: Relativistic Warp-Drive Starfield (Hyperbolic Acceleration & Proximity Streaks)

## 1. Problem Statement
The current starfield moves along linear Z steps, feeling like flat drifting dots rather than an immersive hyperspace journey through the cosmos.

## 2. Proposed Architecture & Relativistic Physics
- **Hyperbolic Acceleration**: As $Z \to 0$, screen-space radial velocity increases proportionally to $\frac{1}{z}$, creating genuine acceleration as stars approach the camera.
- **Warp Speed Streaks**: Track each star's previous projected coordinate `(prevSx, prevSy)` and draw a dynamic motion streak line to `(sx, sy)`. Close stars stretch into brilliant warp-speed lasers pointing away from the center of expansion.
- **Phosphor Accent Color**: Stars strictly adhere to `bgAccentColor` without rogue white dots.

## 3. Acceptance Criteria
- [x] Stars accelerate smoothly as they approach the viewport boundary.
- [x] Proximity motion blur streaks appear dynamically on close stars.
- [x] Zero CPU/GPU lag.
