# Clockity 3 — Manual Verification & Regression Checklist

Use this checklist whenever you add features, tweak styles, or modify the scheduling loops to ensure the **zero-idle architecture**, **visual alignment**, and **subsystems** remain completely intact.

---

## 1. Visual & Layout Integrity
- [ ] **Zero-Jitter Fixed-Width Digit Slots & Melding Prevention**:
  - Watch the numbers change across seconds (`:00` to `:59`) and milliseconds (`.000` to `.999`).
  - Digits and colons must remain **rock solid** without shifting or vibrating horizontally.
  - Verify adjacent wide glyphs (e.g. `22:20` in Orbitron, `22:23` in Silkscreen) do **NOT meld or touch**; each slot enforces dedicated per-font widths and margin separation (`0 0.025em`).
- [ ] **Colon Vertical Centering (HH:MM)**:
  - Both square dots of the colon must sit symmetrically inside the bounding box of the numbers.
  - The bottom dot should *never* dangle below the baseline of the digits.
- [ ] **Seconds Colon Centering (MM:SS)**:
  - When seconds are enabled (`Seconds (:SS)` in drawer), the second colon must align at the exact same height as the primary colon.
- [ ] **Responsive Font Scaling**:
  - In standard H:M mode, digits should fill the screen width gracefully.
  - When seconds (:SS) and milliseconds (.ms) are turned on, font size should scale down smoothly without wrapping to a second line.
- [ ] **OpenType Slashed Zeros & Capability Feedback**:
  - Toggle `Slashed Zero` in the drawer:
    - On fonts with OpenType alternate zero tables (`Orbitron`, `JetBrains Mono`, `Share Tech Mono`, `Inter`), toggles authentic `Slashed Ø (Alt)`.
    - On fixed glyph fonts (`Silkscreen`, `Cinzel`), button clearly reads `Zero (Default)` and informs that the font uses its intrinsic glyph design without OpenType alternates.
- [ ] **12-Hour / 24-Hour Format**:
  - Click `Switch to 12h`: hours should adjust (e.g. 21 → 9), and the `PM`/`AM` badge should appear neatly aligned at the bottom right of the minutes.
  - Click `Switch to 24h`: AM/PM badge hides, hours return to 24-hour format.
- [ ] **Blinking Colon**:
  - Toggle `Blink Colon` in the drawer: colons should dim every alternate second without shifting adjacent numbers or causing layout reflows.

---

## 2. On-Demand Zero-Idle & Performance Engine
- [ ] **Live HUD Sleep State Badge (Bottom-Right)**:
  - **Standard H:M Mode**: Badge reads `Zero-Idle • ~...s Sleep`. Verify the second count matches the time remaining until the next minute. CPU should be virtually **0.00%**.
  - **Seconds Mode**: Badge switches to `Active • 1.0 Hz` (ticks strictly once per second).
  - **Milliseconds / Sand Timer**: Badge switches to `High Precision • 30 Hz`.
- [ ] **Eco Mode Power Governor (Click Badge, press `E`, or toggle in Drawer)**:
  - Actively suppresses all high-frequency updates: hides milliseconds (`.ms`) and seconds (`:SS`), stops blinking colons, halts animated backgrounds (`bgAnim = 'none'`), and reduces glow filter shaders.
  - Locks the clock into minute-synced deep sleep (`Eco Governor • ~...s Sleep`).
  - Badge turns eco-green/cyan with `.eco-active` state.
  - **State Restoration**: Toggling Eco Mode off restores previous user settings (re-enables seconds, ms, and background animation).
  - **Graceful Yield**: Clicking `Seconds`, `Millisec`, or an animated background while in Eco Mode automatically disengages Eco Mode and applies the selected feature.
- [ ] **Tab Visibility Freeze**:
  - Open DevTools or minimize / switch tabs away from Clockity.
  - All timers and `requestAnimationFrame` loops must **pause completely** (`0.0 Hz / Suspended`).
  - Switch back to Clockity: clock must instantly wake up and display the exact current time without stuttering.
- [ ] **Zero DOM Garbage Churn**:
  - Open DevTools Performance / Memory tab.
  - Let Clockity run for 60 seconds. There should be **no saw-tooth garbage collection spikes** because digit slots reuse DOM elements via `textContent`.
- [ ] **Throttled Idle Dimming**:
  - Leave the mouse untouched for 3.5 seconds: controls and mouse cursor must smoothly fade out.
  - Move the mouse: controls and cursor restore instantly without lag or dropped frames.

---

## 3. Clock Modes
- [ ] **12h Analog Mode**:
  - Shows outer glowing dial, 12 major hour numerals, and smooth hour/minute/second hands.
- [ ] **24h Analog Mode**:
  - Dial switches to 24-hour solar format (numbered 00 to 23 with single hand rotation per day).
- [ ] **Progress Bars Mode**:
  - Displays Day, Hour, and Minute percentage bars filling from left to right.
  - Second bar appears dynamically when seconds or milliseconds are toggled on.
- [ ] **Sand Timer (Hourglass) Mode**:
  - Top bulb drains smoothly over the course of each minute while the bottom bulb accumulates sand.
  - Digital readout below the hourglass remains synchronized.
- [ ] **Binary Matrix (BCD) Mode**:
  - 4-bit weighted columns (`8, 4, 2, 1`) glow in `var(--clock-color)` to represent hours, minutes, and seconds.
  - Shows corresponding decimal values underneath in `var(--date-color)`.
  - **Zero-Idle Alignment**: When seconds are hidden, sleeps until the next minute boundary (0.00% CPU). When seconds are toggled on, seconds columns appear and tick at 1.0 Hz.
- [ ] **Clean Mode Transitions**:
  - Switching between any mode should instantly halt canvas loops of inactive modes so only the active view runs.

---

## 4. Lazy Background Canvas Allocation
- [ ] **Pure Solid (Default)**:
  - Inspect `#bg-canvas` in DevTools: width and height must be `0px` and `display: none` (consuming **0 bytes of GPU RAM**).
- [ ] **Procedural Backgrounds**:
  - Test each background: `Time of Day`, `Aurora Silk`, `Starfield`, `Matrix Rain`, `Ember Fire`, `Deep Water`, `CRT Static`, `Cyber Grid`.
  - **Cyber Grid Perspective Horizon**: Renders an infinite 3D perspective synthwave grid scrolling smoothly toward the horizon, rendered purely in `bgAccentColor` and `bgColor` at battery-friendly ~20 FPS.
  - **CRT Static Authentic Co-Rasterization**: Renders an authentic retro cathode-ray tube raster in 240p (240x135) offscreen buffer. Horizontal TVL scanline gaps and RF phosphor static noise are co-rasterized on the exact same pixel grid, framed by a curved phosphor bulb vignette. Uses pure `bgAccentColor` and `bgColor`.
  - **Starfield Pure Ambient Shimmer**: Shimmers entirely in variations and opacities of `bgAccentColor` against `bgColor` (no rogue white stars).
  - **Matrix Rain Palette Decoupling**: Rain drops and fading characters strictly adhere to `bgAccentColor` and `bgColor`, completely decoupled from the foreground `clockColor`.
  - Canvas renders at a cool, battery-friendly ~20 FPS.
  - Switching back to `Pure Solid` or activating `Eco Mode` immediately resets canvas dimensions to `0x0` and kills the animation loop.

---

## 5. Panel De-Energizer (Screen Blanker / OLED Rest)
- [ ] **Blank Screen Toggle (Press `B` or click `Blank`)**:
  - Entire screen turns dark (pitch black `#000000` or selected tint).
  - Screen wake-lock remains active while rendering loops freeze.
- [ ] **Cursor Visibility & Waking Interaction**:
  - Mouse cursor is **NOT** trapped or forced invisible: moving the mouse reveals the standard pointer and illuminates the central pill: `DISPLAY SLEEPING • CLICK ANYWHERE OR PRESS ANY KEY TO WAKE`.
  - Leaving the mouse untouched for 3.5 seconds naturally fades out both cursor and hint text.
  - Clicking anywhere on the screen or pressing any key immediately restores the display and resumes ticking.
- [ ] **Auto-Blank Timer**:
  - Select `5 min` in settings: screen should automatically blank after 5 minutes of idle time.

---

## 6. Customization Studio Drawer & Shortcuts
- [ ] **Drawer Open/Close**:
  - Toggle via `C` key, `Customize` button, `Close` button, clicking backdrop, or `Escape` key.
- [ ] **Themes**:
  - Test all 10 curated presets: `Emerald`, `Amber Phosphor`, `Cyberpunk`, `Nixie`, `Mono`, `Crimson`, `Ocean`, `Matcha`, `Amethyst Violet`, `Solarpunk Zen`.
- [ ] **Hourly Acoustic Chime (Web Audio API)**:
  - Test modes: `Off`, `Bell` (dual-tone harmonic chime), and `Digital` (retro watch beep).
  - Click `Preview ♫` to test acoustic output immediately.
  - Generates pure mathematical synthesizer waveforms via HTML5 Web Audio API with zero external audio assets.
- [ ] **Custom Color Pickers (4 Aligned Swatches)**:
  - Check the 2x2 grid: `Clock`, `Date`, `Backdrop`, and `BG Accent`.
  - Swatches are neatly enclosed in crisp rounded frames without browser user-agent offset.
- [ ] **Font Faces**:
  - Test all 6 fonts: `Orbitron`, `Share Tech Mono`, `JetBrains Mono`, `Modern Sans (Inter)`, `Pixel LED (Silkscreen)`, `Chronos (Cinzel)`.
- [ ] **Date Formats (Clean Pills)**:
  - Test `[Full, 日本, American, Numeric, Short, Off]`.
  - Buttons sit symmetrically in a 3-column row with ample breathing room.

---

## 7. Controls & Quick Actions
- [ ] **Brightness Dimmer**:
  - Cycle brightness icon: 100% → 65% → 35% → 15%.
- [ ] **Zoom Scaling**:
  - Zoom Out (`-`) down to 60%, Zoom In (`+`) up to 300%.
  - Click `Reset` (circular arrow): resets to 200% default view.
- [ ] **Fullscreen Mode**:
  - Toggle with `F` key, `Enter Fullscreen` button, or double-clicking the background.
- [ ] **Reset View**:
  - Click `Reset` or press `0`: restores standard 200% zoom, digital mode, and default emerald styling.
- [ ] **Shortcuts HUD Modal & Extended Hotkeys**:
  - Press `?` or click `?` in control bar: reveals comprehensive keyboard shortcuts cheat sheet.
  - Test mode hotkeys `1` to `6`: switches immediately between Digital, Analog 12h, Analog 24h, Progress, Sand Timer, and Binary.
  - Test `T` key: quickly cycles through all 10 curated color themes.
  - Test `M` key: cycles hourly acoustic chime (`Off` → `Bell` → `Beep`).
  - Test `+` / `-` keys: smooth zoom scaling.
  - Test `H` key: switches between 12-hour and 24-hour formats.
  - Press `Escape`: cleanly dismisses active shortcuts cheat sheet and customization drawer.
- [ ] **Mobile & Viewport Responsiveness**:
  - On screens `<= 768px`, the control bar smoothly scrolls horizontally without wrapping or breaking, with touch momentum scrolling.
  - Labels condense gracefully to retain full functionality on compact screens.

---

## 8. Persistence Check
- [ ] **Reload Test**:
  - Change mode, theme, font, and zoom level.
  - Refresh the browser (`Ctrl+R` / `F5`).
  - All selected preferences must persist seamlessly from `localStorage`.
