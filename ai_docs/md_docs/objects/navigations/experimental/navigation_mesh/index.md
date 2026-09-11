# Navigation Mesh (Experimental)


*Navigation Mesh (Experimental)* is a node of the experimental navigation system. It defines the part of the world to be baked into a navigation mesh and stores the result in a `.navmesh` asset. Agents find their paths over this navigation mesh.


> **Notice:** Not to be confused with the [Navigation Mesh](../../../../objects/navigations/navigation/navigation_mesh/index.md) node: despite the similar name the two belong to different systems and are unrelated.


### See Also


- The *[ExperimentalNavigationMesh](../../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)* class to manage the node and to query it via API
- The *[ExperimentalBakeNavigation](../../../../api/library/pathfinding/class.experimentalbakenavigation_cpp.md)* class to bake and to invalidate navigation meshes via API
- The [Navigation Mesh Area Volume (Experimental)](../../../../objects/navigations/experimental/area_volume/index.md) node to mark parts of the walkable surface
- The [Navigation Mesh Invoker (Experimental)](../../../../objects/navigations/experimental/invoker/index.md) node to stream tiles in a large world


## Adding Navigation Mesh


To add a navigation mesh to the scene via UnigineEditor, do the following:


1. On the Menu bar, click *Create -> Navigation -> Navigation Mesh (Experimental)*.
2. Place the node in the world and set *[Size](#bake_parameters)* so that the volume covers the area the agents are going to walk over.
3. Check that the geometry to be baked is taken in. Its [bake mask](../../../../principles/bit_masking/index.md#bake_mask) has to share a bit with the *[Mask](#bake_parameters)* of the node, and that mask is set separately on:

  - each surface of an object;
  - a [Global Terrain](../../../../objects/objects/terrain/terrain_global/index.md) or a [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) as a whole, and on every detail mask of the latter;
  - each [area volume](../../../../objects/navigations/experimental/area_volume/index.md).
4. Set up the [bake parameters](#bake_parameters) of the node.
5. Click *[Bake](../../../../editor2/navigation_baking/index.md#bake_button)*. Baking runs in the background, so you can keep working in the Editor.


> **Notice:** When *Mesh Path* is empty, the first bake creates the asset next to the world file and names it after the world and the node.


## Navigation Mesh Parameters


Parameters of the node are available in the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window.


### Common Parameters


| Mesh Path | The `.navmesh` asset this node bakes into. *Bake* writes the asset to this path, and the node loads its tiles from it. When the path is empty, the first bake creates the asset next to the world file, named after the world and the node. > **Notice:** A *Dynamic* navigation mesh writes no asset, so the parameter is hidden in that mode. |
|---|---|
| Mode | Mode defines how the navigation mesh is built and whether it can change afterwards: - **Static**. The navigation mesh is baked and cannot change. Any change requires a rebake. - **Static With Carve**. The navigation mesh is baked, and [Navigation Mesh Area Volume](../../../../objects/navigations/experimental/area_volume/index.md) nodes in *Dynamic* mode can change it at run time: repaint the surface or cut holes in it. - **Dynamic**. The navigation mesh is not baked. It is built on the fly as needed, and requires a [Navigation Mesh Invoker](../../../../objects/navigations/experimental/invoker/index.md) node for anything to be built at all. > **Notice:** Switching to *Static With Carve* takes effect only after a rebake. Until then the node keeps the data baked in *Static* mode, and the area volumes change nothing. |
| Navigation Mask | Selects which agents and invokers use this navigation mesh. A path query reaches it only if the [Navigation](../../../../principles/bit_masking/index.md#navigation_mask) mask of its [filter](../../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md) shares a bit with this one, and an invoker streams its tiles only if its own navigation mask shares a bit with this one. Use it to tell navigation meshes apart when several of them cover the same place. The size of the agent is baked into the surface and cannot be changed afterwards, so a mesh baked for a walking agent and a mesh baked for a vehicle are separate meshes. An agent takes the meshes this mask lets it into, and among those the engine gives it the one closest to its own size. |
| Streaming | Loads only the tiles the agents actually need, instead of holding the whole navigation mesh in memory. A tile is loaded within the *Load Distance* of a [Navigation Mesh Invoker](../../../../objects/navigations/experimental/invoker/index.md) and unloaded beyond its *Clear Distance*. With this off, the whole asset is loaded together with the world and no tile is ever dropped. The parameter is not available in *Dynamic* mode, where the navigation mesh always follows the invokers. > **Notice:** Streaming works through invokers only, and an invoker serves this navigation mesh only while their navigation masks share a bit. With no invoker that matches, nothing is loaded and every path query over this navigation mesh fails for lack of data. |


### Bake Parameters


The *Bake* section holds the parameters the navigation mesh is built with and the *Bake* button that builds it. They are described in [Baking Navigation Meshes](../../../../editor2/navigation_baking/index.md), together with the window that bakes several meshes at once.
