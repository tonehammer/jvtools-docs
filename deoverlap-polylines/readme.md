# Deoverlap Polylines

<div style="text-align:center; background:#0d1117; border-radius:16px; padding:2.5rem 1rem; margin:0.5rem 0 1.5rem;">
  <img src="static/deoverlap-polylines_icon.svg" alt="Deoverlap Polylines" width="150" style="max-width:60%;">
</div>

<p style="text-align:center; margin:0 0 1.5rem;"><a href="https://jvtonehammer.gumroad.com/l/deoverlap_polylines_hda"><strong>Get it free on Gumroad →</strong></a></p>

**Deoverlap Polylines** (v1.0) finds where your curves cross and pushes them apart at the crossings, so a tangle reads as separate strands. Hair, fibres, cables, stitched lines, a grid of rows and columns.

The over/under **alternates** by default, so a lattice comes out genuinely woven rather than one set of curves lifted off the other. The push is measured per crossing from both curves' tangents, so it holds up on curves that wander in 3D, and it eases along the curve instead of kinking.

One measured push, not a solver — curves can still touch afterwards.

Houdini has no native node that does this. The closest is the **Detangle** SOP, which is a solver component: it needs a previous-position attribute hand-fed before it will touch static curves, it resolves overlap rather than pushing by an amount you asked for, and it has no over/under control — on a grid it stacks every column over every row instead of weaving. Past that you are into Vellum or the Wire solver, which means substeps, a cache and a sim to art-direct. This is one cook.

## Requirements

- **Houdini 22.0+**, Indie or Apprentice — it ships as `.hdalc`
- **Windows** — the only platform it has been tested on

## Pages

- [Getting started](getting-started.md)
- [Using Deoverlap Polylines](using.md)
- [Parameter reference](reference/parameters.md)
- [Changelog](reference/changelog.md)
- [License](reference/license.md)
