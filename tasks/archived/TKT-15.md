# TKT-15: Dynamic Zero-Idle Live Tab Favicon

## 1. Problem Statement
Clockity currently has no `<link rel="icon">`, showing a default empty document icon and causing 404 console fetches for `/favicon.ico`.

## 2. Proposed Architecture
- Render a 32×32 tickless analog clock icon using an offscreen canvas:
  - Deep dark circular bezel with a 1.5px glowing rim matching `state.clockColor`.
  - Clean hour and minute hands pointing to current time in `state.clockColor`.
  - Zero clutter, tickless face.
- Synchronize:
  - Updates once per minute at `msToNextMin` boundary (zero CPU during sleep).
  - Updates immediately when changing color themes.
  - Updates `<link id="dynamic-favicon" rel="icon">` via Data URI.

## 3. Acceptance Criteria
- [x] Browser tab displays dynamic tickless analog icon.
- [x] Icon hands update once every minute.
- [x] Icon color matches the selected theme color.
- [x] 0.00% CPU overhead between minute updates.
