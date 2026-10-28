---
icon: rocket
order: 100
---

# Getting started

## Installing

>>> 1. Drop the file in your otls folder
Put `JV-MAPout-v1.0.hdalc` in `Documents/houdini22.0/otls/`. Houdini picks it up on the next launch. The one file holds both nodes.
>>>

>>> 2. Delete the previous version's file
If you're updating, **delete the old `.hdalc` first**. Two files defining the same asset collide.
>>>

>>> 3. Find the node
**Tab ▸ JV ▸ MAPout Setup**, at SOP level. MAPout Output is not in the Tab menu: the Setup makes it for you.
>>>

!!!warning Indie asset format
`.hdalc` is Houdini's Indie/Apprentice asset format. Houdini FX and Core can load it, but doing so switches that session to limited-commercial (Indie) mode. That's a SideFX licensing rule, not a choice this tool makes.
!!!

!!!tip Before you start: the projector itself
Turn off the projector's own keystone correction and digital zoom: they resample the image before MAPout sees the wall, and two corrections fight. Optical lens shift, if your projector has it, is free, so use it first. Run the projector at its native resolution with Windows display scaling at 100%, so one pixel in MAPout is one pixel on the wall.
!!!

## Your first mapping

>>> 1. Drop a MAPout Setup
Anywhere in a geometry network. Set **Canvas Resolution** to the size you want the COP image to be. **Presets** lists the screens connected right now, so the projector's own resolution is one click away.
>>>

>>> 2. Press Build COP Network and Output
A black COP Network and a MAPout Output appear below the Setup, wired together. The COP Network follows the Canvas Resolution live.
>>>

>>> 3. Open the output on the projector
On the MAPout Output, pick the projector as **Screen** and press **Open Output**. The window covers that screen and stays on top. **Ctrl+W** on the projector closes it.
>>>

>>> 4. Pin the corners
Back on the Setup, turn on **Edit Mapping** (or press **E** with the pointer on the projector). A calibration grid and four corner handles appear on the wall. Drag the corners until the grid's cells are equal. Equal cells mean the keystone is gone.
>>>

>>> 5. Draw your shapes on the wall
Press **R** for a rectangle, **O** for an ellipse or **P** for a polygon, and draw on the projection. Points snap to other shapes' points, so faces that meet share their corners.
>>>

>>> 6. Press Sync Shapes to COPs
Every shape gets a row in the COP Network: a pink `ART_<name>` null where its artwork starts and a teal `SHAPE_<name>` null where it ends. Build each face's look between the two.
>>>

Turn **Edit Mapping** off and the wall shows the COP network, pinned and masked to your shapes.

!!!tip Check the UVs before building artwork
Turn on **Show UV Check** (Shapes tab) and every face shows a numbered, coloured grid. It shows at a glance which way up each face is and whether it stretches.
!!!

## Saving the mapping

The mapping is stored on the Setup, so it is saved with the scene. To reuse a projector setup in another scene, use **Mapping File** on the Mapping tab: **Save Mapping** writes the corners, mesh, rotation, multi-projector region and grid to a JSON file, and **Load Mapping** reads it back. Turn on **Shapes** under Include to carry the shapes too.

## The controls on the projector

The help bar at the bottom of the projector lists the current tool's mouse and keys, and the Setup's **Utilities** tab lists all of them. The ones you need first:

| Input | What it does |
|---|---|
| **E** | Edit Mapping on or off |
| **W V R O P** | Warp, Select, Rectangle, Ellipse, Polygon |
| **LMB drag** (Warp) | move a corner, or the selected mesh points |
| **1–4**, **Tab**, **arrows** (Warp) | pick a corner, step to the next point, nudge 1 px |
| **Double-click** or **F2** (Select) | rename a shape; its COP row follows |
| **M** (Select) | mask the selected shapes on or off |
| **Ctrl+Z**, **Ctrl+Shift+Z** | undo, redo |
| **H** | hide the help bar |
| **Ctrl+W** | close the output |
