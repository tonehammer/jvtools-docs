# Using FLIP DOP Controller

Set **DOP Network**, press **Connect Parameters**, then work from this panel. Connect writes channel references onto the targets, so the values live here and the sim reads them.

## What goes where

| This node | Target |
|---|---|
| Particle Separation, Grid Scale, Closed Boundaries | FLIP Object |
| Min/Max Substeps, CFL Condition | FLIP Solver |
| Size, Center | FLIP Solver — Volume Limits |
| Cache Memory, Time Scale | DOP Network |

FLIP nodes are found by **type**, not name; more than one of either and you are asked which. **Voxel Size connects to nothing** — no FLIP node takes one.

## The Link checkboxes

They decide whether Connect includes that parameter. **They do not switch the parameter off.** All default on.

## Unlink

Removes what this node wrote and freezes each target at its current value. It only removes its own expressions; anything else is reported and left alone. On **Connect**, a foreign expression *is* taken over, and named in the report.

## Add Linked SOPs

One row per parameter driven: the **SOP**, which value to **Send**, the **Target Parameter**, and a **Multiplier**. The target is typed explicitly because the name is not stable — Particle Fluid Surface 3.0 uses `particlesep`, version 1 uses `stepsize`. One that does not exist is reported, never silently skipped.

Leave **DOP Network** empty and Connect drives only these rows.

## The container box

Drives the solver's Volume Limits. **Match Input Size** fits it to the input; **Match Size to Parms** bakes that into Size and Center and switches the fit off.

**There is no Rotate** — the solver's Volume Limits are axis-aligned, so a rotated box would draw one boundary while the sim enforced another.

## Traps

- **Particle Separation is the one that matters** — halving it is roughly eight times the particles.
- **Time Scale slows the whole DOP Network**, every object in it, not just the fluid.
- **Status is a record, not a live watch.** It does not see hand edits in the dopnet.
