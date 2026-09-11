# Converting Landscape Terrain to Geometry with Landscape Exporter


## Overview


![](terrain_manipulator.png)


> **Warning:** The **Landscape Exporter** tool is intended for selective terrain adjustment use in specific tasks, not as an alternative terrain system.


The *[Landscape Terrain](../../objects/objects/terrain/landscape_terrain/index.md)* system provides advanced simulation of terrain, but in some particular cases even that might be insufficient. Converting a finalized landscape into geometry gives access to features unavailable for *ObjectLandscapeTerrain*. Besides, once the landscape is complete, its extensive functionality may become redundant and a simplified geometry version can potentially save performance in some projects, since using multiple high-resolution *[Landscape Layer Maps](../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)* is computationally expensive, especially in VR.


The **Landscape Exporter** tool scans the specified landscape area, captures its terrain height and albedo data, and stores it in the vertex structure of the output `.mesh` or `.fbx` file.


> **Notice:** The recommended *Landscape Terrain* size to export is not more than **1x1 kilometer (or smaller)**.


The **maximum** supported *Landscape Terrain* size is **10x10 kilometers**, but it is strongly recommended to keep it as small as necessary for your particular purpose, as converting large terrains will cause noticeable inaccuracies in the resulting mesh due to floating-point precision limits of the *[Mesh class](../../code/usage/mesh_class/index_cpp.md#indices)*. Additionally, large, high-poly meshes consume a considerable amount of video memory.


In general, *ObjectLandscapeTerrain* remains more efficient for simulation, as it uses *[adaptive hardware tessellation](../../editor2/settings/render_settings/landscape/index.md#geometry_progression)* with displacement mapping and *[streaming](../../objects/objects/terrain/landscape_terrain/settings.md#streaming)*. However, there are several specific terrain-related cases where using geometry is more practical or necessary.


## Use Cases


1. **Using Terrain in Third-Party Applications**. Finalize the landscape and export it as an `.fbx` file for offline rendering or use in DCC tools (e.g., *After Effects, 3ds Max, Maya*). Larger landscapes and higher output resolutions produce proportionally larger files, so ensure the target application can handle them. > **Notice:** The `.mesh` format is proprietary to UNIGINE and cannot be read by third-party software.
2. **Adding shadows**. *ObjectLandscapeTerrain* doesn't cast shadows or self-shadows from light sources, and currently supports only *[screen-space shadows](../../objects/lights/parameters/index.md#ss_shadow_settings)*. If landscape shadows are required (e.g. for a huge mountain or a canyon in the scene), to minimize performance cost:

  - Use *ObjectLandscapeTerrain*, but create a low-poly mesh version of the terrain for shadow casting, hidden from the viewport with *[shadow masks](../../content/optimization/lights/index.md#masking)*.
  - Keep polygon count as low as possible by decreasing *[mesh grid resolution](#output_resolution)* while preserving acceptable visual fidelity. ![](mesh_size.png)
  - **Export only the necessary terrain fragments** instead of the entire landscape.
3. **Adding Tunnels and Caves.** Some features (caves, tunnels, overhangs, walkable areas, precise snapping buildings and other assets to the surface, etc.) cannot be implemented directly with *ObjectLandscapeTerrain* (e.g. *[decal-based tunnels](../../objects/objects/terrain/landscape_terrain/index.md#decal_holes)* don't allow visibility through them). Export the **minimal required part** of the landscape with all the necessary adjustments, modify it in a 3D editor (3DSMax, Maya, etc.), re-import and blend it seamlessly into the existing landscape using the *[Terrain Lerp](../../content/materials/library/mesh_base/index.md#terrain_lerp)* feature.
4. **Using Terrain as a Distant Background Element.** When terrain is used as a static background, converting it to a mesh can simplify the setup. However:

  - A mesh has a fixed polygon count, while *ObjectLandscapeTerrain* uses geomorphing and built-in *[optimizations](../../objects/objects/terrain/landscape_terrain/settings.md)*, which are often more efficient.
  - For distant geometry, use **simplified low-poly meshes** and create *[LODs](../../principles/world_management/index.md#lods)*. ![](vertex_density.png) *Vertex Density heatmap.*
  - **Use a lower export mesh grid resolution for VR** to reduce memory consumption while maintaining acceptable visual quality.


### Recommendations


If you choose to use the *Landscape Exporter* tool, follow these recommendations:


- **For realtime projects (especially VR)**: keep the number of polygons as low as possible, particularly for flat landscapes (an acceptable error limit may be around 100 meters or more).
- **For offline or third-party use**: you can export larger terrains as `.fbx` files - some DCC tools support double-precision coordinates and can handle larger data sets. However, such files are not intended for importing back into the Engine as this will entail *[positioning errors](../../code/double_precision/index.md#positioning_error)*.
- **Precision and coordinate handling**: when exporting terrain areas far from the world origin, precision errors may occur when rendering the generated mesh. Use the *[Corner of Bound](#mesh_pivot)* pivot mode to place the pivot (center of mesh's local coordinate system) to the corner of the area's bounding box. The `.fbx` format is preferable for large landscapes due to its double-precision coordinate support. > **Notice:** The *[exported mesh](../../editor2/exporting_nodes/index.md#export_to_mesh)* will be saved in the world coordinates.
- **For flight simulators**: using mesh landscapes in flight simulators is generally inefficient - Landscape streaming provides much better scalability, while meshes always keep a constant polygon count regardless of distance. > **Notice:** Do not use mesh landscapes for flight simulators - a static mesh wastes resources rendering details that the user will never see.
- You can export the landscape in parts or as a single mesh - *[profile](../../tools/profiling/index.md)* to determine which approach works best for your project.


## Tool Overview


To open the *Landscape Exporter* tool window, go to *Tools -> Landscape Exporter* on the *[Menu Bar](../../editor2/interface/index.md#menu_bar)* of UnigineEditor.


![](landscape_export.png)


The *Landscape Exporter* tool window will open:


![](landscape_export_ui.png)


Alternatively, in the *World Nodes* hierarchy, right-click on an *ObjectLandscapeTerrain* or *LandscapeLayerMap* node and choose *Export to -> Mesh*.


![](landscape_export_to_mesh.png)


This opens the tool window and automatically sets node-specific *[output geometry parameters](#landscape_export_output)* (resolution, area bounds, rotation, and height limits) based on the selected node(s) data. If applied to an *ObjectLandscapeTerrain*, its child *LandscapeLayerMap* nodes data is collected recursively, and the optimal export parameters are derived from their values. For more details, see the *[Preset Default Geometry Parameters](#take_parameters)* section below.


### Landscape Layer Map Nodes


This section displays all the *LandscapeLayerMap* nodes in the currently loaded world. Node selection in the list is synchronized with the *World Node* hierarchy.


| **Use** | Defines whether the selected Layer Map is to be exported or ignored. > **Notice:** Disables the corresponding node in the *World Nodes* hierarchy if unchecked. |
|---|---|
| **Name** | Node name in the *World Nodes* hierarchy. |
| **Resolution** | Layer Map resolution (in pixels). |
| **Size** | Layer Map size (in units). |
| **Minimum Height** | Minimum height of the Layer Map (in units). |


### Output Geometry


This section displays the export parameters.


| **Show Output Area Size** | Enables visualization of the selected area in the viewport. |
|---|---|
| **Output Geometry Resolution** | Defines polygon density of the exported mesh. The landscape area is divided into a grid of this resolution (e.g., 256x256), with a vertex placed at each grid point. Lower values create a simpler, more performant mesh, while higher values preserve more detail. > **Warning:** Using a value higher than the source *LandscapeLayerMap* resolution will not increase visual quality and only adds unnecessary vertex overhead. |
| **Output Area Position** | Center position of the export area. |
| **Output Area Size** | Size of the export area manipulator (in units), defining the size of the landscape region to export. The generation process will include data from all *[enabled](#use)* Layer Maps within this area. |
| **Output Area Rotation** | Rotation of the export area manipulator (in degrees). |
| **Information Lost Height** | Height value (in units) to be set for areas where landscape data is not available (e.g. missing Layer Map data, or no Layer Maps in the area). |
| **Pivot** | Defines the generated mesh pivot. Available modes: - **World Origin** - the mesh pivot is relative to the world center. - **Corner Of Bound** - the mesh pivot is placed at the corner of its bounding box. |
| **File Name** | Name of the generated output file with exported geometry. |
| **Destination** | Target directory where the output file will be saved. > **Notice:** If the destination is within the `/data` folder, the created asset is automatically placed in the world (as the selected node) in the initial location of the exported fragment. Otherwise, the output folder will open in your system's file explorer, when generation is complete. |
| **Format:** | Output file format - **Mesh** - a `.mesh` file will be created. - **FBX** - an `.fbx` file will be created. |
| **Overwrite File If Name Match** | Replaces the existing file in the destination folder if a file with the same name already exists. |
| **Export Landscape** | Starts mesh generation. At least one *LandscapeLayerMap* must be marked with *[Use](#use)* for the button to become active. |


> **Notice:** The exported mesh has the landscape albedo information embedded as *[**vertex color** data](../../code/usage/mesh_class/index_cpp.md#vertex_color)*. All landscape masks data is discarded.


### Preset Default Geometry Parameters


When opened via the *World Nodes* hierarchy, the tool automatically applies the *Take Geometry Parameters* option using the selected node(s) data as defaults for:


- **Output Geometry Resolution** - uses the highest Layer Map resolution value if multiple nodes are selected.
- **Output Area Position** - sets the center position for the selected node(s).
- **Output Area Size** - expands to include all selected nodes.
- **Output Area Rotation** - if changed, sets to 0 when multiple nodes are selected.
- **Information Lost Height** - uses the lowest value if multiple nodes are selected.


You can also activate *Take Geometry Parameters* via the context menu in the *[Landscape Layer Map Nodes](#landscape_export_nodes)* list by right-clicking a *LandscapeLayerMap* node(s).


![](take_parameters.png)


## Using the Tool


To generate geometry from a landscape in your project:


1. Prepare the landscape in the Editor. ![](landscape_prep.png)
2. Open the *[Landscape Exporter](#landscape_export_tool)* tool.
3. Specify the area to export using the *Output Area Position, Output Area Size* and *Output Area Rotation* parameters in the tool window.
4. Adjust the *Output Geometry Resolution* - lower resolution is wider grid step and lower polygon count.
5. Select the output file format: `.mesh` or `.fbx`.
6. Set other parameters according to your needs. ![](landscape_set.png)
7. Press the ***Export Landscape*** button to start generation. If your destination path is within the project's `/data` folder, the mesh will be automatically added to your scene in the initial location of the exported fragment, otherwise the target folder will open. ![](landscape_mesh.png)
8. You can continue working with the mesh in the Editor or make any further modifications you need in DCC apps (e.g. model custom geometry such as tunnels or overhangs). > **Notice:** The albedo data is stored as vertex colors.
9. To seamlessly blend a mesh fragment into the main terrain, enable the *[Terrain Lerp](../../content/materials/library/mesh_base/index.md#terrain_lerp)* option in the node's surface *Material -> States* section. This smoothly interpolates the mesh with the underlying *Landscape Terrain* ![](landscape_lerp.png)
