# Clips & Layers

## What to do where

The Rigger has two core jobs, and it helps to know them before you plan a shot:

* **Animating from scratch in Houdini**, body and face: the controls and gears, the Character Picker, catalog poses, Face Puppet, Face Key Muscle, Auto Blink, Auto Breathe and Look At.
* **Refining a clip exported on the same character**: add the clip, switch to it with **Play Clip**, and adjust it on layers — a contact, a glance, a blink, a facial beat.

Some work is better done in Reallusion's tools and exported onto your character: mocap capture and cleanup, face capture and lip-sync, assembling takes and transitions, and combining body and face from different takes all belong in iClone. To put a motion on a different character, apply it to **your** character in Character Creator 5 or iClone and export it from there. Every Character Creator body shares one skeleton and Character Creator keeps each body's own posture, so the clip then plays exactly, with nothing retargeted in Houdini.

A clip exported on another character still works, because it is retargeted automatically when you add it — but it is an approximation. The posture follows the source body (a curvy character played with a straighter body's walk gets its spine straightened, which can pinch the waist), and the face is approximate across Character Creator's two facial profiles (see [below](#clips-from-the-other-facial-profile)). Use such a clip for blocking and reference; for final animation, apply the motion in Character Creator 5 or iClone.

Edits made in Houdini stay in Houdini. There is no round trip back to iClone.

## Motion clips

The character's own clip is baked when the rig is built. The **Motion Clips** folder on the rig node holds the rest.

* **Clip Files** lists the clips to bake. A row takes a Character Creator **Motions** clip (USD — the small, fast one), a character export (USD or FBX), or any FBX animation on a Character Creator skeleton. Picking a file fills the **Frames** limits with its range; the two arrow buttons reset them.
* **Update Motion Clips** bakes the list onto the rig without rebuilding it. New rows are baked, each into a clip of its own, removed rows leave, and unchanged rows are kept as they are. The character's own clip always stays.
* **Clear Motion Clips** empties the list and updates in one step, after asking.
* **Play Clip** picks the clip the rig plays and renders, and fits the playback range to it. Switching takes a couple of seconds and re-bakes nothing.

!!!warning Careful with this one: switch clips with Play Clip
The animate state's **Layers** tab has a clip menu of its own at the top. It's SideFX's, and in their workflow it picks which of a rig's clips you animate. A pick there also changes what plays, but it doesn't move **Play Clip** or fit the frame range, so a longer clip gets cut off at the old range. Use **Play Clip**, which moves that menu along with it, and the two stay in step.
!!!

### Clips from the other facial profile

Character Creator characters come with one of two facial profiles: **HD** (Character Creator 5's) and **Extended** (Character Creator 4's). A clip made on a character with the other profile has its face converted through Reallusion's own channel table. The body plays normally, but the face is an approximation: the HD profile has mouth and cheek shapes the Extended profile has no counterpart for, so mouth shapes can look off. For a faithful face, apply the motion to your character in iClone and export it from there.

## Animation layers

Your keys sit on animation layers, stacked in the animate state's **Layers** tab. At the bottom is **BaseAnimation**: the character's own animation, even if that's just the pose it was exported in. Every other layer sits on top of it, which is why Houdini won't let you delete it.

The **Layers** row at the top of the rig node has five tools for them, as icons:

* **Add Rest Pose Layer** adds an override layer, **RestPose**, holding every body and face channel at rest, and makes it active. It's how you start from scratch without losing the clip: key on it, and mute or delete it to get the clip back. Don't lower the BaseAnimation weight instead — it fades every channel toward zero, scales included, and the character collapses.
* **Clear Body Keys** and **Clear Face Keys** remove the active layer's animation. On BaseAnimation, the body or face goes to the **rest pose** (not back to the clip). On any other layer the channels leave that layer, and the layers below show through. Gear settings are never touched.
* **Revert to Clip** puts BaseAnimation back to the clip as it was baked, for **Body**, **Face** or **Both**. Other layers and gear settings stay as they are, and Ctrl+Z undoes the revert. It also works after a scene is saved and reopened, where Ctrl+Z no longer reaches.
* **Show Face Keys** lists the face curves in the Animation Editor; see [Face Tools](face-tools.md#show-face-keys).

### Editing a stretch of a clip

A baked clip has a key on every frame. So if you move the arm at frame 30 on BaseAnimation, only frame 30 changes, and the arm pops there. To adjust a stretch of motion, put the change on a layer of its own:

1. Select the control.
2. Create a layer from the selected controls (the **+** in the Layers tab).
3. Right-click the new layer and choose **Additive**.
4. Key the change at a few frames: nothing at 20, arm up at 30, nothing at 40.

The additive layer adds on top of the clip and eases between its keys. This is the usual way to edit mocap, and it keeps the clip itself untouched.

### What lands on BaseAnimation by accident

Keying on a layer of your own keeps the clip safe. These are the things that write to BaseAnimation, and that **Revert to Clip** undoes:

* a catalog pose applied with **Add to New Layer** off,
* **Face Key Muscle** drags (they key BaseAnimation by design),
* a Face Puppet take with **Record to New Layer** off,
* **Clear Body Keys** or **Clear Face Keys** with BaseAnimation active.

### Animating a layer's weight

A layer's weight scales everything on it, and you can key it. Right-click the layer in the Layers tab:

* **Add Weight to Channel List** puts the weight curve in the Animation Editor.
* **Set Weight Keyframe** and **Remove Weight Keyframe** key or unkey the current weight at the current frame.
* **Set Weight from Playbar Selection**: Shift-drag a range on the timeline first, and the weight becomes 1 over it and 0 just outside.

Once the weight has keys, moving its slider keys it at the current frame.
