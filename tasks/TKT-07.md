# TKT-07: True Free-Flow Screen-Space Matrix Drops (Removing Monospace Column Grid)

## 1. Problem Statement
The user inquired whether Matrix is absolute screen space or still stuck in monospace columns. Currently, stream x-coordinates are still seeded via `i * 16px`, maintaining a regular column grid. For a true screen-saver aesthetic that prevents LCD pixel wear across dead space, drops should have fully randomized, continuous horizontal coordinate distributions across the entire viewport width.

## 2. Proposed Architecture
- Re-architect `bgState.matrixStreams` to spawn drops at continuous random horizontal positions `x = Math.random() * w`.
- When a drop reaches the bottom, re-seed its `x` at a new random coordinate, allowing drops to organically scan and paint across every pixel of dead space over time like an authentic screensaver.

## 3. Acceptance Criteria
- [ ] Matrix drops are not locked to repeating fixed x-column rails.
- [ ] Over time, drops cover all horizontal pixel regions evenly.
