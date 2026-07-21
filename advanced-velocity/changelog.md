# Changelog

## Version 1.0

The first public release.

**Velocity types**

* Four velocity types on one node — Basic, Directional, Exploding, and Angular (`@w`) — each in its own section with a header checkbox, and its controls hidden until switched on
* Identical **Adjust** and **Mask** controls on every type, promoted from Houdini's Attribute Adjust nodes: scale, rotate, spread, randomise or noise the result, and restrict it with a constant, an attribute, noise, or a line / radial / bounding-box gradient
* Directional velocity aimed at either the second input or another SOP's centre, with a **Create Point** button that builds and wires the target for you, a normalize option, and a distance falloff ramp
* Exploding velocity from the whole object — **Centroid** or **Medial Axis**, so hollow and irregular bodies burst outward sensibly

**Point Source explosions**

* A single blast origin placed inside the object, affecting only the pieces within its radius — built for dense fractured RBD
* Interactive viewport placement: drag on the surface to position the source, scroll to push it into the body, Shift+R to reset the depth
* Live tint of the affected pieces, normalized so the hot core always reads
* **Outward**, **Inward**, and **Both** directions — Both splits thin objects off both faces instead of sliding pieces sideways within the slab
* **Never Push Into Surface** to keep every piece travelling outward from the body

**Mixing and output**

* Additive mixing with per-type gains, or weighted mixing normalized to the enabled types with an overall Mix Scale
* Output section — write the combined `@v`, and optionally keep individual sub-velocities as their own attributes. Everything else is stripped before the output

**Visualization**

* Per-type guide lines scaled by each type's real contribution to the mix, so the display tracks what the mixer is doing
* One-click toggles for Houdini's own `@v` attribute vectors and viewport point trails

---

!!!info
Future updates and their changes will be listed here. Your purchase includes all future versions of Advanced Velocity at no extra cost — check back after updating to see what's new.
!!!
