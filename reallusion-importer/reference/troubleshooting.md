# Troubleshooting & FAQ

Common issues and their fixes. Most import problems trace back to either an export setting or a moved file.

## The character is grey / has no textures

**Cause:** the tool can't find the texture folder.

**Fix:** make sure the `textures` folder (and the `.fbm` folder) sit right next to the FBX, exactly as Character Creator exported them. If you moved the FBX, move its texture folders with it. The tool resolves textures relative to the FBX file.

**If you transferred the export between machines through Google Drive (or another cloud download):** check that you got _all_ of it. Google Drive splits large folder downloads into **multiple zip parts** — extracting only one part leaves the folder structure looking perfectly intact while half the texture files are silently missing, and the character builds white. Extract every part into the same folder, then rebuild. The tool prints a console warning naming any materials it couldn't find a diffuse texture for — if you see it, count your zip parts.

## Accessories are plain white, or no displacement appears

**Cause:** your export is missing its material `.json` file. Character Creator stores displacement, subsurface, wrinkle weights, and the colors of custom accessories (horns, props, GoZ clothing) in a `my_character.json` beside the FBX — not in the FBX itself. If it's absent, the tool has no displacement data (so no displacement nodes are built) and no color for untextured accessories (so they render white). The rest of the character can still look fine, which makes this easy to miss.

**Fix:** make sure a `my_character.json` sits next to your FBX. It's created by Character Creator's **Export JSON for Auto Material Setup** option, which is on by default — if you don't have one, that option was off, so re-export with it enabled. Keep the `.json` with the FBX when moving files. See [Preparing Your Character](../getting-started/preparing-your-character.md). (Note: this is unrelated to the Embed Textures setting — leave that off.)

## Wrinkles don't animate

**Cause:** almost always the **Bake Wrinkles for Still Frame** export setting was left on.

**Fix:** re-export from Character Creator with **Bake Wrinkles for Still Frame turned OFF**. See [Preparing Your Character](../getting-started/preparing-your-character.md). With it on, the wrinkles are frozen into one pose and can't react to animation.

You can confirm wrinkles are working by clicking **Go to Max Wrinkle Frame** in the Wrinkles folder — it jumps to the most expressive frame so you can see them.

## Nothing happens when I click Build Character

**Cause:** no FBX is set, or the path doesn't exist.

**Fix:** set a valid FBX path on the **CC5/iClone FBX** field, then click Build Character. The tool will warn you if the path is empty or missing.

## The hair recolor controls don't do anything

**Cause:** your character's hair doesn't carry Character Creator's hair maps (root/ID/flow), so there's nothing for the recolor system to work with — it stays on the baked color.

**Fix:** this is expected for hairstyles that bake everything into a flat diffuse, and for caps and some brows/lashes. The hair will still look correct; it just can't be re-dyed. Hair that _does_ carry the maps (most styled scalp hair) will recolor normally. See [Hair](../using/hair.md).

## A control I changed didn't update the render

**Cause:** a few controls — **SSS Quality** and the **eye-light controls** (Eyes Cast Light, Light Quality, Light Intensity) — are Karma render properties, which Karma reads only when a render starts.

**Fix:** restart your Karma render after changing these. Every other control updates live.

## Displacement looks like it's exploding / cracking

**Cause:** displacement strength too high.

**Fix:** lower the **Displacement Strength** — these maps are sensitive, and values around 0.002 are typical. See [Displacement](../using/displacement.md).

## Houdini runs out of memory

**Cause:** character data and animation clips are memory-heavy.

**Fix:** remove animation clips you're not using, clear the scene cache, and work with one character at a time on a tight memory budget. See [Performance & Caching](performance.md).

## My render looks noisy in the soft skin areas

**Cause:** subsurface scattering needs more samples.

**Fix:** raise **SSS Quality** in the Skin folder (and restart the render, since it's a render property). Make sure you're in Production quality, not Preview.

## Clothing or an accessory pokes through the body

**Cause:** Character Creator outfits don't always sit perfectly on every body.

**Fix:** use **Skin Fix** (the **Skin-Fix** folder → **Create Skin-Fix Setup**). Double-click into the gold subnetwork and brush the green **Sculpt** / **Soft Edit** nodes to push the body in (or the garment out), then turn on **Use Skin-Fix Mesh**. Move points only — don't add, delete, or change the mesh's point count, and only touch the green nodes. See [Skin Fix](../using/skin-fix.md).

## A small element (usually facial hair) breaks up or mangles during animation

**Cause:** in rare cases Character Creator double-, triple-, or quadruple-exports the blendshape targets for a particular element. The duplicated targets fight each other once the face animates, and that element tears apart. It most often hits parts of facial hair.

**Fix:** use the **Fix Broken Blendshape** folder on the Reallusion Importer node. Put the offending element into **Broken Elements** as an `@name` group (the `@name` attribute of that mesh), then turn on **Fix Broken Blendshape**. That element is now excluded from the character's blendshape deform and instead point-deformed by the nearest face/body geometry, so it follows the animation cleanly. If you see deforming artifacts on the fixed element, adjust the **Radius**. Leave this off unless you actually have a broken element — with no element specified, the toggle would bypass the whole mesh.

## Can I use this in a commercial studio pipeline?

The tool is a limited-commercial (Indie) asset. Loading it into a commercial Houdini session switches that session to limited-commercial mode, per SideFX's rules. If that's a problem for your pipeline, this tool may not fit it. You are responsible for your own SideFX license compliance. See [Requirements & Installation](../getting-started/installation.md).

## My eyes don't look like they did in Character Creator

This is expected. Character Creator's HD eye shader bakes very little of its look into the export, so the eye imports with a neutral base color. Use the tool's eye controls (Iris Color Tint, Iris Scale, Limbus, Eye Shadow, Eye Glossiness) to rebuild the look in Houdini. Some aspects (true iris depth/parallax, pupil resize) can't be reproduced at all because the data isn't exported. See [Limitations & Expectations](limitations.md) and [Eyes](../using/eyes.md).

## A control does nothing on my character

Many features are character-dependent — they only work if your character's export carries the data they need (hair maps, tear-line mesh, wrinkle maps, displacement maps). If a control seems inert, your character likely doesn't have that data. This is expected behavior, not a bug. See [Limitations & Expectations](limitations.md).

## Still stuck?

If something isn't covered here, reach out through the official [JVtools Discord](https://discord.gg/fKYDHcHdZ).
