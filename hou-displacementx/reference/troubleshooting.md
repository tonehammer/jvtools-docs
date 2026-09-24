# Troubleshooting

**Nothing appears / the node errors** — the node draws the whole map on the GPU through Houdini's OpenCL device. If other OpenCL COPs do not cook on your machine, this one will not either - check that Houdini has a working OpenCL device before looking anywhere else.

**Changing Resolution has no effect** — a layer is wired into the **Size Reference** input, and that layer's size wins. Unwire it, or change the size of what is feeding it instead.

**My displaced geometry barely changes** — the geometry is too sparse - displacement only moves the points that are already there. Subdivide or Remesh it first, then raise **Displace Amount**. Also check **Midpoint**: at 0.5 a mid-grey area barely moves at all, since it sits close to the surface either way.
