# Unigine::ExperimentalNavigationMesh Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


> **Notice:** Not to be confused with the legacy [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_usc.md) class: despite the similar name they are unrelated.


The walkable surface of a world, baked out of scene geometry as convex polygons and split into tiles. Everything else in the navigation system reads it: paths are searched over its polygons, corridors follow bands of them, and avoidance keeps agents inside its boundaries.


Where the legacy navigation classes required the walkable space to be authored by hand, this node derives it from the geometry already in the scene. What goes in is selected by [BakeMask](../../../api/library/pathfinding/class.experimentalnavigationbakesettings_usc.md#BakeMask); how it is turned into polygons is governed by the **Bake** settings; [BakeMode](#BakeMode) decides whether the result is loaded from an asset, carved at runtime, or generated in memory from scratch.


Two families of settings look alike and are worth telling apart. The **Bake** ones describe what the mesh *will* be built with and can be edited at any time. The **Data** ones report what the loaded data was *actually* built with. Queries compare against the second family, so changing a bake setting without rebaking never silently invalidates an agent's assumptions.


## ExperimentalNavigationMesh Class

### Members

## ExperimentalNavigationBakeSettings getBakeSettings () const

Returns the current settings the mesh is baked with. They belong to a separate object shared with the legacy [NavigationMesh](../../../api/library/pathfinding/class.navigationmesh_usc.md) node, so one editor panel drives both. The object lives as long as the node does.
### Return value

Current bake settings of this node.
## void setBakeMode ( int mode )

Sets a new where the navigation data comes from and whether it changes at runtime. One node covers all three cases; the mode can be switched while the application runs.
### Arguments

- *int* **mode** - The mode, one of the [BAKE_MODE_*](#BAKE_MODE_STATIC) values. The default value is [BAKE_MODE_STATIC](#BAKE_MODE_STATIC).

## int getBakeMode () const

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
## int getDataBakeMode () const

Returns the current mode the loaded data was actually produced in. It can differ from the mode set on the node until the mesh is baked again.
### Return value

Current bake mode of the data, one of the [BAKE_MODE_*](#BAKE_MODE_STATIC) values.
## float getDataCellSize () const

Returns the current cell size the loaded data was actually baked with.
### Return value

Current cell size of the data, in units.
## getDataHash () const

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
## getDataVersion () const

Returns the current counter bumped every time the data changes � after a bake, a rebuild, or a tile being streamed in or out. Polygon identifiers stay valid only while it holds still, so anything caching them has to store the version alongside and re-resolve when it moves.
### Return value

Current version of the data.
## int isFileLoaded () const

Returns the current value indicating if the asset file of the mesh is loaded. In [BAKE_MODE_DYNAMIC](#BAKE_MODE_DYNAMIC) it is always false � there is no file, the data is generated in memory.
### Return value

Current the asset file is loaded
## int isNeedBake () const

Returns the current value indicating if the data no longer matches the settings and the geometry it was built from.
### Return value

Current the mesh has to be baked again
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
## void setStreamingEnabled ( int enabled )

Sets a new value indicating if the tiles of the mesh are loaded and unloaded on demand instead of being kept resident as a whole. It is what makes a navigation mesh larger than memory workable, and it needs at least one [invoker](../../../api/library/pathfinding/class.experimentalnavigationmeshinvoker_usc.md) in the world to decide which tiles are wanted.
### Arguments

- *int* **enabled** - The tile streaming for the mesh

## int isStreamingEnabled () const

Returns the current value indicating if the tiles of the mesh are loaded and unloaded on demand instead of being kept resident as a whole. It is what makes a navigation mesh larger than memory workable, and it needs at least one [invoker](../../../api/library/pathfinding/class.experimentalnavigationmeshinvoker_usc.md) in the world to decide which tiles are wanted.
### Return value

Current tile streaming for the mesh
## float getWalkableArea () const

Returns the current total surface an agent can stand on, in square metres. It is the quickest sanity check after a bake: a value far below what the level looks like usually means the bake mask or the agent size is wrong.
### Return value

Current walkable area, in square metres.
## getEventTilesChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## static ExperimentalNavigationMesh ( )

The ExperimentalNavigationMesh constructor. Creates a static navigation mesh with the default bake settings and no data.
## static ExperimentalNavigationMesh find ( ExperimentalNavigationMeshFilter filter )

Returns the navigation mesh that best fits an agent. Among the meshes whose navigation mask matches and whose data was baked for an agent at least as large, the one with the smallest excess is chosen. There is no fallback to a mesh baked for a smaller agent.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.

### Return value

Navigation mesh serving the agent, or NULL if none does.
## static ExperimentalNavigationMesh find ( ExperimentalNavigationMeshFilter filter , Vec3 point , Vec3 ret_point , long ret_polygon )

Returns the navigation mesh that fits an agent at a given place, along with the snapped point and its polygon. It answers "where am I and which mesh am I on" in one call, which is what spawning, teleporting, and landing need.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **point** - Point to look near, in world coordinates.
- *Vec3* **ret_point** - Nearest point on the walkable surface.
- *long* **ret_polygon** - Polygon under the returned point.

### Return value

Navigation mesh serving the agent at that place, or NULL if none does.
## int findNearestPoint ( ExperimentalNavigationMeshFilter filter , Vec3 point , Vec3 ret_point )

Snaps a point onto the walkable surface of this mesh. Only the box given by the snap size of the filter is searched, so a point far above or below the surface is not found.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **point** - Point to snap, in world coordinates.
- *Vec3* **ret_point** - Nearest point on the walkable surface.

### Return value

true if a point was found; otherwise, false.
## long findNearestPolygon ( ExperimentalNavigationMeshFilter filter , Vec3 point )

Returns the polygon nearest to a point. This is the entry point of the anchor model: the result goes into the anchored forms of the path request and into the teleport method of a corridor.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **point** - Point to snap, in world coordinates.

### Return value

Polygon nearest to the point, or 0 if there is none.
## int findPointOutsideObstacles ( ExperimentalNavigationMeshFilter filter , Vec3 point , Vec3 ret_point )

Pushes a point out of any obstacles it is standing inside, staying on the walkable surface. Use it for an agent that ended up inside an obstacle that appeared around it, which no amount of path planning can resolve.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent and the obstacles to consider.
- *Vec3* **point** - Point to push out, in world coordinates.
- *Vec3* **ret_point** - Point moved clear of the obstacles.

### Return value

true if the point was moved; otherwise, false.
## int findRandomPoint ( ExperimentalNavigationMeshFilter filter , Vec3 ret_point )

Returns a random point on the walkable surface of this mesh, distributed evenly by area. It promises nothing about reachability: the point may sit in a locked room or on an island the agent cannot get to. For spawning and wandering use [findRandomReachablePoint()](#findRandomReachablePoint_ExperimentalNavigationMeshFilter_Vec3_float_Vec3_llong_int) instead.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **ret_point** - Random point on the walkable surface.

### Return value

true if the query succeeded; otherwise, false.
## int findRandomReachablePoint ( ExperimentalNavigationMeshFilter filter , Vec3 point , float max_cost , Vec3 ret_point , long start_polygon = 0 )

Returns a random point that is actually reachable from the given one within a cost budget. This is what spawning, wandering, and "run somewhere away from here" need.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **point** - Point to search around, in world coordinates.
- *float* **max_cost** - Cost budget the point has to be within.
- *Vec3* **ret_point** - Random reachable point.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int findReachablePoints ( ExperimentalNavigationMeshFilter filter , Vec3 point , float max_cost , Vec3[] OUT_ret_points , long[] OUT_ret_polygons , long start_polygon = 0 )

Collects every point reachable from the given one within a cost budget. Use it as a candidate generator � for cover positions, patrol targets, or the reachable area of a unit with limited movement.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **point** - Point to search around, in world coordinates.
- *float* **max_cost** - Cost budget the points have to be within.
- *Vec3[]* **OUT_ret_points** - Reachable points found. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long[]* **OUT_ret_polygons** - Polygons the points lie on. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

Number of points found.
## int getBoundaryIntersection ( ExperimentalNavigationMeshFilter filter , Vec3 from , Vec3 to , Vec3 ret_point , vec3 ret_normal , long start_polygon = 0 )

Traces a straight segment across the walkable surface and reports where it runs off the edge. It answers "can the agent walk straight there, and if not, where does it stop" without planning a path.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **from** - Start of the segment, in world coordinates.
- *Vec3* **to** - End of the segment, in world coordinates.
- *Vec3* **ret_point** - Point where the segment leaves the walkable surface.
- *vec3* **ret_normal** - Normal of the boundary edge at that point.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int getNearestBoundary ( ExperimentalNavigationMeshFilter filter , Vec3 point , float max_radius , Vec3 ret_point , vec3 ret_normal , float ret_distance , long start_polygon = 0 )

Finds the closest edge of the walkable surface around a point. Use it to keep an agent clear of ledges, or to know how much room it has before it falls off.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **point** - Point to measure from, in world coordinates.
- *float* **max_radius** - Distance to search within, in units.
- *Vec3* **ret_point** - Nearest point on the boundary.
- *vec3* **ret_normal** - Normal of the boundary edge, pointing inwards.
- *float* **ret_distance** - Distance to the boundary, in units.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int getPolygonAreaIndex ( long polygon )

Returns the area a polygon carries.
### Arguments

- *long* **polygon** - Polygon identifier.

### Return value

Area index of the polygon.
## int getPolygonFlags ( long polygon )

Returns the flags a polygon carries.
### Arguments

- *long* **polygon** - Polygon identifier.

### Return value

Flags of the polygon.
## int getPolygons ( ExperimentalNavigationMeshFilter filter , WorldBoundBox bounds , long[] OUT_ret_polygons )

Collects every polygon of this mesh inside a region. Useful for area effects that have to know what walkable ground they cover.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *WorldBoundBox* **bounds** - Region to collect the polygons in, in world coordinates.
- *long[]* **OUT_ret_polygons** - Polygons found inside the region. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of polygons found.
## int getSlidePoint ( ExperimentalNavigationMeshFilter filter , Vec3 from , Vec3 to , Vec3 ret_point , long start_polygon = 0 )

Moves a point towards a target and slides it along the boundary instead of letting it leave the walkable surface. It is the navigation-mesh equivalent of sliding along a wall in a physics collision, and it is what keeps a directly controlled character on the mesh.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **from** - Start of the movement, in world coordinates.
- *Vec3* **to** - Point the agent is trying to reach, in world coordinates.
- *Vec3* **ret_point** - Point the agent actually ends up at.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

true if the query succeeded; otherwise, false.
## int getSlidePoints ( ExperimentalNavigationMeshFilter filter , Vec3[] points , Vec3[] OUT_ret_points , long[] OUT_ret_polygons , long start_polygon = 0 )

Slides a whole polyline along the walkable surface in one call, instead of stepping through it segment by segment.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3[]* **points** - Polyline the agent is trying to follow, in world coordinates.
- *Vec3[]* **OUT_ret_points** - Points the agent actually passes through. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long[]* **OUT_ret_polygons** - Polygons the resulting points lie on. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *long* **start_polygon** - Polygon to start the search from, when it is already known. 0 means the point is snapped by position.

### Return value

Number of points produced.
## void getTriangles ( Vec3[] OUT_ret_vertices , int[] OUT_ret_indices , int[] OUT_ret_areas )

Reads the walkable surface out as a triangle mesh together with the area of every triangle. Use this overload when the areas have to be colored or told apart.
### Arguments

- *Vec3[]* **OUT_ret_vertices** - Vertices of the walkable surface. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **OUT_ret_indices** - Triangle indices into the vertex array. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int[]* **OUT_ret_areas** - Area index of every triangle. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## int isPointInObstacle ( ExperimentalNavigationMeshFilter filter , Vec3 point )

Checks whether a point is standing inside an obstacle. Pair it with [findPointOutsideObstacles()](#findPointOutsideObstacles_ExperimentalNavigationMeshFilter_Vec3_Vec3_int): this one detects the problem, that one fixes it.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - Filter describing the agent.
- *Vec3* **point** - Point to test, in world coordinates.

### Return value

true if the point is inside an obstacle the filter accounts for; otherwise, false.
## int isPolygonValid ( long polygon )

Checks whether a polygon identifier is still usable. Anything caching identifiers across frames has to call this: after a rebuild or a tile reload a stale identifier can quietly refer to a different polygon.
### Arguments

- *long* **polygon** - Polygon identifier to check.

### Return value

true if the identifier still refers to a live polygon; otherwise, false.
## int setMeshPath ( string path , int force_load = 0 )

Sets the asset the navigation data is loaded from.
### Arguments

- *string* **path** - Path to the navigation mesh asset.
- *int* **force_load** - Load flag.

  - If true is specified, the asset is loaded immediately.
  - If false is specified, only the path is stored.

### Return value

true if the path was set and, when requested, the asset was loaded; otherwise, false.
## bool getMesh ( Mesh ret_mesh )

Converts the resident navigation data into a triangle mesh: polygons are triangulated, tile seams are stitched, and the result is welded into a single surface. Only loaded tiles are converted, so what comes out describes the data in memory rather than the whole world.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **ret_mesh** - Mesh to receive the walkable surface.

### Return value

true if the surface was written to the mesh; otherwise, false.
## void resetBakeMode ( )

Resets the bake mode to its default value.
