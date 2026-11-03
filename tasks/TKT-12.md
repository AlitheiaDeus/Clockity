# TKT-12: High-Rate vs Zero-Idle HUD Visual Distinction (Drawer Architecture)

## 1. Problem Statement
Clockity prides itself on true zero-idle engineering, but currently all settings buttons look identical. Users cannot tell at a glance which features keep the clock in true 0.00 Hz deep sleep (e.g. 24h, Slashed Zero, Date Format, Fonts) versus which features engage continuous CPU/GPU wake locks (e.g. Milliseconds, Seconds, Procedural Animations, Sand Timer).

## 2. Proposed Architecture
- Add clear visual badge indicators or distinct pill stylings:
  - **Zero-Idle Elements**: Subtle green dot or clean neutral border (`0 Hz Safe`).
  - **High-Rate Elements**: Subtle pulse indicator or dedicated energy icon (`Active Wake / ~15–30 Hz`).
- Group or demarcate them cleanly so power-conscious users understand their system impact before toggling.

## 3. Acceptance Criteria
- [ ] Drawer clearly distinguishes 0 Hz zero-idle features from active RAF / high-rate features.
