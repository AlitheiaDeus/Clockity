# BUG-02: Cyber Grid Vanishing Point Hotspot & Starline Burn-In Mitigation

## 1. Problem Statement
The Cyber Grid background animation has a persistent, intense bright spot at the horizon / vanishing point (VP). Because the perspective star lines emanating from the VP are essentially static or converging at constant pixels, this presents an acute burn-in / image-retention risk on OLEDs and tired LCDs. Additionally:
- The top half of the screen is completely unaffected and empty during the animation.
- The corner between the horizon and the "road" grid edges remains unnaturally dark.

## 2. Proposed Architecture & Remediation
- Diffuse or eliminate the stationary high-luminance hotspot at the horizon vanishing point.
- Introduce dynamic displacement, oscillation, or gentle scanline drift to prevent static line burn-in.
- Balance atmospheric lighting across the top half (e.g. subtle horizon haze, retro vector sun, or celestial particles).
- Smooth lighting transition into the road horizon corners to eliminate the pitch-black seam.

## 3. Acceptance Criteria
- [ ] No static high-intensity pixel clusters at the horizon/VP.
- [ ] Top half of viewport integrates into the aesthetic rather than abrupt empty cutoff.
- [ ] Corner lighting between road and horizon blends smoothly.
- [ ] Safe for OLED / long-term ambient display use.
