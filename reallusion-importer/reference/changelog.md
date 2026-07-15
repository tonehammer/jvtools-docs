---
icon: history
order: 70
---

# Changelog

## Version 1.2.1

* **Fixed:** textures now load for iClone "Export USD (Omniverse)" characters, whose texture folders are laid out differently from Character Creator's USD export.
* Added dedicated Character Creator **FBX** and **USD** export walkthroughs, and a new **iClone** export section — including how to bring iClone-authored motion into Houdini (an FBX round-trip through Character Creator, or the NVIDIA Omniverse plugin). Note: iClone's direct USD export is experimental — standard characters work, stylized ones may not.
* Documented the **best-quality workflow**: an FBX-imported character driven by lightweight USD motion clips, so you keep the expression wrinkles while the animation stays light.
* Refreshed in-app tooltips and help that still referred only to FBX now that USD import is supported.
* Bug fixes and improvements.

## Version 1.2

**USD import mode**

* **New USD import path.** A new **Import** dropdown at the top of the node lets you import Character Creator's **Export USD (Omniverse)** output instead of FBX. USD import is **dramatically faster and lighter on memory** — around 50–75× faster, with the gap widening on heavier characters — and is now the **default** mode. FBX import is unchanged and still available. See [USD vs FBX](../getting-started/import-modes.md).
* **Sparse facial deformation in USD mode.** The facial blendshapes now stay sparse through deformation instead of being expanded into memory — only the expressions active on the current frame are computed. The heaviest HD characters drop from **~26 GB to under 3 GB** of working RAM, identical results. With this, **16 GB of RAM works for standard characters and 32 GB covers HD** in USD mode (FBX mode keeps its previous requirements).
* **Real Character Creator eye & skin values.** In USD mode the tool reads Character Creator's actual shader values and seeds the lookdev controller with them automatically — real iris color, iris size, limbal ring, sclera shading, and subsurface amount — instead of the generic starting points the FBX export forces. Reset to Defaults returns to these real values in USD mode.
* **Honest feature gating.** Character Creator's USD export omits the data behind **expression wrinkles** and the **root-to-tip / highlight hair re-dye**, so those controls are clearly disabled with an "(FBX import only)" note in USD mode. Flat hair re-dye, the Lightness (Bleach) control, displacement, and everything else work in both modes.
* **Animation database accepts USD motion clips.** Add Animation now also takes the `Motions/*.usd` clips Character Creator writes beside a USD export — they load instantly and use a fraction of an FBX clip's RAM. FBX and USD clips mix freely in one database and work in either import mode; USD clips can even drive an FBX-imported character, keeping expression wrinkles working from featherweight clips. **Retarget Animation** now engages automatically when a clip's format differs from the import mode.
* **Cross-character clips no longer break characters with accessory bones.** A clip from a character without this character's hair/accessory rig used to explode those parts; they now follow along rigidly (hair rides the head).
* Scenes saved before 1.2 open in FBX mode automatically — existing work is unaffected.
* Bug fixes and improvements.

## Version 1.1

* **Documentation moved to the new JVtools docs site** (the one you're reading now).
* **In-app update check.** The asset now checks for a newer version when you build a character and shows an unobtrusive notice if one is available — so you never miss an update. A version label on the node shows which version you have.
* Bug fixes and improvements.

## Version 1.0

The first public release.

**Materials**

* Karma MaterialX materials for skin, eyes, teeth, hair, and clothing — tuned for Karma XPU, also render in Karma CPU
* Physically-based skin with subsurface scattering, normal detail, and roughness controls
* SSS Color, Amount, Radius, and Quality controls to balance lifelike scatter against skin detail
* Skin Re-tint: shift overall skin tone (warmer/cooler, tan, pale) live, across all skin, without re-exporting from Character Creator
* Teeth controls (Brightness, Roughness, Specular, SSS Amount) to tame Character Creator's over-bright, glary teeth — grouped in a Teeth sub-folder inside Skin
* Refractive ray-traced corneas (Hero Eyes) with a fast cutout fallback
* Dielectric clothing/accessory handling (ignores Character Creator's junk metallic maps by default)

**Wrinkles**

* Expression-driven head wrinkle system reconstructed live in Karma
* Per-channel control over wrinkle relief, color, and roughness
* "Go to Max Wrinkle Frame" helper to find the most expressive frame

**Hair**

* Full hair re-dye system: root-to-tip ombré and ID-based highlight streaks
* Luminance-preserving recolor that keeps strand detail intact
* Lightness (Bleach) control to lift dark hair lighter — turn a brown- or black-haired character blonde/platinum, not just recolor them
* Specular-mask control to tame over-bright highlights
* Flow-map-driven anisotropic sheen for realistic directional hair highlights
* Independent eyebrow tinting (Brows sub-folder) to match dyed hair

**Eyes**

* Iris color tint, iris scale, and limbal ring — reproducing Character Creator's HD eye look (which isn't baked into the export)
* Sclera tinting for subtle realism pushes or fully stylized colored eyes
* Eyelid contact shadow, faked on the occlusion mesh with a top bias
* Overall eye glossiness/wetness control (works on every character)
* Tear-line wetness controls for characters that ship a tear-line mesh
* Separate eyeball normal strength
* Stylized eye glow with several modes (flat, texture, multiply, iris circle, iris dot)
* Eyes-as-light-source — glowing eyes illuminate the scene
* Controls organized into Iris / Limbus / Sclera / Eye Shadow / Wetness tabs

**Displacement**

* Per-character displacement: bump or true displacement
* Adjustable displacement strength

**Animation**

* Animation database: add, select, and remove FBX motion clips
* Embedded-animation and database sources
* Retarget Animation: drive a character with a clip authored on a differently-proportioned Character Creator character — body proportions matched, teeth/tongue/eyes kept seated, and facial expressions/visemes/blinks carried over automatically
* Separate Body and Facial animation sources: drive the body from one clip and the face from another (Embedded / Animation Database), or bypass the face entirely — keep this character's own facial performance on a borrowed body clip, with retargeting engaged automatically when the sources differ

**Fixes & workarounds**

* Fix Broken Blendshape: excludes elements affected by Character Creator's rare duplicate-blendshape export glitch and point-deforms them cleanly
* Skin Fix: an editable subnetwork with ready-to-use Sculpt and Soft Edit tools for quickly fixing mesh intersections (clothing poking through the body) before skinning — blendshape data is separated out and merged back automatically

**Rendering & Setup**

* Optional one-click three-point light rig, camera, and Karma XPU render settings
* Lookdev controller gathering all look controls on one node
* Reset to Defaults button to return every lookdev control to its original value in one click
* Quality presets (Preview / Production) for fast look-dev

**Utilities**

* Geometry caching and a scene-cache reclaim utility
* Navigation buttons and quick links to documentation and community

---

!!!info
Future updates and their changes will be listed here. **All future updates to this product are included with your purchase** — check back after updating the asset to see what's new.
!!!
