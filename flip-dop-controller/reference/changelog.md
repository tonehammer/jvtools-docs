# Changelog

## v1.0 — 29 August 2026

First release.

**Linking**

- New: **Connect Parameters** writes channel references onto the FLIP Object, the FLIP Solver and the DOP Network so they read from this node.
- New: **Unlink** removes them, freezing every target at its current value.
- New: a **Link** checkbox per parameter decides what gets connected.
- New: FLIP nodes are found by node type, not by name, so they can be called anything.
- New: a target already carrying an expression is taken over and named in the report.
- New: **Status** readout reports what is currently linked.

**Controls**

- New: Particle Separation, Grid Scale, Min/Max Substeps, CFL Condition and Closed Boundaries.
- New: Cache Memory and Time Scale, targeting the DOP Network.
- New: **Drive By** menu decides whether you author Particle Separation or Voxel Size.

**Container**

- New: the simulation container box is built here and drives the FLIP Solver's Volume Limits.
- New: **Match Input Size** fits the box to incoming geometry; **Match Size to Parms** bakes the fit.
- New: the box is drawn as guide geometry, so it never enters the geometry stream.

**Linked SOPs**

- New: **Add Linked SOPs** sends a value to any downstream SOP, with an explicit target parameter and a multiplier.
- New: a target parameter that does not exist is reported, never silently skipped.
- New: works with no DOP Network at all — Linked SOPs rows alone are a valid setup.
