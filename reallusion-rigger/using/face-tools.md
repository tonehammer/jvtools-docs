# Face Tools

Every Character Creator morph channel is keyable on the rig as `face_<channel>`, and a clip carries its facial performance with its body. The **Face Tools** folder is greyed out on a body-only rig.

## Sliders and the face board

In the animate state, sliders sit on the face for brows, blinks, gaze, cheeks, jaw, mouth, tongue and visemes, and a small panel beside the head holds the rest. A slider **adds** to the clip's value, so a keyed slider is an offset over the performance.

The **Face** gear beside the head carries `boxlayout` (the same sliders as a flat panel locked to the viewport, the face board) and `mouthControls` (the lower teeth and tongue FK controls, hidden by default), among others.

!!!warning Jaw Open needs the jaw bone
Keying `face_Jaw_Open` alone doesn't open the mouth. Character Creator opens the jaw with the jaw bone, and the morph is only the skin correction. Key `JawRoot_rx` as well. The Jaw Open slider and Face Puppet drive both.
!!!

## Face Key Muscle

**Face Key Muscle** opens Character Creator's Muscle mode: a drawing of the face with Full Face, Eye, Mouth and Tongue tabs. In the animate state, click a region (Ctrl-click for several) and drag. The face follows, and the frame is keyed when you let go, as one undo step. Esc cancels a drag.

**Symmetric** brings the other side along. **Expressiveness** sets how far a drag can push a shape, and **Mouse Range** how far you move for it. **Reset Selected**, **Reset to Zero** and **Revert** return regions or the whole face to neutral, or restore the animation as it was when the panel opened. Muscle drags key **BaseAnimation**; **Revert to Clip** undoes that.

## Face Puppet

Face Puppet records a facial performance with the mouse. The pad sits bottom-left in the animate state. Its menu sprite (top right of the pad) picks the profile, from Character Creator's puppet tables, and the sprite beside it picks **Solo**, which limits the parts of the face the profile may move. Nothing picked means everything the profile drives. The menu lists region profiles, then iClone's Full Face Control presets.

To record, press **Record** (the red dot) in Face Tools, put the mouse over the viewport and press **SPACE**. A red countdown runs the **Preroll**, then the playbar plays with a red frame round the viewport while the mouse drives the pad. **SPACE** again or the end of the range stops, and **Esc** cancels. Hold the left mouse button to close the eyes, and Q W E R T Y switch to preset 1 to 6 of the current Full Face set. **Preview** is the same control with no playbar and no keys.

**Record Mode** decides what a take does to what is already there: **Replace** (iClone's default) makes the take the animation of the features it drives, and **Blend** adds it on top. With **Record to New Layer** on (the default), each take gets its own layer, FacePuppet, FacePuppet2 and so on, and one undo removes the whole take. With it off, a Replace take overwrites the clip's keys on BaseAnimation.

## Show Face Keys

The Animation Editor lists only the channels of the controls you select, and face morphs belong to no control, so face curves never show up there. In the animate state, **Show Face Keys** (in the **Layers** row) lists every face channel with keys on the **active** layer, and edits there play back at once. It replaces whatever was pinned and goes away when you exit Animate.
