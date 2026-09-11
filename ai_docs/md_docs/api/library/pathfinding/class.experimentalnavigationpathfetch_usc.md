# Unigine::ExperimentalNavigationPathFetch Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


A single path request. It carries the two endpoints, the [filter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md) describing the agent, and the budgets the search may spend; once it completes, the result is taken out as an [ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md). A fetch is a one-shot promise with a lifecycle, which is why the reusable per-agent settings live in the filter and not here.


Requests run either synchronously via [fetchForce()](#fetchForce_int) on the calling thread, or on workers via [fetchAsync()](#fetchAsync_void) with [EventReady](#EventReady) reporting completion. Both have batch versions that take many fetches at once � sending a whole squad in one call is cheaper than sending each agent separately.


Endpoints can be given as bare world positions, in which case the engine snaps them onto a navigation mesh, or as a mesh, polygon and position triple when the anchor is already known from an earlier query. The second form skips the snap and rules out the ambiguity of a point that sits between two overlapping meshes.


## ExperimentalNavigationPathFetch Class

### Members

## void setFilter ( ExperimentalNavigationMeshFilter filter )

Sets a new filter describing the agent the path is requested for. It decides which navigation meshes are eligible, which polygons are passable, and what each area costs.
### Arguments

- *[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_usc.md)* **filter** - The filter used by the request.

## ExperimentalNavigationMeshFilter getFilter () const

Returns the current filter describing the agent the path is requested for. It decides which navigation meshes are eligible, which polygons are passable, and what each area costs.
### Return value

Current filter used by the request.
## Vec3 getFrom () const

Returns the start point of the request in world coordinates.
### Return value

start point of the request.
## ExperimentalNavigationMesh getFromNavigationMesh () const

Returns the navigation mesh the start point is anchored to, if the anchor was given explicitly.
### Return value

navigation mesh of the start anchor, or NULL if the start point is resolved by snapping.
## long getFromPolygon () const

Returns the polygon the start point is anchored to, if the anchor was given explicitly.
### Return value

polygon of the start anchor, or 0 if the start point is resolved by snapping.
## void setHeuristicScale ( float scale )

Sets a new scale applied to the distance heuristic of the search. Values below 1 keep the heuristic admissible and the result optimal; raising it makes the search greedier and faster at the price of a longer route.
### Arguments

- *float* **scale** - The heuristic scale. The default value is 0.999.

## float getHeuristicScale () const

Returns the current scale applied to the distance heuristic of the search. Values below 1 keep the heuristic admissible and the result optimal; raising it makes the search greedier and faster at the price of a longer route.
### Return value

Current heuristic scale. The default value is 0.999.
## int isFetching () const

Returns the current value indicating if the request is currently being processed.
### Return value

Current the request has been started and has not finished yet
## int isReady () const

Returns the current value indicating if the result of the request can be taken.
### Return value

Current the result is ready to be taken
## void setMaxCost ( float cost )

Sets a new cost budget of the search. When the accumulated cost exceeds it, the search stops and the path comes back partial with [FAILURE_COST_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#FAILURE_COST_LIMIT).
### Arguments

- *float* **cost** - The maximum cost. The default value is 0, which means no cost limit.

## float getMaxCost () const

Returns the current cost budget of the search. When the accumulated cost exceeds it, the search stops and the path comes back partial with [FAILURE_COST_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#FAILURE_COST_LIMIT).
### Return value

Current maximum cost. The default value is 0, which means no cost limit.
## void setMaxSearchNodes ( int nodes )

Sets a new node budget of the search. When it is exhausted, the search stops and the path comes back partial with [FAILURE_SEARCH_NODES_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#FAILURE_SEARCH_NODES_LIMIT). It bounds the cost of a single request on a large navigation mesh.
### Arguments

- *int* **nodes** - The maximum number of search nodes. The default value is 2048.

## int getMaxSearchNodes () const

Returns the current node budget of the search. When it is exhausted, the search stops and the path comes back partial with [FAILURE_SEARCH_NODES_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#FAILURE_SEARCH_NODES_LIMIT). It bounds the cost of a single request on a large navigation mesh.
### Return value

Current maximum number of search nodes. The default value is 2048.
## void setNavigationMesh ( ExperimentalNavigationMesh mesh )

Sets a new navigation mesh the search is restricted to. When it is set, the eligible meshes are not looked up by the filter and the search runs on this mesh alone.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md)* **mesh** - The navigation mesh of the request, or NULL if the mesh is chosen by the filter.

## ExperimentalNavigationMesh getNavigationMesh () const

Returns the current navigation mesh the search is restricted to. When it is set, the eligible meshes are not looked up by the filter and the search runs on this mesh alone.
### Return value

Current navigation mesh of the request, or NULL if the mesh is chosen by the filter.
## int getNumExcludeNavigationMeshes () const

Returns the current number of navigation meshes this request skips.
### Return value

Current number of excluded navigation meshes.
## void setPriority ( int priority )

Sets a new priority of the request in the asynchronous queue. Higher-priority requests are taken by the workers first; the value has no effect on synchronous calls.
### Arguments

- *int* **priority** - The priority, one of the [PRIORITY_*](#PRIORITY_LOW) values. The default value is [PRIORITY_NORMAL](#PRIORITY_NORMAL).

## int getPriority () const

Returns the current priority of the request in the asynchronous queue. Higher-priority requests are taken by the workers first; the value has no effect on synchronous calls.
### Return value

Current priority, one of the [PRIORITY_*](#PRIORITY_LOW) values. The default value is [PRIORITY_NORMAL](#PRIORITY_NORMAL).
## void setStraightMode ( int mode )

Sets a new rule that decides where the straightened path gets its points. It trades the number of points against how much the agent knows about what it walks over.
### Arguments

- *int* **mode** - The straightening mode, one of the [STRAIGHT_MODE_*](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#STRAIGHT_MODE_CORNERS) values of [ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md). The default value is [STRAIGHT_MODE_AREA_CROSSINGS](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#STRAIGHT_MODE_AREA_CROSSINGS).

## int getStraightMode () const

Returns the current rule that decides where the straightened path gets its points. It trades the number of points against how much the agent knows about what it walks over.
### Return value

Current straightening mode, one of the [STRAIGHT_MODE_*](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#STRAIGHT_MODE_CORNERS) values of [ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md). The default value is [STRAIGHT_MODE_AREA_CROSSINGS](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#STRAIGHT_MODE_AREA_CROSSINGS).
## Vec3 getTo () const

Returns the target point of the request in world coordinates.
### Return value

target point of the request.
## ExperimentalNavigationMesh getToNavigationMesh () const

Returns the navigation mesh the target point is anchored to, if the anchor was given explicitly.
### Return value

navigation mesh of the target anchor, or NULL if the target point is resolved by snapping.
## long getToPolygon () const

Returns the polygon the target point is anchored to, if the anchor was given explicitly.
### Return value

polygon of the target anchor, or 0 if the target point is resolved by snapping.
## Event<> getEventReady () const

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

## static ExperimentalNavigationPathFetch ( )

The ExperimentalNavigationPathFetch constructor. Creates an empty request with the default budgets.
## void addExcludeNavigationMesh ( ExperimentalNavigationMesh navigation_mesh )

Adds a navigation mesh that this request must not use, even when the filter makes it eligible.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md)* **navigation_mesh** - Navigation mesh to be skipped.

## void clearExcludeNavigationMeshes ( )

Empties the list of the navigation meshes this request skips.
## void fetchAsync ( )

Queues the request for the workers and returns immediately. Completion is reported by [EventReady](#EventReady) and by [IsReady](#IsReady).
## static void fetchAsync ( ExperimentalNavigationPathFetch [] fetches )

Queues a batch of requests for the workers at once. Sending a group of agents in a single call spreads them over the workers better than queueing each request separately.
### Arguments

- *[ExperimentalNavigationPathFetch](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_usc.md)[]* **fetches** - Requests to be queued.

## void fetchAsync ( Vec3 from , Vec3 to )

Sets both endpoints and queues the request for the workers in one call.
### Arguments

- *Vec3* **from** - Start point in world coordinates.
- *Vec3* **to** - Target point in world coordinates.

## int fetchForce ( )

Runs the request on the calling thread and returns when it is finished. A partial path counts as a success � inspect the status of the path to tell the cases apart.
### Return value

true if a path was built; otherwise, false.
## static void fetchForce ( ExperimentalNavigationPathFetch [] fetches )

Runs a batch of requests and returns when all of them are finished. Each request keeps its own result, which is taken from it individually.
### Arguments

- *[ExperimentalNavigationPathFetch](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_usc.md)[]* **fetches** - Requests to be executed.

## int fetchForce ( Vec3 from , Vec3 to )

Sets both endpoints and runs the request on the calling thread in one call.
### Arguments

- *Vec3* **from** - Start point in world coordinates.
- *Vec3* **to** - Target point in world coordinates.

### Return value

true if a path was built; otherwise, false.
## ExperimentalNavigationMesh getExcludeNavigationMesh ( int num )

Returns a navigation mesh from the exclusion list of the request.
### Arguments

- *int* **num** - Number of the navigation mesh in the exclusion list.

### Return value

Excluded navigation mesh.
## void removeExcludeNavigationMesh ( ExperimentalNavigationMesh navigation_mesh )

Removes a navigation mesh from the list of the meshes this request skips.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md)* **navigation_mesh** - Navigation mesh to be made eligible again.

## void setFrom ( Vec3 from )

Sets the start point of the request. The point is snapped onto a navigation mesh when the request runs; if the snap finds nothing, the path fails with [FAILURE_START_OUTSIDE](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#FAILURE_START_OUTSIDE).
### Arguments

- *Vec3* **from** - Start point in world coordinates.

## void setFrom ( ExperimentalNavigationMesh navigation_mesh , long polygon , Vec3 from )

Sets the start point together with the anchor it lies on, skipping the snap. Use it when the anchor is already known from an earlier query � this also removes the ambiguity of a point that sits between two overlapping navigation meshes.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md)* **navigation_mesh** - Navigation mesh the start polygon belongs to.
- *long* **polygon** - Start polygon.
- *Vec3* **from** - Start point in world coordinates.

## void setTo ( Vec3 to )

Sets the target point of the request. The point is snapped onto a navigation mesh when the request runs; if the snap finds nothing, the path fails with [FAILURE_TARGET_OUTSIDE](../../../api/library/pathfinding/class.experimentalnavigationpath_usc.md#FAILURE_TARGET_OUTSIDE).
### Arguments

- *Vec3* **to** - Target point in world coordinates.

## void setTo ( ExperimentalNavigationMesh navigation_mesh , long polygon , Vec3 to )

Sets the target point together with the anchor it lies on, skipping the snap.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_usc.md)* **navigation_mesh** - Navigation mesh the target polygon belongs to.
- *long* **polygon** - Target polygon.
- *Vec3* **to** - Target point in world coordinates.

## ExperimentalNavigationPath takePath ( )

Takes the result out of the request. The request keeps no copy afterwards, so the path must be taken once and kept by the caller.
### Return value

Path produced by the request. The caller owns it from this moment on.
## void waitForce ( )

Blocks the calling thread until an asynchronous request finishes. Returns immediately if nothing is running.
