---
icon: sliders
order: 110
---

# Parameter Reference

Every control on the Reallusion Importer, grouped by where you find it. There are two panels:

* **The Reallusion Importer node** (in SOPs) — import, build, animation, and utility controls.
* **The Lookdev Controller** (a red node in LOPs, created by **Build Character** and reached with **Go to LOPs**) — every look control for skin, eyes, hair, wrinkles, and displacement.

Each section links to the fuller walkthrough in [Using the Asset](../using/).

!!!info
Hovering any parameter in Houdini shows its tooltip, which is the authoritative, always-current description. If this page and a tooltip ever disagree, trust the tooltip.
!!!

---

## On the Reallusion Importer node (SOPs)

### Import

| Parameter | Description |
| --- | --- |
| **Import** | Choose the source format: **USD** (Character Creator's "Export USD (Omniverse)" — fast, light, the default) or **FBX**. See [USD vs FBX](../getting-started/import-modes.md). |
| **USD File** / **FBX File** | Path to the character export to import. Keep the exported textures folder (and the `.json` sidecar, for FBX) beside the file when moving it. Which field shows depends on the Import mode. |
| **Go to LOPs** | Jumps to the LOP network and frames this character's lookdev controller. Build the character first. |

### Build

| Parameter | Description |
| --- | --- |
| **Create Render Setup** | When on, **Build Character** also creates a three-point light rig, a bust-framed camera, and a Karma XPU render settings node for an immediately renderable scene. Created once and not overwritten on rebuilds, so your light tweaks survive. See [Rendering](../using/rendering.md). |
| **Build Character** | Imports the character and generates everything: geometry, materials, displacement, the wrinkle system, and the lookdev controller. Your dialed-in controller values are preserved across rebuilds. |

### Fix Broken Blendshape

A workaround for a rare Character Creator export glitch that mangles certain elements (often facial hair) once animation plays. Only needed if you actually see an element breaking up.

| Parameter | Description |
| --- | --- |
| **Broken Elements** | The element(s) to exclude from the blendshape deform, entered as an `@name` group. Listed elements are point-deformed by the nearest face/body geometry instead. |
| **Fix Broken Blendshape** | Performs the bypass-to-point-deform. Off by default; enable only after specifying a Broken Element (with none picked it would bypass the entire mesh). |
| **Radius** | Point-deform capture radius for the bypassed elements. Adjust if you see deforming artifacts on the fixed element. |

### Skin Cache (recommended)

Caches the imported geometry to disk to avoid the slow FBX re-import on every session. *FBX mode only — hidden in USD mode, where import is already about a second.* See [Performance & Caching](performance.md).

| Parameter | Description |
| --- | --- |
| **Load from Disk** | Loads the cached geometry from disk instead of re-importing the FBX. Much faster for heavy characters. Enable after saving a cache. |
| **Reload Geometry** | Re-reads the cache from disk. Use after re-saving the cache for the same character. |
| **Save to Disk** | Writes the current character geometry to the cache file. Recommended for heavy/HD characters. Re-save if you re-export the character. |
| **Geometry File** | Disk location of the geometry cache (`.bgeo.sc`). The **FBX File** must stay set even with Load from Disk on — the skeleton and animation always read from the FBX. |

### Animation

Play the motion baked into the imported character, or a library of clips you add from other FBX / USD files. See [Animation](../using/animation.md).

| Parameter | Description |
| --- | --- |
| **Body Animation Source** | Which motion drives the **body** (skeleton): Embedded Animation, Animation Database (the active added clip), or No Animation (static pose). |
| **Facial Animation Source** | Where the **face** comes from, independent of the body: Embedded Animation, Animation Database, or Bypass Animation (calms the facial blendshapes). Mix a borrowed body clip with this character's own face. |
| **Add Animation** | Opens a file browser to add a motion clip (FBX or USD). The first clip creates the animation database subnet, switches the source to Animation Database, and makes the new clip active. |
| **Remove Animation** | Removes a chosen clip and frees its memory (also clears the scene cache). If the last clip is removed, the source falls back to Embedded. |
| **Select Animation** | Chooses which database clip plays, and switches the source to Animation Database. |
| **Current Animation** | Shows the name of the active database clip. Display only. |
| **Retarget Animation** | Off by default. Turn on for a clip authored on a **differently-proportioned** Character Creator character — it remaps the motion onto this character (proportions matched, teeth/tongue/eyes seated, facial performance carried over). Auto-engages when the facial and body sources differ, or when a clip's format differs from the import mode. |

### Skin Fix

Quick point-level fixes to mesh intersections (clothing poking through the body), in an editable subnetwork beside the node. See [Skin Fix](../using/skin-fix.md).

| Parameter | Description |
| --- | --- |
| **Create Skin-Fix Setup** | Creates (or jumps to) the skin-fix subnetwork. Inside, use the green **Sculpt** and **Soft Edit** nodes to push points where the body and clothing intersect. Move points only — don't add, delete, or change the point count. |
| **Use Skin Fix** | Switches the character onto the edited mesh. Off by default; safe to toggle even before a subnetwork exists (it falls back to the unedited mesh). |

### Utilities

| Parameter | Description |
| --- | --- |
| **Clear Scene Cache** | Unloads cached geometry from Houdini's caches to reclaim memory — useful after deleting characters or removing animations. Currently-displayed geometry won't unload (delete or bypass those nodes first). |
| **Documentation / Gumroad / Discord / YouTube** | Links out to the online documentation, the product page, the community Discord, and video tutorials. |

---

## On the Lookdev Controller (LOPs)

**Build Character** creates a red controller node in the LOP network hosting all look controls. Material expressions reference it, so adjusting a control updates the Karma render **live** — except the render-property controls noted below, which need the render restarted. See [The Lookdev Controller](../using/lookdev-controller.md).

Two buttons sit at the top: **Go to SOPs** jumps back to the Reallusion Importer node, and **Reset to Defaults** returns every control on the controller to its original value (after a confirmation prompt).

### Quality

| Parameter | Description |
| --- | --- |
| **Quality** | Preset that sets the two toggles below. *Preview* turns subsurface off and uses cheap cutout corneas for fast look-dev; *Production* restores full quality. |
| **Remove SSS** | Disables subsurface scattering on skin and teeth — the single biggest render-time saving. |
| **Hero Eyes** | Refractive ray-traced corneas for close-up realism. Off uses a cheaper cutout cornea for distant or background characters. |

### Skin

See [Skin](../using/skin.md).

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

See [Wrinkles](../using/wrinkles.md).

| Parameter | Description |
| --- | --- |
| **Wrinkle Strength** | Master intensity of all wrinkle channels. 0 disables wrinkles; 1 is as authored. |
| **Normal / Diffuse / Roughness Strength** | Per-channel trims on top of the master strength (relief, crease darkening, sheen). |

**Displacement**

See [Displacement](../using/displacement.md).

| Parameter | Description |
| --- | --- |
| **Mode** | How displacement maps render: **Bump** (cheap), **True Displacement** (real geometry, needs subdivision, slower), or **Disable**. Only matters for characters exported with displacement maps. |
| **Displacement Strength** | Scale of the displacement effect. Small values (~0.002) are typical. |

### Eyes

Rebuilds Character Creator's HD eye look, which barely travels in the export. Organized into Iris / Limbus / Sclera / Eye Shadow / Wetness tabs, with Glow below. See [Eyes](../using/eyes.md).

| Parameter | Description |
| --- | --- |
| **Eye Normal Strength** | Eyeball surface detail (sclera veins, iris relief), separate from the head. Low by default (0.2) — CC's eye normal is strong. |

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

Re-dye and shade the character's scalp hair. Applies to hair carrying CC's hair maps (root, ID, flow); simpler hair and caps keep their baked color. See [Hair](../using/hair.md).

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
| **Brow Tint Color** / **Brow Tint Amount** | Re-tint the eyebrows independently of scalp hair, keeping strand detail. Amount 0 by default. Use to match brows to dyed hair. |
