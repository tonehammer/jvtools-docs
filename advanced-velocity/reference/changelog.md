# Changelog

## Version 1.3

**Force output**

* **Fixed:** Force mode now drives an RBD Bullet Solver.
* **New: Create Connected RBD Sim** wires the solver for whichever Output As mode is set.
* **New: Force Scale** sets the force multiplier.
* **New: Scale Gravity to Scene** matches solver gravity to your input's size.
* The Force Attribute now defaults to `av_force`.

**Scale**

* **New:** world-space speeds size themselves to your input when geometry is first connected.
* **New: Measure Input Scale** reports the measured size and what it set.

**Events**

* **New: Copy From** overwrites the event you are on with another event's data.

**Bug fixes and improvements**

* **Fixed:** the point-source placement state ignored input size.
* **Fixed:** the Documentation button opened a stale docs URL.
* **Clear Setup** now parks the playhead at the range start.

## Version 1.2

**Bug fixes and improvements**

* **Fixed:** the event timeline HUD did not draw when the node sat inside a transformed object.
* **Fixed:** ten tooltips on the Velocity from Motion and Curl Noise streams described the exploding velocity.
* **Fixed:** the pulse waveform icon shifted position when the Pattern changed.
* **New:** a Website button in the Utilities link row.
* The Ballistic Return node is now called **Advanced Velocity Ballistic Return** in the tab menu.
* Removed a stray placeholder parameter from the top of the panel.
* Interior network tidy-up.

## Version 1.1

The first public release — version 1.0 below is the feature set it launched with.

**Ballistic Motion**

* **New: a second output** delivering the pieces already flying, with no solver.
* **New: Return to Home** — one slider flies every piece back to exactly where it started.
* **New: Return Shaping** — arc, swirl, extra turns and staggered arrivals.
* Optional return-path guides.
* **New: Ballistic Return**, a second node that applies the return to a finished simulation.

**Event Strength**

* **New: per-event strength sliders** at the top of the Velocity Mixer.

**Visualization**

* **New: Ghost Style** for the motion preview — Full Wireframe, Bounding Boxes (the new default) or Points.
* Preview Motion no longer switches itself off on heavy inputs.

**Bug fixes and improvements**

* **Fixed:** the three Point Source menus could display the wrong entry, and Point Source could not be picked from the Origin menu.
* **Fixed:** Output Guides Only now respects Preview Motion.
* **New: Propagate to All** buttons beside each event's Mute Gravity and Release Mode.
* Panel tidy-up, and creating an event now switches the Events list to its tab.

## Version 1.0

The launch feature set.

**Velocity types**

* Six velocity types on one node — Basic, Directional, Exploding, Velocity from Motion, Curl Noise and Angular.
* Adjust and Mask controls on every type, plus a one-click Randomize row.
* Directional velocity with a Direction Bias continuum from at-target through orbit to away.
* Exploding velocity from the whole object or a Point Source, with interactive viewport placement.
* Velocity inherited from animated input.
* Divergence-free curl turbulence with fractal detail and time evolution.

**Timed Events**

* Bake the setup into events at different frames and play them back as one timeline.
* Per-event Attack / Hold / Release envelopes in frames, with curve presets.
* Pulse timing — Hit, Build or Wave — as an alternative to the envelope.
* An on-screen event timeline with per-event state markers.
* Motion preview — guides and a tumbling ghost advanced to where the events predict.
* Rest-position attributes per event.
* Stagger Points, with an optional ramp and a choice of order.
* An Injecting Now output signal for gating an RBD solver.

**Mixing and output**

* Additive mixing with per-type gains, or weighted mixing, under one Master Speed.
* Incoming Velocity as its own stream, on by default.
* Velocity output for the RBD Bullet Solver, or accumulated force for POP and Vellum.
* Per-event Mute Gravity, plus Create Connected RBD Sim to wire a solver up in one click.
* Scale by Piece Size, from a mass attribute or each piece's real size.
* Speed clamping, per-stream exports and an Activation Age export.

**Visualization**

* Per-type guide trails scaled by each stream's real contribution to the mix.
* Guide density control, per-type colours and scales.
* A Utilities toggle to output the guide curves for rendering.

---

!!!info
Future updates and their changes will be listed here. Your purchase includes all future versions of Advanced Velocity at no extra cost — check back after updating to see what's new.
!!!
