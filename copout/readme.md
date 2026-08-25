# COPout

!!!warning Pre-release — private draft
These docs cover **COPout v0.1**, which has not been built yet. It is a productization of an in-house shelf tool, so the feature set below describes what the tool already does rather than what the HDA ships. Parameter names, defaults, and whole feature areas will change. This section is private and not linked from the public site.
!!!

Welcome! **COPout** (v0.1) puts a Copernicus network on a projector or second screen as a borderless, chrome-free output window — Houdini's missing Perform window.

TODO — the overview paragraph.

## Why it exists

Houdini's Composite View cannot be stripped of its chrome. The whole pane — menu bar, toolbars, footer — is drawn *inside a single GL surface*, so there is no toolbar to hide and no setting that removes it. There is also no zoom or pan API on that pane at all. So for projector work, installations and live visuals, the native route simply cannot give you a clean full-screen image you can align.

COPout draws the pixels itself instead.

## What it does

TODO — expand each of these into real prose:

- **Three sources** — the COP image, the 3D viewport, or the viewport over the COP.
- **Any screen, any fit** — pick the projector from a dropdown, go fullscreen, letterbox or crop or 1:1 or stretch.
- **Align it by hand and keep it** — right-drag to move the image, nudge with the arrows, and the alignment is saved with the scene.
- **Follows the playbar** — nothing runs its own clock, so a COP feedback sim steps exactly once per frame.
- **Grade it on the way out** — exposure and gamma, applied on the GPU.

## What it does not do

TODO — it does not record or render to file; it does not run its own clock; it drives one output window, not several. Naming these saves a support conversation.

## Requirements

- Houdini 22.0+ (Indie or Apprentice — ships as `.hdalc`)
- Windows (the only tested platform)
- A Copernicus network in the scene

## Pages

- [Getting started](getting-started.md)
- [Using COPout](using.md)
- [Parameter reference](parameters.md)
- [Changelog](changelog.md)
