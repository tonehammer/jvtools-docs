---
icon: upload
order: 30
---

# Output & Attributes

## The two outputs

RPLidar In has **two outputs** and no inputs.

| Output | Name | Contents | Use for |
| --- | --- | --- | --- |
| **0** | Points & Guides | Scan points **plus** any enabled visualization guides | Display / setup — this is the default when you display the node |
| **1** | Points | Scan points **only**, all guides stripped | Feeding solvers and downstream networks |

Output 0 is the default display, so you see the sensor guide and range ring while you work. When you connect the node into a simulation, pull from **Output 1** — it removes the `rplidar_viz` guide geometry for you, so nothing display-only leaks into your solver.

> If you feed a solver from Output 0 by mistake, the guide points get simulated too. Either switch to Output 1, turn off the Visualize guides, or delete the `rplidar_viz` group downstream.

## The point cloud

Each valid laser return becomes one point. Invalid returns (empty space, no reflection) are filtered out — see [Modes](modes.md#a-note-on-invalid-returns).

### Position

Point positions are in world units at your **Units per Meter** scale (default: meters). The layout:

* Angle **0°** points toward **−Z**.
* Angles increase **clockwise** seen from **+Y** (looking down at the sensor).
* The sensor sits at the origin.

### Per-point attributes

| Attribute | Type | Meaning |
| --- | --- | --- |
| `quality` | int | Return quality, 0–15. In Express mode valid samples report 15. |
| `angle` | float | Measured angle in degrees. |
| `dist` | float | Measured distance in **millimeters** (raw sensor units, before scaling). |

## Guide geometry

When visualization is on, the guides are added in the point/primitive group **`rplidar_viz`**, coloured via the point `Cd` attribute. This group only appears on Output 0. See [Visualization](visualization.md).
