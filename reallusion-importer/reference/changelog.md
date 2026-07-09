# Changelog

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
