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

The fastest thing to look at is a grid, because the weave is unmistakable.

>>> 1. Make a grid of crossing lines
Drop a **Grid** SOP and set it to **Rows and Columns**. Ten by ten is plenty.
>>>

>>> 2. Wire it into a Deoverlap Polylines
That's it — no setup. The defaults are meant to work.
>>>

>>> 3. Look at it from the side
The rows and columns now weave over and under each other. Turn **Push Amount** up and down and watch the whole lattice breathe.
>>>

!!!tip A Grid SOP is a welded lattice, and that used to be the hard case
In Rows and Columns mode a grid shares a *single point* at every intersection — the rows and columns aren't crossing, they're joined. A shared point can't move two ways at once, so nothing could push them apart. **Split Shared Points** (on by default) separates them, which is what makes this work at all. On a welded lattice it does raise the output point count, one point per curve; that's unavoidable.
!!!

## Looking at what it found

Two guides, both in the **Visualization** folder:

- **Visualize Intersection Points** puts a sphere at every crossing. This is the first thing to turn on when nothing seems to be happening — if the spheres aren't there, the problem is detection, not the push.
- **Visualize Push Weight** colours the curves by how much push each point received, so you can see how far the effect reaches.

!!!info The guides vanish when you select another node
They're guide geometry, which Houdini only draws while the node is *current*. Not a bug — it's what keeps them out of your geometry stream entirely.
!!!
