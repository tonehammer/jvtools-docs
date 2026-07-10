---
icon: alert
order: 100
---

# Limitations & Expectations

This page is here to set honest expectations before and after you buy. The tool does a lot, but Character Creator's FBX export — and Houdini itself — impose some hard limits that no importer can work around. Reading this will save you frustration and help you judge whether the tool fits your pipeline.

Most of these fall into three buckets: **what Character Creator doesn't export**, **what varies from character to character**, and **how Houdini behaves**. A couple have fixes planned (see the roadmap notes).

## Memory (the big one, READ BEFORE BUYING)

!!!danger
**Character Creator characters are memory-heavy in Houdini when imported via FBX.** A fully-featured HD character can use **20–40 GB of RAM**, and each added animation clip adds several gigabytes more. Plan for **48 GB minimum** (for simpler characters)**, 64 GB recommended**.
!!!

!!!success USD import dramatically reduces this
The figures above are for **FBX import**. Version 1.2's **USD import mode** (now the default) keeps the facial blendshapes sparse, cutting import memory by roughly **10–14×** and import time by **50–75×** — a heavy character that needs 20–40 GB via FBX imports in about a second at a fraction of the RAM. **If memory is a concern, export and import as USD.** See [USD vs FBX](../getting-started/import-modes.md). The FBX figures still apply when you specifically need FBX-only features (wrinkles, root-to-tip/highlight hair re-dye).
!!!

This isn't a flaw in the tool — it's how Houdini expands **FBX** character data (especially the facial blendshapes) into memory on import. The tool includes geometry-caching and memory-reclaim utilities to help you manage it, but they can't change the underlying footprint (USD import sidesteps it instead).

**Animation is the biggest memory driver of all.** A clip's cost scales with its frame-length, because Houdini holds the expanded character for every frame in the range — so a long, multi-thousand-frame clip can use far more RAM than the static character. Keep your animation frame-ranges to what you actually need. See [Performance & Caching](performance.md).

If you're on 16 GB or less, expect to struggle with HD characters or animation. See [Performance & Caching](performance.md) for strategies. Recommended 64+ GB.

!!!success This is largely solved in 1.2
The USD-based character import mentioned as a plan in earlier versions **shipped in Version 1.2** and is now the default — it's the biggest single reduction in this memory footprint. Import as USD to get it. (A deeper USD-native rebuild remains on the longer-term roadmap.)
!!!

## The eyes

This is the most important section to understand, because the eyes are where Character Creator's export is least complete.

Character Creator's premium "Digital Human" / HD eye has a rich shader with many controls — iris color, iris and pupil scale, limbal ring, iris depth/parallax, sclera shading, cornea wetness, and more. **Almost none of that is baked into the exported FBX or its texture data.** The export carries a neutral base iris texture and standard PBR maps; the rest of the eye's look lives only inside Character Creator and does not travel with the file.

!!!warning
**Don't rely on heavy eye customization in Character Creator carrying over.** If you carefully dial in iris color, depth, and shading in CC, the exported character will _not_ look the same in Houdini — that detail isn't in the file. Treat the CC eye look as a reference, not something that transfers.
!!!

**What the tool reproduces** (faked convincingly on the imported eye): iris color tint, iris scale, the limbal ring, eyelid contact shadow, and overall eye glossiness/wetness. These give you strong art-directable control over the eye look — see [Eyes](../using/eyes.md).

**What the tool cannot reproduce** (the source data isn't exported): true iris depth and parallax (the deep "looking into the eye" effect), pupil resizing, and Character Creator's layered cornea/wetness shading. These can only be approximated, never matched, because the information needed to build them faithfully never leaves Character Creator.

The practical takeaway: **set your eye look in Houdini using the tool's eye controls, not by trying to match a CC render.**

## Character-dependent features

Several features depend on what your specific character and its export actually contain. The tool detects what's present and enables those features automatically — so if a control seems to do nothing, the most likely reason is that your character doesn't carry the data that feature needs. This is normal and expected.

* **Hair re-dye** needs the character's hair to carry Character Creator's hair maps (root, ID, flow). Most styled scalp hair does; some hairstyles, caps, and simpler hair bake everything into a flat texture and can't be re-dyed (they still import and look correct). See [Hair](../using/hair.md).
* **Tear-line wetness** needs the character to export a tear-line mesh. Some characters have one, some don't — it varies by base mesh and export. The tool's overall **Eye Glossiness** control works on every character regardless, so you always have a wet-eye lever. See [Eyes](../using/eyes.md).
* **Wrinkles** need the character's expression-wrinkle maps (most CC heads have them).
* **Displacement** needs exported displacement maps.

None of these are bugs — they reflect what each character's export provides. When in doubt, a feature that "doesn't do anything" usually means the underlying maps aren't in that particular character.

## UDIM (multi-tile) textures

Standard Character Creator characters use a single UV tile per material, which the tool handles normally. Characters authored with **UDIM / multi-tile textures** — an advanced setup, uncommon on stock CC base meshes — are **not currently supported**: the tool resolves one texture per channel, so only a single tile would load. If you work with UDIM characters, flatten them to a single 0–1 tile before export. Most users will never run into this.

## Animation

A motion clip carries the skeleton and proportions of its source character. Clips made for _this_ character play back directly; for a clip from a **differently-proportioned** Character Creator character, turn on **Retarget Animation** to remap it onto your character (see [Animation](../using/animation.md#retarget-animation)).

!!!info
**Retargeting works between Character Creator characters** — it relies on the shared CC skeleton and blendshape set, so the facial performance (expressions, visemes, blinks) carries over too. Retargeting non-CC motion (e.g. mocap on a foreign skeleton) is outside the tool's scope.
!!!

## Render-property controls (need a render restart)

A few controls — **SSS Quality** and the **eye-light controls** (Eyes Cast Light, Light Quality, Light Intensity) — are Karma _render properties_, which Karma reads only when a render begins. Changing them requires restarting your Karma render to take effect. This is inherent Karma behavior, not a tool limitation. Every other control updates live. These controls note this in their tooltips and on their documentation pages.

## Platform

The tool was developed and tested on **Windows**, with **Houdini 21+**. macOS and Linux are untested. The materials are built and tuned for **Karma XPU** and also render in **Karma CPU** — XPU is the recommended path for the look and speed they were designed around, but CPU is a supported fallback. See [Requirements & Installation](../getting-started/installation.md).

## Mesh fixes (Skin Fix)

**Skin Fix** is for quick, point-level cleanup of mesh intersections (clothing poking through the body) — you move points, you don't change the mesh. Adding, deleting, or re-topologising geometry will break the character downstream, so it's intentionally constrained to nudging existing points. It's best for body and clothing; edits in face regions can be partially overridden by the blendshapes (those targets are defined against the original rest shape). For anything beyond quick fixes, do the work in Character Creator/ZBrush and re-export. See [Skin Fix](../using/skin-fix.md).

## In short

The tool is built to get you from a Character Creator export to a beautiful, art-directable Houdini character fast. Where Character Creator's export is complete, it reproduces the look faithfully. Where the export is partial (most notably the eyes), it gives you strong controls to rebuild the look in Houdini — which is the right workflow anyway. The honest line: **use the tool's controls to author your look in Houdini, rather than expecting a 1:1 copy of the Character Creator viewport.**
