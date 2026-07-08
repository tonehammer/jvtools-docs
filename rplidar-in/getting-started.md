---
icon: :rocket:
order: 100
---

# Getting Started

## 1. Install the asset

Copy the `RPLidar_In.hdalc` file into your Houdini otls directory, or use **File → Import → Houdini Digital Asset** and point it at the file. It installs the SOP node type **RPLidar In**.

> **Indie / Apprentice only.** The asset is saved as `.hdalc`, which loads in Houdini Indie and Apprentice but **not** in commercial (FX/Core) licenses.

## 2. Connect the sensor

See [Hardware & Cabling](hardware.md) for the full wiring. In short:

1. Plug the **data cable** (through the USB/UART adapter) into your computer.
2. Plug the **5V motor cable** into any USB port or charger.
3. Make sure the adapter's baud switch is set to **256000** (correct for the A2 family).

Windows should install the CP210x driver automatically and give the adapter a COM port (e.g. `COM3`).

## 3. See your first scan

1. Drop down an **RPLidar In** SOP (inside a Geometry object).
2. Set **Mode** to **Live**.
3. Cook the node (display it in the viewport).

The motor spins up over about two seconds, then a ring of points appears — one point per laser return. Empty space in front of the sensor produces gaps; walls and objects produce dense arcs.

If nothing appears, press **Test Sensor** to print the sensor's identity, health, and available scan modes to the console, and check [Troubleshooting](troubleshooting.md).

## 4. Set your working scale

Sensor distances are real-world meters. The **Units per Meter** parameter maps them to Houdini units:

* `1` (default) — work in meters. A wall 3 m away lands 3 units from the origin.
* `100` — work in centimeters.
* `0.5` — shrink the world to half size.

## Where to go next

* Develop without the sensor connected → [Recording & Playback](recording.md).
* Drive a simulation from the live points → [Live Simulation](live-sim.md).
* Understand the point cloud → [Output & Attributes](output.md).
