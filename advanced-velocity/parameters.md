---
icon: sliders
order: 80
---

# Parameter Reference

Every parameter on the Advanced Velocity node, grouped as it appears in the interface. Names in `code` are the internal parameter names.

Each velocity type also carries an identical **Adjust** and **Mask** pair, promoted from Houdini's Attribute Adjust nodes — see [Adjust and Mask](using.md#adjust-and-mask).

## Basic Velocity

| Parameter | Name | Description |
| --- | --- | --- |
| Basic Velocity | `add_basic_vel` | The section's header checkbox. Enables the type and reveals its controls. |
| Value | `value1v` | The velocity vector applied to every point. |

## Directional Velocity

| Parameter | Name | Description |
| --- | --- | --- |
| Directional Velocity | `add_directional_vel` | Header checkbox. |
| Direction | `direction_source` | Use Second Input, or SOP Path. |
| Create Point | `dir_create_point` | Builds an Add SOP with one point above the mesh and wires it into the second input. |
| Ptnum to Target | `pt_to_target` | Which point of the second input to aim at. |
| SOP Path | `dir_vel_sop_path` | The SOP whose centre the velocity aims at. |
| Method | `method` | How that SOP's centre is measured — centre of mass, bounding box, or convex hull. |
| Normalize Direction | `dir_normalize` | Make every direction unit length, so distance no longer affects speed. |
| Distance Falloff | `dir_falloff_enable` | Fade the velocity with distance from the target. |
| Falloff Min / Max | `dir_falloff_min`, `dir_falloff_max` | The distance range the falloff spans. |
| Falloff Ramp | `dir_falloff_ramp` | Shape of the fade across that range. |

## Exploding Velocity

| Parameter | Name | Description |
| --- | --- | --- |
| Exploding Velocity | `add_exploding_vel` | Header checkbox. |
| Origin | `exp_origin` | Whole Object, or Point Source. |
| Method | `exp_vel_method` | Whole Object only — Centroid or Medial Axis. |
| Move Centroid | `t` | Whole Object only — offsets the centroid the burst radiates from. |
| Direction | `exp_direction` | Point Source only — Outward, Inward, or Both (split thin objects). |
| Source Position | `exp_source_pos` | Point Source only — the world-space blast origin. |
| Select Source Position Interactively | `exp_pick` | Enters the viewport placement state. |
| Depth Scroll Step | `exp_pick_depth_step` | How far one wheel notch pushes the source during placement. |
| Falloff Radius | `exp_radius` | Pieces beyond this distance from the source get no velocity. Measured to each piece's pivot. |
| Strength | `exp_strength` | Peak outward speed at the source, in units per second. |
| Never Push Into Surface | `exp_clamp_outward` | Mirror any velocity heading back into the body. Hidden in Both mode. |
| Falloff | `exp_falloff` | Velocity multiplier across the blast — left is the source, right is the radius. |
| Show Affected Pieces | `exp_show_affected` | Tint the pieces this blast will move. Writes `Cd`. |
| Affected Color | `exp_viz_ramp` | Colour across the blast, normalized to the strongest affected piece. |

## (Extra) Angular Velocity

| Parameter | Name | Description |
| --- | --- | --- |
| (Extra) Angular Velocity | `add_angular_vel` | Header checkbox. Creates `@w` on the output. |
| Angular Velocity Value | `angular_vel` | The `@w` vector, in radians per second. |

## Velocity Mixer

| Parameter | Name | Description |
| --- | --- | --- |
| Mixer Mode | `mixer_mode` | Additive, or Weighted (Normalized). |
| Basic / Directional / Exploding Gain | `gain_basic`, `gain_dir`, `gain_exp` | Additive only — multiplier for that type before it is summed. |
| Basic / Directional / Exploding Weight | `weight_basic`, `weight_dir`, `weight_exp` | Weighted only — blend weight, normalized against the other enabled types. |
| Mix Scale | `mix_scale` | Weighted only — overall multiplier applied after normalization. |

### Output

| Parameter | Name | Description |
| --- | --- | --- |
| Combine Into @v | `out_combine` | Write the mixed result to `v@v`. On by default. |
| Export Basic | `out_basic` | Keep `@basic_vel` on the output. |
| Export Directional | `out_dir` | Keep `@dir_vel` on the output. |
| Export Exploding | `out_exp` | Keep `@exp_vel` on the output. |

Anything not exported is stripped before the output.

## Visualization

| Parameter | Name | Description |
| --- | --- | --- |
| @v Vectors | `viz_v_attrib` | Houdini's own `@v` attribute visualizer — the yellow vectors. |
| Point Trails | `viz_point_trails` | Houdini's viewport Point Trails display — the blue motion trails. |
| Scale | `viz_scale` | Length multiplier for the guide lines below. |
| Basic / Directional / Exploding / Angular Velocity | `viz_basic`, `viz_dir`, `viz_exp`, `viz_angular` | Draw guide lines for that type, scaled by its real contribution to the mix. Each has its own colour. |

## About

| Parameter | Name | Description |
| --- | --- | --- |
| Current Version | `version2` | The product version installed. |
