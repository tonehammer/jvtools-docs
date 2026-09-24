---
icon: question
order: 80
---

# Troubleshooting

## Nothing appears / the node errors

The node draws the whole map on the GPU through Houdini's OpenCL device. If other OpenCL COPs do not cook on your machine, this one will not either - check that Houdini has a working OpenCL device before looking anywhere else.

## Sprites do nothing

**Enable Sprites** is off by default. Turn it on, and make sure at least one of the four packs is ticked - with none ticked, nothing is stamped.

## Changing Resolution has no effect

A layer is wired into the **Size Reference** input, and that layer's size wins. Unwire it, or change the size of what is feeding it instead.

## My displaced geometry barely changes

The geometry is too sparse - displacement only moves the points that are already there. Subdivide or Remesh it first, then raise **Displace Amount**. Also check **Midpoint**: at 0.5 a mid-grey area barely moves at all, since it sits close to the surface either way.

## The map does not match the web version with the same settings

The random sequence here is seeded independently, so the same settings give a different map with the same look, not the same map. Use **Seed** to reproduce a specific map inside Houdini rather than trying to match the web version's output.

## A sprite is partly cut off / moved

**Rotate** turns each sprite about the image centre, not the sprite's own centre - as in the original. On a non-square image this can carry a rotated sprite partly off-canvas.

## Show Color replaced my heightfield material

That is expected: **Show Color** assigns a HeightField Visualize material to preview the Color Gradient, and it replaces whatever material was already on the heightfield. Switch it off before rendering.

## The node says a new version is available

Download the new file from Gumroad, delete the old one, and restart Houdini.
