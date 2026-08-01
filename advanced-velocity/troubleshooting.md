# Troubleshooting

## I tweak the Setup sliders and nothing changes

You're in **Timed Events** mode (the default), where the live Setup is a template — only *baked events* reach the output. Press **Create Event** to bake the setup, or **Update** on an existing event's row to fold your changes into it. The **Stale** readout and a pink timeline marker appear when an event no longer matches the setup it came from.

If you want the setup evaluated live every frame instead, set **Mode** to *Single Field*.

## The node outputs zero velocity

All six velocity types are **off by default** — tick the checkbox in a section's header. If a type is on and you still get zero, check the **Velocity Mixer**: a **Gain** of 0 (Additive) or a **Weight** of 0 (Weighted) mutes that type. And in Timed Events, remember: no events, no output.

## The node changed the velocity my geometry already had

**Incoming Velocity** in the mixer controls this. It's **on** by default, so upstream `@v` passes through and the node layers on top of it. Switch it off to author the attribute outright — that's the mode where the node overwrites whatever arrived.

## There's no `@v` attribute at all

Either **Combine Into Attribute** (Output tab) is off, or **Output As** is set to *Force* — in Force mode the result is written to the Force Attribute (`@force` by default) instead.

## The guides vanished

Guide trails are **guide geometry**: they draw while the Advanced Velocity node is the current node, like the Bend SOP's guide. Select the node again and they return. Also check the **Show Guides** master switch, and **Guide Density** — at low values most trails are deliberately not drawn.

## The preview ghost doesn't appear on a heavy mesh

Preview Motion auto-disables on inputs above the **Visualization Limit** (Visualization tab, default 25,000 points) — integrating and moving that much geometry every frame is too slow to be a preview. The **At Frame** readout says so while it's the case. Raise the limit, switch **Enforce Visualization Limit** off, or author on a lighter proxy (packed pieces count one point each).

## The event timeline disappeared

The timeline is drawn by the node's viewer state, and refreshing asset libraries (among other things) drops the viewer out of it. Press **Utilities ▸ Restore Viewport HUD**.

## The Point Source explosion doesn't affect anything

The pieces are outside **Falloff Radius** — it's drawn as a wireframe sphere around the source, so check what actually sits inside it. The falloff is measured to each packed piece's real bounds, so what the sphere touches is what it catches. **Show Affected Pieces** tints exactly what will move.

## The blast pushes pieces through the object instead of blowing them off it

With the source placed *on* the surface, "away from the source" points through the body for every piece behind it — geometrically correct, and rarely what you want. Use **Direction ▸ Off Surface** (the default): pieces travel away from the *object*, and the source only decides which pieces are caught and how hard.

## Both / Off Surface ignore my normals

They need a **point** `@N`. A vertex normal isn't seen — set the Normal SOP to *Point* normals. Without point normals, Off Surface pushes away from the body's centre and Both uses the thinnest bounding-box axis.

## My RBD pieces fight gravity / hang in the air

The solver's **Overwrite Attributes from SOP** is re-stamping `@v` every frame, so gravity never accumulates. Gate the **Overwrite Attributes list** on the node's **Injecting Now** readout so velocity is only taken during an event's attack and hold — the exact recipe is in [Driving an RBD solver](timed-events.md#driving-an-rbd-solver). Don't gate the Overwrite from SOP toggle itself; the solver latches it at the sim's first frame.

## The pieces suddenly "stop rotating" mid-flight

They almost certainly haven't — a piece in free flight has no contacts, so no torque, so its spin rate is exactly constant, which reads as frozen next to fast translation. Watch what happens when they land: the tumble comes back. (The motion preview's ghost is a straight-line prediction, so judge rotation from the sim, not the ghost.)

## Medial Axis is extremely slow

It runs a VDB shrink loop to find the body's skeleton, and re-runs whenever the incoming geometry changes. Cache the geometry upstream, or set **Guides** to *Events* in Timed Events so the live setup isn't cooked every frame, or use Centroid while blocking and switch to Medial Axis at the end.

## Curl Noise doesn't keep swirling in the sim

By design — every type here authors an *initial* velocity, a one-time push. Sustained in-sim turbulence is a force field, which belongs in the solver (a POP Wind / custom force), not in the initial state.

## I re-fractured my object and the events went quiet

Event bakes are stored per point, so a changed point count no longer matches and those events are skipped. **Recall** and **Update** each event against the new fracture.

## My scene's nodes didn't pick up the new version

The Houdini node type never changes between product versions, so scenes update in place. If you're still on the old behaviour, you likely have **two** `.hdalc` files defining the asset — delete the older one and restart Houdini.

## Still stuck?

Find me on the [JVtools Discord](https://discord.gg/AG2w83WSM).
