# Clockity 4

> **Ultra on-demand, zero-idle ambient digital clock with minute-boundary sleep, CRT rasterizer, Eco Governor, and decoupled procedural shaders in pure vanilla HTML5/CSS3/JS.**

---

## Highlights

- **Zero-Idle Architecture**: Standard digital mode (HH:MM) calculates exact remaining milliseconds to the upcoming `:00` minute mark and enters deep sleep (`0.00%` CPU).
- **Eco Power Governor**: Instantly silences all high-rate consumers (animations, sub-seconds, blurs) via shortcut `E` or the bottom-right HUD badge (`0.016 Hz`).
- **Low-Overhead Side-Panel Display**: Ambient background canvas loops are calibrated to a gentle, battery-conscious ~15 FPS.
- **CRT Phosphor Co-Rasterizer**: 240p offscreen canvas buffer where television raster lines, scanline shadow masks, and RF snow occupy the exact same TVL pixel space.
- **Burn-In & Image Retention Safety**: Anti-Burn drift mode (`Anti-Burn Drift` / periodic pixel shift), diffuse vanishing point, and dark mode black level blanker (`B`).
- **Palette Independence**: Decoupled Foreground (`clockColor`, `dateColor`) and Background Accent (`bgColor`, `bgAccentColor`).
- **Zero Dependencies**: Pure HTML5, CSS3, and modern JavaScript. No build step, no npm, no Tailwind bloat.

---

## Clock Modes

1. **Digital Mode**: Fixed-width zero-jitter digit slots, OpenType slashed zeros (`Ø`), optional seconds (`:SS`), milliseconds (`.ms`), and blinking colon.
2. **12h Analog Dial**: Clean mechanical radial sweep with illuminated hour and minute hands.
3. **24h Military Dial**: Full 24-hour single-revolution dial.
4. **Progress Bars**: Visual metric breakdown of day elapsed, hour elapsed, minute elapsed, and second elapsed.
5. **Sand Timer (Hourglass)**: Continuous particle physics hourglass simulator with minute sand-settling dynamics.
6. **Binary BCD**: 8421 Binary Coded Decimal grid for horology enthusiasts.

---

## Procedural Ambient Backgrounds

- **Matrix Rain**: Screen-space continuous drop streams with calibrated non-ghosting alpha trails.
- **Cyber Grid**: Retro-futuristic perspective synth grid with diffused vanishing point, upper twilight sky, and corner lighting.
- **Starfield**: 3D warp perspective stars shimmering in background accent.
- **CRT Static**: 240p co-rasterized RF snow with authentic TV scanlines and curved bulb vignette.
- **Ember Fire & Deep Water**: Fluid, low-rate procedural ambient particles.
- **Time of Day & Aurora Silk**: Dynamic celestial gradients matching daylight rhythms.

---

## Quickstart

Clockity runs in any modern browser without a web server or compilation step.

### Direct Launch
Double-click `Clockity4.html` or open it directly in Chrome, Firefox, Safari, or Edge.

### Local Dev Server (Optional)
If testing with local HTTP server:
```bash
python -m http.server 8000
# open http://localhost:8000/Clockity4.html
```

---

## Keyboard Shortcuts

| Key | Action |
| :--- | :--- |
| <kbd>C</kbd> | Open / Close Customization Studio Drawer |
| <kbd>B</kbd> | Panel De-Energizer / Blank Screen (Rest pixels) |
| <kbd>E</kbd> | Eco Power Governor (Enforce minute-sync 0.016 Hz sleep) |
| <kbd>F</kbd> | Fullscreen Toggle |
| <kbd>T</kbd> | Cycle Color Themes |
| <kbd>1</kbd> – <kbd>6</kbd> | Switch Clock Mode (Digital, Analog12, Analog24, Progress, Sand, Binary) |
| <kbd>+</kbd> / <kbd>-</kbd> | Zoom In / Out |
| <kbd>0</kbd> | Reset Zoom to 200% Default |
| <kbd>H</kbd> | Toggle 12-Hour / 24-Hour Format |
| <kbd>M</kbd> | Toggle Hourly Acoustic Chime (Bell / Digital) |
| <kbd>?</kbd> | Open Shortcuts HUD |
| <kbd>Esc</kbd> | Close active drawer / modal |

---

## License

MIT License. Free for personal, commercial, and embedded display usage.
