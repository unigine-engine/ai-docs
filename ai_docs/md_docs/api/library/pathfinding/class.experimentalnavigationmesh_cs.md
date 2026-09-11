# Unigine::ExperimentalNavigationMesh Class (CS)

**Inherits from:** Node


> **Notice:** Not to be confused with the legacy [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cs.md) class: despite the similar name they are unrelated.


The walkable surface of a world, baked out of scene geometry as convex polygons and split into tiles. Everything else in the navigation system reads it: paths are searched over its polygons, corridors follow bands of them, and avoidance keeps agents inside its boundaries.


Where the legacy navigation classes required the walkable space to be authored by hand, this node derives it from the geometry already in the scene. What goes in is selected by [BakeMask](../../../api/library/pathfinding/class.experimentalnavigationbakesettings_cs.md#BakeMask); how it is turned into polygons is governed by the **Bake** settings; [BakeMode](#BakeMode) decides whether the result is loaded from an asset, carved at runtime, or generated in memory from scratch.


Two families of settings look alike and are worth telling apart. The **Bake** ones describe what the mesh *will* be built with and can be edited at any time. The **Data** ones report what the loaded data was *actually* built with. Queries compare against the second family, so changing a bake setting without rebaking never silently invalidates an agent's assumptions.


## ExperimentalNavigationMesh Class

### Enums

## BAKE_MODE

| Name | Description |
|---|---|
| **STATIC** = 0 | The navigation data is loaded from the asset and never changes. The cheapest mode, and the right one for a level whose walkable space is fixed. |
| **STATIC_CARVE** = 1 | The navigation data is loaded from the asset, and runtime obstacles are carved out of it. It suits a fixed level with things that move through it � a lowered barrier, a parked vehicle, rubble from a collapse. |
| **DYNAMIC** = 2 | The navigation data is generated in memory from the current geometry and never touches an asset. Meant for procedurally built levels, where there is nothing to bake beforehand. |

### Properties

## 🔒︎ ExperimentalNavigationBakeSettings BakeSettings

The settings the mesh is baked with. They belong to a separate object shared with the legacy [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_cs.md) node, so one editor panel drives both. The object lives as long as the node does.
## ExperimentalNavigationMesh.BAKE_MODE BakeMode

The where the navigation data comes from and whether it changes at runtime. One node covers all three cases; the mode can be switched while the application runs.
## 🔒︎ float DataAgentHeight

The agent height the loaded data was actually baked with. Queries are matched against this value, not against the bake setting.
## 🔒︎ float DataAgentRadius

The agent radius the loaded data was actually baked with. A query is served by this mesh only when the radius in its filter does not exceed this value.
## 🔒︎ ExperimentalNavigationMesh.BAKE_MODE DataBakeMode

The mode the loaded data was actually produced in. It can differ from the mode set on the node until the mesh is baked again.
## 🔒︎ float DataCellSize

The cell size the loaded data was actually baked with.
## 🔒︎ ullong DataHash

The hash of the inputs the loaded data was produced from. Comparing it against the current settings and geometry is how the engine tells whether the mesh is still up to date.
## 🔒︎ float DataMaxSlopeAngle

The maximum slope angle the loaded data was actually baked with.
## 🔒︎ float DataMaxStepHeight

The maximum step height the loaded data was actually baked with. A query asks for no more than it can climb, so this value is matched against the step limit of the filter.
## 🔒︎ int DataTileResolution

The tile resolution in cells the loaded data was actually baked with.
## 🔒︎ float DataTileWorldSize

The world size of one tile of the loaded data, in units.
## 🔒︎ ullong DataVersion

The counter bumped every time the data changes � after a bake, a rebuild, or a tile being streamed in or out. Polygon identifiers stay valid only while it holds still, so anything caching them has to store the version alongside and re-resolve when it moves.
## 🔒︎ bool IsFileLoaded

The value indicating if the asset file of the mesh is loaded. In [BAKE_MODE_DYNAMIC](#BAKE_MODE_DYNAMIC) it is always false � there is no file, the data is generated in memory.
## 🔒︎ bool IsNeedBake

The value indicating if the data no longer matches the settings and the geometry it was built from.
## 🔒︎ string MeshPath

The Returns the path to the asset the navigation data is loaded from.
## int NavigationMask

The mask that decides which queries this mesh serves. A query uses the mesh only when the navigation mask of its filter shares at least one bit with this one, which is how meshes baked for different kinds of agent are kept apart.
## 🔒︎ int NumLoadedTiles

The number of tiles currently resident in memory. Compared against the total it shows how much of the mesh streaming is keeping around.
## 🔒︎ int NumPolygons

The number of polygons in the loaded data. It is the practical measure of how heavy a search over this mesh is.
## 🔒︎ int NumTiles

The total number of tiles the mesh is divided into, resident or not.
## bool StreamingEnabled

The value indicating if the tiles of the mesh are loaded and unloaded on demand instead of being kept resident as a whole. It is what makes a navigation mesh larger than memory workable, and it needs at least one [invoker](../../../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cs.md) in the world to decide which tiles are wanted.
## 🔒︎ float WalkableArea

The total surface an agent can stand on, in square metres. It is the quickest sanity check after a bake: a value far below what the level looks like usually means the bake mask or the agent size is wrong.
## 🔒︎ Event< WorldBoundBox > EventTilesChanged

The event triggered when the tiles of the mesh within the reported region have changed, whether because they were rebuilt or because streaming loaded or unloaded them. Agents holding polygon identifiers in that region should re-validate them. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WorldBoundBox bounds)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TilesChanged event handler
void tileschanged_event_handler(WorldBoundBox bounds)
{
	Log.Message("\Handling TilesChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections tileschanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventTilesChanged.Connect(tileschanged_event_connections, tileschanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventTilesChanged.Connect(tileschanged_event_connections, (WorldBoundBox bounds) => {
		Log.Message("Handling TilesChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
tileschanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TilesChanged event with a handler function
publisher.EventTilesChanged.Connect(tileschanged_event_handler);

// remove subscription to the TilesChanged event later by the handler function
publisher.EventTilesChanged.Disconnect(tileschanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection tileschanged_event_connection;

// subscribe to the TilesChanged event with a lambda handler function and keeping the connection
tileschanged_event_connection = publisher.EventTilesChanged.Connect((WorldBoundBox bounds) => {
		Log.Message("Handling TilesChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
tileschanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
tileschanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
tileschanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TilesChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventTilesChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventTilesChanged.Enabled = true;

```

</details>

### Members

---

## ExperimentalNavigationMesh ( )

The ExperimentalNavigationMesh constructor. Creates a static navigation mesh with the default bake settings and no data.
## static ExperimentalNavigationMesh Find ( ExperimentalNavigationMeshFilter filter )

Returns the navigation mesh that best fits an agent. Among the meshes whose navigation mask matches and whose data was baked for an agent at least as large, the one with the smallest excess is chosen. There is no fallback to a mesh baked for a smaller agent.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.

### Return value

Navigation mesh serving the agent, or NULL if none does.
## static ExperimentalNavigationMesh Find ( ExperimentalNavigationMeshFilter filter , vec3 point , out Vec3 ret_point , out long ret_polygon )

Returns the navigation mesh that fits an agent at a given place, along with the snapped point and its polygon. It answers "where am I and which mesh am I on" in one call, which is what spawning, teleporting, and landing need.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3* **point** - Point to look near, in world coordinates.
- *out Vec3* **ret_point** - Nearest point on the walkable surface.
- *out long* **ret_polygon** - Polygon under the returned point.

### Return value

Navigation mesh serving the agent at that place, or NULL if none does.
## bool FindNearestPoint ( ExperimentalNavigationMeshFilter filter , vec3 point , out Vec3 ret_point )

Snaps a point onto the walkable surface of this mesh. Only the box given by the snap size of the filter is searched, so a point far above or below the surface is not found.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3* **point** - Point to snap, in world coordinates.
- *out Vec3* **ret_point** - Nearest point on the walkable surface.

### Return value

true if a point was found; otherwise, false.
## long FindNearestPolygon ( ExperimentalNavigationMeshFilter filter , vec3 point )

Returns the polygon nearest to a point. This is the entry point of the anchor model: the result goes into the anchored forms of the path request and into the teleport method of a corridor.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3* **point** - Point to snap, in world coordinates.

### Return value

Polygon nearest to the point, or 0 if there is none.
## bool FindPointOutsideObstacles ( ExperimentalNavigationMeshFilter filter , vec3 point , out Vec3 ret_point )

Pushes a point out of any obstacles it is standing inside, staying on the walkable surface. Use it for an agent that ended up inside an obstacle that appeared around it, which no amount of path planning can resolve.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent and the obstacles to consider.
- *vec3* **point** - Point to push out, in world coordinates.
- *out Vec3* **ret_point** - Point moved clear of the obstacles.

### Return value

true if the point was moved; otherwise, false.
## bool FindRandomPoint ( ExperimentalNavigationMeshFilter filter , out Vec3 ret_point )

Returns a random point on the walkable surface of this mesh, distributed evenly by area. It promises nothing about reachability: the point may sit in a locked room or on an island the agent cannot get to. For spawning and wandering use [findRandomReachablePoint()](#findRandomReachablePoint_ExperimentalNavigationMeshFilter_Vec3_float_Vec3_llong_int) instead.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *out Vec3* **ret_point** - Random point on the walkable surface.

### Return value

true if the query succeeded; otherwise, false.
## bool FindRandomReachablePoint ( ExperimentalNavigationMeshFilter filter , vec3 point , float max_cost , out Vec3 ret_point , long start_polygon = 0 )

Returns a random point that is actually reachable from the given one within a cost budget. This is what spawning, wandering, and "run somewhere away from here" need.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3* **point** - Point to search around, in world coordinates.
- *float* **max_cost** - Cost budget the point has to be within.
- *out Vec3* **ret_point** - Random reachable point.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int FindReachablePoints ( ExperimentalNavigationMeshFilter filter , vec3 point , float max_cost , vec3[] OUT_ret_points , long[] OUT_ret_polygons , long start_polygon = 0 )

Collects every point reachable from the given one within a cost budget. Use it as a candidate generator � for cover positions, patrol targets, or the reachable area of a unit with limited movement.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3* **point** - Point to search around, in world coordinates.
- *float* **max_cost** - Cost budget the points have to be within.
- *vec3[]* **OUT_ret_points** - Reachable points found. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long[]* **OUT_ret_polygons** - Polygons the points lie on. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

Number of points found.
## bool GetBoundaryIntersection ( ExperimentalNavigationMeshFilter filter , vec3 from , vec3 to , out Vec3 ret_point , out vec3 ret_normal , long start_polygon = 0 )

Traces a straight segment across the walkable surface and reports where it runs off the edge. It answers "can the agent walk straight there, and if not, where does it stop" without planning a path.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3* **from** - Start of the segment, in world coordinates.
- *vec3* **to** - End of the segment, in world coordinates.
- *out Vec3* **ret_point** - Point where the segment leaves the walkable surface.
- *out vec3* **ret_normal** - Normal of the boundary edge at that point.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## bool GetNearestBoundary ( ExperimentalNavigationMeshFilter filter , vec3 point , float max_radius , out Vec3 ret_point , out vec3 ret_normal , out float ret_distance , long start_polygon = 0 )

Finds the closest edge of the walkable surface around a point. Use it to keep an agent clear of ledges, or to know how much room it has before it falls off.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3* **point** - Point to measure from, in world coordinates.
- *float* **max_radius** - Distance to search within, in units.
- *out Vec3* **ret_point** - Nearest point on the boundary.
- *out vec3* **ret_normal** - Normal of the boundary edge, pointing inwards.
- *out float* **ret_distance** - Distance to the boundary, in units.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int GetPolygonAreaIndex ( long polygon )

Returns the area a polygon carries.
### Arguments

- *long* **polygon** - Polygon identifier.

### Return value

Area index of the polygon.
## int GetPolygonFlags ( long polygon )

Returns the flags a polygon carries.
### Arguments

- *long* **polygon** - Polygon identifier.

### Return value

Flags of the polygon.
## int GetPolygons ( ExperimentalNavigationMeshFilter filter , WorldBoundBox bounds , long[] OUT_ret_polygons )

Collects every polygon of this mesh inside a region. Useful for area effects that have to know what walkable ground they cover.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *[WorldBoundBox](../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bounds** - Region to collect the polygons in, in world coordinates.
- *long[]* **OUT_ret_polygons** - Polygons found inside the region. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of polygons found.
## bool GetSlidePoint ( ExperimentalNavigationMeshFilter filter , vec3 from , vec3 to , out Vec3 ret_point , long start_polygon = 0 )

Moves a point towards a target and slides it along the boundary instead of letting it leave the walkable surface. It is the navigation-mesh equivalent of sliding along a wall in a physics collision, and it is what keeps a directly controlled character on the mesh.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3* **from** - Start of the movement, in world coordinates.
- *vec3* **to** - Point the agent is trying to reach, in world coordinates.
- *out Vec3* **ret_point** - Point the agent actually ends up at.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int GetSlidePoints ( ExperimentalNavigationMeshFilter filter , vec3[] points , vec3[] OUT_ret_points , long[] OUT_ret_polygons , long start_polygon = 0 )

Slides a whole polyline along the walkable surface in one call, instead of stepping through it segment by segment.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3[]* **points** - Polyline the agent is trying to follow, in world coordinates.
- *vec3[]* **OUT_ret_points** - Points the agent actually passes through. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long[]* **OUT_ret_polygons** - Polygons the resulting points lie on. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

Number of points produced.
## void GetTriangles ( vec3[] OUT_ret_vertices , int[] OUT_ret_indices )

Reads the walkable surface out as a triangle mesh. Meant for drawing the navigation mesh in a custom tool or exporting it; the engine has its own visualizer behind the *navigation_show_mesh* console variable.
### Arguments

- *vec3[]* **OUT_ret_vertices** - Vertices of the walkable surface. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **OUT_ret_indices** - Triangle indices into the vertex array. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void GetTriangles ( vec3[] OUT_ret_vertices , int[] OUT_ret_indices , int[] OUT_ret_areas )

Reads the walkable surface out as a triangle mesh together with the area of every triangle. Use this overload when the areas have to be colored or told apart.
### Arguments

- *vec3[]* **OUT_ret_vertices** - Vertices of the walkable surface. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **OUT_ret_indices** - Triangle indices into the vertex array. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **OUT_ret_areas** - Area index of every triangle. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool IsPointInObstacle ( ExperimentalNavigationMeshFilter filter , vec3 point )

Checks whether a point is standing inside an obstacle. Pair it with [findPointOutsideObstacles()](#findPointOutsideObstacles_ExperimentalNavigationMeshFilter_Vec3_Vec3_int): this one detects the problem, that one fixes it.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* **filter** - Filter describing the agent.
- *vec3* **point** - Point to test, in world coordinates.

### Return value

true if the point is inside an obstacle the filter accounts for; otherwise, false.
## bool IsPolygonValid ( long polygon )

Checks whether a polygon identifier is still usable. Anything caching identifiers across frames has to call this: after a rebuild or a tile reload a stale identifier can quietly refer to a different polygon.
### Arguments

- *long* **polygon** - Polygon identifier to check.

### Return value

true if the identifier still refers to a live polygon; otherwise, false.
## bool SetMeshPath ( string path , bool force_load = 0 )

Sets the asset the navigation data is loaded from.
### Arguments

- *string* **path** - Path to the navigation mesh asset.
- *bool* **force_load** - Load flag.

  - If true is specified, the asset is loaded immediately.
  - If false is specified, only the path is stored.

### Return value

true if the path was set and, when requested, the asset was loaded; otherwise, false.
## bool GetMesh ( Mesh ret_mesh )

Converts the resident navigation data into a triangle mesh: polygons are triangulated, tile seams are stitched, and the result is welded into a single surface. Only loaded tiles are converted, so what comes out describes the data in memory rather than the whole world.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **ret_mesh** - Mesh to receive the walkable surface.

### Return value

true if the surface was written to the mesh; otherwise, false.
## void ResetBakeMode ( )

Resets the bake mode to its default value.
