---
icon: stack
order: 60
---

# Clips & Layers

## What to do where

The Rigger has two core jobs: **animating from scratch in Houdini**, body and face, and **refining a clip exported on the same character**. For the second, add the clip, switch to it with **Play Clip**, and adjust it on layers.

Mocap capture and cleanup, face capture and lip-sync, assembling takes and transitions, and combining body and face from different takes are better done in iClone, then exported on your character. To put a motion on a different character, apply it to your character there and export it. Every Character Creator body shares one skeleton and Reallusion keeps each body's own posture, so the clip plays exactly.

A clip exported on another character still works, because it is retargeted automatically, but it is an approximation. The posture follows the source body, which can pinch the waist, and the face is approximate across Character Creator's HD and Extended facial profiles. Use such a clip for blocking and reference. Edits made in Houdini stay in Houdini; there is no round trip back to iClone.

## Motion clips

The character's own clip is baked when the rig is built. The **Motion Clips** folder on the rig node holds the rest.

* **Clip Files** lists the clips to bake: a Character Creator Motions clip (USD), a character export (USD or FBX), or any FBX animation on a Character Creator skeleton. Picking a file fills the **Frames** limits with its range.
* **Update Motion Clips** bakes the list onto the rig without rebuilding it. New rows are baked, each into a clip of its own, removed rows leave, and unchanged rows are kept. The character's own clip always stays.
* **Clear Motion Clips** empties the list, after asking.
* **Play Clip** picks the clip the rig plays and fits the playback range to it.

Careful with this one: switch clips with **Play Clip**, not the clip menu at the top of the animate state's Layers tab. That menu is SideFX's own and doesn't fit the frame range, so a longer clip is cut at the old range.

## Animation layers

BaseAnimation is the character's own animation, even if that's just the pose it was exported in. Every other layer sits on top of it, so Houdini won't let you delete it. The **Layers** row on the rig node has the tools:

* **Add Rest Pose Layer** adds an override layer, RestPose, holding every body and face channel at rest, and makes it active. Key on it, and mute or delete it to get the clip back. Don't lower the BaseAnimation weight instead: it fades every channel toward zero, scales included, and the character collapses.
* **Clear Body Keys** and **Clear Face Keys** remove the active layer's animation. On BaseAnimation the body or face goes to the rest pose. On another layer the channels leave it and the layers below show through. Gear settings are never touched.
* **Revert to Clip** puts BaseAnimation back to the clip as it was baked, for Body, Face or Both. Other layers and gear settings stay as they are. It also works after a scene is saved and reopened, where Ctrl+Z no longer reaches.
* **Show Face Keys** is covered in [Face Tools](face-tools.md#show-face-keys).

Key on a layer of your own to keep the clip safe. To adjust a stretch of a clip, use an additive layer, because a change at one frame of a baked clip is a pop: select the control, create a layer from the selected controls (the + in the Layers tab), right-click it and choose Additive, then key a few frames: nothing at 20, arm up at 30, nothing at 40.
