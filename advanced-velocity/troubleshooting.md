# Troubleshooting

## I tweak the Setup sliders and nothing changes

You're in **Timed Events** mode, the default, where the live Setup is only a template — only *baked events* reach the output. Press **Create Event** to bake the setup, or **Update** on an existing event's row to fold your changes into it. The **Stale** readout and a pink timeline marker appear whenever an event no longer matches the setup it came from.

If you'd rather the setup were evaluated live every frame, set **Mode** to *Single Field*.

## The node outputs nothing

Work down this list — it's almost always one of them:

* All six velocity types are **off by default**. Tick the checkbox in a section's header.
* In the **Velocity Mixer**, a **Gain** of 0 (Additive) or a **Weight** of 0 (Weighted) mutes that type.
* In Timed Events: no events, no output.
* **Combine Into Attribute** (Output tab) is off.
* **Output As** is set to *Force*, so the result went to the Force Attribute (`@force`) rather than `@v`.

## The node changed the velocity my geometry already had

**Incoming Velocity** in the mixer controls this, and it's **on** by default — upstream `@v` passes through and the node layers on top. Switch it off to author the attribute outright.

## My events went quiet after I changed the input geometry

An event's bake is stored **per point**, so anything that changes the point count — re-fracturing, deleting geometry, a different scatter — leaves the old bakes unusable and the node silently writes zero. You'll see a warning on the **Events** tab when this has happened.

Press **Utilities ▸ Re-bake All Events**. It replays each event against its own stored snapshot at its own frame, so your timings and settings survive. This is *not* the same as pressing Update on every row: Update re-bakes from the **live** Setup, which overwrites each event with whatever is currently on screen.

## The guides vanished

Guide trails are **guide geometry** — they only draw while the Advanced Velocity node is the current node, exactly like the Bend SOP's guide. Select the node again and they're back. Also check the **Show Guides** master switch and **Guide Density**, which deliberately drops most trails at low values.

## The event timeline disappeared

The timeline is drawn by the node's viewer state, and refreshing asset libraries (among other things) drops the viewer out of it. **Utilities ▸ Restore Viewport HUD** brings it back.

## Everything feels sluggish — scrubbing, parm edits, adding events

Check **Preview Motion** (Visualization tab) first. It ships off, but if you switched it on it's the usual culprit: the ghost draws a *second complete copy* of your input on every viewport redraw, slowing down anything that causes one, not just playback. To keep it on, drop **Ghost Style** from *Full Wireframe* (default, and the expensive one) to **Bounding Boxes** (one wire box per piece, cheap at any density) or **Points**. Treat it as a check-your-timing tool: flip on, look, flip off.

After that, the other two costs are **Guide Density** (1.0 on a dense input is a trail per point; the node auto-picks a sensible value on first connection, so a hand-raised one is worth a second look) and **Guides Show = Both**, which draws the live-setup *and* baked-event streams at once.

One thing that isn't the node: a heavily textured mesh is expensive to draw whatever you do to it.

Quick way to tell them apart: **click any other node.** All guide geometry stops drawing, because it only appears while this node is current. If everything snaps responsive, the cost is in the visualization controls above. If it doesn't, it's your input geometry.

## The explosion pushes pieces the wrong way, or misses them entirely

Two different causes, and it's worth knowing which you have.

If pieces are driven *through* the object: with the source placed on the surface, "away from the source" points through the body for every piece behind it. Geometrically correct, rarely what you wanted. Use **Direction ▸ Off Surface** (the default) — pieces travel away from the *object*, and the source only decides which get caught and how hard.

If pieces don't move at all: they're outside **Falloff Radius**, drawn as a wireframe sphere around the source. The falloff is measured to each packed piece's real bounds, so what the sphere touches is what it catches. **Show Affected Pieces** highlights exactly what will move, in the viewport only.

One thing to check: *Off Surface* and *Both* need a **point** `@N`. A vertex normal is invisible to them, and the Normal SOP defaults to vertex — set it to *Point*. Without point normals, Off Surface falls back to pushing away from the body's centre.

## My RBD pieces fight gravity, or hang in the air

The solver's **Override Attributes from SOP** is re-stamping `@v` every frame, so gravity never accumulates. Gate the **Attributes** field beneath it on the node's **Injecting Now** readout, so velocity is only taken during an event's attack and hold — the recipe is in [Driving an RBD solver](timed-events.md#driving-an-rbd-solver).

Don't gate the *Override Attributes from SOP* toggle itself: the solver latches it at the sim's first frame, so your gating does nothing.

Both live under **Properties ▸ Pieces ▸ Override Attributes**. Beware the similarly named *Overwrite Attributes from SOP* under **Collision ▸ Collision Geometry** — that one is for collision geometry and is not what you want.

## My trigger wrangle does nothing

`trigger` is almost certainly missing from the solver's **Overwrite Attributes** field (**Properties ▸ Pieces ▸ Override Attributes ▸ Attributes**). This is the single most common reason a trigger setup goes completely silent, and it's worth understanding why it's silent rather than just patching it: the solver copies every SOP attribute once, when it builds the objects at the sim's first frame, so `@trigger` genuinely exists inside the sim. It's simply never refreshed after that — frozen at whatever it read on frame one, which is almost always 0. So `f@trigger` reads a flat 0 on every substep of every frame, `if (amp > 0)` never fires, and the wrangle does nothing at all. No error on the wrangle, no error on the solver, nothing in the node's own warnings — it just quietly never fires.

To confirm it: find a frame where the node's own `@trigger` is clearly nonzero, then check the same attribute inside the sim at that frame. If it reads a flat 0 there while the node says otherwise, that's the diagnosis, and adding `trigger` to the Attributes field is the fix — see [Exporting the trigger](timed-events.md#exporting-the-trigger) for the full setup, including why `v` has to come **out** of that same field once `trigger` goes in.

Same trap, mirror image: if pieces never launch at all when you're driving the solve with the node's velocity directly, check that `v` is listed there instead, gated on **Injecting Now** — see [Driving an RBD solver](timed-events.md#driving-an-rbd-solver).

## My scene's nodes didn't pick up the new version

The Houdini node type never changes between product versions, so scenes update in place. If you're still seeing the old behaviour you most likely have **two** `.hdalc` files defining the asset — delete the older one and restart Houdini.

## Still stuck?

Find me on the [JVtools Discord](https://discord.gg/AG2w83WSM).
