# Getting Started

## Install the asset

1. Download `JV-Advanced_Velocity-vX.Y.hdalc` from your Gumroad library.
2. Drop it into your Houdini `otls` folder:
   * **Windows** — `C:\Users\<you>\Documents\houdini22.0\otls\`
   * **macOS** — `~/Library/Preferences/houdini/22.0/otls/`
   * **Linux** — `~/houdini22.0/otls/`
3. Restart Houdini, or use **Assets ▸ Install Digital Asset Library**.

The node then appears in the SOP tab menu under **JV ▸ Advanced Velocity**.

!!!warning Updating
When a new version arrives, **delete the previous `.hdalc` file** before adding the new one. Two files defining the same asset will collide. Because the internal node type never changes between versions, your existing scenes pick up the new version automatically.
!!!

## Your first velocity

1. Drop an **Advanced Velocity** node after any geometry.
2. Open **Basic Velocity** and tick its header checkbox.
3. Set **Value** to something like `0, 5, 0`.

That's it — the node now outputs `@v`, and the viewport shows red guide lines pointing the way the points will travel. Feed it into a POP, FLIP, Vellum, or RBD solver.

!!!info Nothing happens?
All four velocity types are **off by default**, so a freshly dropped node outputs a zero velocity. Tick the checkbox in a section header to switch that type on — the section's controls stay hidden until you do.
!!!

## The shape of the node

The interface is four sections:

**Setup** holds the four velocity types. Each one is a collapsible section with a checkbox in its header; its controls appear once it's switched on.

**Velocity Mixer** decides how the enabled types combine, and what leaves the node.

**Visualization** controls the on-screen guides.

**About** shows the version you have installed.

## A quick explosion

1. Fracture something — a Voronoi Fracture into an Assemble with **Create Packed Geometry** on is the usual setup.
2. Drop **Advanced Velocity** after it and switch on **Exploding Velocity**.
3. Leave **Origin** on *Whole Object* and set **Strength**.

Every piece now flies away from the object's centre. To blast from a specific spot instead, read [Point Source](using.md#point-source-explosions).
