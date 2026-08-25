# Getting started

## Installing

>>> 1. Drop the file in your otls folder
Put `JV-COPout-v1.0.hdalc` in `Documents/houdini22.0/otls/`. Houdini picks it up on the next launch.
>>>

>>> 2. Delete the previous version's file
If you're updating, **delete the old `.hdalc` first**. Two files defining the same asset will collide, and which one wins is not something you want to discover mid-show.
>>>

>>> 3. Find the node
It appears under **Tab ▸ JV ▸ COPout**, at SOP level.
>>>

!!!warning Indie and Apprentice only
`.hdalc` is the Indie/Apprentice asset format. It will **not** load in Houdini FX or Core (commercial). That's a licensing rule of Houdini's, not a choice this tool makes.
!!!

## Your first output window

The short version: drop the node, wire a copnet in, pick a screen, press the button.

>>> 1. Drop a COPout at SOP level
Anywhere in `/obj`. It's an ordinary SOP.
>>>

>>> 2. Wire a COP Network into its input
A SOP-level **COP Network** node has an output, so it wires straight in. COPout reads whichever node inside it holds the display flag.
>>>

>>> 3. Pick your display
The **Screen** dropdown lists the screens Qt can see right now — so your projector shows up as an entry once Windows has it.
>>>

>>> 4. Press Output COP
The window opens on that screen, borderless, at the COP's own resolution. **Close Output** tears it down again.
>>>

That's it. Everything from here is placement and taste.

!!!tip No network yet? Use the test pattern
Turn on **Test Pattern** and press **Output COP** with nothing wired at all. You get a grid, a centre crosshair, an aspect circle, colour bars and a gamma ramp — enough to aim and focus a projector before the content exists. Pick the aspect you're *going* to work at from the resolution menu beside it.
!!!

## Getting around the window

It has no title bar, so the usual furniture isn't there. The bindings are also listed in the node's **Utilities** tab, right where you'll be looking for them:

| Input | What it does |
|---|---|
| **Middle-drag** | move the window itself |
| **Right-drag** | move the image inside the window |
| **Double-click** or **F** | fullscreen |
| **Esc** | leave fullscreen |
| **Arrow keys** | nudge the image a pixel (Shift for ×10) |
| **Wheel**, or **+** / **-** | zoom |
| **0** | reset the position |

## If something looks wrong

Three things that look like bugs and aren't:

**Windowed and fullscreen look identical.** They genuinely coincide whenever the COP's resolution already matches the screen exactly — the windowed size *is* the screen size. Nothing is broken; change the COP resolution if you want to see the difference.

**The "Both" overlay doesn't match COP mode.** It won't, and that's expected. In Both mode the COP is composited by the viewport, which applies an approximate gamma rather than the exact sRGB curve. Treat Both as a reference view. **If a colour decision matters, make it in Copernicus mode.**

**The frame rate caps out lower than you asked for.** Almost always your COP network's own cook time, not the output path — a 1920×1400 feedback sim measures 24–43 ms a frame on its own, which is a 25–40 fps ceiling before COPout does anything. Read the **Status** field: it reports the measured read time and the frame rate that implies, so you can tell which side the limit is on. Raising **Max FPS** past what the network can cook buys you nothing.
