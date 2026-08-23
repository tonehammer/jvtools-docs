# Using Neonyte

This page is the "why it does what it does" tour — the systems behind the signs and the levers you have over them. If you just want to make signs, [Getting Started](getting-started.md) is enough; come here when you want to steer the result.

## Content — the names and icons

The single most important thing Neonyte does is make signs that **don't smell generated**. The trap it's built to avoid is what you get from naive randomness — "Gray Foot Cafe / Black Skull Bistro / Yellow Snake Restaurant" — where every name has the same shape and the register is all over the place.

The way out is that the **business type is drawn first**, and it drives everything after it:

- **The name form follows the type, with realistic weights.** Real streets are full of category-only signs (`LIQUOR`, `DINER`, `PIZZA`, `OPEN 24 HOURS`), possessives with real surnames (`Katz's`), toponyms (`Havana Club`), single evocative words (`Stardust`, `Orpheum`), foreign-language names keyed to cuisine, and the occasional invented-but-pronounceable word. Whimsical `The Blue Ox` names exist but are capped low — they're a spice, not the dish.
- **Not every sign gets both text and an icon.** An icon-only martini glass is a bar; text-only is half of every real street.
- **Names come from real material.** The banks are curated with a frontier model at authoring time and cross-checked against public-domain corpora — Wikidata venue names, NYPL and other city directories, photographed sign archives, census name-frequency data — plus a character-level model derived from tens of thousands of real establishment names for the invented-word slot.
- **No repeats where it counts.** Names are de-duplicated within a building, and the name *forms* are varied too (you won't get four possessives in a row). Across Randomize presses the space is combinatorially huge, so repetition is rare without any saved state.

You don't drive any of this directly under normal use — it's the default behaviour. You *bias* it with themes and Adjustment Notes (below).

## Layout — templates and armatures

Where the lettering, subtitle, icon and decoration sit is decided by a **layout template**. There are dozens of hand-authored ones plus a **procedural generator** that composes fresh lockups, and the box's aspect ratio partially decides which are eligible.

Layouts are built from **slots**:

- **Text** (the title), **subtitle** (an optional second line, usually a different font — `FINE FOOD · COCKTAILS`, `EST. 1952`), **icon**, and **armature**.
- **Armatures** are the decorative tubes: ovals, lozenges, underlines, frames, arrows, plus background kinds (grids, lattices, scallops, rays, chevrons, bulb rows) that sit *behind* everything at a weaker glow, and entrance arrows that point down toward the door.
- **Depth layering, not intersection.** When a script name sweeps across an oval badge, Neonyte doesn't try to trim curves — it stacks the tubes at slightly different depths, exactly the way real neon does. Overlap in 2D, resolved by Z.

There's also **glyph substitution** — the classic neon trick of an icon replacing a letter (a donut as the O in DONUTS, a martini glass as the I). It's probability-gated so a street doesn't overdo it.

!!!tip Reading a layout
Icons and armatures aren't decoration for its own sake — they carry the type. A dim background lattice or a bulb border reads as "old marquee"; a down-arrow reads as "entrance here". If a street feels too busy or too plain, the Adjustment Notes below are the fastest lever.
!!!

## Colour and glow

Each sign gets a **neon palette** — a primary and secondary picked from classic neon hues, biased by the business type. Text usually takes the primary; armatures and icons take the secondary. The colour drives two things: the **viewport `Cd`** so you can read the sign without rendering, and a per-sign **emission scale** that gives Karma a real HDR glow, brighter on the title than on the dim background armatures.

## Hardware

Turn **Hardware** on (it's on by default) and every sign gets the metalwork that would actually hold it to a building, in three levels:

- **Level 1 — backing:** a plate, a pipe grid, or a mix, sized to the sign rather than the whole box (so it doesn't read as machine-made), with truss bracing patterns and rivets. Solid sheet backings are deliberately rare — most signs are open truss.
- **Level 2 — sub-frame:** a simpler spine/cross/ladder/grid sitting behind level 1.
- **Level 3 — standoffs:** the brackets that hold the sign off the wall. Their direction is derived from the geometry — a leg raycasts back toward the building, and **a leg that finds nothing within reach is not built**, so signs don't attach to thin air. Signs stand proud of the facade on real brackets rather than sitting flush.

Hardware ships as its own `hardware` primitive group, so you can shade it, isolate it or blast it separately.

!!!warning A placement caveat
Hardware that reaches back to the building is computed at placement time. Signs already sitting in your scene keep their baked positions and hardware until they're re-placed or nudged — re-run placement after moving a building.
!!!

## Steering — themes and Adjustment Notes

Two levers re-weight what Neonyte generates, without breaking determinism:

- **Themes** — a menu of presets (Classic Americana, Vegas Strip, Cyberpunk, Noir, Modern Minimal) that bias type weights, palettes, fonts and templates. Pure data, instant.
- **Adjustment Notes** — a plain-language string like *"fewer icons, no yellow, only 1950s-style names"* or *"all strip clubs"* or *"only weather-based names"*. It's read when you press the button, translated into constraints, and applied to the whole street.

The important part of the contract: translation happens **in the button press, never in the cook**, so your scene still reloads and renders deterministically on a farm. Notes that can't be understood are reported rather than silently ignored — if a clause did nothing, Neonyte tells you.

!!!info How much it understands
Adjustment Notes are handled by a layered matcher — a rule parser for the common phrasings, a semantic sentence-matcher for the rest, and (optionally) a local model. It handles quantifiers ("no / fewer / more / only"), colours, business types, fonts, scripts/languages, decoration, era and brightness. Negation is handled ("not so many little pictures" turns icons down).
!!!

## The Signs panel — per-box control

When you want to touch individual signs rather than the whole street, the **Signs** panel gives you one entry per box (shown as a tab so a big street doesn't stretch the pane). For each box you can:

- **Re-roll** just that sign (a "Variation") without disturbing the others.
- **Edit the title and subtitle** by hand — a text override that changes the words without reshuffling the sign's layout or colour.
- See the **Translation** of a non-Latin name (read-only), where one applies.
- Open **Advanced** for per-sign overrides — pin the type, colours, layout family, ornaments, font, script, icon amount, brightness, tube gauge or dashing. A per-sign override beats that sign's notes.

## Multi-script names

Names and subtitles can appear in **Japanese, Chinese, Cyrillic and Arabic** as well as Latin scripts, keyed to type and steerable ("japanese signs"). The text pipeline carries Unicode end to end; Arabic is pre-shaped at authoring time because the Font SOP doesn't do OpenType shaping or right-to-left on its own.

!!!warning Pre-release note
Everything on this page is real and working in v0.9, but the breadth is still growing and some controls are still moving between tabs. Where a control's exact name or home differs from this page, the node's own tooltips win.
!!!
