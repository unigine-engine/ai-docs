# FBX Import Guide


FBX is a file format owned by Autodesk that is used to provide interoperability between various Digital Content Creation (DCC) applications. Most of modern 3D modelling applications support export to FBX: Autodesk Maya, Autodesk 3ds Max, Blender, Modo, etc.


UNIGINE's FBX import pipeline allows simple transfer of content from any DCC application that supports this format.


The advantages of using FBX Import over other importing methods are:


- Static meshes, skeletal meshes, animations, and morph targets are combined in a single file format.
- Multiple assets can be contained in a single file.
- Import of multiple LODs and morph targets in a single import operation.
- Materials and textures can be imported with and applied to meshes.
- Cameras and light sources can also be imported.


Along with importing data from FBX containers, UNIGINE also provides an ability to [export data to `.fbx` files](../../editor2/exporting_nodes/index.md#export_to_fbx).


> **Notice:** For the FBX asset to be imported, the *[FbxImporter](../../code/plugins/fbximporter/index.md)* plugin must be loaded.


## Importing FBX Asset


When you import an FBX asset (just like [importing any other asset](../../editor2/assets_workflow/assets_create_import.md#import)), the import settings window appears:


![](parameters.png)


> **Notice:** To simplify sequential import of multiple similar assets, *Asset Browser* remembers previous asset import settings and offers to use them by default. To reset import settings to system defaults use the **Restore Defaults** button.


The list of available import options covers all components that can be imported from an FBX scene and includes the following:


### Mesh Import Options


| Import Meshes | Import geometry meshes from the file. |
|---|---|
| Use Instances | Imports FBX with mesh instances. When enabled, a single mesh is imported instead of several identical ones. If you add such FBX to the scene, all meshes in the World Hierarchy will refer to the single mesh stored inside the imported FBX container. |
| Merge Static Meshes | Merges all of the children static meshes into a single one (named after the parent mesh). All surfaces of all meshes surfaces will be copied and shown in the *Surfaces* hierarchy. |
| Merge Surfaces by Materials | Enables merging surfaces that have the same materials. |
| Split by Grid | Enables splitting of imported meshes. Too large models having sizes, that exceed 10000 units may have various artefacts (jitter, etc.) associated with positioning errors. You can eliminate such artefacts by splitting your mesh into multiple separate meshes. To do so, just enable this option and set the size of the grid cell (see the **Grid Size** parameter below) to be used for mesh splitting. > **Notice:** This option does not split surfaces. |
| Grid Size | Size of the grid cell to split imported meshes, in units. |
| Repivot to Center | Places a pivot of generated mesh to its center. Can be used for meshes having their geometry located too far from their pivot, as this may lead to various artefacts (jitter, etc.) associated with positioning errors. |
| Optimize Vertex Cache | Enables vertex cache optimization. This option reorders an indexed triangle list to improve vertex cache utilization at runtime. It can be turned off to accelerate saving process; however, it should always be turned on if saving the final version. |
| Correct Triangulation | Enables correct triangulation of meshes, NURBS and patches. > **Notice:** Disabling this option decreases import time, but may lead to triangulation errors resulting in incorrect geometry. |
| Import Tangent Space | Imports built-in tangent space data instead of recalculating it. > **Notice:** If the option is checked, but an FBX asset has no tangent space, it will be calculated with orientation for the right-handed coordinate system. |
| Import Morph Targets | Enables importing morph targets from the file. |
| Morph Target Normals | The morph target import parameter that defines how the normals of the morph target are imported. Three modes are available: - **None** � morph targets normals are the same as in the base mesh. - **Import** � morph targets normals are imported with the 3D asset. - **Recalculate** � morph targets normals are recalculated using the specified *Morph Target Normals Angle* in the range [0, 180]. With the maximum value of 180, all edges become smoothed out. The minimum value of 0 makes the edges sharp. |
| Use LODs | Defines if [Levels of Detail (LODs)](#lods) are to be used for the imported model, as well as the LOD creation and configuration mode. |


### Levels of Detail


To create several variations of one object with different level of detail ([LODs](../../principles/world_management/index.md#lods)) you should have them as separate surfaces of the object. This will allow you to reduce the number of nodes in the hierarchy and simplify the settings of the LODs visibility.


UNIGINE provides automatic assignment and configuration of Levels of Detail based on the name postfixes, enabling you to create and export different meshes for different LODs of your model in a single FBX file. When naming these meshes, you should add a postfix to specify the LOD each mesh represents. You can also specify visibility and fade distances for each LOD of your model at the importing stage, saving time, as you don't have to adjust these settings for the surfaces on the scene - choose **Combine by Postfixes** in the **Use LODs** dropdown.


> **Notice:** See the video tutorial on [how to configure LODs](../../videotutorials/how_to/how_to_basics/configure_lods.md) for more details.


You can also enable the **[Merge Static Meshes](#fbx_merge_static_meshes)** option for more optimization.


1. Choose **Combine by Postfixes** in the **Use LODs** dropdown. ![](combine_by_lods.png) This will show additional LODs settings: | Max LODs Count | Number of Levels of Detail. | |---|---| | Postfix | Postfix added to the surface name to disambiguate the current LOD from other surfaces. | | Min Visibility | The minimum distance on which this LOD is visible in camera local axes. -inf � the LOD is visible by default. | | Max�Visibility | The maximum distance on which this LOD is visible in camera local axes. inf � the LOD is visible by default. | | Min Fade | Over this distance, the surface fades in until it is completely visible. Along this distance the engine automatically interpolates the level of detail from completely invisible to completely opaque. Fading-in starts when the camera has reached the minimum distance of surface visibility and is in the full visibility range. | | Max Fade | Over this distance, the surface fades out until it is completely invisible. Fading out starts when the camera has reached the maximum distance of surface visibility and is out of the full visibility range. |
2. Select the number of LODs that are stored in the FBX container.
3. For each LOD, define a postfix that will be used to group objects in an FBX file into a corresponding LOD. > **Notice:** The postfix must be the same as the one used when creating objects in a 3D editor. The names of generated surfaces will be as follows: *material_name + LOD_postfix*.
4. Specify the minimum and maximum visibility and fade distances for each LOD.


#### Automatic Generation of LODs


Automatic LOD Generation feature based on the [*meshoptimizer* library](https://github.com/zeux/meshoptimizer) will help in case you only have a high-poly model, saving you a lot of time on preparing levels of detail manually.


![](lods_autogen.png)


To use the feature choose **Auto-Generated** in the **Use LODs** dropdown and configure the settings listed below - the Engine will do the rest, generating all LODs automatically based on your configuration.


| Number Of LODs | Number of Levels of Detail. |
|---|---|
| Postfix | Postfix added to the surface name to disambiguate the current LOD from other surfaces. |
| Target Polycount | Desired degree of geometry simplification for each LOD (target geometry complexity percentage from the initial number of polygons). > **Notice:** Please keep in mind that this is only a *target* value, that in some cases may be unreachable for the mesh simplifier. In case any artefacts with the topology of the simplified meshes occur, try increasing this value. |
| Normals Preserve | This parameter indicates the impact of normals on mesh topology simplification. *Higher* values increase the influence of normals, by the value of 0 normals are ignored. Avoid setting too *high* values as this may restrict simplifier too much and simplification will fail (as normals may differ significantly). Default setting is suitable for most cases. |
| Recalculate Normals by Angle | Enables recalculation of normals in the process of mesh simplification based on the specified angle threshold. If an angle between the normals to adjacent polygons exceeds this value, normals will be recalculated between them to smoothen the look of the geometry and get rid of possible shading issues. |
| Visibility / Fade Distances | [See their description above.](#fbx_combine_min_visibility) |


### Lightmaps Options


| UV For Lightmap | UV channel to be used for lightmaps. |
|---|---|
| Lightmap Target Resolution | Resolution of lightmap texture. |
| Unwrap UV Channel 0 | Enables automatic unwrapping for UV Channel 0. |
| Unwrap UV Channel 1 | Enables automatic unwrapping for UV Channel 1. |
| Unwrap UV Version | Approach to generating UV atlases: - **Xatlas V0** � basic unwrapping (for backward compatibility) - **Xatlas V1** � improved unwrapping > **Warning:** Changing this setting during reimport may result in the lightmap being lost. |


### Hierarchy Options


![](parameters_hierarchy.png)


This auxiliary section is available in the *[Parameters](../../editor2/interface/index.md#parameters)* window when selecting an imported FBX asset in the Asset Browser. It enables you to preview the content of the FBX asset according to the current [Mesh Import Options](#options_mesh_import).


| Nodes | List of nodes obtained from the FBX asset. |
|---|---|
| Surfaces | List of surfaces of the selected node. |
| Use Custom Settings | Enables custom [Lightmaps](#options_lightmaps) options for the selected surface(s). |


### Material Import Options


| Import Materials | Enables importing materials from the file. |
|---|---|
| Assets Mode | Enables to choose whether to use existing materials or to overwrite them with the ones imported. Available options: - **Take By Name From Assets Or Create New** � use existing materials if available; if there is no material with such name, create a new material. - **Take By Name From Assets Without Creation** � use existing materials with the same name if available; if there is no material with such name, the **mesh_base** material is assigned. This option allows minimizing creation of unwanted materials when importing a lot of models. - **Overwrite Assets** � overwrite existing materials (if any). |
| Base Materials Mode | Enables to choose the base material for imported materials. Available options: - **Inherited Material Graphs** � autoselected graph-based material is used as the base material. This mode finds the most suitable autogenerated graph-based material with the appropriate functionality and inherits the imported materials from it. If such graph-based material isn't found in the project, then it will be autogenerated and used as the base one. > **Notice:** This mode allows to reuse the existing graph-based base materials and avoid the creation of a lot of unique base materials when importing FBX files. - **Unique Material Graphs** � autogenerated graph-based material is used as the base material. In this mode all imported material will be inherited from unique autogenerated graph-based materials. - **Inherited Mesh Base** � [mesh_base](../../content/materials/library/mesh_base/index.md) is used as the base material. This mode uses the default [mesh_base](../../content/materials/library/mesh_base/index.md) material as the base one for the imported materials. |
| Workflow | Provides an interface to choose a [workflow](../../content/materials/library/mesh_base/index.md#workflow) for the imported physically based materials (if any). Available options: - **Metalness** � uses the new standard of textures (albedo, metalness, roughness). - **Specular** � uses the old standard of textures that was used in **[mesh_base](../../content/materials/library/mesh_base/index.md)** material (diffuse, specular, gloss). |
| Add Asset Name as Prefix | Enables to add a prefix for imported materials to avoid collision of names. |
| Add Prefix | Enabling this option makes the name of each material have the name of the imported FBX asset as a prefix. |
| Merge Similar Materials | Enables to merge materials with the same settings, but different names. |


### Skeleton Import Options


| Import Skeletons | Enables importing skeletons from the file. |
|---|---|
| Import Skeleton Mode | Specifies the import mode for skeletons. Available options: - **Create** - Creates a new skeleton asset based on the hierarchy contained in the imported file. - **Take Shared** - Reuses an existing skeleton asset. |
| Shared Skeleton | Specifies the skeleton asset that should be used for the imported mesh or animations. |


### Animation Import Options


| Import Animations | Enables importing animations from the file. |
|---|---|
| Import Bones Without Skin | Enables import of bones that are not attached to the skeleton and do not affect the animation's skin, for example, a weapon held in the character's hands. If disabled, such bone is not imported and bones connected to it, if any, become orphans. |
| Create Transform Bones for Joints | Imports the hierarchy of the joints (bones) for animated FBX assets as a list of *[World Transform Bones](../../objects/worlds/world_transforms/transform_bone/index.md)*. If this option is disabled, [imported animations](#animation) for a mesh will still work. |
| Joints Reorientation | Enables changing orientation of bones for animations and animated geometry. When enabled, all bones will have the same forward axis as the geometry. This simplifies work with animations via code for programmers reducing excessive axis manipulations: if a mesh has **+Y** as a forward axis, the bones will have **+Y** as well. |
| Animation FPS | Number of frames per second of imported animation. |
| Force Loop | Forced smoothing of looped animation playback. ![](animation_forceloop.gif) |
| Looped Frames | Number of frames to be used for smoothing of looped animation playback. The specified number of frames is taken from the beginning and from the end of the animation. If the specified value exceeds the (total_number_of_frames)/2, the latter is used instead. |


### Texture Import Options


| Import Textures | Enables importing textures from the file. |
|---|---|
| Invert G-Channel For Normal Maps | Inverts the G-channel in normal maps. |


### Other Import Options


| Import Lights | Imports light sources from an FBX scene. |
|---|---|
| Import Cameras | Imports cameras from an FBX scene. |
| Skip Empty Nodes | Enables skipping empty nodes. Complex CAD models may contain a lot of empty nodes, resulting in an overloaded world hierarchy. You can enable this option to simplify generated hierarchy by ignoring nodes, that do not contain any useful information. |
| Front Axis | Provides an interface to choose an axis to be considered as the forward vector of the World Coordinate System. |
| Up Axis | Provides an interface to choose an axis to be considered as the up vector of the World Coordinate System. |
| Scale | Geometry scale multiplier. When added to the scene in UNIGINE, your mesh might require scaling to fit properly. However, applying the *Scale* transformation to the mesh affects its physics � the mesh cannot participate in collision properly in this case. Therefore, it is recommended to define the required scale value using the [scale manipulator](../../editor2/select_position_nodes/index.md#scale_object) and then re-import the mesh using the resulting value, which is displayed in the [Common Parameters](../../editor2/node_parameters/transformation_common/index.md#transformation_params). |


### Create Root Motion Joint (FBX Only)


| Create Root Motion Joint | Creates an addition joint in the skeleton, which is used to extract root motion in the animation. |
|---|---|
| Target Root Motion Joint | The name of the joint from which root motion will be extracted. |
| Root Motion Position Component | Defines which translation components of the target joint will be used as root motion. |
| Root Motion Rotation Component | Defines which rotational components of the target joint are used for root motion. |
| Root Motion Forward Axis | Specifies which local axis of the *[Target Root Motion Joint](#fbx_import_target_root_motion_joint)* is treated as the forward direction. This setting is used only when *[Root Motion Rotation Component](#fbx_import_root_motion_rotation)* is set to **Only Vertical**. The selected axis defines the forward vector in the joint's local coordinate system. During import, this vector is projected onto the horizontal plane and used to compute the character's vertical rotation (yaw) from the animation. > **Notice:** This parameter refers to the local basis of the joint, not to the visual facing direction of the character model. |


Specific options for various types of data stored in an FBX container are described below.


### Geometry


The most commonly used type of data stored in an FBX container is polygonal geometry.


When importing geometry keep in mind the following **mesh limitations** set in UNIGINE:


| Maximum number of **vertices** per mesh | 4,294,967,295 |
|---|---|
| Maximum number of **surfaces** per mesh | 32,768 |
| Maximum amount of **weights** per vertex | 4 |


To import 3D geometry data contained in an FBX scene, you should enable the **[Import Meshes](#fbx_import_meshes)** option.


| ![](child_nodes.png) | Imported geometry (same as any object in the scene) after being added to the world, becomes a [node](../../start/index.md#node) and can be seen in the *[World Hierarchy](../../editor2/interface/index.md#world_hierarchy)* window. This node will have the same name as the imported FBX asset and a hierarchy of child nodes representing the hierarchy of static meshes contained in the imported scene. |
|---|---|


You can combine all child objects into a single one by enabling the **[Merge Static Meshes](#fbx_merge_static_meshes)** option. In this case, all surfaces of child meshes will be copied to the single parent mesh and will appear in its *Surfaces* hierarchy.


![](merge_static_meshes.png)

*Surfaces of a single mesh generated instead of separate meshes withdevice_calculatorandglass_matmaterials assigned*


You can also merge the surfaces having the same material assigned by enabling the **[Merge Surfaces by Materials](#fbx_merge_surfaces_materials)** option.


![](surfaces_merge_by_material.png)

*Surfaces merged by materials*


Different measurement systems can be used in different 3D modelling applications. To adjust the scale of imported geometry, you can use the **[Scale](#fbx_scale)** parameter.


It is also possible to optimize the vertex cache when importing geometry. To do so, use the **[Optimize Vertex Cache](#fbx_optimize_vertex_cache)** option.


The **[Import Tangent Space](#fbx_import_tangent)** option allows importing built-in tangent space data instead of recalculating it.


### Materials


An FBX container can also store materials assigned to the surfaces of the objects in a 3D editor.


To import materials from an FBX container, you should enable the **[Import Materials](#fbx_import_materials)** option. In this case, the surfaces of the imported model will have the corresponding materials assigned.


> **Notice:** If materials are imported, the material [assets](../../editor2/assets_workflow/index.md#asset_system) are created in the `materials` subfolder of the folder where the `.fbx` asset is stored.


The following textures will be imported and assigned (if any):


- Diffuse (albedo) texture
- Normal map or bump map (needs to be converted into 2-channel (*RG*) for Unigine)
- Specular texture
- Light map


The following material parameters will also be imported (if defined):


- Diffuse color
- Specular color and power
- Emission color


> **Notice:** You should [adjust other material settings](../../editor2/materials_settings/index.md) manually.


When the **[Import Materials](#fbx_import_materials)** option is disabled, all surfaces of the model will have the default *[mesh_base](../../content/materials/library/mesh_base/index.md)* material assigned.


When importing materials, you might have a situation when a material with a given name already exists in the project. You can choose whether to overwrite existing materials (the corresponding assets will be overwritten) or not. For this purpose, the **[Overwrite Existing Materials](#fbx_assets_mode)** option is used. When unchecked, existing materials will be used.


In case when a source model contains lots of objects with many identical materials that just have different names (often happens when an FBX file was exported from a CAD system), it makes sense to combine such materials into a single one. To do so, you should enable the **[Merge Similar Materials](#fbx_merge_similar_materials)** option.


Also you can [choose](#fbx_base_material_mode) the base material for the imported materials: it can be an autoselected/autogenerated [graph-based](../../content/materials/graph/index.md) material or the built-in [mesh_base](../../content/materials/library/mesh_base/index.md) material.


If the **[Base Materials Mode](#fbx_base_material_mode)** is set to **Inherited Mesh Base**, you should use the **[Workflow](#fbx_workflow)** option to set the desired one. UNIGINE supports two workflows for PBR materials: *Metalness* and *Specular*.


### Textures


When reading the materials data, you are also able to import textures stored in an FBX container. To do so, enable the **[Import Textures](#fbx_import_textures)** option.


> **Notice:** If textures are imported, the corresponding texture [assets](../../editor2/assets_workflow/index.md#asset_system) are created in the same folder, where the `.fbx` asset is stored.


### Animation and Morph Targets


You can import skeletal animations and morph targets from an FBX file.


To import animations from an FBX container:


- If the FBX file contains a skeleton, enable **[Import Skeletons](#options_skeletons_import)** and choose an import mode. Use *Create* to generate a new skeleton asset, or *Take Shared* to reuse an existing skeleton from the project.
- Enable the **[Import Animations](#fbx_import_animations)** option.
- Specify the number of frames per second for imported animation in the **[Animation FPS](#fbx_animation_fps)** field.


To import morph targets just enable the **[Import Morph Targets](#fbx_import_morphs)** option. Morph targets will be imported as child nodes.


If you have an FBX file containing skeletal animation without any geometry, you can import it to your UNIGINE project via the **[Import Bones Without Skin](#fbx_import_bones_wo_skin)** and use generated `.anim` files.


### Lights


You can import light sources from an FBX scene (if any) by simply enabling the **[Import Lights](#fbx_import_lights)** option. Imported light sources will be added as child nodes to the root node. The following conversion will be performed:


- Directional lights are converted into *[world](../../objects/lights/world/index.md)* light sources.
- Point lights are converted into *[omni](../../objects/lights/omni/index.md)* light sources.
- Spot lights are converted into *[projected](../../objects/lights/proj/index.md)* light sources.


The following parameters of lights are automatically imported into UNIGINE, so there is no need to set them up twice:


- Light color
- Light radius and attenuation
- Light source position and orientation


### Cameras


Cameras can also be imported from an FBX scene (if they exist) by simply enabling the **[Import Cameras](#fbx_import_cameras)** option. They are converted into *[PlayerDummy](../../objects/players/dummy/index.md)* (cameras without physical properties). Both types of projection are supported in UNIGINE:


- Orthographic (with Z near and far clipping planes support)
- Perspective (with FOV support)


To view the scene through the imported camera choose its name in the drop-down list in the top left corner of the *[Editor Viewport](../../editor2/interface/index.md#viewports)* window.


## Adding Imported FBX Asset to the World


To add a new imported FBX asset to the scene, as any other asset, simply drag it from the *[Asset Browser](../../editor2/assets_workflow/index.md#asset_browser)* to the *[Viewport](../../editor2/interface/index.md#viewports)* window. The corresponding node will be created and displayed in the *[World Hierarchy](../../editor2/interface/index.md#world_hierarchy)* window. This node will have the same name as the imported FBX asset and a hierarchy of child nodes representing separate objects contained in the 3D model.


![](asset_drag.png)


Non-native geometry asset types (`fbx, obj, dae`, etc.) are containers for meshes. If you double-click such asset in the *Asset Browser* (or use the right-click *[Open](../../editor2/interface/context/index.md#open)* command), the [generated runtime](../../editor2/assets_workflow/assets_runtimes.md) `.mesh, .anim` and `.node` files stored in the container asset will be displayed:


![](fbx_container.gif)

*Opening FBX Container*


## Video Tutorial: Importing 3D Models
