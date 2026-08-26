---
icon: sliders
order: 110
---

# Parameter reference

<!-- 🔴 The parm Help fields on the HDA are the SOURCE OF TRUTH for tooltips.
     This page syncs FROM them, never the reverse, and all layers sync MANUALLY
     (STANDARDS §9). Re-read this page whenever a feature lands.
     Synced 2026-08-25 from build_assets.py::build_parms — panel order below
     matches the built parm surface exactly. -->

Everything lives on one **Setup** tab, plus **Utilities**. Listed here in panel order.

!!!info Scene View disables a lot, on purpose
Most of the image controls only mean something when a COP is being read, so in **Scene View** mode they grey out. That's the panel telling you the truth, not a control going inert — switch **Source** back to Copernicus and they return.
!!!

## The action row

| Parameter | Default | What it does |
|---|---|---|
| **Output COP** | — | Opens the borderless output window for the COP network wired into the input. |
| **Close Output** | — | Closes this node's window. Does nothing if it isn't open. |
| **Status** | *(read-only)* | Source resolution and channel count, then the measured time to read one frame and the frame rate that implies. |
| **Blackout** | Off | Blacks the output instantly without closing the window. Off is just as instant, and the image comes back current. |

**Status is the one to read** when the frame rate disappoints. That ceiling is the COP network's own cook cost, not this node's — if it's lower than you want, the answer is COP resolution.

In Scene View and Both modes, **Blackout** hides the viewport window instead, which also stops it cooking.

## Source

| Parameter | Default | What it does |
|---|---|---|
| **Source** | Copernicus | *Copernicus (the COP image)* — read through our own sRGB shader, and the one to trust for grading. *Scene View (3D only)* — a borderless viewport framed on the COP canvas, reading no COP at all. *Both (3D over the COP)* — a reference view; its gamma is approximate, not exact sRGB. |
| **Output Index** | 0 | Which output of the display node to show. Most COP chains end in a single-output node, so this is almost always 0. |
| **Max FPS** | 60 | Upper limit on how often the COP is re-read. **0 means no limit** — not "off", and not 1. |
| **Test Pattern** *(toggle)* | Off | Replaces the image with a built-in alignment pattern: grid, centre crosshair, aspect circle, colour bars, gamma ramp. Works with nothing wired. |
| **Test Pattern** *(resolution)* | Match COP | The pattern's resolution, which sets its aspect. *Match COP* uses the wired network's own resolution (1920×1080 when nothing is wired); the presets — 1920×1080, 3840×2160, 1600×1200, 1080×1080, 1080×1920 — are for aiming at the aspect the content *will* have. |

The pattern goes through the same path as real content, so Fit, Zoom, Offset and the flips all apply to it. That's what makes it useful for aiming a projector rather than just proving the window opens.

## Window

| Parameter | Default | What it does |
|---|---|---|
| **Screen** | *(primary)* | Which display the window opens on. The list is the screens Qt can see right now, so a projector appears once Windows has it. It's also an indicator — middle-drag the window elsewhere and this updates to name where it landed. |
| **Fullscreen** | Off | Fills the screen. Off gives a window at exactly the COP's resolution, centred. Double-clicking the window toggles it too. |
| **Always On Top** | **On** | Keeps the window above everything else — what you want on a projector, and what you may not want while grading. |
| **Auto-Open On Load** | Off | Opens the window automatically when the scene loads, using the saved Screen and Fullscreen settings. Does nothing if there's no COP wired and no test pattern on. |
| **Hide Cursor** | Off | Hides the pointer over the output window. It still drags and clicks normally. |

## Image

| Parameter | Default | What it does |
|---|---|---|
| **Fit** | Fit (letterbox) | *Fit (letterbox)* — the whole image, bars where the aspect differs. *Fill (crop)* — fills the screen, cropping the long axis. *1:1 pixels* — one image pixel per screen pixel. *Stretch* — distorts to fill. |
| **Smooth Scaling** | **On** | Bilinear filtering when the image is scaled. Turn it off to see the real pixels — what you want when projecting a low-resolution source deliberately. |
| **Offset** | 0, 0 | Moves the image inside the window, in screen pixels. Right-dragging the image writes straight into this. |
| **Zoom** | 1.0 | Scales the image about the centre of the window, on top of the fit mode. The wheel writes here too. |
| **Flip Horizontal** | Off | Mirrors left to right — for rear projection. |
| **Flip Vertical** | Off | Mirrors top to bottom — for a ceiling-mounted projector. |
| **Reset Position** | — | Puts offset, zoom and both flips back to their defaults. Leaves the screen choice, the fit mode and the grade alone. |

Everything in this section is saved with the scene, so a projector alignment survives a save and travels with the hip.

## Grade

| Parameter | Default | What it does |
|---|---|---|
| **Exposure** | 1.0 | Linear multiplier applied *before* the sRGB display transform. |
| **Gamma Trim** | 1.0 | Extra gamma on top of the sRGB display transform, for matching a projector that isn't sRGB. 1 is no trim. |

Both are display trims. They change nothing upstream in the COP network — do the real grading there.

## Utilities

| Parameter | Default | What it does |
|---|---|---|
| **Show Diagnostics** | Off | Draws a readout in the bottom right of the output window: frame, source, resolution, measured read time, and the frames actually reaching the screen. Costs nothing when off. |

Show Diagnostics updates every frame, which **Status** deliberately does not — that one is a parameter, so it's rounded and written only when it changes.

Underneath sit the window's input bindings, and links to the store page, these docs, the Discord and the YouTube channel.

## Version signals

Every jvtools node carries these at the bottom of its parameter list:

| Parameter | What it does |
|---|---|
| **Current Version** | The product version of the asset you have installed. |
| *(update notice)* | Appears when a newer version is available on the store. |
