# Using RPLidar In

*This is a test rewrite of the [original page](/rplidar-in/using/).*

This page walks through the three modes, the two outputs, the on-screen guides, cropping, recording, and driving a live simulation. For a flat list of every control, see the [Parameter Reference](/rplidar-in/parameters/).

## Modes

**Mode** is the master switch on the node. Three settings.

### Off

Motor stopped, no output. Use this when you're not actively reading the sensor -- it frees up the serial port for other programs and stops the motor spinning.

> Guides you've enabled still draw in Off mode, so you can lay out your scene against the range ring without the sensor running.

### Live

Streams the sensor in real time. The motor spins up on the first cook (about two seconds), then every cook outputs the latest full rotation as points.

* Choose the density with **Scan Mode** (below).
* Rotations aren't dropped between cooks, even while recording.
* **Test Sensor** prints live stream stats while streaming (samples/second, valid points per rotation).

#### Scan Mode

Live only. How fast the sensor samples:

| Setting | Rate | Points per rotation (typical) |
| --- | --- | --- |
| **Standard** | ~4,000 samples/s | ~110 valid |
| **Express** | ~8,000 samples/s | ~230 valid |

Express roughly doubles the point density. Changing Scan Mode while Live restarts the stream (about two seconds).

### Playback

Plays a recorded `.jsonl` file against the playbar clock, so the scan scrubs and renders like any other animated geometry. Good for developing with the sensor disconnected. See [Recording & Playback](#recording-and-playback).

### A note on invalid returns

Not every laser pulse hits something -- empty space or a non-reflective surface comes back **invalid** and gets filtered out. On a desk, more than half of every rotation can be invalid. That's normal, not a fault. The point counts above are valid points only.

---

## Outputs and attributes

RPLidar In has **two outputs** and no inputs.

| Output | Name | Contents | Use for |
| --- | --- | --- | --- |
| **0** | Points & Guides | Scan points **plus** any enabled visualization guides | Display / setup -- the default when you display the node |
| **1** | Points | Scan points **only**, guides stripped | Feeding solvers and downstream networks |

Output 0 is the default display, so you see the sensor guide and range ring while you work. When you connect the node into a simulation, pull from **Output 1** -- it strips the `rplidar_viz` guide geometry for you.

> **Output 1 is switchable.** With [Blob tracking](#blob-tracking) on, the **Solver Output** menu decides whether it carries the whole scan cloud or just the tracked blob points. If a solver suddenly sees three points instead of three hundred, check that menu first.

> If you feed a solver from Output 0 by mistake, the guide points get simulated too. Switch to Output 1, turn off the Visualize guides, or delete the `rplidar_viz` group downstream.

### The point cloud

Each valid laser return becomes one point. Invalid returns are filtered out.

**Position.** Point positions are in world units at your **Units per Meter** scale (default: meters).

* Angle **0 deg** points toward **-Z**.
* Angles increase **clockwise** seen from **+Y** (looking down at the sensor).
* The sensor sits at the origin.

**Per-point attributes:**

| Attribute | Type | Meaning |
| --- | --- | --- |
| `quality` | int | Return quality, 0-15. In Express mode valid samples report 15. |
| `angle` | float | Measured angle in degrees. |
| `dist` | float | Measured distance in **millimeters** (raw sensor units, before scaling). |

### Guide geometry

When visualization is on, the guides are added in the point/primitive group **`rplidar_viz`**, coloured via the point `Cd` attribute. This group only appears on Output 0. See [Visualization](#visualization).

---

## Visualization

The **Visualize** controls draw optional on-screen guides so you can see the sensor, its range, and its beams. All guides sit in the group **`rplidar_viz`**.

> **Guides are display-only.** They travel on Output 0. Feed a solver from Output 1, which strips them automatically -- or turn the guides off / delete the `rplidar_viz` group.

### Sensor guide

| Parameter | What it does |
| --- | --- |
| **Show Sensor Guide** | Draws a marker sphere at the origin (the sensor) plus a circle at max range. On by default. |
| **Guide Color** | Color of the guide geometry. |
| **Range (m)** | Radius of the range circle in real meters. The A2M12's max range is 16 m. |
| **Sensor Size (m)** | Diameter of the origin sphere, in real meters. |

### Connect Points (beam fan)

| Parameter | What it does |
| --- | --- |
| **Connect Points** | Draws a line from the sensor to each scan point -- the beam fan. Off by default. Independent of the sensor guide. |
| **Ray Color** | Color of the connecting rays. |

The rays use copies of the scan points, so your real scan points keep their own attributes untouched.

### Static map (bake)

Baking captures a short slice of the live stream into a fixed map -- useful for seeing where the room's walls are while the live points keep moving.

| Parameter | What it does |
| --- | --- |
| **Bake Current Map** | Captures ~1.5 s of the live stream into a static map. **Requires Mode = Live.** Re-baking overwrites the previous map. |
| **Show Static Map** | Overlay the baked map. Part of `rplidar_viz`. |
| **Map Color** | Color of the baked map marks. |

---

## Attribute color

The **Attribute color** controls (in Visualize, under **Store as Cd**) tint the scan points by their measured **angle** or **distance**, through a range remap and a color ramp. Handy for reading the scan at a glance, or for carrying color downstream into a render.

| Parameter | What it does |
| --- | --- |
| **Store as Cd** | Master switch for where the color goes. **Off:** color is visualization only, the solver-ready output stays uncolored. **On:** color is baked into `Cd` and travels downstream on the clean output too. |
| **Angle** | Color the points by `angle` (which direction the return came from). |
| **Angle Range** | The angle range (degrees) mapped across the Angle ramp. Values outside are clamped. |
| **Angle Ramp** | Color ramp for angle. Default: yellow -> blue -> green -> red around the circle. |
| **Distance** | Color the points by `dist` (how far the return is). |
| **Distance Range** | The distance range (millimeters) mapped across the Distance ramp. |
| **Distance Ramp** | Color ramp for distance. Default: orange near -> teal far. |

Turn on Angle, Distance, or both -- with both on, distance wins (applied last). Guides keep their own colors; only the real scan points are tinted.

> **Store as Cd is the on/off for feeding color downstream.** Leave it off and the color is just a viewport aid; turn it on when you want the `Cd` in a render or a color-driven effect.

---

## Crop

The **Crop** controls cull scan points outside a rectangle on the ground, so only points inside it reach downstream nodes. Useful when the sensor sits in the corner of a room and you only care about a stage, doorway, or walkway.

| Parameter | What it does |
| --- | --- |
| **Enable Crop** | Turn culling on. Points outside the rectangle are removed. A red guide shows the rectangle while this is on. |
| **Center** | Center of the rectangle on the ground (X, Z), relative to the sensor at the origin. |
| **Size** | Rectangle extent along X and Z. Default `26 x 26` (the sensor's full 16 m range spans `32 x 32`). |
| **Rotation** | Rotation of the rectangle about the sensor's vertical axis -- align it to walls that aren't square to 0 deg. |
| **Edit Crop in Viewport** | Enter the interactive crop handle (see below). |

Center, Size, and Rotation stay disabled until Enable Crop is on.

### Editing the crop in the viewport

You don't have to type numbers. Select the RPLidar In node in a Scene View (or press **Edit Crop in Viewport**) and a box handle appears over the crop rectangle, like a grid SOP:

* **Drag a side** to resize that edge.
* **Drag the body** to move the rectangle.
* **Drag the ring** to rotate it.

Everything writes straight back to Center, Size, and Rotation.

**Typical setup:**

1. Sensor in a room corner, scanning a walkway.
2. Enable Crop and watch the red guide.
3. Drag the box sides over the walkway (or type into Center / Size).
4. If the walkway runs at an angle to the sensor, rotate the box to line it up.

Now only points on the walkway survive.

---

## Camera

The **Camera** controls set up a top-down orthographic camera for the classic overhead installation look.

| Parameter | What it does |
| --- | --- |
| **Create Orthographic Camera** | Creates (or retargets) an orthographic camera at the object level, looking straight down at the sensor, framing its full range. Up direction is +X. One camera per node -- pressing again retargets the same camera. |
| **Camera to Crop** | Moves and zooms that camera to frame the current Crop rectangle. Create the camera first. |

Typical flow: Create Orthographic Camera for the overhead view, set up your Crop, then Camera to Crop to zoom onto that region.

> The camera lives at the object (`/obj`) level, not inside the SOP network -- its path is printed to the console when created.

---

## Blob tracking

A raw scan is a few hundred loose points that vanish and reappear every rotation -- fine for a point cloud, wrong shape for most interactive work. What you usually want to know is "where is the hand, and how fast is it moving," and a cloud of anonymous points can't answer that.

**Blob tracking** answers it. It clusters the scan into blobs, follows each one across frames, and gives it a stable **id** and a **velocity**.

Turn on **Enable Tracking** in the Tracking tab. Everything below works on the scan *after* [Crop](#crop) -- crop first, then track.

| Parameter | What it does |
| --- | --- |
| **Enable Tracking** | Master switch. Off, nothing changes about the outputs. |
| **Blob Mode** | **Single** emits one primary blob -- the largest, held with hysteresis so it doesn't flicker. **Multi** emits every blob found, each with its own stable id. |
| **Solver Output** | What Output 1 carries: **All Points** (whole scan cloud) or **Blobs** (only tracked blob points). |
| **Max Blobs** | Multi only -- a cap, largest first. |

Single is for "one hand, one object, one person" installations. Multi is for many things at once -- each blob keeps its id as long as the tracker can follow it.

### Background subtraction

Read this before tuning anything else. Raw clustering of a real room usually finds several blobs, and the largest one is almost never the hand -- it's a chair leg, a wall corner, a box. Single mode locks onto furniture and stays there. Nothing is broken; the furniture genuinely is the biggest thing in the room.

The fix: tell the node what the empty room looks like, then track only what intrudes on it.

| Parameter | What it does |
| --- | --- |
| **Subtract Background** | Track only returns closer than the baked empty scene. Falls back to the full scan when nothing is baked yet, so it can't silently blank your tracking. |
| **Foreground Margin (m)** | How much closer than the background a return must be to count. Raise to reject noise hugging a wall; lower to catch objects sitting right against the background. |
| **Bake Background** | Capture the current static scene as the reference. **Requires Mode = Live.** |

Workflow:

1. Go Live, and clear the interaction area.
2. Press Bake Background.
3. Turn on Subtract Background, then walk back in.

With a background bake, tracking locks onto you instead of the furniture -- clean tracking on a room that used to confuse it.

Careful with this one: bake with the area **empty**. Bake while you're standing in it and you've taught the node that you're part of the wall -- after which you become invisible to it. Re-bake whenever you move the sensor or rearrange the room.

**Bake Background shares its storage with the Visualize tab's Bake Current Map** -- one snapshot serves both, so baking on either button replaces the other. Turn on Show Static Map to see the background you just baked.

### Clustering

These decide what counts as one blob.

| Parameter | What it does |
| --- | --- |
| **Cluster Gap (m)** | How far apart two neighbouring returns can be and still belong to the same blob. Raise to merge, lower to split. |
| **Min Points** | Blobs with fewer returns than this are discarded -- the noise floor. |
| **Blob Size min/max (m)** | Keep only blobs whose physical width falls in this range. |

**Blob Size does the most work.** A hand is roughly 0.05-0.15 m across; a wall reads far wider. Set a sane maximum first -- it throws out room geometry and saves you tuning everything else.

Cluster Gap **grows automatically with distance**. Returns get sparser further out, so a fixed gap that works at one meter would shred a single object into five at eight meters -- the node scales it out for you.

### Smoothing and association

These decide how a blob behaves once it *is* a blob -- where the difference between "twitchy" and "usable" lives.

| Parameter | What it does |
| --- | --- |
| **Position Smooth** | Smooths blob position over time. 0 = raw and snappy, 1 = heavily damped. |
| **Velocity Smooth** | Smooths the `v` attribute. Raise it if velocity looks noisy driving a solver. |
| **Max Speed (m/s)** | Both an association gate and a clamp: a blob can't move faster than this between frames and still be considered the same track. |
| **Hold Time (s)** | Keep a lost track alive this long, coasting to a stop, before dropping it. |

Some position smoothing is nearly always right, since a centroid from a handful of noisy returns jitters even when the hand is still -- but it buys steadiness with lag, and past about 0.7 things start feeling like they're responding underwater.

**Max Speed is the anti-teleport control.** Lower it and a track refuses implausible jumps; raise it for genuinely fast motion. Too low and a fast hand gets abandoned mid-swipe and comes back as a new id.

**Hold Time** bridges brief dropouts -- a hand turning edge-on, a rotation that catches nothing. Without it, every flicker starts a fresh id and resets anything keyed to it. A quarter of a second covers most dropouts without leaving ghosts hanging around.

### What tracking outputs

Tracked blobs come out as one point per blob in the group **`rplidar_track`**, carrying:

| Attribute | Type | Meaning |
| --- | --- | --- |
| `id` | int | Stable track id. Survives as long as the tracker can follow the blob. |
| `v` | vector | Velocity in units per second (at your Units per Meter scale). |
| `age` | float | Seconds since the track was born. |
| `size` | float | Physical width of the blob, in meters. |
| `angle` / `dist` | float | Same meaning as on the scan points -- degrees, and millimeters. |

Set Solver Output to Blobs and Output 1 carries exactly these points -- a handful with velocity, instead of a few hundred anonymous ones, which is what you want feeding a POP force or a Vellum collider.

`v` is a real velocity attribute, so POP nodes that read `v` pick it up with no conversion. That, plus the stable `id`, is the whole point of tracking: your effect can follow *this* blob rather than reacting to whatever's nearby.

### Markers

| Parameter | What it does |
| --- | --- |
| **Show Markers** | Draw a diamond plus a velocity line at each tracked blob. On by default. |
| **Marker Color** | Color of those markers. |

The velocity line is the useful half -- direction and magnitude at a glance, so you can see whether smoothing is too aggressive or Max Speed is clipping. Markers are guide geometry: they ride on Output 0 and are stripped from Output 1.

> Tuning tip: turn markers on, put the node's display flag up, and move around in front of the sensor. If the diamond follows you, you're done. If it sits on a chair, you skipped the background bake.

---

## Recording and playback

Recording captures the live stream to disk so you can replay it later -- develop offline, iterate on a solver against a repeatable take, or archive an installation.

Each recording is a `.jsonl` file: one JSON line per rotation, holding the timestamp and the rotation's samples.

| Parameter | What it does |
| --- | --- |
| **Recording Directory** | Where recordings are saved and listed from. Defaults to `$HIP/rplidar-recordings`. |
| **Recording File** | The file used for Playback. The dropdown lists the directory. Leave blank to use the newest file. |
| **Loop Playback** | Loop the recording. When off, the last scan holds after the file ends. |
| **Start Recording** | Begin writing the live stream to a new timestamped file. Live mode only. |
| **Stop Recording** | Finish the recording and auto-select it in Recording File. |
| **Delete Recording** | Delete the file currently picked in Recording File (asks for confirmation). |

**Recording a take:**

1. Set Mode -> Live and confirm points are streaming.
2. Press Start Recording. A new timestamped `.jsonl` file is created.
3. Perform your take (walk through the scene, move objects, etc.).
4. Press Stop Recording. The finished file is auto-selected.

No rotations are missed between Houdini cooks while recording.

**Playing it back:**

1. Set Mode -> Playback.
2. Pick a file in Recording File (or leave blank for the newest).
3. Scrub the timeline or press Play -- the scan follows the playbar clock.

Use Loop Playback to cycle a short take continuously while you tune a downstream network.

---

## Live simulation

RPLidar In's point cloud is ordinary SOP geometry, so it can feed any solver -- POPs, Vellum, or your own network. Two buttons set up a working example in one click.

> Feeding the raw cloud is the straightforward route, and often all you need for emission or collision. But if your effect should follow *a person* rather than react to a wall of points, set up [Blob tracking](#blob-tracking) first and set Solver Output to Blobs -- a far better thing to attach a force to.

### Create Generic POP Network

Press **Create Generic POP Network** and the node builds a ready-to-run POP network below itself, wired to the solver-ready output (Output 1), with presets tuned for live work. It also creates (or reuses) a small green control null and registers the new sim on it.

### The control null

The green control null is the master runtime control for this sensor -- one per RPLidar In node. (Create Control Null makes it on its own; Create Generic POP Network makes it for you.) It carries a Solvers list -- every DOP network it drives -- and three buttons:

| Button | What it does |
| --- | --- |
| **Start** | Sets RPLidar In to Live and plays the timeline in real time, running every listed sim against the live sensor. |
| **Stop** | Stops playback and sets RPLidar In back to Off (which stops the motor). |
| **Reset** | Re-seeds every listed sim (clears the current particles) and rewinds, without stopping the motor. |

### How it actually runs

The live simulation is driven by plain real-time timeline playback, not continuous cook. Pressing Start plays the timeline: each frame advances the sim and re-reads the sensor for a fresh rotation.

> What to watch: the "it's running" indicator is the playbar frame counter climbing in real time. If frames are advancing and points are simulating, it's working.

Because a live installation never "finishes," Start sets a very long frame range (start ... start + 1,000,000) so playback can run for hours. That overwrites your scene's frame range -- see [Caching a take](#caching-a-take) for when that matters.

### Two ways to run the sim

* **Real time (Live):** press Start on the control null. The solver advances against the live sensor as the timeline plays. Best for interactive installations -- not deterministic, since the input is whatever the room is doing right now.
* **Over a frame range (Playback):** Mode = Playback against a recording. The sim steps frame by frame from a repeatable input, so you can scrub, cache, and render a deterministic result.

### Caching a take

A live sim can't be cached deterministically -- the room changes every real-world moment, so there's no "re-simulate frame 500 and get the same thing." To bake a repeatable result, go through the recording path:

1. **Capture the input.** In Live, Start Recording, perform your take, Stop Recording (see [Recording & Playback](#recording-and-playback)). The `.jsonl` is frame-locked and repeatable.
2. **Switch to Playback** and pick the recording. Every frame now produces the same scan, so the sim downstream is fully deterministic.
3. **Cache over a finite range.** Set your frame range to the recording's length -- not the huge range Start leaves behind. Drop a File Cache SOP after the sim, set the range, and Save to Disk. Then flip it to Load from Disk to scrub and render the baked result.

> Don't cache against the 1,000,000-frame range that Start sets. Set a finite range first, or just don't press Start -- drive the sim with the File Cache / the timeline yourself.

### Recipes

A **recipe** is a whole downstream network -- a sim plus a look -- packed into a single `.py` file, so a finished effect can be dropped in behind the sensor in one press. Enable Use Recipe, point Recipe File at the `.py`, and press Generate Recipe: it builds the network next to the node, inside its own subnet, and registers its sims on the control null.

!!!warning No recipes ship with 1.0
The machinery works, but there's nothing in the box to load yet -- recipe packs are planned as a separate release. For now this is a way to load your own recipe file, or one someone shares with you. See [Building your own](#building-your-own) below.
!!!

> Recipe files are executed Python. Only load recipe files from sources you trust.

### Building your own

There's nothing special about the generated network -- you can wire the node's Output 1 into any solver's source. It's the clean point cloud with all visualization guides removed, so it's safe to feed directly. See [Outputs and attributes](#outputs-and-attributes) for the per-point attributes you can read (`quality`, `angle`, `dist`).
