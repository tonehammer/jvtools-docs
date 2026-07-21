# Troubleshooting

## The node outputs nothing / `@v` is all zero

All four velocity types are **off by default**. Tick the checkbox in a section's header to switch that type on.

If a type is on and you still get zero, check the **Velocity Mixer** — in Additive mode a **Gain** of 0 mutes that type, and in Weighted mode a **Weight** of 0 does the same.

## There's no `@v` attribute at all

**Combine Into @v** in the Mixer's Output section has been turned off. That's the switch that writes `v@v`.

## The Point Source explosion doesn't affect anything

**Falloff Radius** is measured from the source to each piece's **pivot**, not its surface. On packed fractured geometry every piece's pivot sits at its centre, so a radius smaller than your average piece size catches nothing at all. Raise the radius until pieces start to tint.

## The blast pushes pieces into the object instead of away from it

That's geometrically correct — with the source placed on the surface, "away from the source" points *into* the body for every piece behind it. Turn on **Never Push Into Surface** to mirror those, or use **Direction ▸ Both** if the object is thin.

## Both mode sends every piece the same way

Both needs to know which face each piece leaves by. If your geometry has a **vertex** normal rather than a **point** normal, it isn't seen — set the Normal SOP to *Point* normals, or remove `N` entirely and let the node use the thinnest bounding-box axis instead.

## Medial Axis is extremely slow

It runs a VDB shrink loop to find the body's skeleton, and it re-runs whenever the incoming geometry changes. Cache the geometry upstream, or use Centroid while you're setting other things up and switch to Medial Axis at the end.

## Coloured lines and `Cd` are appearing on my output

Those are the per-type visualization guides. They're real polylines merged onto the output and they set `Cd`. Switch off the type toggles in the **Visualization** section before sending the result downstream.

**Show Affected Pieces** on the Point Source explosion also writes `Cd`.

## The velocity guides don't respond to the mixer

They should — the guides are scaled by each type's real contribution. If a guide vanishes entirely rather than shortening, that type's gain or weight has reached 0, which switches the type off completely.

## The interactive placement button does nothing

The state needs a Scene View to enter. If nothing happens, make sure a viewport is open and the node is selected. Placement only responds while **Origin** is set to *Point Source* — the button switches it there for you.

## My scene's nodes didn't pick up the new version

The Houdini node type never changes between product versions, so scenes update in place. If you're still on the old behaviour, you likely have **two** `.hdalc` files defining the asset — delete the older one and restart Houdini.

## Still stuck?

Find me on the [JVtools Discord](https://discord.gg/AG2w83WSM).
