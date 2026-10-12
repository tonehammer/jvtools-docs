# Auto Animation

Auto Blink and Auto Breathe write ordinary keys, each press on an animation layer of its own, so you can mute, reweight or delete the result. Both are in the rig node's **Auto Animation** folder.

## Auto Blink

**Add Auto Blink** keys `face_Eye_Blink_L` and `face_Eye_Blink_R` over the **Frame Range** on a layer named AutoBlink, AutoBlink2 and so on. It is one undo step and is greyed out on a body-only rig.

* **Profile** uses iClone's Auto Blink profiles: Normal, Nervous, Speechless, Charming and Child.
* **Clip Blinks** sets what happens to blinks already in the animation. **Keep** leaves them and makes an additive layer. **Replace** makes an override layer, so the eyelids blink only when Auto Blink says so over the Frame Range.
* **Seed** gives a different pattern with the same profile. To try another, delete the layer, change the Seed and press again.
* **Frame Range** follows the playback range until you type your own. Right-click it and choose Revert to Defaults to follow the playback range again.

## Auto Breathe

**Add Auto Breathe** keys breathing onto an additive layer named AutoBreathe, AutoBreathe2 and so on. It needs no facial rig.

* **Profile:** Calm is about 12 breaths a minute and shallow, Normal about 16, Heavy about 30 and deep with the shoulders lifting, Sleeping about 10, slow and deep, from the ribs.
* **Depth** scales the breaths (1 is the profile as it comes), and the layer's weight scales them again.
* **Seed** and **Frame Range** work as they do for Auto Blink.

It moves the chest, the two ribcage controls (`L_RibsTwist`, `R_RibsTwist`) and, on Calm, Normal and Heavy, the clavicles. The head keeps its aim and the hands stay where the clip holds them. Only whole breaths inside the Frame Range are written.

## Look At

The eyes can aim at two kinds of target, and the **Look At** slider chooses between them.

* **Each eye has its own small cross** in front of it. The crosses ride with the head and normally sit where the clip puts the gaze, so the clip's eye motion lives on them. Animate glances here.
* **The yellow three-ring control**, about a metre in front of the face, stays put in the world. Park it on another character or the camera and the eyes stay on it whatever the head does.

At **0** the crosses stay with the clip and the yellow target does nothing. At **1** the crosses sit on the yellow target, the eyes look at it, and the head and chest turn to help (**Head Weight**, **Body Weight**). In between, they sit partway. So moving the slider moves the crosses back and forth, which is intended. Neither target can do both jobs alone, so Look At blends from one to the other, as iClone's does.
