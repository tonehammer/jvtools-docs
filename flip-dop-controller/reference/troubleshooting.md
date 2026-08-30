---
icon: question
order: 80
---

# Troubleshooting

**"Nothing to connect"** — no DOP Network set and no Add Linked SOPs rows. There is genuinely nothing to write to.

**"No FLIP Solver found" / "No FLIP Object found"** — three causes. Discovery looks at the dopnet's **direct children**, so a solver inside a DOP subnet is missed. Or it is a SOP FLIP setup (see below). Or the path points somewhere unexpected.

**"The DOP Network path does not resolve"** — the path points at a node that does not exist. Distinct from an empty path, which is a valid SOP-only setup.

**I use the SOP FLIP nodes** — not supported directly. What works: leave DOP Network empty and add **Add Linked SOPs** rows for your `flipcontainer` and `flipsolver` SOPs, which carry `particlesep` and `gridscale` under those names. They hold those values independently, so you need a row for each. Substeps, CFL and the bounding box cannot be driven this way.

**The container box vanished** — guide geometry only draws while its node is current. Select the controller again.

**Connect took over an expression I wrote** — by design, and it said so in the report. Untick that parameter's **Link** checkbox to leave it alone. Unlink is the conservative direction and would have left yours alone.

**A Linked SOPs row says "NOT FOUND"** — the named parameter does not exist on that SOP, usually a node-version difference. Hover the parameter in the SOP's own panel to get its internal name.

**Unticking Link switched my parameter off** — it did not. Link only decides whether Connect includes it.

**Status is out of date** — it records the last Connect or Unlink. Press either to refresh.

**Time Scale slowed something that is not the fluid** — expected. It scales the whole DOP Network.

**The node is not in the Tab menu** — check the `.hdalc` is in `Documents/houdini22.0/otls/` and that you have refreshed asset libraries. If Houdini refuses the file, check your licence: `.hdalc` is Indie/Apprentice only.

---

Still stuck? Find me on the JVtools Discord — the invite link is in the **Utilities** folder on the HDA node.
