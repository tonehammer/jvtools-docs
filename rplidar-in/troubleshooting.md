---
icon: bug
order: 10
---

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

You fed the solver from **Output 0** (Points & Guides). Switch to **Output 1** (Points), which strips the `rplidar_viz` guide geometry. Alternatively turn off the Visualize guides or delete the `rplidar_viz` group downstream. See [Output & Attributes](output.md).

## Playback shows nothing

* Confirm **Mode = Playback** and a valid file is picked in **Recording File** (or leave it blank for the newest).
* Confirm the **Recording Directory** points at where your `.jsonl` files actually live.
* Make sure the timeline is playing or you've scrubbed — Playback is driven by the playbar clock.

## The asset won't load

RPLidar In ships as `.hdalc`, which loads only in **Houdini Indie and Apprentice**, not commercial (FX/Core) licenses.

## Changing Scan Mode or Baud pauses the stream

Expected. Changing either restarts the sensor stream, which takes about two seconds.
