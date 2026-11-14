# TKT-16: Unified Master RAF Heartbeat & Hardware Acceleration Guard

## 1. Problem Statement
Clockity ran dual unsynchronized `requestAnimationFrame` loops (`highFreqRafId` at ~30 FPS and `bgRafId` at ~15 FPS) when combining animations with subseconds/sand mode. Additionally, permanent CSS `filter: brightness(1)` on fullscreen surfaces prevented hardware zero-copy scanout, causing video playback frame drops and UI stutter.

## 2. Proposed Architecture
- **Unified Master RAF Loop (`state.masterRafId`)**:
  - Merge the clock ticker and background canvas renderer into one coordinated frame heartbeat.
  - Eliminate dual RAF thrashing and redundant loop scheduling.
- **Conditional Filter Bypass**:
  - Set `filter: none !important` when brightness is 100%, activating `filter: brightness(...)` only when dimmed.
- **Layer Containment**:
  - Add `contain: layout paint` to `.clock-digits` and `#bg-canvas`.
- **Hardware Acceleration Startup Check**:
  - WebGL unmasked renderer probe on boot.
  - Display one-time startup toast if software rendering (SwiftShader/llvmpipe) is detected.
  - Store `state.hardwareAccelerated = false` for future throttling hooks.

## 3. Acceptance Criteria
- [x] Single coordinated RAF loop handles all active frame renders.
- [x] Direct scanout preserved when brightness is 100%.
- [x] One-time startup warning toast on software rendering.
