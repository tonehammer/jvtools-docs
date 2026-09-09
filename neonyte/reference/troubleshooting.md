---
icon: tools
order: 80
---

# Troubleshooting

## No signs appear after pressing the button

Check three things: that you have actually placed a sign, that any hand-built boxes are wired into input 2 and not input 1 (input 1 is the building geometry and passes through untouched), and that each hand-built box carries a front-face group.

## Signs show colour but no glow

The colour in the viewport is a preview. The glow is only visible in a Karma render - press **Send to Solaris** and render.

## Rendered signs are dark

Check **Keep Colour (Cd)** and **Keep Emission (emit)** are both on. Check the material library has not been deleted. Press **Send to Solaris** again to rebuild it.

## Tubes or signs are the wrong size

Set **Real-World Scale** to match your scene's units: 1 for metres, 100 for centimetres, 3.28 for feet.

## Standoffs are missing

A standoff only builds where it finds a building surface within reach. **Standoff Count** sets how many a sign tries to build; only the ones that actually find a surface get built.

## A note did nothing

Press **Give me the Signs**, or **Apply** on a card, to apply a note - typing it alone does nothing until you do. Read the status bar for what was understood and what was not. A card's Note or a Manual Override can beat a street-wide note; the status bar says which one did. A scope phrase like "big signs" needs an instruction paired with it - "red on the big signs" works, "big signs" alone does not.

## A force attribute in the pre-plan VEXpression stripped every other sign

You wrote a numeric type instead of a string. Every force attribute is a string, including the numeric-looking ones. See [VEXpression](../control/vexpression.md).

## A force did nothing

Check the spelling against the Advanced row's own values. An unparseable value is ignored rather than guessed at.

## The scene is slow while placing signs

Turn on **Placeholder Boxes Only**, or press **B** in the viewport, while you lay out a street. Lower **Tube Detail** for a heavier scene.

## The node cooks on every frame

Check **Animate Flicker in SOPs**. Turning it off moves the blink back into the material, and the node stops being time dependent.

## The Signs list is empty but signs exist in the scene

Press **Rebuild List from Signs** to give every sign already in the scene a card.

## A Done Editing button appeared

An edit was started and not finished. Press it to call off the edit.
