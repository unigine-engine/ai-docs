# Landscape Terrain


[![](landscape_sm.jpg)](landscape.png)


The **Landscape Terrain** system provides advanced simulation of terrain - the most important object in outdoor scene rendering. *Object Landscape Terrain* allows reconstructing practically any arbitrary landscape with diverse features:


- Virtually infinite terrain surface
- Extreme details up to 1 mm per pixel
- Adaptive hardware tessellation with displacement mapping
- Dynamic modification at run time - craters, funnels, trenches
- Simple and clear [API](../../../../api/library/objects/landscape_terrain/index.md)
- Up to 1024 detail materials
- Layers system with flexible blending rules
- Binoculars/scopes support (x20 / down to 1-degree FOV)
- Optimized rendering and physics performance
- Support for [simultaneous editing](#collaboration) by a team of 3D artists
- Decal-based holes
- Data compression support


The *Landscape Terrain* system is based on the principle of decomposing terrain graphic data that is too large to fit in the graphic memory in its entirety into smaller rectangular sections known as "**tiles**". Asynchronous streaming of these tiles makes it possible to render only necessary data at a full level of detail, regardless of the camera's field of view with multiple cameras supported. Flexible streaming settings make it possible to configure terrain rendering even for computers with a limited VRAM capacity.


![FOV](fov.gif)


> **Notice:** To simulate overhangs and caves, use [static meshes](../../../../objects/objects/mesh/index.md).


> **Warning:** - DirectX is the recommended graphic API for projects that use the *Landscape Terrain* system.
> - *Landscape Terrain* uses complex shaders that rely on double-precision floating-point calculations. Many **Intel GPUs (particularly on Windows) do not support double-precision math** in shaders under DirectX 12. As a result, terrain rendering may behave incorrectly or not function as expected on these systems.


### See Also


- The *[ObjectLandscapeTerrain](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md)* class to manage landscape terrain object parameters via API
- The *[Landscape](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md)* class to edit landscape terrain via API
- The *[landscape_terrain_base](../../../../content/materials/library/landscape_terrain_base/index.md)* material for terrain
- The *[landscape_terrain_detail_base](../../../../content/materials/library/landscape_terrain_detail_base/index.md)* material for details
- The *[Editing Landscape Terrain](../../../../editor2/brush_editor/index.md)* article to learn about Brush Editor
- The *[*Landscape Terrain* Optimization](../../../../content/optimization/terrain/index.md#landscape)* article.


## Landscape Terrain Operation


The *Landscape Terrain* system is represented by two types of nodes:


- **[Landscape Terrain](#create)** object is represented by an infinite plane. It is the main node, which is responsible for visualization and calculations: this object renders geometry and graphic data presented in the world and provides intersection detection settings. Also, it stores [detail](#details) data. > **Notice:** There can be several *Landscape Terrain* objects in the scene, but only one of them (active) shall be rendered.
- [**Landscape Layer Map**](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md) nodes store arbitrary graphic data used for rendering (height, albedo, and masks) and represent rectangular terrain layers that can be arranged in the scene and [blended](#layers_blending) with each other, thus composing the landscape.


![](landscape_layers.png)


Graphic data from *Landscape Layer Maps* and details (original full-size textures and generated mipmaps) are [asynchronously streamed](#tiling) and transferred to the main Virtual Texture, based on which the *Landscape Terrain* is rendered. The Virtual Texture consists of 3 components:


- **Albedo** � an RGBA8 texture defining the landscape color data,
- **Normal** � an RGBA8 texture, which stands for small details on the landscape surface,
- **Height** � an R32F texture defining the height data, according to which the landscape geometry is tessellated.


> **Notice:** The Normal texture is based on the Height data.


![](render_textures.png)

*Output of theRender Textureshelper. TheTerrain Virtual Texturesection contains Landscape-related textures.*


## Creating a Terrain


To create a *Landscape Terrain* in UnigineEditor perform the following actions:


1. In the *Create* menu, select *Landscape -> Landscape Terrain*. Click somewhere in the Editor Viewport to add the terrain. ![](create_landscape.png) *Landscape Terrain* is created with a *Landscape Layer Map* as a child.
2. Set up [Height, Albedo and Masks data](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#set_graphic_data) for the Landscape Layer Map(s), adjust via [Brush Editor](../../../../editor2/brush_editor/index.md).
3. To add another layer (an inset), click *Create -> Landscape -> Landscape Layer Map*.


## Layer Maps


*[Landscape Layer Maps](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)* represent rectangular terrain layers. By creating and arranging one or several layer maps you define the look and functionality of the terrain.


![](layer_maps.png)


Each *LandscapeLayerMap* node refers to an `.lmap` asset which stores a set of textures:


- **Heightmap** used to generate the geometry of *Landscape Terrain*,
- **Albedo** texture representing color data,
- Up to **20 single-channel masks**.


Albedo and Heightmap are the primary terrain components defining its look and shape, masks provide additional features. Please note that the density of the terrain graphic data is limited by the [render parameters](../../../../objects/objects/terrain/landscape_terrain/settings.md#render) regardless of the density of the source textures.


Depending on the size and resolution of your landscape, the size of the data can be quite large. You can use lossless and lossy [compression](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#compression) options to reduce the size of the `.lmap` file.


Compression method options:

- **Our Method** � recommended. UNIGINE compression method optimized for compressing 2D and 3D textures. It provides better results than **LZ4** and **Zlib** without quality reduction.
- **Zlib** � for high compression ratio (can provide up to 2 times higher compression ratio, but takes up to 20 times longer).
- **LZ4** � temporary option, planned to be removed in the upcoming releases.


All components of a *Landscape Layer Map* can be edited via [Brush Editor](../../../../editor2/brush_editor/index.md).


### Masks


*Landscape Layer Maps* can store up to 20 masks composing terrain layers that are not visible directly but can be used in certain graphical and logical tasks.


*Landscape Layer Map* is designed as a shared data pool, *mask* data of which can be used to add [details](#details) to the *Landscape Terrain* surface, used in [logic](../../../../api/library/objects/landscape_terrain/class.landscapefetch_cpp.md#getMask_int_float) (e.g. as a landcover classification map) and by other objects as well, such as [Grass](../../../../objects/objects/grass/index.md#terrain_mask), for example.


![](layer_masks.gif)

*An example of a biome with details based on masks.*


> **Notice:** To preview a landscape mask, go to *[Helpers -> Landscape Masks](../../../../editor2/using_visual_helpers/index.md#landscape_masks)* and choose the desired mask. Also, you can use the `render_show_landscape_mask N` console command, where *N* is the index of a mask from 1 to 20.


Masks are named for convenience, names of masks are synchronized with the *ObjectLandscapeTerrain* currently used. You can rename each mask via both the *ObjectLandscapeTerrain* parameters (by double-clicking the mask title and typing a new name) and the *LandscapeLayerMap* parameters in the corresponding **Name** fields with no reimport required.


![](layer_masks_names.png)

*Names of masks are synchronized withObjectLandscapeTerrain.*


Select a mask to see its parameters:


![](mask_parameters.png)


| Dithering | Dither amount enabling you to reduce graphical artefacts caused by insufficient mask's bit depth or increased *Mask Contrast* value set per-detail. This Dither amount is multiplied by the [global dithering amount](../../../../editor2/settings/render_settings/landscape/index.md#detail_mask_dither). |
|---|---|
| Default Value | Default value of the mask enabling you to skip import of single-color masks (e.g., a full white texture), thus lightening streaming load. |
| Mask by Albedo | Select an albedo color of *Landscape Layer Maps* to be used as an additional filter for the mask. > **Notice:** Control opacity by using the Alpha channel of the **Mask by Albedo** color. |


> **Notice:** Names of masks are stored by *Landscape Terrain* objects, i.e. names shown in the parameters of a *Landscape Layer Map* will change in correspondence with the current enabled *Landscape Terrain*.


Each mask can be represented by a single-channel image. For optimization purposes mask data is stored in blocks - **RGBA8** images (each containing 4 masks, one mask per each channel). There are 5 blocks, as the terrain has 20 masks available. Thus, the data of the 9th mask shall be stored in the R-channel of the third block (index = 2). The following parameters display the info on the corresponding mask texture and can be used to [access the mask via API](../../../../api/library/objects/landscape_terrain/class.landscapeimages_cpp.md#getMask_int_ImagePtr):


![](detail_parameters_mask_info.png)


| Mask Texture | The index of the mask block used. |
|---|---|
| Channel | The channel of the mask texture used. |


### Blending Layer Maps


When overlapping each other, *Landscape Layer Maps* are blended per component providing convenient development workflow. The following [blending modes](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#height_blending_mode) can be set for each [texture of a Landscape Layer Map](#layer_maps) individually:


- *[Additive](../../../../principles/render/blending/index.md#id_8)* � data of the layer map is added atop.
- *[Alpha Blend](../../../../principles/render/blending/index.md#id_2)* � the colors of this layer map and the underlying one are blended.
- *[Overlay](../../../../principles/render/blending/index.md#id_1)* � added data replaces the data below it.
- *[Multiplicative](../../../../principles/render/blending/index.md#id_9)* � the albedo colors are multiplied.


> **Notice:** Heightmap supports only the *Additive* and the *Alpha Blend* modes.


![](blend_before.jpg) ![](blend_after.jpg)


Additionally, it is possible to paint the opacity mask for each terrain component using the [Brush Editor](../../../../editor2/brush_editor/index.md) or specify it for each texture (provided the **Data Filling** mode is set to *From Tileset*). For this purpose, specify a texture and its channel to be treated as the [opacity mask](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#heightmap_opacity) for the corresponding texture:


![](layer_map_blending_opacity.png)


The order of blended layers matters, use the higher **[Order](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#landscape_layer_map_parameters)** value for layer maps that should be on top.


> **Notice:** Opacity of Landscape Layer Maps that have no underlying layers (i.e. their **Order** is the lowest) is ignored.


Layer maps can vary in density and size, so it is easy to create insets of different quality and [modify the terrain surface at run time](#modification).


### Collaborative Editing


Blending of separate layer maps makes the *Landscape Terrain* system friendly for collaborative editing. A team of 3D artists can design separate layer maps simultaneously and develop a large landscape piece by piece without conflicts.


Combined with UNIGINE features for cooperative development (e.g. *[Node Layer](../../../../objects/nodes/layer/index.md), [Node Reference](../../../../objects/nodes/reference/index.md)*), the system enables multiple artists to develop separate areas and layers of landscape of virtually any complexity simultaneously.


To prepare a world with a *Landscape Terrain* for collaborative editing via a VCS, follow this workflow:


1. Prepare node layers:

  1. Create a new *[Node Layer](../../../../objects/nodes/layer/index.md)* for each *Landscape Layer Map* representing a static area of the landscape. For convenience, it is recommended to [reset transformation](../../../../editor2/node_parameters/transformation_common/index.md#transformation_params) of each *Node Layer*.
  2. Make each *Landscape Layer Map* a [child](../../../../editor2/organizing_nodes/index.md#make_child_node) to the corresponding *Node Layer*.
2. After changing the content or parameters of any *Landscape Layer Map*, it only needs to save the parent node layer and commit the changed `*.node` asset and resources via your version control system.
3. Upon checkout and world reloading, the changes will be applied and visible on workstations of other team members.
4. Dynamic and repetitive *Landscape Layer Maps* (such as craters or chunks of tracks) can be saved as *[Node References](../../../../objects/nodes/reference/index.md)*.


### Run-Time Modification


Vehicles leaving tracks while moving or even an excavator digging trenches are easy to implement. Two ways of run-time terrain modification are available:


- **By adding layers**. Spawn new *Landscape Layer Maps* representing chunks of trenches or pits to modify the terrain surface. This way is similar to using [Decals](../../../../objects/decals/index.md): each layer is a separate node, so you can control each modification separately. Furthermore, using *Landscape Layer Maps* implies no data density limits, enabling you to achieve realistic results with high-quality insets. ![](runtime_trace_low.gif)
- **By modifying terrain buffers**. Low-level terrain CPU- or GPU-based modification via API is as simple as 1, 2, 3: For more details on performing run-time CPU- and GPU-based modification, please refer to the *[Landscape Class](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md)* article.

  1. Set the desired area, and the Engine copies a part of terrain data for this area to a buffer.
  2. Modify the buffer as you want (height, color, masks, or all of them at once).
  3. Upon completion the Engine pastes the buffer back to the terrain replacing old data.


Adjust [streaming settings](../../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_settings) to achieve appropriate performance of run-time terrain modification.


## Tiling and Streaming


A scene may contain thousands of *Landscape Layer Maps*, so the full-size graphic data of the *Landscape Terrain* may be too large to fit in the video memory in its entirety. Instead all resources are decomposed into smaller rectangular sections � **tiles** of variable density depending on the distance to the camera.


![](visible_tiles.png)


Individual tiles are asynchronously loaded into the main virtual texture when necessary � only if currently seen by the camera � from the lowest to the highest available MIP-level. All tiles have the fixed resolution in video memory - 128�128 px.


![](streaming_tiles_low.gif)

*Unoptimized streaming settings cause noticeable loading of tiles when the camera moves.*


Thus, the *Landscape Terrain* detail level and performance are highly affected by the number of viewports and their resolution. When developing a project using a Landscape Terrain, **performance and memory consumption should be considered and tuned for the set of cameras and screen resolution of the target platform**.


Flexible streaming settings make it possible to configure terrain rendering even for computers with a limited VRAM capacity, but these settings depend on the content used (distances, level of detail, etc.) and requirements (the number of cameras and viewports, etc.) and are **to be adjusted for each project individually**.


For more details on configuring streaming settings, please refer to the [**Configuring Visualization and Performance**](../../../../objects/objects/terrain/landscape_terrain/settings.md#streaming) and [**Landscape Terrain Optimization**](../../../../content/optimization/terrain/index.md#landscape) articles.


## Details


*Landscape Terrain* object stores visual settings for **20** detail masks intended for reaching better level of visual quality in close up views. Details represent arbitrary albedo, roughness and height (displacement) data, so you can drastically improve the look of the landscape terrain. Details are applied according to [masks](#layers_masks) of *Landscape Layer Maps*.


![](details_off.png) ![](details_on.png)


> **Notice:** If your project requires detection of collisions with the terrain surface, you should keep in mind that Details don't participate in [Intersection and Collision Detection](#intersections), so it's not recommended to apply intense displacement using details since visual inconsistency may appear.


Detail settings available in *ObjectLandscapeTerrain* parameters allow defining the detail visual appearance, adding up to **1024** details to a mask and defining the material of each detail.


![](detail_parameters.png)

*Detail parameters are available on theNodetab of theObjectLandscapeTerrainparameters.*


For more information on adding details, please refer to the [**Configuring Details**](../../../../objects/objects/terrain/landscape_terrain/details.md) article.


## Intersections and Collisions


The *Landscape Terrain* system provides intersection and collision detection with the terrain surface the same way as for usual meshes. To enable collisions and/or intersection detection for a landscape:


- Turn on the **Collider Object** flag on the *Node* tab.
- Switch to the *Surface* tab and enable the Intersection and Collision flags, configure the [bit masks](../../../../principles/bit_masking/index.md).
- For landscape layer maps that should take part in collisions and intersections enable the corresponding [**Collision and Intersection**](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#landscape_asset_parameters) flags.


> **Notice:** [Details](#details) don't participate in Intersection and Collision Detection.


Intersections are detected with a variable precision, starting from a lower value and ending up with a higher one.


Normally there's no need to modify these values. In case of intersection detection errors you can open *Landscape Terrain* parameters and try tweaking start and end precision values and enable cubic filtering of textures for optimum balance, but be careful as it may significantly affect performance and accuracy:


![](landscape_terrain_parameters.png)


| Collision Bicubic Filter | Enables bicubic filtering of textures for collision detection. |
|---|---|
| Intersection Bicubic Filter Normal | Enables bicubic filtering of the normal texture for intersection detection. |
| Intersection Bicubic Filter Height | Enables bicubic filtering of the height texture for intersection detection. |
| Intersection Precision Begin | Starting precision of intersection detection. |
| Intersection Precision End | Ending precision of intersection detection. |


## Decal-Based Holes


In some cases you may need to cut out an area of the terrain surface. For this purpose the **Decal-Based Holes** feature is supported by *Landscape Terrain*.


Make sure the [**Holes**](../../../../editor2/settings/render_settings/landscape/index.md#holes) feature is enabled and place any [decal](../../../../objects/decals/index.md) (orthographic, projected or a mesh one) with the *[decal_terrain_hole_base](../../../../content/materials/library/decal_terrain_hole_base/index.md)* material assigned over the desired location:


1. In the Create menu, select *Landscape -> Hole Projected* (or another one). Click in the Editor Viewport to add the decal. ![](decal_hole_create.png)
2. Adjust the transform and material parameters of the decal.


This will create a hole in the *Landscape Terrain* surface.


![](decal_hole.png)

*A decal-based hole with a circlemaskapplied.*


Accurate [intersection](../../../../code/usage/intersections/index_cpp.md) with decal-based terrain holes is supported, enabling [collision detection](../../../../principles/physics/collision/index.md) as well as all corresponding Editor features such as [selection](../../../../editor2/select_position_nodes/index.md#select_nodes), [snapping to surface](../../../../editor2/select_position_nodes/index.md#snap_surface), etc.

> **Notice:** Intersection and collision accuracy significantly depends on the terrain polygon count. The higher the number of polygons, the higher the accuracy.


## Customizing Terrain Surface


Integration of static meshes into the landscape is simpler with the use of **Terrain Lerp** feature.


Enabled *[Terrain Lerp](../../../../content/materials/library/mesh_base/index.md#terrain_lerp)* state of the *[mesh_base](../../../../content/materials/library/mesh_base/index.md)* material marks an object to be covered by projected textures of the Landscape Terrain what makes it unnecessary to set up materials for its surfaces.


![](../terrain_global/terrain_lerp_preview_1.png) ![](../terrain_global/terrain_lerp_preview_2.png)


The feature is suitable for creating any insets such as caves and tunnels through mountains on the terrain. As an example, on the picture below a tunnel is integrated by just cutting some area of the terrain [with a decal](#decal_holes) and replacing it with a mesh with the *[Terrain Lerp](../../../../content/materials/library/mesh_base/index.md#terrain_lerp)* parameter enabled.


![](../terrain_global/holes/tunnel.png)

*A mesh integrated in a terrain with theTerrain Lerpenabled.*


## Video Tutorial: Landscape Terrain
