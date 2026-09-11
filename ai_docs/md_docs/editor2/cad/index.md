# CAD Import Guide


CAD assets are imported into UNIGINE as [any other asset](../../editor2/assets_workflow/assets_create_import.md#import). The following CAD formats are supported:


- IGES
- STEP
- STL
- BREP


> **Notice:** For the CAD asset to be imported, the *[CadImporter](../../code/plugins/cadimporter/index.md)* plugin must be loaded.


## Importing CAD Asset


When you import a CAD asset, the import settings window appears:


![](cad_import.png)


> **Notice:** To simplify sequential import of multiple similar assets, *Asset Browser* remembers previous asset import settings and offers to use them by default. To reset import settings to system defaults use the **Restore Defaults** button.


The list of available import options includes the following:


### Mesh Import Options


| Import Meshes | Import geometry meshes from the file. |
|---|---|
| Merge Static Meshes | Merges all children static meshes in one (names it after the parent mesh). All of the meshes surfaces will be copied and shown in the *Surfaces* hierarchy. |
| Merge Surfaces by Materials | Enables merging surfaces that have the same materials. |
| Split by Grid | Enables splitting of imported meshes. Too large models having sizes, that exceed 10000 units may have various artefacts (jitter, etc.) associated with positioning errors. You can eliminate such artefacts by splitting your mesh into multiple separate meshes. To do so, just enable this option and set the size of the grid cell (see the **Grid Size** parameter below) to be used for mesh splitting. > **Notice:** This option does not split surfaces. |
| Grid Size | Size of the grid cell to split imported meshes, in units. |
| Repivot to Center | Places a pivot of generated mesh to its center. Can be used for meshes having their geometry located too far from their pivot, as this may lead to various artefacts (jitter, etc.) associated with positioning errors. |
| Optimize Vertex Cache | Enables vertex cache optimization. This option reorders an indexed triangle list to improve vertex cache utilization at runtime. It can be turned off to accelerate saving process; however, it should always be turned on if saving the final version. |
| Linear Deflection | Limits the distance between triangles and the original surface. It is used to define triangulation of the imported model together with the *[Angular Deflection](#angular_deflection)*. |
| Angular Deflection | Limits the angle between adjacent triangles generated from a surface. It is used to define triangulation of the imported model together with the *[Linear Deflection](#linear_deflection)*. |
| Use LODs | Defines if [Levels of Detail (LODs)](#lods) are to be used for the imported model. |


### Levels of Detail


Automatic LOD Generation feature based on the [*meshoptimizer* library](https://github.com/zeux/meshoptimizer) will help create several variations of one object with different level of detail ([LODs](../../principles/world_management/index.md#lods)).


![](lods_autogen.png)


To use the feature choose **Auto-Generated** in the **Use LODs** dropdown and configure the settings listed below - the Engine will do the rest, generating all LODs automatically based on your configuration.


> **Notice:** See the video tutorial on [how to configure LODs](../../videotutorials/how_to/how_to_basics/configure_lods.md) for more details.


You can also enable the **[Merge Static Meshes](#merge_static_meshes)** option for more optimization.


| Number of LODs | Number of Levels of Detail. |
|---|---|
| Target Polycount | Desired degree of geometry simplification for each LOD (target geometry complexity percentage from the initial number of polygons). > **Notice:** Please keep in mind that this is only a *target* value, that in some cases may be unreachable for the mesh simplifier. In case any artefacts with the topology of the simplified meshes occur, try increasing this value. |
| Normals Preserve | This parameter indicates the impact of normals on mesh topology simplification. *Higher* values increase the influence of normals, by the value of 0 normals are ignored. Avoid setting too *high* values as this may restrict simplifier too much and simplification will fail (as normals may differ significantly). Default setting is suitable for most cases. |
| Recalculate Normals by Angle | Enables recalculation of normals in the process of mesh simplification based on the specified angle threshold. If an angle between the normals to adjacent polygons exceeds this value, normals will be recalculated between them to smoothen the look of the geometry and get rid of possible shading issues. |
| Min Visibility | The minimum distance on which this LOD is visible in camera local axes. -inf � the LOD is visible by default. |
| Max�Visibility | The maximum distance on which this LOD is visible in camera local axes. inf � the LOD is visible by default. |
| Min Fade | Over this distance, the surface fades in until it is completely visible. Along this distance the engine automatically interpolates the level of detail from completely invisible to completely opaque. Fading-in starts when the camera has reached the minimum distance of surface visibility and is in the full visibility range. |
| Max Fade | Over this distance, the surface fades out until it is completely invisible. Fading out starts when the camera has reached the maximum distance of surface visibility and is out of the full visibility range. |


### Lightmaps Options


| UV For Lightmap | UV channel to store the lightmap. |
|---|---|
| Lightmap Target Resolution | Resolution of the resulting lightmap. |
| Unwrap UV Channel 0 | Enables automatic unwrapping for UV Channel 0. |
| Unwrap UV Channel 1 | Enables automatic unwrapping for UV Channel 1. |


### Material Import Options


| Import Materials | Enables importing materials from the file. Materials are stored in the `.step, .stp` and `.iges, .igs` files. When importing, only the albedo (diffuse) color is copied. Other material parameters should be set up after the model is added to the scene. |
|---|---|
| Assets Mode | Enables to choose whether to use existing materials or to overwrite them with the ones imported. Available options: - **Take From Assets** � use existing materials (if any). - **Overwrite Assets** � overwrite existing materials (if any). |
| Base Materials Mode | Enables to choose the base material for the imported materials. Available options: - **Inherited Material Graphs** - an autoselected graph-based material is used as the base material. This mode finds the most suitable autogenerated graph-based material with the appropriate functionality and inherits the imported materials from it. If such graph-based material isn't found in the project, it will be autogenerated and used as the base one. > **Notice:** This mode allows reusing the existing graph-based base materials and avoiding creation of multiple unique base materials when importing CAD files. - **Unique Material Graphs** - an autogenerated graph-based material is used as the base material. In this mode all the imported materials will be inherited from the unique autogenerated graph-based materials. - **Inherited Mesh Base** - the built-in [mesh_base](../../content/materials/library/mesh_base/index.md) material is used as the base material for the imported materials. |
| Workflow | Provides an interface to choose a [workflow](../../content/materials/library/mesh_base/index.md#workflow) for the imported physically-based materials (if any). Available options: - **Specular workflow** � use the old standard of textures that was used in the **[mesh_base](../../content/materials/library/mesh_base/index.md)** material (*diffuse, specular, gloss*). - **Metalness workflow** � use the new standard of textures (*albedo, metalness, roughness*). |
| Add Asset Name as Prefix | Appends the name of the imported asset as a prefix to the imported materials names. |
| Add Prefix | Appends the specified prefix for the imported materials names to avoid name collisions. > **Notice:** If multiple CAD models are imported together this feature does not guarantee that all materials with the same names will be preserved, as only one prefix is used for all of them (if two models have different materials named *black*, only one of them shall remain with the specified prefix). To avoid such cases, models should be imported sequentially with different prefixes. |
| Merge Similar Materials | Merge materials with identical settings but having different names. |


### Texture Import Options


| Import Textures | Import textures stored in the CAD file. If textures are imported, the corresponding texture [assets](../../editor2/assets_workflow/index.md#asset_system) are created in the same folder, where the CAD asset is stored. |
|---|---|
| Invert G-Channel For Normal Maps | Invert the G-channel in normal maps. |


### Other Import Options


| Front Axis | Provides an interface to choose an axis to be considered as the forward vector of the World Coordinate System. |
|---|---|
| Up Axis | Provides an interface to choose an axis to be considered as the up vector of the World Coordinate System. |
| Scale | Geometry scale multiplier. > **Notice:** The default unit of length for CAD models can be *millimeter, inch*, etc. On model importing, it is transferred to *meter* used in UNIGINE. So, you may need to scale the model on importing to get the appropriate size. The specified value doesn't affect [scale](../../editor2/node_parameters/transformation_common/index.md#scale) of the model added to the world. |


### Hierarchy Options


This auxiliary section is available in the *[Parameters](../../editor2/interface/index.md#parameters)* window when selecting an imported *CAD* asset in the Asset Browser. It enables you to preview the content of the CAD asset imported with the current [Mesh Import Options](#options_mesh_import).


![](cad_hierarchy.png)


| Nodes | List of nodes obtained from the CAD asset. |
|---|---|
| Surfaces | List of surfaces of the selected node. |
| Use Custom Settings | Enables custom [Lightmaps](#options_uv) options for the selected surface(s). |


### Asset Preview


This section is available in the *[Parameters](../../editor2/interface/index.md#parameters)* window when selecting an imported *CAD* asset in the *Asset Browser*. It allows you to preview the imported model.


![](cad_preview.png)


### Geometry


CAD model can be represented as a single *detail* or as an *assembly*. If parts of the assembly are stored in separate files, you should specify all of them on the assembly import.


To import 3D geometry data contained in a CAD model, you should enable the **[Import Meshes](#import_meshes)** option. When you add the imported geometry to the scene, it will be available in the *World Hierarchy* as a *Dummy Node*:


- If the imported CAD asset stores a detail, a single static mesh will be a child of the *Dummy Node*.
- If the imported CAD asset stores an assembly, the *Dummy Node* will have a hierarchy of child nodes representing parts of the assembly.


![](detail_and_assembly.png)

*A Detail (left) and An Assembly (right)*


By default, the surfaces of each detail of the CAD model that have the same material are merged resulting in a single surface for each detail in most cases.


If you enable the **[Merge Static Meshes](#merge_static_meshes)** option, all child meshes will be combined into a single one. At that, all surfaces of child meshes will be copied to the single parent mesh and will appear in its *Surfaces* hierarchy.


You can also merge the surfaces of the CAD model having the same material assigned by enabling the **[Merge Surfaces by Materials](#merge_surfaces)** option.


Usually, the unit of length of the CAD models differs from *meters*. When importing a model into UNIGINE, it is transferred to *meters*. It may lead to improper size of the imported model: to adjust the scale of the imported geometry, you can use the **[Scale](#scale)** parameter.


It is also possible to optimize the vertex cache when importing geometry. To do so, use the **[Optimize Vertex Cache](#optimize_vertex)** option.


### Materials


A CAD model can also store materials assigned to surfaces of the details. To import materials from a CAD model, enable the **[Import Materials](#import_materials)** option. In this case, the surfaces of the imported model will have the corresponding materials assigned.


> **Notice:** Materials are usually stored in the `.step, .stp` and `.iges, .igs` files. On their importing, only the *albedo (diffuse) color* is copied. Other material parameters should be set up after the model is added to the scene.


When the **[Import Materials](#import_materials)** option is disabled, all surfaces of the model will have the default *mesh_base* material assigned.


When importing materials, you might have a situation when a material with a given name already exists in the project. You can choose whether to overwrite existing materials (the corresponding assets will be overwritten) or not. For this purpose, the **[Overwrite Assets](#cad_assets_mode)** option is used. When unchecked, the existing materials will be used.


Also you can [choose](#materials_mode) the base material for the imported materials: it can be an autoselected/autogenerated [graph-based](../../content/materials/graph/index.md) material or the built-in [mesh_base](../../content/materials/library/mesh_base/index.md) material.


If the **[Base Materials Mode](#materials_mode)** is set to **Inherited Mesh Base**, you should use the **[Workflow](#workflow)** option to set the desired one. UNIGINE supports two workflows for PBR materials: *Metalness* and *Specular*.


## Adding Imported CAD Asset to the World


To add an imported CAD asset to the scene, drag it from the *[Asset Browser](../../editor2/assets_workflow/index.md#asset_browser)* to the *[Viewport](../../editor2/interface/index.md#viewports)* window. The corresponding node will be created and displayed in the *[World Hierarchy](../../editor2/interface/index.md#world_hierarchy)* window. This node will have the same name as the imported CAD asset and a hierarchy of child nodes representing separate objects contained in the model.


![](cad_model_imported.png)


If you double-click the imported CAD asset in the Asset Browser, the `.mesh` and `.node` files generated in run-time and stored in the CAD file will be displayed.
