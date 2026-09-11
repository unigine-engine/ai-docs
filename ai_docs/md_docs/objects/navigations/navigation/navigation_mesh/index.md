# Navigation Mesh


The **Navigation Mesh** is a navigation area which is arranged above the surface of an arbitrary mesh. In fact, the *Navigation Mesh* is an area of the specified height above the mesh polygons, which is available for pathfinding.


The mesh it stands on is either made by hand and loaded into the node, or built out of the geometry of the scene by the *[Bake](#bake_parameters)* section of the node.


Compared to a [navigation sector](../../../../objects/navigations/navigation/navigation_sector/index.md), a *Navigation Mesh* follows an arbitrary surface instead of a box, and it comes with the following restrictions:


- Only 2D routes can be calculated within the *Navigation Mesh*.
- Pathfinding can be performed within 1 *Navigation Mesh* only. Pathfinding within the following areas is not supported:

  - Within several intersecting *Navigation Meshes*
  - Within the intersecting *Navigation Mesh* and sector


> **Notice:** Not to be confused with the [Navigation Mesh (Experimental)](../../../../objects/navigations/experimental/navigation_mesh/index.md) node: despite the similar name the two belong to different systems and are unrelated. Routes over this node are calculated with the *[PathRoute](../../../../api/library/pathfinding/class.pathroute_cpp.md)* class.


### See also


- The *[NavigationMesh](../../../../api/library/pathfinding/class.navigationmesh_cpp.md)* class to manage navigation meshes via API
- The article on [Creating Routes](../../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md) to learn how to create routes inside the navigation mesh
- The article on [Baking Navigation Meshes](../../../../editor2/navigation_baking/index.md), which builds the mesh of this node out of the scene geometry
- The [Navigation Mesh (Experimental)](../../../../objects/navigations/experimental/navigation_mesh/index.md) node of the experimental navigation system
- [Navigation](../../../../sdk/api_samples/cs/navigation.md) samples in *C# Component Samples* suite


## Creating Navigation Mesh


A *Navigation Mesh* is created out of an existing mesh asset, and the mesh it holds can be replaced or rebuilt at any time afterwards.


1. [Run](../../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click *Create -> Navigation -> Navigation Mesh*. ![](create_nav_mesh.png)
3. In the file dialog window that opens, choose the required mesh to be used as a base for the new navigation area and click *OK*. [![](choose_nav_mesh_sm.png)](choose_nav_mesh.png)
4. Click somewhere in the world to place the *Navigation Mesh*. A new *Navigation Mesh* is added to UnigineEditor and you can edit it via the *[Parameters](../../../../editor2/node_parameters/index.md)* window.


> **Notice:** The created *Navigation Mesh* only provides an area within which 2D routes are calculated. The routes themselves should be [created using the script](../../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md).


### Mesh Requirements


Before adding a *Navigation Mesh*, you should prepare a mesh, on which this *Navigation Mesh* will be based. Such mesh is created separately and should meet the following requirements:


- Any polygon of the mesh must not share its edge with more than 2 other polygons; otherwise, an error will occur.
- Mesh polygons should be as wide as possible (ideally, they should be equilateral). Too narrow and high polygons may reduce accuracy of path calculation.
- The mesh should be optimized: it should not contain a large number of polygons.


> **Notice:** A mesh produced by *[Bake](#bake_parameters)* meets these requirements by construction, so they concern a mesh made by hand only.


### Example


If you have a scene with different objects and need to calculate a 2D route among them, add the *Navigation Mesh* to this scene as follows:


1. Create a flat mesh with holes in places where the objects are positioned. | [![](scene_example_sm.png)](scene_example.png) | [![](scene_sample_mesh_sm.png)](scene_sample_mesh.png) | |---|---| | *The scene* | *The mesh created for theNavigation Mesh* |
2. Specify this mesh as a base for a *Navigation Mesh* within which the route is calculated, and add the *Navigation Mesh* to the world. It will be highlighted in green: [![](navmesh_added_sm.png)](navmesh_added.png) *ANavigation Meshbased on the flat mesh*
3. Place the *Navigation Mesh* above the scene. [![](navmesh_on_scene_sm.png)](navmesh_on_scene.png) *TheNavigation Meshpositioned above the scene*


> **Notice:** In this case, you can also use a [navigation sector](../../../../objects/navigations/navigation/navigation_sector/index.md) with [obstacles](../../../../objects/navigations/obstacle/index.md) positioned inside it instead of the *Navigation Mesh*. However, the *Navigation Mesh* is preferred for more complex cases.


## Navigation Mesh Parameters


In the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the *Navigation Mesh*:


### Common Parameters


![](edit_nav_mesh.png)


| Mesh Path | The `.mesh` asset the walkable polygons are taken from. Pick another asset here to replace the mesh the node stands on. > **Notice:** *[Bake](#bake_parameters)* always writes to an asset named after the world and the node, and points this parameter at it. The asset goes to the directory open in the *Asset Browser*, or next to the world file when that directory is not writable. A path chosen by hand survives a bake only when its file name already matches that name. |
|---|---|
| Navigation Mask | The *Navigation* mask of the *Navigation Mesh* must match the *Navigation* mask of the route that is calculated within it. Otherwise, the *Navigation Mesh* does not participate in pathfinding. |
| Quality | Quality of optimization for route calculation. This value specifies the number of iterations that are used to find the shortcut. The higher the value, the longer the route calculation takes. |
| Velocity | Scaling factor for velocity of the point that moves inside the *Navigation Mesh*. |
| Dangerous | Danger factor that indicates if a moving point should try to avoid the *Navigation Mesh*. > **Notice:** If the danger factor exceeds the maximum danger factor set for the route, the *Navigation Mesh* is excluded from pathfinding calculations. |
| Depth | Depth of the heuristics used while a route is calculated. It sets how far ahead the search looks when it weighs the way out of a polygon: 0 weighs the neighbor polygon alone, and every step of the value takes one more polygon beyond it into account. The more the depth value, the better control over accuracy and speed of route calculation is provided. The value is an integer in the [0;5] range, and it is set to 0 for a new *Navigation Mesh*. Larger values are accepted and behave the same as 5. |
| Height | Distance above the mesh polygons available for pathfinding. By default, the height is set to 1 for a new *Navigation Mesh*. |
| Save Mesh As | Writes the polygons the node holds to a mesh asset. Use it to keep a baked result as an asset of its own, or to take the mesh of the node elsewhere. > **Notice:** The button works on one node at a time. With several *Navigation Mesh* nodes selected together it is greyed out. |


### Bake Parameters


The mesh a *Navigation Mesh* stands on does not have to be made by hand. The *Bake* section builds it out of the geometry of the scene: the parameters set how that geometry is traced, and the *Bake* button writes the polygons found inside the bake volume into the mesh of this node.


![](bake_nav_mesh.png)


The parameters are the same ones the experimental navigation system bakes with, and they are described in [Baking Navigation Meshes](../../../../editor2/navigation_baking/index.md#bake_parameters) together with the [mask](../../../../editor2/navigation_baking/index.md#bake_mask) the geometry has to carry to be taken in. Not every parameter of the section reaches a bake into this node � see the [notice](../../../../editor2/navigation_baking/index.md#bake_parameters) under the parameter table there.


Baking runs in the background and the editor stays usable while it goes on. Pressing the button again cancels it, and the polygons built before the cancel are kept. The button next to *Bake* opens *[Experimental Navigation](../../../../editor2/navigation_baking/index.md)*, the window that bakes every navigation mesh of the world from one list.


> **Notice:** A bake overwrites the mesh of the node and reassigns *[Mesh Path](#mesh_path)*. Save the current mesh with *[Save Mesh As](#save_mesh_as)* first when it is worth keeping.
