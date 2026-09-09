# VEXpression

Neonyte has two VEX hook parameters. Both run once per sign. Between them they cover the whole pipeline: before the planner has made a decision, and after it has made every decision.

## Where the two hooks run

This is the order geometry passes through the node.

```text
placeholder boxes
  -> ANCHORS        one point per sign, 9 attributes
  -> anchor_vex     PRE-PLAN VEXpression   (parm: vex_anchor)
  -> sign_plan      the planner
  -> SLOTS          one point per sign, 134 attributes
  -> plan_vex       POST-PLAN VEXpression  (parm: vex_override)
  -> PLAN
  -> neon geometry, then hardware geometry
```

The pre-plan VEXpression runs before the planner has made any decisions: at that point every sign is still a single anchor point, and business type, name, layout, colours, hardware and wear are all still open. The post-plan VEXpression runs after every decision the planner has made, on the finished plan, before any geometry is built.

Hardware is built after `plan_vex` runs, but it is still reachable from it. Every hardware decision is stamped onto the plan as an `hw_*` attribute before the hardware geometry is generated from it, so writing to an `hw_*` attribute here changes what gets built.

## Pre-plan: `vex_anchor`

This runs on ANCHORS, one point per sign, before the planner runs. It is the earliest point in the pipeline where you can touch a sign, and the only point where you can steer a decision before the planner makes it rather than overwrite the result afterward.

From here you can reach decisions made inside the planner: business type, name form, era, script, palette, font, layout, theme, glyph substitution, and decay. You reach them through 29 **force hooks** - one per Advanced row that has a VEXpression column in the master matrix. The force hooks are derived directly from the 52 Advanced rows, so the two cannot drift apart.

The 9 attributes available on ANCHORS:

| Attribute | Type | Meaning |
|---|---|---|
| `v@P` | vector | Sign centre, world space. |
| `f@aspect` | float | Width divided by height of the placeholder box front face. |
| `v@extents` | vector | Box size on the sign's own axes: width, height, depth. |
| `i@piece` | int | Sign index, 0-based. Stable for a given input. |
| `s@sign_name` | string | Name typed on this sign's card, empty when the engine is free to choose. |
| `i@sign_seed` | int | The seed this sign draws from. |
| `v@xaxis` | vector | Sign-local right, world space. |
| `v@yaxis` | vector | Sign-local up, world space. |
| `v@zaxis` | vector | Sign-local forward (out of the front face), world space. |

The 29 force hooks:

| Anchor attribute | Sets | Advanced row | Section |
|---|---|---|---|
| `s@force_align` | `gen_align` | Alignment (`ga_align`) | Layout |
| `s@force_arch` | `gen_arch` | Composition (`ga_arch`) | Layout |
| `s@force_bg` | `background` | Background Decor (`ga_bg`) | Decor |
| `s@force_col_mode` | `col_mode` | Title Colour Policy (`ga_col_mode`) | Type |
| `s@force_colors` | `colour_only` | Colour (`ga_colors`) | Type |
| `s@force_dash` | `dash_mult` | Dashed Decor (`ga_dash`) | Decor |
| `s@force_decay_amt` | `decay_amt` | Deterioration Amount (`decay_amt`) | Aging |
| `s@force_decay_mode` | `decay_mode` | Deterioration (`decay`) | Aging |
| `s@force_decor_n` | `arm_n` | Decor Count (`ga_decor_n`) | Decor |
| `s@force_emit` | `emit_mult` | Brightness (`ga_emit`) | Type |
| `s@force_era` | `era` | Era (`ga_era`) | Content |
| `s@force_font` | `font_style_only` | Font Style (`ga_font`) | Type |
| `s@force_fontclass` | `font_class_only` | Font Class (`ga_fontclass`) | Type |
| `s@force_form` | `form_only` | Name Form (`ga_form`) | Content |
| `s@force_gauge` | `gauge` | Tube Gauge (`ga_gauge`) | Type |
| `s@force_glyph` | `glyph` | Letter Swapped For Icon (`ga_glyph`) | Layout |
| `s@force_icon` | `icon_mult` | Icon Presence (`ga_icon`) | Layout |
| `s@force_layout` | `template_only` | Named Layout (`ga_layout`) | Layout |
| `s@force_ornaments` | `decor_only` | Decor Family (`ga_ornaments`) | Decor |
| `s@force_radius` | `radius_mult` | Tube Thickness (`ga_radius`) | Type |
| `s@force_script` | `script_only` | Script (`ga_script`) | Content |
| `s@force_strokes` | `strokes` | Decor Stroke Lines (`ga_strokes`) | Decor |
| `s@force_theme` | `theme` | Theme (`theme`) | Content |
| `s@force_txt_fit` | `txt_lock` | Title Auto-Fit (`ga_txt_fit`) | Content |
| `s@force_txt_offx` | `txt_offx` | Title Offset X (`ga_txt_offx`) | Content |
| `s@force_txt_offy` | `txt_offy` | Title Offset Y (`ga_txt_offy`) | Content |
| `s@force_txt_rot` | `txt_rot` | Title Rotate (`ga_txt_rot`) | Content |
| `s@force_txt_track` | `txt_track` | Title Tracking (`ga_txt_track`) | Content |
| `s@force_type` | `type_only` | Business Type (`ga_type`) | Content |

!!!warning Every force attribute is a string
This includes the numeric ones. It is deliberate, and it matters.

A bound VEX write binds at compile time. If you write `if (@piece == 3) f@force_icon = 0.0;`, VEX creates `f@force_icon` on **every** point, not just point 3 - and every point that does not take the `if` branch is left at the float default of `0.0`. That silently strips icons off every other sign on the street.

A string attribute defaults to empty, and empty means "the engine decides". So the same conditional write, done as a string, is safe by construction: points that do not take the branch stay empty, and empty is a no-op.

**Always write `s@force_...`, and always assign a string** - even for a value that looks numeric.

An unparseable value is ignored, never guessed at. If you misspell a value, the hook does nothing and the engine falls back to its own decision - it does not try to coerce your typo into the closest plausible value. A typo stays visible as "nothing changed" rather than silently picking something else.
!!!

Verified example - this one produced a Japanese bar sign titled `焼鳥 とり吉`:

```vex
s@force_type   = "bar";
s@force_script = "ja";
s@force_colors = "red";
```

Per-sign, using the anchor's own `@piece`:

```vex
if (@piece == 3) {
    s@force_type = "ramen";
    s@force_era  = "1980s";
}
```

## Post-plan: `vex_override`

This runs on the finished plan, one point per sign, after every decision the planner has made and before any geometry is built. It sees the whole plan: 134 attributes covering neon and lettering, hardware, content and placement.

Normal VEX typing applies here - `i@`, `f@`, `v@`, `s@` - because these attributes already exist on every point by the time this hook runs. The compile-time binding trap described above does not apply on this hook.

Hardware is built after this hook runs, but it is reachable from it: every hardware decision is stamped onto the plan as an `hw_*` attribute before geometry is generated from it, so writing to an `hw_*` attribute here changes what gets built.

#### Neon and lettering (`slot_*`)

33 attributes.

| Attribute | Example value | Meaning |
|---|---|---|
| `i@slot_arm` | `19` | Which decor shape this slot draws. 0 on text and icon slots. |
| `i@slot_arm_n` | `0` | Repeat count for a decor shape's lines (rays, slashes, lattice bars). |
| `i@slot_col_mode` | `0` | Title colour policy: 0 single colour, 1 per letter, 2 first letter, 3 per word. |
| `v@slot_color` | `(0.55, 1, 0.78)` | Primary tube colour for this slot. |
| `v@slot_color2` | `(0.55, 1, 0.78)` | Secondary tube colour, used by the multi-colour policies. |
| `v@slot_color3` | `(0, 0, 0)` | Third tube colour, used by the two-tone and per-word policies. |
| `i@slot_dash` | `0` | 1 if this decor line is drawn dashed or dotted. |
| `f@slot_dead` | `0` | Share of this sign's letters that go fully dark, 0-1. |
| `v@slot_dead_cd` | `(0, 0, 0)` | Colour of the unlit glass on a dead letter. |
| `i@slot_decay_seed` | `0` | Random seed for this sign's per-letter decay rolls. |
| `f@slot_dim` | `0` | Share of this sign's letters that run dim, 0-1. |
| `f@slot_dim_lvl` | `0` | Brightness multiplier applied to a dim letter, 0-1. |
| `f@slot_emit` | `1.396` | Emission multiplier for this slot's tubes. |
| `i@slot_fit` | `1` | 1 if this shape stretches to fill its rect, 0 if it scales uniformly. |
| `f@slot_fit_lock` | `0` | 0 scales the title to fit, 1 locks cap height and lets it run wide. |
| `f@slot_flash_f` | `0` | Share of this sign's letters that blink fast, 0-1. |
| `f@slot_flash_m` | `0` | Share of this sign's letters that blink at medium speed, 0-1. |
| `f@slot_flash_s` | `0` | Share of this sign's letters that blink slowly, 0-1. |
| `s@slot_font` | `` | Font path for this text slot, empty on non-text slots. |
| `i@slot_gone` | `()` | Font SOP textindex values whose tube is broken off entirely. |
| `s@slot_icon` | `` | Icon name drawn on this slot, empty on non-icon slots. |
| `i@slot_id` | `0` | This slot's 0-based index among the sign's own slots. |
| `i@slot_kind` | `1` | 0 text, 1 decor shape, 2 icon. |
| `i@slot_layer` | `-1` | Depth-stacking order for overlapping decor; higher draws further forward. |
| `f@slot_radius` | `0.0075` | Tube radius for this slot, in metres. |
| `f@slot_rmax` | `0` | Maximum corner-rounding radius for this slot's outline, script or icon dependent. |
| `f@slot_rot` | `0` | Rotation applied to this slot, in degrees. |
| `i@slot_strokes` | `1` | Number of parallel outline strokes on this decor shape, 1-3. |
| `s@slot_sub_icon` | `` | Icon substituted for a letter, when Letter Swapped For Icon fired. |
| `i@slot_sub_idx` | `-1` | Font SOP textindex of the letter slot_sub_icon replaces, -1 when none. |
| `s@slot_text` | `` | The literal text this slot draws, empty on icon and decor slots. |
| `f@slot_tracking` | `0` | Extra letter spacing added to this slot's text. |
| `i@slot_word_of` | `()` | Per-character-position word index, used by the per-word colour policy. |

#### Hardware (`hw_*`)

85 attributes.

Attributes with a `_ctl` row in the Advanced section take the same values as that row's menu.

| Attribute | Example value | Meaning |
|---|---|---|
| `i@hw_bp` | `0` | LED backplate level: 0 none, 1 solid emissive field, 2-4 scattered dots, coarse to fine. |
| `f@hw_bp_b` | `0` | Backplate colour, blue component. |
| `f@hw_bp_burn` | `0` | Share of backplate LEDs burned out from deterioration, 0-1. |
| `f@hw_bp_dot` | `0` | Dot radius as a fraction of the backplate's LED pitch. |
| `f@hw_bp_emit` | `0` | Backplate emission brightness. |
| `f@hw_bp_g` | `0` | Backplate colour, green component. |
| `f@hw_bp_lift` | `0` | How far the backplate sits in front of the metal behind it, in metres. |
| `f@hw_bp_max` | `0` | Hard cap on backplate LED dots for this sign. |
| `f@hw_bp_pitch` | `0` | Spacing between backplate LED dots, in metres. |
| `f@hw_bp_r` | `0` | Backplate colour, red component. |
| `i@hw_brace` | `0` | Backing grid bracing: 0 plain, 1 Pratt, 2 Howe, 3 Warren, 4 cross-braced, 5 K truss, 6 chevron, 7 ladder. |
| `f@hw_bu0` | `-0.4191` | Backing rectangle left edge, box fraction. |
| `f@hw_bu1` | `0.4191` | Backing rectangle right edge, box fraction. |
| `f@hw_bv0` | `-0.11` | Backing rectangle bottom edge, box fraction. |
| `f@hw_bv1` | `0.19` | Backing rectangle top edge, box fraction. |
| `i@hw_cab_n` | `2` | Number of cable runs from the electrical box to the glass. |
| `f@hw_cab_r` | `0.009` | Cable radius, in metres. |
| `f@hw_cab_sag` | `0.7926` | How far a cable sags at full deterioration, fraction of sign height. |
| `i@hw_cols` | `4` | Number of grid bays across the backing. |
| `f@hw_decay` | `0` | Overall hardware deterioration for this sign, 0-1; fades the paint tone. |
| `f@hw_eb_d` | `0.1945` | Electrical box depth, in metres. |
| `f@hw_eb_gap` | `0.02` | Gap held between the electrical box and its mount, in metres. |
| `f@hw_eb_h` | `0.3044` | Electrical box height, in metres. |
| `f@hw_eb_mind` | `0.055` | Minimum electrical box depth allowed by the wall-clearance clamp, in metres. |
| `i@hw_eb_n` | `1` | Number of electrical boxes on this sign. |
| `i@hw_eb_style` | `0` | Electrical box style: 0 square junction box, 1 driver brick, 2 flat LED panel. |
| `f@hw_eb_w` | `0.2646` | Electrical box width, in metres. |
| `i@hw_edge` | `1` | Panel edge: 0 none, 1 outset bevel, 2 inset chamfer. |
| `i@hw_fit` | `1` | 0 backing fills the whole box, 1 backing is fitted to the content. |
| `i@hw_frame` | `1` | Rim frame: 0 none, 1 stands proud of the face, 2 recessed cabinet. |
| `f@hw_frame_d` | `0.0399` | Rim frame depth, in metres. |
| `f@hw_frame_w` | `0.0522` | Rim frame width, fraction of the panel's shorter side. |
| `f@hw_grey` | `0.7715` | Metal tone of the rig, 0-1, dark to pale. |
| `f@hw_inset` | `-0.0205` | Panel edge bevel depth, in metres; follows hw_edge. |
| `i@hw_l1` | `1` | Backing kind: 0 solid plate, 1 pipe grid, 2 part plate/grid, 3 minimal runs. |
| `i@hw_l2` | `1` | Sub-frame pattern: 0 spine, 1 cross, 2 ladder, 3 small perimeter grid. |
| `i@hw_l2_n` | `2` | Number of rungs or members in the sub-frame. |
| `i@hw_l3_fan` | `0` | 1 if standoffs may give up on the wall and reach for the roof instead. |
| `f@hw_l3_max` | `4.5` | Maximum standoff reach before it counts as open air, in metres. |
| `i@hw_l3_n` | `3` | Number of standoffs holding the panel off the wall. |
| `i@hw_l3_pat` | `2` | Standoff spacing: 0 evenly spaced, 1 spaced with gaps, 2 clustered in pairs. |
| `f@hw_l3_slack` | `1.6` | How far past the measured wall distance a standoff may still reach. |
| `f@hw_margin` | `0.0291` | Gap kept between the content and the backing edge, box fraction. |
| `i@hw_min_n` | `1` | Number of straight runs carrying a MINIMAL-backing sign. |
| `f@hw_min_r` | `0.016` | Tube radius of a MINIMAL-backing run, in metres. |
| `f@hw_miss_cable` | `0` | Share of cable runs dropped by deterioration, 0-1. |
| `f@hw_miss_elec` | `0` | Share of electrical boxes dropped by deterioration, 0-1. |
| `f@hw_miss_pipe` | `0` | Share of pipe members dropped by deterioration, 0-1. |
| `f@hw_missing` | `0` | Overall share of the rig dropped by deterioration, 0-1. |
| `i@hw_mix` | `3` | Which regions of the backing are solid plate versus open grid. |
| `f@hw_plate_t` | `0.02` | Backing plate thickness, in metres. |
| `f@hw_prof_u` | `(-0.5, -0.5, 0.5, 0.5)` | Sign silhouette outline, u coordinates, box fraction -0.5..0.5. |
| `f@hw_prof_v` | `(-0.5, 0.5, 0.5, -0.5)` | Sign silhouette outline, v coordinates, box fraction -0.5..0.5. |
| `i@hw_profile` | `1` | Member cross-section: 1 round tube, 2 square section. |
| `i@hw_proj` | `0` | 1 if this sign hangs sideways off the wall, a blade sign. |
| `f@hw_pu0` | `-0.4191` | Usable content rectangle left edge, box fraction. |
| `f@hw_pu1` | `0.4191` | Usable content rectangle right edge, box fraction. |
| `f@hw_pv0` | `-0.11` | Usable content rectangle bottom edge, box fraction. |
| `f@hw_pv1` | `0.19` | Usable content rectangle top edge, box fraction. |
| `f@hw_r1` | `0.008` | Backing/panel member tube radius, in metres. |
| `f@hw_r2` | `0.01` | Sub-frame member tube radius, in metres. |
| `f@hw_r3` | `0.0125` | Rooftop truss member tube radius, in metres. |
| `i@hw_rig` | `0` | How the sign is held up: 0 wall standoffs, 1 rooftop truss. |
| `i@hw_rivet` | `6` | Rivet layout pattern index; 0 is no rivets. |
| `f@hw_rivet_r` | `0.017` | Rivet radius, in metres. |
| `i@hw_rows` | `1` | Number of grid bays down the backing. |
| `i@hw_rv_diag` | `0` | Rivet pattern flags: which diagonals carry rivets. |
| `i@hw_rv_edges` | `0` | Rivet pattern flags: which panel edges carry a row of rivets. |
| `i@hw_rv_flags` | `0` | Rivet pattern flags: corner, centre and offset placements. |
| `i@hw_rv_nu` | `5` | Rivet count along the panel's u axis. |
| `i@hw_rv_nv` | `0` | Rivet count along the panel's v axis. |
| `i@hw_seed` | `11756138` | Random seed for this sign's standoff and rivet detail draws. |
| `i@hw_shape` | `0` | Sign silhouette: 0 rectangular panel, otherwise an index into the profile bank. |
| `f@hw_sup_min` | `0.4564` | Shortest standoff length allowed, as a fraction of the full reach. |
| `f@hw_sup_r` | `0.005` | Standoff tube radius, in metres. |
| `f@hw_sup_step` | `0.3608` | Spacing between standoffs along a run, in metres. |
| `f@hw_tr_base` | `0.6499` | How far the roof truss base runs back, multiple of sign height. |
| `i@hw_tr_brace` | `5` | Bracing inside each roof truss triangle: 0 bare, 1 post, 2 two posts, 3 tie, 4 post+tie, 5 K, 6 X, 7 three ties. |
| `f@hw_tr_foot` | `0` | How far the truss base runs forward as an outrigger foot, multiple of sign height. |
| `f@hw_tr_inset` | `0.0832` | How far the truss legs are inset from the sign's ends, fraction of the truss span. |
| `i@hw_tr_n` | `2` | Number of rooftop truss frames across the sign. |
| `i@hw_tr_tie` | `0` | 1 if the truss frames are tied together along the sign. |
| `f@hw_tr_top` | `0.8899` | How high up the sign the truss hypotenuse lands, fraction of sign height. |
| `f@hw_z1` | `0.1962` | Depth of the backing/panel plane behind the front face, box fraction. |
| `f@hw_z2` | `0.0853` | Depth of the sub-frame plane behind the front face, box fraction. |

#### Content (`sign_*`)

5 attributes.

| Attribute | Example value | Meaning |
|---|---|---|
| `s@sign_name` | `` | Name typed on this sign's card, empty when the engine chose the title. |
| `s@sign_sub` | `` | Subtitle text drawn under the title, when this sign has one. |
| `s@sign_title` | `Bimini Roasters` | The sign's title as drawn. |
| `s@sign_trans` | `` | English gloss of a non-Latin title, empty when already English or hand-typed. |
| `s@sign_type` | `cafe` | Business type key this sign was generated as. |

#### Placement and identity

| Attribute | Example value | Meaning |
|---|---|---|
| `v@P` | `(0, 0, 0)` | Sign centre, world space. Same on every slot of this sign. |
| `v@extents` | `(4, 2, 0.5)` | Box size on the sign's own axes: width, height, depth. Same on every slot. |
| `s@name_form` | `toponym` | Which naming method produced this sign's title, such as toponym or possessive. |
| `i@piece` | `0` | Sign index, 0-based. Same as the anchor's piece. |
| `v@rect_c` | `(0, 0.04, 0)` | Centre of this slot's content rect, box-fraction u, v. |
| `v@rect_s` | `(0.613, 0.34, 0)` | Size of this slot's content rect, box-fraction width, height. |
| `i@template` | `70` | Index into the layout template bank this sign used. |
| `s@usd_name` | `Bimini_Roasters` | USD-safe version of the title, used to name this sign's geometry groups. |
| `v@xaxis` | `(1, 0, 0)` | Sign-local right, world space. Same on every slot of this sign. |
| `v@yaxis` | `(0, 1, 0)` | Sign-local up, world space. Same on every slot of this sign. |
| `v@zaxis` | `(0, 0, 1)` | Sign-local forward, out of the front face, world space. Same on every slot. |

Verified examples:

```vex
f@slot_emit *= 3.0;          // three times the emission
i@hw_l1     = 0;             // strip the backing panel
i@hw_cab_n  = 0;             // and the cable runs
```

## Both hooks

Both parameters carry the stock `attribwrangle` snippet tags, including the button that creates spare parameters from every `ch()` call in the expression. So writing `chramp("falloff", x)` in either hook gives you a real ramp control on the node.

There is no output 2. The node has one output. To see what the plan holds at any point, read the attributes listed on this page rather than looking for a debug stream.
