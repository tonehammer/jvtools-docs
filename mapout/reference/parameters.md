---
icon: sliders
order: 110
---

# Parameter reference

MAPout is two nodes. The **MAPout Setup** has five tabs — Canvas, Mapping, Shapes, Visualization and Utilities. The **MAPout Output** has one. Listed here in panel order.

## MAPout Setup

### Canvas

| Parameter | Default | What it does |
|---|---|---|
| **Canvas Resolution** | 1920 × 1080 | The size of the image the COP Network makes, in pixels. Start from the projector's own resolution. The COP Network follows it live. |
| **Presets** | — | Pick a size: the native size of each display connected right now, the usual projector sizes (1080p, WUXGA, WXGA, XGA, 4K and the rest), then Houdini's own list. |
| **Playground** | *(read-only)* | While the output is open: how many projector pixels the pinned image really covers, against the COP Network's resolution. |
| **Build COP Network and Output** | — | Lays out a COP Network and a MAPout Output below this node, wired. Pressing it again reuses what is there and moves nothing. |

### Mapping

| Parameter | Default | What it does |
|---|---|---|
| **Edit Mapping** | Off | Edit on the projector itself: the calibration grid, the corner handles and the shapes. **E** on the projector toggles it. |
| **Tool** | Warp | What a click on the projector does. *Warp* (W): corners and mesh points. *Select* (V): pick, move, rename and mask shapes. *Rectangle*, *Ellipse* (R, O): drag to draw one. *Polygon* (P): click its points. |
| **Selection** | Box | What a drag on empty space draws to select: a *Box* or a *Lasso*. **L** on the projector switches it. |

#### Mapping File

| Parameter | Default | What it does |
|---|---|---|
| **File** | `$HIP/mapout/mapping.json` | The file Save and Load write and read. |
| **Save Mapping** / **Load Mapping** | — | Write the Included parts of the mapping to the file, or read them back (one undo step). Loaded shapes replace the drawn ones. |
| **Corner Pin and Rotation** | On | Include the four corners, the edge feather and the rotation. |
| **Mesh Warp** | On | Include the mesh warp: on or off, its cells and points. |
| **Multi-Projector** | On | Include the canvas region and the edge blend. |
| **Calibration Grid** | On | Include the grid's cells, diagonals and circle. |
| **Shapes** | Off | Include the shapes: points, boxes, curves, names, mask and UV switches. |

#### Corner Pin

| Parameter | Default | What it does |
|---|---|---|
| **Reset Corners** | — | Puts the four corners back on the screen's own corners. |
| **Top Left**, **Top Right**, **Bottom Right**, **Bottom Left** | the screen's corners | Where each corner of the image sits, as a fraction of the screen (0 to 1, top left origin, Y down). A perspective corner pin: on a flat wall it corrects keystone, an off-centre projector and wall tilt exactly. |
| **Edge Feather** | 0 | Fades the image out toward its edges, as a fraction of the image height. 0 is a hard edge. |

#### Rotation

| Parameter | Default | What it does |
|---|---|---|
| **Rotation** | Off | Turns the whole image on the projector. Off, the angle is ignored. |
| **Pivot** | Top Left | What stays put while the image turns: one of the pinned corners, or *Center*, where the image's diagonals cross. |
| **Rotate** | 0 | The turn in degrees, counterclockwise as seen on the wall. |

#### Mesh Warp

| Parameter | Default | What it does |
|---|---|---|
| **Mesh Warp** | Off | A lattice of control points inside the corner pin, for surfaces that are not flat. Drag the diamond points on the projector with the Warp tool. |
| **Reset Mesh** | — | Puts every lattice point back to rest. |
| **Mesh Cells** | 3 × 3 | Cells across and down. Changing it starts the lattice over. |

#### Multi-Projector

| Parameter | Default | What it does |
|---|---|---|
| **Multi-Projector** | Off | One Setup and Output per projector on a shared COP Network. Off, the region and blend are ignored. |
| **Canvas Region Min** / **Max** | 0, 0 / 1, 1 | The part of the canvas this projector shows (0 to 1, top left origin). |
| **Edge Blend** | 0 | Fades this projector out over its Left, Right, Top and Bottom edges. Enter the overlap width, as a fraction of the canvas, on the overlapping side of both Setups. |
| **Blend Curve** | 1 | Bends the blend ramps for a projector whose response is not sRGB. 1 is exact for an sRGB display. |

### Shapes

| Parameter | Default | What it does |
|---|---|---|
| **Go to Shapes Network** | — | Shows the Setup's Shapes network, where every shape is an ordinary SOP wired into `ALL_SHAPES`. |
| **Snap to Points** | On | A placed or dragged point snaps to another shape's point or a canvas corner within 10 pixels. Hold Ctrl to place freely. |
| **Mask Group** | `mask` | Also treats these primitives as masks: a group name or pattern. For shapes made by hand. |
| **Mask Feather** | 0 | Softens the mask edges, as a fraction of the image height. |
| **Sync Shapes to COPs** | — | Gives every shape its own row in the COP Network, from a pink `ART_<name>` null to a teal `SHAPE_<name>` null. New shapes get rows, deleted ones lose theirs, the rest keep their artwork. |
| **Show UV Check** | Off | A numbered, coloured UV grid on every shape instead of its artwork. Uses SideFX Labs; a plain checkerboard without it. |
| **COP Group** | `*` | Which shapes Add Group Layers makes a row for. |
| **Add Group Layers** | — | A row after the composite for the COP Group, with the group's mask, a per-face ID and an SDF to the face edges. |
| **Shapes to Geometry** | — | Puts the synced shapes beside the Setup as flat polygons in the COP Network's own frame. |
| **Snap View** | — | Points the viewport straight at the canvas plane, orthographic. |
| **Make Camera** | Off | Snap View also makes an orthographic OBJ camera with that view, at the Canvas Resolution. |

### Visualization

| Parameter | Default | What it does |
|---|---|---|
| **Show Calibration Grid** | On | Draws the grid over the image while editing. |
| **Grid Cells** | 3 × 3 | Cells across and down. On a flat wall, equal cells mean the keystone is gone. |
| **Diagonals** | Off | The grid's two diagonals, crossing at the canvas centre. |
| **Circle** | Off | A circle that is round in canvas pixels. An ellipse on the wall means the pinned area does not have the canvas's aspect. |
| **Grid Line Width** | 1 | In projector pixels. |
| **Frame Line Width** | 4 | The frame around the canvas, drawn inside its edge, in projector pixels. |
| **Shape Lines** | On, white | The shape outlines while editing, and their colour. Masks draw red and the selection yellow. |
| **Shape Line Width** | 4 | In projector pixels. |
| **Crosshair Cursor** | Off | Draws the pointer as a crosshair across the whole image, to find it from across a room. |
| **Show Help** | On | The help bar on the projector while editing. **H** on the projector toggles it. |

### Utilities

The full list of mouse and key bindings on the projector, and links to the website, the store page, this documentation, the Discord and the YouTube channel.

## MAPout Output

| Parameter | Default | What it does |
|---|---|---|
| **Open Output** | — | Opens the projector window, fullscreen and on top, on the chosen Screen. **Ctrl+W** on the projector closes it. |
| **Close Output** | — | Closes this node's window. |
| **Status** | *(read-only)* | The image size and channels, the measured time to read one frame off the COP Network, and the frame rate that implies. |
| **Blackout** | Off | Blacks the projector instantly without closing the window. |
| **Screen** | — | The display the window covers. A projector appears in the list once it is connected. |
| **Auto-Open On Load** | Off | Opens the window when the scene is loaded, for an installation that has to come back up by itself. |
| **Test Pattern** | Off | A built-in alignment pattern at the COP Network's size. Works with nothing wired. |
| **Flip Horizontal** / **Flip Vertical** | Off | For rear projection and ceiling mounts, when the projector cannot flip itself. |
| **Exposure** | 1 | Linear multiplier before the sRGB display transform, for matching two projectors' brightness. |
| **Gamma Trim** | 1 | Extra gamma on top of the sRGB transform, for a projector that is not sRGB. |
| **Show Diagnostics** | Off | A panel on the projector: frame, image size, read time, new frames reaching the wall per second, and how often the window checks. |
