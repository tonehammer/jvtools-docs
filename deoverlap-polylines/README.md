---
icon: static/deoverlap-polylines_icon.svg
order: 70
image: static/social.png
---

# Deoverlap Polylines

<p style="text-align:center; margin:0 0 1.5rem;"><a href="https://jvtonehammer.gumroad.com/l/deoverlap_polylines_hda"><strong>Get it free on Gumroad &rarr;</strong></a></p>

**Deoverlap Polylines** (v{{ dp.version }}) finds where your curves cross each other and pushes them apart at those crossings, so a tangle reads as separate strands.

Wire curves in, curves come out separated. Hair, fibres, wires, cables, stitched lines, scattered strands, a grid of rows and columns — anything that looks like a mess because the curves are sitting on top of each other.

It's a small, free tool that does one thing.

## What it actually does

Three stages, and the middle one is what makes it more than a blunt displacement.

1. **It finds every crossing.**
2. **It decides which curve goes over and which goes under** — and by default that decision *alternates*, so a lattice of rows and columns comes out genuinely **woven**, like a hatch or a fence, instead of one set of curves lifted off the other.
3. **It pushes the two apart along the axis that actually separates them** — computed per crossing from both curves' tangents, so it stays correct on curves that wander in 3D. The push eases off along the curve rather than stepping, so the result undulates instead of kinking.

## What it does not do

Worth stating plainly, because each one saves a support conversation:

- It is **not a collision solver.** One measured push, no iteration, no convergence. Two curves can still overlap afterwards.
- It is **not a groom tool.** It works on curves that already exist; it does not generate, clump, comb or guide them.
- It is **not a mesh fixer.** Polylines only.
- It works on **polygon curves.** NURBS and Bezier curves pass through untouched — unless **Initial Resample** is on, which converts them to polylines on the way in and then it works normally.

!!!info Everything is a ratio, not a distance
The node normalises your geometry into a fixed box before it works on it and restores the transform on the way out. That's why every tolerance here reads as a small number and why one set of defaults behaves the same on a 1-unit curve set and a 1000-unit one. Read them as fractions of your input, not as world-space distances.
!!!

## Requirements

- **Houdini 22.0+**, Indie or Apprentice — it ships as `.hdalc`
- **Windows** — the only platform it has been tested on

## Pages

- [Getting started](getting-started.md)
- [Using Deoverlap Polylines](using.md)
- [Parameter reference](reference/parameters.md)
- [Changelog](reference/changelog.md)
- [License](reference/license.md)
