# terrain_global_base


A *terrain_global_base* material is a default material for the [global terrain object](../../../../objects/objects/terrain/terrain_global/index.md). Via this material you can adjust different visual and optimization parameters and control the post processing for the global terrain.

> **Notice:** Casting of shadows for this material is disabled by default. You can enable it via the [Common tab](../../../../editor2/materials_settings/index.md#options)

 Prior KnowledgeThis article assumes you have prior knowledge of the following topics. Please read them before proceeding:
- *[Materials Settings](../../../../editor2/materials_settings/index.md)*
- *[mesh_base](../../../../content/materials/library/mesh_base/index.md)* material states, textures, parameters


## States


The *terrain_global_base* material has the following Options and Post processing states.


![States](states.png)

*Material Settings,Statestab.*


### Options


Specify the following options:


- **Use Insets** - toggles terrain insets on and off. Disabling insets leads to performance gain. > **Notice:** When insets are disabled, two adjacent LODs **[aren't blended](../../../../objects/objects/terrain/terrain_global/index.md#lod_blending)** together if there is no data for the more detailed LOD: masks used for such LODs blending aren't generated. In the areas with no data, holes or sharp edges will occur.
- **Fast Frustum Culling** - enables/disables optimization of frustum culling. When enabled, the number of culled polygons increases thereby increasing performance. If you have some issues with polygons rendering, try to disable the option (however, note that performance may drop).
- **Filter Mask Albedo** - enables/disables linear filtering for the masks of the albedo LODs.
- **Filter Mask Normal** - enables/disables linear filtering for the masks of the normal LODs.
- **SSDirt** - enables rendering of the [SSDirt](../../../../editor2/settings/render_settings/ssdirt/index.md) effect for the material, allowing you to simulate worn scratched edges and accumulation of dirt and dust in cavities.


### Post Processing


- **Material SSAO** - enables SSAO (screen-space ambient occlusion) post for the global terrain.
- **Material SSR** - enables SSR (screen-space reflections) post for the global terrain.
- **Material SSSSS** - enables SSSSS (screen-space sub-surface scattering) post for the global terrain.
- **Material DOF** - enables DOF (depth of field) for the global terrain.
- **Material Motion Blur** - enables motion blur for the global terrain.
- **Material Screen-Space Shadows** - enables screen-space shadows for the global terrain.


### Visualizer


- **LODs** - enables/disables visualizer for LODs. One of the following:

  - **Albedo** - shows visualizer for albedo LODs.
  - **Normal** - shows visualizer for normal LODs.
  - **None** - disables visualizer for LODs.
- **No imagery Data** - enables visualizer for areas with no imagery data available.


## Parameters


![Parameters](parameters.png)

*Material Settings,Parameterstab.*


- **Shadow Offset** - offset along the Z axis of the height LODs that [cast shadows](../../../../objects/objects/terrain/terrain_global/index.md#cast_shadow). If the low poly LOD casts shadows to the high poly LOD in areas where no shadows should be rendered, this parameter can be used to reduce this effect.
- **LOD Padding** - distance from the LOD edge to which this LOD is dilated (the polygons are rendered outside the edges of the LOD). Decreasing the value leads to decreasing the number of rendered polygons. This value is used to adjust smooth transitions between LODs and improve performance. | ![](lod_padding_0.png) | ![](lod_padding_1.png) | |---|---| | *Terrain Grid with LOD Padding = 0.1* | *Terrain Grid with LOD Padding = 0.3* |
- **Frustum Culling Padding** - value, by which the borders of the current frustum are increased. Frustum culling is performed for the frustum of the increased size. By the maximum value of 1, the frustum borders will be increased by the size of the current frustum.
- **Subpixel Polygons Reduction** - minimum allowed ratio of a polygon size (in screen space) to the size of an [area seen in the viewport](../../../../editor2/camera_settings/index.md#fov). If the ratio calculated for the polygon is less than this value, such polygon will be removed. Polygons rendered at the distance between the camera and its near clipping plane aren't removed. This parameter should be used for terrain optimization. | ![](subpixel_reduction_0.png) | ![](subpixel_reduction_1.png) | |---|---| | *Terrain Grid with Subpixel Polygons Reduction = 10* | *Terrain Grid with Subpixel Polygons Reduction = 30* |
- **Back Face Culling** - multiplier for the angle between the tessellation patch normal and the camera's view direction. The parameter is used for culling the tessellation patches that are turned to the camera by their back faces. The range of values is [**0; 1**]. The higher the value, the less the angle between the patch normal and the camera's direction is required for culling this patch. For example, the parameter culls the back of the mountain: the number of rendered polygons decreases and performance improves.
- **Oblique Frustum Culling** - multiplier for culling tessellation patches beyond the oblique frustum plane. The range of values is [**0; 1**]. The higher the value, the more patches will be culled. Try reducing this value if excessive polygon culling occurs (can be noticed, for example, in planar reflections of a low-poly terrain).


### SSDirt


**SSDirt** enables rendering of the [SSDirt](../../../../editor2/settings/render_settings/ssdirt/index.md) effect for the material, allowing you to simulate worn scratched edges and accumulation of dirt and dust in cavities.

> **Notice:** Enabling this effect for the terrain result in having it rendered for dynamic objects (e.g., characters and so on) moving across its surface.


#### SSDirt Parameters


##### Cavity Scale


Scale factor for the SSDirt effect in concave areas. *Higher* values result in more pronounced effect in slits and cavities.


##### Convexity Scale


Scale factor for the SSDirt effect in convex areas. *Higher* values result in more pronounced effect on edges and convexities.


##### Curvature UV Transform


UV-coordinates transformation for textures applied in concave and convex areas.


### Base


- **Albedo** - albedo color multiplier.
- **Roughness** - roughness multiplier.
- **Microfiber** - microfiber multiplier.


### Default


- **Material mask** - specifies material bit-mask.


### Fade Lods


- **Albedo** - linear interpolation factor for albedo LODs. Determines crossfading smoothness.
- **Normal** - linear interpolation factor for normal LODs. Determines crossfading smoothness.
- **Height** - linear interpolation factor for height LODs. Determines crossfading smoothness.
- **Masks** - linear interpolation factor for masks LODs. Determines crossfading smoothness.
