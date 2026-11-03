# BUG-01: Matrix Background Persistent Fade-Off Trails & Screen Strips

## 1. Problem Statement
In `Clockity4.html`, the Matrix background rain effect leaves an indefinite trail/light strips across the screen. The fading opacity is insufficient or accumulating over long periods without clearing completely to `--bg-color`, causing persistent ghost vertical lines.

## 2. Root Cause Analysis
- Canvas clear pass uses a semi-transparent fill (`ctx.fillStyle = rgba(...)`) with too little alpha or rounding artifacts against 8-bit color buffers, preventing trails from fading completely down to `0`.
- In addition, fixed column quantization can lead to noticeable gaps and rigid banding.

## 3. Scope of Work
- Tune alpha fade on Matrix render loop so pixels cleanly decay to 0 within expected frame duration.
- Ensure true background color clearance when appropriate.

## 4. Acceptance Criteria
- [ ] Matrix drops fade smoothly to total black / background color without residual ghost light strips.
- [ ] Runs within standard zero-idle & RAF constraints (~20/30 FPS).
