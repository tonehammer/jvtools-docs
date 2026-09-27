---
icon: history
order: 70
---

# Changelog

## Version 1.0
<p style="font-size:0.75rem; font-weight:400; opacity:0.38; letter-spacing:0.02em; margin:-0.85rem 0 1.2rem;">24 September 2026</p>

The first public release.

**Generator**

* The **Hou-DisplacementX** COP node - a GPU port of the Displacement X generator, drawn by one OpenCL kernel.
* **Seed** reproduces the same map at any resolution; **New Seed** picks a random one.
* **Iterations**, **Background**, **Seamless** and **Invert**.
* **Resolution** up to 8192, with a preset menu, or matched to a layer wired into **Size Reference**.

**Shapes and sprites**

* Five shape types - Rectangles, Grid, Columns, Rows and Lines - each with its own enable and ranges.
* Four sprite packs from the original, with optional 90-degree **Rotate**.
* Sixteen blend modes, picked at random per shape from the ones ticked.
* **Randomize All** plus a Randomize button per section, neither touching Seed or Resolution.

**Outputs**

* **height**, **normal**, **basecolor** and **id** layers at once, in full 32-bit float.
* Output names match Houdini Engine for Unreal's texture types.
* **Normal Strength**, and a **Color Gradient** for basecolor.

**Heightfield node**

* The **Hou-DisplacementX Heightfield** SOP - a heightfield with nothing wired, or triplanar displacement of wired geometry.
* **Size** and **Height Scale** for the heightfield; **Tile Size**, **Tile Offset**, **Blend Sharpness**, **Displace Amount** and **Midpoint** for displacement.
* **All Layers** output adds normal, basecolor and id as volumes, or as point attributes when displacing.
* **Show Color** previews the Color Gradient in the viewport.

**Utilities**

* Links to the website, Gumroad page, documentation, Discord and YouTube.
* Update check on the first Randomize All of a session.
* Licensed under GPL-3.0; the asset ships unlocked, with the licence text inside.
