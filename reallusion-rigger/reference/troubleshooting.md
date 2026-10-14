---
icon: question
order: 80
---

# Troubleshooting & FAQ

This page covers the rig, the animation tools, and the character's look and materials.

## Look and materials

**The character is grey or has no textures.** The tool can't find the texture folder. Make sure the `textures` folder (and the `.fbm` folder) sit right next to the FBX, exactly as Character Creator exported them, and move them with the FBX if you move it. Textures are resolved relative to the FBX file. If you moved the export between machines through Google Drive (or another cloud download), check that you got all of it: Google Drive splits large folder downloads into multiple zip parts, and extracting only one part leaves the folder structure looking intact while half the texture files are missing. Extract every part into the same folder, then rebuild. The tool prints a console warning naming any materials it couldn't find a diffuse texture for, so if you see it, count your zip parts.

**Accessories are plain white, or no displacement appears.** Your export is missing its material `.json` file. Character Creator stores displacement, subsurface, wrinkle weights and the colors of custom accessories (horns, props, GoZ clothing) in a `my_character.json` beside the FBX, not in the FBX itself. Make sure it sits next to your FBX. It is created by the **Export JSON for Auto Material Setup** option, which is on by default, so if you don't have one, re-export with that option enabled. See [Preparing Your Character](../getting-started/preparing-your-character.md).

**Wrinkles don't animate.** The **Bake Wrinkles for Still Frame** export setting was left on, which freezes the wrinkles into one pose. Re-export from Character Creator with it turned OFF. To confirm wrinkles are working, click **Go to Max Wrinkle Frame** in the Wrinkles folder: it jumps to the most expressive frame. See [Preparing Your Character](../getting-started/preparing-your-character.md).

**A control I changed didn't update the render.** **SSS Quality** and the eye-light controls (Eyes Cast Light, Light Quality, Light Intensity) are Karma render properties, which Karma reads only when a render starts. Restart your Karma render after changing them. Every other control updates live.

**My hand edits to a material disappeared.** **Build Character** rebuilds the material networks from scratch every time, so anything you edited inside a material goes with them. Make look changes on the lookdev controller instead: its values are preserved across rebuilds, and so are your lights, camera, render settings and the rig. See [What survives a rebuild](../lookdev/lookdev-controller.md#what-survives-a-rebuild).

**Clothing or an accessory pokes through the body.** Use Skin Fix: **Create Skin-Fix Setup** in the **Skin-Fix** folder, then push the body in or the garment out. With **Stash Rig** on, press **Update Motion Clips** on the rig node to bring the edit into the rig. See [Skin Fix](../using/skin-fix.md).

**A small element, usually facial hair, breaks up during animation.** Character Creator sometimes exports duplicate blendshape targets for an element, and they fight each other once the face animates. Use the **Fix Broken Blendshape** folder on the Reallusion Rigger node: put the element in **Broken Elements** as an `@name` group (the `@name` attribute of that mesh), then turn on **Fix Broken Blendshape**. Adjust **Radius** if you see deforming artifacts. Leave it off otherwise: with no element picked, the toggle would bypass the whole mesh.

**My eyes don't look like they did in Character Creator.** Character Creator's HD eye shader bakes very little of its look into the export, so the eye imports with a neutral base color. Use the eye controls on the lookdev controller to rebuild the look in Houdini. Some aspects, such as true iris depth and pupil resize, can't be reproduced because the data isn't exported. See [Limitations & Expectations](limitations.md#the-eyes) and [Eyes](../lookdev/eyes.md).

**A control does nothing on my character.** Many features are character-dependent: they only work if your character's export carries the data they need (hair maps, a tear-line mesh, wrinkle maps, displacement maps). If a control seems inert, your character likely doesn't have that data. See [Limitations & Expectations](limitations.md#character-dependent-features).

**Does this work in an ACES pipeline?** Yes. Every texture is tagged with its colorspace explicitly and the tool sets no OCIO override of its own, so it follows your scene's config. The materials were built in ACEScg. See [Color management and ACES](../lookdev/rendering.md#color-management-and-aces).

**Can I use this in a commercial studio pipeline?** It is a limited-commercial (Indie) asset. Loading it into a commercial Houdini session switches that session to limited-commercial mode, per SideFX's rules, and you are responsible for your own SideFX license compliance. See [Requirements & Installation](../getting-started/installation.md).

## Build and rig

**I changed the character file or import settings and nothing happened.** The rig freezes the character it was built for. Delete the rig node and press **Build Character** again. Pressing it with a rig in place only refreshes the materials.

**The Face Tools and Auto Blink controls are greyed out.** The rig was built with **Build Facial Rig** off, so it has no face tools. Auto Breathe still works. To get the face tools, delete the rig node, turn **Build Facial Rig** on and build again.

**The Animation Catalog is empty after I reopened the scene.** The catalog is not saved with the hip. Press **Reload Catalog Poses** on the rig node.

**I use External File for the stash and the clips are missing.** The files have to travel with the hip. If they went missing, press **Update Motion Clips** to bake the clips again.

## Face

**I keyed `face_Jaw_Open` to 1 and the mouth did not open. It even looks more closed.** In Character Creator the jaw opens by rotating the jaw bone, and the `Jaw_Open` morph is only the skin correction that goes with that rotation, so on its own it pushes the lips and chin. Key `JawRoot_rx` (the bone), ideally together with `face_Jaw_Open`. The Jaw Open slider and Face Puppet drive both.

**I can't find the head-turn morphs among the face keys.** `Head_Turn_L/R/Up/Down` and `Head_Tilt_L/R` reshape the neck when the head moves, and the rig drives them from the head control, so they count as body channels. Clear Body Keys resets them with the head, while Clear Face Keys and Show Face Keys leave them alone. Edit them by moving the head.

**The Animation Editor never shows my face curves.** It lists only the channels of the controls you select, and face morphs belong to no control. Press **Show Face Keys** in the animate state.

**How do I see only the blinks Auto Blink wrote?** Click the AutoBlink layer in the Layers tab to make it active, then press **Show Face Keys**. Only `face_Eye_Blink_L` and `face_Eye_Blink_R` are listed.

**Moving the Look At slider pushes the eye crosses back and forth.** That is intended. See [Look At](../using/auto-animation.md#look-at).

## Catalog and posing

**I dragged a pose into the viewport and it says "No controls selected".** Dropping a catalog item into the viewport needs selected controls, for all three options in the drop menu. That's SideFX's rule. With nothing selected, click the pose's tile and press **Apply** in the panel beside it.

**Add to New Layer made an empty layer.** A new layer is built from the selected controls. Select them first: the Character Picker's Hands tab (left or right fingers) for a hand pose, the face gear for an expression.

**The fist showed on one frame, but the expression held across the whole clip.** A pose writes one key at the current frame. The fingers already carry the clip with a key on every frame, so the fist replaces just that frame. The expression lands on the face gear's channels, which had no other keys, and a single key holds everywhere. Apply a second expression at another frame and the face blends between the two, apply a neutral one where it should end, or use Add to New Layer and set that layer's weight over the frames you want.

**I clicked Mirror and only a pale preview arm appeared.** That is the live preview. Press **Enter** over the viewport to apply it, or Shift+click the Mirror icon for a mirror that applies at once.

## Clips and layers

**Play Clip and the clip menu in the Layers tab disagree.** Switch clips with **Play Clip**. It changes what the node plays and renders, fits the frame range, and moves the Layers-tab menu with it. The menu is SideFX's own, and a pick there doesn't move Play Clip or the frame range, so a longer clip is cut at the old range.

**I moved the arm at one frame and only that frame changed.** The baked clip has a key on every frame, so an edit changes only the key at the current frame. Put the change on an additive layer and key it at a few frames. See [Clips & Layers](../using/clips-and-layers.md#animation-layers).

**I can't delete BaseAnimation.** It is the character's own animation, even if that's just the pose it was exported in. Every other layer sits on top of it.

**I changed BaseAnimation by mistake.** Press **Revert to Clip** and pick Body, Face or Both. It also works after the scene was saved and reopened.

**How do I animate a layer's weight?** Right-click the layer in the Animation Layers pane and use **Add Weight to Channel List**, **Set Weight Keyframe**, **Remove Weight Keyframe** or **Set Weight from Playbar Selection**. Once the weight has keys, moving its slider keys it at the current frame.

**A clip from another character pinches the waist, or its mouth shapes look off.** Cross-character clips are approximations. The posture follows the source body, and the face is converted between Character Creator's HD and Extended profiles through Reallusion's channel table, which has no counterpart for some HD mouth and cheek shapes. Apply the motion to your character in Character Creator 5 or iClone and export it from there.

**Does Pin Controls lock the pose?** No. It lists that gear's channels in the Animation Editor, and pinning another gear replaces the list.

---

For anything not covered here, find me on the JVtools Discord - the invite link is in the **Utilities** folder on the HDA node.
