# Rig Settings

## Stash Rig

**Stash Rig** stores the built, baked rig in the node, so reopening the scene or changing the frame range loads it in about a second. **Update Motion Clips** stores the new bake. The Rigger's own **Stash Rig** toggle decides this for a new rig, and this one changes it afterwards. Off rebuilds the rig live, about as long as the first build.

**Stash In** says where it lives, and changing it writes nothing.

* **Inside the Hip:** the scene file carries it, about 220 MB for a standard character, plus each clip.
* **External File:** **Save to Disk** writes the rig to the **Geometry File** (default `$HIP/jv_rig_cache/$OS.bgeo.sc`) and each baked clip beside it as `<file>_clip_<clip>.bgeo.sc`. The hip stays small, and the files are about 40% of the in-hip size.

Careful with this one: with External File, the files have to travel with the hip. If they go missing, press **Update Motion Clips** to bake the clips again.

## Hair Follows Head Only

Off, the hair keeps Character Creator's own skinning, so long hair drapes over moving shoulders. On, every hair mesh follows the head only. Switching re-cooks the output (a few seconds, longer on heavy characters) and keeps your keys.

## Viewport materials

The **Viewport** folder (closed by default, with a checkbox) shows the textured character in the SOP viewport, from the textures the importer resolved at **Build Character**. Off is plain grey. **Textured** picks which groups draw textured, and **Hair** is Off, **Opaque Cards** (solid cards in the hair's average colour) or **Transparent Cards** (the real opacity maps, best in an unlit viewport).

## The rig node is unlocked

The build unlocks the rig node, because your keys are stored in its interior. The license lets you open and modify it in your own scenes.

!!!danger Never use Match Current Definition on a built rig
It would wipe the generated rig and your animation.
!!!
