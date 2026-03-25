# Navigation Mesh


The **Navigation Mesh** is a navigation area which is arranged above the surface of an arbitrary mesh. In fact, the *Navigation Mesh* is an area of the specified height above the mesh polygons, which is available for pathfinding.


In contrast to [navigation sectors](../../../../objects/navigations/navigation/navigation_sector/index.md), the *Navigation Mesh* enables the following:


- Only 2D routes can be calculated within the *Navigation Mesh*.
- Pathfinding can be performed within 1 *Navigation Mesh* only. Pathfinding within the following areas is not supported:

  - Within several intersecting *Navigation Meshes*
  - Within the intersecting *Navigation Mesh* and sector


### See also


- The *[NavigationMesh](../../../../api/library/pathfinding/class.navigationmesh_cpp.md)* class to manage navigation meshes via API
- The article on [Creating Routes](../../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md) to learn how to create routes inside the navigation mesh
- A set of samples located in the `<UnigineSDK>/data/samples/paths` folder:

  - `mesh_00`
  - `route_03`
- [Navigation](../../../../sdk/api_samples/cs/navigation.md) samples in *C# Component Samples* suite


## Creating Navigation Mesh


Before adding a *Navigation Mesh*, you should prepare a mesh, on which this *Navigation Mesh* will be based. Such mesh is created separately and should meet the following requirements:


- Any polygon of the mesh must not share its edge with more than 2 other polygons; otherwise, an error will occur.
- Mesh polygons should be as wide as possible (ideally, they should be equilateral). Too narrow and high polygons may reduce accuracy of path calculation.
- The mesh should be optimized: it should not contain a large number of polygons.


When a mesh is prepared, you can add the *Navigation Mesh* to the scene via UnigineEditor:


1. [Run](../../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click *Create -> Navigation -> Navigation Mesh*. ![](create_nav_mesh.png)
3. In the file dialog window that opens, choose the required mesh to be used as a base for the new navigation area and click *OK*. [![](choose_nav_mesh_sm.png)](choose_nav_mesh.png)
4. Click somewhere in the world to place the *Navigation Mesh*. A new *Navigation Mesh* is added to UnigineEditor and you can edit it via the *[Parameters](../../../../editor2/node_parameters/index.md)* window.


> **Notice:** The created *Navigation Mesh* only provides an area within which 2D routes are calculated. The routes themselves should be [created using the script](../../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md).


### Example


If you have a scene with different objects and need to calculate a 2D route among them, add the *Navigation Mesh* to this scene as follows:


1. Create a flat mesh with holes in places where the objects are positioned. | [![](scene_example_sm.png)](scene_example.png) | [![](scene_sample_mesh_sm.png)](scene_sample_mesh.png) | |---|---| | *The scene* | *The mesh created for theNavigation Mesh* |
2. Specify this mesh as a base for a *Navigation Mesh* within which the route is calculated, and add the *Navigation Mesh* to the world. It will be highlighted in green: [![](navmesh_added_sm.png)](navmesh_added.png) *ANavigation Meshbased on the flat mesh*
3. Place the *Navigation Mesh* above the scene. [![](navmesh_on_scene_sm.png)](navmesh_on_scene.png) *TheNavigation Meshpositioned above the scene*


> **Notice:** In this case, you can also use a [navigation sector](../../../../objects/navigations/navigation/navigation_sector/index.md) with [obstacles](../../../../objects/navigations/obstacle/index.md) positioned inside it instead of the *Navigation Mesh*. However, the *Navigation Mesh* is preferred for more complex cases.


## Editing Navigation Mesh


In the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the *Navigation Mesh*:


![](edit_nav_mesh.png)


| Navigation Mask | The *Navigation* mask of the *Navigation Mesh* must match the *Navigation* mask of the route that is calculated within it. Otherwise, the *Navigation Mesh* does not participate in pathfinding. |
|---|---|
| Quality | Quality of optimization for route calculation. This value specifies the number of iterations that are used to find the shortcut. The higher the value, the longer the route calculation takes. |
| Velocity | Scaling factor for velocity of the point that moves inside the *Navigation Mesh*. |
| Dangerous | Danger factor that indicates if a moving point should try to avoid the *Navigation Mesh*. > **Notice:** If the danger factor exceeds the maximum danger factor set for the route, the *Navigation Mesh* is excluded from pathfinding calculations. |
| Depth | Depth value. This value affects the quality of the route that is currently calculated. The more the depth value, the better control over accuracy and speed of route calculation is provided. The depth can take integer value in range [0;4]. By default, the depth is set to 0 for a new *Navigation Mesh*. The 2, 3, 4 values are used for deeper heuristics. |
| Height | Distance above the mesh polygons available for pathfinding. By default, the height is set to 1 for a new *Navigation Mesh*. |


### Loading a New Mesh


To load a new mesh on which the navigation area is based:


1. On the *Navigation* tab, press ![](navigation_mesh_load.png).
2. In the file dialog window that opens, choose the required mesh and press *OK*.


### Saving the Current Mesh


To save the current mesh on which the navigation area is based:


1. On the *Navigation* tab, press ![](navigation_mesh_save.png).
2. In the file dialog window that opens, specify a name for the mesh and press *OK*.
