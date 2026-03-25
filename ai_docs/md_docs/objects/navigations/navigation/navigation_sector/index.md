# Navigation Sector


> **Warning:** 3D navigation feature is experimental and not recommended for production use.


A **Navigation Sector** is a cuboid-shaped navigation area that enables the following:


- Both the 2D and 3D routes can be calculated within navigation sectors.

  - In case of 2D routes, a point moves in a lower plane of the navigation sector (Z coordinate is not taken into account). If the height or radius set for this point is greater than the size of the navigation sector, such sector is discarded from pathfinding.
  - In case of 3D routes, a point moves in three dimensions. If the radius set for this point is greater than the size of the navigation sector, such sector is discarded from pathfinding.
- Routes can be calculated within several intersecting navigation sectors. The intersecting sectors are treated as a single navigation area. > **Notice:** In case of 2D routes, the height difference between the intersecting sectors must not exceed the maximum height set for the 2D route; otherwise these sectors are discarded from pathfinding.


### See also


- The *[NavigationSector](../../../../api/library/pathfinding/class.navigationsector_cpp.md)* class to manage navigation sectors via API
- The *[PathRoute](../../../../api/library/pathfinding/class.pathroute_cpp.md)* class to create 2D and 3D routes inside navigation sectors
- The article on [Creating Routes](../../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md)
- A set of samples located in the `<UnigineSDK>/data/uniginescript_samples/paths` folder:

  - `route_00`
  - `route_01`
  - `route_02`
  - `sector_00`
  - `sector_01`
  - `sector_02`
- *[Navigation](../../../../sdk/api_samples/cs/navigation.md)* samples in *C# Component Samples* suite


## Creating Navigation Sector


To create a navigation sector via UnigineEditor:


1. [Run](../../../../editor2/index.md#run) UnigineEditor.
2. On the Menu bar, click *Create -> Navigation -> Navigation Sector*. ![](create_nav_sector.png)
3. Click somewhere in the world to place the navigation sector. [![](add_nav_sector_sm.png)](add_nav_sector.png) *A navigation sector* A new navigation sector is added to UnigineEditor and you can edit it via the *[Parameters](../../../../editor2/node_parameters/index.md)* window.


> **Notice:** The created navigation sector only provides an area within which 2D and 3D routes are calculated. The routes themselves should be [created from the code](../../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md).


## Editing Navigation Sector


In the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the navigation sector:


![](edit_nav_sector.png)


| Navigation Mask | The *Navigation* mask of the navigation sector must [match](../../../../principles/bit_masking/index.md) the *Navigation* mask of the route that is calculated within it. Otherwise, the sector does not participate in pathfinding. By using the *Navigation* mask, you can specify sectors that must be ignored during pathfinding. |
|---|---|
| Quality | Quality of optimization for route calculation. This value specifies the number of iterations that are used to find the shortcut. The higher the value, the longer the route calculation will take. |
| Velocity | Scaling factor for velocity of the point that moves inside the navigation sector along the calculated route. |
| Dangerous | Danger factor that indicates if a moving point should try to avoid the navigation sector. > **Notice:** If the danger factor exceeds the maximum danger factor set for the route, the navigation sector is excluded from pathfinding calculations. |
| Size | Size of the navigation sector's box along the axes. |
