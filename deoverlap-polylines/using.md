---
icon: tools
order: 90
---

# Using Deoverlap Polylines

The node has two tabs and three folders, and most of the time you'll only touch two sliders. This page goes through them in panel order, and ends with the handful of things that look like bugs and aren't.

## Push

This is where you'll spend your time.

**Push Amount** is the total separation at a crossing — the whole gap, not the distance each curve moves. **Push Symmetry** decides how it's shared: at 1 both curves move half the distance, which reads as a real over/under; at 0 one curve moves the whole way and the other stays exactly as you drew it. That second one is genuinely useful when one set of curves is the thing you care about and the other is free to move. Either way the total gap is the same.

**Push Radius** is how far along the curves the push reaches from each crossing. Here's the part worth understanding: it's measured as a fraction of the **average distance between crossings**, not in point counts. That's deliberate, and it's what makes one default hold from a four-points-per-curve grid to a hundred-point one. Around 0.5 reaches halfway to the neighbouring crossing and gives a smooth weave. Push past 1 and neighbouring pushes start overlapping and partly cancelling, so the gap you actually get shrinks.

Careful with this one: where crossings genuinely sit closer together than Push Radius, the separation you get is *less* than Push Amount. That blending is exactly what makes a woven grid undulate instead of step, so it's a feature — but it does mean the number on the slider is a ceiling rather than a promise.

**Push Core** widens the flat top around each crossing before the falloff starts. Zero gives a smooth peak; raise it and the weave reads squarer and more stepped.

### Push Along

Leave this on **Automatic**. It takes the tangent of each curve at the crossing and pushes along the axis perpendicular to both — correct per crossing, no setup, and the only mode that stays correct on curves that wander in 3D.

The rest are there for when you *want* everything moving along one fixed direction: **Curve Normal** pushes sideways relative to the first curve, and **Up Vector** / **X** / **Y** / **Z** push along a direction you name. On flat curves they're all fine. On 3D curves they'll look wrong at some crossings, which is the whole reason Automatic is the default.

### Over/Under Pattern

**Alternating** swaps over and under at every crossing along both curves, which is what produces the weave. It's decided from each crossing's position along its own curves, so it doesn't depend on the order your curves happen to be in — that's why a grid comes out as a proper checkerboard rather than something that looks almost right.

**By Curve Order** puts the lower-numbered curve over every time, so the curves read as stacked layers. Reach for it when you want a clear front-to-back rather than a weave.

## Crossings

Everything about *finding* the crossings. When the node appears to be doing nothing, the answer is nearly always in here.

**Initial Resample** densifies the curves before the analysis. It's off by default and most inputs don't need it — crossing detection doesn't care about point count. Reach for it when your curves are so coarse that a crossing falls between points. It's also what makes NURBS and Bezier input work, since resampling converts them to polylines.

**Split Shared Points** is on by default and should stay that way. See the note in [Getting started](getting-started.md) for why a Grid SOP needs it.

**Intersect Mode** chooses between every curve against every other, or only **Group A** against **Group B** — for when one set of curves should move around another. Leaving both group fields empty behaves exactly like All.

**Proximity Tolerance** is how close two curves have to come to count as crossing, in multiples of the average spacing between points. On flat curves it barely matters — they genuinely intersect. **On curves that wander in 3D it matters more than anything else on the node**, because two skew segments essentially never intersect exactly, so this is the setting that decides whether there's a crossing there at all. If a 3D curve set comes out barely touched, raise this first.

**Snap Intersecting Points** merges crossings that land near each other into one, so a near-tangential pass doesn't register as a cluster of separate crossings all pushing at once.

## Visualization

Both of these draw as guide geometry — visible only while this node is current, never in the output stream.

**Visualize Intersection Points** is the diagnostic. **Visualize Push Weight** colours the curves by how much push each point received, which is the quickest way to see what Push Radius and Push Core are actually doing.

## Utilities

**Output Deintersect Attribute** keeps the `deintersect` point attribute on the output — a 0 to 1 weight of how much each point was pushed. Off by default, so the node leaves nothing behind in your geometry. Turn it on if you want to drive something downstream off the push.

**Check for Updates** asks whether a newer version is on Gumroad. It reads a small version file and sends nothing anywhere.

The four buttons below it open the store page, these docs, the Discord and the YouTube channel.

## Things that look wrong and aren't

- **The intersection spheres disappear when you select another node.** They're guide geometry, which only draws while this node is current. That's what keeps the output clean.
- **The tolerances look absurdly small.** They are. The tool normalises your geometry into a fixed box before working on it, so a tolerance is a fraction of your input's bounding box, not a world-space distance. That's what makes the defaults work at any scale.
- **A Grid SOP in Rows and Columns does nothing with Split Shared Points off.** It can't — the curves are welded, and a shared point can't move two ways.
- **NURBS or Bezier curves pass straight through.** Turn on Initial Resample, or put a Convert SOP in front.
- **The gap is smaller than Push Amount.** Your crossings are closer together than Push Radius, so neighbouring pushes are blending. Lower Push Radius if you want the full separation.
- **Nothing happens at all on 3D curves.** Raise Proximity Tolerance. Two skew segments almost never intersect exactly, so with a tight tolerance there is genuinely nothing there to find.
- **The output has more points than the input.** Only on a welded lattice, and only because each shared point had to become one point per curve. That's the price of separating joined curves.
- **The node says nothing when there's nothing to do.** It can't. An HDA cannot raise a warning on itself — Houdini only propagates interior *errors*, and erroring on "no crossings found" would break your chain over a perfectly reasonable input. Turn on the intersection spheres instead; that's the readout.
