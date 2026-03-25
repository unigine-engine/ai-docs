# Unigine::PathRoute Class (CPP)

**Header:** #include <UniginePathFinding.h>


> **Warning:** - 3D navigation feature is experimental and not recommended for production use.
> - There is no connection between functions of the *PathRoute* class and functions of the *Path* class.


This class calculates the shortest 2D or 3D route around the obstacles within connected navigation areas and sets the size and velocity of the point moving along this route.


- In case of **2D** route, a point moves in the lower plane of the navigation area. The Z coordinate is not taken into account when calculating the 2D route. The height and radius values set for the point via *[*setHeight()*](#setHeight_float_void)* and *[*setRadius()*](#setRadius_float_void)* are used to check whether the navigation area can take part in pathfinding: if the height or radius set for the point is greater than the size of the navigation area, such navigation area will be discarded. If the height difference between the connected areas exceeds the [maximum height](#setMaxHeight_float_void), the navigation area is also discarded from calculations.
- In case of **3D** route (available only for [navigation sectors](../../../api/library/pathfinding/class.navigationsector_cpp.md)), a point moves in 3 dimensions. The radius set for the point via *[*setRadius()*](#setRadius_float_void)* is used to check whether the navigation sector can take part in pathfinding: if the radius set for the point is greater than the size of the navigation sector, it will be discarded. Also the point cannot rise up higher than the [maximum height](#setMaxHeight_float_void) set for the navigation sector.


Functions of the PathRoute class allow ignoring the specified [navigation areas](#setExcludeNavigations_VECNode_void) and [obstacles](#setExcludeObstacles_VECNode_void).


The [maximum time](#setMaxTime_float_void) acceptable to get to the destination point and the [maximum danger](#setMaxDangerous_float_void) factor can be limited as well.


> **Notice:** To choose between navigation areas, A* algorithm is used.


### See Also


- The [Creating Routes](../../../code/usage/navigation_and_pathfinding/routes/index_cpp.md) usage example demonstrating how to create routes and recalculate them considering obstacles
- *[Navigation](../../../sdk/api_samples/cpp/navigation.md)* section in C++ Samples
- *[Navigation](../../../sdk/api_samples/cs/navigation.md)* section in C# Component Samples
- *[Pathfinding](../../../code/uniginescript/samples/pathfinding.md)* section in UnigineScript samples


## PathRoute Class

### Members

## void setVelocity ( float velocity )

Sets a new velocity of the point that moves along the route.
### Arguments

- *float* **velocity** - The velocity of the point moving along the route.

## float getVelocity () const

Returns the current velocity of the point that moves along the route.
### Return value

Current velocity of the point moving along the route.
## void setRadius ( float radius )

Sets a new radius required to move the point along the route inside the navigation area. If the specified radius exceeds the size of the navigation area, the point will not move inside it.
### Arguments

- *float* **radius** - The radius required to move the point along the route inside the navigation area. If a negative value is provided, **0** will be used instead.

## float getRadius () const

Returns the current radius required to move the point along the route inside the navigation area. If the specified radius exceeds the size of the navigation area, the point will not move inside it.
### Return value

Current radius required to move the point along the route inside the navigation area. If a negative value is provided, **0** will be used instead.
## void setObstacleMask ( int mask )

Sets a new obstacle mask. The obstacle is taken into account if its obstacle mask [matches](../../../principles/bit_masking/index.md) the obstacle mask of the route.
### Arguments

- *int* **mask** - The integer value, each bit of which is used to set a mask.

## int getObstacleMask () const

Returns the current obstacle mask. The obstacle is taken into account if its obstacle mask [matches](../../../principles/bit_masking/index.md) the obstacle mask of the route.
### Return value

Current integer value, each bit of which is used to set a mask.
## int getNumPoints () const

Returns the current number of turning points along the route.
### Return value

Current number of turning points along the route.
## void setNavigationMask ( int mask )

Sets a new navigation mask. The navigation mask of the navigation area must [match](../../../principles/bit_masking/index.md) the navigation mask of the route that is calculated within it. Otherwise, the area will not participate in pathfinding.
### Arguments

- *int* **mask** - The integer value, each bit of which is used to set a mask.

## int getNavigationMask () const

Returns the current navigation mask. The navigation mask of the navigation area must [match](../../../principles/bit_masking/index.md) the navigation mask of the route that is calculated within it. Otherwise, the area will not participate in pathfinding.
### Return value

Current integer value, each bit of which is used to set a mask.
## void setMaxTime ( float time )

Sets a new maximum time for reaching the destination point. If the route takes longer, the point will not move along it.
### Arguments

- *float* **time** - The maximum movement time.

## float getMaxTime () const

Returns the current maximum time for reaching the destination point. If the route takes longer, the point will not move along it.
### Return value

Current maximum movement time.
## void setMaxHeight ( float height )

Sets a new maximum height difference between the connected navigation areas acceptable when finding the 2D route. In case of the 3D route, it is the maximum height the point can move up to.
### Arguments

- *float* **height** - The maximum height.

## float getMaxHeight () const

Returns the current maximum height difference between the connected navigation areas acceptable when finding the 2D route. In case of the 3D route, it is the maximum height the point can move up to.
### Return value

Current maximum height.
## void setMaxDangerous ( float dangerous )

Sets a new maximum danger factor acceptable for moving along this route. If the navigation areas have a higher danger factor, the point will not move along it.
### Arguments

- *float* **dangerous** - The maximum danger factor.

## float getMaxDangerous () const

Returns the current maximum danger factor acceptable for moving along this route. If the navigation areas have a higher danger factor, the point will not move along it.
### Return value

Current maximum danger factor.
## void setMaxAngle ( float angle )

Sets a new cosine of the maximum possible angle between [navigation mesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md) polygons. For example, this option enables to exclude walls when calculating a valid route.
### Arguments

- *float* **angle** - The maximum angle cosine.

## float getMaxAngle () const

Returns the current cosine of the maximum possible angle between [navigation mesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md) polygons. For example, this option enables to exclude walls when calculating a valid route.
### Return value

Current maximum angle cosine.
## void setHeight ( float height )

Sets a new height that is required to move the point along the 2D route inside the navigation area. If the specified height exceeds the height of the navigation area, the point will not move inside it.
### Arguments

- *float* **height** - The height that is required to move the point inside the navigation area. If a negative value is provided, **0** is used instead.

## float getHeight () const

Returns the current height that is required to move the point along the 2D route inside the navigation area. If the specified height exceeds the height of the navigation area, the point will not move inside it.
### Return value

Current height that is required to move the point inside the navigation area. If a negative value is provided, **0** is used instead.
## int isReady () const

Returns the current value indicating that the route is calculated.
### Return value

Current the route is calculated
## int isReached () const

Returns the current value indicating that the destination point of the route is reached.
### Return value

Current the destination point is reached
## int isQueued () const

Returns the current value indicating that the route is queued to be calculated.
### Return value

Current the route is queued for calculation
## float getTime () const

Returns the current time required for the point to move along the route.
### Return value

Current time required for the point to move along the route, in seconds.
## float getDistance () const

Returns the current length of the route.
### Return value

Current length of the route, in units.
## float getDangerous () const

Returns the current highest danger factor of the navigation areas met along the route.
### Return value

Current highest danger factor
---

## static PathRoutePtr create ( float radius = 0.0f )

Constructor. Creates a new 2D or 3D route. The radius is used to check whether the point can move inside a navigation area or this navigation area should be excluded from pathfinding.
### Arguments

- *float* **radius** - Radius of the point moving along the route.

## void setExcludeNavigations ( const Vector < Ptr < Node > > & exclude_navigations )

Sets the list of navigation sectors and navigation meshes to be ignored during pathfinding.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> > &* **exclude_navigations** - Array of the ignored navigation areas.

## Vector < Ptr < Node > > getExcludeNavigations ( )

Returns the list of navigation sectors and navigation meshes excluded from pathfinding.
### Arguments

### Return value

Container to store the result.
## void setExcludeObstacles ( const Vector < Ptr < Node > > & obstacles )

Sets the list of obstacles to be ignored during pathfinding.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> > &* **obstacles** - Array of the ignored obstacles.

## Vector < Ptr < Node > > getExcludeObstacles ( )

Returns the list of obstacles ignored during pathfinding.
### Return value

Container for obstacles.
## Ptr < Obstacle > getIntersection ( const Ptr < PathRouteIntersection > & intersection )

Returns the first intersected obstacle.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[PathRouteIntersection](../../../api/library/pathfinding/class.pathrouteintersection_cpp.md)> &* **intersection** - PathRouteIntersection node.

### Return value

Intersected obstacle.
## Ptr < Navigation > getNavigation ( int num )

Returns the navigation sector or mesh within which the specified route point is located.
### Arguments

- *int* **num** - Point number.

### Return value

Navigation sector or navigation mesh.
## Ptr < Obstacle > getObstacle ( int num )

Returns the obstacle around which the route is turning.
### Arguments

- *int* **num** - Point number.

### Return value

Obstacle.
## Math:: Vec3 getPoint ( int num )

Returns the coordinates of the turning point in the route.
### Arguments

- *int* **num** - Point number.

### Return value

Point coordinates.
## void addExcludeNavigation ( const Ptr < Node > & navigation )

Sets a navigation sector or a navigation mesh to be ignored during pathfinding. Excluded sectors/meshes are added into the list.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **navigation** - A navigation area to be ignored.

## void addExcludeObstacle ( const Ptr < Node > & obstacle )

Sets an obstacle to be ignored during pathfinding. Excluded obstacles are added into the list.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **obstacle** - An obstacle to be ignored.

## void create2D ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int delay = 0 )

Calculates a 2D route between the given points with the specified delay.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - The starting point.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - The destination point.
- *int* **delay** - The number of frames which is possible to delay pathfinding calculations. **0** means the pathfinding should be calculated immediately.

## void create3D ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , int delay = 0 )

Calculates a 3D route between the given points with the specified delay.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - The starting point.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - The destination point.
- *int* **delay** - The number of frames which is possible to delay pathfinding calculations. **0** means the pathfinding should be calculated immediately.

## void removeExcludeNavigation ( const Ptr < Node > & navigation )

Removes a navigation sector or a navigation mesh from the list of ignored ones during pathfinding.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **navigation** - A navigation area.

## void removeExcludeObstacle ( const Ptr < Node > & obstacle )

Removes an obstacle from the list of ignored ones during pathfinding.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **obstacle** - An obstacle.

## void renderVisualizer ( const Math:: vec4 & color )

Renders the route in a given color.
> **Notice:** You should enable the engine visualizer by the **show_visualizer 1** console command.


### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Route color.
