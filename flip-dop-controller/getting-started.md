# Getting started

## Install

1. Put `JV-FLIP_DOP_Controller-v1.0.hdalc` in `Documents/houdini22.0/otls/`.
2. **Delete the previous version's file** if you are updating — two files of the same type collide.
3. Restart Houdini, or **Assets ▸ Refresh Asset Libraries**.
4. It appears at **Tab ▸ JV ▸ FLIP DOP Controller**, at SOP level.

!!!warning Indie and Apprentice only
`.hdalc` does not load in commercial FX or Core.
!!!

## First setup

You need a DOP Network with a FLIP Object and a FLIP Solver already in it — this connects to a sim, it does not build one.

1. Drop the node at SOP level, anywhere.
2. Optionally wire in the geometry that defines your volume; that is what **Match Input Size** matches.
3. Set **DOP Network** to your dopnet.
4. Press **Connect Parameters**.

A report lists everything it wrote. From here the sliders on this node drive the sim.

## Three things that look wrong and are not

- **The box vanishes when you select another node.** It is guide geometry. That is how it stays out of your geometry stream.
- **The node has no output.** Deliberate — it is a controller.
- **Voxel Size will not accept typing.** It is derived. Set **Drive By** to *Voxel Size* to swap which of the pair you author.
