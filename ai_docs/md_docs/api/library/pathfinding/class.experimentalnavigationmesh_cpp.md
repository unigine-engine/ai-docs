# Unigine::ExperimentalNavigationMesh Class (CPP)

**Header:** #include <UnigineExperimentalNavigation.h>

**Inherits from:** Node


> **Notice:** Not to be confused with the legacy [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md) class: despite the similar name they are unrelated.


The walkable surface of a world, baked out of scene geometry as convex polygons and split into tiles. Everything else in the navigation system reads it: paths are searched over its polygons, corridors follow bands of them, and avoidance keeps agents inside its boundaries.


Where the legacy navigation classes required the walkable space to be authored by hand, this node derives it from the geometry already in the scene. What goes in is selected by [BakeMask](../../../api/library/pathfinding/class.experimentalnavigationbakesettings_cpp.md#BakeMask); how it is turned into polygons is governed by the **Bake** settings; [BakeMode](#BakeMode) decides whether the result is loaded from an asset, carved at runtime, or generated in memory from scratch.


Two families of settings look alike and are worth telling apart. The **Bake** ones describe what the mesh *will* be built with and can be edited at any time. The **Data** ones report what the loaded data was *actually* built with. Queries compare against the second family, so changing a bake setting without rebaking never silently invalidates an agent's assumptions.


## ExperimentalNavigationMesh Class

### Enums

## BAKE_MODE

| Name | Description |
|---|---|
| **BAKE_MODE_STATIC** = 0 | The navigation data is loaded from the asset and never changes. The cheapest mode, and the right one for a level whose walkable space is fixed. |
| **BAKE_MODE_STATIC_CARVE** = 1 | The navigation data is loaded from the asset, and runtime obstacles are carved out of it. It suits a fixed level with things that move through it � a lowered barrier, a parked vehicle, rubble from a collapse. |
| **BAKE_MODE_DYNAMIC** = 2 | The navigation data is generated in memory from the current geometry and never touches an asset. Meant for procedurally built levels, where there is nothing to bake beforehand. |

### Members

## ExperimentalNavigationBakeSettings getBakeSettings () const

Returns the current settings the mesh is baked with. They belong to a separate object shared with the legacy [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cpp.md) node, so one editor panel drives both. The object lives as long as the node does.
### Return value

Current bake settings of this node.
## void setBakeMode ( ExperimentalNavigationMesh::BAKE_MODE mode )

Sets a new where the navigation data comes from and whether it changes at runtime. One node covers all three cases; the mode can be switched while the application runs.
### Arguments

- *[ExperimentalNavigationMesh::BAKE_MODE](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md#BAKE_MODE)* **mode** - The mode, one of the [BAKE_MODE_*](#BAKE_MODE_STATIC) values. The default value is [BAKE_MODE_STATIC](#BAKE_MODE_STATIC).

## ExperimentalNavigationMesh::BAKE_MODE getBakeMode () const

Returns the current where the navigation data comes from and whether it changes at runtime. One node covers all three cases; the mode can be switched while the application runs.
### Return value

Current mode, one of the [BAKE_MODE_*](#BAKE_MODE_STATIC) values. The default value is [BAKE_MODE_STATIC](#BAKE_MODE_STATIC).
## float getDataAgentHeight () const

Returns the current agent height the loaded data was actually baked with. Queries are matched against this value, not against the bake setting.
### Return value

Current agent height of the data, in units.
## float getDataAgentRadius () const

Returns the current agent radius the loaded data was actually baked with. A query is served by this mesh only when the radius in its filter does not exceed this value.
### Return value

Current agent radius of the data, in units.
## ExperimentalNavigationMesh::BAKE_MODE getDataBakeMode () const

Returns the current mode the loaded data was actually produced in. It can differ from the mode set on the node until the mesh is baked again.
### Return value

Current bake mode of the data, one of the [BAKE_MODE_*](#BAKE_MODE_STATIC) values.
## float getDataCellSize () const

Returns the current cell size the loaded data was actually baked with.
### Return value

Current cell size of the data, in units.
## unsigned long long getDataHash () const

Returns the current hash of the inputs the loaded data was produced from. Comparing it against the current settings and geometry is how the engine tells whether the mesh is still up to date.
### Return value

Current hash of the data.
## float getDataMaxSlopeAngle () const

Returns the current maximum slope angle the loaded data was actually baked with.
### Return value

Current maximum slope angle of the data, in degrees.
## float getDataMaxStepHeight () const

Returns the current maximum step height the loaded data was actually baked with. A query asks for no more than it can climb, so this value is matched against the step limit of the filter.
### Return value

Current maximum step height of the data, in units.
## int getDataTileResolution () const

Returns the current tile resolution in cells the loaded data was actually baked with.
### Return value

Current tile resolution of the data, in cells.
## float getDataTileWorldSize () const

Returns the current world size of one tile of the loaded data, in units.
### Return value

Current tile size of the data, in units.
## unsigned long long getDataVersion () const

Returns the current counter bumped every time the data changes � after a bake, a rebuild, or a tile being streamed in or out. Polygon identifiers stay valid only while it holds still, so anything caching them has to store the version alongside and re-resolve when it moves.
### Return value

Current version of the data.
## bool isFileLoaded () const

Returns the current value indicating if the asset file of the mesh is loaded. In [BAKE_MODE_DYNAMIC](#BAKE_MODE_DYNAMIC) it is always false � there is no file, the data is generated in memory.
### Return value

**true** if the asset file is loaded; otherwise **false**.
## bool isNeedBake () const

Returns the current value indicating if the data no longer matches the settings and the geometry it was built from.
### Return value

**true** if the mesh has to be baked again; otherwise **false**.
## const char * getMeshPath () const

Returns the path to the asset the navigation data is loaded from.
### Return value

path to the navigation mesh asset.
## void setNavigationMask ( int mask )

Sets a new mask that decides which queries this mesh serves. A query uses the mesh only when the navigation mask of its filter shares at least one bit with this one, which is how meshes baked for different kinds of agent are kept apart.
### Arguments

- *int* **mask** - The navigation mask. The default value is 1.

## int getNavigationMask () const

Returns the current mask that decides which queries this mesh serves. A query uses the mesh only when the navigation mask of its filter shares at least one bit with this one, which is how meshes baked for different kinds of agent are kept apart.
### Return value

Current navigation mask. The default value is 1.
## int getNumLoadedTiles () const

Returns the current number of tiles currently resident in memory. Compared against the total it shows how much of the mesh streaming is keeping around.
### Return value

Current number of loaded tiles.
## int getNumPolygons () const

Returns the current number of polygons in the loaded data. It is the practical measure of how heavy a search over this mesh is.
### Return value

Current number of polygons.
## int getNumTiles () const

Returns the current total number of tiles the mesh is divided into, resident or not.
### Return value

Current number of tiles.
## void setStreamingEnabled ( bool enabled )

Sets a new value indicating if the tiles of the mesh are loaded and unloaded on demand instead of being kept resident as a whole. It is what makes a navigation mesh larger than memory workable, and it needs at least one [invoker](../../../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cpp.md) in the world to decide which tiles are wanted.
### Arguments

- *bool* **enabled** - Set **true** to enable tile streaming for the mesh; **false** - to disable it.

## bool isStreamingEnabled () const

Returns the current value indicating if the tiles of the mesh are loaded and unloaded on demand instead of being kept resident as a whole. It is what makes a navigation mesh larger than memory workable, and it needs at least one [invoker](../../../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cpp.md) in the world to decide which tiles are wanted.
### Return value

**true** if tile streaming for the mesh is enabled ; otherwise **false**.
## float getWalkableArea () const

Returns the current total surface an agent can stand on, in square metres. It is the quickest sanity check after a bake: a value far below what the level looks like usually means the bake mask or the agent size is wrong.
### Return value

Current walkable area, in square metres.
## Event<const Math:: WorldBoundBox &> getEventTilesChanged () const

event triggered when the tiles of the mesh within the reported region have changed, whether because they were rebuilt or because streaming loaded or unloaded them. Agents holding polygon identifiers in that region should re-validate them. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Math::WorldBoundBox & bounds)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TilesChanged event handler
void tileschanged_event_handler(const Math::WorldBoundBox & bounds)
{
	Log::message("\Handling TilesChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections tileschanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventTilesChanged().connect(tileschanged_event_connections, tileschanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventTilesChanged().connect(tileschanged_event_connections, [](const Math::WorldBoundBox & bounds) {
		Log::message("\Handling TilesChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
tileschanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection tileschanged_event_connection;

// subscribe to the TilesChanged event with a handler function keeping the connection
publisher->getEventTilesChanged().connect(tileschanged_event_connection, tileschanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
tileschanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
tileschanged_event_connection.setEnabled(true);

// ...

// remove subscription to the TilesChanged event via the connection
tileschanged_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A TilesChanged event handler implemented as a class member
	void event_handler(const Math::WorldBoundBox & bounds)
	{
		Log::message("\Handling TilesChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventTilesChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId tileschanged_handler_id;

// subscribe to the TilesChanged event with a lambda handler function and keeping connection ID
tileschanged_handler_id = publisher->getEventTilesChanged().connect(e_connections, [](const Math::WorldBoundBox & bounds) {
		Log::message("\Handling TilesChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventTilesChanged().disconnect(tileschanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TilesChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventTilesChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventTilesChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static ExperimentalNavigationMeshPtr create ( )

The ExperimentalNavigationMesh constructor. Creates a static navigation mesh with the default bake settings and no data.
## static Ptr < ExperimentalNavigationMesh > find ( const Ptr < ExperimentalNavigationMeshFilter > & filter )

Returns the navigation mesh that best fits an agent. Among the meshes whose navigation mask matches and whose data was baked for an agent at least as large, the one with the smallest excess is chosen. There is no fallback to a mesh baked for a smaller agent.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.

### Return value

Navigation mesh serving the agent, or NULL if none does.
## static Ptr < ExperimentalNavigationMesh > find ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & point , Math:: Vec3 & ret_point , long long & ret_polygon )

Returns the navigation mesh that fits an agent at a given place, along with the snapped point and its polygon. It answers "where am I and which mesh am I on" in one call, which is what spawning, teleporting, and landing need.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point to look near, in world coordinates.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_point** - Nearest point on the walkable surface.
- *long long &* **ret_polygon** - Polygon under the returned point.

### Return value

Navigation mesh serving the agent at that place, or NULL if none does.
## bool findNearestPoint ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & point , Math:: Vec3 & ret_point )

Snaps a point onto the walkable surface of this mesh. Only the box given by the snap size of the filter is searched, so a point far above or below the surface is not found.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point to snap, in world coordinates.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_point** - Nearest point on the walkable surface.

### Return value

true if a point was found; otherwise, false.
## long long findNearestPolygon ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & point )

Returns the polygon nearest to a point. This is the entry point of the anchor model: the result goes into the anchored forms of the path request and into the teleport method of a corridor.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point to snap, in world coordinates.

### Return value

Polygon nearest to the point, or 0 if there is none.
## bool findPointOutsideObstacles ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & point , Math:: Vec3 & ret_point )

Pushes a point out of any obstacles it is standing inside, staying on the walkable surface. Use it for an agent that ended up inside an obstacle that appeared around it, which no amount of path planning can resolve.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent and the obstacles to consider.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point to push out, in world coordinates.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_point** - Point moved clear of the obstacles.

### Return value

true if the point was moved; otherwise, false.
## bool findRandomPoint ( const Ptr < ExperimentalNavigationMeshFilter > & filter , Math:: Vec3 & ret_point )

Returns a random point on the walkable surface of this mesh, distributed evenly by area. It promises nothing about reachability: the point may sit in a locked room or on an island the agent cannot get to. For spawning and wandering use [findRandomReachablePoint()](#findRandomReachablePoint_ExperimentalNavigationMeshFilter_Vec3_float_Vec3_llong_int) instead.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_point** - Random point on the walkable surface.

### Return value

true if the query succeeded; otherwise, false.
## bool findRandomReachablePoint ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & point , float max_cost , Math:: Vec3 & ret_point , long long start_polygon = 0 )

Returns a random point that is actually reachable from the given one within a cost budget. This is what spawning, wandering, and "run somewhere away from here" need.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point to search around, in world coordinates.
- *float* **max_cost** - Cost budget the point has to be within.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_point** - Random reachable point.
- *long long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int findReachablePoints ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & point , float max_cost , Vector < Math:: Vec3 > & OUT_ret_points , Vector <long long> & OUT_ret_polygons , long long start_polygon = 0 )

Collects every point reachable from the given one within a cost budget. Use it as a candidate generator � for cover positions, patrol targets, or the reachable area of a unit with limited movement.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point to search around, in world coordinates.
- *float* **max_cost** - Cost budget the points have to be within.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)> &* **OUT_ret_points** - Reachable points found. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<long long> &* **OUT_ret_polygons** - Polygons the points lie on. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

Number of points found.
## bool getBoundaryIntersection ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & from , const Math:: Vec3 & to , Math:: Vec3 & ret_point , Math:: vec3 & ret_normal , long long start_polygon = 0 )

Traces a straight segment across the walkable surface and reports where it runs off the edge. It answers "can the agent walk straight there, and if not, where does it stop" without planning a path.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **from** - Start of the segment, in world coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **to** - End of the segment, in world coordinates.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_point** - Point where the segment leaves the walkable surface.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_normal** - Normal of the boundary edge at that point.
- *long long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## bool getNearestBoundary ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & point , float max_radius , Math:: Vec3 & ret_point , Math:: vec3 & ret_normal , float & ret_distance , long long start_polygon = 0 )

Finds the closest edge of the walkable surface around a point. Use it to keep an agent clear of ledges, or to know how much room it has before it falls off.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point to measure from, in world coordinates.
- *float* **max_radius** - Distance to search within, in units.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_point** - Nearest point on the boundary.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_normal** - Normal of the boundary edge, pointing inwards.
- *float &* **ret_distance** - Distance to the boundary, in units.
- *long long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int getPolygonAreaIndex ( long long polygon )

Returns the area a polygon carries.
### Arguments

- *long long* **polygon** - Polygon identifier.

### Return value

Area index of the polygon.
## int getPolygonFlags ( long long polygon )

Returns the flags a polygon carries.
### Arguments

- *long long* **polygon** - Polygon identifier.

### Return value

Flags of the polygon.
## int getPolygons ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: WorldBoundBox & bounds , Vector <long long> & OUT_ret_polygons )

Collects every polygon of this mesh inside a region. Useful for area effects that have to know what walkable ground they cover.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[WorldBoundBox](../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bounds** - Region to collect the polygons in, in world coordinates.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<long long> &* **OUT_ret_polygons** - Polygons found inside the region. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of polygons found.
## bool getSlidePoint ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & from , const Math:: Vec3 & to , Math:: Vec3 & ret_point , long long start_polygon = 0 )

Moves a point towards a target and slides it along the boundary instead of letting it leave the walkable surface. It is the navigation-mesh equivalent of sliding along a wall in a physics collision, and it is what keeps a directly controlled character on the mesh.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **from** - Start of the movement, in world coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **to** - Point the agent is trying to reach, in world coordinates.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_point** - Point the agent actually ends up at.
- *long long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int getSlidePoints ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Vector < Math:: Vec3 > & points , Vector < Math:: Vec3 > & OUT_ret_points , Vector <long long> & OUT_ret_polygons , long long start_polygon = 0 )

Slides a whole polyline along the walkable surface in one call, instead of stepping through it segment by segment.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)> &* **points** - Polyline the agent is trying to follow, in world coordinates.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)> &* **OUT_ret_points** - Points the agent actually passes through. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<long long> &* **OUT_ret_polygons** - Polygons the resulting points lie on. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

Number of points produced.
## void getTriangles ( Vector < Math:: Vec3 > & OUT_ret_vertices , Vector <int> & OUT_ret_indices )

Reads the walkable surface out as a triangle mesh. Meant for drawing the navigation mesh in a custom tool or exporting it; the engine has its own visualizer behind the *navigation_show_mesh* console variable.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)> &* **OUT_ret_vertices** - Vertices of the walkable surface. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_ret_indices** - Triangle indices into the vertex array. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void getTriangles ( Vector < Math:: Vec3 > & OUT_ret_vertices , Vector <int> & OUT_ret_indices , Vector <int> & OUT_ret_areas )

Reads the walkable surface out as a triangle mesh together with the area of every triangle. Use this overload when the areas have to be colored or told apart.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)< Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)> &* **OUT_ret_vertices** - Vertices of the walkable surface. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_ret_indices** - Triangle indices into the vertex array. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_ret_areas** - Area index of every triangle. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool isPointInObstacle ( const Ptr < ExperimentalNavigationMeshFilter > & filter , const Math:: Vec3 & point )

Checks whether a point is standing inside an obstacle. Pair it with [findPointOutsideObstacles()](#findPointOutsideObstacles_ExperimentalNavigationMeshFilter_Vec3_Vec3_int): this one detects the problem, that one fixes it.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)> &* **filter** - Filter describing the agent.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point to test, in world coordinates.

### Return value

true if the point is inside an obstacle the filter accounts for; otherwise, false.
## bool isPolygonValid ( long long polygon )

Checks whether a polygon identifier is still usable. Anything caching identifiers across frames has to call this: after a rebuild or a tile reload a stale identifier can quietly refer to a different polygon.
### Arguments

- *long long* **polygon** - Polygon identifier to check.

### Return value

true if the identifier still refers to a live polygon; otherwise, false.
## bool setMeshPath ( const char * path , int force_load = 0 )

Sets the asset the navigation data is loaded from.
### Arguments

- *const char ** **path** - Path to the navigation mesh asset.
- *int* **force_load** - Load flag.

  - If true is specified, the asset is loaded immediately.
  - If false is specified, only the path is stored.

### Return value

true if the path was set and, when requested, the asset was loaded; otherwise, false.
## bool getMesh ( Mesh ret_mesh ) const

Converts the resident navigation data into a triangle mesh: polygons are triangulated, tile seams are stitched, and the result is welded into a single surface. Only loaded tiles are converted, so what comes out describes the data in memory rather than the whole world.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cpp.md)* **ret_mesh** - Mesh to receive the walkable surface.

### Return value

true if the surface was written to the mesh; otherwise, false.
## void resetBakeMode ( )

Resets the bake mode to its default value.
