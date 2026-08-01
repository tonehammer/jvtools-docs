---
icon: zap
order: 95
---

# Quickstart

Two walkthroughs. The first is the smallest thing that does something. The second is the one this node was really built for — a telekinetic sequence where events push a rigid-body sim around and physics fills in the gaps.

## The 30-second explosion

1. Fracture something — a **Voronoi Fracture** into an **Assemble** with *Create Packed Geometry* on is the usual setup.
2. Drop **Advanced Velocity** after it, set **Mode** to *Single Field*, and switch on **Exploding Velocity**.
3. Leave **Origin** on *Whole Object*.

Every piece now flies away from the object's centre. To blast from a specific spot instead, switch **Origin** to *Point Source* and read [Point Source](using.md#point-source-explosions).

That's one push. The rest of this page is what happens when you want four.

---

## The telekinetic car

We're going to lift a car off the road, burst it apart, let the pieces orbit, and then draw them back into a solid ball — with gravity switched off until the very last beat, so the whole sequence floats and only the ending falls.

<!-- Screenshot Q0 (hero for this page) — a frame from the sequence: the car in pieces, suspended, mid-orbit:
![The telekinetic car mid-sequence](static/quickstart-hero.png) -->

Four events, in order:

| # | Frame | What it does | Mute Gravity |
| --- | --- | --- | --- |
| 1 | 20 | Lifts the car straight up | **on** |
| 2 | 45 | Bursts it apart | **on** |
| 3 | 70 | Swirls the pieces around the centre | **on** |
| 4 | 110 | Pulls everything back into a ball | **off** |

### Prepare the geometry

Fracture the car and pack it: **Voronoi Fracture** ▸ **Assemble** with *Create Packed Geometry* on. Packed pieces are one point each, which is what keeps this fast — a million-polygon car might only be a few thousand pieces, and Advanced Velocity works per point.

Drop **Advanced Velocity** after the Assemble and set **Mode** to *Timed Events*.

### Build the solver first

Press **Create Connected RBD Sim** in the **Output** tab.

That builds an RBD Bullet Solver below the node with a ground plane and gravity on, already wired to both of the contracts described below. Build it now rather than at the end — you want to see each event land in the sim as you author it, not discover at the end that nothing was connected.

### The two contracts

This is the part worth understanding, because it's what makes events and physics coexist. Advanced Velocity sits **upstream** of the sim, so it can't move anything itself. What it does is publish two live 0/1 signals that the solver reads.

<!-- Screenshot Q1 — the Output tab with Injecting Now reading 1 and Muting Gravity reading 0, mid-event:
![Injecting Now and Muting Gravity in the Output tab](static/contracts-output-tab.png) -->

**Injecting Now** (Output tab) reads 1 while any event is delivering energy — its attack and its hold — and 0 the rest of the time.

The Bullet solver takes velocity by *overwriting* it, not by adding to it. Left reading every frame, it re-stamps your velocity constantly and the pieces can never accelerate under gravity — they hang, and it looks broken. Gated on Injecting Now, the solve takes the velocity on impulse frames and runs free in between.

On the solver, that lives in:

> **Properties** ▸ **Pieces** ▸ **Override Attributes**

!!!warning Two similarly named parameters
There is a second *Overwrite Attributes from SOP* under **Collision ▸ Collision Geometry**. That is the collision one and it is not what you want. The one you want is under **Properties ▸ Pieces** and is called **Override Attributes from SOP**.
!!!

Leave **Override Attributes from SOP** switched **on** permanently, and gate the **Attributes** field beneath it instead — a Python expression that returns `v` only while Injecting Now is 1:

```python
"v" if hou.node("/obj/geo1/advanced_velocity1").evalParm("dyn_injecting") else ""
```

Don't gate the toggle itself. The solver latches it at the simulation's first frame, so a toggle that reads 0 on frame 1 delivers nothing at all, no matter how correctly it reads later.

<!-- Screenshot Q2 — the solver's Properties > Pieces > Override Attributes section, toggle ON and the gating expression visible in the Attributes field:
![Override Attributes from SOP on the RBD Bullet Solver](static/solver-override-attributes.png) -->

**Muting Gravity** (Output tab, just below Injecting Now) reads 1 while any event with **Mute Gravity** switched on is delivering energy — the same attack-plus-hold window.

On the solver, gravity lives in:

> **Forces** ▸ **Gravity** ▸ **Force**

Put the expression on that field's **Y** component, so gravity is your normal value except while an event is muting it:

```python
0.0 if hou.node("/obj/geo1/advanced_velocity1").evalParm("dyn_mute_gravity") else -9.80665
```

Drive the **Force** value, not the **Gravity** checkbox above it. Both work today, but a force magnitude is read every step by definition, whereas a toggle deciding whether the force exists is the same shape as Override Attributes from SOP — the kind of parameter that gets latched at frame 1.

<!-- Screenshot Q3 — the solver's Forces > Gravity section with the muting expression on the Force Y field:
![Gravity force on the RBD Bullet Solver](static/solver-gravity-force.png) -->

!!!warning Gravity belongs to the whole solve
Muting is not per piece. An event that mutes gravity mutes it for **every object in that simulation**, not only the pieces the event moves. Two fractured objects in one solver and only one being lifted means both will float.
!!!

### Event 1 — the lift (frame 20)

In **Setup**, switch on **Basic Velocity** and set **Value** to something like `0, 6, 0`. Go to frame 20 and press **Create Event**.

<!-- Screenshot Q4 — an event card with Event Options expanded, showing Track Motion, Create Rest Position Attribute and Mute Gravity:
![Event Options with Mute Gravity](static/event-options.png) -->

Open **Event Options** on the event card and switch **Mute Gravity** on. Then shape the envelope: a slow **Attack** of around 0.6 s so the car peels off the ground rather than snapping upward, a **Hold** of about 0.5 s, and **Release** off so the lift latches instead of fading.

Scrub through. The car should rise and then simply stay up — no fall, because gravity is muted and nothing else is pulling on it.

### Event 2 — the burst (frame 45)

Switch **Basic Velocity** off and switch **Exploding Velocity** on, leaving **Origin** on *Whole Object*. Keep it modest — this is a burst, not a detonation. Go to frame 45 and press **Create Event**.

Switch **Mute Gravity** on again. Give it a sharp **Attack** (0.1 s or so) and a short **Hold**, then a **Release** of about 1 s set to **Drag**, which decays the motion smoothly instead of cutting it. The pieces spread out and drift, still weightless.

### Event 3 — the orbit (frame 70)

Switch Exploding off and switch **Directional Velocity** on. Set **Direction** to *To Position*, leave the target at the world centre or type in the middle of the car, and pull **Direction Bias** to `0` — that's pure orbit, tangential motion with no pull inward or outward.

Go to frame 70, press **Create Event**, and switch **Mute Gravity** on. Use a gentle attack and a long hold so the swirl persists.

Because the pieces have moved a long way from where they were baked, leave **Track Motion** on (it's the default, in Event Options). It re-aims the field at the pieces' predicted positions each frame, so the orbit keeps circling the target instead of pointing at where the pieces used to be.

### Event 4 — the reassembly (frame 110)

This is where the rest-position machinery earns its place. On the **first** event, Event Options ▸ **Create Rest Position Attribute** was already on by default, so the car's original pose was recorded when you made it.

Set **Direction** to *To Rest Pose*, pick the rest attribute you want from the **Rest Pose Attribute** menu, and push **Direction Bias** back to `1` — straight at the target. Go to frame 110 and press **Create Event**.

**Leave Mute Gravity off on this one.** That's the whole ending: gravity comes back at the moment the pieces are pulled home, so the reassembled car forms and then drops under its own weight.

Give this event a long attack so the pieces gather rather than snap.

!!!tip To Rest Pose decelerates as it arrives
Its speed equals the distance remaining, so pieces slow down as they close in — an asymptotic approach that never quite slams together. For a constant-speed pull, switch on **Normalize Direction** and set the speed with the Adjust controls instead.
!!!

---

## The stasis trick

A question worth answering directly, because the behaviour is more useful than it first appears.

**What does an event with no velocity types enabled and Mute Gravity on actually do?**

It doesn't just mute gravity — it freezes everything solid. Measured on a real solve, with the pieces already flying upward when a blank event's window arrives:

| | motion per frame inside the window |
| --- | --- |
| Blank event alone | a steady -0.0094 — a slow sink |
| Blank event **+ Mute Gravity** | **exactly 0.0000 — dead stop** |

The reason is that a blank event still opens the Injecting Now gate. Its baked field is all zeros, so the solver dutifully overwrites every piece's velocity with zero. Add Mute Gravity and there is no gravity to pull them down either — so the pieces stop dead in mid-air and stay exactly where they were until the event's hold ends, then resume falling.

That is a genuinely useful beat for this kind of effect: **drop a blank event with Mute Gravity on wherever you want everything to hang suspended.** Set its Hold to the length of the pause you want.

Note the distinction, because it catches people out:

* Want gravity off but the pieces to **keep moving**? Put **Mute Gravity on the event that's already doing the work** — the lift, the burst — as in the walkthrough above.
* Want everything to **hang motionless**? Use a **blank event** with Mute Gravity on.

## If something looks wrong

* **Pieces hang in the air and never fall.** The Attributes list isn't gated — it's overwriting velocity every frame. Check the expression is on **Attributes**, not on the toggle.
* **The impulse never arrives.** You gated **Override Attributes from SOP** itself. Switch it permanently on and gate the list instead.
* **Nothing changes when you tweak the Setup sliders.** In Timed Events, the Setup tab is a template for the *next* event. Press **Update** on an existing event to re-bake it — the **Stale** readout tells you when an event has drifted from the live setup.
* **A later blast affects the wrong pieces.** Which pieces a Point Source catches is frozen when the event is baked. Track Motion re-aims directions, not membership.

More in [Troubleshooting](troubleshooting.md).
