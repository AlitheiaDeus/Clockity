# TKT-10: Smooth Z-Depth Transitions & Relativistic Warp-Drive Physics

## 1. Problem Statement
Clockity currently employs two distinct 3D depth paradigms:
1. **Tiered Depth Planes** (used in Matrix and current Embers): discrete buckets (Far, Mid, Near).
2. **Smooth Continuous Z-Depth & Hyperbolic Acceleration**:
   - Continuous Z-coordinate per particle (`z` from `w` down to `0`).
   - Projection: $X_{\text{screen}} = C_x + \frac{x}{z} \cdot \text{scale}$, with apparent velocity scaling as $\frac{1}{z^2}$ (accelerating as it zips past the camera).
   - Relativistic radial motion streaks / speed lines when particles pass close to the camera.

## 2. Proposed Scope
1. **Continuous Z Ember Floating**: Embers smoothly drift between depth layers (moving toward or away from the camera in 3D volume rather than staying locked in a fixed plane).
2. **Relativistic Warp-Drive Starfield**:
   - Stars don't just move linearly; they accelerate hyperbolically as $Z \to 0$.
   - When close to the camera, stars draw motion streaks (laser star lines) radiating from the center, creating an authentic warp-drive / hyperspace jump effect.

## 3. Acceptance Criteria
- [ ] Starfield features smooth acceleration and proximity speed streaks.
- [ ] Embers drift seamlessly through 3D Z-depth.
