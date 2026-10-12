---
icon: zap
order: 90
---

# Quick Start

This takes you from an empty scene to a character you can animate.

>>> 1. Create the node
Inside a Geometry object, press **Tab** and place a **Reallusion Rigger** (under **JV**).
>>>
>>> 2. Choose an import mode and set the file
Leave **Import** on **USD**, or switch it to **FBX**, then set **USD File** or **FBX File** to your export. See [USD vs FBX](import-modes.md).
>>>
>>> 3. Build the character
Click **Build Character**. **Build APEX Rig** is on by default, so the same press imports the character, builds its materials and lookdev controller, and builds the rig. That takes roughly 40 to 90 seconds on our test characters, and progress prints to the Python console.

When it finishes, a **Reallusion Rigger APEX Rig** node sits directly below the Rigger. It is the animatable character, and it is now the displayed node.

!!!warning Careful with this one
The rig freezes the character. If you change the import settings or the character file afterwards, nothing updates. Delete the rig node and press **Build Character** again. Pressing it with a rig in place only refreshes the materials.
!!!
>>>
>>> 4. Animate
Select the rig node and press **Animate**. Pick a control in the viewport and move or key it. The character's own animation is already there as the **BaseAnimation** layer. **Exit Animate State** returns you to the normal view.
>>>
>>> 5. Render
**Go to LOPs** (in the **Render** folder, below the rig options) jumps to the character and its lookdev controller. Karma reads the rig node's output, so your animation renders. Look development and lighting are the Importer's: see its [Lookdev Controller](/reallusion-importer/using/lookdev-controller.md) and [Rendering](/reallusion-importer/using/rendering.md) pages.
>>>

Next: [Building the Rig](../using/building-the-rig.md) and [Animating](../using/animating.md).
