---
icon: download
order: 100
---

# Requirements & Installation

## Requirements

* **Houdini 22.0 or newer.** The Rigger is built on Houdini 22's APEX autorig builder. (The [Reallusion Importer](/reallusion-importer/getting-started/installation.md) also runs on Houdini 21.)
* **Windows**, which is what it was tested on.
* **A Character Creator 5 / iClone 8 character**, exported as USD or FBX. See [Preparing Your Character](preparing-your-character.md).
* **Karma** for rendering, tuned for XPU.

## Installation

The download is one file. It holds two nodes: the Rigger, and the **Reallusion Rigger APEX Rig** node, which **Build Character** creates below the Rigger. You never place the APEX Rig node by hand.

>>> 1. Locate your Houdini `otls` folder
On Windows, that's typically `C:\Users\<you>\Documents\houdini22.0\otls`. Create the folder if it doesn't exist.
>>>
>>> 2. Copy the file
Copy `JV-Reallusion_Rigger-v1.0_bb.hdalc` into it.
>>>
>>> 3. Restart Houdini
>>>
>>> 4. Verify the install
Inside a Geometry object, press **Tab**. **Reallusion Rigger** is under **JV**.
>>>

## Updating

Copy the new file in, delete the previous version's file (the filename carries the version), and restart Houdini.
