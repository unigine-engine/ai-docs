# Navigation Mesh Invoker (Experimental)


*Navigation Mesh Invoker (Experimental)* is a node of the experimental navigation system. It marks the place where a [navigation mesh](../../../../objects/navigations/experimental/navigation_mesh/index.md) has to be loaded. Tiles are kept around the invoker and dropped once it has moved away, so a world too large to fit in memory holds only the part that is in use.


Attach one to the player, to every active character, or to a camera, and the navigation mesh follows it.


> **Notice:** An invoker does nothing on its own. The navigation mesh it serves has to have *Streaming* switched on, or be in *Dynamic* mode.


### See Also


- The *[ExperimentalNavigationMeshInvoker](../../../../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cpp.md)* class to manage the node via API
- The [Navigation Mesh (Experimental)](../../../../objects/navigations/experimental/navigation_mesh/index.md) node whose tiles the invoker loads


## Adding Navigation Mesh Invoker


To add an invoker to the scene via UnigineEditor, do the following:


1. On the Menu bar, click *Create -> Navigation -> Navigation Mesh Invoker (Experimental)*.
2. Make the node a child of the player, of the character, or of whatever else the navigation mesh has to follow.
3. Set *[Navigation Mask](#navigation_mask)* so that it shares a bit with the navigation mask of the navigation meshes to be served.
4. Set *[Load Distance](#load_distance)* to cover what the agents around the invoker are going to ask about.


## Navigation Mesh Invoker Parameters


Parameters of the node are available in the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window.


| Load Distance | Distance from the invoker, in units, within which the tiles are kept loaded. A path is only searched over the tiles that are loaded, so this distance sets how far an agent near the invoker can plan. A destination beyond it cannot be reached. > **Notice:** Teleporting the invoker drops it where nothing is loaded yet, and the first query there fails for lack of data. The tiles of the destination can be loaded in advance through the [ExperimentalNavigationMeshInvoker](../../../../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cpp.md) class. |
|---|---|
| Clear Distance | Distance from the invoker, in units, beyond which the tiles are unloaded. It never goes below *Load Distance*: a smaller value is raised to it. The gap between the two is what keeps a tile at the border from being loaded and dropped again every time the invoker steps back and forth. |
| Navigation Mask | The invoker serves a navigation mesh only if the [Navigation](../../../../principles/bit_masking/index.md#navigation_mask) mask of that mesh shares a bit with this one. Use it to keep an invoker to its own meshes. The one that follows a walking agent has no reason to load the tiles baked for a vehicle. |
