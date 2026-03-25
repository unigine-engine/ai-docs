# Creating Nodes


A world in UNIGINE is a scene that includes a set of different [built-in objects](../../objects/index.md) with certain parameters. All objects added to the world are called [nodes](../../start/index.md#node). Nodes can be of different types, determining their visual representation and behavior. Some node types appear visually and have surfaces to represent their geometry (mesh), such as [Objects](../../objects/objects/index.md), [Decals](../../objects/decals/index.md), and [Effects](../../objects/effects/index.md). Other nodes ([Light Sources](../../objects/lights/index.md), [Players](../../objects/players/index.md), etc.) are invisible.


There are a number of ways you can add nodes to your world. You can create them using the UnigineEditor's functions as described in this article. You can also [create nodes at runtime via code](../../start/quick_start/pqr/index_cpp.md#creating_nodes).


## Creating Nodes of Built-In Types


UNIGINE provides a set of diverse built-in node types that can be used to represent virtually any object or phenomenon present in real life. These node types are formed into several groups.


You can create a node of any built-in type by selecting the corresponding item in the *Create* menu and specifying necessary parameters.


> **Notice:** The [context *Create* menu](../../editor2/interface/context/index.md#viewport) is also available via **Shift+Right click** in the Viewport.


![](menu_create.png)


> **Notice:** Before creating nodes you have to [create a world or open an existing one](../../editor2/worlds/index.md), otherwise the *Create* menu will be disabled.

The process of creation and the list of parameters available for each of the built-in node types is described in the corresponding article of the [Built-In Node Types](../../objects/index.md) section.
### Standard Primitives


UNIGINE lets you add any 3D model created in a third party digital content creation tool via the [FBX import option](../../editor2/fbx/index.md). Apart from that it offers you a set of standard primitives that might be useful as test objects or in block design. This set includes the following types: *[*Box*](#box), [*Sphere*](#sphere), [*Plane*](#plane), [*Cylinder*](#cylinder)*, and *[*Capsule*](#capsule)*.


These primitives can be used either as placeholders and prototypes, or to create world objects with a simple shape (e.g., a plane is commonly used as a flat ground surface).


You can create any primitive by choosing the corresponding item in the *Create -> Primitives* menu.


> **Notice:** To create primitives via code please use the *[Primitives](../../api/library/rendering/class.primitives_cpp.md)* class.


When creating a standard primitive, specify its geometry parameters in the window that opens, as for the **Box**:


![](create_box.png)

*Creation parameters for the box primitive*


Having specified the primitive's parameters and clicking *OK* you confirm its creation. You can also click *Cancel* to abort.


On confirmation, the Editor switches to the **[*Snap to Surface Mode*](../../editor2/select_position_nodes/index.md#snap_surface)**, so you can specify the position of the new node.


![](drag_create.gif)

*Snap to Surface Mode*


Creation of a primitive produces a corresponding `.mesh` asset generated based on the specified parameters in the current directory of the *Asset Browser* window. The primitive shall be created as a *[Static Mesh](../../objects/objects/mesh/index.md)*.


#### Box


![](box.png)


The **Box** primitive provides a simple geometry for representing boxes and cubes. It has the following parameters:


| X, Y, Z | dimensions along the X, Y, and Z axes. |
|---|---|


#### Sphere


![](sphere.png)


The **Sphere** primitive provides a simple geometry for representing balls and spheres. The sphere has the following parameters:


| Diameter | diameter of the sphere. |
|---|---|
| Segments | number of the latitudinal and longitudinal edges of the sphere running from top to bottom from right to left. Increasing this value enhances the smoothness of the sphere by adding extra facets. |


#### Plane


![](plane.png)


The **Plane** primitive provides a flat polygon mesh for representing ground and surfaces. The plane has the following parameters:


| X, Y | dimensions along the X and Y axes. |
|---|---|
| Segments | number of the lengthwise and transversal edges cutting the surface of the plane into facets. |


#### Cylinder


![](cylinder.png)


The **Cylinder** primitive can be used to represent cylinders and tubes. The cylinder has the following parameters:


| Diameter | diameter of the cylinder. |
|---|---|
| Height | dimension along the Z axis. |
| Stacks | number of latitudinal edges cutting the cylinder from top to bottom. |
| Slices | this value determines how many edges are used to define the cylinder's circumference. The larger the number of sides, the smoother the cylinder appears. |


#### Capsule


![](capsule.png)


The **Capsule** primitive provides a geometry for representing capsules or rounded edge tubes. The capsule has the following parameters:


| Diameter | diameter of the capsule. |
|---|---|
| Height | dimension along the Z axis. |
| Stacks | number of latitudinal edges cutting the capsule from top to bottom. One of them is reserved by the capsule's body and the other are distributed between the caps. Determines the smoothness of the capsule's caps. |
| Slices | this value determines how many edges are used to define the circumference of the capsule's body. Also determines the smoothness of the capsule. |


## Creating Nodes via Asset Browser


A node can be created by simply dragging an asset from the [**Asset Browser**](../../editor2/assets_workflow/index.md#asset_browser) either to the [Editor Viewport](../../editor2/interface/index.md#viewports) or to the *[World Nodes](../../editor2/interface/index.md#world_hierarchy)* window. Asset type determines the type of the node (or hierarchy of nodes) that will be created.


![](drag_asset.png)


Drag-and-drop creation of nodes is supported for the following types of assets:


- `.node` - built-in asset type which contains any node (or a hierarchy of nodes) exported from the UNIGINE world previously. This type of asset produces a *[**Node Reference**](../../objects/nodes/reference/index.md)* by default. You can change the type of node, that will be created by right-clicking on the asset in the *Asset Browser* window and selecting a corresponding item in the context menu: | ![](node_options.png) | - **Place as Node Reference** will create a *[**Node Reference**](../../objects/nodes/reference/index.md)*. - **Place as Node Layer** will create a node of the *[**Node Layer**](../../objects/nodes/layer/index.md)* type. - **Place as Node Content** will import the contents of the `*.node` file, which can be a *[Static Mesh](../../objects/objects/mesh/index.md)* or any other [node type](../../objects/index.md), as well as a hierarchy of nodes. | |---|---|
- `.mesh` - built-in asset type that describes static and skinned geometry. This type of asset produces a *[Static Mesh](../../objects/objects/mesh/index.md)* or a *[Skinned Mesh](../../objects/objects/mesh_skinned/index.md)* if the asset stores animation data as well.
- `.fbx, .obj, .3ds, .dae` - assets that contain 3D models created using a third-party modelling software. This type of asset can produce a *[Static Mesh](../../objects/objects/mesh/index.md)*, a *[Skinned Mesh](../../objects/objects/mesh_skinned/index.md)* or a hierarchy of nodes depending on its contents (cameras, lights. etc.).
- `.lmap` - assets that contain [Landscape Layer Map](../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md) data.


If you drag an asset to the *World Nodes* window, the created node will be placed right in front of the current camera. While dragging the asset to the *Editor Viewport* switches the Editor to the [***Snap to Surface Mode***](../../editor2/select_position_nodes/index.md#snap_surface), so you can choose where to place the created node.


![](drag_to_scene.gif)

*Snap to Surface Mode*
