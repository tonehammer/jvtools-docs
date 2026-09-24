# Troubleshooting

**No points appear in Live mode** — work down this list:

* **Press Test Sensor.** It prints the sensor's identity, health, and available scan modes. No response means Houdini can't talk to the sensor.
* **Check the port.** Leave **Port** blank for auto-detect, or set it explicitly (e.g. `COM3`).
* **Check the motor lead.** The 5V cable must be plugged in — the motor won't spin on data power alone.
* **Give it a moment.** The motor takes about two seconds to spin up on the first cook.
* **Lots of gaps is normal.** On an open desk, most returns are invalid (nothing in range). Point the sensor at a wall to see a dense arc.

**The sensor won't connect at all** — no Windows chime and nothing new in Device Manager means a cable or port problem, not a driver problem: try a different USB port and **swap the data cable** — a faulty data cable stops the device enumerating entirely. If it enumerates but stays silent, check the adapter's baud switch is set to **256000**.

**"Port is in use" / permission errors** — a serial port can only be opened by one program. Close anything else that might hold it:

* Another Houdini session in Live mode → set its **Mode → Off**.
* A separate tester/serial app → close it.
* A crashed process → the motor may keep spinning; unplug the 5V lead or restart to release the port.

**Guides ended up in my simulation** — you fed the solver from **Output 0** (Points & Guides). Switch to **Output 1** (Points), which strips the `rplidar_viz` guide geometry. Or turn off the Visualize guides, or delete the `rplidar_viz` group downstream. See [Outputs and Attributes](../using.md#outputs-and-attributes).

**Tracking locks onto furniture instead of the hand** — almost always the missing background bake. A real room clusters into 7–11 blobs per scan, and the largest is usually a chair or a wall corner — Single mode is picking the biggest thing present. Go **Live**, clear the interaction area completely, press **Bake Background**, then turn on **Subtract Background**. If it still wanders, tighten **Blob Size min/max** (a hand is roughly 0.05–0.15 m). See [Background subtraction](../using.md#background-subtraction).

**Tracking sees nothing at all after a background bake** — you most likely baked while standing in the interaction area, so you were recorded as part of the static scene. Step out and bake again. Re-bake whenever the sensor moves or the room is rearranged. If it's an object hugging a wall that disappears, lower the **Foreground Margin** — a return has to be at least that much closer than the background to count as foreground.

**Blob ids keep changing / a track keeps restarting** — raise **Hold Time** so brief dropouts (a hand turning edge-on) don't end the track. Raise **Max Speed** if the motion is genuinely fast, and **Min Points** if the blob is breaking apart into specks at the edge of its range.

**Playback shows nothing** — confirm **Mode = Playback** and a valid file in **Recording File** (or leave it blank for the newest), and that **Recording Directory** points at where your `.jsonl` files live. Playback is driven by the playbar clock, so the timeline has to be playing or scrubbed.

---

Still stuck? Find me on the JVtools Discord — the invite link is in the **Utilities** folder on the HDA node.
