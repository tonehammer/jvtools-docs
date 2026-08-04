# Changelog

## Version 1.1

The first public release — version 1.0 below is the feature set it launched with, finished just before the store went live.

**Ballistic Motion — the node grew a second output**

* Output 2 delivers the pieces *already flying* — advanced along the velocity you authored, tumbling with any baked `@w`, no solver required. Output 1 is untouched, so your sim workflow doesn't change; the second output is for previz, motion-graphics moves, or anywhere a real solve is overkill
* **Return to Home** — keyframe one slider from 0 to 1 and every piece flies back to exactly where it started, however far the motion has carried it. The landing is exact by construction: at 1 the output equals the input to the last bit
* **Return Shaping** — arc the return paths, swirl them around an axis into a vortex, add whole extra turns, and stagger the arrivals (random, nearest first, or farthest first). None of it can break the landing
* Optional **return-path guides** draw each piece's route home, sampled from the same curve the motion actually follows
* **Ballistic Return** — a second node, shipped in the same file, that applies the whole return to a *finished simulation* instead of to the prediction. **Create Ballistic Return** builds it below your solver and wires it up; it can also return to a captured rest pose by name, for animated inputs

**Event Strength**

* Per-event sliders at the top of the Velocity Mixer — scale whole events against each other after the fact, live at playback, no re-baking. The type Gains balance the streams *inside* an event; Event Strength balances the *events*

**Visualization**

* **Ghost Style** for the motion preview: Full Wireframe, Bounding Boxes (the new default — one wire box per piece, cheap at any density), or Points
* Preview Motion no longer switches itself off on heavy inputs — the Visualization Limit now governs the guide trails only

**Bug fixes and improvements**

* Three Point Source menus (Origin, Method, Direction) could display the wrong entry — and Point Source could not actually be picked from the Origin menu. Fixed
* **Output Guides Only now respects Preview Motion** — with the preview on, the rendered guide pass follows the predicted motion instead of sitting pinned at rest; the ghost still never enters the pass
* **Propagate to All** arrow buttons beside each event's Mute Gravity and Release Mode — copy that setting to every other event in one click, live at playback
* Creating an event now switches the Events list to its tab, Create Connected RBD Sim no longer steals the display flag, and a tidier panel throughout: clearer type labels, a Return Shaping group, and attribute-name fields that only show for the active Output As mode

## Version 1.0

The launch feature set.

**Velocity types**

* Six velocity types on one node — Basic, Directional, Exploding, Velocity from Motion, Curl Noise, and Angular (`@w`) — each in its own section with a header checkbox, its controls hidden until switched on
* Identical **Adjust** and **Mask** controls on every type, promoted from Houdini's Attribute Adjust nodes, plus a one-click **Randomize** row with five variation strengths
* Directional velocity with a **Direction Bias** continuum — at the target, orbiting it, away from it, or anything between (spirals) — with target sources covering another SOP, the second input, a captured rest pose, or a typed position
* Exploding velocity from the whole object (**Centroid** or **Medial Axis**) or a **Point Source**, with interactive viewport placement, a live radius sphere, an affected-piece tint, and **Off Surface / Outward / Inward / Both** directions
* Velocity inherited from animated input, and divergence-free curl turbulence with fractal detail and time evolution

**Timed Events**

* Bake the setup into **events** at different frames and play them back as one summed timeline — create, record live, copy, sort, solo and mute
* Per-event **Attack / Hold / Release** envelopes in **frames**, with curve presets (on by default, switch all off to latch for RBD injection), a Drag release that visibly slows thrown pieces, and **Extend to Next** to hold an event until the following one opens
* **Pulse** timing as an alternative to the envelope — an event repeats across a range as a **Hit**, **Build** or **Wave**, with its own count, easing and hold width
* An on-screen **event timeline** with per-event state markers, a stale-event warning tied to the Recall / Update editing loop, and an **At Frame** readout
* **Motion preview** — guides and a tumbling wireframe ghost advanced to where the events predict the pieces will be — with per-event **Track Motion** re-aiming directional fields as pieces travel
* Rest-position attributes per event — with **Track Motion**, a later event pulls every piece back to its own captured position
* **Stagger Points** per event — the points of an event arrive one at a time across its window instead of all at once, with an optional ramp to shape the distribution and an **Order** that leads the cascade at random, strongest or weakest first, along an axis, or by piece size
* **Injecting Now** output signal for gating an RBD solver, so physics owns the pieces between impulses

**Mixing and output**

* Additive mixing with per-type gains, or weighted mixing normalized across the enabled streams, with one **Master Speed**
* **Incoming Velocity** as its own stream, on by default — nodes stack, caches survive, and in Timed Events it plays as a live base under the events
* Velocity output for the RBD Bullet Solver or accumulated force for POP / Vellum, with independent velocity / force attribute names
* **Injecting Now** and per-event **Mute Gravity** signals for gating an RBD solve — gravity can stay muted **until the next event, or to the end of the shot on the last one**, so pieces coast instead of falling between beats while physics still owns them — plus **Create Connected RBD Sim** to wire a solver to both in one click
* **Scale by Piece Size** — big chunks fly slower, from a mass attribute or each packed piece's real size
* Speed clamping, per-stream exports, an **Activation Age** export (`@av_age`, frames since an event took hold of each point) for driving shading pickup, and an output stripped of every internal attribute

**Visualization**

* Per-type guide trails scaled by each stream's real contribution to the mix, drawn as guide geometry that never touches the output
* Guide density control for heavy fractures, per-type colours and scales, and a Utilities toggle to output the guide curves themselves for rendering

---

!!!info
Future updates and their changes will be listed here. Your purchase includes all future versions of Advanced Velocity at no extra cost — check back after updating to see what's new.
!!!
