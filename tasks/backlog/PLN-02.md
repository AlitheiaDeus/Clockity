# PLN-02: Modular Multi-Pane Settings Windows & Dedicated Animation Studio

## 1. Candidate Architectural Concept
As Clockity grows in features, stacking everything vertically in a single sliding drawer risks visual clutter:
- **Dedicated Sub-Panes / Modal Windows**:
  - `General / Horology` (Clock format, timezones, alarms, chimes)
  - `Visuals & Typography` (Fonts, sizing, text glow, themes)
  - `Animation Studio` (Procedural shaders, speed sliders, custom shader parameters)
  - `Power & Display Health` (Eco Governor, anti-burn drift, blanker timers)
- **Zero-Dependency Invariant**:
  - Maintained strictly within pure single-file HTML/CSS/JS without external libraries, using modular internal DOM templates or CSS tab panels.
  - Export/Import JSON configuration to allow sharing custom theme/shader presets while keeping the single-file portable nature 100% intact.

## 2. Status
Roadmap candidate for future major UI architectural overhaul.
