# Building the Rig

The rig is built by the same **Build Character** button that builds the character, in the **Character ▸ Build** tab.

## What gets built

With **Build APEX Rig** on (the default), **Build Character** also builds a body and facial rig as its own node, directly below the Rigger. It has IK/FK limbs, reverse feet, a spline spine, per-finger and per-toe FK, and a keyable channel for every Character Creator facial morph. The rig node *is* the animatable character: its output is the deformed, textured mesh, and Karma reads it. The character's own animation is baked through the rig once, as the **BaseAnimation** layer.

## The build options

* **Build APEX Rig.** Off gives you the Importer on its own: the character plays its exported animation.
* **Build Facial Rig.** Off builds a body-only rig, which builds faster and is much lighter to animate, but the face stays neutral and the clip's expressions do not play. The jaw and eyes still follow the clip. Use it for dancers and fighters.
* **Load Expression Presets** and **Load Hand Poses.** They put about 300 expression poses and 71 hand poses in the Animation Catalog during the build, adding roughly 5 to 20 seconds and 5 seconds. Hand poses need no facial rig. **Reload Catalog Poses** on the rig node loads them later if you turn them off.
* **Stash Rig.** Stores the built, baked rig in the rig node so a reopened scene loads in seconds. It costs hip size, about 220 MB for a standard character. See [Rig Settings](rig-settings.md).
* **Set Frame Range to Animation.** Sets the scene's frame range to the character's animation before the rig is built. Careful with this one: with **Stash Rig** off, changing the range later rebuilds and rebakes the whole rig, about a minute on a heavy character. It's skipped when the rig already exists or the character has no animation.

## Building again

**Build Character** builds the rig only when the character has none. Pressing it again refreshes the materials and leaves the rig, and the animation keyed on it, alone. To rebuild, delete the rig node and press **Build Character**. Deleting the node also hands the character back to the importer, which plays its embedded animation again.

!!!warning The rig freezes the character
Don't change the import settings or the character file while a rig exists. Delete the rig node first.
!!!

The **Render** folder, **Skin-Fix** and **Fix Broken Blendshape** work as they do on the Importer: see its [Rendering](/reallusion-importer/using/rendering.md) and [Skin Fix](/reallusion-importer/using/skin-fix.md) pages.
