---
icon: arrow-switch
order: 95
---

# Import Modes — USD & FBX

Version 1.2 added a second way to bring your character in. At the very top of the node is an **Import** dropdown with two choices:

* **USD** *(default)* — imports Character Creator's **Export USD (Omniverse)** output. Dramatically faster and lighter on memory.
* **FBX** — the original path, importing a standard **Export FBX** file. Needed for a few features Character Creator only writes to FBX.

Both modes produce the same shaded, animatable character with the same lookdev controller. They differ only in how fast the import is and in a small number of features that depend on data Character Creator includes in one export but not the other.

!!!success The short version
Use **USD** for almost everything — it's much faster and uses a fraction of the memory. Switch to **FBX** only if you specifically need **animated expression wrinkles** or the **root-to-tip / highlight hair re-dye**, which USD exports don't carry (see below).
!!!

## Why USD is the default — speed and memory

Character Creator's FBX stores every facial blendshape as a full mesh copy, and Houdini has to expand all of them on import. On a heavy HD character that means tens of gigabytes of RAM and a minute or more of waiting. The USD export keeps those blendshapes sparse, so Houdini reads them almost instantly.

The difference is not subtle. In our tests:

| Character | FBX import | USD import |
|---|---|---|
| A standard base character | ~19 s, ~5 GB | **~0.4 s, ~0.5 GB** |
| A heavy HD character | ~96 s, ~13 GB | **~1.3 s, ~0.9 GB** |

That's roughly **50–75× faster** and **10–14× less memory**, and the gap grows the heavier your character is. Because USD imports in about a second, the [Skin Cache](../reference/performance.md) is unnecessary in USD mode — so its controls are hidden there.

## What's identical in both modes

Everything that makes up the character and its look is the same:

* Geometry, skeleton, and animation (body + facial)
* All materials — skin, eyes, teeth, hair, clothing, accessories
* Subsurface scattering, displacement, the full lookdev controller
* Retargeting, Split Body/Facial animation, Skin Fix, and the optional render setup

You art-direct a USD-imported character exactly the way you would an FBX one.

## What USD does *better* — real Character Creator eye & skin values

The FBX export leaves out most of Character Creator's HD eye shader, so in FBX mode the eye controls start from sensible-but-generic defaults you dial in by eye. **The USD export carries Character Creator's actual shader values**, so in USD mode the tool reads them and seeds the controller with the real thing automatically:

* **Iris color** — your character's real iris tint, already applied (only when Character Creator actually tinted it; fully-textured eyes are left untouched).
* **Iris size and limbal ring** — sized to Character Creator's own values.
* **Sclera shading and subsurface amount** — seeded from the real per-character values.

You can still change all of it — these are just smarter starting points. See [Eyes](../using/eyes.md).

## What USD mode does *not* carry

Character Creator's USD export omits some data the FBX export includes. Where that happens, the affected controls stay visible but are **disabled with an "(FBX import only)" note** — so nothing is hidden or silently broken, you can always see what a mode does and doesn't do.

* **Expression wrinkles.** The animated head-wrinkle system is **FBX only** — the USD export contains no wrinkle maps or weights. If your character's performance relies on forehead/brow wrinkles, import it as FBX. See [Wrinkles](../using/wrinkles.md).
* **Root-to-tip and highlight hair re-dye.** Character Creator's USD export leaves out the hair root, ID, and flow maps, so the **ombré (root/tip) recolor, ID-based highlight streaks, and flow-based anisotropic sheen are FBX only**. A **flat re-dye and the Lightness (Bleach) control still work** in USD mode — you can recolor and lighten hair, just not drive a root-to-tip gradient or highlight streaks. See [Hair](../using/hair.md).

Everything else — including **displacement** — works in both modes.

!!!info Mixing sources
USD characters bind in a T-pose (FBX binds in an A-pose). This only matters if you drive a **USD** character with an **FBX** animation-database clip from a *different* character — the pose conventions differ, so turn **Retarget Animation** on in that case. A character driven by its own embedded animation is always correct. See [Animation](../using/animation.md).
!!!

## Switching modes

The **Import** dropdown swaps which file field is shown — **CC5/iClone USD** or **CC5/iClone FBX** — and rebuilds accordingly when you click **Build Character**. You can switch an existing node between modes at any time; just make sure the matching file is set. Scenes saved before 1.2 keep working: they load in FBX mode automatically, so nothing you built before changes.

Next: [Preparing Your Character](preparing-your-character.md) covers how to export for **both** modes.
