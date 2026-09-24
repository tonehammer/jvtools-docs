# Troubleshooting

**"No FLIP Solver found" / "No FLIP Object found"** — three causes. Discovery looks at the dopnet's **direct children**, so a solver inside a DOP subnet is missed. Or it is a SOP FLIP setup (see below). Or the path points somewhere unexpected.

**I use the SOP FLIP nodes** — not supported directly. What works: leave DOP Network empty and add **Add Linked SOPs** rows for your `flipcontainer` and `flipsolver` SOPs, which carry `particlesep` and `gridscale` under those names. They hold those values independently, so you need a row for each. Substeps, CFL and the bounding box cannot be driven this way.

**Connect took over an expression I wrote** — by design, and it said so in the report. Untick that parameter's **Link** checkbox to leave it alone. Unlink is the conservative direction and would have left yours alone.

---

Still stuck? Find me on the JVtools Discord — the invite link is in the **Utilities** folder on the HDA node.
