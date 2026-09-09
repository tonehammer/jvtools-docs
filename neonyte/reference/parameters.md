# Parameters

Every control on the node, grouped by the folder it lives in. The description column is the first line of each control's own tooltip, so the two always agree. The `Internal name` column is what you use in a channel reference or a script.

164 controls in total.

The Manual Overrides (Global) folders are the street-wide half of the Advanced rows; each row also appears on every sign's own card. See [Advanced rows](../control/advanced.md) for how Auto and Custom work. The two VEXpression hooks are documented at [VEXpression](../control/vexpression.md).

Rows inside a sign card carry a `#` in the internal name; on the node it is replaced by the card number, so the Title on card 3 is `psa_title3`.

### Top level

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Give me the Signs | `randomize` | Button | Rebuilds every sign on the street using a new random seed, so pressing it again gives you a different set of names, layouts and colors. |
| Done Editing | `done_editing` | Button | Calls off an edit that was started and never finished, and puts the display flag back on this node. |

### Sign Placement

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Place Sign in Viewport | `place_start` | Button | Switches the viewport into placement mode - click any surface to drop a sign there. |
| Edit Sign in Viewport | `edit_start` | Button | Lets you pick a sign in the viewport and put it back into placement mode, following the surface again. |
| Placeholder Boxes Only | `boxes_only` | Toggle | Skips building the signs and shows just the placeholder boxes, so laying a street out stays responsive. |
| Default Sign | `place_type` | Menu | Which kind of sign the placement tool starts with when you enter the viewport. |
| Size | `place_scale` | Float | How big the next placed sign will be, as a multiplier on its normal size. |
| Nudge Step | `place_nudge` | Float | How far one click of the mouse wheel pushes a sign off the surface it is sitting on, in metres. |
| Rotation Step | `place_rot_step` | Float | How many degrees one click of the mouse wheel turns a latched sign. |
| Max Tilt Off Surface | `place_tilt_max` | Float | The furthest a sign can be tilted away from the surface it is sitting on, in degrees. |

### Content / Design

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Seed | `seed` | Int | The master number every sign on the street is generated from. |
| Theme | `theme` | Menu | A style preset that shifts the mix of business types, colors, fonts and layouts toward a look. |
| Adjustment Notes | `adjustment_notes` | String | Words the engine understands, in any order, then press Give me the Signs to apply them. |
| Force Title | `force_title` | String | Puts the same words on every sign in the street, and leaves each one the typography, layout, colour and decor it drew. |

### Content / Design / Manual Overrides (Global) / Content

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Business Type | `ga_type_ctl` | Menu | Pins the trade every sign advertises, overriding whatever the engine would otherwise pick. |
| Business Type | `ga_type` | Menu | Which trade to force on every sign when the row above is set to Custom. |
| Name Form | `ga_form_ctl` | Menu | Pins the shape of every sign's name - a plain category sign, an owner's name, a place name, and so on. |
| Name Form | `ga_form` | Menu | The shape of name to force when the row above is set to Custom. |
| Era | `ga_era_ctl` | Menu | Weights every sign's owner name toward a decade. |
| Era | `ga_era` | Menu | The decade to weight the owner's name toward, when the row above is set to Custom. |
| Script | `ga_script_ctl` | Menu | Forces which writing script every sign's title uses. |
| Script | `ga_script` | Menu | The writing script to force when the row above is set to Custom. |
| Title Auto-Fit | `ga_txt_fit_ctl` | Menu | Controls how every sign's title is scaled to fill its space. |
| Title Auto-Fit | `ga_txt_fit` | Menu | How the title is sized when the row above is set to Custom. |
| Title Offset X | `ga_txt_offx_ctl` | Menu | Shifts the title sideways from where the layout would normally place it. |
| Title Offset X | `ga_txt_offx` | Float | How far to shift the title sideways, as a fraction of the sign's width, when the row above is set to Custom. |
| Title Offset Y | `ga_txt_offy_ctl` | Menu | Shifts the title up or down from where the layout would normally place it. |
| Title Offset Y | `ga_txt_offy` | Float | How far to shift the title up or down, as a fraction of the sign's height, when the row above is set to Custom. |
| Title Rotate | `ga_txt_rot_ctl` | Menu | Tilts the title away from its normal orientation. |
| Title Rotate | `ga_txt_rot` | Float | How many degrees to tilt the title when the row above is set to Custom. |
| Title Tracking | `ga_txt_track_ctl` | Menu | Adjusts the spacing between the title's letters. |
| Title Tracking | `ga_txt_track` | Float | How much extra space to add between the title's letters when the row above is set to Custom. |

### Content / Design / Manual Overrides (Global) / Type

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Colour | `ga_colors_ctl` | Menu | Pins the neon color for every sign. |
| Colour | `ga_colors` | Menu | The neon color to force when the row above is set to Custom. |
| Font Class | `ga_fontclass_ctl` | Menu | Forces the general category of typeface, overriding whatever the name form would normally call for. |
| Font Class | `ga_fontclass` | Menu | The typeface category to force when the row above is set to Custom. |
| Font Style | `ga_font_ctl` | Menu | Prefers typefaces tagged with a particular style, such as stencil or gothic. |
| Font Style | `ga_font` | Menu | The style tag to prefer when the row above is set to Custom, for example stencil, gothic or futuristic. |
| Tube Gauge | `ga_gauge_ctl` | Menu | Forces the thickness of the neon tubing, from real stock sizes. |
| Tube Gauge | `ga_gauge` | Menu | The tube gauge to force when the row above is set to Custom, in millimetres of real stock tubing. |
| Tube Thickness | `ga_radius_ctl` | Menu | Scales the neon tube thickness up or down from its normal gauge. |
| Tube Thickness | `ga_radius` | Float | How much to scale the tube thickness when the row above is set to Custom. |
| Brightness | `ga_emit_ctl` | Menu | Scales how brightly every sign's neon glows. |
| Brightness | `ga_emit` | Float | How much to scale every sign's brightness when the row above is set to Custom. |
| Title Colour Policy | `ga_col_mode_ctl` | Menu | Controls how color is spread across the title's letters. |
| Title Colour Policy | `ga_col_mode` | Menu | How color is spread across the title when the row above is set to Custom. |

### Content / Design / Manual Overrides (Global) / Layout

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Named Layout | `ga_layout_ctl` | Menu | Pins every sign to one of the hand-built layout templates, and turns off the procedural layout generator so the pin actually sticks. |
| Named Layout | `ga_layout` | Menu | Which hand-built layout template to force when the row above is set to Custom. |
| Composition | `ga_arch_ctl` | Menu | Forces the logo lockup style. |
| Composition | `ga_arch` | Menu | The logo lockup arrangement to force when the row above is set to Custom - how the title, icon and decor are grouped together, generated rather than picked from a fixed template. |
| Alignment | `ga_align_ctl` | Menu | Forces which edge every text element on the sign lines up against. |
| Alignment | `ga_align` | Menu | Which edge to align every text element against when the row above is set to Custom. |
| Letter Swapped For Icon | `ga_glyph_ctl` | Menu | Forces one letter in the title to be swapped for a matching icon, or forbids it entirely (a donut for the O in DONUTS is the classic example). |
| Letter Swapped For Icon | `ga_glyph` | Menu | Whether to force a letter-for-icon swap when the row above is set to Custom, or forbid one. |
| Icon Presence | `ga_icon_ctl` | Menu | Scales how likely every sign is to carry an icon. |
| Icon Presence | `ga_icon` | Float | How much to scale the chance of an icon appearing when the row above is set to Custom. |

### Content / Design / Manual Overrides (Global) / Decor

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Decor Family | `ga_ornaments_ctl` | Menu | Restricts every sign's decor to one family, like arrows, stars or scallops. |
| Decor Family | `ga_ornaments` | Menu | Which decor family to restrict every sign to when the row above is set to Custom, for example frame, wave or bunting. |
| Background Decor | `ga_bg_ctl` | Menu | Forces the dim decor sitting behind everything else on the sign on or off. |
| Background Decor | `ga_bg` | Menu | Whether to force the background decor on or off when the row above is set to Custom. |
| Decor Count | `ga_decor_n_ctl` | Menu | Sets how many lines a multi-line decor element draws, such as a set of rays or a row of chevrons. |
| Decor Count | `ga_decor_n` | Menu | How many lines to draw when the row above is set to Custom, for any decor element made of repeated lines. |
| Decor Stroke Lines | `ga_strokes_ctl` | Menu | Draws decor lines as two or three parallel strokes instead of one. |
| Decor Stroke Lines | `ga_strokes` | Menu | How many parallel strokes to draw when the row above is set to Custom. |
| Dashed Decor | `ga_dash_ctl` | Menu | Scales how likely every sign's decor is to be dashed rather than solid. |
| Dashed Decor | `ga_dash` | Float | How much to scale the chance of dashed decor when the row above is set to Custom. |

### Content / Design / Manual Overrides (Global) / Hardware

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Backing | `ga_hw_l1_ctl` | Menu | Forces what kind of backing every sign hangs on. |
| Backing | `ga_hw_l1` | Menu | The backing type to force when the row above is set to Custom. |
| Part-Panel Division | `ga_hw_mix_ctl` | Menu | Forces how a Part panel backing divides the sign face into solid and open regions. |
| Part-Panel Division | `ga_hw_mix` | Menu | How the Part panel backing divides the face when the row above is set to Custom, for example a plate along the top, a band, or a plate behind the text only. |
| Bracing | `ga_hw_brace_ctl` | Menu | Forces the truss pattern inside each bay of a pipe grid backing. |
| Bracing | `ga_hw_brace` | Menu | The truss pattern to force when the row above is set to Custom, from a plain welded grid up to the classic named bridge trusses (Pratt, Howe, Warren) and a diagonal or ladder pattern. |
| Rivet Layout | `ga_hw_rivet_ctl` | Menu | Forces the layout of studs and rivets around the backing panel's edge. |
| Rivet Layout | `ga_hw_rivet` | Menu | Which stud pattern to force when the row above is set to Custom, from a plain perimeter run to a full grid. |
| Rim Frame | `ga_hw_frame_ctl` | Menu | Forces a rim around the backing - either standing proud of the face or returning back like a shallow cabinet - or removes it. |
| Rim Frame | `ga_hw_frame` | Menu | Whether to add a rim around the backing when the row above is set to Custom, and which way it runs. |
| Panel Edge | `ga_hw_edge_ctl` | Menu | Forces how the backing panel's edge is cut - flat, chamfered out, or chamfered in. |
| Panel Edge | `ga_hw_edge` | Menu | How the panel edge is cut when the row above is set to Custom. |
| Backing Size | `ga_hw_fit_ctl` | Menu | Forces whether the backing covers the whole sign box or is fitted tight around the neon it sits behind. |
| Backing Size | `ga_hw_fit` | Menu | Whether the backing covers the whole sign box or is fitted to the neon when the row above is set to Custom. |
| Sign Silhouette | `ga_hw_shape_ctl` | Menu | Forces the backing to follow a badge-style outline instead of a plain rectangle. |
| Sign Silhouette | `ga_hw_shape` | Menu | Which outline the backing follows when the row above is set to Custom, for example ellipse, hexagon, shield or starburst. |
| Member Section | `ga_hw_profile_ctl` | Menu | Forces the cross-section shape of every rig member on every sign. |
| Member Section | `ga_hw_profile` | Menu | The cross-section to force on every rig member when the row above is set to Custom - round tube or square section. |
| Sub-Frame | `ga_hw_l2_ctl` | Menu | Forces the shape of the sub-frame that sits behind the backing. |
| Sub-Frame | `ga_hw_l2` | Menu | The sub-frame shape to force when the row above is set to Custom. |
| Standoff Spacing | `ga_hw_l3pat_ctl` | Menu | Forces how the standoffs bolting every sign to the building are spaced out. |
| Standoff Spacing | `ga_hw_l3pat` | Menu | How the standoffs are spaced when the row above is set to Custom. |
| Standoff Count | `ga_hw_l3n_ctl` | Menu | Forces how many standoffs to try to build. |
| Standoff Count | `ga_hw_l3n` | Menu | How many standoffs to try to build when the row above is set to Custom. |
| Standoffs Reach For The Wall | `ga_hw_l3fan_ctl` | Menu | Forces whether standoffs are allowed to angle sideways to find the building, instead of only going straight back. |
| Standoffs Reach For The Wall | `ga_hw_l3fan` | Menu | Whether standoffs are allowed to angle sideways to reach the building when the row above is set to Custom, instead of only going straight back. |
| Minimal Run Count | `ga_hw_min_n_ctl` | Menu | Forces how many straight rails a Minimal runs backing uses. |
| Minimal Run Count | `ga_hw_min_n` | Menu | How many rails a Minimal runs backing uses when the row above is set to Custom. |
| Backing Margin | `ga_hw_margin_ctl` | Menu | Forces how much extra room the backing leaves around the neon it sits behind. |
| Backing Margin | `ga_hw_margin` | Float | How much extra margin the backing leaves around the neon when the row above is set to Custom, as a fraction of the sign's size. |
| Metal Tone | `ga_hw_grey_ctl` | Menu | Forces how light or dark the rig's metal color is. |
| Metal Tone | `ga_hw_grey` | Float | How light or dark the rig's metal tone is when the row above is set to Custom, from 0 (near black) to 1 (near white). |
| Electrical Boxes | `ga_hw_eb_n_ctl` | Menu | Forces how many transformer or driver boxes every sign carries. |
| Electrical Boxes | `ga_hw_eb_n` | Menu | How many electrical boxes to build when the row above is set to Custom. |
| Electrical Box Style | `ga_hw_eb_style_ctl` | Menu | Forces which kind of electrical box every sign carries. |
| Electrical Box Style | `ga_hw_eb_style` | Menu | The electrical box style to force when the row above is set to Custom. |
| Cable Runs | `ga_hw_cab_n_ctl` | Menu | Forces how many cable runs lead from the electrical box to the rig. |
| Cable Runs | `ga_hw_cab_n` | Menu | How many cable runs to build when the row above is set to Custom. |
| Roof Frame Count | `ga_hw_tr_n_ctl` | Menu | Forces how many support triangles hold up a rooftop sign. |
| Roof Frame Count | `ga_hw_tr_n` | Menu | How many support triangles to build when the row above is set to Custom. |
| Roof Frame Bracing | `ga_hw_tr_brace_ctl` | Menu | Forces the internal bracing pattern inside each rooftop support triangle. |
| Roof Frame Bracing | `ga_hw_tr_brace` | Menu | The bracing pattern to force inside each support triangle when the row above is set to Custom, from a bare triangle up to a fully cross-braced one. |
| Roof Frame Purlins | `ga_hw_tr_tie_ctl` | Menu | Forces whether the rooftop support triangles get longitudinal purlins tying them together. |
| Roof Frame Purlins | `ga_hw_tr_tie` | Menu | Whether to add purlins tying the support triangles together when the row above is set to Custom. |
| Frame Depth | `ga_hw_tr_base_ctl` | Menu | Forces how far a rooftop support triangle's base runs back across the roof. |
| Frame Depth | `ga_hw_tr_base` | Float | How far the support triangle's base runs back across the roof when the row above is set to Custom, as a multiple of the sign's own height. |

### Content / Design / Manual Overrides (Global)

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| VEXpression (Per Sign) | `vex_anchor` | String | Custom VEX over the sign anchors, before the engine decides what each sign is. |
| VEXpression Override | `vex_override` | String | Custom VEX code that runs over the sign plan after the engine has decided everything, before any geometry gets built. |

### Content / Build

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Real-World Scale | `unit_scale` | Float | Tells the asset how many scene units make up one metre, so it can build signs at real-world sizes. |
| Build Hardware | `hardware` | Toggle | Builds the metal rig behind each sign: the backing panel or pipe grid, the frame behind that, and the standoffs bolting it to the building. |
| Tube Detail | `tube_detail` | Menu | How finely the neon tubes are built. |
|   | `lod_preset` | Menu | One-click detail settings for how far the signs are from camera. |
| Hardware Colour | `hw_color` | Float | The colour every sign rig is painted - the backing, the frame, the standoffs and the cabling. |
| Enable Hardware Colour Range | `hw_color_var` | Toggle | Draw each sign rig colour from the ramp instead of using the one colour above. |
| Hardware Colour Range | `hw_color_ramp` | Ramp | Each sign takes one colour from this ramp, at random. |
| Enable Sizing Randomness | `size_rand` | Toggle | Varies the overall size of each placed sign a little, so a street does not look like the same box copied over and over. |
| Sizing Randomness | `size_rand_amt` | Float | How much size variation to use, as a percentage of the sign's own size. |
| Shape Variety | `shape_rand` | Toggle | Lets each sign take one of its type's authored proportions rather than the nominal one - a blade may come out square or tall, a marquee wide or deep. |
| Enable Deterioration | `decay` | Toggle | Ages the signs: letters go dark or start flickering, whole decor lines go out, the rig behind loses paint, and the odd frame piece goes missing. |
| Deterioration | `decay_amt` | Float | How run-down the street looks overall, as a percentage. |
| Flicker | `usd_flicker` | Menu | How fast the faulty tubes blink. |

### Render and Output / Solaris

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Send to Solaris | `render_send` | Button | Builds the Solaris setup for these signs: a SOP Import and a material library, wired together in /stage. |
| USD Root | `usd_root` | String | The name of the branch the signs are gathered under in the USD scene graph, so each one can be found, hidden or overridden on its own. |
| Sign Lights | `usd_lights` | Menu | Whether the signs light the scene around them, or only look bright themselves. |
| Build In | `usd_lopnet` | String | Which LOP network the Send to Solaris button builds into. |

### Render and Output / Output

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Name Attribute | `out_name` | Toggle | Puts a name on every piece of geometry, so a downstream SOP can address one sign without knowing anything about this asset. |
| Sign ID Attribute | `out_classid` | Toggle | Adds an integer id per sign, alongside the name. |
| Keep Colour (Cd) | `out_cd` | Toggle | Carries each sign's colour out on the geometry as Cd. |
| Keep Emission (emit) | `out_emit` | Toggle | Carries each sign's brightness out as emit. |
| Generate UVs | `usd_uv` | Toggle | Builds UVs so the signs can be textured. |
| Animate Flicker in SOPs | `out_flicker` | Toggle | Blinks the faulty tubes in SOPs as well as in the render. |

### Utilities

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Front Group | `front_group` | String | The name of the primitive group that marks which face is the FRONT on placeholder boxes you build by hand and wire into input 2. |
| Links | `website` | Button | Opens the JVtools website in your web browser - every tool, the docs and the store in one place. |
| Gumroad | `gumroad` | Button | Opens the Neonyte product page in your web browser. |
| Documentation | `docs` | Button | Opens the Neonyte documentation in your web browser. |
| Discord | `discord` | Button | Opens the JVtools Discord server in your web browser, for community and support. |
| YouTube | `youtube` | Button | Opens the JVtools YouTube channel in your web browser. |

### Signs

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
|   | `delete_all_signs` | Button | Removes every placed sign from the scene and clears the list below. |
| Delete Signs in Viewport | `delete_in_viewport` | Button | Hands the viewport an eraser brush: a red ball follows your cursor, and dragging with the left mouse button deletes every sign inside it. |
| Open / Close All Signs | `toggle_all_signs` | Button | Opens or shuts every sign card at once - whichever the list needs. |
| Find Sign | `sign_search_go` | Button | Asks you for a business name or a card number, then shuts every sign card except the ones that match. |
| Rebuild List from Signs | `rebuild_sign_list` | Button | Gives every sign already in the scene a card, for when the list below is empty but the signs are there. |

### Signs / Per-Sign / Sign #

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Sign | `psa_name#` | String | The name of the sign this card belongs to. |
|   | `psa_reroll#` | Button | Draws a fresh name, layout and color palette for this sign only - every other sign on the street stays exactly as it is. |
| Edit in Viewport | `psa_edit#` | Button | Picks this sign up in the viewport: it follows the surface again as a green placeholder and one click drops it in its new spot. |
| Zoom to Sign | `psa_zoom#` | Button | Frames this sign in the viewport, so you can see the one you are editing without hunting for it on the street. |
| Reset to Defaults | `psa_reset#` | Button | Clears this card's Note and the steering it applied, so the sign goes back to what the street-wide controls alone would produce. |
| Delete Sign | `psa_del#` | Button | Removes this one sign and its card. |
| Title | `psa_title#` | String | This sign's title. |
| Lock | `psa_title_lock#` | Toggle | Holds this title while everything else re-rolls. |
| Translation | `psa_trans#` | String | The English meaning of the title, when the title is written in another script. |
| Subtitle | `psa_sub#` | String | This sign's subtitle or catchphrase, on layouts that have room for one. |
| Business Group | `psa_group#` | String | Type the same word on two or more cards to make those signs read as one business - they will share a name, a color palette and matching lettering. |

### Signs / Per-Sign / Sign # / Transform

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Translate | `psa_t#` | Float | Where this sign sits in the scene. |
| Rotate | `psa_r#` | Float | This sign's orientation, in degrees. |
| Scale | `psa_scale#` | Float | A uniform size multiplier on this sign's placeholder box. |

### Signs / Per-Sign / Sign # / Adjustment Notes (This Sign)

| Parameter | Internal name | Type | What it does |
|---|---|---|---|
| Note | `psa_notes#` | String | The same vocabulary as the street-wide Adjustment Notes, for this sign only - 'make it a japanese bar', 'no icons or arrows', 'possessive name', 'film noir'. |
| Apply | `psa_apply#` | Button | Translates this sign's note into the constraints the engine reads, and reports what was understood. |
