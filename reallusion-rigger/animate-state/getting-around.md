# Getting Around

This section explains what you see on screen when you press **Animate** on the rig node, and what each part does.

Most of the animate state is SideFX's and is the same for every APEX rig. These pages cover what you need for this rig, and link to SideFX's documentation for the rest: [Working in the animate state](https://www.sidefx.com/docs/houdini/character/kinefx/animatestate.html).

Entering and leaving the state, mirroring, the Character Picker and the Animation Catalog are on the [Animating](../using/animating.md) page. Layers are on [Clips & Layers](../using/clips-and-layers.md). The face tools are on [Face Tools](../using/face-tools.md).

## The pages in this section

* [The Controls](controls.md) — every control on the body and face: what it is, its name, and what it moves.
* [Gears](gears.md) — the gear controls and every setting on them.
* This page — the panels, keys, settings and menus of the animate state itself, and the things that look wrong but aren't.

## The hint panel

The block of text at the top left of the viewport lists the state's main hotkeys. **Shift+F1** hides it.

## Hotkeys worth knowing

SideFX's full list is on their [Animate state hotkeys](https://www.sidefx.com/docs/houdini/character/kinefx/animatestatehotkeys.html) page. These are the ones you'll use most.

| Key | What it does |
| --- | --- |
| G | Opens the parameters HUD (the selected control's values; see below). |
| Ctrl+G | Opens the animate state settings. |
| Shift+V | Shows the selection sets in the HUD. |
| P | Opens the viewport state parameters window (see below). |
| F | Frames the selected controls. |
| Y | Cycles the handle between full transform, translate, rotate, scale and minimized. T, R and E switch straight to translate, rotate and scale. |
| Shift+T, Shift+R | Key the translate or the rotate of the selected controls. |
| Ctrl+A | Selects all controls. |
| PageUp / PageDown | Select the parent / child of the selected control. Home and End select the control to the left / right. Hold Shift to add to the selection. |
| ' (apostrophe) | Shows or hides the handle. |
| Shift+F2 | Shows or hides the HUDs. |

## Moving a control is not always keying it

The animate state follows Houdini's own keying preferences, the same ones as any keyframed parameter. They are in the drop-down menu next to the keyframe button on the playbar: **Auto-key changes** and **Auto-commit changes**. Out of the box, auto-key is off and auto-commit is on. SideFX's [Playbar](https://www.sidefx.com/docs/houdini/anim/playbar.html) page covers the keyframe button.

With **auto-commit** on, moving a control on a channel that already has a key at the current frame updates that key. That's why editing a baked clip works frame by frame: a baked clip has a key on every frame (see [Clips & Layers](../using/clips-and-layers.md#editing-a-stretch-of-a-clip)).

Otherwise the move is **pending**: you see it in the viewport, but nothing is keyed yet.

Careful with this one: change frame while a move is pending and the move is dropped. Key it first: **Shift+T** / **Shift+R**, right-click > **Key Components**, or Alt+click a value in the parameters HUD.

With **auto-key** on, every move is keyed at the current frame straight away.

Keys go on the active animation layer (see [Clips & Layers](../using/clips-and-layers.md#animation-layers)).

## The HUD

The panel the animate state shows over the viewport is its HUD. It has two halves.

* The top half is the **parameters**: with a control selected, its **Controls** tab shows its translate, rotate and scale values. Type a value, drag the value ladder, Alt+click a value to key it, Ctrl+click to remove the key at this frame. **G** brings it up.
* With a gear selected, the same tab lists the gear's settings, such as **Ikfkblend** or **Face set**. [Gears](gears.md) explains every one of them.
* The bottom half holds the **selection sets**, the **Layers** tab (the animation layers, see [Clips & Layers](../using/clips-and-layers.md#animation-layers)) and the **Settings** tab (**Ctrl+G**).

Right-click the HUD for its own options: pin it left or right, lock its position, minimize it, or **Toggle Split View** to show the two halves as separate panels.

SideFX documents the HUDs in [Animate state menus and HUDs](https://www.sidefx.com/docs/houdini/character/kinefx/animatestatesettings.html).

## The P window

**P** over the viewport opens the viewport state parameters. Three of its settings explain things people ask about:

* **Hide Controls During Playback** is on by default. That's why every control disappears when you press Play. There are also **Hide Controls During Scrub** and **Hide Controls During Drag**.
* **Use Click and Drag**: on, you click a control and drag it in one motion. Off, you select first and then drag the handle.
* **Use Control XRay** draws the controls through the character's body, with **XRay Strength** for how opaque.

The Face Puppet and Face Key Muscle recordings have their own **Show Controls While Recording** setting (see [Face Tools](../using/face-tools.md#recording-settings)).

## The right-click menu

Right-click in the viewport for the state's menu: copy and paste poses, handle modes and alignment, **Revert > Revert Controls to Default Values** (resets the selected controls' transforms), and the **Actions** submenu: **Mirror with Plane**, **Mirror with Default**, **Bake Keys**, and saving to the catalog. Mirroring is on the [Animating](../using/animating.md#mirroring-a-pose) page.

!!!warning Reset Animation removes everything you keyed
**Actions > Reset Animation** (and **Reset All**) removes the animation that was added in the animate state on this rig: your keys and the layers you made. The baked clips come back as they were baked. Save the scene before you try it. To put just the clip back, use **Revert to Clip** on the rig node instead (see [Clips & Layers](../using/clips-and-layers.md#animation-layers)).
!!!

Careful with this one: the **Actions** menu also has **New Clip** and **Edit Animation**, SideFX's own clip tools. The rig manages its clips from the **Motion Clips** folder on the rig node; use **Play Clip** there to switch (see [Clips & Layers](../using/clips-and-layers.md#motion-clips)). The same goes for the clip menu at the top of the HUD's **Layers** tab.

## Looks wrong, but isn't

* **The controls vanish when I press Play.** The **Hide Controls During Playback** setting is on by default. Press **P** to change it (see [The P window](#the-p-window)).
* **The arm has no FK rings.** The arm is in IK, and only the active mode's controls are drawn. Click the IK/FK switch on the arm's gear. See [Gears](gears.md#arm-gears).
* **The icons on a gear have no labels.** Hover one to see its name, or open the HUD (**G**) with the gear selected to see them all. See [Gears](gears.md#how-a-gear-works).
* **My pose disappeared when I changed frame.** It was pending, not keyed. See [Moving a control is not always keying it](#moving-a-control-is-not-always-keying-it).
* **I moved the arm and only one frame changed.** A baked clip has a key on every frame. See [Clips & Layers](../using/clips-and-layers.md#editing-a-stretch-of-a-clip).
* **A catalog expression holds on every frame.** It wrote one key on channels that had no other keys. See [Animating](../using/animating.md#the-animation-catalog).
* **The character collapsed when I set the BaseAnimation weight to 0.** Lowering its weight fades every channel toward zero, scales included. To start from the rest pose, use **Add Rest Pose Layer** instead. See [Clips & Layers](../using/clips-and-layers.md#animation-layers).
* **I can't delete, rename, mute or solo BaseAnimation.** Houdini doesn't allow it: it is the bottom of the layer stack and every other layer sits on top of it. Only its weight can change.
* **Moving the Look At slider moves the eye crosses.** That's what it does. See [Auto Animation](../using/auto-animation.md#look-at).
* **A face shape moves, but its slider is at zero.** A face shape has three inputs that add up: its keyed channel, its slider, and its channel on the Face Blendshapes gear. See [Gears](gears.md#face-blendshapes-gear).
