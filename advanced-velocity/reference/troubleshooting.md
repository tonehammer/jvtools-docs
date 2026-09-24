# Troubleshooting

**I tweak the Setup sliders and nothing changes** — you're in **Timed Events** mode, the default, where the live Setup is only a template — only *baked events* reach the output. Press **Create Event** to bake the setup, or **Update** on an existing event's row to fold your changes into it. The **Stale** readout and a pink timeline marker appear whenever an event no longer matches the setup it came from. If you'd rather the setup were evaluated live every frame, set **Mode** to *Single Field*.

**The node outputs nothing** — work down this list, it's almost always one of them:

* All six velocity types are **off by default**. Tick the checkbox in a section's header.
* In the **Velocity Mixer**, a **Gain** of 0 (Additive) or a **Weight** of 0 (Weighted) mutes that type.
* In Timed Events: no events, no output.
* **Combine Into Attribute** (Output tab) is off.
* **Output As** is set to *Force*, so the result went to the Force Attribute (`@av_force` by default) rather than `@v`. In Force mode an RBD solve also needs the wrangle that applies it — press **Create Connected RBD Sim**, or check the one you have reads that attribute and multiplies by `@mass`.

**The node changed the velocity my geometry already had** — **Incoming Velocity** in the mixer controls this, and it's **on** by default — upstream `@v` passes through and the node layers on top. Switch it off to author the attribute outright.

**My events went quiet after I changed the input geometry** — an event's bake is stored **per point**, so anything that changes the point count — re-fracturing, deleting geometry, a different scatter — leaves the old bakes unusable and the node silently writes zero. You'll see a warning on the **Events** tab when this has happened. Press **Re-bake All Events**, the reload icon in the Events tab's All Events row. It replays each event against its own stored snapshot at its own frame, so your timings and settings survive. This is *not* the same as pressing Update on every row: Update re-bakes from the **live** Setup, which overwrites each event with whatever is currently on screen.

**The event timeline disappeared** — the timeline is drawn by the node's viewer state, and refreshing asset libraries (among other things) drops the viewer out of it. **Visualization ▸ Timeline HUD ▸ Restore Viewport HUD** brings it back.

**Everything feels sluggish — scrubbing, parm edits, adding events** — check **Preview Motion** (Visualization tab) first. It ships off, but if you switched it on it's the usual culprit: the ghost draws a *second complete copy* of your input on every viewport redraw. To keep it on, drop **Ghost Style** from *Full Wireframe* to **Bounding Boxes** or **Points**. After that, the other two costs are **Guide Density** and **Guides Show = Both**, which draws the live-setup *and* baked-event streams at once. Quick way to tell them apart from your input: **click any other node.** Guide geometry stops drawing, so if everything snaps responsive the cost is in the visualization controls; if it doesn't, it's your input geometry.

**Off Surface pushes pieces away from the centre, not off the surface** — *Off Surface* and *Both* need a **point** `@N`. The Normal SOP defaults to vertex normals, which they can't see, so they fall back to pushing away from the body's centre. Set the Normal SOP to *Point*.

**My RBD pieces fight gravity, or hang in the air** — the solver's **Override Attributes from SOP** is re-stamping `@v` every frame, so gravity never accumulates. Gate the **Attributes** field beneath it on the node's **Injecting Now** readout, so velocity is only taken during an event's attack and hold — the recipe is in [Driving an RBD solver](../timed-events.md#driving-an-rbd-solver). Don't gate the *Override Attributes from SOP* toggle itself: the solver latches it at the sim's first frame. Both live under **Properties ▸ Pieces ▸ Override Attributes** — not the similarly named *Overwrite Attributes from SOP* under **Collision ▸ Collision Geometry**.

**My trigger wrangle does nothing** — `trigger` is missing from the solver's **Overwrite Attributes** field (**Properties ▸ Pieces ▸ Override Attributes ▸ Attributes**). The solver reads SOP attributes once at the sim's first frame and only refreshes the ones listed there, so `@trigger` stays frozen at 0 and the wrangle never fires, with no error anywhere. Add `trigger` to that field — [Exporting the trigger](../timed-events.md#exporting-the-trigger) has the full setup, including why `v` has to come out of it.

**My scene's nodes didn't pick up the new version** — the Houdini node type never changes between product versions, so scenes update in place. If you're still seeing the old behaviour you most likely have **two** `.hdalc` files defining the asset — delete the older one and restart Houdini.

---

Still stuck? Find me on the JVtools Discord — the invite link is in the **Utilities** folder on the HDA node.
