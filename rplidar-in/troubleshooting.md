# Troubleshooting

## No points appear in Live mode

* **Press Test Sensor.** It prints the sensor's identity, health, and available scan modes. No response means Houdini can't talk to the sensor.
* **Check the port.** Leave **Port** blank for auto-detect, or set it explicitly (e.g. `COM3`).
* **Check the motor lead.** The 5V cable must be plugged in — the motor won't spin on data power alone.
* **Give it a moment.** The motor takes about two seconds to spin up on the first cook.
* **Lots of gaps is normal.** On an open desk, most returns are invalid (nothing in range). Point the sensor at a wall to see a dense arc.

## The sensor won't connect at all

* **No Windows chime and nothing new in Device Manager** → cable or port problem, not a driver problem. Try a different USB port and **swap the data cable** — a faulty data cable stops the device enumerating entirely.
* **Enumerates but silent** → check the adapter's baud switch is set to **256000**.

## "Port is in use" / permission errors

A serial port can only be opened by one program. Close anything else that might hold it:

* Another Houdini session in Live mode → set its **Mode → Off**.
* A separate tester/serial app → close it.
* A crashed process → the motor may keep spinning; unplug the 5V lead or restart to release the port.

## Houdini crashed and the motor is still spinning

The motor runs independently of Houdini once started. Stop it by unplugging the **5V** lead (safe — it's just motor power), or reconnect and set **Mode → Off**.

## Guides ended up in my simulation

You fed the solver from **Output 0** (Points & Guides). Switch to **Output 1** (Points), which strips the `rplidar_viz` guide geometry. Or turn off the Visualize guides, or delete the `rplidar_viz` group downstream. See [Outputs and Attributes](using.md#outputs-and-attributes).

## Tracking locks onto furniture instead of the hand

Almost always the missing background bake. A real room clusters into 7–11 blobs per scan, and the largest is usually a chair or a wall corner — Single mode is picking the biggest thing present, which is working as designed and isn't what you wanted.

Go **Live**, clear the interaction area completely, press **Bake Background**, then turn on **Subtract Background**. If it still wanders, tighten **Blob Size min/max** (a hand is roughly 0.05–0.15 m) — that throws out room geometry before clustering ever has to choose. See [Background subtraction](using.md#background-subtraction).

## Tracking sees nothing at all after a background bake

You most likely baked while standing in the interaction area, so you were recorded as part of the static scene. Step out and bake again. Re-bake whenever the sensor moves or the room is rearranged.

If it's an object hugging a wall that disappears, lower the **Foreground Margin** — a return has to be at least that much closer than the background to count as foreground.

## Blob ids keep changing / a track keeps restarting

* **Raise Hold Time.** Brief dropouts (a hand turning edge-on) end the track and the next appearance gets a fresh id.
* **Raise Max Speed** if the motion is genuinely fast — a blob that moves further between frames than the gate allows can't be matched to its own track.
* **Raise Min Points** if the blob is breaking apart into specks at the edge of its range.

## My solver suddenly sees only a few points

Check **Solver Output** in the Tracking tab. Set to **Blobs**, Output 1 carries only the tracked blob points — a handful, by design. Set it back to **All Points** for the full scan cloud.

## Playback shows nothing

* Confirm **Mode = Playback** and a valid file is picked in **Recording File** (or leave it blank for the newest).
* Confirm the **Recording Directory** points at where your `.jsonl` files actually live.
* Make sure the timeline is playing or you've scrubbed — Playback is driven by the playbar clock.

## The asset won't load

RPLidar In ships as `.hdalc`, which loads only in **Houdini Indie and Apprentice**, not commercial (FX/Core) licenses.

## Changing Scan Mode or Baud pauses the stream

Expected. Changing either restarts the sensor stream, which takes about two seconds.
