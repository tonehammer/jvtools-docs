# Changelog

## Version 1.0

The first public release.

**Streaming**

* Live streaming of Slamtec RPLIDAR sensor data into Houdini as SOP geometry — one point per laser return, updated every cook
* Standard (~4k samples/s) and Express (~8k samples/s) scan modes
* Background reader thread so no rotations are dropped between cooks, including while recording
* Self-contained single asset file — talks the RPLIDAR serial protocol directly, with no Python packages to install
* Auto-detection of the CP210x USB/UART adapter (with a manual **Port** override), and a **Units per Meter** control for working in meters, centimeters, or any scale

**Recording & playback**

* Record the live stream to disk as `.jsonl` and replay it against the playbar clock — develop and iterate with the sensor disconnected
* Recording folder management: directory, file picker (blank = newest), loop, and delete

**Visualization**

* Sensor marker and range-ring guides, with adjustable color, range, and sensor size
* Connect Points (beam fan) — draw a ray from the sensor to each scan point
* Static map bake — capture a short slice of the live stream into a fixed reference map
* Attribute color — tint the scan points by angle or distance through a color ramp, for a viewport-only view or baked into `Cd` for downstream use

**Crop & camera**

* Cull scan points outside a rotatable ground rectangle, so only the region you care about reaches your solver
* Interactive viewport handle — resize, move, and rotate the crop box directly in the Scene View
* One-click top-down orthographic camera, plus a Camera-to-Crop button that frames it to your crop region

**Live simulation**

* One-click **Create Generic POP Network** button that builds a ready-to-run POP network wired to the solver-ready output, plus a control null to start, stop, and reset the live sim
* Recipes — load pre-built downstream networks (sim + look) from a single file
* Two outputs — Points & Guides (display) and Points (solver-ready, guides stripped)

**Test Sensor**

* Prints the sensor's identity, health, and available scan modes to the console — and live stream statistics while streaming

---

!!!info
Future updates and their changes will be listed here. RPLidar In is a free tool, and updates are included at no cost — check back after updating the asset to see what's new.
!!!
