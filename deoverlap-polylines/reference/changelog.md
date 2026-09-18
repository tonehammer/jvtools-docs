# Changelog

## v1.1
<p style="font-size:0.75rem; font-weight:400; opacity:0.38; letter-spacing:0.02em; margin:-0.85rem 0 1.2rem;">18 September 2026</p>

- Fixed: **Proximity Tolerance** could be raised to a value where the node silently stopped finding crossings.
- Fixed: the **Documentation** button opened a dead page.
- Fixed: the **Initial Resample** section no longer starts open over disabled controls.
- New: a **website** button in the Utilities links row.
- The node help page now shows the installed version instead of always reading 1.0.

## v1.0
<p style="font-size:0.75rem; font-weight:400; opacity:0.38; letter-spacing:0.02em; margin:-0.85rem 0 1.2rem;">27 August 2026</p>

First release.

**What it does**

- Finds where polylines cross each other and pushes them apart at the crossings.
- Push direction computed per crossing, perpendicular to both curves.
- **Over/Under Pattern**: alternating weaves rows and columns like a hatch; by curve order stacks them.
- **Push Symmetry** splits the separation between the two curves, or moves only one.
- **Push Radius** is relative to crossing spacing, so one default holds at any curve resolution.
- **Push Core** widens the full-strength region around each crossing.

**What it handles**

- Welded rows-and-columns lattices, via **Split Shared Points**.
- Closed curves, and curves that cross themselves.
- Crossings that land exactly on a vertex, including at curve ends.
- Optional **Initial Resample**, which also converts NURBS and Bezier input to polylines.

**Elsewhere**

- Intersection spheres and push weight draw as guide geometry, never in the output stream.
- Optional `deintersect` point attribute on the output.
