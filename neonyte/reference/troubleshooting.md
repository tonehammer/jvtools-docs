# Troubleshooting

**No signs appear after pressing the button** — check three things: that you have actually placed a sign, that any hand-built boxes are wired into input 2 and not input 1 (input 1 is the building geometry and passes through untouched), and that each hand-built box carries a front-face group.

**Signs show colour but no glow** — the colour in the viewport is a preview. The glow is only visible in a Karma render - press **Send to Solaris** and render.

**Rendered signs are dark** — check **Keep Colour (Cd)** and **Keep Emission (emit)** are both on. Check the material library has not been deleted. Press **Send to Solaris** again to rebuild it.

**Tubes or signs are the wrong size** — set **Real-World Scale** to match your scene's units: 1 for metres, 100 for centimetres, 3.28 for feet.

**A note did nothing** — press **Give me the Signs**, or **Apply** on a card, to apply a note - typing it alone does nothing until you do. Read the status bar for what was understood and what was not. A card's Note or a Manual Override can beat a street-wide note; the status bar says which one did. A scope phrase like "big signs" needs an instruction paired with it - "red on the big signs" works, "big signs" alone does not.

**The scene is slow while placing signs** — turn on **Placeholder Boxes Only**, or press **B** in the viewport, while you lay out a street. Lower **Tube Detail** for a heavier scene.

**The Signs list is empty but signs exist in the scene** — press **Rebuild List from Signs** to give every sign already in the scene a card.

---

Still stuck? Find me on the JVtools Discord — the invite link is in the **Utilities** folder on the HDA node.
