---
icon: broadcast
order: 90
---

# Using RPLidar In

This page covers everything the node does once it's installed and connected: the three modes, the two outputs and their attributes, the on-screen guides, cropping, recording, and driving a live simulation. For a flat list of every control, see the [Parameter Reference](parameters.md).

## Modes

The **Mode** parameter is the master switch for the node. It has three settings.

![The Mode parameter — Off, Live, Playback](static/mode-menu.png)

### Off

Motor stopped, empty output. Use this whenever you aren't actively reading the sensor — it releases the serial port so other programs (or other Houdini sessions) can use it, and it stops the motor spinning.

> Any visualization guides you've enabled still draw in Off mode, so you can lay out your scene against the range ring without the sensor running.

### Live

Streams the sensor in real time. On the first cook the motor spins up over about two seconds, then every cook outputs the most recent full rotation as points.

* Choose the density with **Scan Mode** (below).
* The stream runs on a background thread, so no rotations are dropped between cooks — including while recording.
* **Test Sensor** prints live stream statistics while streaming (samples/second, valid points per rotation).

#### Scan Mode

Live only. Controls how fast the sensor samples:

| Setting | Rate | Points per rotation (typical) |
| --- | --- | --- |
| **Standard** | ~4,000 samples/s | ~110 valid |
| **Express** | ~8,000 samples/s | ~230 valid |

Express roughly doubles the point density. Changing Scan Mode while Live restarts the stream (about two seconds).

![Standard vs Express point density on the same scene](static/scan-mode-comparison.png)

### Playback

Plays a recorded `.jsonl` file against the playbar clock, so the scan is time-dependent and scrubs and renders like any other animated geometry. This lets you develop and iterate with the sensor disconnected. See [Recording & Playback](#recording-and-playback).

### A note on invalid returns

The sensor reports a sample for every laser pulse, but many pulses hit nothing in range (empty space, or a surface that doesn't reflect). Those come back as **invalid** and are filtered out — on a desk, more than half of every rotation can be invalid. This is normal, not a fault. The point counts above are *valid* points only.

---

## Outputs and attributes

RPLidar In has **two outputs** and no inputs.

| Output | Name | Contents | Use for |
| --- | --- | --- | --- |
| **0** | Points & Guides | Scan points **plus** any enabled visualization guides | Display / setup — this is the default when you display the node |
| **1** | Points | Scan points **only**, all guides stripped | Feeding solvers and downstream networks |

![The node's two outputs — Points & Guides, and Points](static/outputs.png)

Output 0 is the default display, so you see the sensor guide and range ring while you work. When you connect the node into a simulation, pull from **Output 1** — it removes the `rplidar_viz` guide geometry for you, so nothing display-only leaks into your solver.

> If you feed a solver from Output 0 by mistake, the guide points get simulated too. Either switch to Output 1, turn off the Visualize guides, or delete the `rplidar_viz` group downstream.

### The point cloud

Each valid laser return becomes one point. Invalid returns (empty space, no reflection) are filtered out — see [above](#a-note-on-invalid-returns).

**Position.** Point positions are in world units at your **Units per Meter** scale (default: meters). The layout:

* Angle **0°** points toward **−Z**.
* Angles increase **clockwise** seen from **+Y** (looking down at the sensor).
* The sensor sits at the origin.

**Per-point attributes:**

| Attribute | Type | Meaning |
| --- | --- | --- |
| `quality` | int | Return quality, 0–15. In Express mode valid samples report 15. |
| `angle` | float | Measured angle in degrees. |
| `dist` | float | Measured distance in **millimeters** (raw sensor units, before scaling). |

### Guide geometry

When visualization is on, the guides are added in the point/primitive group **`rplidar_viz`**, coloured via the point `Cd` attribute. This group only appears on Output 0. See [Visualization](#visualization).

---

## Visualization

The **Visualize** controls draw optional on-screen guides so you can see the sensor, its range, and its beams. All guides are extra geometry tagged with the point/primitive group **`rplidar_viz`**.

> **Guides are display-only geometry.** They travel on **Output 0 (Points & Guides)**. Feed a solver from **Output 1 (Points)**, which strips them automatically — or turn the guides off / delete the `rplidar_viz` group.

### Sensor guide

| Parameter | What it does |
| --- | --- |
| **Show Sensor Guide** | Draws a marker sphere at the origin (the sensor) plus a circle at the maximum range. On by default. |
| **Guide Color** | Color of the guide geometry (point `Cd`). |
| **Range (m)** | Radius of the range circle in real meters. The A2M12's maximum range is 16 m. |
| **Sensor Size (m)** | Diameter of the origin sphere marking the sensor, in real meters. |

![The sensor guide — origin marker and range ring around the scan points](static/sensor-guide.png)

### Connect Points (beam fan)

| Parameter | What it does |
| --- | --- |
| **Connect Points** | Draws a line from the sensor at the origin to each scan point — the beam fan spreading out as the laser sweeps. Off by default. Independent of the sensor guide. |
| **Ray Color** | Color of the connecting rays (point `Cd`). |

The rays use copies of the scan points, so your real scan points keep their own attributes untouched.

![The beam fan — rays drawn from the sensor to each scan point](static/beam-fan.png)

### Static map (bake)

Baking captures a short slice of the live stream into a fixed map — useful for seeing where the room's walls are while the live points keep moving.

| Parameter | What it does |
| --- | --- |
| **Bake Current Map** | Captures ~1.5 s of the live stream into a static map: short vertical marks where the beams are currently blocked. **Requires Mode = Live.** Re-baking overwrites the previous map. |
| **Show Static Map** | Overlay the baked map. Part of the `rplidar_viz` group. |
| **Map Color** | Color of the baked map marks (point `Cd`). |

![A baked static map showing the room's walls behind the live points](static/static-map.png)

---

## Attribute color

The **Attribute color** controls (in the Visualize folder, under **Store as Cd**) tint the scan points by their measured **angle** or **distance**, through a range remap and a color ramp. Use it to read the scan at a glance — near vs. far, or which direction each return came from — or to carry color downstream into a render.

| Parameter | What it does |
| --- | --- |
| **Store as Cd** | Master switch for where the color goes. **Off:** the color is shown for visualization only (on the Points & Guides output); the solver-ready output stays uncolored. **On:** the color is baked into the `Cd` attribute and travels downstream (below the node) on the clean output too. |
| **Angle** | Color the points by their `angle` attribute (which direction the return came from). |
| **Angle Range** | The angle range (degrees) mapped across the Angle ramp. Values outside are clamped. |
| **Angle Ramp** | The color ramp for angle. Default: an even yellow → blue → green → red around the circle. |
| **Distance** | Color the points by their `dist` attribute (how far the return is). |
| **Distance Range** | The distance range (millimeters) mapped across the Distance ramp. |
| **Distance Ramp** | The color ramp for distance. Default: orange near → teal far. |

Turn on **Angle**, **Distance**, or both. With both on, distance wins (it's applied last). The guides keep their own colors — only the real scan points are tinted.

![Scan points colored by distance — orange near the sensor fading to teal at range](static/attribute-color.png)

> **Store as Cd is the on/off for feeding color downstream.** Leave it off and the color is a viewport aid that never reaches your solver; turn it on when you want the `Cd` in a render or a color-driven effect.

---

## Crop

The **Crop** controls cull scan points that fall outside a rectangle on the ground, so only points inside the rectangle reach downstream nodes. This is useful when the sensor sits in the corner of a room and you only care about a stage, a doorway, or a walkway — everything outside the box is discarded before it hits your solver.

| Parameter | What it does |
| --- | --- |
| **Enable Crop** | Turn culling on. Points outside the rectangle are removed. A red guide shows the rectangle while this is on. |
| **Center** | Center of the rectangle on the ground (X, Z), relative to the sensor at the origin. |
| **Size** | Rectangle extent along X and Z. Default `26 × 26` (the sensor's full 16 m range spans `32 × 32`). |
| **Rotation** | Rotation of the rectangle about the sensor's vertical axis — align it to walls that aren't square to 0°. |
| **Edit Crop in Viewport** | Enter the interactive crop handle (see below). |

The Center, Size, and Rotation controls are disabled until **Enable Crop** is on.

![The red crop rectangle guide over a walkway, culling points outside it](static/crop-rectangle.png)

### Editing the crop in the viewport

You don't have to type numbers. Select the RPLidar In node in a Scene View (or press **Edit Crop in Viewport**) and a **box handle** appears over the crop rectangle, like a grid SOP:

* **Drag a side** to resize that edge.
* **Drag the body** to move the rectangle.
* **Drag the ring** to rotate it.

Everything writes straight back to the Center, Size, and Rotation parameters.

**Typical setup:**

1. Sensor in a room corner, scanning a walkway.
2. Enable Crop and watch the red guide.
3. Drag the box **sides** over the walkway (or type into **Center** / **Size**).
4. If the walkway runs at an angle to the sensor, **rotate** the box to line it up.

Now only points on the walkway survive, and stray returns from the rest of the room never reach your simulation.

---

## Camera

The **Camera** controls set up a top-down orthographic camera for the classic overhead installation look — the scan laid out flat, seen from directly above.

| Parameter | What it does |
| --- | --- |
| **Create Orthographic Camera** | Creates (or retargets) an orthographic camera at the object level, looking straight down at the sensor from above, framing the full sensor range. Its **up** direction is **+X**. One camera per node — pressing again retargets the same camera. |
| **Camera to Crop** | Moves and zooms that camera to frame the current **Crop** rectangle — centered on the crop, zoomed to its larger side, and rotated to match the crop's rotation. Create the camera first. |

A typical flow: **Create Orthographic Camera** to get the overhead view, set up your **Crop** over the area of interest, then **Camera to Crop** to zoom the camera onto exactly that region.

> The camera is created at the object (`/obj`) level, not inside the SOP network — look for it there (its path is printed to the console when created). Because it's orthographic, "zoom" is the framing width, not a focal length.

![The top-down orthographic view of a live scan, framed to the crop region](static/camera-topdown.png)

---

## Recording and playback

Recording captures the live stream to disk so you can replay it later — develop offline, iterate on a solver against a repeatable take, or archive an installation.

Each recording is a `.jsonl` file: one JSON line per rotation, holding the timestamp and the rotation's samples.

| Parameter | What it does |
| --- | --- |
| **Recording Directory** | Where recordings are saved and listed from. Defaults to `$HIP/rplidar-recordings`. |
| **Recording File** | The file used for Playback. The dropdown lists the directory. Leave it **blank to use the newest file**. |
| **Loop Playback** | Loop the recording. When off, the last scan is held after the file ends. |
| **Start Recording** | Begin writing the live stream to a new timestamped file. *Live mode only.* |
| **Stop Recording** | Finish the recording and auto-select it in **Recording File**. |
| **Delete Recording** | Delete the file currently picked in **Recording File** (asks for confirmation). |

**Recording a take:**

1. Set **Mode → Live** and confirm points are streaming.
2. Press **Start Recording**. A new timestamped `.jsonl` file is created in the Recording Directory.
3. Perform your take (walk through the scene, move objects, etc.).
4. Press **Stop Recording**. The finished file is selected in **Recording File** automatically.

Recording happens on the sensor's background reader thread, so no rotations are missed between Houdini cooks.

**Playing it back:**

1. Set **Mode → Playback**.
2. Pick a file in **Recording File** (or leave blank for the newest).
3. Scrub the timeline or press Play — the scan is driven by the playbar clock.

Use **Loop Playback** to cycle a short take continuously while you tune a downstream network.

---

## Live simulation

RPLidar In's point cloud is ordinary SOP geometry, so it can feed any solver — POPs, Vellum, or your own network. Two buttons set up a working example and its controls in one click.

### Create Generic POP Network

Press **Create Generic POP Network** and the node builds a ready-to-run POP network below itself, wired to the **solver-ready output** (Output 1, guides stripped), with presets tuned for live work. It also creates (or reuses) a small green **control null** and registers the new sim on it.

![The generated POP network wired to Output 1, with the green control null](static/pop-network.png)

### The control null

The green control null is the master runtime control for this sensor — **one per RPLidar In node**. (**Create Control Null** makes it on its own; Create Generic POP Network makes it for you.) It carries a **Solvers** list — every DOP network it drives — and three buttons:

| Button | What it does |
| --- | --- |
| **Start** | Sets RPLidar In to **Live** and plays the timeline in **real time**, running every listed sim against the live sensor. |
| **Stop** | Stops playback and sets RPLidar In back to **Off** (which stops the sensor motor). |
| **Reset** | Re-seeds every listed sim (clears the current particles) and rewinds, **without** stopping the motor. |

### How it actually runs — no Live Nodes

The live simulation is driven by **plain real-time timeline playback**, not by continuous cook / "Live Nodes." Pressing **Start** simply plays the timeline: each frame advances the sim *and* re-reads the sensor for a fresh rotation. That's all it needs.

> **What to watch:** the "it's running" indicator is the **playbar frame counter climbing** in real time — there is no live-simulation tick. If the frames are advancing and points are simulating, it's working.

Because a live installation never "finishes," **Start** sets a very long frame range (start … start + 1,000,000) so playback can run for hours. Keep that in mind — it overwrites your scene's frame range (see [Caching a take](#caching-a-take) for when that matters).

### Two ways to run the sim

* **Real time (Live):** press **Start** on the control null. The solver advances against the live sensor as the timeline plays. Best for interactive installations. Not deterministic — the input is whatever the room is doing right now.
* **Over a frame range (Playback):** Mode = Playback against a recording. The sim steps frame by frame from a repeatable input, so you can scrub, cache, and render a deterministic result.

### Caching a take

A **live** sim can't be cached deterministically — its input (the room) changes every real-world moment, so there's no "re-simulate frame 500 and get the same thing." To bake a repeatable result, go through the recording path:

1. **Capture the input.** In Live, **Start Recording**, perform your take, **Stop Recording** (see [Recording & Playback](#recording-and-playback)). The `.jsonl` is frame-locked and repeatable.
2. **Switch to Playback** and pick the recording. Now every frame produces the same scan, so the sim downstream is fully deterministic.
3. **Cache over a finite range.** Set your frame range to the recording's length — **not** the huge range that pressing Start leaves behind. Drop a **File Cache SOP** after the sim (or DOP I/O inside the network), set the range, and **Save to Disk**. Then flip it to **Load from Disk** to scrub and render the baked result.

> Don't cache against the 1,000,000-frame range that **Start** sets. Set a finite range first (or just don't press Start — for caching you drive the sim with the File Cache / the timeline yourself).

### Recipes

**Recipes** are pre-built downstream networks (a sim plus a look) shipped as a single `.py` file, so you can drop a finished effect behind the sensor. Enable **Use Recipe**, point **Recipe File** at the `.py`, and press **Generate Recipe** — it builds the network next to the node and registers its sims on the control null, ready to **Start**.

> Recipe files are executed Python. Only load recipe files from sources you trust.

### Building your own

There's nothing special about the generated network — you can wire the node's **Output 1** into any solver's source. Output 1 is the clean point cloud with all visualization guides removed, so it's safe to feed directly. See [Outputs and attributes](#outputs-and-attributes) for the per-point attributes you can read (`quality`, `angle`, `dist`).
