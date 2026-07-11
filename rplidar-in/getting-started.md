# Getting Started

This page takes you from an unopened sensor to your first live scan in Houdini.

## 1. Install the asset

Copy the `RPLidar_In.hdalc` file into your Houdini `otls` directory, or use **File → Import → Houdini Digital Asset** and point it at the file. It installs the SOP node type **RPLidar In**.

!!!warning Indie / Apprentice only
The asset is saved as `.hdalc`, which loads in Houdini **Indie** and **Apprentice** but **not** in commercial (FX/Core) licenses.
!!!

## 2. Connect the hardware

### The sensor

RPLidar In was developed against the **Slamtec RPLIDAR A2M12** — a 360°, 16 m range, spinning laser scanner. Other A2-family units should behave the same. The sensor stays completely silent until Houdini commands the motor to spin, so **no lights or sound when you first plug it in is normal**.

### The two cables

RPLIDAR units use two separate leads — **both must be connected** for a scan:

| Cable | Carries | Plug into |
| --- | --- | --- |
| **USB / data** | Data + adapter power, through the USB/UART adapter | Your computer |
| **5V / motor** | Motor power only | Any USB port or USB charger |

The motor lead can go to a plain charger — it does not need to be the same machine.

![The RPLIDAR sensor with its two leads and the CP210x USB/UART adapter](static/two-cables.png)

### The USB/UART adapter

The sensor connects through a **Silicon Labs CP210x** USB-to-serial adapter, which enumerates as a COM port on Windows (the driver ships with Windows 11, so it installs automatically). The adapter has a **baud-rate switch** — it **must be set to 256000** for the A2 family. At the wrong setting the device is completely silent.

Once connected, Windows gives the adapter a COM port (e.g. `COM3`).

![Close-up of the adapter's baud-rate switch set to 256000](static/adapter-baud-switch.png)

## 3. See your first scan

1. Drop down an **RPLidar In** SOP (inside a Geometry object).
2. Set **Mode** to **Live**.
3. Cook the node (display it in the viewport).

The motor spins up over about two seconds, then a ring of points appears — one point per laser return. Empty space in front of the sensor produces gaps; walls and objects produce dense arcs.

![The first scan — a dense arc of points where the sensor faces a wall](static/first-scan.png)

!!!info Lots of gaps is normal
On an open desk, most laser returns hit nothing in range and come back **invalid** — filtered out before they reach you. More than half of every rotation can be empty. Point the sensor at a wall to see a dense arc. See [Modes → invalid returns](using.md#a-note-on-invalid-returns).
!!!

If nothing appears, press **Test Sensor** to print the sensor's identity, health, and available scan modes to the console, then check [Troubleshooting](troubleshooting.md).

![Test Sensor console output showing the sensor's identity, health, and scan modes](static/test-sensor-console.png)

## 4. Set your working scale

Sensor distances are real-world meters. The **Units per Meter** parameter maps them to Houdini units:

* `1` (default) — work in meters. A wall 3 m away lands 3 units from the origin.
* `100` — work in centimeters.
* `0.5` — shrink the world to half size.

## 5. Finding the port

Leave the node's **Port** parameter blank and it auto-detects the CP210x adapter. If auto-detect picks the wrong device (e.g. you have several serial adapters), set the port explicitly — for example `COM3` on Windows.

!!!warning One program at a time
A serial port can only be opened by one process. If Houdini can't open the sensor, make sure no other program holds the port — a separate tester app, another Houdini session in Live mode, or a stale process. Set **Mode → Off** in any session you're not actively using.
!!!

## Where to go next

* Learn every mode and control → [Using RPLidar In](using.md).
* Develop without the sensor connected → [Recording & Playback](using.md#recording-and-playback).
* Drive a simulation from the live points → [Live Simulation](using.md#live-simulation).
* Something not working → [Troubleshooting](troubleshooting.md).
