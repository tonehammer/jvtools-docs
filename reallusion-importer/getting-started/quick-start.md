---
icon: zap
order: 90
---

# Quick Start

This page gets you from a fresh Houdini scene to a shaded, rendered character in about five steps. We'll keep it simple here — every control is explained in depth later in the [Using the Asset](../using/lookdev-controller.md) section.

!!!success Before you begin
Make sure your character is exported from Character Creator correctly. The export settings genuinely matter — see [Preparing Your Character](preparing-your-character.md) first if you haven't already.
!!!

## Step 1 — Create the node

Inside a Geometry object, press **Tab**, type **Reallusion**, and place a **Reallusion Importer** node.

![](../static/reallusion_importer_fresh_node.png)

## Step 2 — Point it at your FBX

On the node's parameters, find the **CC5/iClone FBX** field and set it to your exported `.fbx` file.

![](../static/elysse-FBX-filepath.png)

!!!info
The tool expects your textures to sit in a `textures` folder next to the FBX (this is how Character Creator exports them by default). Keep the FBX and its texture folder together.
!!!

## Step 3 — Build the character

Click the **Build Character** button.

The tool will now import the character, build all of its materials, set up displacement and wrinkles where the character supports them, and create a look controller. On a heavy or HD character this can take anywhere from a few seconds to a couple of minutes — the progress bar at the bottom of the Houdini window shows what it's doing.

![](../static/elysse-buildchar-button.png)

!!!warning
The first build of a character is the slow part, because Houdini has to load and expand the FBX. Subsequent look changes are fast. See [Performance & Caching](../reference/performance.md) for details.
!!!

## Step 4 — Look at your character

Your character is now built in Solaris (Houdini's `/stage` context). Click the **Go to LOPs** button on the node to jump there, then set up a viewport with a Karma render to see it.

If you'd like an instant lighting and camera setup, see [Rendering](../using/rendering.md) — the tool can build a three-point light rig, a camera, and Karma render settings for you.

![](../static/elysse-render-setup.png)

## Step 5 — Art-direct the look

Find the bright **red controller node** in the LOP network (or click **Go to LOPs** to get there). This node holds every look control: skin, wrinkles, eyes, hair, and more. Adjust a slider or color and the Karma render updates live.

![](../static/elysse_lookdev_controller.png)

That's the whole workflow. From here, explore the [Lookdev Controller](../using/lookdev-controller.md) to learn what every control does — or just start dragging sliders and watching what happens.

## What next?

* **Want to recolor the hair?** See [Hair](../using/hair.md).
* **Want glowing eyes?** See [Eyes](../using/eyes.md).
* **Adding animation?** See [Animation](../using/animation.md).
* **Something not working?** See [Troubleshooting & FAQ](../reference/troubleshooting.md).
