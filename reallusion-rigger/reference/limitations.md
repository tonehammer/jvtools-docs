---
icon: alert
order: 100
---

# Limitations & Expectations

Read this before you buy, and again if something surprises you.

## Platform

The Rigger needs **Houdini 22.0 or newer**, because it is built on Houdini 22's APEX autorig builder. It was tested on Windows. The materials are tuned for Karma XPU.

## Memory

With USD import, 16 GB of RAM is the minimum and 32 GB is recommended. With FBX import it is 48 GB minimum and 64 GB recommended. FBX stays heavy for the reason it does in the Importer: Houdini expands every facial blendshape on import. See [USD vs FBX](../getting-started/import-modes.md).

Stash Rig adds to the size of your scene: about 220 MB for a standard character, more for an HD one, plus each baked clip. An external file keeps the hip small. See [Rig Settings](../using/rig-settings.md).

## What only FBX has

Wrinkles, hair ombre and ID recolour, and flow-map anisotropy. Character Creator's USD export carries no data for them. The rig works in both modes.

## The eyes, hair and textures

These are the Importer's limits, and they apply unchanged: the eye shader is mostly not in Character Creator's export ([The eyes](/reallusion-importer/reference/limitations.md#the-eyes)), several features depend on what your character carries, and multi-tile UDIM textures are not supported. Characters should use a single UV tile per material.

## Animation

* **Clips from another character are approximations.** The posture follows the source body, and the face is approximate across Character Creator facial profiles. For an exact result, apply the motion to your character in Character Creator 5 or iClone and export it. See [Clips & Layers](../using/clips-and-layers.md#what-to-do-where).
* **Mocap, face capture and lip-sync are not here.** AccuLips, AccuFACE and Motion LIVE are out of scope. Do that work in iClone and export the result.
* **Edits stay in Houdini.** There is no round trip back to iClone.
* **Assembling takes and transitions** belong in iClone. **Play Clip** switches whole clips.

## The rig

* **It freezes the character.** After a rig exists, changing the import settings or the character file does nothing until you delete the rig node and press **Build Character** again.
* **The catalog is not saved with the hip.** Press **Reload Catalog Poses** after reopening a scene.
* **Never use Match Current Definition on a built rig.** It would wipe the rig and your animation.
* **Karma render properties** (SSS Quality, the eye-light controls) are read when a render starts, so changing one means restarting the render.
