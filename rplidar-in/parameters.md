---
icon: sliders
order: 80
---

# Parameter Reference

Every parameter on the RPLidar In node, grouped by function. Names in `code` are the internal parameter names.

## Main

| Parameter | Name | Description |
| --- | --- | --- |
| Mode | `mode` | Off / Live / Playback. The master switch. See [Modes](using.md#modes). |
| Test Sensor | `testdevice` | Prints identity, health, and scan modes to the console. While Live, prints stream statistics instead. |
| Create POP Network | `createpop` | Builds a ready-to-run POP network wired to the live points. See [Live Simulation](using.md#live-simulation). |
| Port | `port` | Serial port of the sensor's USB adapter (e.g. `COM3`). Blank = auto-detect the CP210x. |
| Scan Mode | `scanmode` | Standard (~4k samples/s) or Express (~8k). Live only; changing it while Live restarts the stream. |
| Baud Rate | `baud` | Serial baud. 256000 is correct for the A2 family; other values are untested. |
| Units per Meter | `unitscale` | How many Houdini units represent one real meter. 1 = meters, 100 = centimeters. |

## Visualize

| Parameter | Name | Description |
| --- | --- | --- |
| Show Sensor Guide | `visualize` | Draw the origin sensor marker + range ring. On by default. |
| Guide Color | `vizcolor` | Color of the guide geometry. |
| Range (m) | `vizrange` | Radius of the range circle in real meters (A2M12 max 16 m). |
| Sensor Size (m) | `vizsensor` | Diameter of the origin sphere, in real meters. |
| Connect Points | `vizrays` | Draw a line from the sensor to each scan point (the beam fan). Off by default. |
| Ray Color | `vizraycolor` | Color of the connecting rays. |
| Bake Current Map | `mapbake` | Capture ~1.5 s of the live stream into a static map. Live only. |
| Show Static Map | `mapshow` | Overlay the baked static map. |
| Map Color | `mapcolor` | Color of the baked map marks. |

See [Visualization](using.md#visualization).

## Crop

| Parameter | Name | Description |
| --- | --- | --- |
| Enable Crop | `cropenable` | Cull scan points outside the rectangle. Shows a red guide. |
| Center | `cropcenter` | Rectangle center on the ground (X, Z), relative to the sensor. |
| Size | `cropsize` | Rectangle extent along X and Z. Default 32 × 32. |
| Rotation | `croprot` | Rotation of the rectangle about the sensor's vertical axis. |

See [Crop](using.md#crop).

## Recording

| Parameter | Name | Description |
| --- | --- | --- |
| Recording Directory | `recdir` | Where recordings are saved and listed from. Default `$HIP/rplidar-recordings`. |
| Recording File | `recording` | File used for Playback. Blank = newest in the directory. |
| Loop Playback | `loop` | Loop the recording; off holds the last scan. |
| Start Recording | `recstart` | Begin writing the live stream to a new file. Live only. |
| Stop Recording | `recstop` | Finish and select the new recording. |
| Delete Recording | `recdelete` | Delete the picked file (with confirmation). |

See [Recording & Playback](using.md#recording-and-playback).

---

> Tooltips in Houdini (hover any parameter) are the authoritative, always-current descriptions. If this page and a tooltip ever disagree, trust the tooltip.
