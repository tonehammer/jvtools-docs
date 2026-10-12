---
icon: play
order: 90
---

# Animating

Everything here happens on the rig node, in the animate state.

## Animate and Exit

**Animate** enters the APEX animate state, where you pose and key the controls in the viewport. **Exit Animate State** returns you to the normal view. Your keys live on animation layers inside the rig node, with the character's own clip at the bottom as **BaseAnimation**. See [Clips & Layers](clips-and-layers.md).

## Controls and gears

The body has IK/FK limbs, reverse feet, a spline spine, and FK for every finger and toe. Each part also has a **gear** control holding its settings, such as IK/FK and stretch. Two gear buttons are worth knowing:

* **Pin Controls** lists that gear's channels in the Animation Editor. It does not lock the pose, and pinning another gear replaces the list.
* **LOD 1, 2 and 3** are independent show/hide toggles. On the root gear they act on the whole rig, on any other gear only on that part.

The **Mirror** tool is in the Pose Tools row above the viewport. It draws a pale preview arm first: press **Enter** over the viewport to apply it, or Shift+click the Mirror icon to mirror at once.

## The Character Picker

In the animate state, open **New Pane Tab ▸ Animation ▸ APEX Character Picker**. It has Body, Hands, Feet and Face tabs, plus Extras if the character has joints beyond the standard Character Creator skeleton, such as hair bones. Each tab has a button per control, and clicking one selects it. The layout is read-only; to make your own, add a layout in the pane.

## The Animation Catalog

The rig build fills Houdini's Animation Catalog with 301 **expression** poses and 71 **hand poses** from Character Creator's own templates, in folders named after the rig.

Open an Animation Catalog pane in the animate state and apply a pose at the current frame. With controls selected, only those controls take it. With nothing selected, click the pose's tile and press **Apply** in the panel beside it, and it lands on every channel of the active layer. A hand pose sets both hands unless you first select one with **L Fingers** or **R Fingers** on the picker's Hands tab. A pose adds onto the clip's own face.

!!!warning The catalog is not saved with the hip
After reopening a scene, press **Reload Catalog Poses** on the rig node.
!!!

Dropping a pose into the viewport always needs selected controls, and a pose writes a single key. [Troubleshooting](../reference/troubleshooting.md) has the details.
