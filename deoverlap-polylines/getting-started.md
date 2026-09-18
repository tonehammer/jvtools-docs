# Getting started

## Installing

>>> 1. Drop the file in your otls folder
Put `JV-Deoverlap_Polylines-v1.0.hdalc` in `Documents/houdini22.0/otls/`. Houdini picks it up on the next launch.
>>>

>>> 2. Delete the previous version's file
If you're updating, **delete the old `.hdalc` first**. Two files defining the same asset will collide, and you don't want to find out which one won.
>>>

>>> 3. Find the node
It appears under **Tab ▸ JV ▸ Deoverlap Polylines**, at SOP level.
>>>

!!!warning Indie and Apprentice only
`.hdalc` is the Indie/Apprentice asset format. It will **not** load in Houdini FX or Core (commercial). That's a Houdini licensing rule, not a choice this tool makes.
!!!

## Your first result

Drop a **Grid** SOP, set it to **Rows and Columns**, wire it into a Deoverlap Polylines and look from the side. The rows and columns now weave over and under. No setup — the defaults are meant to work.

Turn **Push Amount** up and down to see the whole lattice breathe, and switch on **Visualize Intersection Points** to see what the node found. That guide is the first thing to reach for when nothing seems to be happening: no spheres means the problem is detection, not the push.

!!!tip A Grid SOP is a welded lattice, and that used to be the hard case
In Rows and Columns mode a grid shares a *single point* at every intersection — the rows and columns aren't crossing, they're joined, and a shared point can't move two ways. **Split Shared Points** (on by default) separates them, which is what makes this work at all. On a welded lattice that does raise the output point count, one point per curve.
!!!
