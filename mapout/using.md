# Using MAPout

## How it fits together

Copernicus makes one flat image, the **canvas**, at the Setup's Canvas Resolution. Shapes are drawn in that canvas's space. MAPout only decides where the canvas lands on the wall.

Build COP Network and Output lays out three nodes:

| Node | What it holds |
|---|---|
| **MAPout Setup** | the canvas resolution, the mapping (corners, mesh, rotation, multi-projector) and the shapes |
| **COP Network** | your artwork, plus the rows Sync builds for each shape |
| **MAPout Output** | the projector window: screen, blackout, test pattern, flips and grade |

The Output's two inputs are addresses only: input 1 says which COP Network to show, input 2 which Setup's mapping to use. It never cooks the COP network to find it.

The warp is done in the projector window's own shader, perspective-correct per pixel, so it costs nothing per frame. The COP network never learns the projector exists, so the same network works on any wall.

## The corner pin

The four corners are where the canvas's corners sit on the projector, as fractions of the screen (0 to 1, top left origin). On a flat wall four corners are exact: a projector throwing onto a plane is a perspective transform, and four point pairs define it completely.

With **Edit Mapping** on and the **Warp** tool, drag the corners on the wall. The calibration grid is the check:

- **Equal cells** mean the perspective is right.
- **A round circle** (Visualization ▸ Circle) means the pinned area has the canvas's aspect. If it draws as an ellipse, either pin to a wall area with the canvas's proportions, or change the Canvas Resolution to match the area.

**Shift-drag** a corner to scale the whole image from the opposite corner, **Shift+Alt-drag** to scale from the centre. **1–4** picks a corner, **Tab** steps to the next point, and the **arrow keys** nudge by one projector pixel (Shift ×10, Ctrl ×0.1) at any zoom. **Edge Feather** fades the image out toward its edges.

## Rotation

**Rotation** turns the whole image on the wall about a pinned corner or the image's centre. The corners, the mesh and the shapes turn with it.

## Mesh warp

On a surface that is not flat (curtains, a corner, a curved wall), turn on **Mesh Warp**. A lattice of diamond points appears inside the corner pin: the corners still do most of the work, and the interior points take the bend. Drag them with the Warp tool, or drag on empty space to select several with a box or lasso and move them together. **Reset Mesh** puts every point back.

On a flat wall, leave it off.

## Drawing shapes

Shapes are drawn on the projection with the pointer on the wall:

| Tool | Key | How |
|---|---|---|
| **Rectangle** | R | drag; Shift for a square, Alt from the centre |
| **Ellipse** | O | drag; Shift for a circle, Alt from the centre |
| **Polygon** | P | click for a corner point, drag for a smooth Bezier point; click the first point, double-click or press Enter to close |

Points snap to other shapes' points and the canvas corners, so faces that meet share their corners exactly. Hold Ctrl to place freely.

With the **Select** tool (V) you can:

- click, Shift-click or drag a box or lasso to select shapes;
- drag a shape to move it, or drag its points, Bezier handles or box corners;
- drag just outside a corner of the selection to rotate it (Shift for 15° steps);
- double-click or press F2 to rename a shape — its COP row is renamed with it;
- press **Del** to delete, **Ctrl+D** to duplicate, the arrow keys to nudge;
- press **C** to edit the shape with Houdini's own Curve tool in the viewport.

Every shape is an ordinary SOP inside the Setup's Shapes network (**Go to Shapes Network**), wired into `ALL_SHAPES`. You can build a shape there by hand from any SOPs; it is listed and masked like a drawn one.

## Masks

A masked shape is black on the wall, whatever the COPs do. Mask a drawn shape with the **M** chip on its label, or the M key. **Mask Group** also masks hand-made primitives by group name. **Mask Feather** softens the edges.

## The COP network

Press **Sync Shapes to COPs** after drawing. Every unmasked shape gets a row in the COP Network:

| Node | What it is |
|---|---|
| `mapout_uv` | a subnet that makes every face's UV, one output per shape |
| `ART_<name>` (pink) | where the shape's artwork starts. Its **UV Scale**, **UV Offset** and **UV Rotate** parameters move the UV |
| `<name>_content` | a placeholder checker; replace it with your own nodes |
| `SHAPE_<name>` (teal) | where the shape's artwork ends |
| `mapout_composite` | a subnet that masks each shape and lays them over one another |
| `OUT` (red) | the image the projector shows |

Build each face's look between its `ART_` and `SHAPE_` nulls. Press Sync again after drawing or deleting shapes: new shapes get rows, deleted ones lose theirs, and the rest keep their artwork.

### UV

A four-corner face gets a **perspective UV** from its own corners: content mapped onto the face of a box looks right on the box. Any other shape gets a **box UV** from its bounding box; select it and drag the orange corners of its UV frame onto the surface. A four-point face with a corner close to straight (over 150°) is close to a triangle, so it gets a box UV too. Press **U** to switch a face between the two.

The projector cannot see a face's real proportions, so set its aspect with **UV Scale** on its `ART_` null.

**Show UV Check** puts a numbered, coloured grid on every face instead of its artwork, so you can check which way up each face is and whether it stretches. It uses SideFX Labs' UV Grid Texture; without Labs it falls back to a plain checkerboard. It costs nothing while off.

### Group layers

**Add Group Layers** makes a row for a group of shapes (**COP Group**, `*` for all of them) after the composite: a pink `ART_group_<name>` null carrying the image as it is at that point and a teal `GROUP_<name>` null. An effect built between them lands inside the group only. The group's utils subnet holds its mask, a per-face ID and an SDF measuring the distance to each face's edge — the raw material for effects that run across a whole group.

### Geometry in the canvas frame

**Shapes to Geometry** puts the synced shapes beside the Setup as flat polygons in the COP network's own frame (X −1 to 1, Y ±height/width), so geometry you make from them rasterizes exactly where the shapes are. **Snap View** points the viewport straight at that frame, and **Make Camera** also makes an orthographic camera with the same view.

## More than one projector

Use one Setup and one Output per projector, all reading the same COP Network (point each Output's first input at it). On each Setup, turn on **Multi-Projector**:

- **Canvas Region** is the part of the canvas this projector shows (0 to 1, top left origin). Two projectors side by side might show 0–0.55 and 0.45–1.
- **Edge Blend** fades the overlapping edges so the two projectors add up to one even image. Enter the overlap width on the overlapping side of **both** Setups.
- **Blend Curve** corrects a projector whose response is not sRGB: raise it if the overlap reads bright, lower it if it reads dark.

The **Exposure** and **Gamma Trim** on each Output match the two projectors' brightness.

## With RPLidar In

[RPLidar In](../rplidar-in/README.md) maps a sensor's touches onto the canvas; MAPout maps the canvas onto the wall. They are separate jobs, and the order matters: **warp first, then calibrate RPLidar In.** Once the canvas is a true rectangle on the wall, set RPLidar In's Output Space to Canvas and run its Placement as usual. Re-warping later moves the canvas on the wall, so RPLidar In's corners have to be touched again.

## Speed

The Output's **Status** field reports the measured time to read one frame off the COP network and the frame rate that implies. That ceiling is the COP network's own cost: if it is too low, lower the Canvas Resolution. With the output open, the Setup's **Playground** field says how many projector pixels the pinned image really covers; a canvas much bigger than that cooks pixels the wall never shows.
