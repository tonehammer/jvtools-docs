---
icon: sliders
order: 110
---

# Parameter reference

<!-- 🔴 The parm Help fields on the HDA are the SOURCE OF TRUTH for tooltips.
     This page syncs FROM them, never the reverse, and all layers sync MANUALLY
     (STANDARDS §9). Re-read this page whenever a feature lands — a stale
     reference page is worse than none. -->

In panel order. Every linkable parameter has a **Link** checkbox beside it, which decides whether Connect includes it — it does not switch the parameter off.

## Top

| Parameter | |
|---|---|
| **DOP Network** | The dopnet holding your sim. FLIP nodes are found by type, not name. Leave empty to drive only Add Linked SOPs. |
| **Connect Parameters** | Writes channel references onto the targets and reports what it wrote. |
| **Unlink** | Removes them, freezing each target at its current value. |

## Add Linked SOPs

| Parameter | |
|---|---|
| **SOP** | The node to drive. Absolute path. |
| **Send** | Particle Separation, Voxel Size or Grid Scale. |
| **Target Parameter** | The parameter name on that SOP. Typed explicitly — the name varies by node version. |
| **Multiplier** | Scales the value on its way over. |

## FLIP Parameters

| Parameter | | Links to |
|---|---|---|
| **Drive By** | Which of Particle Separation / Voxel Size you author. The other is derived and greys out. | — |
| **Particle Separation** | Distance between particles; the master resolution control. | FLIP Object |
| **Voxel Size** | One grid cell. Derived as separation × grid scale. | nothing — no FLIP node takes one |
| **Grid Scale** | Voxel size as a multiple of separation. 2 is the default. | FLIP Object |
| **Min Substeps** | Fewest substeps per frame. Raise it when fast fluid tunnels through collisions. | FLIP Solver |
| **Max Substeps** | Most substeps per frame — your ceiling on frame cost. | FLIP Solver |
| **CFL Condition** | How far fluid may travel per substep, in voxels. Lower is more accurate and slower. | FLIP Solver |
| **Closed Boundaries** | Whether the boundary is solid. Off, fluid leaves the container. | FLIP Object |

## Bounding Box Setup

| Parameter | | Links to |
|---|---|---|
| **Size** | Container size per axis. | Solver ▸ Volume Limits |
| **Center** | Container centre. | Solver ▸ Volume Limits |
| **Match Input Size** | Fits the box to the input, and unlocks the settings below. Resets Size and Center first. | — |
| **Match Size to Parms** | Bakes the fit into Size and Center, and turns Match Input Size off. | — |
| **Translate** | Whether the fit moves the box or only resizes it. | — |
| **Scale to Fit** | Whether the box is scaled to the input's bounds. | — |
| **Uniform Fit** | On keeps the box's proportions; off hugs each axis. | — |
| **Scale Axis** | Which axis a uniform fit takes its scale from. | — |
| **Uniform Scale** | Overall multiplier, applied last. | — |
| **Bbox Visualization Color** | Viewport colour. Display only. | — |

## DOP Parameters

Both target the DOP Network, not the FLIP nodes.

| Parameter | | Links to |
|---|---|---|
| **Cache Memory (MB)** | Memory for cached frames. When full, the oldest are dropped. | DOP Network |
| **Time Scale** | Simulation time multiplier. Scales the whole dopnet, every object in it. | DOP Network |

## Utilities

| Parameter | |
|---|---|
| **Status** | What is linked, as of the last Connect or Unlink. Not a live watch. |
| **Links** | Website, Gumroad, docs, Discord, YouTube. |
| **Current Version** | The version you have installed. An update notice appears below it when there is a newer one. |
