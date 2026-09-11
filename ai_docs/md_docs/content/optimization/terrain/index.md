# Terrain Optimization


## Landscape Terrain Optimization


Performance of the **[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)** depends on the data streaming that lies behind its operation: only graphic data of areas that are visible by the camera at a moment is loaded and destroyed when it is no longer needed. Unoptimized streaming settings cause noticeable loading of areas when the camera moves.


![](../../../objects/objects/terrain/landscape_terrain/streaming_tiles_low.gif)

*Visible streaming issues.*


The overall life cycle of graphic data can be thought of as follows:


1. The system determines the tiles that are currently visible in the viewport, their spatial size and their highest available mip-level depending on the distance, terrain density limits and streaming settings.
2. The required graphic data of requested tiles of base textures is loaded from `.lmap` assets in chunks of *128�128 pixels* and cached in the RAM (CPU cache) to be used in intersection calculations and physics.
3. The acquired data is uploaded to the GPU and cached in the video memory, if necessary (GPU cache).
4. The data of several *Landscape Layer Maps* (*Albedo, Height* and *Mask* textures) is blended according to the [Blending Settings](../../../objects/objects/terrain/landscape_terrain/index.md#layers_blending).
5. The base textures are blended with textures of the [details](../../../objects/objects/terrain/landscape_terrain/index.md#details) (if any).
6. The final textures for each of three *Landscape Terrain* components (*Albedo, Normal* and *Height*) are written into the Virtual Texture replacing the oldest chunks.
7. The result is rendered in the viewport with due regard for Adaptive Hardware Tessellation and displacement.
8. The textures are replaced by newer data in the cache when no longer needed.


![](../../../objects/objects/terrain/landscape_terrain/loading_graphic_data.png)

*The life cycle of Landscape Terrain graphic data.*


### Profiling


The camera behavior in a project that utilizes a *Landscape Terrain* object plays an important role. A static camera implies a single load of data, provided all textures fit in the video memory. When the active camera significantly changes its position and orientation while unveiling unloaded areas, streaming may hit hard on performance. Therefore, performance and memory consumption should be considered and tuned for the final set of cameras and screen resolution of the target platform.


For convenient profiling, you can animate the camera movement via **[Tracker](../../../editor2/tools/tracker/index.md)** and run animations for tests.


It is recommended to use the **[Microprofile](../../../tools/profiling/microprofile/index_cpp.md)** tool for detailed in-depth estimation for the performance of a *Landscape Terrain* object.


![](microprofile.png)

*Stages ofLandscape Terrainoperation in the output of the Microprofile tool.*


By using the [Rendering Performance Profiler](../../../tools/profiling/profiler/index.md#render), you can estimate the memory consumption.


![](../../../objects/objects/terrain/landscape_terrain/profiler.png)

*Landscape Terrain-related section of theRendering Performance Profileroutput.*


#### Hardware Recommendations


Streaming implies continuous data loading from disk storage. If your project requires a highly-detailed landscape of large size (several kilometers across), it is recommended to consider using an SSD as slower HDDs may not be capable of providing enough throughput capacity.


At that, multi-core processors have an advantage here enabling you to distribute the load without bottlenecks.


### Landscape Layers


The number and density of different [Landscape Layer Maps](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md) that define the look of the terrain at the current moment is an important factor � multiple blended layers with high resolution textures might make a significant performance drop. In most cases it is reasonable to combine multiple textures into a single one in a raster graphics editor.


> **Notice:** In contrast, you can use several *Landscape Layer Maps* that refer to the same `.lmap` asset without performance drop. You can create a *[Node Reference](../../../objects/nodes/reference/index.md)* containing a *Landscape Layer Map* to propagate repetitive areas.


The **[Current Data Density](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#density)** value for a *Landscape Layer Map* is calculated based on its spatial size and the resolution of base textures used. It's hard to miss that a decent high-detailed landscape would require a texture tileset of an extremely large resolution.

 Best PracticeUse base textures of *Landscape Layer Maps* to create a coarse look of the *Landscape Terrain* and refine the surface using [details](../../../objects/objects/terrain/landscape_terrain/index.md#details) for high-detailed per-pixel quality.
Also, the visibility of layers is taken into account � if a large *Landscape Layer Map* overlaps other layers (has a higher **[Order](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#order)** value), only its graphic data will be loaded and rendered.


![](../../../objects/objects/terrain/landscape_terrain/layers_order.png)

*A schematic representation of severalLandscape Layer Mapsoverlapping each other.The one with the higherOrdervalue overlaps the other ones and only its data will be loaded and visualized.*


Streaming is based on using previously loaded geometry to define the visible areas of terrain. There is no loaded geometry at the very world startup, so the system looks for a *Landscape Layer Map* that has the **[Culling](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#culling)** flag enabled and loads preliminary low-level data of this layer. If your world contains several layers, one of which represents the basic shape of the terrain, while others are used as *insets* placed within the bounds of the base layer and having an insignificant height difference from it, it is recommended for you to disable **Culling** for insets and enable it for the base layer. This is how you can reduce load on CPU at the world startup.


![](inset.png)


### Tiles Loading


Each frame the *Landscape Terrain* system checks which tiles are to loaded and updated. Increase the **[Tiles Update Per Frame](../../../editor2/settings/render_settings/landscape/index.md#tiles_update_per_frame)** parameter to ensure that all necessary tiles are updated on time. However, if this value is too big, it may cause a performance drop during data streaming.


The loading speed of chunks of graphic data depends on the **[Tiles Load Per Frame](../../../editor2/settings/render_settings/landscape/index.md#tiles_load_per_frame)** value. Higher values imply faster multi-threaded loading of tiles but more performance-consuming data streaming. Note that it is pointless to set this value higher than the *Tiles Update Per Frame*.


Thus, it is necessary to find a trade-off when tweaking these parameters.


Use the **[Landscape Terrain VT Streaming](../../../editor2/using_visual_helpers/index.md#landscape_streaming)** helper (or the `render_show_landscape_terrain_vt_streaming 1` console command) to enable visualization of tiles being streamed. In this mode colored areas show the tiles that are currently being rendered in a lower resolution until the highest mip-level is loaded and rendered. The faster the colored tiles disappear, the better.


![](../../../objects/objects/terrain/landscape_terrain/streamed_tiles.png)

*TheLandscape Terrain VT Streaminghelper*


#### Cache


The default values of the **[Cache](../../../editor2/settings/render_settings/landscape/index.md#cache)** settings are suitable for the most cases.


If you modify a layer map by using [Brush Editor](../../../editor2/brush_editor/index.md) or your project implies run-time terrain modification, increase the **GPU Cache Size** limit and **GPU Cache Life Time** for better performance.


When it comes to optimizing intersection and collision detection performed on the CPU side, increase the **CPU Cache Size** for better performance.


#### Run-Time Modification


When something changes a loaded area of the *Landscape Terrain*, the affected tiles are to be restreamed with the changes taken into account.


Increase the **[Tiles Reload Per Frame](../../../editor2/settings/render_settings/landscape/index.md#tiles_reload_per_frame)** parameter�the number of reloaded tiles per each frame�to make the changes be committed faster.


However, be careful not to exceed the bandwidth of the system with too many tiles reloaded at the same time; otherwise, the performance may drop a lot. It is therefore very important to monitor the streaming settings and dynamics of layers and avoid per-frame changes of large areas that cause many tiles to reload.


For more details, please refer to the [**Make It Run-Time**](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_settings) section.


### Details


The *Landscape Terrain* enables you to add up to **1024** [details](../../../objects/objects/terrain/landscape_terrain/index.md#details) to a mask making it possible to create a pretty detailed and diverse look of the landscape. In terms of optimization, minimizing the number of details and textures is a way to faster rendering.


![](../../../objects/objects/terrain/landscape_terrain/detail_parameters.png)


The textures of details are loaded at the world startup and kept in the video memory to be blended with the base textures of the *Landscape Terrain* when rendering. You can specify a lower resolution for the corresponding textures of all detail materials by tweaking the following parameters:


- **[Detail Albedo Texture Resolution](../../../editor2/settings/render_settings/landscape/index.md#detail_albedo_resolution)**
- **[Detail Height Texture Resolution](../../../editor2/settings/render_settings/landscape/index.md#detail_height_resolution)**
- **[Detail Additional Mask Texture Resolution](../../../editor2/settings/render_settings/landscape/index.md#detail_additional_mask_resolution)**


### Virtual Texture


The final textures for tiles of the *Landscape Terrain* are written to the Virtual Texture components (*Albedo, Normal* and *Height*). Increase the **[Texture Memory Size](../../../editor2/settings/render_settings/landscape/index.md#streaming)** value to ensure that the Virtual Texture provides enough capacity to store the loaded high-detail texture chunks.


![](../../../objects/objects/terrain/landscape_terrain/render_textures.png)

*The components of theLandscape TerrainVirtual Texture.*


With a lower size the Virtual Texture requires less video memory but doesn't provide enough capacity to store all the required data resulting in poor performance, low detail level and fast flickering of the Landscape Terrain surface due to continuous reloading of tiles.


### Rendering


Polygons of the *Landscape Terrain* surface are adaptively tessellated on the fly and displaced based on the Heightmap component of the Virtual Texture. The polygon mesh is split up to multiple levels of detail of various density depending on the distance from the camera. The **[Geometry](../../../editor2/settings/render_settings/landscape/index.md#geometry)** settings provide much room for rendering optimization.


![](lods.png)

*Levels of Detail of tessellated geometry.*


Pay attention to the following parameters:


- With lower values of **[Geometry Progression](../../../editor2/settings/render_settings/landscape/index.md#geometry_progression)** less polygons are generated at a distance.
- By configuring the **[Geometry Polygon Size](../../../editor2/settings/render_settings/landscape/index.md#geometry_polygon_size)** parameter you can define the minimum spatial size of polygons in case of excessive detail level.
- **[Geometry Subpixel Reduction](../../../editor2/settings/render_settings/landscape/index.md#geometry_subpixel_reduction)** parameter determines the minimum ratio of polygon size (in the screen space) to the area seen in the viewport. This parameter enables you to quickly decrease the number of polygons or simply remove too small polygons that are barely visible, in order to increase performance.
- Set a lower **[Visibility Distance](../../../editor2/settings/render_settings/landscape/index.md#visibility_distance)** to discard rendering of too remote polygons.


You can decrease the maximum allowed level of detail for the albedo, normal and height textures of the *Landscape Terrain* by increasing the **[Texel Size](../../../editor2/settings/render_settings/landscape/index.md#texel_size)** parameter.


![](../../../editor2/settings/render_settings/landscape/texel_size_1.png) ![](../../../editor2/settings/render_settings/landscape/texel_size_2.png)


Decrease **[Target Resolution](../../../editor2/settings/render_settings/landscape/index.md#target_resolution)**�the resolution of the screen buffer for the *Landscape Terrain* renderer�to gain more performance at a cost of visual quality.


You can also reduce the detail level of polygons facing the camera at oblique viewing angles (**[Detail Level By Angle](../../../editor2/settings/render_settings/landscape/index.md#detail_level_by_angle)**) to optimize streaming load and memory consumption.


Different mip-levels of landscape textures are used at different distances. Switch to the *Low* or *Medium* **[Texture Filtering](../../../editor2/settings/render_settings/landscape/index.md#texture_filtering)** quality to improve performance at a cost of a slightly visible edge between adjacent mipmap levels.


#### Culling Optimization


The polygons of the Landscape Terrain surface are subject to frustum culling optimization. If a polygon falls out of the camera frustum (i.e. its screen position is outside the viewport bounds), it is culled out for rendering. You can enable the **Aggressive Frustum Culling** mode that implies more strict requirements for polygons to be rendered and, therefore, higher performance.


Tweak the **[Culling](../../../editor2/settings/render_settings/landscape/index.md#culling)** settings for more optimizations:


- Enable the **[Culling By Depth](../../../editor2/settings/render_settings/landscape/index.md#culling_by_depth)** option to cull out more polygons occluded by geometry and the *Landscape Terrain* itself.
- Increase the **[Culling Oblique Frustum](../../../editor2/settings/render_settings/landscape/index.md#culling_oblique_frustum)** multiplier to cull out more polygons beyond the oblique frustum plane.


Adjust the [**Advanced**](../../../editor2/settings/render_settings/landscape/index.md#advanced) settings for even finer tuning.


## Global Terrain Optimization


The *[terrain_global_base](../../../content/materials/library/terrain_global_base/index.md)* material provides several parameters for fine tuning of terrain geometry optimization, shadows and LOD blending:


- **[Subpixel Polygons Reduction](../../../content/materials/library/terrain_global_base/index.md#subpixel_polygons_reduction)** parameter determines the minimum ratio of polygon size (in the screen space) to the area seen in the viewport. This parameter allows you to remove too small polygons that are barely visible, in order to increase performance.
- **[Back Face Culling](../../../content/materials/library/terrain_global_base/index.md#back_face_culling)** parameter is used for culling of the tessellation patches that have their back faces turned to the camera. The number of polygons can be significantly reduced (e.g. culling back faces of a large mountain) and increase performance.
- **[Frustum Culling Padding](../../../content/materials/library/terrain_global_base/index.md#frustum_culling_padding)** parameter is used to control culling of the tessellation patches outside the viewing frustum.
- **[Shadow Offset](../../../content/materials/library/terrain_global_base/index.md#shadow_offset)** parameter enables to adjust the look of shadows in cases low-poly LODs cast shadows on high poly LODs in areas, where there should be no shadows should.
- **[LOD Padding](../../../content/materials/library/terrain_global_base/index.md#lod_padding)** parameter can be used to adjust smooth transitions between terrain LODs and increase performance.


In case if your terrain does not require insets, you can disable this option to increase performance. To do so, just uncheck the **[Use Insets](../../../content/materials/library/terrain_global_base/index.md#option_use_insets)** in the *States* tab.


Also you can use frustum culling optimization to affect performance: enable the **[Fast Frustum Culling](../../../content/materials/library/terrain_global_base/index.md#option_fast_frustum_culling)** option in the *States* tab. This option increases the number of culled polygons.
