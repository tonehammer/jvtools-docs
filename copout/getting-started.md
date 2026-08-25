# Getting started

## Installing

TODO — the standard install prose. It always covers:

1. Where the `.hdalc` goes (`Documents/houdini22.0/otls/`).
2. 🔴 **Delete the previous version's file** — two files of the same type collide.
3. Where the node appears: **Tab ▸ JV ▸ COPout**.
4. The Indie caveat: `.hdalc` loads in Indie/Apprentice, not commercial FX/Core.

## Your first output window

TODO — the shortest path from a scene with a copnet in it to an image on the
projector. Should be: drop the node, pick the copnet, pick the screen, press the
button.

## If something looks wrong

TODO — the ones already known from the shelf tool, all of which look like bugs
and are not:

- **Windowed and fullscreen look identical.** They coincide whenever the COP
  resolution matches the screen exactly. That is correct, not an inert control.
- **The "Both" overlay looks different from COP mode.** The overlay is a native
  viewport background and is gamma-approximated, so treat it as a reference view.
  Grade in COP mode.
- **The frame rate caps out.** Almost always the COP network's own cook time, not
  the output path. The panel reports the measured read time and the implied
  ceiling so you can tell the difference.
