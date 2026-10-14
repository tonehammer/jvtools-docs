---
icon: package
order: 100
---

# Building the Rig

The rig is built by the same **Build Character** button that builds the character, in the **Character ▸ Build** tab. There is no separate rigging step: one press imports the character, builds its materials, and builds its rig.

## What gets built

With **Build APEX Rig** on (the default), **Build Character** builds a body and facial rig as its own node, the **Reallusion Rigger APEX Rig**, directly below the Rigger:

<div style="margin:0 0 1rem;"><img src="../../static/rig-node-tile.png" alt="The Reallusion Rigger APEX Rig node" style="height:90px; width:auto;"></div>

* **The body:** IK/FK arms and legs, reverse feet, a spline spine, FK for every finger and toe, and a **gear** control per body part holding that part's settings.
* **The face:** a keyable channel for every Character Creator facial morph, sliders on the face, a flat face board, and the Face gear beside the head.
* **The animation:** the character's own exported clip, baked through the rig once as the bottom animation layer, **BaseAnimation**.
* **The catalog:** Character Creator's expressions and hand poses, loaded into Houdini's Animation Catalog.

The rig node *is* the animatable character. Its output is the deformed, textured mesh, the Rigger hands its Solaris import over to it, and Karma reads it — so what you animate is what renders.

On our test characters the whole press takes roughly **40 to 90 seconds** (a standard character from USD at the fast end, an HD character from FBX at the slow end). Progress shows in the bar at the bottom of the Houdini window, and the console prints how long each stage took when it finishes.

## The build options

The options sit in **Character ▸ Build**, below **Build Character**. They are read when the rig is built, so set them before you press it.

| Option | Default | What it does |
|---|---|---|
| **Build APEX Rig** | On | Off builds the character without a rig: it is shaded and plays the animation it was exported with. |
| **Build Facial Rig** | On | Off builds a body-only rig: faster to build and much lighter to animate. The face stays neutral and the clip's expressions do not play, but the jaw and eyes still follow the clip. |
| **Load Expression Presets** | On | Puts about 300 expression poses in the Animation Catalog during the build. Adds roughly 5 to 20 seconds. |
| **Load Hand Poses** | On | Puts 71 hand poses in the catalog. Adds roughly 5 seconds, and needs no facial rig. |
| **Stash Rig** | On | Stores the built, baked rig in the rig node, so a reopened scene loads in seconds instead of rebuilding. See [Rig Settings](rig-settings.md). |
| **Set Frame Range to Animation** | On | Sets the scene's frame range to the character's animation before the rig is built. |

A few of these deserve a word of explanation.

**Build Facial Rig** is the one to turn off for body work: a dancer, a fighter, a crowd character seen from a distance. The rig builds faster and plays back faster, and **Auto Breathe** still works. **Face Tools** and **Auto Blink** are greyed out on a body-only rig, and there's no way to add the face afterwards except building again with the option on.

**Load Expression Presets** and **Load Hand Poses** only fill the catalog. If you turn them off to save build time, **Reload Catalog Poses** on the rig node loads them whenever you want them. The catalog isn't saved with the scene in any case, so after reopening a scene you press that button anyway.

**Set Frame Range to Animation** matters because Houdini's APEX nodes read the scene's frame range. Careful with this one: with **Stash Rig** off, changing the frame range later rebuilds and rebakes the whole rig, which takes about as long as the first build on a heavy character. With **Stash Rig** on, it doesn't. The option is skipped when the rig already exists or the character was exported without animation.

## A character exported without animation

If you exported **Mesh only**, or Character Creator's two-frame export pose, the rig is built at the character's rest pose: **BaseAnimation** holds one key per control, so a pose you key holds instead of popping back, and the scene's frame range is left as it is. The console line at the end of the build says so.

## Building again

**Build Character** builds the rig only when the character has none. Pressing it again refreshes the materials and leaves the rig, and every key on it, alone. That makes it safe to press while you work on the look.

To rebuild the rig — because you changed the character, the import mode or a build option — delete the rig node and press **Build Character**. Deleting the node also hands the character back to the Rigger, which plays its embedded animation again until the new rig exists.

!!!warning The rig freezes the character
The rig is built from the character as it was when you pressed the button. Changing the import settings or the character file while a rig exists does nothing to it. And your keys live inside the rig node, so deleting the node deletes the animation you keyed on it. Settle the character and the build options before you start animating.
!!!

## The rest of the Build tab

The **Render** folder (**Build In**, **Create Render Setup**, **Go to LOPs**) is covered in [Rendering](../lookdev/rendering.md), **Skin-Fix** in [Skin Fix](skin-fix.md), and **Fix Broken Blendshape** — for a small element, usually facial hair, that breaks up once the face animates — in [Troubleshooting](../reference/troubleshooting.md#look-and-materials).
