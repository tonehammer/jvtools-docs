---
order: 80
---

# Using COPout

## Choosing a source

**Source** decides what the window shows, and the three options are genuinely different animals rather than three views of one thing.

**Copernicus** is the COP image itself, read through COPout's own sRGB shader. This is the one to trust for grading — it's the only mode where what you see is the exact display transform.

**Scene View** puts a clean, borderless 3D viewport up instead: no grid, no gnomons, no chrome. Worth knowing: in this mode **no COP is read at all**, so it genuinely stops the network cooking. That makes it a real way to park a heavy sim.

**Both** draws the 3D geometry over the COP, with the viewport doing the compositing.

Careful with Both: the COP underneath is drawn by the viewport, which applies an approximate gamma rather than the exact sRGB curve. It's a reference view, not a grading view.

!!!warning The one that confuses everybody, including the author
While a **copnet holds the display flag**, the 3D viewport draws its image as a card — so all three modes can look identical and it seems like the Source menu does nothing. It isn't broken. Move the display flag to a geometry SOP and Scene View starts showing your actual scene.
!!!

## Placing the window

**Screen** picks the display. It's also an indicator, which is more useful than it sounds: middle-drag the window onto another monitor and the parameter updates to name where it ended up.

**Fullscreen** covers that screen; off gives you a window at exactly the COP's resolution, centred. Double-clicking the output window does the same thing, and Esc leaves.

**Always On Top** is on by default — that's what you want on a projector while you keep working on the first monitor. Turn it off while grading, when you'd rather it behaved like a normal window.

**Hide Cursor** blanks the pointer over the output. Nothing should be sitting on a projected image.

**Auto-Open On Load** reopens the window when the scene is opened, using the saved Screen and Fullscreen settings. Off by default, and the one to turn on for an installation that has to come back up by itself — double-click the hip and the projector lights up, no clicks.

## Fitting and aligning

**Fit** is the coarse decision — letterbox, crop, 1:1 pixels or stretch — and then **Offset** and **Zoom** place the image on top of that. **Flip Horizontal** and **Flip Vertical** are for rear projection and ceiling mounts. **Reset Position** puts offset, zoom and both flips back, leaving your screen and fit choices alone.

You rarely need to type any of it. Right-drag inside the window writes straight into Offset, the wheel writes into Zoom, the arrow keys nudge a pixel at a time.

**And all of it persists with the scene.** That's the part worth internalising: a projector alignment done by hand at the venue is saved in the hip and travels with it. You align once.

**Smooth Scaling** is on by default. Turn it off when you're projecting a low-resolution source deliberately and want to see the real pixels.

## Blackout

**Blackout** kills the output to black without closing the window or tearing anything down. Recovery is instant and the image is current the moment it comes back, because the frames underneath never stopped arriving.

This is the one to keep a hand on for live work. In Scene View and Both modes it hides the viewport window instead, which also stops it cooking.

## Grading

**Exposure** multiplies before the sRGB display transform; **Gamma Trim** adds a little on top of it. Both are display trims — they change nothing upstream in your network.

They're for matching a projector that runs dark or isn't quite sRGB, not for grading. Do the real work in the COP network, where it's part of the image rather than a property of one output window.

And grade in **Copernicus** mode. It's the only source whose transform is exact.

## Frame rate, honestly

**Max FPS** caps how often the COP is re-read. **0 means no limit** — it does not mean "off" and it does not mean 1.

The network is usually the real ceiling, not this node. Before raising the cap, read **Status**: it reports the measured time to read one frame and the frame rate that implies. If that number is lower than you want, the answer is COP resolution, not this parameter.

**Show Diagnostics** (in Utilities) draws a live readout on the output window itself — frame, source, resolution, read time, the frames actually reaching the screen, zoom and offset. It costs nothing when it's off, and unlike Status it updates every frame.

## Following the playbar

The output window mirrors the playbar and never advances time by itself. Scrub, play, or sit still, and the window follows. A COP feedback simulation therefore steps exactly when your scene steps — there is no second clock anywhere in this tool to get out of sync with.
