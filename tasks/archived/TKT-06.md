# TKT-06: Frame Rate Calibration & Optional Eco Throttling for Side-Panel Ambient Display

## 1. Problem Statement
When running as a secondary side-panel clock, users may feel the current refresh rates are "too extra" or consuming unnecessary GPU overhead for passive ambient display:
- High precision sub-seconds / sand timer runs at ~30 FPS (interval = 32ms).
- Procedural background canvas loop runs at ~20 FPS (interval = 48ms).
- Standard minute clock already runs at 0.00 Hz (deep minute sleep ~0.016 Hz), but when seconds or procedural backgrounds are active, continuous 20-30 FPS rendering may exceed what is needed for a passive side panel.

## 2. Proposed Options
1. **Calibrate Baseline BG Rate**: Lower background animation target from ~20 FPS (48ms) to ~12–15 FPS (66–80ms) for ambient effects where high motion fluidity is unnecessary (Matrix drops, embers, ripples).
2. **Side-Panel / Low FPS Mode**: Provide an optional low-rate switch in the drawer (e.g. 10–15 FPS cap on procedural animations, or throttling seconds/colons to direct state updates).
3. **Clarify Default Rates**: Ensure the HUD / tooltip clearly communicates the active refresh rate so users know when it's at true 0 Hz vs animated.

## 3. Acceptance Criteria
- [ ] Determine user preference on target frame rate for animations (e.g. ~12-15 FPS vs ~20 FPS vs user slider/toggle).
- [ ] CPU/GPU impact minimized for side-panel usage.
