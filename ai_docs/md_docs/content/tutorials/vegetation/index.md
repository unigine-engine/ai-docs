# Vegetation: Authoring Tips


[![](title_small.jpg)](title.jpg)


This article describes principles of modeling and configuring plants and ways to achieve the best performance in scenes with dense vegetation in UNIGINE.


## Polygon Plants


Models of plants based on polygon meshes should be used for close-ups and middle distances for the most realistic representation of real-life greenery. It is crucial to use optimized 3D models of trees in real-time projects.


This section will introduce you to some vegetation authoring tips in UNIGINE and third-party Digital Content Creation software.


### Modeling


When preparing a 3D model of a tree with dense foliage, avoid creating topology for all branches and leaves; instead, it is much more efficient performance-wise to simulate fine details with textures. The main rule of models optimized for use in real-time is "the fewer polygons � the better". Following this rule is much more critical for rendering a dense forest filled with multiple types of plants and grasses.


Therefore, it is highly recommended to prepare several levels of detail (**[LODs](../../../principles/world_management/index.md#lods)**) for a plant to be used at different distances from the camera.


The overall workflow of modeling a tree is as follows:


1. Model several small branches with leaves and bake the models into texture atlases � the obtained textures are going to be your foliage textures. Here are examples of such textures: ![](leaves_texture_alb.png) *Albedo with Alpha channel* ![](leaves_texture_sh.png) *Shading* ![](leaves_texture_n.png) *Normal* ![](leaves_texture_t.png) *Translucent*
2. Create low-poly meshes that will represent foliage chunks, map UVs for proper texturing. The chunks do not have to be flat, you can experiment with the shape and bend of meshes. It is also important to prepare at least 3 LODs, so make sure to optimize the meshes of LODs to the full extent: ![Branches](model_leaves.png) *Foliage LODs*
3. Create the trunk with large branches and levels of detail for it. Prepare and assign necessary textures and materials. ![](model_trunks.png) *Trunk LODs* Also, it is recommended to transfer normals from the trunk to the adjoined vertices of branches to make a more natural look of joints: ![](model_branch_normals.png) *Adjusted normals of branches at joints provide a more natural look*
4. Scatter the LODs of foliage chunks over branches of the corresponding trunk LODs forming the tree crown: ![Tree LODs](model_composite.png) The fact that the same number of chunks is used on all LODs may result in a higher polygon count. However, this approach has a number of advantages:

  - High diversity of branches makes it possible to create more realistic plants.
  - A better, almost seamless transition between LODs. All elements can be adjusted at any time to get rid of any inconsistencies.
  - A more permissive art pipeline enables the artists to collect trees of different sizes and ages out of the same chunks.
  - Accurate work of post effects even on the lowest LODs (*SSAO, SSGI*, etc.).
5. It is also recommended to create a separate low detail foliage LOD to simplify shadow casting. You can duplicate the lowest LOD and optimize it even more for this purpose and [configure shadow casting](#shadow_lod) in UNIGINE.
6. For better blending with terrain, prepare a separate bottom part of the trunk with a new material assigned. You can merge it to the mesh of the highest LOD for convenience: ![Bottom part of the tree for blending with terrain](terrain_blend_mesh.png)
7. [Orient the model](../../../editor2/assets_workflow/export/export_from_blender.md#pre_export) so it will be imported in UNIGINE appropriately, reset all transformations. Pay attention to the correct position of the mesh's pivot point (apparently, all the LODs must have the same position). As a rule, the pivot is placed at the bottommost point of the plant for ease of world design. However, you can alter the position of the pivot if this is needed for [stem animation](#stem).
8. As a result, the model has the following content: ![](tree_structure.png) For convenience, it is recommended to add postfixes to the names of levels of detail that will be used later during import.
9. Consider further adjustment of [vertex normals](#normals) and vertex colors and UVs for [leaves animation](#leaves).
10. [Export the model](../../../editor2/assets_workflow/assets_create_import.md#export) to the recommended FBX format.


### Configuring the Look of the Plant


Import the created model to UNIGINE following the [FBX Import Guide](../../../editor2/fbx/index.md) and [add the plant to the scene](../../../editor2/create_import_nodes/index.md#assets).


To make all separate objects surfaces of the single *Mesh Static*, enable **[Merge Static Meshes](../../../editor2/fbx/index.md#fbx_merge_static_meshes)** in the import settings.


![](tree_surfaces.png)


#### Setting Up LODs


Set the visibility distances for [LODs](../../../content/optimization/geometry/lods/index.md#automatic) by enabling the **[Combine By Postfixes](../../../editor2/fbx/index.md#lods)** option and adjusting values in the import settings.


> **Warning:** The video tutorial is created using **SDK version 2.13**. The general workflow demonstrated in the tutorial is applicable for versions **up to 2.21**. However, specific details such as UI may differ across various versions.


##### Shadow LOD


When [dynamic shadow casting](../../../editor2/lighting/lights/shadows.md#dynamic) is used, all polygons are rendered one more time for each light source with shadows enabled. *[World](../../../objects/lights/world/index.md)* light sources can have up to 4 shadow cascades, so the number of polygons rendered into shadow maps can be tremendous, leading to a strong performance hit. You can estimate this number by using the [Rendering Profiler](../../../tools/profiling/profiler/index.md#rtriangles_shadows).


That is why it is a best practice to use a low-poly mesh for foliage shadows. Perform the following steps:


1. Disable shadow casting for all foliage LODs except the Shadow LOD. You can do it in one of the following ways:

  - By disabling the **[Cast Proj and Omni Shadows](../../../editor2/node_parameters/visual_representation/index.md#cast_shadows)** and **[Cast World Shadows](../../../editor2/node_parameters/visual_representation/index.md#cast_world_shadows)** flags.
  - By toggling off all bits of the [Shadow Mask](../../../editor2/node_parameters/visual_representation/index.md#shadow_mask).
2. Hide the shadow LOD for any camera by toggling off all bits of its [Viewport Mask](../../../editor2/node_parameters/visual_representation/index.md#viewport_mask).


See the demonstration of configuring a shadow LOD in the [Bit Masking](https://youtu.be/nI8Q3bANsM8?t=288) video tutorial.


#### Materials Adjustment


If the **[Import Materials](../../../editor2/fbx/index.md#fbx_import_materials)** flag was enabled in the import options, all necessary materials are already generated and assigned to the surfaces of the tree. Let's consider material parameters that worth being noted:


- Make the leaves material **[Alpha-Test](../../../editor2/materials_settings/index.md#blending)** to cut out texels according to the Alpha channel of the Albedo texture.
- If specular highlights are incorrect, it is recommended to set the **Specular** value to 0. ![Incorrect lighting on flat leaves](tree_normals_flat.png) *Incorrect lighting on theReflections Rendering Debugpreview (left) and the result image (right)*
- Consider enabling the **[Two Sided](../../../editor2/materials_settings/index.md#two_sided)** option for the material to make the foliage denser. Be careful, as it may significantly affect performance if there are too many polygons in the scene. It may be better to switch the **[Backside Normal](../../../content/materials/library/mesh_base/index.md#option_backside_normal)** mode to the **To Front Side** option since it usually provides more realistic results for foliage.
- If textures make it evident that foliage is made of flat chunks, a great solution to this is the **[Angle Fade](../../../content/materials/library/mesh_base/index.md#angle_fade)** feature that cuts out polygons faced to the camera at extreme angles. ![](../../materials/library/mesh_base/anglefade_off.jpg) ![](../../materials/library/mesh_base/anglefade_on.jpg) > **Notice:** This feature may work incorrectly for meshes that have modified normals.
- Adjusting translucency for the foliage material is necessary for a better look. Increase the **[Translucent](../../../content/materials/library/mesh_base/index.md#parameter_translucency)** value to permit light to pass through the object. ![](translucent_0.png) ![](translucent_1.png) You can also enable the use of the **[Translucent Map](../../../content/materials/library/mesh_base/index.md#option_translucent_map)** in the *States* tab to specify a single-channel texture that will define parts of the object that aren't translucent (such as branches). > **Notice:** There is no need to paint fibers and small features of leaves on the **Translucent** texture if the [Normal](../../../content/materials/library/mesh_base/index.md#texture_normal_met) map is used and defines such surface irregularities. | ![](leaves_texture_alb.png) *Albedo texture* | ![](leaves_texture_t.png) *Translucent texture* | |---|---|
- Enable the **[Terrain Lerp](../../../content/materials/library/mesh_base/index.md#terrain_lerp)** flag for the material of the bottom part of the tree to blend your tree with a [Terrain](../../../objects/objects/terrain/index.md) in your scene. ![](terrain_blend_off.png) ![](terrain_blend_on.png)


#### Vertex Normals Adjustment


The fact that foliage is composed of flat chunks results in inaccurate shading. To counteract this and hide the flatness of the mesh, adjust vertex normals and improve the way the foliage is shaded.


The following solutions are possible:


- Enable the **[Normals Rotated To Camera](../../../content/materials/library/mesh_base/index.md#option_normals_rotated_to_camera)** option so all surface normals will be oriented towards the camera, ignoring the geometry normals. This feature checks out as a quick solution, although it makes all polygons shaded the same way. ![](../../materials/library/mesh_base/normals_rotated_to_camera_off.jpg) ![](../../materials/library/mesh_base/normals_rotated_to_camera_on.jpg)
- Edit vertex normals manually in your modeling software. Transfer vertex normals from a boundary cage to make the foliage look like a smooth and dense tree crown. > **Notice:** It is recommended to use a dome-like boundary cage with the sides elongated to the ground to avoid shading errors on lower polygons. ![Transferring normals from a boundary cage](tree_normals_cage.png) *Transferring normals from a boundary cage* As a result, the flatness of foliage geometry is less evident (on the right): ![](tree_normals_2.png) ![](tree_normals_normal.png)


#### MIP Maps


The *MipMapping* technique, supported by UNIGINE renderer, implies sampling lower textures for smaller and distant polygons. At that, minor features of foliage start wiping away with the distance. In some cases, branches and leaves look thicker when far from the camera than on a close-up view.


![MIP maps](../../../editor2/assets_workflow/mipmap_type_combined.png)

*MIP maps*


This issue can be resolved via these approaches:


- Engage the **[Mip Bias](../../../content/materials/library/mesh_base/index.md#option_mip_bias)** feature to shift the distance at which the switch between MIP-levels is performed. This option significantly affects the performance.
- By default, MIP maps for a texture are generated automatically on import using the **[Box](../../../editor2/assets_workflow/texture_import.md#mipmap_type)** filtering that may provide too blurred results. Consider switching to the **[Point](../../../editor2/assets_workflow/texture_import.md#mipmap_type)** filtering type to get sharper MIP maps.
- You can also prepare custom MIP maps in third-party software. For example, here is a comparison between MIP maps generated using the *Box* filtering and the sharper *Kaiser* filtering: ![](mipmaps_kaiser_0.png) ![](mipmaps_kaiser_1.png) To import a texture with custom MIP-levels, use the **[Combine](../../../editor2/assets_workflow/texture_import.md#mipmap_type)** option for a texture with laid out MIP-levels or save them to a `.texture` format and import the texture with the **Unchanged** option enabled.


### Animation


Enable the **[Vegetation](../../../content/materials/library/mesh_base/index.md#option_vegetation)** state to activate a set of animation-related parameters.


![Vegetation options](../../materials/library/mesh_base/vegetation.png)


Vegetation animation consists of [Stem](#stem) and [Leaves](#leaves) animation. To enable both of them, set *Animation* to the **Default** or **Field** option.


At that, *Field Animation* makes the plant be affected by [Field Animation](../../../objects/effects/fields/field_animation/index.md) volumes enabling you to override animation parameters locally (e.g., simulation of rotor downwash effects in close proximity to a rotorcraft).


#### Stem Animation


Stem animation applies vertex movement based on spatial 3D noise to simulate bending of the plant's trunk or stem caused by wind. The mesh's pivot point is considered fixed, and the further the vertex is along the Z axis, the stronger movement is applied to it.


Thus, it is necessary to place the pivot point at the correct position (usually, it is the bottommost point of the stem) and orient the model, so the Z axis goes upwards.


![Stem animation preview](stem_animation.gif)

*Stem animation example*


A set of **[Parameters](../../../content/materials/library/mesh_base/index.md#animation_parameters)** controls the animation.


![Animation parameters](../../materials/library/mesh_base/animation_params.png)


Please note that all surfaces of the plant must have identical stem animation parameters in order to synchronize their movement.


![Different stem animation parameters result in not synchronized parts of the tree](animation_stem_sync.gif)

*Different stem animation parameters result in not synchronized parts of the tree*


#### Leaves Animation


The *Leaves* animation is another layer of vertex shader animation mainly applied to foliage, providing additional detail bending. Using this type of animation requires preliminary adjustment to geometry on the modeling stage.


[Several approaches](../../../content/materials/library/mesh_base/index.md#vegetation_leaves) of leaves animation are available out of the box. Choose the type of animation using the **Leaves** option.


##### Geometry Vertex Color Based


This recommended approach providing the best control over foliage implies that leaves are rendered as polygons, and vertex colors are used for animation.


![](../../materials/library/mesh_base/animation_vertex.gif)


Vegetation movements are defined by RGB channels of vertex colors as follows:


| ![](../../materials/library/mesh_base/R_channel_veg.png) | Red channel is used for animation of smaller or peripheral parts of vegetation (leaves). Bright parts are animated, and dark parts are stiff. |
|---|---|
| ![](../../materials/library/mesh_base/G_channel_veg.png) | Green channel is used to define the movement order for branches in order to desynchronize them. The movement sequence starts from the brightest element to the darkest. |
| ![](../../materials/library/mesh_base/B_channel_veg.png) | Blue channel is used to define which parts of branches can be bent. Brighter parts indicate bendable portions, and darker parts���stiff portions. |


The [animation parameters](../../../content/materials/library/mesh_base/index.md#animation_parameters) control vertices movement:


![](../../materials/library/mesh_base/animation_params_vertex.png)


It is also a regular practice to animate branches using this technique even if they are attached to the trunk:


![](leaves_branches.gif)

*The Green and Blue channels define the movement of vertices; the Red channel is not used for branches*


At that, related surfaces must have the same vertex colors on adjacent vertices and identical animation parameters in order to synchronize their movement:


![](leaves_branches_colors.png)

*The colors of adjacent vertices of the trunk and foliage are the same, so the geometry stays connected when animated*


![](vertex_color_animation.gif)

*Geometry Vertex Color Based leaves animation*


##### Geometry UV-based


This is a rather legacy approach when leaves are rendered as standard polygons. It requires the UV Channel 2 to be defined for the mesh.


| ![](../../materials/library/mesh_base/animation_uv.gif) *Geometry UV-based animation* | ![](animation_geometry_uv_map.png) *UV Channel 2: the stiffest vertices are in the top left corner* |
|---|---|


Animation uses UV channel 2 of an object as follows: in the UV grid, [0,1] is the pivot point for the object's movements and the stiffest part of the object, and towards [1,0], the object becomes more flexible.


| ![](../../materials/library/mesh_base/leaf_mesh_uv.png) | ![](../../materials/library/mesh_base/geometry_uv.gif) |
|---|---|


Control the vertices movement via the same [Animation Parameters](../../../content/materials/library/mesh_base/index.md#animation_parameters).


##### Billboard


*Billboard* is the most performance-friendly way of animating distant vegetation: all quads are rendered as *billboards* that always face the camera; the UV Channel 2 defines the size and movement of polygons. Hence, the foliage mesh should contain only quad polygons for leaves.


| ![](../../materials/library/mesh_base/animation_billboards.gif) *A billboards-based bush* | ![](leaves_billboard_mesh.png) *The mesh of the bush* |
|---|---|


Animation uses UV channel 2 of an object as follows: in the UV grid, [0,1] is the pivot point for the billboard's movements, and the billboard's size can be changed by scaling the polygon in the UV channel.


| ![](leaves_billboard_uv0.png) *UV Channel 1* | ![](../../materials/library/mesh_base/billboard_uv.png) *UV Channel 2* | ![](../../materials/library/mesh_base/billboard_uv.gif) *Mesh (above) and the result (below)* |
|---|---|---|


Control the polygons movement via the same [Animation Parameters](../../../content/materials/library/mesh_base/index.md#animation_parameters).


#### Global Animation Options


Stem and leaves animation are also controlled by the global **[Vegetation Animation Parameters](../../../editor2/settings/render_settings/vegetation/index.md)**. Via these settings, you can adjust stem and leaves animation intensity, speed, and wind effect globally and control the weather conditions per world.


![](animation_weather.gif)


Note that the global parameters are just multipliers for the per-material animation parameters.


### Scattering Plants


To randomly scatter a significant number of identical meshes across the terrain, *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md)* is used. *Mesh Clutter* scatters objects procedurally and renders only those objects which are in the viewing frustum. The typical workflow is as follows:


1. Click *Create -> Clutter -> Mesh* and specify the `.mesh` asset to be used as the source mesh for the *Mesh Clutter*. Click within the viewport to place the new node in the world. > **Notice:** `.fbx` assets are containers for `.mesh` assets, right-click on the asset and choose *Open* or double-click on it to access its content. | ![](../../../objects/objects/mesh_clutter/clutter_create.png) | ![](clutter_create_select.png) | |---|---|
2. If you already have a configured tree in your world, you can copy all materials and parameters from surfaces of the configured tree and paste them [sequentially or by surface names](../../../editor2/node_parameters/visual_representation/index.md#copy_paste) to *Mesh Clutter*. ![](clutter_copy_surfaces.gif)
3. Place the node in the scene and set the **[Size](../../../objects/objects/mesh_clutter/index.md#size)** to cover the whole playable area. > **Notice:** The operation of *Mesh Clutter* objects is float-based, so it is not recommended to use Sizes bigger than 10000 units lengthwise and widthwise. If you need to fill areas beyond this limit, you will need to manually split the single *Mesh Clutter* object into a grid of several clutters. > > > [Sandworm Tool](../../../editor2/sandworm/index.md) does the slicing automatically when generating terrain.
4. Adjust the scattering parameters: set the desired **[Density](../../../objects/objects/mesh_clutter/index.md#density)** in meshes per square unit; diversify the appearance of the forest by randomizing the *[Scale, Offset, and Rotation](../../../objects/objects/mesh_clutter/index.md#randomizing)* parameters.
5. Make the clutter object child to the terrain and enable the [**Intersection**](../../../objects/objects/mesh_clutter/index.md#relief) flag to make trees follow the surface. ![](clutter_intersection_off.png) ![](clutter_intersection_on.png) > **Notice:** If the *Intersection* flag is enabled, toggle it off and on to forcefully re-generate the *Clutter* object.
6. Adjust the **[Visibility](../../../objects/objects/mesh_clutter/index.md#visible_distance)** and **[Fade](../../../objects/objects/mesh_clutter/index.md#fade_distance)** distances. Given the number of polygons a dense forest may consist of, it is recommended to make *Mesh Clutter* visible as close as possible and use *[Impostor](#impostors)* objects at a farther distance.
7. By default, trees are scattered across the whole area. You can [mask areas with vegetation](../../../objects/objects/mesh_clutter/index.md#masking) via the following approaches:

  - By using a single-channel texture. You can prepare a texture in third-party software or create a new one and [draw the mask](../../../editor2/mask_editor/index.md) from scratch. All *Mesh Clutter* and *[Grass](#impostors)* objects that use that texture are updated on the fly. ![](clutter_mask_texture_ui.png) ![](clutter_mask_texture_edit.gif)
  - By using [Landscape Terrain masks](../../../objects/objects/terrain/landscape_terrain/index.md#layers_masks). You can use the data of Landscape Terrain masks to define the density of the vegetation, provided your world contains *Landscape Terrain* with configured masks: select the desired mask in the **[Mask Terrain](../../../objects/objects/mesh_clutter/index.md#terrain_mask)** parameter: ![](clutter_mask_terrain_ui.png) ![](clutter_mask_landscape_0.png) *Landscape Terrain* ![](clutter_mask_landscape_1.png) *Mask previewof Landscape Terrain* ![](clutter_mask_landscape_2.png) *Vegetation is scattered according to the terrain mask* You can also edit the mask by using the [Brush Editor](../../../editor2/brush_editor/index.md) and have the *Mesh Clutter* updated on the fly. > **Notice:** All Landscape Terrain data, including masks, is subject to [data streaming](../../../objects/objects/terrain/landscape_terrain/index.md#tiling). If you have unoptimized streaming settings, there might be a bottleneck in mask data loading on world startup and changing the camera position, affecting the performance of *Mesh Clutter* generation.
  - As an additional feature, [masking by a mesh](../../../objects/objects/mesh_clutter/index.md#mesh_mask) is also available: ![](../../../objects/objects/mesh_clutter/mesh_mask.jpg) ![](../../../objects/objects/mesh_clutter/mesh_masked.jpg)
  - [Cutout by intersection](https://youtu.be/nI8Q3bANsM8?t=406) with objects: ![](mask_cutout_off.png) ![](mask_cutout_on.png) *Cutting out trees within a box*

    1. Create *[Mesh Static](../../../objects/objects/mesh/index.md)* or *[Decal](../../../objects/decals/index.md)* representing a bounding cutout volume. Enable the **[Clutter Interaction](../../../editor2/node_parameters/transformation_common/index.md#clutter_interaction)** flag for it.
    2. Choose and enable a bit of the *[Intersection](../../../principles/bit_masking/index.md#intersection_mask)* mask of the object that will be used for the cutout feature.
    3. Enable the same bit of the *[Cutout Intersection](../../../objects/objects/mesh_clutter/index.md#cutout_intersection)* mask of the *Clutter* object.
    4. Hide the visual representation of the object from the camera by disabling all bits of its *[Viewport](../../../principles/bit_masking/index.md#viewport)* mask and disabling [shadow casting](../../../editor2/node_parameters/visual_representation/index.md#cast_world_shadows) for it.
8. Keep the optimal **[Step](../../../objects/objects/mesh_clutter/index.md#step)** value for the best performance. The *Clutter* is rendered as a 2D grid, in each cell of which meshes are randomly scattered depending on the density and probability of appearing. Generation of meshes in the cells is time-sliced starting from the nearest cells to reduce the load on the CPU. ![](clutter_step_1.png) *Cell division* The *Step* value defines the cell size in units. Thus, this value specifies the resulting number of cells along each axis (the size divided by the step). It is highly recommended to choose the values that are **divided with no remainder**. > **Notice:** Each cell requires 1 DIP call, so the higher the number of cells (i.e., the smaller the step), the more reduced the performance is. However, creating a large cell takes a longer time. When the camera moves fast enough, small cells are created one by one very fast and smoothly, but large ones can noticeably pop into sight and cause a slight rendering lag.


You can scatter bushes and chunks of polygon grass across the terrain the same way.


![](grass_mesh.png)

*A chunk of optimized polygon-based grass*


Finally, by combining several clutters for different types of trees, bushes, and grass, you get a diverse look of vegetation.


![](clutter_vegetation.gif)

*Combination of severalMesh Clutterobjects for diverse vegetation*


### Manual Placement


As a finishing touch, you can place trees as *Static Mesh* where needed. It is efficient performance-wise to collect a significant number of identical meshes into a *[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)* object in order to treat and render a bunch of meshes as one object.


> **Notice:** In terms of performance optimization, *Mesh Cluster* objects have an advantage over *Mesh Clutter* objects as meshes baked into clusters support culling by [Occluders](../../../objects/worlds/world_occluders/index.md), making it possible to improve performance when some geometry occludes them (e.g., a building).


You can bake identical meshes of their hierarchy or collect all similar meshes in the world. Refer to the dedicated article for more details on the ways of [collecting a cluster](../../../objects/objects/mesh_cluster/index.md#collecting).


The other convenient approach to quickly scatter clusters of grass, bushes and trees across the scene is using the mesh placement brush tool:


1. Switch to the [*Cluster Editor*](../../../editor2/interface/index.md#tools_panel) mode: ![](../../../editor2/cluster_editor/cluster_editor_mode.png)
2. Select one or several *Mesh Cluster* objects in the scene or create a new one by using the *Create* button in the *Active Tool* window.
3. Paint areas with brush, scattering meshes across the scene: ![](../../../editor2/cluster_editor/cluster_editor.gif)
4. If needed, [edit the cluster](../../../objects/objects/mesh_cluster/index.md#expanding) manually to reposition or remove some meshes.


## Billboards


*[Billboard](../../../objects/objects/billboards/index.md)* is a flat rectangular object that always faces the camera. Using *billboards* instead of fully functional objects that are barely seen from far off significantly simplifies and speeds up rendering.


### Impostors


In terms of UNIGINE, *Impostor* is a *billboard*-like object capable of mimicking the appearance of polygon meshes by displaying different areas of textures depending on the angle of view. *Impostor* objects serve to speed up geometry rendering by reducing the number of polygons while saving visual fidelity.


![](grass_impostor_alb.png)

*Albedo texture for a tree impostor*


The built-in *[Impostor Creator](../../../content/optimization/geometry/impostors/index.md)* tool makes it easy to generate *Impostors* for single meshes and *Mesh Clutters*.


For a forest based on *[Mesh Clutter](#clutter)*, the *[Grass](../../../objects/objects/grass/index.md)* object with the *[grass_impostor_base](../../../content/materials/library/grass_impostor_base/index.md)* material will be used as a low-poly LOD. At that, the [*Clutter* and grass parameters](../../../objects/objects/grass/index.md#low_poly_grass) must match to make sure the position and orientation of all LODs are the same.


| ![](../../optimization/geometry/impostors/clutter_impostors_0.png) *Mesh Clutter and Impostors* | ![](../../optimization/geometry/impostors/clutter_impostors.png) *Meshes' and Impostors' Wireframes* |
|---|---|


Grass objects are also rendered as a 2D grid to optimize performance. The *[Step](../../../objects/objects/grass/index.md#step)* parameter defines the cell size. Usually, impostors are visible much further than meshes, and the *Step* value is to be chosen respectively. You can use the *[Subdivision](../../../objects/objects/grass/index.md#subdivision)* parameter that subdivides large grass cells so that they match smaller cells of a *Mesh Clutter* to make positions of randomly scattered objects coincide with positions of grass-based impostors. Therefore, the Clutter *Step* must match the ratio of *Step/Subdivision* values of the grass.


### Grass


![](../../../objects/objects/grass/grass_field_sm.jpg)


The [Grass](../../../objects/objects/grass/index.md) object with the *[grass_base](../../../content/materials/library/grass_base/index.md)* material can fill empty spots on the terrain and increase the overall density of lower vegetation in the scene. The *grass_base* material is intended to represent the basic features of grass. It has a lower visual fidelity compared to the *mesh_base* material, so *Grass* should be thought of as an additional filling layer of grass.


First, you need to prepare a **[Diffuse](../../../content/materials/library/grass_base/index.md#texture_diffuse)** texture with chunks representing small grass tufts:


![](grass_diffuse.png)

*Diffuse Texture for Grass of Various Types*


Chunks are to be placed in the texture as follows:


- Columns represent different grass species, each of which will be distributed according to the corresponding channel of the *[Mask](../../../objects/objects/grass/index.md#mask)* texture. Therefore, the number of columns must match the number of channels of the *Mask* texture; otherwise, grass tufts will be sliced incorrectly.
- Rows represent variations of grass of the particular species (thinner, thicker, tangled, etc.). There can be from 1 to 4 rows, and this number must coincide with the **[Num Textures](../../../objects/objects/grass/settings.md#num_textures)** value.


For the grass texture with 4 columns, a mask with 4 channels should be used:


![](../../../objects/objects/grass/tutorial/variation_grass_mask.png)

*RGBAImage Mask for Grass of4Various Types*


Refer to the *[Texture Slots](../../../objects/objects/grass/index.md#slots)* section for more details.


Visually attractive grass, however, may reduce performance if rendered as a whole. All computations are time-sliced and performed per cell of a 2D grid to allow rendering at interactive frame rates. So choosing the optimal *[Step](../../../objects/objects/grass/index.md#step)* for cells is crucial for better performance.


For more details on creating and configuring grass, refer to the in-depth tutorial: [Adding Grass](../../../objects/objects/grass/tutorial/index.md).


### Grass: General Recommendations


When adding grass in the scene, try to follow these general recommendations to avoid the performance drop:


- Use LODs and simplify the farthest LOD to the maximum extent. The fade distances between LODs shouldn't be very big, because these transitions imply that two objects are displayed simultaneously instead of one, which definitely affects performance.
- Disable shadows cast by the grass object surface and use screen-space shadows.
- The grass mesh normals should be directed upwards to ensure correct shading.
- Make the albedo/roughness of the ground, which is visible in the background, similar to the grass albedo/roughness so that the transition between these two objects in the distance is smooth and natural.


## See Also


- Generating vegetation based on landcover data using *[Sandworm](../../../editor2/sandworm/workflow/vegetation/index.md)*
- [Grass Optimization](../../../objects/objects/grass/index.md#optimization)
- *[Vegetation](../../../content/samples/main_samples/vegetation.md)* content sample
- *[Vegetation](../../../sdk/addons/vegetation/index.md)* add-on
- *[Fox Hole](../../../sdk/demos/fox_hole.md)* demo
