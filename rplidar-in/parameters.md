---
icon: sliders
order: 80
---

# Parameter Reference

Every parameter on the RPLidar In node, grouped as it appears in the interface. Names in `code` are the internal parameter names.

## Main

| Parameter | Name | Description |
| --- | --- | --- |
| Mode | `mode` | Off / Live / Playback. The master switch. See [Modes](using.md#modes). |
| Pre-Rotate | `prerotate` | Spins the whole scan about the sensor, in degrees, so a physically-angled sensor lines up with your scene. Applied first, so Crop, tracking and the guides all follow. Turns the same way as Crop **Rotation**. |
| Create Control Null | `createnull` | Creates the master runtime-control null for this sensor (one per node) — Start / Stop / Reset buttons plus a Solvers list. See [Live Simulation](using.md#live-simulation). |
| Create Generic POP Network | `createpop` | Builds a ready-to-run POP network wired to the solver-ready output, and registers it on the control null. See [Live Simulation](using.md#live-simulation). |
| Use Recipe | `use_recipe` | Enables the recipe controls below. See [Recipes](using.md#recipes). |
| Recipe File | `recipefile` | A recipe `.py` file — a whole downstream network (sim + look). None ship with 1.0; point this at your own. |
| Generate Recipe | `recipegen` | Builds the picked recipe file next to the node and registers its sims on the control null. |

## Sensor

| Parameter | Name | Description |
| --- | --- | --- |
| Test Sensor | `testdevice` | Prints identity, health, and scan modes to the console. While Live, prints stream statistics instead. |
| Scan Mode | `scanmode` | Standard (~4k samples/s) or Express (~8k). Live only; changing it while Live restarts the stream. |
| Baud Rate | `baud` | Serial baud. 256000 is correct for the A2 family; other values are untested. |
| Units per Meter | `unitscale` | How many Houdini units represent one real meter. 1 = meters, 100 = centimeters. |
| Port | `port` | Serial port of the sensor's USB adapter (e.g. `COM3`). Blank = auto-detect the CP210x. |

## Crop

| Parameter | Name | Description |
| --- | --- | --- |
| Enable Crop | `cropenable` | Cull scan points outside the rectangle. Shows a red guide. |
| Center | `cropcenter` | Rectangle center on the ground (X, Z), relative to the sensor. |
| Size | `cropsize` | Rectangle extent along X and Z. Default 26 × 26 (the sensor's 16 m range spans 32 × 32). |
| Rotation | `croprot` | Rotation of the rectangle about the sensor's vertical axis. |
| Edit Crop in Viewport | `editcrop` | Enter the interactive crop handle — drag the sides to resize, body to move, ring to rotate. See [Crop](using.md#crop). |
| Fit to COP Space | `copfit` | Remap the output onto a default Copernicus canvas: the crop becomes −1 to +1 across X, centred on the sensor, rotation undone, and the ground plane stood up into XY. Off by default. See [Feeding a Copernicus network](using.md#feeding-a-copernicus-network). |
| COP Network | `copnetpath` | The Copernicus network this sensor feeds. Used only by Snap Crop to COP — it is not a cook dependency. |
| Snap Crop to COP | `snapcrop` | Set the crop's Size Z from the COP canvas's aspect, so the crop and the canvas are the same shape. Size X is left alone. |

## Camera

| Parameter | Name | Description |
| --- | --- | --- |
| Create Orthographic Camera | `makecam` | Create (or retarget) a top-down orthographic camera looking down at the sensor, up = +X. One per node. See [Camera](using.md#camera). |
| Camera to Crop | `camtocrop` | Move and zoom that camera to frame the current Crop rectangle. |

## Tracking

Cluster the scan into blobs and follow them across frames. See [Blob tracking](using.md#blob-tracking).

| Parameter | Name | Description |
| --- | --- | --- |
| Enable Tracking | `trackenable` | Master switch. Clusters the (cropped) scan into blobs, tracks them, and adds `id` + `v`. Off leaves the outputs unchanged. |
| Blob Mode | `trackmode` | Single (one primary blob, largest, held with hysteresis) or Multi (every blob, each with a stable id). |
| Solver Output | `solverout` | What Output 1 carries: All Points (the full scan cloud) or Blobs (only the tracked blob points). |
| Max Blobs | `trackmax` | Multi only — cap on how many blobs are emitted, largest first. |
| Cluster Gap (m) | `clustergap` | Max distance between neighbouring returns for them to count as one blob. Grows automatically with range. Raise to merge, lower to split. |
| Min Points | `minpoints` | Discard blobs with fewer returns than this — the noise floor. |
| Blob Size min/max (m) | `blobsize` | Keep only blobs whose physical width is in this range. A hand is roughly 0.05–0.15 m. |
| Subtract Background | `bgsubtract` | Track only what intrudes on the baked empty scene, so clustering ignores static clutter. Falls back to all points when nothing is baked. |
| Foreground Margin (m) | `bgmargin` | How much closer than the baked background a return must be to count as foreground. |
| Bake Background | `bgbake` | Capture the current static scene as that reference. **Live only** — bake with the interaction area empty. Shares its store with the Visualize map bake. |
| Position Smooth | `possmooth` | Smooths blob position over time. 0 = raw/snappy, 1 = heavily damped. |
| Velocity Smooth | `velsmooth` | Smooths the `v` attribute. 0 = raw, 1 = heavy. |
| Max Speed (m/s) | `maxspeed` | Association gate and velocity clamp — a blob can't move faster than this between frames and still be the same track. |
| Hold Time (s) | `holdtime` | Keep a lost track alive this long (coasting to a stop) before dropping it. Bridges brief dropouts. |
| Show Markers | `trackviz` | Draw a diamond + velocity line at each tracked blob. Guide geometry — stripped from Output 1. |
| Marker Color | `blobcolor` | Color of the blob markers (point `Cd`). |

## Recording

| Parameter | Name | Description |
| --- | --- | --- |
| Recording Directory | `recdir` | Where recordings are saved and listed from. Default `$HIP/rplidar-recordings`. |
| Recording File | `recording` | File used for Playback. Blank = newest in the directory. |
| Loop Playback | `loop` | Loop the recording; off holds the last scan. |
| Start Recording | `recstart` | Begin writing the live stream to a new file. Live only. |
| Stop Recording | `recstop` | Finish and select the new recording. |
| Delete Recording | `recdelete` | Delete the picked file (with confirmation). |

## Visualize

| Parameter | Name | Description |
| --- | --- | --- |
| Show Sensor Guide | `visualize` | Draw the origin sensor marker + range ring. On by default. |
| Guide Color | `vizcolor` | Color of the guide geometry. |
| Range (m) | `vizrange` | Radius of the range circle in real meters (A2M12 max 16 m). |
| Sensor Size (m) | `vizsensor` | Diameter of the origin sphere, in real meters. |
| Connect Points | `vizrays` | Draw a line from the sensor to each scan point (the beam fan). Off by default. |
| Ray Color | `vizraycolor` | Color of the connecting rays. |
| Store as Cd | `attrcd` | Bake the attribute colors below into `Cd` so they travel downstream. Off = the colors are shown for visualization only. See [Attribute color](using.md#attribute-color). |
| Angle (enable) | `angle_enable` | Color the scan points by their `angle` attribute. |
| Angle Range | `angle_range` | Attribute value range mapped onto the Angle ramp (outside clamped). |
| Angle Ramp | `angle_ramp` | Color across the remapped angle range. |
| Distance (enable) | `dist_enable` | Color the scan points by their `dist` attribute. |
| Distance Range | `dist_range` | Attribute value range mapped onto the Distance ramp (outside clamped). |
| Distance Ramp | `dist_ramp` | Color across the remapped distance range. |
| Bake Current Map | `mapbake` | Capture ~1.5 s of the live stream into a static map. Live only. |
| Show Static Map | `mapshow` | Overlay the baked static map. |
| Map Color | `mapcolor` | Color of the baked map marks. |

See [Visualization](using.md#visualization) and [Attribute color](using.md#attribute-color).

## Utilities

| Parameter | Name | Description |
| --- | --- | --- |
| Links | `gumroad` | Open the RPLidar In store page in your browser. |
| (Documentation) | `docs` | Open this documentation. |
| (Discord) | `discord` | Open the JVtools Discord. |
| (YouTube) | `youtube` | Open the JVtools YouTube channel. |

---

> Tooltips in Houdini (hover any parameter) are the authoritative, always-current descriptions. If this page and a tooltip ever disagree, trust the tooltip.
