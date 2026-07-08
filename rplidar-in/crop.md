---
icon: filter
order: 50
---

# Crop

The **Crop** folder culls scan points that fall outside a rectangle on the ground, so only points inside the rectangle reach downstream nodes. This is useful when the sensor sits in the corner of a room and you only care about a stage, a doorway, or a walkway — everything outside the box is discarded before it hits your solver.

| Parameter | What it does |
| --- | --- |
| **Enable Crop** | Turn culling on. Points outside the rectangle are removed. A red guide shows the rectangle while this is on. |
| **Center** | Center of the rectangle on the ground (X, Z), relative to the sensor at the origin. |
| **Size** | Rectangle extent along X and Z. Default `32 × 32` encloses the sensor's full 16 m range (so nothing is cropped until you shrink it). |
| **Rotation** | Rotation of the rectangle about the sensor's vertical axis — align it to walls that aren't square to 0°. |

The Center, Size, and Rotation controls are disabled until **Enable Crop** is on.

## Typical setup

1. Sensor in a room corner, scanning a walkway.
2. Enable Crop and watch the red guide.
3. Drag **Center** over the walkway and shrink **Size** to just cover it.
4. If the walkway runs at an angle to the sensor, dial **Rotation** to line the box up.

Now only points on the walkway survive, and stray returns from the rest of the room never reach your simulation.
