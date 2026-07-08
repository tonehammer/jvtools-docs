---
icon: :arrows_counterclockwise:
order: 80
---

# Modes

The **Mode** parameter is the master switch for the node. It has three settings.

## Off

Motor stopped, empty output. Use this whenever you aren't actively reading the sensor — it releases the serial port so other programs (or other Houdini sessions) can use it, and it stops the motor spinning.

> Any visualization guides you've enabled still draw in Off mode, so you can lay out your scene against the range ring without the sensor running.

## Live

Streams the sensor in real time. On the first cook the motor spins up over about two seconds, then every cook outputs the most recent full rotation as points.

* Choose the density with **Scan Mode** (see below).
* The stream runs on a background thread, so no rotations are dropped between cooks — including while recording.
* **Test Sensor** prints live stream statistics while streaming (samples/second, valid points per rotation).

### Scan Mode

Live only. Controls how fast the sensor samples:

| Setting | Rate | Points per rotation (typical) |
| --- | --- | --- |
| **Standard** | ~4,000 samples/s | ~110 valid |
| **Express** | ~8,000 samples/s | ~230 valid |

Express roughly doubles the point density. Changing Scan Mode while Live restarts the stream (about two seconds).

## Playback

Plays a recorded `.jsonl` file against the playbar clock, so the scan is time-dependent and scrubs and renders like any other animated geometry. This lets you develop and iterate with the sensor disconnected. See [Recording & Playback](recording.md).

## A note on invalid returns

The sensor reports a sample for every laser pulse, but many pulses hit nothing in range (empty space, or a surface that doesn't reflect). Those come back as **invalid** and are filtered out — on a desk, more than half of every rotation can be invalid. This is normal, not a fault. The point counts above are *valid* points only.
