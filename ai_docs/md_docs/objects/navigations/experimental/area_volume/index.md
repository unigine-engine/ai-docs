# Navigation Mesh Area Volume (Experimental)


*Navigation Mesh Area Volume (Experimental)* is a node of the experimental navigation system. It marks the part of a [navigation mesh](../../../../objects/navigations/experimental/navigation_mesh/index.md) that falls inside its shape: the ground there is given an area, and a search treats it as mud, as a road, or as a place to keep out of. The same node also cuts, taking the walkable surface inside it away.


The scene geometry is not touched either way. Only the navigation mesh is.


### See Also


- The *[ExperimentalNavigationMeshAreaVolume](../../../../api/library/pathfinding/class.experimentalnavigationmeshareavolume_cpp.md)* class to manage the node via API
- The *[ExperimentalNavigation](../../../../api/library/pathfinding/class.experimentalnavigation_cpp.md)* class that holds the areas with their names, costs and flags
- The [Navigation Mesh (Experimental)](../../../../objects/navigations/experimental/navigation_mesh/index.md) node the volume applies to


## Adding Navigation Mesh Area Volume


To add an area volume to the scene via UnigineEditor, do the following:


1. On the Menu bar, click *Create -> Navigation -> Navigation Mesh Area Volume (Experimental)*.
2. Place the volume over the ground to be marked and set its *[Shape](#shape)* and size.
3. Pick the *[Area](#area)* to mark with, or *Cut* to take the walkable surface away.
4. Check that *[Bake Mask](#bake_mask)* shares a bit with the bake mask of the navigation mesh, and bake it again.


## Navigation Mesh Area Volume Parameters


Parameters of the node are available in the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window. The rows that do not apply to the current shape and mode are hidden.


| Shape | Shape of the volume: *Box*, *Sphere* or *Cylinder*. > **Notice:** A box only turns around the vertical axis. Tilting the node leaves the marked volume upright. |
|---|---|
| Size | Size of the box along the node axes, in units. Shown for the *Box* shape. |
| Radius | Radius of the sphere or of the cylinder, in units. Shown for the *Sphere* and *Cylinder* shapes. |
| Height | Height of the cylinder along the node vertical axis, in units. Shown for the *Cylinder* shape. |
| Area | Area the ground inside the volume is marked with. The names, the costs and the flags of the areas live in one registry shared by the whole world, and the button next to the list opens its editor. > **Notice:** The reserved *Cut* area marks nothing. It takes the walkable surface inside the volume away. |
| Priority | Overlapping volumes are applied from the lowest priority to the highest, so the highest one wins. Volumes of equal priority go in order of traversal cost, and the more expensive area wins. > **Notice:** A volume that cuts wins over any marking volume whatever the priority. Ground that has been cut away is never filled back in. |
| Expand By Agent Radius | Grows the volume sideways by the agent radius of the navigation mesh. Use it for a zone the agent has to keep away from, rather than one it must not step on. The height stays as it is. |
| Mode | When the volume does its work: - **Bake**. The volume is written into the navigation mesh while it is baked, and does nothing afterwards. Changing it asks for a rebake. - **Dynamic**. The volume keeps applying itself while the application runs, and rebuilds the ground it covers every time it changes. > **Notice:** A *Dynamic* volume needs a navigation mesh that is allowed to change: baked in *Static With Carve* or *Dynamic* mode. A mesh baked in *Static* mode ignores it. |
| Apply Only When Stationary | Applies the volume only once it has stopped moving. A volume that keeps moving rebuilds the ground under it over and over, so switch this off only for a volume that has to follow a moving object. Shown for the *Dynamic* mode. |
| Move Threshold | How far the volume has to move, in units, before the move counts as a move. It keeps jitter from postponing the update forever. Shown for the *Dynamic* mode. |
| Time To Stationary | How long the volume has to stay still, in seconds, before the ground it covers is rebuilt. Shown when *Apply Only When Stationary* is on. |
| Bake Mask | The volume takes part in the bake of a navigation mesh only if this [Bake](../../../../principles/bit_masking/index.md#bake_mask) mask shares a bit with the bake mask of that navigation mesh. |
