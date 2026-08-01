# Timed Events

One velocity field is rarely the whole story. The shot is a car *lifted* at frame 10, *torn apart* at frame 40, *spun* at frame 70 — three different velocity setups, at three different times, summed where they overlap. **Timed Events** is that: a keyframe animator for velocity.

Think of the Setup and Mixer tabs as a template. You dial in a velocity, press **Create Event**, and the node bakes the field it produces into an event stamped at the current frame. Then you change the setup and create the next one. At playback, every event contributes its baked field, faded in and out by its own envelope, and the output is the sum.

!!!info Why the sliders "do nothing"
In Timed Events mode the live Setup does not reach the output — only baked events do. If you tweak a slider and the sim doesn't respond, the event you're shaping hasn't been re-baked: press **Update** on its row. The node tells you when this happens — see [Editing an event](#editing-an-event).
!!!

## Creating events

* **Create Event** bakes the current setup into a new event at the playbar frame.
* **Record Events** jumps to the start frame and plays the range once — press Create Event as it plays to drop events in real time, like tapping keys into a performance. **Stop** ends it. Guides pause for the take (they are the bulk of the per-frame cost on dense inputs) and come back the moment playback ends.

Recording by feel wants a responsive playbar, so it is at its best on **lighter inputs** — packed pieces (one point per piece, realtime at any practical count) or meshes up to a few tens of thousands of points. On very dense raw-point inputs every event you drop starts contributing immediately, and playing back the events themselves costs per frame — the take will slow down as you stack them. Rough it in on a lighter proxy or the packed stream, then Update the events against the full-resolution input afterwards.
* **Copy Event** duplicates an existing event at the current frame — the same blast, later, with nothing re-baked.
* **Sort by Frame** reorders the rows chronologically (playback doesn't care about row order; this is for reading).

Each event is a tab in the **Events** list, named, stamped with its frame, and carrying a **Captured** summary of what it actually baked — which types, how many points, the peak speed. That line is worth glancing at: an event named "explosion" that captured `basic | 60 pts | max |v| 1` is telling you something.

## The envelope

Every event has an Attack / Hold / Release envelope around its **Event Frame** — the peak moment. Each phase has an enable checkbox and a duration in **frames**, the same unit as the Event Frame itself:

* **Attack** ramps the event in from zero to full, ending at the event frame — so an Attack of 5 opens five frames *before* the event frame. Off = it switches on instantly.
* **Hold** keeps it at full strength after the peak.
* **Release** fades it out afterwards, in one of two modes: **Fade to Zero** ramps down over the Release time; **Drag** decays gradually at a rate, so the pieces the event threw visibly slow down. Drag is the one timing control expressed per *second* rather than in frames — a decay rate per frame would be an unreadable fraction.

So an event's window — the span it delivers full strength — runs from `Event Frame − Attack` to `Event Frame + Hold`. That window is what **Injecting Now** and **Mute Gravity** key off, and it is worth being able to read off the timeline at a glance.

**Extend to Next**, on the Hold row, sets Hold so this event holds until the next one takes over: the hold ends exactly where the next event's Attack opens, so the two windows touch with no gap and without both sitting at full strength at once. The next event is the next by frame, whatever is soloed or muted. On the last event it does nothing and says so in the status bar. The small **undo** button beside it puts Hold back to what that press replaced — that one setting only, one press deep.

Attack and Release each take a **Curve** — Linear, Ease, Sharp, Snap, or Soft — for the shape of the ramp.

All three phases are **on** by default, so a fresh event ramps in, holds, and fades back out — a timed burst, which is what events are for. If you want a velocity that stays on for the whole shot, that is what **Single Field** mode is; and switching all three phases **off** makes an event *latch* — it starts at its frame and keeps delivering at full strength forever.

Latching is the right shape when an RBD solver overwrites `@v` every frame — a fading velocity handed to that solver would *brake* the pieces it just threw. (The better recipe is to keep the fade and gate the solver on **Injecting Now** instead — see [Driving an RBD solver](#driving-an-rbd-solver).) Note that a latched event also keeps the node cooking on every frame after it starts, which is worth knowing on heavy inputs.

## Editing an event

**Recall** loads an event's captured setup back into the live Setup and jumps to its frame. Edit whatever you like, then press **Update** to re-bake it.

The node watches for the trap in that loop: if the live Setup no longer matches the event it was last based on, the **Stale** readout names the event and its timeline marker turns **pink**. Nothing is lost — press Update to capture your changes, or Create Event to make the changes a new event instead.

**Clear Setup** (the broom next to Fold / Unfold All) switches every velocity type in the live Setup off — a clean slate for authoring the next event.

## Solo and Mute

**Solo** plays back *only* the listed events; **Mute** silences the listed ones. Both take space-separated numbers and ranges (`1 3-5`), and picking from the dropdown *adds* to the list rather than replacing it. Solo wins over Mute, and a soloed event is never cut short by the events it was soloed away from.

## The event timeline

With **Event Timeline** on (Visualization tab), a frame ruler draws along the bottom of the viewport with a marker per event and a playhead. The marker colours tell you each event's state at a glance:

* **Orange** — ready: baked and waiting for its frame.
* **Green** — playing: contributing right now.
* **Pink** — stale: the live Setup has moved since this event was baked.

Each event's label carries the same state in words, and the **At Frame** readout in the parameters spells out exactly which events are contributing at the current frame — including, in a gap, when the next one starts.

**Scheme** switches the timeline between Dark and Light palettes to match your viewport background.

!!!info If the timeline disappears
The timeline is drawn by the node's viewer state, and some actions (like refreshing asset libraries) drop the viewer out of it. **Utilities ▸ Restore Viewport HUD** brings it back.
!!!

## Motion preview

Baked vectors are only half the picture — you also want to see where the pieces *go*. **Preview Motion** (Visualization tab) advances the baked-event guides to where the events predict the pieces will be at the current frame, and the **ghost** draws a wireframe of the pieces there, tumbling with any baked `@w`. **Offset** slides the whole prediction sideways in multiples of the object's width, so the forecast reads beside the real geometry instead of on top of it.

On inputs above the **Visualization Limit** (Visualization tab, default 25,000 points) the preview auto-disables — integrating and moving that much geometry every frame is too slow to be a preview. The **At Frame** readout says so when it happens. Guide trails also cap themselves at the same limit, with **Guide Density** scaling within that budget. Raise the limit or switch **Enforce Visualization Limit** off to visualize everything regardless of cost.

The live Setup guides deliberately stay on the input mesh — the thing you're authoring reads in place, the prediction sits beside it.

The prediction is a straight-line integration of the baked fields — no collisions, no drag — so treat it as a forecast, not a simulation.

### Track Motion

An event's baked vectors were sampled at the input positions. Once pieces travel, a "toward the target" field frozen at bake time no longer points at the target. **Track Motion** (per event, on by default) re-aims the event's directional velocity at the pieces' predicted positions each frame — an orbit stays tangential, a Toward keeps pointing home.

It's only available when the event captured a *plain* Directional field: Adjust, Mask, Distance Falloff, per-piece scaling or a mix of types can't be re-evaluated, and the event then honestly replays frozen rather than guessing.

## Rest position attributes

Every cook stamps `@startframe_rest` — each point's position at the scene start frame — and each event with **Create Rest Position Attribute** on records its own `<name>_rest` at its frame. The Directional type's **To Rest Pose** mode aims at any of them: blow an object apart with one event, then pull the pieces back home with a later one. The attributes are stripped from the output unless **Export Rest Position Attributes** (with the other exports at the bottom of the Output tab) keeps them.

## Driving an RBD solver

The RBD Bullet Solver reads `@v` through **Override Attributes from SOP** (under **Properties ▸ Pieces ▸ Override Attributes**) — but left on every frame, it re-stamps the velocity constantly and the pieces fight gravity. The events should *inject*, then let physics own the pieces. That's what **Injecting Now** (Output tab) is for: it reads 1 while any event is delivering energy (attack + hold) and 0 the rest of the time.

On the solver:

1. Leave **Override Attributes from SOP** ON. (Don't gate the toggle itself — the solver latches it at the sim's first frame, and gating it delivers nothing at all.)
2. Gate the **Attributes** field beneath it instead — an expression that returns `v` only while Injecting Now reads 1, e.g. a Python expression on that parameter:

```python
"v" if hou.node("/obj/geo1/advanced_velocity1").evalParm("dyn_injecting") else ""
```

The solve then takes the velocity on the impulse frames and runs free in between — pieces launch, arc, and land under gravity, and the next event kicks them again. Leave `w` out of the list unless your events author angular velocity, or the solver's own tumble gets overwritten.

**In a hurry? Press Create Connected RBD Sim** (Output tab). It builds an RBD Bullet Solver below the node with a ground plane, gravity, and both gates already wired — the fastest way to see the contracts working, and a worked example to copy into your own setup.

For POP and Vellum none of this is needed. Set **Output As** to Force and the node writes an accumulated `@force` instead: those solvers add forces every step rather than overwriting velocity, so there is nothing to gate.

### Muting gravity for an impulse

Sometimes the physics is the problem. A telekinetic lift that fights 9.8 m/s² the whole way up reads as weak, and no amount of extra velocity fixes it — you want the object to genuinely float while the event holds it.

**Mute Gravity** (per event, in **Event Options**) does that. It has three settings:

* **Off** — gravity is never touched. The default.
* **During Impulse** — muted over the same window as Injecting Now, the attack and the hold, then back to 0. Gravity returns at the end of the peak and the pieces arc over naturally as the impulse fades.
* **Until Next Event** — the mute carries on until the next event opens, however short this event's Hold is.

That last one is what to reach for when a sequence of events leaves the pieces **falling in the gaps between beats**. It is deliberately *not* the same as extending Hold. Extending Hold keeps Injecting Now open too, so the solver re-stamps `@v` on every frame of the gap: the pieces fly on rails, with no collisions and no tumble. Extending only the gravity mute lets the impulse fade normally while the solver keeps the pieces — they coast on the momentum it already gave them, keep tumbling, still collide, and simply do not fall.

The last event has no next event, so it falls back to During Impulse — at the end of a shot the pieces are usually meant to land.

It's per event on purpose: the lift mutes, the blast that follows doesn't. Wire it on the solver the same way as the injection gate, but on the gravity *force* (**Forces ▸ Gravity ▸ Force**, on its Y component) rather than the **Gravity** checkbox above it:

```python
0.0 if hou.node("/obj/geo1/advanced_velocity1").evalParm("dyn_mute_gravity") else -9.80665
```

Drive the force value rather than the checkbox. Both work today, but a force magnitude is read every step by definition, whereas a toggle that decides whether the force exists is the same shape as **Override Attributes from SOP** — which is latched at the first frame and silently ignores animation.

!!!warning Gravity belongs to the whole solve
Muting is not per piece. Gravity in a simulation applies to every object in it, so an event that mutes gravity mutes it for *everything* in that solve, not only the pieces the event moves. If you have two fractured objects in one solver and only one is being lifted, both will float.
!!!

## Good to know

* **Incoming Velocity is a live base layer.** The velocity arriving on your input plays underneath the events, every frame — it's never baked into them, so it can't be double-counted and an animated input stays live between events.
* **Bakes are per-point.** An event's field is stored against the input's point count; re-fracture the object and existing events skip until you **Update** them.
* **A later blast kicks the pieces that were near it at bake time**, wherever they've since travelled — the radius selection is frozen when the event is baked. Track Motion re-aims directions, not membership.
* **Baked guides can be unified to one colour** (Visualization ▸ Unify Baked Guides) when the per-type colours are more information than you want.
* **A blank event with Mute Gravity on freezes everything solid.** With no velocity types enabled its baked field is all zeros, and it still opens the injection gate — so the solver overwrites every piece's velocity with zero while gravity is muted, and the pieces hang exactly where they were until the event's hold ends, then fall again. Useful on purpose: drop one wherever you want everything to hang suspended, and set its Hold to the length of the pause — or press **Extend to Next** to hang everything right up to the following beat. Note the distinction — Mute Gravity on a *real* event means gravity off while the pieces keep flying; a *blank* event with it on means everything stops dead.
