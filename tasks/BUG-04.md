# BUG-04: Ambient Animation Alpha Bleed vs True Luminance & Accent Vibrancy

## 1. Problem Statement
Preset background accents remain too dim because background animations (Matrix, Fire, Water, Stars, Grid) apply multiple semi-transparent alpha overlays (`rgba(..., 0.24 - 0.38)`). In CSS / Canvas alpha compositing over near-black backdrops, low alpha cuts perceived luminance drastically ($L_{\text{perceived}} \approx L_{\text{color}} \times \alpha$). 

## 2. Proposed Architecture & Remediation
- Boost the preset `bgAccent` colors in `THEMES` to vibrant, high-saturation tones (e.g. `25-35%` base luminance).
- Re-tune the animation alpha levels so that strokes and lead glyphs draw at $\alpha \ge 0.65 - 0.90$ with higher contrast.
- Ensure the trailing fade operates smoothly without suffocating the initial rendering vibrancy.

## 3. Acceptance Criteria
- [ ] Animations are vibrant, clearly visible, and unmistakable against all presets.
- [ ] Digital clock foreground remains sharp and dominant.
