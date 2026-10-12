---
icon: checklist
order: 80
---

# Preparing Your Character

The Rigger imports the same files the Importer does, so the export settings are the same. The [Importer's page](/reallusion-importer/getting-started/preparing-your-character.md) covers them for [USD](/reallusion-importer/getting-started/preparing-your-character.md#exporting-as-usd-recommended), [FBX](/reallusion-importer/getting-started/preparing-your-character.md#exporting-as-fbx) and [iClone](/reallusion-importer/getting-started/preparing-your-character.md#exporting-from-iclone). Do that first. These are the points the rig adds.

* **Include the animation.** Export **Character** (not All), with **Include Motion** on if you want the character's own animation. The rig bakes that clip as its **BaseAnimation** layer.
* **Export without animation if you prefer.** The rig is then built at the character's rest pose, and **Set Frame Range to Animation** has nothing to set.
* **FBX: start with the bind pose.** Set **First frame pose type** to **Start with BindPose** in Character Creator 5's FBX export options. USD exports need no special settings.
* **Keep the files together.** The `Materials` folder stays beside the `.usd`, and the `.json`, `.fbm` and `textures` stay beside the `.fbx`.
* **Apply other motions in Character Creator.** A clip from a different character plays but is an approximation. For motion that matters, apply it to your character in Character Creator 5 or iClone and export it. See [Clips & Layers](../using/clips-and-layers.md#what-to-do-where).
