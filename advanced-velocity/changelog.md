---
icon: history
order: 60
---

# Changelog

## Version 1.0

The first public release.

**Velocity types**

* Six velocity types on one node — Basic, Directional, Exploding, Velocity from Motion, Curl Noise, and Angular (`@w`) — each in its own section with a header checkbox, its controls hidden until switched on
* Identical **Adjust** and **Mask** controls on every type, promoted from Houdini's Attribute Adjust nodes, plus a one-click **Randomize** row with five variation strengths
* Directional velocity with a **Direction Bias** continuum — at the target, orbiting it, away from it, or anything between (spirals) — with target sources covering another SOP, the second input, a captured rest pose, a typed position, or the geometry's own normals
* Exploding velocity from the whole object (**Centroid** or **Medial Axis**) or a **Point Source**, with interactive viewport placement, a live radius sphere, an affected-piece tint, and **Off Surface / Outward / Inward / Both** directions
* Velocity inherited from animated input, and divergence-free curl turbulence with fractal detail and time evolution

**Timed Events**

* Bake the setup into **events** at different frames and play them back as one summed timeline — create, record live, copy, sort, solo and mute
* Per-event **Attack / Hold / Release** envelopes with curve presets, latch-by-default for RBD, and a Drag release that visibly slows thrown pieces
* An on-screen **event timeline** with per-event state markers, a stale-event warning tied to the Recall / Update editing loop, and an **At Frame** readout
* **Motion preview** — guides and a tumbling wireframe ghost advanced to where the events predict the pieces will be — with per-event **Track Motion** re-aiming directional fields as pieces travel
* Rest-position attributes per event, so a later event can pull the pieces back home
* **Injecting Now** output signal for gating an RBD solver, so physics owns the pieces between impulses

**Mixing and output**

* Additive mixing with per-type gains, or weighted mixing normalized across the enabled streams, with one **Master Speed**
* **Incoming Velocity** as its own stream, on by default — nodes stack, caches survive, and in Timed Events it plays as a live base under the events
* **Quick Setups** for RBD Bullet Solver (velocity) and POP / Vellum (accumulated force), with independent velocity / force attribute names
* **Scale by Piece Size** — big chunks fly slower, from a mass attribute or each packed piece's real size
* Speed clamping, per-stream exports, and an output stripped of every internal attribute

**Visualization**

* Per-type guide trails scaled by each stream's real contribution to the mix, drawn as guide geometry that never touches the output
* Guide density control for heavy fractures, per-type colours and scales, and a Utilities toggle to output the guide curves themselves for rendering

---

!!!info
Future updates and their changes will be listed here. Your purchase includes all future versions of Advanced Velocity at no extra cost — check back after updating to see what's new.
!!!
