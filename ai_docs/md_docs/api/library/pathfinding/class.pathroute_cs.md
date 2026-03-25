# Unigine::PathRoute Class (CS)


> **Warning:** - 3D navigation feature is experimental and not recommended for production use.
> - There is no connection between functions of the *PathRoute* class and functions of the *Path* class.


This class calculates the shortest 2D or 3D route around the obstacles within connected navigation areas and sets the size and velocity of the point moving along this route.


- In case of **2D** route, a point moves in the lower plane of the navigation area. The Z coordinate is not taken into account when calculating the 2D route. The height and radius values set for the point via *[*Height*](#setHeight_float_void)* and *[*Radius*](#setRadius_float_void)* are used to check whether the navigation area can take part in pathfinding: if the height or radius set for the point is greater than the size of the navigation area, such navigation area will be discarded. If the height difference between the connected areas exceeds the [maximum height](#setMaxHeight_float_void), the navigation area is also discarded from calculations.
- In case of **3D** route (available only for [navigation sectors](../../../api/library/pathfinding/class.navigationsector_cs.md)), a point moves in 3 dimensions. The radius set for the point via *[*Radius*](#setRadius_float_void)* is used to check whether the navigation sector can take part in pathfinding: if the radius set for the point is greater than the size of the navigation sector, it will be discarded. Also the point cannot rise up higher than the [maximum height](#setMaxHeight_float_void) set for the navigation sector.


Functions of the PathRoute class allow ignoring the specified [navigation areas](#setExcludeNavigations_VECNode_void) and [obstacles](#setExcludeObstacles_VECNode_void).


The [maximum time](#setMaxTime_float_void) acceptable to get to the destination point and the [maximum danger](#setMaxDangerous_float_void) factor can be limited as well.


> **Notice:** To choose between navigation areas, A* algorithm is used.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cs.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## PathRoute Class

### Properties

## float Velocity

The velocity of the point that moves along the route.
## float Radius

The radius required to move the point along the route inside the navigation area. If the specified radius exceeds the size of the navigation area, the point will not move inside it.
## int ObstacleMask

The obstacle mask. The obstacle is taken into account if its obstacle mask [matches](../../../principles/bit_masking/index.md) the obstacle mask of the route.
## 🔒︎ int NumPoints

The number of turning points along the route.
## int NavigationMask

The navigation mask. The navigation mask of the navigation area must [match](../../../principles/bit_masking/index.md) the navigation mask of the route that is calculated within it. Otherwise, the area will not participate in pathfinding.
## float MaxTime

The maximum time for reaching the destination point. If the route takes longer, the point will not move along it.
## float MaxHeight

The maximum height difference between the connected navigation areas acceptable when finding the 2D route. In case of the 3D route, it is the maximum height the point can move up to.
## float MaxDangerous

The maximum danger factor acceptable for moving along this route. If the navigation areas have a higher danger factor, the point will not move along it.
## float MaxAngle

The cosine of the maximum possible angle between [navigation mesh](../../../api/library/pathfinding/class.navigationmesh_cs.md) polygons. For example, this option enables to exclude walls when calculating a valid route.
## float Height

The height that is required to move the point along the 2D route inside the navigation area. If the specified height exceeds the height of the navigation area, the point will not move inside it.
## 🔒︎ bool IsReady

The value indicating that the route is calculated.
## 🔒︎ bool IsReached

The value indicating that the destination point of the route is reached.
## 🔒︎ bool IsQueued

The value indicating that the route is queued to be calculated.
## 🔒︎ float Time

The time required for the point to move along the route.
## 🔒︎ float Distance

The length of the route.
## 🔒︎ float Dangerous

The highest danger factor of the navigation areas met along the route.
### Members

---

## PathRoute ( float radius = 0.0f )

Constructor. Creates a new 2D or 3D route. The radius is used to check whether the point can move inside a navigation area or this navigation area should be excluded from pathfinding.
### Arguments

- *float* **radius** - Radius of the point moving along the route.

## void SetExcludeNavigations ( Node [] exclude_navigations )

Sets the list of navigation sectors and navigation meshes to be ignored during pathfinding.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **exclude_navigations** - Array of the ignored navigation areas.

## Node [] GetExcludeNavigations ( )

Returns the list of navigation sectors and navigation meshes excluded from pathfinding.
### Arguments

### Return value

Container to store the result.
## void SetExcludeObstacles ( Node [] obstacles )

Sets the list of obstacles to be ignored during pathfinding.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **obstacles** - Array of the ignored obstacles.

## Node [] GetExcludeObstacles ( )

Returns the list of obstacles ignored during pathfinding.
### Return value

Container for obstacles.
## Obstacle GetIntersection ( PathRouteIntersection intersection )

Returns the first intersected obstacle.
### Arguments

- *[PathRouteIntersection](../../../api/library/pathfinding/class.pathrouteintersection_cs.md)* **intersection** - PathRouteIntersection node.

### Return value

Intersected obstacle.
## Navigation GetNavigation ( int num )

Returns the navigation sector or mesh within which the specified route point is located.
### Arguments

- *int* **num** - Point number.

### Return value

Navigation sector or navigation mesh.
## Obstacle GetObstacle ( int num )

Returns the obstacle around which the route is turning.
### Arguments

- *int* **num** - Point number.

### Return value

Obstacle.
## vec3 GetPoint ( int num )

Returns the coordinates of the turning point in the route.
### Arguments

- *int* **num** - Point number.

### Return value

Point coordinates.
## void AddExcludeNavigation ( Node navigation )

Sets a navigation sector or a navigation mesh to be ignored during pathfinding. Excluded sectors/meshes are added into the list.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **navigation** - A navigation area to be ignored.

## void AddExcludeObstacle ( Node obstacle )

Sets an obstacle to be ignored during pathfinding. Excluded obstacles are added into the list.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **obstacle** - An obstacle to be ignored.

## void Create2D ( vec3 p0 , vec3 p1 , int delay = 0 )

Calculates a 2D route between the given points with the specified delay.
### Arguments

- *vec3* **p0** - The starting point.
- *vec3* **p1** - The destination point.
- *int* **delay** - The number of frames which is possible to delay pathfinding calculations. **0** means the pathfinding should be calculated immediately.

## void Create3D ( vec3 p0 , vec3 p1 , int delay = 0 )

Calculates a 3D route between the given points with the specified delay.
### Arguments

- *vec3* **p0** - The starting point.
- *vec3* **p1** - The destination point.
- *int* **delay** - The number of frames which is possible to delay pathfinding calculations. **0** means the pathfinding should be calculated immediately.

## void RemoveExcludeNavigation ( Node navigation )

Removes a navigation sector or a navigation mesh from the list of ignored ones during pathfinding.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **navigation** - A navigation area.

## void RemoveExcludeObstacle ( Node obstacle )

Removes an obstacle from the list of ignored ones during pathfinding.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **obstacle** - An obstacle.

## void RenderVisualizer ( vec4 color )

Renders the route in a given color.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


### Arguments

- *vec4* **color** - Route color.
