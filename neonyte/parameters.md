# Parameters

!!!danger Provisional — v0.9
Neonyte's control surface is still being built and rearranged. This page describes the controls **by function and by tab**, not as a frozen list of internal names — some of these are still moving between tabs and some labels will change before release. The node's own **tooltips are the source of truth**; this reference syncs from them once the surface settles.
!!!

The controls are organised into a tab strip. The everyday ones live in **Setup**; deeper tuning is in **Advanced**; per-box control is in **Signs**; and the store/docs links plus a few globals are in **Utilities**.

## Setup

The controls you reach for on every sign wall.

| Control | What it does |
| --- | --- |
| **Give me the Sign** | The master button. Regenerates every sign from a fresh draw (it advances the Seed). This is where Adjustment Notes are translated and applied. |
| **Seed** | The number the whole result derives from. Set it by hand to return to a result you liked; the button changes it for you. Determinism is a feature — same seed, same signs. |
| **Adjustment Notes** | A plain-language steer applied on the next press ("fewer icons, no yellow, only 1950s-style names"). Understood clauses are applied; unrecognised ones are reported rather than silently dropped. |
| **Theme** | A preset that re-weights types, palettes, fonts and templates (Classic Americana / Vegas Strip / Cyberpunk / Noir / Modern Minimal), or None. |
| **Real-World Scale** | Sizes the physical elements (tube gauges, hardware, standoffs) to your scene's units, so a 50 mm tube reads as 50 mm. |
| **Hardware** | Turns the procedural metalwork (backing, sub-frame, standoffs) on or off. On by default; ships as its own `hardware` primitive group. |

## Advanced

Global tuning below the everyday controls — content and typography weighting, decoration behaviour, and the finer knobs behind the defaults. This tab is still being organised for v0.9; lean on the tooltips here more than anywhere else.

## Signs — per-box control

A tabbed panel with **one entry per input box** (shown as tabs so a large street doesn't stretch the parameter pane). Each entry lets you touch a single sign without disturbing the others.

| Per-box control | What it does |
| --- | --- |
| **Box** | Which input piece this entry drives (the tab is named from the box's own `name` attribute where it has one). |
| **Variation** | Re-rolls just this sign — a new draw for this box only, leaving every other sign untouched. |
| **Title** / **Subtitle** | Hand-edit the words. A text override changes what the sign says without reshuffling its layout, colours or seed. |
| **Translation** | A read-only gloss of a non-Latin name, where one applies. |
| **Notes** | Per-sign Adjustment Notes, applied to this box only. |
| **Advanced** | Per-sign overrides: pin the type, colours, layout family, ornaments, font, script, icon amount, brightness, tube gauge or dashing. A per-sign override beats this sign's notes. |

!!!info How the panel stays in sync
Pressing the master button keeps your per-box edits: entries are rebuilt only when the set of boxes actually changes, and hand-edited titles survive a re-press. Editing a title is a text-only override — it never reshuffles the sign.
!!!

## Utilities

Globals that aren't part of the everyday flow, plus the links and version readout.

| Control | What it does |
| --- | --- |
| **Front Group** | The name of the primitive group marking each box's front face. Default `front`. Only matters for hand-authored box input — the interactive placement tool names this group itself. |
| **Links** | Buttons to the store page, this documentation, the community Discord, and the YouTube channel. |
| **Current Version** / update notice | Shows the installed version and flags when a newer one is available on the store. |

## The viewer state — Place Sign in Viewport

Not a parameter, but a tool on the node: an interactive way to drop and aim a single sign on a surface, roll it, and nudge it. It has its own on-screen controls and menu (right-click), and **Shift+X** resets a placement. See [Getting Started](getting-started.md#place-a-sign-by-hand).
