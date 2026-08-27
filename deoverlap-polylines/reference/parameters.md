# Parameter reference

Every control on the node, in panel order. The prose version is in
[Using Deoverlap Polylines](../using.md).

## Push

| Parameter | What it does |
|---|---|
| **Push Along** | Direction the crossing curves are pushed apart along. *Automatic* is perpendicular to both curves at each crossing — correct per crossing, no setup, and the only mode that stays right on 3D curves. *Curve Normal* is sideways relative to the first curve, using Up Vector as reference. *Up Vector* and *X* / *Y* / *Z* push along a fixed direction. |
| **Invert Direction** | Push the opposite way. |
| **Up Vector** | Reference direction for Curve Normal, and the push direction itself in Up Vector mode. A curve running parallel to it falls back to another axis rather than collapsing. |
| **Over/Under Pattern** | Which curve of each crossing goes over. *Alternating* swaps at every crossing along both curves, so rows and columns come out woven. *By Curve Order* always puts the lower-numbered curve over, which reads as stacked layers. |
| **Push Amount** | The **total** separation at a crossing, split between the two curves by Push Symmetry. A fraction of one tenth of the input's largest bounding-box axis. |
| **Push Symmetry** | How the separation is shared. 1 splits it evenly (a real over/under); 0 moves one curve the whole way and leaves the other exactly as drawn. The total gap is the same either way. |
| **Push Radius** | How far along the curves the push reaches from each crossing, as a fraction of the average distance **between crossings**. Around 0.5 gives a smooth weave; above 1 neighbouring pushes overlap and partly cancel. |
| **Push Core** | Radius around each crossing that gets the full push before the falloff starts. Zero is a smooth peak; raising it flattens the top and the weave reads squarer. |

## Crossings

| Parameter | What it does |
|---|---|
| **Initial Resample** | Resample the curves before the crossing analysis. Off by default. Use it when the curves' own point resolution is too low — and it is what makes NURBS/Bezier input work, since it converts them to polylines. |
| **Maximum Segment Length** / **Length** | Limit the length of each resampled segment. In the input's **own units** — the resample runs before the tool's internal normalization, so this is a world-space distance. |
| **Maximum Segments** / **Segments** | Limit the number of segments per curve instead. |
| **Split Shared Points** | Split points belonging to more than one curve so they can move independently. Required for a welded lattice (a Grid SOP in Rows and Columns). A no-op on curves that are already separate, and it never moves a point. |
| **Intersect Mode** | *All* finds crossings between every curve; *Specific Groups* only between Group A and Group B. Both group fields empty behaves like All. |
| **Proximity Tolerance** | How close two curves must come to count as crossing, in multiples of the average spacing between points. Barely matters on flat curves; on 3D curves it is the single most important setting here. |
| **Group A** / **Group B** | The two primitive groups, in Specific Groups mode. |
| **Snap Intersecting Points** | Merge crossings that land within this distance of each other into one. |

## Visualization

Both draw as **guide geometry** — visible only while the node is current, never in the output stream.

| Parameter | What it does |
|---|---|
| **Visualize Intersection Points** | A sphere at every crossing the node found. The first thing to check when nothing seems to happen. |
| **Intersection Points** | Colour of those spheres. |
| **Size** | Their size, relative to the input's bounding box. |
| **Visualize Push Weight** | Colour the curves by how much push each point received. |

## Utilities

| Parameter | What it does |
|---|---|
| **Output Deintersect Attribute** | Keep the `deintersect` point attribute (0 to 1 push weight) on the output. Off by default, so the node leaves nothing behind. |
| **Check for Updates** | Check whether a newer version is on Gumroad. Reads a version file; sends nothing anywhere. |
| **Links** | Store page, documentation, Discord, YouTube. |

## Version signals

Every jvtools node carries these at the bottom of its parameter list:

| Parameter | What it does |
|---|---|
| **Current Version** | The product version of the asset you have installed. |
| *(update notice)* | Appears when a newer version is available on the store. |
