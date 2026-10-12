---
# Absolute on purpose: Retype's "See also" cards copy this string verbatim onto sub-pages, where a relative path 404s.
icon: https://jvtools.dev/docs/reallusion-rigger/static/reallusion_rigger_logo.svg
order: 990
---

# Reallusion Rigger for Houdini

<div style="text-align:center; background:#0d1117; border-radius:16px; padding:2.5rem 1rem; margin:0.5rem 0 1.5rem;">
  <img src="static/reallusion_rigger_logo.svg" alt="Reallusion Rigger for Houdini" width="150" style="max-width:60%;">
</div>

<p style="text-align:center; margin:0 0 1.5rem;"><a href="https://jvtonehammer.gumroad.com/l/reallusionimporterforhoudini"><strong>Get it on Gumroad →</strong></a><br><a href="https://jvtools.dev/" style="font-size:0.9em;">More Houdini tools at jvtools.dev</a></p>

**{{ rr.name }}** (v{{ rr.version }}) imports a Character Creator 5 or iClone 8 character into Houdini's Solaris environment, builds Karma XPU materials for it, and builds an APEX animation rig for it. The **Build Character** button does all of this.

It includes everything the [Reallusion Importer](/reallusion-importer/README.md) does: FBX or USD import, MaterialX materials and the lookdev controller. The Rigger adds a rig node below the importer. Press **Animate** on it to pose and key the character in the viewport, face included.

## Rigger and Importer compared

* **Pick the Importer** to render characters with their exported animation, or if you work in Houdini 21. It runs on Houdini 21 and 22 and ships as one file.
* **Pick the Rigger** to animate in Houdini. It needs Houdini 22 or newer, because it is built on Houdini 22's APEX autorig builder. It also ships as one file.

One Gumroad page sells both as separate versions. Buying one does not include the other, and there is no upgrade from the Importer to the Rigger; they are separate purchases.

## What the Rigger adds

A body rig and a facial rig with every morph channel keyable, Face Puppet, Face Key Muscle, 301 expressions and 71 hand poses, Auto Blink, Auto Breathe, Look At, motion clips, layer tools and Stash Rig.

AccuLips, AccuFACE and Motion LIVE are out of scope. Do mocap, face capture and lip-sync in iClone and export the result.

## Requirements

Houdini 22.0 or newer, on Windows (what it was tested on), and a Character Creator 5 / iClone 8 character exported as USD or FBX. RAM: with USD import, 16 GB minimum and 32 GB recommended. With FBX import, 48 GB minimum and 64 GB recommended.

!!!warning About the Indie license format
The Rigger is a Houdini Indie `.hdalc` asset. It loads in Houdini Indie and Apprentice. Houdini FX and Core can load it too, but that switches the session to limited-commercial (Indie) mode, per SideFX.
!!!

## Where to start

Read [Requirements & Installation](getting-started/installation.md), [Preparing Your Character](getting-started/preparing-your-character.md) and [Quick Start](getting-started/quick-start.md) in that order. **Using the Asset** covers the rig and the animation tools. Materials and look development are the Importer's, so see its [docs](/reallusion-importer/using/lookdev-controller.md).

!!!info
This tool is an independent product and is not affiliated with, endorsed by, or sponsored by Reallusion or SideFX. "Character Creator," "iClone," and "Houdini" are trademarks of their respective owners.
!!!
