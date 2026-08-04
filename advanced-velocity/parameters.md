# Parameter Reference

Every hand-authored parameter on the Advanced Velocity node, grouped the way it appears in the interface. Names in `code` are the internal parameter names.

Each velocity type also carries an identical **Adjust** and **Mask** pair, promoted straight from Houdini's Attribute Adjust nodes — those are not repeated here; see [Adjust and Mask](using.md#adjust-and-mask) and the SideFX pages for the full reference on them.

## Top level

| Parameter | Name | Description |
| --- | --- | --- |
| Group | `group` | Point group that receives the final velocity write. Points outside it keep the velocity they arrived with. |
| Mode | `av_mode` | **Timed Events**: the output is a sequence of baked events. **Single Field**: the setup is evaluated live and written straight to the output. |

## Events

Visible in Timed Events mode. See [Timed Events](timed-events.md) for the workflow.

| Parameter | Name | Description |
| --- | --- | --- |
| At Frame | `dyn_now` | Live readout of which events are contributing at the current frame, and by how much. |
| Stale | `dyn_recall_note` | Warns when the live Setup no longer matches the event it was last based on. |
| Record / Stop / Create Event | `record_events`, `stop_events`, `create_event` | Play the range for live marking; stop; bake the current setup into a new event at the current frame. |
| Copy Event | `copy_event` | Duplicate an existing event at the current frame, nothing re-baked. |
| Sort by Frame | `dyn_sort_events` | Reorder the event rows chronologically. |
| Solo / Mute | `dyn_solo`, `dyn_mute` | Play only / ignore the listed events. Space-separated numbers and ranges (`1 3-5`); the dropdowns add to the list. |

### Per event

| Parameter | Name | Description |
| --- | --- | --- |
| Name | `ev_name#` | Label for the event, shown on its tab and the timeline. |
| Event Frame | `ev_frame#` | The peak frame — Attack ramps into it, Release ramps out of it. |
| Captured | `ev_summary#` | What the event actually baked: types, point count, peak speed. |
| *Event Options* ▸ Track Motion | `ev_track#` | Re-aim the event's directional velocity at the pieces' predicted positions each frame. On by default, and what makes **To Rest Pose** work at all. Refuses when anything per-point (Adjust, Mask, Distance Falloff) sits between the field and the bake; Captured says so. |
| *Event Options* ▸ Create Rest Position Attribute | `ev_rest_en#` | Record this event's positions into a `<name>_rest` attribute for To Rest Pose. |
| *Event Options* ▸ Mute Gravity | `ev_mute_grav#` | Off / During Impulse (attack + hold) / Until Next Event / End. Off by default. The arrow button beside it propagates this event's setting to every other event. The third setting keeps gravity muted across the gap to the next event without holding the impulse on, so pieces coast instead of falling; on the last event it runs until that event stops contributing — to the end of the range when Release is off, since the envelope latches there. Mutes gravity for the whole solve, not just this event's pieces. |
| *Event Options* ▸ Stagger Points | `ev_stagger#` | Bring the points in one at a time across the event's window (Attack + Hold) instead of all at once. Off by default. Applied at playback, so it needs no re-bake. Waiting points hold in mid-air rather than falling. |
| *Event Options* ▸ Shape Distribution Ramp | `ev_stagger_shape#` | Reveal a ramp over the activation times. |
| *Event Options* ▸ Distribution | `ev_stagger_ramp#` | Left to right is each point's place in the shuffle, height is when it activates (0 = start of the window, 1 = end). Straight is an even spread. |
| *Event Options* ▸ Order | `ev_stagger_order#` | Who leads the cascade: Random, Strongest First (a shockwave out of a Point Source blast), Weakest First, Along Axis, or by piece size. Modes with nothing to measure fall back to Random. |
| *Event Options* ▸ Sweep Axis | `ev_stagger_axis#` | Direction of the Along Axis cascade — low end first. Negate to sweep the other way. |
| Timing | `ev_timing#` | **Envelope**: one Attack / Hold / Release around the Event Frame. **Pulse**: a train of grips distributed evenly across a range. |
| Range (F) | `ev_pulse_range#` | Pulse timing — the frames the train spans, starting at the Event Frame. Has its own Extend to Next + undo. |
| Pulse Count / Hold (F) | `ev_pulse_count#`, `ev_pulse_hold#` | How many grips tile the range; how long each counts as delivering energy (drives Injecting Now and Mute Gravity, anchored at each grip's peak). |
| Pattern / Curve | `ev_pulse_pattern#`, `ev_pulse_curve#` | Each grip's intensity: Hit (spike then decay), Build (ramp then cut, final grip holds), Wave (smooth swell). Curve eases Hit and Build. |
| Additional Exports ▸ Export Activation Age | `out_age` | Write `@av_age`: frames since a playing event last took hold of each point, −1 if never touched. Stagger- and pulse-aware — built for shading pickup glows. Timed Events only. |
| Attack / Hold / Release | `ev_atk#`, `ev_hold#`, `ev_rel#` | Envelope phases in **frames**, each with its own enable checkbox, all on by default. Switch all three off to latch the event at full strength forever. |
| Extend to Next | `ev_extend#` | Set Hold so this event holds until the next event's Attack opens. Next is by frame, ignoring solo/mute. Refuses on the last event. |
| (undo, beside Extend to Next) | `ev_extend_undo#` | Put Hold back to what the last Extend to Next replaced. That setting only, one press deep; greyed until Extend has been used. |
| Attack / Release Curve | `ev_atk_curve#`, `ev_rel_curve#` | Ramp shape: Linear, Ease, Sharp, Snap, Soft. |
| Release Mode | `ev_rel_mode#` | **Fade to Zero** ramps out over the Release time; **Drag** decays at a rate, so thrown pieces visibly slow. The arrow button beside it propagates this event's mode to every other event. |
| Drag | `ev_drag#` | Decay per second, in Drag mode. |
| Recall / Update | `ev_recall#`, `ev_update#` | Load the event's setup back for editing / re-bake it from the live Setup. |

## Setup

| Parameter | Name | Description |
| --- | --- | --- |
| Fold / Unfold All | `dyn_fold_setup` | Collapse or expand the *enabled* velocity sections at once. Sections whose type is switched off are left closed — their controls are hidden anyway. |
| Clear Setup | `dyn_clear_setup` | Switch every velocity type in the live Setup off. |

Every type's Adjust folder opens with the same row: **Variation** (`variation1`–`6`, five strengths), **Randomize** (`randomize1`–`6`, the dice), and **Reset** (`reset_variation1`–`6`).

### Basic Velocity

| Parameter | Name | Description |
| --- | --- | --- |
| Add Basic Velocity | `add_basic_vel` | Header checkbox. One fixed vector applied to every point. |
| Value | `value1v` | The velocity vector, in units per second. |

### Directional Velocity

| Parameter | Name | Description |
| --- | --- | --- |
| Add Directional Velocity | `add_directional_vel` | Header checkbox. |
| Direction | `direction_source` | To Position (the default), SOP Path, Use Second Input, or To Rest Pose. |
| Create Point | `dir_create_point` | Second Input mode — builds an Add SOP with one point above the mesh and wires it in. |
| SOP Path | `dir_vel_sop_path` | The SOP whose geometry is the target. |
| Target Group | `dir_target_group` | Which part of the target the centre is computed from. A single point number aims at exactly that point. |
| Group Type | `dir_target_grouptype` | What kind of element the Target Group names (default Points, so a bare number means a point). |
| Method | `method` | How a single position is derived: Center of Mass, Bounding Box Center, Convex Hull Center. |
| Rest Pose Attribute / Strength | `rest_attrib`, `rest_strength` | To Rest Pose mode — which rest pose to aim at, and how fast. |
| Target Position | `dir_target_pos` | To Position mode — the world position to aim at. |
| Toward / Around / Away | `dir_aim_toward`, `dir_aim_around`, `dir_aim_away` | Snap Direction Bias to +1 / 0 / −1. |
| Direction Bias | `dir_bias` | The continuum: +1 at the target, 0 pure orbit, −1 straight away; in between spirals. Speed blends from orbital radius to full distance. |
| Orbit Axis | `dir_orbit_axis_mode` | Toward Target (moving the target tilts the spin) or Custom Vector. |
| Custom Axis | `dir_orbit_axis` | The fixed world axle direction, in Custom Vector mode. |
| Normalize Direction | `dir_normalize` | Unit-length direction, so distance no longer affects speed. |
| Distance Falloff | `dir_falloff_enable`, `dir_falloff_min`, `dir_falloff_max`, `dir_falloff_ramp` | Fade the velocity with distance to the target (from the axle when orbiting). |

### Exploding Velocity

| Parameter | Name | Description |
| --- | --- | --- |
| Add Exploding Velocity | `add_exploding_vel` | Header checkbox. |
| Origin | `exp_origin` | Whole Object, or Point Source. |
| Method | `exp_vel_method` | Whole Object — Centroid or Medial Axis. |
| Move Centroid | `t` | Whole Object — offsets the centre the burst radiates from. |
| Direction | `exp_direction` | Point Source — Off Surface (default), Outward, Inward, or Both (split thin objects). |
| Place Source | `exp_pick` | Enters the viewport placement state. |
| Source Position | `exp_source_pos` | The world-space blast origin, drawn with a radius sphere. |
| Depth Scroll Step | `exp_pick_depth_step` | How far one Shift + scroll notch pushes the source during placement. A plain scroll scales the Radius instead. |
| Falloff Radius | `exp_radius` | Blast reach, measured to each piece's real bounds. |
| Strength | `exp_strength` | Peak speed at the source, in units per second. |
| Never Push Into Surface | `exp_clamp_outward` | Mirror any velocity heading back into the body. Hidden in the modes that already leave it. |
| Falloff | `exp_falloff` | Multiplier across the blast — left is the source, right is the radius edge. |
| Show Affected Pieces / Affected Color | `exp_show_affected`, `exp_viz_ramp` | Highlight the pieces the blast will move, normalized to the strongest one. Drawn in the viewport only — nothing is written to the output. |

### Velocity from Motion

| Parameter | Name | Description |
| --- | --- | --- |
| Add Motion Velocity | `add_inherited_vel` | Header checkbox. Velocity from the input's frame-to-frame movement. |
| Velocity Scale | `inherited_scale` | Multiplier on the derived velocity. |

### Curl Noise Velocity

| Parameter | Name | Description |
| --- | --- | --- |
| Add Curl Velocity | `add_curl_vel` | Header checkbox. A divergence-free turbulent field. |
| Frequency / Amplitude | `curl_freq`, `curl_amp` | Vortex size and speed. |
| Reverse Direction | `curl_reverse` | Every swirl runs the other way. |
| Offset | `curl_offset` | Shifts the field — vary for a different swirl pattern. |
| Evolution Speed | `curl_evolve` | How fast the field churns over time. 0 holds it static. |
| Octaves / Roughness / Lacunarity | `curl_octaves`, `curl_rough`, `curl_lacunarity` | Fractal detail controls. |

### Angular Velocity

| Parameter | Name | Description |
| --- | --- | --- |
| Add Angular Velocity (@w) | `add_angular_vel` | Header checkbox. Writes `@w`. |
| Source | `angular_source` | Constant, or Inherited from Motion (needs a point `orient` on the input). |
| Angular Velocity Value | `angular_vel` | The spin axis and magnitude, radians per second. |

## Velocity Mixer

| Parameter | Name | Description |
| --- | --- | --- |
| Event Strength | `evmix_amount#` | Timed Events only — one slider per event, named live after it. Scales that whole event across the whole range, applied at playback (never makes the event stale). The Gains below balance the types *inside* an event; these balance the events against each other. Does not close Injecting Now / Mute Gravity — use Mute for that. |
| Mixer Mode | `mixer_mode` | Additive, or Weighted (Normalized). |
| Incoming Velocity | `add_input_vel`, `input_amount` | Feed the velocity already on the geometry in as another stream (on by default), and how much of it. In Timed Events it plays as a live base layer under the events. |
| Gains | `gain_basic`, `gain_dir`, `gain_exp`, `gain_inherited`, `gain_curl` | Additive — per-type multipliers before the sum. |
| Weights | `weight_basic`, `weight_dir`, `weight_exp`, `weight_inherited`, `weight_curl` | Weighted — blend weights, normalized against each other. |
| Master Speed | `out_master_scale` | Overall multiplier on the final combined velocity, both modes. |

## Output

| Parameter | Name | Description |
| --- | --- | --- |
| Combine Into Attribute | `out_combine` | Write the mixed result to the output attribute. On by default. |
| Muting Gravity | `dyn_mute_gravity` | Live 0/1 — 1 while any playing event is inside its Mute Gravity window. Drive a solver's gravity force from it. Always 0 in Single Field. |
| Create Connected RBD Sim | `make_rbd_sim` | Build an RBD Bullet Solver below the node, already gated on Injecting Now and Muting Gravity. |
| Output As | `out_as` | Velocity (`@v`) — set directly, what RBD reads — or Force (`@force`) — accumulated by POP and Vellum. |
| Velocity Attribute / Force Attribute | `out_attrib_name`, `out_force_name` | The written attribute name; only the field for the current Output As mode is shown, and both names are kept. |
| Injecting Now | `dyn_injecting` | Live 0/1: an event is delivering energy right now. Gate an RBD solver's Overwrite Attributes list on it — see [Driving an RBD solver](timed-events.md#driving-an-rbd-solver). |
| Clamp Speed | `out_clamp`, `out_clamp_min`, `out_clamp_max` | Clamp the final speed into a range. |

### Ballistic Motion (output 2)

| Parameter | Name | Description |
| --- | --- | --- |
| Add Ballistic Motion | `ballistic_enable` | Header checkbox, on by default. Output 2 delivers the pieces advanced along the authored velocity — no solver. Output 1 is untouched; with the toggle off, output 2 is empty. |
| Include Rotation | `ballistic_spin` | Fold baked `@w` into each packed piece's transform, so the pieces tumble as they fly. |
| Display Offset | `ballistic_offset` | Slide the flying pieces sideways, in multiples of the object's width — an exploded-view shift, recorded as `jv_preview_shift`. |
| Return to Home | `ballistic_return` | 0 = full flight, 1 = every piece back at exactly its input position. Keyframe it for a reassembly; the landing at 1 is exact by construction. |
| *Return Shaping* ▸ Return Profile | `ballistic_return_ramp` | Ramp over the return blend, for easing the approach. |
| *Return Shaping* ▸ Stagger / Return Order | `ballistic_return_stagger`, `ballistic_return_order` | Give each piece its own return window; Order picks who leads — Random, Nearest First, Farthest First. Everyone is home by 1. |
| *Return Shaping* ▸ Arc / Swirl / Swirl Axis | `ballistic_arc`, `ballistic_swirl`, `ballistic_swirl_axis` | Bow each return path sideways; Swirl blends the arcs toward a shared rotation about the axis — a vortex funnelling home. |
| *Return Shaping* ▸ Extra Turns / Seed | `ballistic_turns`, `ballistic_arc_seed` | Whole extra loops on the unwind (invisible at both ends), and the re-roll for the per-piece arc directions. |
| *Return Shaping* ▸ Show on Preview Ghost | `ballistic_preview` | Let the motion-preview ghost follow Return to Home too. |
| *Return Shaping* ▸ Return Paths | `viz_arc`, `viz_arc_color` | Draw each piece's route home as a guide curve — sampled from the same curve the blend walks. |
| Create Ballistic Return | `make_ballistic_return` | Builds a [Ballistic Return](#ballistic-return-the-sidecar-node) node below this one — the same return, applied to a real simulation instead of the prediction. |
| Scale by Piece Size | `out_piece_scale`, `out_piece_influence` | Big chunks fly slower. Mass from a point `mass` attribute or the piece's size; Influence blends from uniform (0) to full inverse mass (1). |
| Additional Exports | `out_basic`, `out_dir`, `out_exp`, `out_inherited`, `out_curl` | Collapsed section — keep a sub-velocity on the output under its own name. In Timed Events the export carries the playing events' contribution (events baked before per-type storage need Update). Everything else is stripped. |
| Export Rest Position Attributes | `output_rest` | In Additional Exports — keep `startframe_rest` and every event's `<name>_rest` on the output, for reassembly or retargeting downstream. |

### Ballistic Return (the sidecar node)

Ballistic Motion returns the pieces home from a *prediction*. Often what you
actually want is to reassemble a **finished simulation** — and that has to
happen downstream of the solver, on a node of its own. That node is **Ballistic
Return**, and it ships in the same file: press **Create Ballistic Return**, or
grab it from the JV tab menu.

It wires itself up: input 1 takes the simulated pieces (the RBD solver below
your Advanced Velocity node, if there is one), input 2 takes the rest pose
(Advanced Velocity's own first output — the geometry before anything moved it).
Then keyframe **Return to Home** from 0 to 1 and the pieces fly back together.

Why the landing is always exact: the blend's endpoint is *absolute*. At Return 1
the result **is** the rest pose, whatever the simulation was doing underneath —
there is nothing to fight, because the target is not relative to the motion it
replaces. Nothing is snapshotted either, so re-simulating upstream can never
leave this node stale. Pieces are matched by point number, which a Bullet solve
preserves.

| Parameter | Name | Description |
| --- | --- | --- |
| Return to Home | `ballistic_return` | 0 leaves the sim alone, 1 puts every piece back at exactly its rest position and orientation. Keyframe this. |
| Rest Attribute | `ballistic_rest_attrib` | Which pose to return to. Empty uses the second input's positions — the usual case. Name a vector point attribute on the first input instead (that is what **Export Rest Position Attributes** writes) and the pieces return to *that* captured pose. |
| Include Rotation | `ballistic_spin` | Also unwind each packed piece's orientation. Reads the rest transforms from the second input, so keep it wired; only does anything on packed geometry. |
| *Return Shaping* | *(same names as above)* | Return Profile, Stagger, Return Order, Arc, Swirl, Swirl Axis, Extra Turns, Seed and Return Paths — identical to the Ballistic Motion folder. |

Careful with this one: if your input mesh is **animated**, the second input's
positions have moved on by the time the return happens, so "home" is a moving
target. That is what Rest Attribute is for — turn on **Export Rest Position
Attributes** upstream and return to `startframe_rest` (or any event's captured
pose) instead. On a static mesh you can ignore all of this and leave the field
empty.

## Visualization

| Parameter | Name | Description |
| --- | --- | --- |
| *(top right, icon)* Reset Visualization | `viz_reset` | Put every control on this tab back to its default. Guide Density is re-picked from the current input rather than left at 1.0. |
| Show Guides | `viz_guides` | Master switch for all velocity guides. |
| Guide Global Scale | `viz_scale` | Length multiplier for all guide trails. |
| Normalize Guide Length | `viz_normalize`, `viz_normalize_amt` | Blends every trail toward one uniform length — the joined 0-1 slider controls how much. At 1, every guide draws at exactly Guide Global Scale length; directions never change, and the output is untouched. |
| Guide Density | `viz_density` | Fraction of trails actually drawn, for viewport speed. Picked for you the first time geometry is connected to a fresh node, aiming at roughly 200 trails; after that it is yours and is never changed again. On dense inputs the trails also auto-cap at the Visualization Limit; Density scales within that budget. |
| Enforce Visualization Limit | `viz_limit_enable`, `viz_limit` | Point budget (default 100,000) capping how many guide trails are drawn. Raise it or switch it off to draw everything regardless of cost. Guide trails only — Preview Motion is not affected. |

The next two groups appear in Timed Events only.

| Parameter | Name | Description |
| --- | --- | --- |
| *Timed Events* ▸ Source | `dyn_guide_source` | Which stream the guides draw: Setup, Events, or Both. |
| *Timed Events* ▸ Preview Motion | `dyn_preview`, `dyn_preview_ghost`, `dyn_ghost_color` | Advance the baked guides to the predicted positions, with an optional ghost of the pieces. **Off by default — the most expensive control here:** the ghost redraws your pieces on every refresh, which slows scrubbing and parm edits on heavy or textured objects. |
| *Timed Events* ▸ Ghost Style | `dyn_ghost_style` | How the ghost draws: Full Wireframe, Bounding Boxes (default — one wire box per piece, cheap at any density), or Points. |
| *Timed Events* ▸ Offset | `dyn_preview_offset` | Slide the preview sideways, in multiples of the object's width. |
| *Timed Events* ▸ Unify Baked Guides | `viz_baked_yellow`, `viz_baked_tint` | Draw every baked-event guide in one colour instead of per-type colours. |
| *Timeline HUD* ▸ Event Timeline / Scheme | `viz_timeline`, `viz_timeline_scheme` | The on-screen frame ruler with a marker per event; Dark or Light palette. Drawn by the viewer state rather than as guide geometry, so Show Guides and the Visualization Limit do not affect it. |

| Parameter | Name | Description |
| --- | --- | --- |
| Per-type rows | `viz_input`, `viz_basic`, `viz_dir`, `viz_exp`, `viz_inherited`, `viz_curl`, `viz_angular` + `_color` + `_scale` | A toggle, colour and extra scale per stream, incoming velocity included. |

## Utilities

| Parameter | Name | Description |
| --- | --- | --- |
| Output Guides Only (No Geometry) | `out_guides_only` | Output the guide curves instead of the geometry — for rendering the guides as their own pass. In Timed Events it always emits the baked event trails, ignoring Show Guides and Source (so the pass can't be empty), and **respects Preview Motion** — on, the trails follow the predicted motion; off, they sit at rest. The ghost never enters the pass. |
| Restore Viewport HUD | `util_restore_hud` | Re-enter the node's viewer state, bringing the event timeline back after an asset refresh. |
| Links | `gumroad`, `docs`, `discord`, `youtube` | This documentation, the store page, and the community. |

## About

| Parameter | Name | Description |
| --- | --- | --- |
| Current Version | `version2` | The product version installed. The node checks for updates when you press its action buttons and tells you when a newer one is on Gumroad. |
