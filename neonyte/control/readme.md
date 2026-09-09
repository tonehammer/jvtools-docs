# Control

Every decision Neonyte makes has a default. Press **Give me the Signs** with nothing else set and you get a complete street.

Three levels of control sit on top of those defaults: Adjustment Notes, the Advanced rows, and the VEXpression hooks. They reach the same decisions three different ways.

## The three levels

| Level | Where it lives | How exact | When to use it |
| --- | --- | --- | --- |
| Adjustment Notes | One text field in the Content tab | Changes how likely things are | Art-directing a whole street fast |
| Advanced rows | 52 rows in Manual Overrides (Global), street-wide | Sets one decision exactly | Pinning one decision for the whole street |
| A sign's card | The Note, Title, Subtitle and Business Group on each sign's card | Sets one sign | Steering one sign without touching the rest |
| VEXpression | Two fields, VEXpression (Per Sign) and VEXpression Override | Exact, per sign, can read the input geometry | Per-sign control, or anything driven by the geometry |

## Precedence

Each level overrides the ones above it. An override replaces the value rather than blending with it. A card whose Note says `yellow` beats a street-wide Colour row set to something else. The status bar says which control overrode a note.

| Order | Source | Effect |
| --- | --- | --- |
| 1 (weakest) | Theme preset | Sets the base weighting everything else starts from |
| 2 | Adjustment Notes | Merged over the theme |
| 3 | Street-wide Advanced rows | Overlay, replaces |
| 4 | The sign's own card (its Note, Title, Subtitle, Business Group) | Overlay, replaces |
| 5 | Pre-plan VEXpression `force_*` | Overlay, replaces - wins over everything above |
| 6 (strongest) | Post-plan VEXpression | Runs after everything, on the finished plan - the last word before geometry is built |

## Every control at a glance

Every control, and the three ways to reach it. A blank cell means that control cannot be reached at that level; hardware has no pre-plan VEXpression hook, so change hardware from the post-plan VEXpression Override instead.

| Section | Control | Parm | VEXpression | In a note |
|---|---|---|---|---|
| Aging | Deterioration | `decay` | `s@force_decay_mode` | fresh, immaculate, maintained |
| Aging | Deterioration Amount | `decay_amt` | `s@force_decay_amt` | abandoned, aged, battered, broken |
| Colour | Colour families | - | - | warmer, cooler, pastel, acid, jewel |
| Colour | One palette for the street | - | - | consistent, all the same, one palette |
| Content | Business Type | `ga_type` | `s@force_type` | adult, arcade, arcades, auto, only bars |
| Content | Era | `ga_era` | `s@force_era` | 1900s, 1910s, 1920s, 1930s |
| Content | Name Form | `ga_form` | `s@force_form` | acronym, acronyms, attested, categories |
| Content | Script | `ga_script` | `s@force_script` | arab, arabic, cantonese, cyrillic |
| Content | Theme | `theme` | `s@force_theme` | americana, brash, classy, cyber |
| Content | Title Auto-Fit | `ga_txt_fit` | `s@force_txt_fit` | fill the sign, leave the title alone |
| Content | Title Offset X | `ga_txt_offx` | `s@force_txt_offx` | nudge the title left, nudge the title right |
| Content | Title Offset Y | `ga_txt_offy` | `s@force_txt_offy` | nudge the title up, nudge the title down |
| Content | Title Rotate | `ga_txt_rot` | `s@force_txt_rot` | tilted, angled, slanted, level titles, straight titles |
| Content | Title Tracking | `ga_txt_track` | `s@force_txt_track` | tighter lettering, tight tracking, wider tracking, looser lettering, spaced out |
| Decor | Background Decor | `ga_bg` | `s@force_bg` | background decor, a backdrop |
| Decor | Dashed Decor | `ga_dash` | `s@force_dash` | dashed, dotted |
| Decor | Decor Count | `ga_decor_n` | `s@force_decor_n` | busier, busy, busiest, simplest, sparse |
| Decor | Decor Family | `ga_ornaments` | `s@force_ornaments` | arrow, arrows, badge, badges |
| Decor | Decor Stroke Lines | `ga_strokes` | `s@force_strokes` | thicker decor lines, thin decor lines |
| Hardware | Backing | `ga_hw_l1` | - | panel, panels, plate, backboard, scaffolding |
| Hardware | Backing Margin | `ga_hw_margin` | - | tight margin, generous margin |
| Hardware | Backing Size | `ga_hw_fit` | - | fitted backing |
| Hardware | Bracing | `ga_hw_brace` | - | trussed, cross braced |
| Hardware | Cable Runs | `ga_hw_cab_n` | - | cable, cables, clean mounts, tidy mounts |
| Hardware | Electrical Box Style | `ga_hw_eb_style` | - | driver brick, led panel box |
| Hardware | Electrical Boxes | `ga_hw_eb_n` | - | electrical box, junction box |
| Hardware | Frame Depth | `ga_hw_tr_base` | - | deep frame, shallow frame |
| Hardware | Member Section | `ga_hw_profile` | - | square section |
| Hardware | Metal Tone | `ga_hw_grey` | - | dark metal, pale metal, bright metal |
| Hardware | Minimal Run Count | `ga_hw_min_n` | - | one run, two runs, three runs |
| Hardware | Panel Edge | `ga_hw_edge` | - | outset edge, inset edge, square edge |
| Hardware | Part-Panel Division | `ga_hw_mix` | - | top plate, bottom plate, left plate, right plate, band plate |
| Hardware | Rim Frame | `ga_hw_frame` | - | rim frame |
| Hardware | Rivet Layout | `ga_hw_rivet` | - | rivet, rivets |
| Hardware | Roof Frame Bracing | `ga_hw_tr_brace` | - | roof bracing |
| Hardware | Roof Frame Count | `ga_hw_tr_n` | - | roof frame |
| Hardware | Roof Frame Purlins | `ga_hw_tr_tie` | - | purlins |
| Hardware | Sign Silhouette | `ga_hw_shape` | - | rect shaped, rect signs, ellipse shaped, ellipse signs, rounded shaped |
| Hardware | Standoff Count | `ga_hw_l3n` | - | standoff, standoffs, spacers |
| Hardware | Standoff Spacing | `ga_hw_l3pat` | - | evenly spaced standoffs, standoffs in pairs |
| Hardware | Standoffs Reach For The Wall | `ga_hw_l3fan` | - | legs to the wall, standoffs to the wall |
| Hardware | Sub-Frame | `ga_hw_l2` | - | spine frame, cross frame, ladder frame |
| Layout | Alignment | `ga_align` | `s@force_align` | centred titles, centered titles, left aligned, right aligned |
| Layout | Composition | `ga_arch` | `s@force_arch` | horizontal lockup, wordmark, split composition, mark only, emblem composition |
| Layout | Icon Presence | `ga_icon` | `s@force_icon` | icons, symbols, no icons |
| Layout | Letter Swapped For Icon | `ga_glyph` | `s@force_glyph` | letter swap, swap a letter, letter for an icon |
| Layout | Named Layout | `ga_layout` | `s@force_layout` | underlined, framed, with borders, bordered |
| Modifier | Scale that strength | - | - | a bit, slightly, very, way, max |
| Modifier | Strength of a clause | - | - | no, fewer, more, mostly, only |
| Scope | Aim at a trade | - | - | yellow on the bars, red for the diners |
| Scope | Aim at part of the street | - | - | big signs, the vertical ones, rooftop signs, every other sign |
| Scope | Everything but | - | - | except, apart from, other than |
| Type | Brightness | `ga_emit` | `s@force_emit` | blazing, blinding, bright, brighter |
| Type | Colour | `ga_colors` | `s@force_colors` | amber, amethyst, apricot, aqua, only red |
| Type | Font Class | `ga_fontclass` | `s@force_fontclass` | army, bold, cursive, deco |
| Type | Font Style | `ga_font` | `s@force_font` | army, bold, cursive, deco |
| Type | Title Colour Policy | `ga_col_mode` | `s@force_col_mode` | one colour per sign, one color per sign, single colour, single color, one colour titles |
| Type | Tube Gauge | `ga_gauge` | `s@force_gauge` | lightest gauge, fine gauge, medium gauge, fat gauge, heaviest gauge |
| Type | Tube Thickness | `ga_radius` | `s@force_radius` | beefy, bolder, boldest, bulky |

## Which one do I want

- **Adjustment Notes** to art-direct a whole street fast, in plain language, without opening a single folder.
- **An Advanced row** to pin one decision exactly across the street, when a note does not give you a strong enough guarantee. For one sign, use its card's Note.
- **A VEXpression** for exact per-sign control, for a decision the rows and notes do not cover, or for anything that has to be driven by the input geometry itself rather than by a fixed rule.

## In this section

- [VEXpression](vexpression.md) - the two script hooks and what each one reaches.
- [Advanced rows](advanced.md) - the 52 street-wide and per-sign controls.
- [Adjustment Notes](notes.md) - the plain-language steering vocabulary.
- [Defaults and weights](defaults.md) - what the engine does with nothing set.
