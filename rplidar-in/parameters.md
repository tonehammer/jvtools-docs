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
| Create Control Null | `createnull` | Creates the master runtime-control null for this sensor (one per node) — Start / Stop / Reset buttons plus a Solvers list. See [Live Simulation](using.md#live-simulation). |
| Create Generic POP Network | `createpop` | Builds a ready-to-run POP network wired to the solver-ready output, and registers it on the control null. See [Live Simulation](using.md#live-simulation). |
| Use Recipe | `use_recipe` | Enables the recipe controls below. See [Recipes](using.md#recipes). |
| Recipe File | `recipefile` | A JVtools recipe `.py` file — a pre-made downstream network (sim + look). |
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

## Camera

| Parameter | Name | Description |
| --- | --- | --- |
| Create Orthographic Camera | `makecam` | Create (or retarget) a top-down orthographic camera looking down at the sensor, up = +X. One per node. See [Camera](using.md#camera). |
| Camera to Crop | `camtocrop` | Move and zoom that camera to frame the current Crop rectangle. |

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

---

> Tooltips in Houdini (hover any parameter) are the authoritative, always-current descriptions. If this page and a tooltip ever disagree, trust the tooltip.
