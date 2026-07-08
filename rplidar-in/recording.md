---
icon: :red_circle:
order: 70
---

# Recording & Playback

Recording captures the live stream to disk so you can replay it later — develop offline, iterate on a solver against a repeatable take, or archive an installation.

Each recording is a `.jsonl` file: one JSON line per rotation, holding the timestamp and the rotation's samples.

## The Recording folder

| Parameter | What it does |
| --- | --- |
| **Recording Directory** | Where recordings are saved and listed from. Defaults to `$HIP/rplidar-recordings`. |
| **Recording File** | The file used for Playback. The dropdown lists the directory. Leave it **blank to use the newest file** in the directory. |
| **Loop Playback** | Loop the recording. When off, the last scan is held after the file ends. |
| **Start Recording** | Begin writing the live stream to a new timestamped file. *Live mode only.* |
| **Stop Recording** | Finish the recording and auto-select it in **Recording File**. |
| **Delete Recording** | Delete the file currently picked in **Recording File** (asks for confirmation). |

## Recording a take

1. Set **Mode → Live** and confirm points are streaming.
2. Press **Start Recording**. A new timestamped `.jsonl` file is created in the Recording Directory.
3. Perform your take (walk through the scene, move objects, etc.).
4. Press **Stop Recording**. The finished file is selected in **Recording File** automatically.

Recording happens on the sensor's background reader thread, so no rotations are missed between Houdini cooks.

## Playing it back

1. Set **Mode → Playback**.
2. Pick a file in **Recording File** (or leave blank for the newest).
3. Scrub the timeline or press Play — the scan is driven by the playbar clock.

Use **Loop Playback** to cycle a short take continuously while you tune a downstream network.
