---
icon: history
order: 70
---

# Changelog

## Version 1.2.3

* **New: Eye "Lightness (Bleach)"** — brightens the final eye colour.
* **Create Skin-Fix Setup** now switches the Skin-Fix mesh on for you.
* Skin-Fix now reports its progress in the console during its first cook.
* **Fixed:** on FBX import, characters whose pieces share a texture no longer come in flat white.

## Version 1.2.2

* **Fixed:** on FBX import, characters whose pieces share a texture no longer come in flat white.
* Bug fixes and improvements.

## Version 1.2.1

* **Fixed:** textures now load for iClone "Export USD (Omniverse)" characters.
* Added Character Creator FBX and USD export walkthroughs, and an iClone export section.
* Documented the best-quality workflow.
* Refreshed tooltips and help that still referred only to FBX.
* Bug fixes and improvements.

## Version 1.2

**USD import mode**

* **New: USD import**, reading Character Creator's Export USD (Omniverse) output. Now the default mode.
* Sparse facial deformation in USD mode — the heaviest HD characters drop from ~26 GB to under 3 GB.
* Real Character Creator eye and skin values are read from the export and seeded into the lookdev controller.
* Controls the USD export cannot supply are disabled with an "(FBX import only)" note.
* The animation database now accepts USD motion clips.
* **Fixed:** cross-character clips no longer break characters with accessory bones.
* Scenes saved before 1.2 open in FBX mode.
* Bug fixes and improvements.

## Version 1.1

* Documentation moved to the JVtools docs site.
* **New: in-app update check**, plus a version label on the node.
* Bug fixes and improvements.

## Version 1.0

The first public release.

**Materials**

* Karma MaterialX materials for skin, eyes, teeth, hair and clothing.
* Physically-based skin with subsurface scattering, normal detail and roughness controls.
* SSS Color, Amount, Radius and Quality controls.
* Skin Re-tint across all skin, with no re-export from Character Creator.
* Teeth controls — Brightness, Roughness, Specular, SSS Amount.
* Refractive ray-traced corneas (Hero Eyes), with a fast cutout fallback.
* Dielectric clothing and accessory handling.

**Wrinkles**

* Expression-driven head wrinkle system, reconstructed live in Karma.
* Per-channel control over wrinkle relief, colour and roughness.
* "Go to Max Wrinkle Frame" helper.

**Hair**

* Hair re-dye: root-to-tip ombre and ID-based highlight streaks.
* Luminance-preserving recolour.
* Lightness (Bleach) control for lifting dark hair.
* Specular-mask control.
* Flow-map-driven anisotropic sheen.
* Independent eyebrow tinting.

**Eyes**

* Iris colour tint, iris scale and limbal ring.
* Sclera tinting.
* Eyelid contact shadow.
* Overall eye glossiness and wetness control.
* Tear-line wetness controls.
* Separate eyeball normal strength.
* Stylized eye glow with several modes.
* Eyes as a light source.
* Controls organized into Iris / Limbus / Sclera / Eye Shadow / Wetness tabs.

**Displacement**

* Per-character displacement — bump or true displacement.
* Adjustable displacement strength.

**Animation**

* Animation database — add, select and remove FBX motion clips.
* Embedded-animation and database sources.
* Retarget Animation for clips authored on differently-proportioned characters.
* Separate Body and Facial animation sources.

**Fixes & workarounds**

* Fix Broken Blendshape, for Character Creator's duplicate-blendshape export glitch.
* Skin Fix — an editable subnetwork with Sculpt and Soft Edit tools for mesh intersections.

**Rendering & Setup**

* Optional one-click three-point light rig, camera and Karma XPU render settings.
* Lookdev controller gathering every look control on one node.
* Reset to Defaults button.
* Quality presets — Preview and Production.

**Utilities**

* Geometry caching and a scene-cache reclaim utility.
* Navigation buttons and quick links to documentation and community.

---

!!!info
Future updates and their changes will be listed here. **All future updates to this product are included with your purchase** — check back after updating the asset to see what's new.
!!!
