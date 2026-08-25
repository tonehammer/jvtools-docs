# Parameter reference

TODO — one section per parameter folder, in panel order, once the node exists.

Provisional control set, inherited from the shelf tool:

| Control | What it does |
|---|---|
| **Copernicus Network** | Which copnet to display. Defaults to the one in the scene when there is only one. |
| **Output Index** | Which output of the display node to read. Only shown when the display node has more than one. |
| **Source** | Copernicus (the COP image) / Scene View (3D only) / Both (3D over the COP). |
| **Screen** | Which display to output to, by name. |
| **Fullscreen** | Fill the chosen screen. |
| **Fit** | Fit (letterbox) / Fill (crop) / 1:1 pixels / Stretch. |
| **Offset / Zoom** | Image placement. Right-drag on the output window does the same thing. |
| **Flip H / Flip V** | Mirror the image. |
| **Exposure / Gamma** | Output grade, applied on the GPU. |
| **FPS Cap** | Upper bound on redraw rate. |

## Version signals

Every jvtools node carries these at the bottom of its parameter list:

| Parameter | What it does |
|---|---|
| **Current Version** | The product version of the asset you have installed. |
| *(update notice)* | Appears when a newer version is available on the store. |
