---
icon: tools
order: 90
---

# Using Advanced Velocity

## The four velocity types

Each type lives in its own collapsible section with a checkbox in the header. The controls stay hidden until the type is switched on, so the interface only shows you what you're actually using.

### Basic

A fixed vector applied to every point. The simplest possible velocity, and the one you'll reach for to give a whole body a shove in one direction.

### Directional

Velocity aimed at a target. **Direction** chooses where the target comes from:

* **Use Second Input** — the target is a point plugged into the node's second input. Press **Create Point** and the node builds an Add SOP holding a single point, one unit above your mesh, and wires it in for you. Move that point to aim.
* **SOP Path** — the target is the centre of another SOP, measured by centre of mass, bounding-box centre, or convex-hull centre.

**Normalize Direction** makes every direction unit length, so distance no longer affects speed. The **Distance Falloff** section fades the velocity with distance from the target through a ramp.

### Exploding

An outward burst, with two very different origins.

**Whole Object** radiates from the body itself:

* **Centroid** — everything pushes away from one point, which you can offset with **Move Centroid**.
* **Medial Axis** — the direction is measured from the *skeleton* of the body, so hollow, curved, or L-shaped objects burst outward sensibly instead of all sliding away from one average point. It's considerably slower, since it runs a VDB shrink loop to find the skeleton.

**Point Source** is covered below.

### Angular

An extra `@w` angular velocity vector, in radians per second, for solvers that read it. It's independent of the mixer — `@w` is simply written when the type is on.

---

## Point Source explosions

Point Source places a single blast origin *inside* the object and only affects the pieces near it. This is the mode built for dense fractured RBD — a wall taking an impact in one spot rather than an entire building flying apart.

### Placing the source interactively

Press **Select Source Position Interactively** and the viewport enters a placement state:

| Input | Action |
| --- | --- |
| **LMB drag** | Place the source on the surface, sliding it as you drag |
| **Wheel** (while dragging) | Push the source into or out of the mesh, along the view ray |
| **Ctrl / Shift** + wheel | Depth step ×10 / ×0.1 |
| **Shift + R** | Reset depth — the next click lands back on the surface |
| **Esc** | Finish |

The controls are also listed on screen while the state is active.

<!-- Screenshot 2 — the interactive placement state, HUD visible, affected pieces tinted:
![Placing the blast source in the viewport](static/point-source.png) -->

### Seeing what will move

**Show Affected Pieces** tints the pieces the blast will move, through the **Affected Color** ramp — green across most of the blast, hot pink at the core. The tint is normalized against the strongest affected piece, so the core always reads clearly whatever the radius or strength.

!!!info Falloff is measured to each piece's pivot
A radius smaller than your average piece size will catch nothing at all, because the distance is measured to each packed piece's pivot rather than its surface. If nothing tints, raise **Falloff Radius**.
!!!

### Direction

* **Outward** — a normal explosion, radiating away from the source.
* **Inward** — pieces are pulled toward the source, for implosions.
* **Both** — for thin objects: walls, panels, floors. Pieces are pushed off **both faces** instead of radiating sideways within the slab, which is what a radial blast does when every piece is roughly coplanar with the impact.

Both uses a **point** `@N` on your incoming geometry if it has one. A vertex normal won't do — set the Normal SOP to *Point* normals. Without a point `@N` it uses the thinnest axis of the bounding box, which is the wall normal for any slab-like shape. Fractured packed pieces carry no `@N` and all their pivots sit on the mid-plane, so pieces are split randomly across the two faces.

**Never Push Into Surface** mirrors any velocity heading back into the body, so every piece travels outward from the object's centre. It's off by default — the raw blast direction is the physically honest one, and this is an art-directable override. It's hidden in Both mode, which already guarantees pieces leave the surface.

---

## Adjust and Mask

Every velocity type carries the same pair of folders, promoted from Houdini's own Attribute Adjust nodes.

**Adjust** reshapes the velocity: scale its length, rotate its direction, spread it, or drive it from a random value or noise. Turn on **Adjust Value** to enable it. The Noise / Random section appears once you pick a random or noise value type, and carries the full fractal controls plus animation over time.

**Mask** restricts the velocity to part of the geometry — through a constant, random values, noise, another attribute, or a line, radial, or bounding-box gradient, remapped through a ramp.

Both blocks are Houdini's own controls, so the [Attribute Adjust Vector](https://www.sidefx.com/docs/houdini/nodes/sop/attribadjustvector.html) and [Attribute Adjust Float](https://www.sidefx.com/docs/houdini/nodes/sop/attribadjustfloat.html) help pages are the full reference for the parameters not described here.

---

## The Velocity Mixer

**Additive** multiplies each enabled type by its **Gain** and sums them. Gains default to 1 and go above it, so this is your straightforward "more of this, less of that" control.

**Weighted (Normalized)** blends the types in proportion to their **Weights**. The weights are normalized, so only their *ratio* matters and the result can never exceed the source magnitudes — **Mix Scale** is what pushes the blend past that.

### Output

**Combine Into @v** writes the mixed result to `v@v`. That's the normal output and it's on by default.

The three **Export** toggles keep an individual sub-velocity on the output as its own named attribute — `@basic_vel`, `@dir_vel`, `@exp_vel` — for when you want to blend them yourself downstream. Anything not exported is stripped before the output, so the node never leaks its internals.

Turning **Combine Into @v** off and exporting one or more sub-velocities gives you the raw ingredients with no `@v` at all.

---

## Visualization

**@v Vectors** and **Point Trails** switch on Houdini's own viewport displays — the yellow attribute vectors and the blue motion trails respectively.

The per-type toggles below draw coloured guide lines, one per point, scaled by **Scale** *and by that type's real contribution to the mix*. Turn a gain down and the guides shorten with it, so what you see tracks what the mixer is actually doing.

!!!warning The guide lines are real geometry
The per-type guides are polylines merged onto the output, and they set `Cd`. Switch them off before sending the result downstream.
!!!
