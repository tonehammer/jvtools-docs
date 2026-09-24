---
order: 110
---

# Parameter reference

## Hou-DisplacementX (COP)

### Generator

| Parameter | What it does |
|---|---|
| **Seed** | Decides where every shape lands. The same Seed with the same settings always gives the same map, at any resolution. Default 1; 0 to 1000. |
| **New Seed** | Picks a random Seed - the Generate button of the web version. |
| **Iterations** | How many shapes to draw. Each iteration draws one randomly picked shape type, so more iterations give a busier map. Cook time grows with Iterations times the pixel count. Default 100; 10 to 2000. |
| **Background** | The grey the canvas starts from, before any shape is drawn. Default 0.125; 0 to 1. |
| **Resolution** | Output size in pixels. Ignored when a layer is wired into the **Size Reference** input - the node then matches that layer instead. Default 2048 x 2048; 16 to 8192. |
| **Resolution Menu** | Picks a common square size for Resolution. You can still type any size into the fields. |
| **Seamless** | Wraps shapes that cross an edge around to the opposite edge, so the map tiles. Lines always span the whole image and are not affected. Default off. |
| **Invert** | Flips the height map: raised becomes recessed. Default off. |
| **Randomize All** | Rolls new random settings for everything, like the web version's Randomize all. Does not change Seed or Resolution. |

### Shapes

Rectangles, Grid, Columns, Rows and Lines each have their own folder with a header checkbox (**Enable Rectangles**, **Enable Grid**, and so on) and a **Randomize** button that rerolls that shape's own settings without touching Seed. A shape type left off still takes its share of the iterations, so the others do not get denser.

| Parameter | What it does |
|---|---|
| **Brightness** | Each shape gets a grey value picked between Min and Max. 0 is black, 1 is white; in height terms, low reads as recessed and high as raised. Default 0 to 1. |
| **Opacity** | Each shape gets an opacity picked between Min and Max. Lower values let the layers underneath show through. Rectangles default 0.5 to 1; the others default 0.8 to 1. Range 0 to 1. |
| **Scale** | Multiplies the size of every shape of that type. 1 matches the web version's 100%. Default 1; 0.2 to 2. |
| **Amount** *(Grid, Columns, Rows only)* | How many cells each shape draws, picked between Min and Max, separately per direction. Default 2 to 5; 1 to 10. |
| **Gap** *(Grid, Columns, Rows only)* | Space between cells, as a multiple of the cell size. 1 leaves a gap as wide as a cell. Default 1; 0.1 to 10. |
| **Width** *(Lines only)* | Line thickness, as a fraction of the image size, picked between Min and Max. The web version's 5-10 is 0.002-0.004 here. Default 0.002 to 0.004; 0.0001 to 0.05. |

### Sprites

| Parameter | What it does |
|---|---|
| **Enable Sprites** | Stamps sci-fi panel sprites from the packs below. Off by default, as in the web version. |
| **Classic** | Includes the Classic pack. With several packs on, each sprite is picked from all of them at once. Default on. |
| **Big Data** | Includes the Big Data pack. Default off. |
| **Aggromaxx** | Includes the Aggromaxx pack. Default off. |
| **Crap Pack** | Includes the Crap Pack pack. Default off. |
| **Rotate** | Turns each sprite by a random multiple of 90 degrees. As in the web version, the turn is about the image centre, so it moves the sprite as well as turning it. Default on. |
| **Randomize Sprites** | Picks random packs and a random Rotate setting. |

### Blend Modes

Sixteen toggles - Color Burn, Color Dodge, Darken, Difference, Exclusion, Hard Light, Lighten, Lighter (Add), Luminosity, Multiply, Overlay, Screen, Soft Light, Source Atop, Normal, XOR - each allowing that blend mode. Every shape picks one of the ticked modes at random; with none ticked, every shape uses Normal. Normal is the only one on by default. **Randomize Blend Modes** ticks a random set.

### Outputs

| Parameter | What it does |
|---|---|
| **Normal Strength** | How steep the normal output reads the height map. Higher values give harder, more pronounced edges. Default 1; 0 to 10. |
| **Color Gradient** | Maps the height map to colour for the basecolor output: the left end colours black, the right end colours white. |

### Utilities

| Parameter | What it does |
|---|---|
| **Links** | Opens the JVtools website in your browser. |
| **Gumroad** | Opens Gumroad in your browser. |
| **Documentation** | Opens the documentation in your browser. |
| **Youtube** | Opens Youtube in your browser. |

## Hou-DisplacementX Heightfield (SOP)

### Output

| Parameter | What it does |
|---|---|
| **Output** | What the node outputs. *Heightfield*: with nothing wired, the height layer as a heightfield (height and mask volumes); with geometry wired, that geometry displaced. *All Layers*: adds the normal, basecolor and id layers as volumes, or, when displacing, writes `Cd` and `displacementx_id` onto the points. |
| **Show Color** | Shows the Color Gradient in the viewport. On a heightfield it assigns a HeightField Visualize material mapping the gradient over 0 to Height Scale; on displaced geometry it writes `Cd` onto the points. Off by default - the material replaces any material already on the heightfield. |

### Heightfield

| Parameter | What it does |
|---|---|
| **Size** | The heightfield's width in scene units. The other side follows the aspect of Resolution. 1000 matches the HeightField SOP's default, so erosion and other scale-dependent tools behave as they do on a fresh heightfield. Voxel spacing is Size divided by Resolution. Not used when geometry is wired. Default 1000; 1 to 5000. |
| **Height Scale** | How tall a full-white pixel stands, in scene units. The height layer runs from 0 to 1, so this is the height of the tallest panel. Not used when geometry is wired. Default 50; 0 to 500. |

### Displace Input

| Parameter | What it does |
|---|---|
| **Tile Size** | How big one repeat of the map is on the object, in scene units. Smaller tiles the map more often. While geometry is wired, Seamless is always on, so the repeats meet without a seam. Default 2; 0.001 to 20. |
| **Tile Offset** | Slides the projection over the object, in scene units. Default 0, 0, 0; 0 to 10. |
| **Blend Sharpness** | How crisply the three projections (along X, Y and Z) hand over to each other where the surface turns. Low values blend them over a wide band; high values make short, sharp transitions. Default 4; 1 to 16. |
| **Displace Amount** | How far a full-white pixel pushes the surface out along its normal, in scene units. Displacement only moves the points that are there, so the geometry needs to be dense - Subdivide or Remesh it first. Default 0.1; 0 to 1. |
| **Midpoint** | The grey that stays on the surface. 0 pushes everything outward; 0.5 pushes light areas out and dark areas in. Default 0; 0 to 1. |

Every Generator, Shapes, Sprites, Blend Modes and Outputs control listed above for the COP node is also present on the Heightfield node, under the same label, and works the same way.

## Version signals

Every jvtools node carries these at the bottom of its parameter list:

| Parameter | What it does |
|---|---|
| **Current Version** | The product version of the asset you have installed. |
| *(update notice)* | Appears when a newer version is available on the store. |
