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

## The two modes

The **Mode** menu at the top is the first thing to understand:

* **Timed Events** (the default) — the output is a sequence of baked velocity *events*, each captured from the setup at a frame and faded in and out by its own envelope. The setup you edit is a template; nothing reaches the output until you press **Create Event**. This is the headline feature — see [Timed Events](timed-events.md).
* **Single Field** — the setup is evaluated live and written straight to the output. What you tweak is what you get, every frame, like an ordinary SOP.

If you just want one velocity field with no time axis, switch to **Single Field** and everything below responds immediately.

## Your first velocity

1. Drop an **Advanced Velocity** node after any geometry.
2. Set **Mode** to *Single Field*.
3. Open **Basic Velocity** in the Setup tab and tick its header checkbox.
4. Set **Value** to something like `0, 5, 0`.

That's it — the node now outputs `@v`, and the viewport shows red guide trails pointing the way the points will travel. Feed it into a POP, FLIP, Vellum, or RBD solver.

!!!info Velocity you already had is safe
A fresh node **passes the incoming velocity through** — the **Incoming Velocity** stream in the mixer is on by default, so dropping this node after a cache or a previous sim layers on top of that motion instead of erasing it. Switch that toggle off when you want to author the attribute outright.
!!!

## The shape of the node

Along the top: **Mode**, the **Group** the final write is restricted to, and (in Timed Events) the **Dynamic Events** section holding the event list.

Below that, two tab strips:

**Setup | Velocity Mixer** — the six velocity types, each a collapsible section with a checkbox in its header, and the mixer that decides how the enabled types combine.

**Output | Visualization | Utilities** — what leaves the node and under which name, the viewport guides and event timeline, and the utility toggles plus links to these docs, Discord and YouTube.

The version you have installed is shown at the very bottom of the parameter list.

## A quick explosion

1. Fracture something — a Voronoi Fracture into an Assemble with **Create Packed Geometry** on is the usual setup.
2. Drop **Advanced Velocity** after it, set **Mode** to *Single Field*, and switch on **Exploding Velocity**.
3. Leave **Origin** on *Whole Object*.

Every piece now flies away from the object's centre. To blast from a specific spot instead, switch **Origin** to *Point Source* and read [Point Source](using.md#point-source-explosions). And when one explosion isn't enough — a lift, then a blast, then a spin — that's what [Timed Events](timed-events.md) is for.
