---
icon: zap
order: 40
---

# Live Simulation (POP Network)

RPLidar In's point cloud is ordinary SOP geometry, so it can feed any solver — POPs, Vellum, or your own network. The **Create POP Network** button sets up a working example for you in one click.

## Create POP Network

Press **Create POP Network** and the node builds a ready-to-run POP network below itself, wired to the **solver-ready output** (Output 1, guides stripped) with sensible presets for live work. It also drops a small green helper control — the **`_run` null** — for driving everything.

## The _run helper

The helper is a null with three buttons. It is **not required** — the RPLidar In node generates points on its own, and you can play the timeline and toggle Live Nodes by hand — but it wires the common actions together:

| Button | What it does |
| --- | --- |
| **Start (Live)** | Sets RPLidar In to **Live**, plays the timeline, and enables **Live Nodes** (continuous cook) — starting the live simulation in real time. |
| **Stop** | Stops playback, disables Live Nodes, and sets RPLidar In back to **Off** (which also stops the sensor motor). |
| **Reset Sim** | Presses **Reset Simulation** on the POP network, clearing the current particles so it re-seeds. |

## Two ways to run the sim

* **Real time (Live):** Mode = Live + timeline playing + Live Nodes on. The solver advances against the live sensor as fast as it can cook. Best for interactive installations.
* **Over a frame range (Playback):** Mode = Playback against a recording. The sim steps frame by frame, so you can scrub, cache, and render a repeatable result.

## Building your own

There's nothing special about the generated network — you can wire the node's **Output 1** into any solver's source. Output 1 is the clean point cloud with all visualization guides removed, so it's safe to feed directly. See [Output & Attributes](output.md) for the per-point attributes you can read (`quality`, `angle`, `dist`).
