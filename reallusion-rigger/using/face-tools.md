---
icon: smiley
order: 80
---

# Face Tools

Every Character Creator morph channel is keyable on the rig as `face_<channel>`, and a clip carries its facial performance along with its body, so playing a clip plays the face too. On top of plain keys, the rig gives you four ways to work on the face: sliders, Face Key Muscle, Face Puppet, and catalog expressions (see [Animating](animating.md#the-animation-catalog)).

The **Face Tools** folder on the rig node is greyed out on a body-only rig (built with **Build Facial Rig** off).

## Sliders and the face board

In the animate state, sliders sit on the face for the brows, blinks, gaze, cheeks, jaw, mouth, tongue and visemes, and a small panel beside the head holds the channels that have no spot on the face. A slider **adds** to the clip's value, so a keyed slider is an offset on top of the performance, not a replacement of it.

The **Face** gear beside the head carries the face's settings. Two you'll use:

* **boxlayout** shows the same sliders as a flat panel locked to the viewport — the **face board** — and hides the ones on the face. It's easier to work with when the head is turned or small on screen. Drag the board by its circle; the X beside the circle turns it off again.
* **mouthControls** shows the lower teeth and tongue FK controls, hidden by default.

The Face gear's set menu (the face sprite at the bottom left of the viewport opens the same list) picks which sliders are shown: **Curated** (the essentials, the default), one region of the face with every channel in it, or **None**.

!!!warning Jaw Open needs the jaw bone
Keying `face_Jaw_Open` to 1 doesn't open the mouth — it can even look more closed. In Character Creator the jaw opens by rotating the jaw bone, and the `Jaw_Open` morph is only the skin correction that goes with that rotation, so on its own it pushes the lips and chin. To open the jaw by curve, key `JawRoot_rx` (the bone), ideally together with `face_Jaw_Open`. The Jaw Open slider and Face Puppet drive both for you.
!!!

The head-turn morphs (`Head_Turn_L/R/Up/Down`, `Head_Tilt_L/R`) reshape the neck as the head moves, and the rig drives them from the head control. So they count as **body** channels: **Clear Body Keys** resets them with the head, and **Clear Face Keys** and **Show Face Keys** leave them alone. Edit them by moving the head.

## Face Key Muscle

**Face Key Muscle** opens Character Creator's Muscle mode for this character: a drawing of the face with **Full Face**, **Eye**, **Mouth** and **Tongue** tabs. In the animate state, click a region (Ctrl-click for several) and drag. The face follows while you drag, and the frame is keyed when you let go, as one undo step. Esc cancels a drag.

* **Symmetric** brings the other side of the face along.
* **Expressiveness** sets how far a drag can push a shape, and **Mouse Range** how far you move the mouse for it.
* **Reset Selected**, **Reset to Zero** and **Revert** return the picked regions or the whole face to neutral, or restore the animation as it was when the panel opened.

Muscle drags key **BaseAnimation** directly. If that wasn't what you wanted, **Revert to Clip** undoes it; see [Clips & Layers](clips-and-layers.md#animation-layers).

## Face Puppet

Face Puppet records a facial performance with the mouse, the way iClone's does: you move the mouse, the playbar runs, and the face follows and is keyed.

**The pad** sits bottom-left in the animate state. Its menu sprite, at the pad's top right, picks the **profile**, from Character Creator's own puppet tables: region profiles first (brows, eyes, mouth and so on), then iClone's **Full Face** presets. The sprite beside it picks **Solo**, which limits the parts of the face the profile may move: Brow L/R, Blink L/R, Eye L/R, Eyeball L/R, Nose Tip, Nose L/R, Cheek L/R, Mouth, Jaw, Head Turn, Head Up/Down and Head Tilt. With nothing picked, the profile moves everything it drives. With some picked, the rest of the face keeps what the clip or your keys already had, and a take writes only those parts — solo **Mouth** and **Jaw** on a Full Face profile to puppet just the mouth.

### Recording a take

1. Press **Record** (the red dot) in the **Face Tools** folder.
2. Put the mouse over the viewport and press **SPACE**.
3. A red countdown runs the **Preroll** seconds, so you have time to find the motion. Then the playbar plays, with a red frame around the viewport while frames are being recorded, and the mouse drives the pad.
4. **SPACE** again, or the end of the frame range, stops the take. **Esc** cancels it.

While a take runs, hold the left mouse button to close the eyes, and press **Q W E R T Y** to switch to preset 1 to 6 of the current Full Face set. **Preview** (the play triangle) is the same control with no playbar and no keys, for trying a profile out.

### Where a take goes

**Record Mode** decides what a take does to the animation already there: **Replace** (iClone's default) makes the take the animation of the features it drives, and **Blend** adds it on top.

With **Record to New Layer** on (the default), each take gets a layer of its own — FacePuppet, FacePuppet2 and so on — that you can mute, delete or re-weight without touching the clip, and one undo removes the whole take. Replace makes that layer an override (the take replaces the face over its frames), Blend an additive one. With **Record to New Layer** off, a Replace take overwrites the clip's keys on BaseAnimation.

**Recording Settings** (closed by default) holds the rest: **Preroll**, **Record Speed** (1 is real time — slow it down for a tricky beat), **Mouse Range**, **Smoothing**, **Return to Start** and **Show Controls While Recording**.

## Show Face Keys

The Animation Editor lists only the channels of the controls you select, and face morphs belong to no control — so face curves never show up there on their own.

In the animate state, **Show Face Keys** (an icon in the rig node's **Layers** row) lists every face channel with keys on the **active** layer. Edits there play back at once, and Ctrl+Z undoes them. It replaces whatever was pinned, and it goes away when you exit the animate state.

To see only what one tool wrote, make its layer active first. For example, click the **AutoBlink** layer in the Layers tab, then press **Show Face Keys**, and only `face_Eye_Blink_L` and `face_Eye_Blink_R` are listed.
