# Parameter Reference

Three panels, three tables: the **Reallusion Rigger** node (in SOPs), the **Reallusion Rigger APEX Rig** node (the rig), and the lookdev controller (a red node in LOPs, created by **Build Character** and reached with **Go to LOPs**). Labels are exactly as they appear on the node.

!!!info
Hovering any parameter in Houdini shows its tooltip, which is the authoritative, always-current description. If this page and a tooltip ever disagree, trust the tooltip.
!!!

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

### Rig Settings

| Parameter | What it does |
|---|---|
| **Hair Follows Head Only** | On: every hair mesh follows the head only. Off: Character Creator's own skinning. |
| **Stash Rig** | On: the built and baked rig is stored. Off: it is dropped and rebuilt live. |
| **Stash In** | Inside the Hip or External File. Changing it writes nothing. |
| **Geometry File** | The file **Save to Disk** writes the rig to and the rig reads from. |
| **Save to Disk** | Writes the rig and its baked clips to files and reads them from there. |

### Motion Clips

| Parameter | What it does |
|---|---|
| **Play Clip** | The clip the rig plays: the character's own, or a baked clip file. The playback range follows. |
| **Clip #** | An animation clip file to bake onto the rig. |
| **Frames** / **to** | First and last frame of the clip to bake (0 means from the start / to the end). |
| **Start** / **End** | Reset the start or end frame to the clip's own. |
| **Update Motion Clips** | Bakes the listed clips onto the rig without rebuilding it. |
| **Clear Motion Clips** | Empties the list and updates in one step. Asks first. |

### Face Tools ▸ Face Key Muscle

| Parameter | What it does |
|---|---|
| **Open Face Key Muscle** | Opens the Face Key Muscle pane, Character Creator's Muscle mode for this character: a drawing of the face with its regions. |
| **Record** | Records the picked regions over time as keys, on a FaceKeyMuscle layer. |
| **Preview** | Tries the picked regions with the mouse, without recording. |

### Face Tools ▸ Face Key Muscle ▸ Face Key Muscle Settings

| Parameter | What it does |
|---|---|
| **Symmetric** | A picked region brings its other side along. |
| **Key** | Which channels a drag keys at the frame: Moved Channels or Whole Face. |
| **Ease In** | Frames before the current frame over which each edit fades in. |
| **Ease Out** | Frames after the current frame over which each edit fades out. Follows Ease In until you set it. |
| **Expressiveness** | How far a drag can push a shape: 1 is Character Creator's full shape, 2 twice that. |
| **Drag Range** | Pixels of drag on the drawing for a full shape. Lower is more sensitive. |

### Face Tools ▸ Face Puppet

| Parameter | What it does |
|---|---|
| **Record** | Records a Face Puppet take as keys. |
| **Preview** | Tries a Face Puppet profile with the mouse, without recording. |

### Face Tools ▸ Recording Settings

| Parameter | What it does |
|---|---|
| **Record Mode** | Replace or Blend: what a take, from either Record, does to the animation already there. |
| **Record to New Layer** | Puts each take on an animation layer of its own. On by default. |
| **Preroll** | Seconds counted down before a take starts. |
| **Record Speed** | How fast the playbar runs while recording. 1 is real time. |
| **Mouse Range** | Pixels of mouse travel for a full deflection of the pad (a full shape on a Face Key Muscle take). |
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
| **Target** (Look At) | The camera, object or SOP node the eyes look at. |
| **Group** | For a SOP Target, the points whose centre the eyes aim at. Empty aims at the whole geometry. |
| **Offset** | Moves the aim point in the Target's own frame. |
| **Transition** | Frames to turn onto the Target and back. 0 switches at once. |
| **Frame Range** | The frames to look at the Target. |
| **Bake Look At Target** | Keys the Look At target onto the Target over the frame range, on a layer of its own. |

## Lookdev controller (LOPs)

**Build Character** creates a red controller node in the LOP network hosting all look controls. Material expressions reference it, so adjusting a control updates the Karma render **live** — except the render-property controls noted below, which need the render restarted. See [The Lookdev Controller](../lookdev/lookdev-controller.md).

Two buttons sit at the top: **Go to SOPs** jumps back to the Reallusion Rigger node, and **Reset to Defaults** returns every control on the controller to its original value (after a confirmation prompt).

### Quality

| Parameter | Description |
| --- | --- |
| **Quality** | Preset that sets the two toggles below. *Preview* turns subsurface off and uses cheap cutout corneas for fast look-dev; *Production* restores full quality. |
| **Light Setup** | Switches the light rig built by **Create Render Setup** between *Cinematic* (warm, moody key) and *Neutral* (flat, even). Only affects that rig. |
| **Remove SSS** | Disables subsurface scattering on skin and teeth — the single biggest render-time saving. |
| **Hero Eyes** | Refractive ray-traced corneas for close-up realism. Off uses a cheaper cutout cornea for distant or background characters. |

### Skin

See [Skin](../lookdev/skin.md).

| Parameter | Description |
| --- | --- |
| **Skin Normal Strength** | Intensity of the base skin normal map (pore and surface detail). |
| **Skin Roughness** | Multiplier on skin roughness. Below 1 = glossier and more lifelike; above 1 = more matte. |
| **Diffuse Contrast** | Contrast of the skin color texture around mid-grey. Very sensitive — useful range roughly 1.0–1.1. |
| **Respect Metallic Maps** | Honor Character Creator's metallic textures on teeth, tongue, and clothing. Off by default (these are dielectric and CC's metallic maps on them are usually junk). |

**Skin Re-tint** (sub-folder)

| Parameter | Description |
| --- | --- |
| **Skin Re-tint Color** | The color the skin diffuse is tinted toward. White (default) is a no-op. Affects diffuse only, across all skin. |
| **Skin Re-tint Amount** | How strongly the re-tint color is applied. 0 = untouched; 1 = full multiply. Caps at 3 but accepts higher typed values for an overdriven push. |
| **Skip Nails** | Exclude the fingernail/toenail material from the re-tint. Off by default. |

**Teeth** (sub-folder)

| Parameter | Description |
| --- | --- |
| **Teeth Brightness** | Overall brightness of the teeth/tongue diffuse. Pull below 1 for more natural teeth (CC exports them near-white). 1 = as exported. |
| **Teeth Roughness** | Multiplier on teeth/tongue roughness. Raise above 1 to soften a glary specular; below 1 for a wetter look. |
| **Teeth Specular** | Strength of the wet specular reflection on teeth/tongue. Lower it to reduce blown-out catchlights. |
| **Teeth SSS Amount** | Subsurface scattering on teeth/tongue only. Lower it to make teeth read more solid. Disabled when Remove SSS is on. |

**Subsurface** (sub-folder — disabled when Remove SSS is on)

| Parameter | Description |
| --- | --- |
| **SSS Color** | Per-channel scatter falloff color. Default a warm skin tone; cooler = bluer scatter, warmer = redder. Applies to skin and teeth. |
| **SSS Amount** | How much subsurface scattering skin and teeth receive. 1 = full lifelike scatter; lower recovers surface detail; 0 = none. |
| **SSS Radius** | How deep light scatters. Higher = softer and more translucent but washes out detail. |
| **SSS Quality** | Subsurface ray limit (higher = cleaner and slower). A Karma **render property** — a change may only take effect after restarting the render. |

**Wrinkles** *(FBX import only)*

See [Wrinkles](../lookdev/wrinkles.md).

| Parameter | Description |
| --- | --- |
| **Wrinkle Strength** | Master intensity of all wrinkle channels. 0 disables wrinkles; 1 is as authored. |
| **Normal / Diffuse / Roughness Strength** | Per-channel trims on top of the master strength (relief, crease darkening, sheen). |

**Displacement**

See [Displacement](../lookdev/displacement.md).

| Parameter | Description |
| --- | --- |
| **Mode** | How displacement maps render: **Bump** (cheap), **True Displacement** (real geometry, needs subdivision, slower), or **Disable**. Only matters for characters exported with displacement maps. |
| **Displacement Strength** | Scale of the displacement effect. Small values (~0.002) are typical. |

### Eyes

Rebuilds Character Creator's HD eye look, which barely travels in the export. Organized into Iris / Limbus / Sclera / Eye Shadow / Wetness tabs, with Glow below. See [Eyes](../lookdev/eyes.md).

| Parameter | Description |
| --- | --- |
| **Eye Normal Strength** | Eyeball surface detail (sclera veins, iris relief), separate from the head. Low by default (0.2) — CC's eye normal is strong. |
| **Lightness** | Lifts the brightness of the whole eye, applied after the iris tint, limbus and sclera. 1 = unchanged; above 1 brightens (slider to 5, accepts higher); below 1 darkens. Raise this when a dark iris won't take a tint. Both import modes. |

**Iris tab**

| Parameter | Description |
| --- | --- |
| **Iris Color Tint** / **Iris Tint Amount** | Reproduce CC's iris color (masked to the iris, so the sclera stays white). Amount can exceed 1 to over-saturate. |
| **Iris Scale** | Resizes the iris. |
| **Iris Tint Radius** / **Iris Tint Feather** | Size and soften the tint disc. |

**Limbus tab**

| Parameter | Description |
| --- | --- |
| **Limbus Color / Width / Scale / Strength / Feather** | The dark ring at the iris/sclera edge. Strength 0 by default (a little reads as depth); Width and Feather set thickness and edge softness; Scale fits the ring to the iris. |

**Sclera tab**

| Parameter | Description |
| --- | --- |
| **Sclera Color** / **Sclera Tint Amount** | Tint the white of the eye. Amount 0 by default; the tint is the exact inverse of the iris mask, so the iris is never affected. |

**Eye Shadow tab**

| Parameter | Description |
| --- | --- |
| **Color / Strength / Radius / Feather** | The eyelid contact shadow on the eyeball (top-biased). Strength 0 by default; bigger Radius reaches further in. |

**Wetness tab**

| Parameter | Description |
| --- | --- |
| **Eye Glossiness** | Overall eyeball shine/wetness. Works on every character (try 1.2–2 for a wet look). |
| **Tearline Gloss / Presence / Ripple** | The wet lid rim — only on characters that ship a tear-line mesh (no effect otherwise; use Eye Glossiness instead). Gloss is roughness, Presence scales the reflection, Ripple adds micro wet-bump detail. |

**Glow**

| Parameter | Description |
| --- | --- |
| **Glow Mode** | Stylized eye emission: *Flat Color*, *Use Eye Texture*, *Multiply with Texture*, *Iris (Circle)*, *Iris (Dot)*. None by default. |
| **Eyes Cast Light** | Treats the glowing eyes as a light source that illuminates nearby surfaces. A Karma **render property** — this and the two controls below may only take effect after restarting the render. |
| **Light Quality / Light Intensity** | Sampling quality of the eye light (reduces noise) and how strongly the eyes light their surroundings. |
| **Glow Strength / Glow Color** | Brightness and color for the Flat, Texture, and Multiply modes. |
| **Iris Color** | Color of the iris glow for both Iris modes. |
| **Iris Strength / Iris Radius / Iris Feather** | Per-mode brightness, disc size, and (Dot) edge softness for the Iris modes. |

### Hair

Re-dye and shade the character's scalp hair. Applies to hair carrying CC's hair maps (root, ID, flow); simpler hair and caps keep their baked color. See [Hair](../lookdev/hair.md).

| Parameter | Description |
| --- | --- |
| **Hair Color Mode** | *Baked (CC)* keeps the exported hair color; *Custom* re-dyes from the controls below, keeping strand detail. |
| **Root Color** / **Tip Color** | The roots-to-tips ombré gradient in Custom mode. *(FBX import only — USD mode does a flat re-dye from Root Color.)* |
| **Lightness (Bleach)** | Lightens or bleaches the hair, in **both** Baked and Custom modes. 1 = unchanged; above 1 bleaches toward light/blonde (slider to 20, accepts higher); below 1 darkens. |
| **Highlight Color** / **Highlight Amount** | A second color blended into highlighted strands (balayage/streaks) and how strongly it shows. 0 disables highlights. *(FBX import only.)* |
| **Controlled Specular Highlights** | Uses the hair's specular mask to restrain over-exposed highlights (CC's intended look). Off gives full specular. |
| **Hair Anisotropy** | Stretches the specular highlight along the strands (directional hair sheen), steered by the flow map. 0 is off. *(FBX import only.)* |

**Brows** (sub-folder)

| Parameter | Description |
| --- | --- |
| **Brow Lightness** | Lifts the brows' brightness. 1 = unchanged; slider to 20, accepts higher. Applies at any tint amount, including 0. CC's brow maps are near-black, so raise this first or a tint reads as doing nothing — 6–14 is the usual working range. |
| **Brow Tint Color** / **Brow Tint Amount** | Re-tint the eyebrows, keeping strand detail. Amount 0 by default. Use to match brows to dyed hair. Note brows also run through the scalp re-dye, so Custom mode reaches them and these controls layer on top. |

**Facial Hair** (sub-folder)

Beards, moustaches and sideburns. Decoupled from the scalp hair — the Hair color controls above do not touch them. See [Hair](../lookdev/hair.md#facial-hair).

| Parameter | Description |
| --- | --- |
| **Facial Hair Lightness** | Lifts the beard's brightness. 1 = unchanged; slider to 20, accepts higher. Applies at any tint amount, including 0 — this alone greys or lightens a beard. Blows out from around 4x. |
| **Facial Hair Tint Color** / **Facial Hair Tint Amount** | Re-tint facial hair, keeping strand detail. Amount 0 by default. CC names every piece `Beard1`, `Beard2` and so on, so moustaches, sideburns and soul patches all follow these. |
