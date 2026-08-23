# Getting Started

Neonyte is a **SOP** — it lives inside a Geometry object and works on geometry you feed it. That geometry is a set of **placeholder boxes**: one box per sign, positioned, sized and oriented where you want a sign on your building, with its **front face** marked.

## The input contract

Each piece of the input is treated as one sign:

- **One box = one sign.** Neonyte connectivity-splits the input, so any set of separate boxes works — a hand-placed row, boxes scattered on a facade, whatever your layout tool produces.
- **Mark the front face.** Each box needs a primitive **group** naming the face the sign should point out of. By default this group is called **`front`**; you can change the name in **Utilities → Front Group**. The front face fixes both the sign's facing direction and its up direction.
- **Size and aspect matter.** The box's proportions influence which layout templates are eligible — a tall narrow box tends to get vertical lettering, a wide box a banner layout.
- **Unmarked pieces are skipped.** A piece with no front group is silently ignored and passes through untouched, so you can mix boxes and other geometry.

The placeholder box itself is **deleted** once its sign is built — the output is signs (plus optional hardware), not your boxes.

!!!info Why boxes?
In v1 the box is a deliberately simple, unambiguous way to say "put a sign here, this big, facing this way." Smarter input analysis (auto-detecting faces, per-piece bounding boxes, shrinkwrap) is a later design question — for now, boxes with a front group are the contract.
!!!

## Your first street

>>> 1. Make some boxes
Create a few boxes inside a Geometry object. Give each one a primitive group named **`front`** on the face that should face the street. (A quick way: a Group SOP by normal, or by bounding region on the front face.)
>>>
>>> 2. Drop the node
Append a **Neonyte** SOP after your boxes.
>>>
>>> 3. Press the button
Press **Give me the Sign**. Every fronted box is replaced by a generated neon sign — name, icon, colours, layout and hardware.
>>>
>>> 4. Roll again
Press it again for a completely different set of signs. The **Seed** value is what changes; set it by hand to return to a result you liked.
>>>

## See the glow

The viewport shows each sign in its neon colour, but the **emission** — the HDR glow that makes neon read as neon — is a Karma material. To see it lit:

- Import the Neonyte SOP into a **Solaris (LOP)** stage with **SOP Import**, and make sure it **creates material bindings** (the bind option is off by default, so nothing shades until you turn it on).
- Add a light (even a dim dome) and render with **Karma**. The signs emit; the rest of the scene reads them as light sources.

## Set your scale

Neonyte's hardware, tube gauges and standoffs are sized in real-world units. If your scene isn't in metres, use **Real-World Scale** so a 50 mm tube reads as 50 mm rather than filling the whole sign.

## Place a sign by hand

Beyond feeding boxes, you can drop and aim a single sign interactively with the **Place Sign in Viewport** tool (a viewer state on the node). It lets you position a sign on a surface, roll it, and nudge it — handy for one-off hero placements or fixing a box that landed awkwardly. The on-screen tool shows its own controls; a right-click opens its menu, and **Shift+X** resets a placement.

!!!warning Pre-release note
The exact button labels, the Front Group location, and the viewer-state hotkeys are still settling for v0.9 — if something here doesn't match your build, trust the node's own tooltips (they are the source of truth these docs sync from).
!!!
