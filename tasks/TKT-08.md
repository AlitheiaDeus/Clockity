# TKT-08: Live FPS Counter & Performance HUD Toggle

## 1. Problem Statement
Users need a way to inspect the actual real-time FPS of the clock and ambient backgrounds in the viewport, verifying whether Clockity is sleeping at 0.00 Hz, running at 15 Hz, or executing sub-second RAF.

## 2. Proposed Architecture
- Add an optional `showFps: false` setting in `state`.
- Measure delta time across animation / RAF frames and calculate a moving average FPS.
- Display a small minimalist live FPS readout in the bottom HUD or inside the `#eco-badge`.
- Add a toggle in Customization Studio.

## 3. Acceptance Criteria
- [ ] Toggleable live FPS readout.
- [ ] Displays actual measured frame rate accurately without generating garbage collection overhead.
