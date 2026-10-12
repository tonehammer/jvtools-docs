# USD vs FBX

The **Import** dropdown at the top of the node (USD by default, or FBX) works exactly as it does on the Importer, and the rig works in both modes. The [Importer's USD vs FBX page](/reallusion-importer/getting-started/import-modes.md) has the full comparison.

## Speed and memory

USD is much faster and lighter. Measured on our test characters:

| | **USD** | **FBX** |
|---|---|---|
| Kevin (standard) | 0.4 s, 0.5 GB | 19 s, 5.2 GB |
| Jester (HD) | 1.3 s, 0.9 GB | 96 s, 12.9 GB |
| **RAM to plan for** | 16 GB minimum, 32 GB recommended | 48 GB minimum, 64 GB recommended |

## What only FBX has

Character Creator's USD export carries no data for expression wrinkles, hair ombre and ID recolour, or flow-map anisotropy on hair, so those are FBX-only. Everything else works in both modes, including the rig, the facial rig and every animation tool.

Once the rig exists, **Stash Rig** (on by default) keeps a reopened scene from importing the FBX again at all. See [Rig Settings](../using/rig-settings.md).
