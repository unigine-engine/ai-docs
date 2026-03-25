# Navigation and Pathfinding


This section provides a set of examples introducing various approaches to pathfinding implementation. These examples explain how to calculate routes in 2D and 3D spaces, with or without obstacles, and also showcase the features and usage of different navigation areas.


In UNIGINE, pathfinding can be performed within a *Navigation Area* of one of the following types:


- **[Navigation Mesh](../../../objects/navigations/navigation/navigation_mesh/index.md)** based on an [arbitrary mesh](../../../objects/navigations/navigation/navigation_mesh/index.md#create), allowing calculation of only 2D routes within it.
- **[Navigation Sector](../../../objects/navigations/navigation/navigation_sector/index.md)**, a plain cuboid-shaped navigation area where both 2D and 3D routes can be calculated.


You can place **[obstacles](../../../objects/navigations/obstacle/index.md)** in the navigation area: invisible nodes to be bypassed by the routes. You can use an obstacle as a single node or as a child node of a node that needs to be bypassed. The difference is in how the obstacle's transformation will change. UNIGINE provides 3 types of obstacles. You should select the appropriate type depending on the shape of the node or area to be bypassed during pathfinding.


### See Also


- Articles of the *[Pathfinding Objects](../../../objects/navigations/index.md)* section.
- The C# component samples on *[Navigation](../../../sdk/api_samples/cs/navigation.md)*.
