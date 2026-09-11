# Using Visual Helpers


The *Helpers* panel provides quick access to frequently used helpers and auxiliary visualizers. These helpers can be used to facilitate the process of world building. All auxiliary information you need at the moment, from icons and gizmos to information about nodes, geometry, shapes and physical joints can be easily controlled via this panel.


![](helpers_panel.png)


All these helpers can also be enabled via the corresponding [console](../../code/console/index.md) commands.


## Visualizer Mode


**Visualizer Mode** incorporates all visual helpers described in this article, except the FPS counter. You can quickly show or hide all helpers, when necessary, as well as enable or disable depth testing for them by choosing the appropriate mode via *Helpers -> Visualizer Mode*, instead of turning them on and off one by one.


![](visualizer.jpg)


## Visualizer Antialiasing


**Visualizer Antialiasing** allows separately toggling antialiasing for wireframes and for the Visualizer and other FFP lines.


## FPS


The FPS counter at the top-left corner of the *Editor Viewport* displays the current frame rate (in frames per second) as well as minimum, maximum and average FPS values for the recent time period. To toggle the FPS counter, choose *Helpers -> FPS*.


![](fps.png)


## ViewCube


The **ViewCube** is displayed at the top-right corner of the *Editor Viewport*. It allows you to control orientation of the current camera. You can toggle the ViewCube by choosing *Helpers -> Show ViewCube*.


![](viewcube.png)


## Wireframe


Toggles displaying of all wireframes in the *Editor Viewport*.


![](all_wireframes.jpg)


## Selected Nodes Outline


Toggles displaying of the outline for the selected nodes.


![](node_outline.jpg)


## Selected Surfaces Wireframe


Toggles displaying of all polygon edges for the selected surface of an object.


![](wireframe.jpg)


## Immovable Objects


Toggles displaying of wireframes of objects with the *[Immovable](../../editor2/node_parameters/transformation_common/index.md#clutter)* option enabled.


Available settings:


- *Disabled* - visualization is disabled.
- *Show objects with the Immovable option enabled* - wireframes of **all** objects with this flag are displayed in red.
- *Show objects that belong to a separate immovable spatial tree* - wireframes of **all non-collider** objects with the Immovable option enabled are displayed in red.


## Scissors


Toggles displaying of scissor rectangles.


## Spatial Tree


The [spatial tree](../../principles/world_management/index.md#bsp) is a hierarchical structure obtained by division and organizing all the scene data. You can toggle the spatial tree by choosing *Helpers -> Spatial*.


## Shadow Cascades


The [world lights](../../objects/lights/world/index.md) use the concept of [cascaded shadow maps](../../principles/render/sequence/index.md#shadow_maps_world) for rendering shadows. The cascades are displayed as rectangular areas of different colors.


![](world_cascades_1.jpg)


## World Shadow Casters


Toggles displaying of the wireframe for all surfaces that are configured to cast shadows from the current [World Light](../../objects/lights/world/index.md) source (this means the *[Cast World Shadows](../../editor2/node_parameters/visual_representation/index.md#cast_world_shadows)* option is enabled and the masks are set correctly for the surfaces).


## Lighting Mode


Toggles displaying of the wireframe for all surfaces with the selected [Lighting Mode](../../editor2/node_parameters/visual_representation/index.md#lighting_mode).


## Decals


Toggles displaying of wireframes for all [decal](../../objects/decals/index.md) objects in the *Editor Viewport*.


## Alpha Test


Toggles displaying of wireframes for materials with the *Alpha Test* preset enabled.


![](alpha_test.jpg)


## Emission


Toggles highlighting of materials with the *Emission* state enabled or connecting any data to the *Emission* input in the material graph.


## Mesh Statics


Toggles displaying of wireframes for all *[Mesh Static](../../objects/objects/mesh/index.md)* objects.


## Mesh Dynamics


Toggles displaying of wireframes for all *[Mesh Dynamic](../../objects/objects/mesh_dynamic/index.md)* objects.


## Complex Shadow Shader


Toggles highlighting of all objects that cast shadows in the following way: the pixels are cut out during the shadow pass, like in Alpha Test or Alpha Blend materials, materials assigned to animated *Mesh Skinned*, opaque materials with the enabled *Depth Offset* or any other effects that affect shadows.


## Surface Custom Texture Not Available


Toggles highlighting of surfaces with the materials that use the [surface custom texture](../../content/materials/graph/node_library/textures/surface_custom_texture.md) in the material graph, however the option is not enabled for the surface.


## Surface Custom Texture Not Used


Toggles highlighting of surfaces with the [surface custom texture](../../content/materials/graph/node_library/textures/surface_custom_texture.md) enabled and/or set, but not used in the material graph.


## Surface Custom Texture


Toggles highlighting of surfaces with the [surface custom texture](../../content/materials/graph/node_library/textures/surface_custom_texture.md) enabled.


## Physics Intersection


Toggles highlighting of surfaces for which *[Physics Intersection](../../editor2/node_parameters/physics/index.md#surface_physics_intersection)* is enabled.


## Intersection


Toggles highlighting of surfaces for which *[Intersection](../../editor2/node_parameters/physics/index.md#surface_intersection)* is enabled.


## Collision


Toggles highlighting of surfaces for which *[Collision](../../editor2/node_parameters/physics/index.md#surface_collision)* is enabled.


## Material Graph Based


Toggles highlighting of surfaces and decals that use the materials created in the *[Material Editor](../../content/materials/graph/index.md)*.


## Not Material Graph Based


Toggles highlighting of surfaces that use the materials inherited from [mesh_base](../../content/materials/library/mesh_base/index.md).


## Clusters


Toggles displaying of wireframes for all *[Mesh Cluster](../../objects/objects/mesh_cluster/index.md)* objects.


## Transparent


Toggles displaying of wireframes for materials with the *Alpha Blend* preset enabled.


## Geodetic Pivot


Toggles displaying of [geodetic pivots](../../objects/geodetics/geodeticpivot/index.md).


## Occlusion Queries


Toggles displaying of [occlusion query](../../content/optimization/geometry/culling/index.md#occlusion_query) boxes.


## Occluders


Toggles displaying of the buffer used for [occluders](../../objects/worlds/world_occluders/index.md) in the *Editor Viewport*.


## Render Textures


Toggles displaying of textures filling [GBuffer](../../principles/render/sequence/index.md#gbuffer).


## Selected Object Bounds


Toggles displaying of axis-aligned bounding boxes for the selected objects.


![](bounds.jpg)


## Selected Object Inner Bounds


Toggles displaying of inner bounding boxes for the selected objects.


## Selected Node Info


Sometimes you might need additional information on the nodes you work with. To toggle displaying of additional information for the selected node, choose *Helpers -> Show Selected Node Info*. The following information will be displayed near the selected node, depending on its type:


- **Object Type : Name**
- **File** - Asset file GUID (Global identifier)
- **Surface** - Selected surface of the node
- **Property** - The property assigned to the node
- **Triangles** - Number of triangles
- **Center** - Coordinates of the node's center point
- **Radius** - The radius of the sphere described about the selected node. In fact, it is the maximum size along one of axes
- **Distance** - Distance from the current camera


![](info.jpg)


## Bones


To toggle visualization of bones, that are used to control the animation of [skinned meshes](../../objects/objects/mesh_skinned/index.md), choose *Helpers -> Show Bones*.


![](bones.png)


## Selected Surfaces TBN


Toggles displaying of tangent, bitangent, and normal vectors for the selected surface of an object.


![](tbn.jpg)


The vector length can be set via the available *Size* setting.


## Landscape Terrain VT Streaming


Toggles displaying of *Landscape Terrain* tiles that are currently being rendered in a lower resolution until the highest mip-level is loaded.


![](landscape_streaming.jpg)


## Nodes Interaction With


Toggles displaying of nodes for which interaction with *Triggers/Clutters/Grass* is enabled.


## Voxel Probe Visualizer


Visualizes the inner space of *Voxel Probe* using spheres. The spheres help to show the illumination in each voxel from all directions.


Available settings:


- *Grid Size* � number of spheres in every row/column, the value from 7 to 40.
- *Sphere Scale* � size of the visualizing sphere.


![Voxel Probe Visualizer](../../objects/lights/voxelprobe/voxel_probe_v.gif)


## Show Landscape Data


Toggles displaying of *Albedo* data or one of 20 masks belonging to all *Landscape Layer Maps* in the scene. Names are synchronized with the current active *Landscape Terrain* object.


This visualizer lets you isolate a preview for one of terrain components for easier editing of terrain using the [**Brush Editor**](../../editor2/brush_editor/index.md).


![](landscape_masks.jpg)


## Physics


This group of visualizers can be used to view the elements of the physical representation of objects (bodies, shapes, joints) as well physical interactions in your world.


### Shapes


To show or hide the [shapes](../../principles/physics/shapes/index.md) of the [physical bodies](../../principles/physics/bodies/index.md) assigned to objects, choose *Helpers -> Physics - > Shapes*.


You can also define how to visualize shapes � as wireframes or as solid objects, and specify the distance from the camera whithin which the shapes are highlighted.


![](physics_shapes.png)


### Joints


To show or hide the [joints](../../principles/physics/joints/index.md), that connect different [physical bodies](../../principles/physics/bodies/index.md), choose *Helpers -> Physics - > Joints*.


### Contacts


To toggle visualization of physical interactions between the [physical bodies](../../principles/physics/bodies/index.md), choose *Helpers -> Physics - > Contacts*. You can use this option to check contact points of colliding objects.


![](physics_contacts.png)


## Visualizer by Mask


Toggles visualization of nodes that use the selected [mask](../../principles/bit_masking/index.md) or masks.


## Visualizer Distance


Sets the distance from the camera within which the helpers are visualized.


## Show Visualizer On Invisible Surfaces


Toggles visualization of surfaces hidden in the viewport when the camera and surface use different [viewport masks](../../principles/bit_masking/index.md#viewport).


## Icons and Gizmos


You can also turn on and off icons and gizmos for all [built-in node types](../../objects/index.md) via the corresponding checkboxes next to each node type in the tree-view hierarchy:


![](helpers_icons_gizmos.png)


**Icons** represent a schematic image of the node type.


**Gizmos** show additional information such as area of applied forces, radius of the light, etc.


![](gizmo.jpg)

*Particles object with enabled gizmo (in red) to display force*


| Icon Size | Size of the icons to be displayed. The **3D** toggle enables the dependence of the icon sizes on the distance from the camera. |
|---|---|
| Icon Visibility Distance | Distance from the node and the camera, up to which the node icon is still visible. |
| Use Icons For Frame Selection | If enabled, nodes can be selected using the rectangular selection in the viewport. Nodes are selected in the *World Nodes* hierarchy list, if their icons are enabled and within this rectangular selection. |


You can select which icons and gizmos should be displayed. Every node category has subcategories to fine-tune display of icons. To display incomplete selection inside a category, the box is partially filled.


![](icon_selection.gif)
