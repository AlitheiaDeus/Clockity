# TKT-02: Text Glow Effect User Toggle & State Persistence

## 1. Problem Statement
Clockity applies a vibrant neon text-glow filter (`--glow-primary`, `--glow-secondary`) across digital digits and elements, but provides no user drawer option to toggle the glow off (e.g. for users preferring crisp, flat, non-diffused typography or low power).

## 2. Proposed Architecture
- Add `textGlow: true | false` to reactive `state`.
- Add interactive toggle button in Settings Drawer (`#settings-drawer`) under Display / Visuals section.
- Sync state to CSS variables / classes (`--glow-primary: none` or body class `.no-glow`).
- Persist in `localStorage` (`loadPreferences`, `savePreferences`).

## 3. Acceptance Criteria
- [ ] Drawer has accessible pill button to toggle text glow on and off.
- [ ] Setting persists across browser reloads.
- [ ] Turning glow off eliminates all `text-shadow` / filter blur without altering digit layout or slot dimensions.
