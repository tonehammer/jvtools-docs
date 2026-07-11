---
icon: book
order: 110
---

# RPLidar In

Welcome! **RPLidar In** brings live [Slamtec RPLIDAR](https://www.slamtec.com/) point-cloud data straight into Houdini as SOP geometry. Plug in the sensor, drop the node, and every rotation of the spinning laser becomes a fresh ring of points you can feed into simulations, visualizations, or interactive installations — in real time.

It is built for **TouchDesigner-style interactive work**: a person walks past the sensor, and their outline drives a POP or Vellum solver live, with no baking step in between.

## What it does for you

* **Live streaming** — reads the sensor over USB and outputs one point per laser return, updated every cook.
* **Recording & playback** — capture the stream to disk and replay it against the timeline, so you can develop offline without the hardware connected.
* **Built-in visualization** — optional on-screen guides (sensor marker, range ring, beam fan, baked static map) so you can see what the sensor sees.
* **Crop** — cull everything outside a rotatable ground rectangle, so only the points you care about reach your solver.
* **One-click live simulation** — a button builds a ready-to-run POP network wired to the live points.
* **Self-contained** — a single asset file with no Python packages to install. Talks the RPLIDAR serial protocol directly.

## Who it's for

RPLidar In is for artists and technical directors building **live, interactive, sensor-driven work** in Houdini — installations, performances, and experiments where real movement in a room drives a simulation on screen. If you own an RPLIDAR and want its scan inside Houdini without writing serial code, this is for you.

## Requirements

* **Houdini 21.0** (Indie or Apprentice — the asset ships as `.hdalc`).
* A **Slamtec RPLIDAR** sensor. Developed and verified against the **A2M12**; other A2-family models should work.
* The sensor's **USB/UART adapter** (CP210x) — enumerates as a serial COM port.
* **Windows** — the tested platform.

## How to use this documentation

If you're brand new, read these two pages in order:

1. [Getting Started](getting-started.md) — install the asset, connect the hardware, and see your first scan.
2. [Using RPLidar In](using.md) — modes, outputs, visualization, crop, recording, and live simulation.

After that, the [Parameter Reference](parameters.md) covers every control, and [Troubleshooting](troubleshooting.md) collects the fixes for common problems.

## Quick tour

The node has three [modes](using.md#modes) — **Off**, **Live**, and **Playback** — and two [outputs](using.md#outputs-and-attributes):

* **Output 0 — Points & Guides** (the default display): scan points plus any visualization guides.
* **Output 1 — Points** (solver-ready): scan points only, with all guides stripped.

!!!info
RPLidar In is a free tool. It is not affiliated with, endorsed by, or sponsored by Slamtec. "RPLIDAR" and "Slamtec" are trademarks of their respective owners.
!!!
