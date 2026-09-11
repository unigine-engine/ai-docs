# Terrain Modification & Usage

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Asynchronous Terrain Albedo Height Brushes

This sample demonstrates several techniques for destructive runtime modification of the **[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)** by altering the underlying textures of a **[Landscape Layer Map](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)** using **[Landscape::asyncTextureDraw()](../../../api/library/objects/landscape_terrain/class.landscape.md#asyncTextureDraw_UGUID_ivec2_ivec2_int_void)** in combination with custom base materials.


It features three distinct painting modes:


- **Albedo Painter:** Allows painting of the terrain's albedo texture using a customizable brush (texture, mask, size, angle, opacity, and color).
- **Height Painter:** Enables height modification using height values and scaling options, along with support for alpha or additive blending modes.
- **Height To Albedo:** Converts terrain height data into albedo colorization based on a user-selected gradient and specified height range.


You can dynamically change brush parameters through a UI panel (textures, masks, gradient, size, spacing, angle, opacity, and color) and visualize the brush as an orthographic decal projected onto the terrain.


**Use Cases**


- Runtime terrain painting tools for level editors and world-building interfaces
- Terrain sculpting systems in games or simulations
- Custom height-based texturing workflows for stylized or procedurally modified terrains
- Visualization of terrain blending behavior with UI interactivity.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/asynchronous_terrain_albedo_height_brushes*
## Asynchronous Terrain Data Fetch

This sample demonstrates how to retrieve detailed information from a **[LandscapeTerrain object](../../../objects/objects/terrain/landscape_terrain/index.md)** at any arbitrary point on its surface using **[LandscapeFetch](../../../api/library/objects/landscape_terrain/class.landscapefetch.md)**.


**Key Features:**


- Casts a ray from the camera through the mouse cursor
- Performs asynchronous intersection tests with the terrain
- Retrieves:

  - Surface **height**
  - Surface **normal**
  - **Blend mask values** for all configured layers
  - Surface albedo
- Visualizes results in the viewport with:

  - A **normal vector**
  - A floating **text box** showing the terrain fetch data.


This feature can be used for terrain debugging, editor extensions, dynamic content placement, and real-time visualization of terrain attributes.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/asynchronous_terrain_data_fetch*
## Asynchronous Terrain Mask Brushes

This sample demonstrates real-time painting of **[Landscape Layer Map](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)** mask data using a customizable brush system.

 **Key Features:**
- Terrain modification using *[Landscape::asyncTextureDraw()](../../../api/library/objects/landscape_terrain/class.landscape.md#asyncTextureDraw_UGUID_ivec2_ivec2_int_void)*
- Brush parameters:

  - Texture, mask
  - Size, angle, spacing, opacity
- Visual brush preview via *[DecalOrtho](../../../objects/decals/ortho/index.md)*
- Powered by a custom base material (**landscape_mask_brush.basemat**) for applying edits.


Ideal for runtime editing tools, vegetation control, or any system requiring dynamic terrain mask authoring.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/asynchronous_terrain_mask_brushes*
## Creating Detail Layers

This sample demonstrates how to add and manage detail layers for a **[LandscapeTerrain](../../../objects/objects/terrain/landscape_terrain/index.md)** object using the *[getDetailMask()](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain.md#getDetailMask_int_TerrainDetailMask)* and *[addDetail()](../../../api/library/objects/landscape_terrain/class.terraindetailmask.md#addDetail_TerrainDetail)* methods.


It dynamically creates and configures three types of terrain details:


- **Grass**
- **Stone**
- **Snow caps** (simple white material applied based on elevation using height constraints - no texture).


**Each detail is:**


- Mapped to a separate detail mask
- Assigned a custom material
- Ordered visually using *[swapRenderOrder()](../../../api/library/objects/landscape_terrain/class.terraindetailmask.md#swapRenderOrder_TerrainDetailMask_void)* to ensure natural blending (stone below grass, grass below snow).


This setup is useful for biome-style terrain detailing, visual layering of materials, and real-time terrain customization.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/creating_detail_layers*
## Generating Mesh From Terrain

This sample demonstrates how to generate a procedural mesh (**[ObjectMeshDynamic](../../../objects/objects/mesh_dynamic/index.md)**) that represents a selected region of the **[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)**.


**Key Features:**


- Terrain data (height and albedo) is fetched at runtime using **[LandscapeFetch](../../../api/library/objects/landscape_terrain/class.landscapefetch.md)**
- Mesh resolution, position, scale, and rotation can be customized via UI
- Optionally render a bounding box and wireframe overlay
- Ideal for:

  - Runtime terrain previews
  - Simplified **LOD** meshes or data extraction for analysis/simulation.


The generated mesh uses a basic material and includes color data sampled from the terrain's albedo layer. Use the **Generate** button to fetch terrain data and construct the mesh in real time.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/generating_mesh_from_terrain*
## Generating Terrain From Textures

This sample demonstrates how to dynamically generate a **[Landscape Layer Map](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)** using tiled **albedo, height,** and **mask** textures. The process uses the **[LandscapeMapFileCreator](../../../api/library/objects/landscape_terrain/class.landscapemapfilecreator.md)** and **[LandscapeMapFileSettings](../../../api/library/objects/landscape_terrain/class.landscapemapfilesettings.md)** APIs to build a fully functional **.lmap** file and configure it for use with the **[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)** object.


**Key features:**


- Supports tile-based input with user-defined grid size and resolution
- Loads and validates image tiles for:

  - **Albedo**
  - **Height**
  - **Grass mask**
  - **Stone mask**
- Applies blend settings for each layer using ***[LandscapeMapFileSettings](../../../api/library/objects/landscape_terrain/class.landscapemapfilesettings.md)***
- Automatically creates and attaches the landscape objects to the world.


This workflow is ideal for runtime terrain generation, procedural terrain tools, or editor extensions that need to assemble terrain data from image sources.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/generating_terrain_from_textures*
## Height Slicing

This sample demonstrates a hybrid approach to terrain editing using both **non-destructive** (using multiple **[Landscape Layer Maps](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)**) and **destructive** (using **[Landscape::asyncTextureDraw()](../../../api/library/objects/landscape_terrain/class.landscape.md#asyncTextureDraw_UGUID_ivec2_ivec2_int_void)** method) **[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)** modification techniques.


**It works by:**


- Sampling height data from a **Source** Landscape Layer Map
- Using **Landscape::asyncTextureDraw()** in combination with a custom material additive height blending to modify the **Target** Layer Map if the sampled height is above the provided threshold:

  - The target terrain is flattened (clamped to the height threshold)
  - The target albedo (on the threshold height level) is painted orange.


This sample is ideal for tools that require selective terrain stamping, erosion masks, or custom terrain sculpting.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/height_slicing*
## Polygon-Based Procedural Modifications

This sample demonstrates procedural generation of polygon objects from world points, enabling runtime landscape editing and object placement.


It dynamically creates polygonal geometry and applies it in multiple contexts:


- **ObjectMeshStatic** - creates *ObjectMeshStatic* and places it at the center of the *WorldBoundBox* formed by the points.
- **DecalMesh** - creates *DecalMesh* and places it at the center of the *WorldBoundBox* formed by the points.
- **DecalOrtho** - renders mesh into a texture applied to the albedo slot of *DecalOrtho* material.
- **Terrain mask** - renders mesh into Layer Map mask to control clutter placement (cubes) on landscape.
- **Level terrain** - levels terrain height to the lowest point value within the polygon area.
- **Lower terrain** - lowers terrain by 20 units within the polygon area.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/polygon_based_procedural_modifications*
## Real-Time Excavation

This sample demonstrates **destructive, real-time modification** of a **[Landscape Layer Map](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)** using a 3D object (e.g., a tractor grader) as an excavation tool.


**Key features:**


- Samples base terrain height from a **source layer**
- Projects the grader's **depth map** onto the terrain using an **orthographic camera**
- Uses a custom material (**digging_tool.basemat**) to update height data and clear mask layers
- Applies updates asynchronously using *[Landscape::asyncTextureDraw()](../../../api/library/objects/landscape_terrain/class.landscape.md#asyncTextureDraw_UGUID_ivec2_ivec2_int_void)*
- Supports full interactive movement and rotation of the grader with the *Manipulator* widget.


This sample is ideal for developing terrain deformation mechanics in simulators, construction games, or any scenario requiring runtime landscape sculpting based on object interaction.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/real_time_excavation*
## Real-Time Terrain Rut Deformation

This sample demonstrates non-destructive runtime modification of the **[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)** by dynamically spawning multiple **[Landscape Layer Map](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)** beneath moving objects (such as vehicles or characters) to create realistic track imprints on the terrain.
 Each track is rendered using a dedicated **[Landscape Layer Map](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)** that blends additively with the terrain�s height data and alpha blends with the albedo, producing visually convincing trails without altering the original terrain layers.


**Key Features**


- Automatic track spawning based on object movement
- Track maps are spawned only when the object has moved a minimum distance (user-defined)
- The number of active track maps is limited for performance (configurable limit)
- Albedo and height blending are handled via standard non-destructive layering, ensuring easy track removal or replacement.


**Customizable Parameters**


- **Min Distance Between Tracks** - Controls how frequently new track maps are spawned based on movement
- **Max Number of Track Maps** - Caps the number of simultaneously active track layers to manage memory and performance.


**Use Cases**


- Vehicle or character track systems for games and simulations
- Temporary terrain effects (e.g., tire marks, footprints, sliding trails)
- Runtime procedural content that doesn't permanently modify base terrain.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/terrain_modification_usage/real_time_terrain_rut_deformation*
