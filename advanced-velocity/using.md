---
icon: tools
order: 90
---

# Using Advanced Velocity

This page covers the setup surface: the six velocity types, the mixer, the output and the visualization. The event workflow is a big enough topic that it gets [its own page](timed-events.md).

## The six velocity types

Each type lives in its own collapsible section with a checkbox in the header. The controls stay hidden until you actually turn the type on, so you are only ever looking at the things you're using.

### Basic

A fixed vector applied to every point. The simplest possible velocity — this is the one you reach for when you just want to give the whole body a shove in one direction.

### Directional

Velocity with a *direction* — at a target, around it, or away from it. First thing to set is **Direction**, which chooses where the target comes from:

* **To Position** (the default) — aim at a typed world-space position. No geometry needed at all.
* **SOP Path** — aim at another SOP in the scene. **Method** decides how the centre of that thing is measured (centre of mass, bounding box, convex hull), and **Target Group** restricts the measurement to a part of it. Tip: put a single point number in there and you are aiming at exactly that point.
* **Use Second Input** — aim at whatever geometry is wired into the second input of the node. Press **Create Point** and the node makes an Add SOP holding a single point above your mesh and wires it in for you.
* **To Rest Pose** — every point aims at its *own* captured rest position (the scene start frame, or any event's frame). This is the reassembly mode: pair it with **Track Motion** and an earlier event that throws the pieces, and each piece gets pulled back to its own captured spot — see [rest attributes](timed-events.md#rest-position-attributes).

**Direction Bias** is the main control here, and it is a *continuum*, not a set of modes: **+1** aims straight at the target, **0** is a pure orbit around an axle through it, **−1** points straight away. Anything in between spirals — meaning a vortex that also draws things inward does not need a second node. The **Toward / Around / Away** buttons just snap the bias to those three values. **Orbit Axis** decides the axle: *Toward Target* runs it from the object's centre through the target (so you can tilt the spin just by moving the target around), or you give it a fixed *Custom Vector*.

**Normalize Direction** makes every direction unit length, so distance stops affecting speed. **Distance Falloff** fades the velocity with distance — measured from the target, or from the axle when we are orbiting.

### Exploding

An outward burst, with two very different origins.

**Whole Object** radiates from the body itself:

* **Centroid** — everything pushes away from a single point, which you can offset with **Move Centroid**.
* **Medial Axis** — the direction is measured from the *skeleton* of the body instead. Why? Because hollow, curved or L-shaped objects don't really have a meaningful centre — with a centroid everything just slides away from one averaged point, whereas from the skeleton they burst outward sensibly. It is considerably slower, though, as it runs a VDB shrink loop to actually find that skeleton.

**Point Source** is a big enough topic that it gets [its own section below](#point-source-explosions).

### Velocity from Motion

Velocity derived from the movement the input already has, frame-to-frame — exactly the way a Trail SOP computes it. The use case is handing pre-sim momentum to an RBD or POP solve: animate a character swinging a prop, fracture the prop, and the pieces inherit the swing. Only meaningful on animated/deforming input, naturally — a static mesh gives you zero.

### Curl Noise

A divergence-free turbulent field (meaning: natural swirls with no sources or sinks) for debris drift and secondary motion. **Frequency** is the size of the vortices, **Amplitude** is the speed, **Octaves / Roughness / Lacunarity** add the fractal detail, and **Evolution Speed** churns the field over time (0 = frozen field). One thing to understand: this authors an *initial* velocity — a one-time push, not a force that keeps acting inside the sim.

### Angular

An extra `@w` spin vector, in radians per second, for the solvers that read it. **Source** is either a *Constant* vector, or *Inherited from Motion*, which computes it from the input's own rotation between frames (this one needs a point `orient` quaternion on the input to work). This type is independent of the mixer — `@w` is simply written whenever the type is on.

---

## Point Source explosions

Point Source places a single blast origin *inside* the object, and only the pieces within its **Falloff Radius** (drawn as a wireframe sphere in the viewport) get affected. This is the mode made for dense fractured RBD — think a wall taking an impact in one spot, rather than the entire building flying apart.

Important detail: the falloff is measured to each packed piece's **real bounds**, not just its centre point, so the radius behaves the way it looks against the sphere.

The falloff also decides *which pieces move, full stop*: Adjust and Mask variation (the Randomize row included) shape the pieces the blast caught, but can never add motion to a piece outside the radius — the output always agrees with the affected-piece tint.

### Placing the source interactively

Press **Place Source** and the viewport enters a placement state:

| Input | Action |
| --- | --- |
| **LMB drag** | Place the source on the surface, sliding it as you drag |
| **Scroll** (while dragging) | Grow or shrink the area of influence — the radius sphere follows live |
| **Shift + scroll** (while dragging) | Push the source into or out of the mesh, along the view ray |
| **Ctrl** + either scroll | Bigger steps |
| **Shift + R** | Reset depth and radius — the next click lands back on the surface at the default size |
| **Esc** | Finish |

The controls are also listed on screen while the state is active, so no need to memorize this table.

![Placing the blast source in the viewport](static/point-source.png)

### Seeing what will move

**Show Affected Pieces** highlights the pieces the blast will actually move, through the **Affected Color** ramp — green across most of the blast, hot pink at the core. The highlight is normalized against the strongest affected piece, so the core always reads clearly no matter what radius or strength you have set.

Important detail: the highlight is **drawn in the viewport, not painted onto your geometry**. Nothing is written to the output, so you can leave it on and send the result straight into a solver without dragging a stray `Cd` along with it. The flip side is that it only shows while the node's own tool is active — click the node in the viewport, or press **Restore Viewport HUD** on the Utilities tab if it has gone quiet.

### Direction

* **Off Surface** (the default) — pieces travel away from the *object*: along their point normals if the input has them, otherwise away from the body's centre. The source point still decides which pieces get caught and how hard. This is the mode that reads as "blowing a hole outwards".
* **Outward** — radiating away from the source point itself, as if a charge was sitting right at that point. Careful with this one: with the source placed *on* the surface, it drives material through the body and out the far side — geometrically correct, but usually Off Surface is the answer you actually wanted.
* **Inward** — pieces get pulled toward the source. Implosions.
* **Both** — made for thin objects: walls, panels, floors. Pieces get pushed off **both faces** instead of radiating sideways within the slab. Uses a point `@N` when present, otherwise the thinnest axis of the bounding box.

**Never Push Into Surface** mirrors any velocity that is heading back into the body. Think of it as an art-directable override for Outward / Inward; the modes that already leave the body (Both, Off Surface) hide it, as it would do nothing there.

---

## Adjust and Mask

Every velocity type carries the same pair of folders, promoted straight from Houdini's own Attribute Adjust nodes.

**Adjust** reshapes the velocity: scale the length, rotate the direction, spread it, or drive it from a random value or a noise. Turn on **Adjust Value** to enable it. The Noise / Random section appears once you pick a random or noise value type, and it carries the full fractal controls plus animation over time.

At the top of every Adjust folder sits the **Randomize** row: pick a **Variation** level (1 Subtle to 5 Extreme) and press the dice. The node looks at your input and detects whether it is discrete pieces (→ per-piece random) or a continuous surface (→ coherent noise), and presets the Adjust controls accordingly. Everything it does stays visible and hand-tunable, and the undo arrow reverts it. One special case: on Curl Noise the dice re-rolls the swirl pattern instead — different swirls, same character.

**Mask** restricts the velocity to a part of the geometry — a constant, random values, noise, another attribute, or a line / radial / bounding-box gradient, remapped through a ramp. The Line and Radial guides **fit themselves to your input** the first time you enable them, and there's a **Fit to Input** button to re-fit them any time after.

Both blocks are Houdini's own controls, so for the parameters not described here, the [Attribute Adjust Vector](https://www.sidefx.com/docs/houdini/nodes/sop/attribadjustvector.html) and [Attribute Adjust Float](https://www.sidefx.com/docs/houdini/nodes/sop/attribadjustfloat.html) help pages are the full reference.

---

## The Velocity Mixer

**Additive** multiplies each enabled type by its **Gain** and sums them up. Gains default to 1 and can go above it — this is your straightforward "more of this, less of that" way of working.

**Weighted (Normalized)** blends the types in proportion to their **Weights**. The weights are normalized, so only the *ratio* between them matters, and the result can never exceed the source magnitudes.

**Incoming Velocity** takes the velocity already sitting on the geometry and feeds it in as just another stream. It is on by default, and it is what lets you stack multiple Advanced Velocity nodes, or build on top of a cache or a previous sim. Its amount slider is a multiplier in Additive mode and a weight in Weighted mode. In Timed Events it plays as a live base layer under the events.

**Master Speed** is the single overall magnitude control, applied after the gains/weights in both modes.

In Timed Events the tab gains a second block above all of this: **Event Strength**, one slider per event. This is the *other* axis of mixing — the Gains and Weights balance the velocity types baked *into* an event, Event Strength balances whole events against each other. It applies live at playback, so dragging a slider never makes an event stale and never needs an Update; drop one to 0.2 and that whole beat plays at a fifth of its punch. One deliberate exception: a strength of 0 does not close the event's Injecting Now / Mute Gravity windows — those key off the event's timing, not its amount — so use **Mute** when you want an event genuinely out of the solve.

**Group**, at the very top of the node, restricts the final write: points outside the group keep whatever velocity they arrived with. This is how several Advanced Velocity nodes can each drive their own region.

---

## Output

**Combine Into Attribute** writes the mixed result to the output attribute — the normal output, on by default.

**Output As** picks between the two ways a solver can take motion from you, and the choice depends entirely on what you are feeding:

* **Velocity (`@v`)** — for the **RBD Bullet Solver**, which has no per-point force input at all. Important to understand: velocity is *set*, not added — whatever the solve had accumulated gets replaced on the frames you write. That is exactly why an RBD setup needs gating (below); leave this writing on every frame and the pieces can never fall.
* **Force (`@force`)** — for **POP** and **Vellum**, which *accumulate* forces every step. Nothing gets overwritten, so no gating is needed, and a fading release simply stops pushing rather than braking motion the sim already has.

The short version: **if it's Bullet, write velocity and gate it; if it's POP or Vellum, write force and forget about it.**

**Velocity Attribute** and **Force Attribute** let you name the written attribute in each mode — so you can author `targetv` for Vellum, for example, without touching a wrangle.

**Injecting Now** and **Muting Gravity** are live 0/1 readouts for driving an RBD solve, and **Create Connected RBD Sim** builds a solver already wired to both — see [Driving an RBD solver](timed-events.md#driving-an-rbd-solver).

### Ballistic Motion — the second output

The node has a second output, and it delivers the pieces **already flying**: advanced along the velocity you authored, frame by frame, tumbling with any baked `@w` if **Include Rotation** is on. No solver anywhere. Output 1 is completely untouched by this — your sim still gets the pieces at rest with `@v` on them — so wire output 2 when a real solve is overkill: previz, motion-graphics moves, a quick look test before committing to Bullet.

It's a straight-line integration — no collisions, no gravity — the same maths as the motion-preview ghost, applied to the real geometry. **Display Offset** slides the result sideways in multiples of the object's width, for reading it next to the original.

**Return to Home** is the part that makes it a tool rather than a toy. Keyframe it from 0 to 1 and every piece flies back to *exactly* where it started — and that landing is exact by construction: at 1, output 2 equals the input bit for bit, no matter how far the motion carried the pieces or what shaping you piled on. Telekinesis reassembly in one slider.

**Return Shaping** (collapsed under the slider) art-directs the way home without ever being able to break the landing:

* **Return Profile** — a ramp over the blend, for easing the approach.
* **Stagger** gives each piece its own return window, with **Return Order** deciding who leads: Random, Nearest First, or Farthest First. Everyone is still home by 1.
* **Arc** bows each piece's path sideways instead of a dead-straight line; **Swirl** blends those arcs toward a shared rotation around the **Swirl Axis** — crank it and the return becomes a vortex funnelling home.
* **Extra Turns** adds whole loops to the unwind. A full turn is invisible at both ends, so it only shows mid-flight.
* **Seed** re-rolls the per-piece arc directions.

The **Return Paths** toggle at the bottom draws each piece's route home as a guide curve — sampled from the very same curve the blend walks, so what you see is what plays.

**Post-Process** holds the final touches:

* **Clamp Speed** clamps the final speed into a Min / Max range.
* **Scale by Piece Size** makes the big chunks fly slower than the slivers — honestly the single biggest realism win on fractured RBD. Mass comes from a point `mass` attribute when present, otherwise from each packed piece's real size; **Influence** blends from uniform (0) through equal-energy (0.5) to full inverse mass (1). The average-sized piece keeps its speed, so the overall energy of the shot doesn't change.

The **Additional Exports** section (collapsed by default) keeps the individual sub-velocities on the output as their own named attributes — `@basic_vel`, `@dir_vel`, `@exp_vel`, `@motion_vel`, `@curl_vel` — plus the rest-position attributes, for when you want to blend or retarget things downstream. Anything not exported gets stripped, so the node never leaks its internals.

---

## Visualization

The guides are **guide geometry**: they draw in the viewport while the node is current and never touch the output — so there is nothing to clean up before a sim. Select a downstream node and they disappear with the selection, same as Houdini's own node guides.

* **Show Guides** is the master switch.
* Each stream has a toggle, a colour, and its own extra **Scale**, on top of the **Guide Global Scale**. The trail lengths are scaled by each stream's *real contribution to the mix* — turn a gain down and its guides shorten with it, so what you are seeing always tracks what the mixer is actually doing. Live setup trails draw dashed; baked event trails draw solid.
* **Normalize Guide Length** blends every trail toward one uniform length, with the joined 0–1 slider deciding how much. This is the one you reach for when a few fast points leave everything else unreadably short — at full normalization every guide draws at exactly Guide Global Scale length, so colour and direction carry the information instead of magnitude. Directions never change, and it's purely a display control — the output velocities are untouched.
* **Guide Density** draws only a fraction of the trails, for viewport speed on heavy fractures. The same pieces stay chosen frame to frame, so the selection doesn't flicker. On dense inputs the trails also auto-cap at the **Visualization Limit** (default 100,000), with Density scaling within that budget — raise the limit or switch it off if you really want to draw everything.

    The **first** time you connect geometry to a fresh node, Density gets set for you from the input's point count, aiming at roughly 200 trails — enough to read the field without covering the whole object. A few hundred points keeps every trail; a couple of thousand lands around `0.1`. This happens once and silently: change the value and it is yours, and re-wiring a different mesh later will never override it.
* Two further groups appear in Timed Events only. **Timed Events** holds **Source** (which stream the guides draw — Setup, Events or Both), **Preview Motion** with its ghost, **Ghost Style** and **Offset**, and **Unify Baked Guides**. Preview Motion ships **off** on purpose — it's the one control here with a real cost, since the ghost redraws your pieces every refresh. **Ghost Style** is what keeps that affordable: **Bounding Boxes** (the default) draws one wire box per piece and stays cheap at any density, **Points** is cheaper still, and **Full Wireframe** is the pretty one for light objects. Flip the preview on to check timing, then off again; on anything heavy it's what makes the whole scene feel sluggish. **Timeline HUD** holds the on-screen event ruler — see [the timeline and the preview](timed-events.md#the-event-timeline). The timeline itself is drawn by the viewer state rather than as guide geometry, which is why Show Guides and the Visualization Limit leave it alone.

Need the guides as *renderable* geometry, for a breakdown or a preview render? **Utilities ▸ Output Guides Only** swaps the node's output to the guide curves themselves.

In Timed Events this always gives you the baked event trails in their per-type colours, and it ignores **Show Guides** and **Source** — so the pass can't come out empty and can't accidentally pick up the pinned Setup guides. **Preview Motion is respected**: with it on, the trails follow the predicted motion, which is what you want comped over a moving render; with it off you get the trails anchored at the rest positions. The ghost never enters the pass either way, and the viewport shows the same thing, so what you see is what you render.
