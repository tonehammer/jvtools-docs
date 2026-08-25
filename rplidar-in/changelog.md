---
icon: history
order: 60
---

# Changelog

## Version 1.0

The first public release.

**Streaming**

* Live streaming of Slamtec RPLIDAR data into Houdini as SOP geometry.
* Standard and Express scan modes.
* Background reader thread, so no rotations are dropped between cooks.
* Self-contained single asset file, with no Python packages to install.
* Auto-detection of the CP210x USB adapter, with a manual Port override.
* Units per Meter control.

**Recording & playback**

* Record the live stream to disk and replay it against the playbar.
* Recording folder management — directory, file picker, loop and delete.

**Visualization**

* Sensor marker and range-ring guides.
* Connect Points — draw a ray from the sensor to each scan point.
* Static map bake.
* Attribute colour — tint the scan points by angle or distance through a ramp.

**Blob tracking**

* Cluster the scan into blobs and track them across frames, each with a stable id and a velocity.
* Single and Multi tracking modes.
* Background subtraction.
* Clustering, smoothing and association controls.
* Solver Output switch — the full scan cloud or just the tracked blob points.
* On-screen blob markers with velocity lines.

**Placement, crop & camera**

* Pre-Rotate, applied before everything else.
* Cull scan points outside a rotatable ground rectangle.
* Interactive viewport handle for the crop box.
* One-click top-down orthographic camera, plus Camera to Crop.

**Live simulation**

* Create Generic POP Network — one button builds a POP network wired to the solver-ready output.
* Recipes — a loader for whole downstream networks packed as a single file.
* Two outputs — Points & Guides, and Points.

**Test Sensor**

* Prints the sensor's identity, health and scan modes to the console, plus live stream statistics.

---

!!!info
Future updates and their changes will be listed here. RPLidar In is a free tool, and updates are included at no cost — check back after updating the asset to see what's new.
!!!
