---
icon: arrow-switch
order: 95
---

# USD vs FBX

At the very top of the node is an **Import** dropdown with two choices — **USD** (the default) and **FBX**. Both produce the same shaded character with the same lookdev controller, and the rig builds on either; they differ only in import speed, memory use, and a few features that depend on data Character Creator writes to one export but not the other.

## TL;DR — what you get from each

| | **USD** *(default)* | **FBX** |
|---|---|---|
| **Import speed** | less than a minute, even for HD characters | 1 - 3 min (grows with character weight) |
| **Memory (one loaded character)** | less than 8GB, even for HD characters | ~10–40 GB |
| **RAM to plan for** | 16 GB min / 32 GB recommended | 48 GB min / 64 GB recommended (HD) |
| Geometry, skeleton, body + facial animation | ✅ Full | ✅ Full |
| Materials (skin, eyes, teeth, hair, clothing) | ✅ Full | ✅ Full |
| Subsurface, displacement, Skin Fix, render rig | ✅ Full | ✅ Full |
| The APEX rig, the facial rig and every animation tool | ✅ Full | ✅ Full |
| **Real CC eye & skin values** (iris color, iris size, limbus, sclera, SSS) | ✅ Read from the file & auto-applied | ⚠️ Not exported — generic starting defaults |
| **Expression wrinkles** | ❌ Not in the USD export | ✅ Yes |
| **Hair root-to-tip ombré + highlight streaks + flow sheen** | ❌ Maps not in the USD export | ✅ Yes |
| Hair flat re-dye + Lightness (Bleach) | ✅ Yes | ✅ Yes |

!!!success Bottom line
Use **USD** for almost everything — it's far faster, far lighter, and *better* at eyes/skin because it carries Character Creator's real shader values. Switch to **FBX** only when you specifically need **animated expression wrinkles** or the **full hair re-dye** (root-to-tip / highlight streaks).
!!!

## The best-quality workflow

**An FBX character.** The expression wrinkles are the single feature that makes a Character Creator face read as *alive* in motion, and they're **FBX-only** — the rig carries them through to its output, so a face you animate on the rig wrinkles the way Character Creator's does. When the look matters, import the character as **FBX**.

!!!info An honest caveat
This is the best-quality path, not the lightest one. An FBX-imported character is memory-heavy no matter what — that's the cost of carrying the wrinkle data, and it's unavoidable if you want wrinkles. Once the rig is built, **Stash Rig** (on by default) means a reopened scene never imports the FBX again, so you pay the import once per character, not once per session. See [Rig Settings](../using/rig-settings.md). If you don't need wrinkles at all, a plain **USD** import is the lighter choice.
!!!

## Why USD is so much faster and lighter

Character Creator's FBX stores every facial blendshape as a full mesh copy, and Houdini has to expand all of them on import — tens of gigabytes of RAM and a minute or more on a heavy HD character. The USD export keeps those blendshapes sparse, and the tool keeps them sparse **through deformation too**: only the expressions actually active on the current frame are computed. On the heaviest HD character, working footprint drops from **~26 GB via FBX to under 8 GB via USD**, and raw import time drops from a minute and a half to about a second — the gap grows the heavier the character.

## What USD does *better* — real Character Creator eye & skin values

The FBX export leaves out most of Character Creator's HD eye shader, so in FBX mode the eye controls start from generic defaults you dial in by eye. **The USD export carries Character Creator's actual shader values**, so in USD mode the tool reads them and seeds the controller automatically — real iris color (when CC actually tinted it), iris size and limbal ring, and sclera shading and subsurface amount from the real per-character values. It's all still adjustable; these are just smarter starting points, and **Reset to Defaults** returns to them. See [Eyes](../lookdev/eyes.md).

## What USD mode does *not* carry

Character Creator's USD export omits some data the FBX export includes. Where that happens, the affected controls stay visible but are **disabled with an "(FBX import only)" note** — nothing is hidden or silently broken.

* **Expression wrinkles** — the animated head-wrinkle system is **FBX only**; the USD export contains no wrinkle maps or weights. See [Wrinkles](../lookdev/wrinkles.md).
* **Root-to-tip and highlight hair re-dye** — Character Creator's USD export leaves out the hair root, ID, and flow maps, so the ombré recolor, highlight streaks, and flow-based sheen are **FBX only**. A **flat re-dye and the Lightness (Bleach) control still work** in USD. See [Hair](../lookdev/hair.md).

Everything else — including **displacement**, the rig and every animation tool — works in both modes.

!!!info Motion clips
The rig's **Clip Files** list takes Character Creator **USD** Motions clips and **FBX** animation alike — a USD Motions clip is the small, fast one. A clip exported on a different character is retargeted automatically, but it is an approximation; see [Clips & Layers](../using/clips-and-layers.md#what-to-do-where).
!!!

## Switching modes

The **Import** dropdown swaps which file field is shown — **USD File** or **FBX File** — and builds accordingly on **Build Character**. Before a rig exists you can switch any time; just set the matching file. Once the rig is built it is frozen to the character it was built from, so switching modes afterwards changes nothing until you delete the rig node and press **Build Character** again.

Next: [Preparing Your Character](preparing-your-character.md) covers how to export for **both** modes.
