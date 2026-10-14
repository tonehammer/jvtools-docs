---
icon: alert
order: 100
---

# Limitations & Expectations

Read this before you buy, and again if something surprises you.

## Platform

The Rigger needs **Houdini 22.0 or newer**, because it is built on Houdini 22's APEX autorig builder. It was tested on Windows; macOS and Linux are untested. The materials are tuned for **Karma XPU** and also render in **Karma CPU**. XPU is the path they were designed around, and CPU is a supported fallback. See [Requirements & Installation](../getting-started/installation.md).

## Memory

With USD import, 16 GB of RAM is the minimum and 32 GB is recommended. With FBX import it is 48 GB minimum and 64 GB recommended. FBX stores every facial blendshape as a full mesh copy, and Houdini must expand them all on import, so a fully-featured HD character can use 20–40 GB of RAM via FBX. See [USD vs FBX](../getting-started/import-modes.md). For ways to keep memory down, see [Performance & Memory](performance.md).

Stash Rig adds to the size of your scene: about 220 MB for a standard character, more for an HD one, plus each baked clip. An external file keeps the hip small. See [Rig Settings](../using/rig-settings.md).

## What only FBX has

Wrinkles, hair ombre and ID recolour, and flow-map anisotropy. Character Creator's USD export carries no data for them. The rig works in both modes.

## The eyes

This is the most important section to understand, because the eyes are where Character Creator's export is least complete.

Character Creator's premium "Digital Human" / HD eye has a rich shader — iris color, iris and pupil scale, limbal ring, iris depth/parallax, sclera shading, cornea wetness, and more. **Almost none of that is baked into the exported FBX or its texture data.** The export carries a neutral base iris texture and standard PBR maps; the rest of the eye's look lives only inside Character Creator.

!!!warning
**Don't rely on heavy eye customization in Character Creator carrying over.** If you carefully dial in iris color, depth, and shading in CC, the exported character will _not_ look the same in Houdini — that detail isn't in the file. Treat the CC eye look as a reference, not something that transfers.
!!!

**What the tool reproduces** (faked convincingly on the imported eye): iris color tint, iris scale, the limbal ring, eyelid contact shadow, and overall eye glossiness/wetness. See [Eyes](../lookdev/eyes.md).

**What the tool cannot reproduce** (the source data isn't exported): true iris depth and parallax, pupil resizing, and Character Creator's layered cornea/wetness shading. These can only be approximated, because the information needed to build them faithfully never leaves Character Creator.

**Set your eye look in Houdini using the tool's eye controls, not by trying to match a CC render.**

## Character-dependent features

Several features depend on what your specific character and its export actually contain. The tool detects what's present and enables those features automatically — if a control seems to do nothing, your character most likely doesn't carry the data that feature needs. This is normal and expected.

* **Hair re-dye** needs the character's hair to carry Character Creator's hair maps (root, ID, flow). Most styled scalp hair does; some hairstyles, caps, and simpler hair bake everything into a flat texture and can't be re-dyed (they still import and look correct). See [Hair](../lookdev/hair.md).
* **Tear-line wetness** needs the character to export a tear-line mesh. Some characters have one, some don't — it varies by base mesh and export. The tool's overall **Eye Glossiness** control works on every character regardless, so you always have a wet-eye lever. See [Eyes](../lookdev/eyes.md).
* **Wrinkles** need the character's expression-wrinkle maps (most CC heads have them).
* **Displacement** needs exported displacement maps.

None of these are bugs — they reflect what each character's export provides.

## UDIM (multi-tile) textures

Standard Character Creator characters use a single UV tile per material, which the tool handles normally. Characters authored with **UDIM / multi-tile textures** — an advanced setup, uncommon on stock CC base meshes — are **not currently supported**: the tool resolves one texture per channel, so only a single tile would load. If you work with UDIM characters, flatten them to a single 0–1 tile before export. Most users will never run into this.

## Mesh fixes (Skin Fix)

**Skin Fix** is for quick, point-level cleanup of mesh intersections (clothing poking through the body) — you move points, you don't change the mesh. Adding, deleting, or re-topologising geometry will break the character downstream, so it's intentionally constrained to nudging existing points. It's best for body and clothing; edits in face regions can be partially overridden by the blendshapes (those targets are defined against the original rest shape). For anything beyond quick fixes, do the work in Character Creator/ZBrush and re-export. See [Skin Fix](../using/skin-fix.md).

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
