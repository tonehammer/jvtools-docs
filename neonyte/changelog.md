# Changelog

!!!warning Pre-release
Neonyte has not had a public release yet. This page tracks the pre-release state; the first public entry will be **1.0**.
!!!

## Version 0.9 (pre-release)

The v1 architecture is complete and the breadth pass is well underway. In place so far:

- **Box-to-sign pipeline** — connectivity split, per-piece front-face frame, placeholder deletion, one generated sign per fronted box.
- **Content engine** — type-first generation across ~30 business types with realistic name-form distributions, curated banks cross-checked against public-domain corpora, a character-level generator for invented words, within-building de-duplication, and a famous-marks blocklist.
- **Layout** — dozens of hand-authored templates plus a procedural layout generator; text, subtitle, icon and armature slots with depth-layered overlap; glyph-substitution wordplay.
- **Armatures** — ovals, underlines, frames, arrows, plus dim background kinds (grids, lattices, scallops, rays, chevrons, bulb rows), entrance arrows, and several ornament systems; optional dashed tubes.
- **Icons** — a large tagged library vendored to neon-tube polylines, mapped to business type.
- **Colour + emission** — per-sign neon palettes driving viewport colour and per-sign HDR emission for Karma.
- **Hardware** — three-level procedural metalwork (backing/truss, sub-frame, standoffs) that reaches back and lands on the building, with an open-air guard so nothing attaches to thin air.
- **Steering** — theme presets, plain-language Adjustment Notes (rule parser + semantic matcher + optional local model), and a per-box Signs panel with re-roll, hand-editable title/subtitle, and per-sign Advanced overrides.
- **Multi-script** — Japanese, Chinese, Cyrillic and Arabic names/subtitles, with Arabic pre-shaped at authoring time.

Still in flight for 1.0: further breadth, control-surface cleanup, and the productization/release pass.
