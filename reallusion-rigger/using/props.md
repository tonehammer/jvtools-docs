# Props

A prop, such as a sword, a cup or a phone, can be added to the rig's APEX scene and parented to a hand in the animate state. It then moves with the hand, and it renders with the character in Karma.

## Adding a prop

1. Dive into the rig node and find the **ANIMATE** node (see [Animating](animating.md#where-your-animation-lives)).
2. Put an **APEX Scene Add Prop** node between ANIMATE and the node above it: wire that node into the Add Prop node's first input, and the Add Prop node into ANIMATE.
3. Wire the prop's geometry into the Add Prop node's second input. Model it where it should sit at rest, in world space.
4. Press **Animate** on the rig node.

The prop has one control of its own, so you can move and key it like any other control.

## Putting it in a hand

1. In the animate state parameters, **Constraint** tab, set **Constraint** to **Offset** and **Offset** to **Static**, so the prop keeps the place it has relative to the hand at the moment you constrain it.
2. Move the prop's control to where it should sit in the hand.
3. Select the prop's control, Shift-select the hand control, and press **H**.

The prop now follows the hand. The constraint's **Blend** is keyable: key it to 0 at the frame the hand lets go, and the prop stays where it was released.

## Rendering

The prop reaches `/stage` with the character, as a mesh with no material. Assign it one in LOPs, as you would any other geometry.

!!!warning An update that re-bakes the character's own clip resets the props
**Update Motion Clips**, when it bakes the character's own clip again, resets ANIMATE's keys and constraints, the prop's included. Add the prop after the clips are final, or be ready to parent it again.
!!!
