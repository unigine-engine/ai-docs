# Optimizing Grass


Rendering of the *Grass* object can also reduce the performance. Grass optimization means reducing the number of the grass polygons rendered each frame. This can be achieved by using the specific grass settings.


> **Notice:** To control the number of rendered grass polygons, take a look at the **[Triangles](../../../../objects/objects/grass/settings.md#triangles)** counter in the *Grass* tab of the *Parameters* window.


## Setting Up Step for Cell Division


For optimization purposes, the grass field is split into cells forming a grid. These cells are rendered one by one, from the camera to the horizon. Each cell requires 1 DIP call, so the higher number of cells, the lower the performance. The number of cells is determined by two parameters - the **[Size](../../../../objects/objects/grass/settings.md#size_x)** of the grass field and the **[Step](../../../../objects/objects/grass/settings.md#step)** by which the grass field is split into cells.


![](grass_cells.png)


There are two requirements for these parameters that should be met:


- The size of the field should be divided by the step **exactly, with no remainder by division**.
- The step value should stay within the [recommended optimal range](../../../../objects/objects/grass/index.md#step) of [10;25], as the small enough cells are rendered fast and smoothly while the large cells may take more time for rendering.


For example, if the size of the grass field is 4097 x 4097, the recommended Step value is 17. It is in the range and the field size is divided by this value exactly.


## Thinning Grass


Except reducing the number of cells rendered per frame, the grass field can be thinned out with a distance. For this, enable the **[Thinning](../../../../objects/objects/grass/settings.md#thinning)** option to reduce the number of grass polygons rendered across the grass *Fade distance*.


![](grass_thinning.png)


## Density Considerations


Increasing *[Density](../../../../objects/objects/grass/settings.md#density)* can dramatically increase RAM and VRAM usage. Adjust this value with extreme caution: for large areas (more than 1 square kilometer) covered with grass, high density settings can generate tens of gigabytes of data in memory and on the GPU.


Values above **1.0** should be used only after careful consideration and together with other optimization techniques such as limiting the [visibility distance](../../../../principles/world_management/index.md#visible), using [levels of detail](../../../../objects/objects/grass/index.md#low_poly_grass) and enabling the grass [Thinning](../../../../objects/objects/grass/settings.md#thinning) option, as even small increases can cause excessive memory consumption.
