---
icon: list-unordered
order: 110
---

# Parameter Reference

Two nodes, one table each. Labels are exactly as they appear on the node. The look-development controls live on the lookdev controller, which is the Importer's: see its [Lookdev Controller](/reallusion-importer/using/lookdev-controller.md) page.

## Reallusion Rigger

### Top of the node

| Parameter | What it does |
|---|---|
| **Import** | Which Character Creator export format to import: USD or FBX. |
| **Import Modes** | Opens the USD vs FBX documentation page. |
| **FBX File** | The Character Creator 5 / iClone 8 FBX export to import. Textures and material data are read from alongside it. |
| **USD File** | The `.usd` from Character Creator's Export USD (Omniverse). Keep the `Materials` folder beside it as exported. |

### Character ▸ Build

| Parameter | What it does |
|---|---|
| **Build Character** | Imports the character and builds the materials, displacement and lookdev controller, plus the rig when **Build APEX Rig** is on. Safe to re-run: lookdev values are kept and an existing rig is left as it is. |
| **Build APEX Rig** | Also builds the rig, as its own node below this one. Never rebuilds or deletes an existing rig. Off: the importer on its own. |
| **Build Facial Rig** | Also builds the facial rig. Off gives a faster, lighter body-only rig with a neutral face. |
| **Load Expression Presets** | Loads about 300 Character Creator face poses into the Animation Catalog during the build. |
| **Load Hand Poses** | Loads Character Creator's 71 hand gestures into the Animation Catalog during the build. |
| **Stash Rig** | Stores the built and baked rig inside the rig node so a reopened scene loads in seconds. |
| **Set Frame Range to Animation** | Sets the scene's frame range to the character's animation before the rig is built. |

### Character ▸ Build ▸ Render

| Parameter | What it does |
|---|---|
| **Build In** | Which LOP network **Build Character** builds into. Defaults to `/stage`. Change it before building. |
| **Create Render Setup** | Also builds a 3-point light rig, a bust-framed camera and a Karma XPU render settings node. |
| **Go to LOPs** | Jumps to the LOP network and frames the lookdev controller. |

### Character ▸ Skin-Fix

| Parameter | What it does |
|---|---|
| **Create Skin-Fix Setup** | Creates (or jumps to) the Skin Fix subnetwork, for mesh intersections such as clothing poking through the body. |
| **Use Skin-Fix Mesh** | Switches the character onto the edited mesh. Off by default; safe to toggle any time. |

### Character ▸ Fix Broken Blendshape

| Parameter | What it does |
|---|---|
| **Broken Elements** | Elements that skip the blendshapes and follow the nearest face or body geometry, picked by their `@name`. |
| **Fix Broken Blendshape** | Does the bypassing. Only available once an element is picked. |
| **Radius** | Point Deform radius for the bypassed elements. |

### Utilities

| Parameter | What it does |
|---|---|
| **Clear Scene Cache** | Flushes Houdini's geometry cache to reclaim RAM. |
| **CC Export Settings** | A reminder of the Character Creator export settings for the current import mode. |
| **Links** | Opens jvtools.dev. |
| **Gumroad**, **Documentation**, **Discord**, **Youtube** | Open the product page, the documentation, the community Discord and the YouTube channel. |
| **Current Version** | The installed version. A notice appears beside it when a newer one is available. |

## Reallusion Rigger APEX Rig

### Top rows

| Parameter | What it does |
|---|---|
| **Animate** | Enters the APEX animate state on the rig, to pose and key the character in the viewport. |
| **Exit Animate State** | Back to the normal view. |
| **Layers** (the row) | Add Rest Pose Layer, **Clear Body Keys**, **Clear Face Keys**, **Revert to Clip** and **Show Face Keys**, in that order. |
| **Add Rest Pose Layer** | Adds an override layer, RestPose, holding every body and face channel at rest. It becomes the active layer. |
| **Clear Body Keys** | Removes the body animation of the active layer. One undo step. |
| **Clear Face Keys** | The same for the face. |
| **Revert to Clip** | Puts BaseAnimation back to the clip as baked: Body, Face or Both. |
| **Show Face Keys** | Lists the face channels with keys on the active layer in the Animation Editor. |
| **Reload Catalog Poses** | Puts this character's expression and hand poses back in the Animation Catalog. |

### Viewport

| Parameter | What it does |
|---|---|
| **Viewport Materials** | The textured character in the SOP viewport. Off is plain grey. |
| **Textured** | Which material groups draw textured: Body, Eyes, Teeth, Clothing & Accessories. |
| **Hair** | Off, Opaque Cards or Transparent Cards. |

### Motion Clips

| Parameter | What it does |
|---|---|
| **Play Clip** | The clip the rig plays: the character's own, or a baked clip file. The playback range follows. |
| **Clip #** | An animation clip file to bake onto the rig. |
| **Frames** / **to** | First and last frame of the clip to bake (0 means from the start / to the end). |
| **Start** / **End** | Reset the start or end frame to the clip's own. |
| **Update Motion Clips** | Bakes the listed clips onto the rig without rebuilding it. |
| **Clear Motion Clips** | Empties the list and updates in one step. Asks first. |

### Face Tools

| Parameter | What it does |
|---|---|
| **Face Key Muscle** | Opens Character Creator's Muscle mode for this character. |
| **Record** | Records a Face Puppet take as keys. |
| **Preview** | Tries a Face Puppet profile with the mouse, without recording. |
| **Record Mode** | Replace or Blend: what a take does to the animation already there. |
| **Record to New Layer** | Puts each take on an animation layer of its own. On by default. |

### Face Tools ▸ Recording Settings

| Parameter | What it does |
|---|---|
| **Preroll** | Seconds counted down before a take starts. |
| **Record Speed** | How fast the playbar runs while recording. 1 is real time. |
| **Mouse Range** | Pixels of mouse travel for a full deflection of the pad. |
| **Smoothing** | Frames of smoothing on the recorded mouse path. |
| **Return to Start** | Puts the playhead back where the take started. |
| **Show Controls While Recording** | Keeps the rig's controls drawn while a take plays. |

### Auto Animation

| Parameter | What it does |
|---|---|
| **Profile** (Auto Blink) | Normal, Nervous, Speechless, Charming or Child. |
| **Clip Blinks** | Keep or Replace the blinks already in the animation. |
| **Seed** | A different pattern of blinks with the same profile. |
| **Frame Range** | The frames to blink over. Follows the playback range until you type your own. |
| **Add Auto Blink** | Keys blinks onto a layer of their own. |
| **Profile** (Auto Breathe) | Calm, Normal, Heavy or Sleeping. |
| **Depth** | How deep the breaths are. 1 is the profile as it comes. |
| **Seed** | A different rhythm with the same profile. |
| **Frame Range** | The frames to breathe over. |
| **Add Auto Breathe** | Keys breaths onto an additive layer of its own. |

### Rig Settings

| Parameter | What it does |
|---|---|
| **Hair Follows Head Only** | On: every hair mesh follows the head only. Off: Character Creator's own skinning. |
| **Stash Rig** | On: the built and baked rig is stored. Off: it is dropped and rebuilt live. |
| **Stash In** | Inside the Hip or External File. Changing it writes nothing. |
| **Geometry File** | The file **Save to Disk** writes the rig to and the rig reads from. |
| **Save to Disk** | Writes the rig and its baked clips to files and reads them from there. |
