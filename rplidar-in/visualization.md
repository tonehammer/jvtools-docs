# Visualization

The **Visualize** folder draws optional on-screen guides so you can see the sensor, its range, and its beams. All guides are extra geometry tagged with the point/primitive group **`rplidar_viz`**.

> **Guides are display-only geometry.** They travel on **Output 0 (Points & Guides)**. Feed a solver from **Output 1 (Points)**, which strips them automatically — or turn the guides off / delete the `rplidar_viz` group. See [Output & Attributes](output.md).

## Sensor guide

| Parameter | What it does |
| --- | --- |
| **Show Sensor Guide** | Draws a marker sphere at the origin (the sensor) plus a circle at the maximum range. On by default. |
| **Guide Color** | Color of the guide geometry (point `Cd`). |
| **Range (m)** | Radius of the range circle in real meters. The A2M12's maximum range is 16 m. |
| **Sensor Size (m)** | Diameter of the origin sphere marking the sensor, in real meters. |

## Connect Points (beam fan)

| Parameter | What it does |
| --- | --- |
| **Connect Points** | Draws a line from the sensor at the origin to each scan point — the beam fan spreading out as the laser sweeps. Off by default. Independent of the sensor guide. |
| **Ray Color** | Color of the connecting rays (point `Cd`). |

The rays use copies of the scan points, so your real scan points keep their own attributes untouched.

## Static map (bake)

Baking captures a short slice of the live stream into a fixed map — useful for seeing where the room's walls are while the live points keep moving.

| Parameter | What it does |
| --- | --- |
| **Bake Current Map** | Captures ~1.5 s of the live stream into a static map: short vertical marks where the beams are currently blocked. **Requires Mode = Live.** Re-baking overwrites the previous map. |
| **Show Static Map** | Overlay the baked map. Part of the `rplidar_viz` group. |
| **Map Color** | Color of the baked map marks (point `Cd`). |

## Points convention

Point angle 0° points toward **−Z**, sweeping clockwise seen from **+Y** (looking down). Positions are in world units at your chosen **Units per Meter** scale.
