# Using Deoverlap Polylines

Most of the time you'll touch two sliders. This goes through the panel in order.

## Push

**Push Amount** is the total gap at a crossing, not the distance each curve moves. **Push Symmetry** shares it: at 1 both curves move half, at 0 one curve moves the whole way and the other stays exactly as you drew it — useful when one set is the thing you care about.

**Push Radius** is how far the push reaches along the curves from each crossing, measured as a fraction of the **average distance between crossings** rather than in points. That's what makes one default hold from a four-point curve to a hundred-point one. Around 0.5 gives a smooth weave.

Careful with this one: where crossings sit closer together than Push Radius, neighbouring pushes blend and partly cancel, so you get *less* separation than Push Amount asks for. That blending is what makes a weave undulate instead of step — but it means the slider is a ceiling, not a promise. Lower Push Radius if you want the full gap.

**Push Core** widens the flat top around each crossing. Zero is a smooth peak; raise it and the weave reads squarer.

### Push Along

Leave this on **Automatic** — it takes both curves' tangents at the crossing and pushes perpendicular to both, which is the only mode that stays correct on curves that wander in 3D. The others (Curve Normal, Up Vector, X/Y/Z) push everything along one fixed direction. Fine on flat curves, wrong at some crossings on 3D ones.

### Over/Under Pattern

**Alternating** swaps over and under at every crossing, which is what produces the weave. It's decided from each crossing's position along its own curves, so it doesn't depend on the order your curves happen to be in. **By Curve Order** puts the lower-numbered curve over every time, for stacked layers rather than a weave.

## Crossings

Everything about *finding* the crossings. When the node seems to be doing nothing, the answer is nearly always in here.

**Proximity Tolerance** is how close two curves must come to count as crossing. On flat curves it barely matters. **On 3D curves it matters more than anything else on the node** — two skew segments essentially never intersect exactly, so this decides whether there's a crossing there at all. If a 3D curve set comes out barely touched, raise this first.

**Split Shared Points** is on by default and should stay on: a Grid SOP's rows and columns share a point at every junction, and a shared point can't move two ways. It's also why a welded lattice comes out with more points than it went in with.

**Initial Resample** densifies the curves first. Off by default and rarely needed — but it's what makes NURBS and Bezier input work, since it converts them to polylines. Without it they pass straight through untouched.

**Intersect Mode** chooses every curve against every other, or only **Group A** against **Group B**. **Snap Intersecting Points** merges crossings that land near each other, so a near-tangential pass doesn't register as a cluster.

## Visualization

**Visualize Intersection Points** shows what the node found; **Visualize Push Weight** colours the curves by how much push each point got, which is the quickest way to see what Push Radius is doing.

Both draw as guide geometry, so they're visible only while this node is current and never enter the output. That's also the answer when the spheres vanish as you select another node.

!!!info The node can't tell you when it found nothing
An HDA cannot raise a warning on itself — Houdini only propagates interior *errors*, and erroring on "no crossings" would break your chain over a perfectly reasonable input. Turn on the intersection spheres; that's the readout.
!!!

## Utilities

**Output Deintersect Attribute** keeps the `deintersect` point attribute — a 0–1 weight of how much each point moved — for driving something downstream. Off by default, so the node leaves nothing behind.

**Check for Updates** asks whether a newer version is on Gumroad. The four buttons below open the store page, these docs, the Discord and the YouTube channel.
