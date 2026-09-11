# Unigine::ExperimentalNavigationPathFetch Class (CS)


A single path request. It carries the two endpoints, the [filter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md) describing the agent, and the budgets the search may spend; once it completes, the result is taken out as an [ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_cs.md). A fetch is a one-shot promise with a lifecycle, which is why the reusable per-agent settings live in the filter and not here.


Requests run either synchronously via [fetchForce()](#fetchForce_int) on the calling thread, or on workers via [fetchAsync()](#fetchAsync_void) with [EventReady](#EventReady) reporting completion. Both have batch versions that take many fetches at once � sending a whole squad in one call is cheaper than sending each agent separately.


Endpoints can be given as bare world positions, in which case the engine snaps them onto a navigation mesh, or as a mesh, polygon and position triple when the anchor is already known from an earlier query. The second form skips the snap and rules out the ambiguity of a point that sits between two overlapping meshes.


## ExperimentalNavigationPathFetch Class

### Enums

## PRIORITY

| Name | Description |
|---|---|
| **LOW** = 0 | The request waits until no request of a higher priority is queued. |
| **NORMAL** = 1 | Default priority. |
| **HIGH** = 2 | The request is taken by the workers before the normal and low ones. |

### Properties

## ExperimentalNavigationMeshFilter Filter

The filter describing the agent the path is requested for. It decides which navigation meshes are eligible, which polygons are passable, and what each area costs.
## 🔒︎ vec3 From

The Returns the start point of the request in world coordinates.
## 🔒︎ ExperimentalNavigationMesh FromNavigationMesh

The Returns the navigation mesh the start point is anchored to, if the anchor was given explicitly.
## 🔒︎ long FromPolygon

The Returns the polygon the start point is anchored to, if the anchor was given explicitly.
## float HeuristicScale

The scale applied to the distance heuristic of the search. Values below 1 keep the heuristic admissible and the result optimal; raising it makes the search greedier and faster at the price of a longer route.
## 🔒︎ bool IsFetching

The value indicating if the request is currently being processed.
## 🔒︎ bool IsReady

The value indicating if the result of the request can be taken.
## float MaxCost

The cost budget of the search. When the accumulated cost exceeds it, the search stops and the path comes back partial with [FAILURE_COST_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_cs.md#FAILURE_COST_LIMIT).
## int MaxSearchNodes

The node budget of the search. When it is exhausted, the search stops and the path comes back partial with [FAILURE_SEARCH_NODES_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_cs.md#FAILURE_SEARCH_NODES_LIMIT). It bounds the cost of a single request on a large navigation mesh.
## ExperimentalNavigationMesh NavigationMesh

The navigation mesh the search is restricted to. When it is set, the eligible meshes are not looked up by the filter and the search runs on this mesh alone.
## 🔒︎ int NumExcludeNavigationMeshes

The number of navigation meshes this request skips.
## ExperimentalNavigationPathFetch.PRIORITY Priority

The priority of the request in the asynchronous queue. Higher-priority requests are taken by the workers first; the value has no effect on synchronous calls.
## ExperimentalNavigationPath.STRAIGHT_MODE StraightMode

The rule that decides where the straightened path gets its points. It trades the number of points against how much the agent knows about what it walks over.
## 🔒︎ vec3 To

The Returns the target point of the request in world coordinates.
## 🔒︎ ExperimentalNavigationMesh ToNavigationMesh

The Returns the navigation mesh the target point is anchored to, if the anchor was given explicitly.
## 🔒︎ long ToPolygon

The Returns the polygon the target point is anchored to, if the anchor was given explicitly.
## 🔒︎ Event<> EventReady

The event triggered when an asynchronous request finishes, whether it produced a path or failed. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Ready event handler
void ready_event_handler()
{
	Log.Message("\Handling Ready event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections ready_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventReady.Connect(ready_event_connections, ready_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventReady.Connect(ready_event_connections, () => {
		Log.Message("Handling Ready event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
ready_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Ready event with a handler function
publisher.EventReady.Connect(ready_event_handler);

// remove subscription to the Ready event later by the handler function
publisher.EventReady.Disconnect(ready_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection ready_event_connection;

// subscribe to the Ready event with a lambda handler function and keeping the connection
ready_event_connection = publisher.EventReady.Connect(() => {
		Log.Message("Handling Ready event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
ready_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
ready_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
ready_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Ready events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventReady.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventReady.Enabled = true;

```

</details>

### Members

---

## ExperimentalNavigationPathFetch ( )

The ExperimentalNavigationPathFetch constructor. Creates an empty request with the default budgets.
## void AddExcludeNavigationMesh ( ExperimentalNavigationMesh navigation_mesh )

Adds a navigation mesh that this request must not use, even when the filter makes it eligible.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md)* **navigation_mesh** - Navigation mesh to be skipped.

## void ClearExcludeNavigationMeshes ( )

Empties the list of the navigation meshes this request skips.
## void FetchAsync ( )

Queues the request for the workers and returns immediately. Completion is reported by [EventReady](#EventReady) and by [IsReady](#IsReady).
## static void FetchAsync ( ExperimentalNavigationPathFetch [] fetches )

Queues a batch of requests for the workers at once. Sending a group of agents in a single call spreads them over the workers better than queueing each request separately.
### Arguments

- *[ExperimentalNavigationPathFetch](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_cs.md)[]* **fetches** - Requests to be queued.

## void FetchAsync ( vec3 from , vec3 to )

Sets both endpoints and queues the request for the workers in one call.
### Arguments

- *vec3* **from** - Start point in world coordinates.
- *vec3* **to** - Target point in world coordinates.

## bool FetchForce ( )

Runs the request on the calling thread and returns when it is finished. A partial path counts as a success � inspect the status of the path to tell the cases apart.
### Return value

true if a path was built; otherwise, false.
## static void FetchForce ( ExperimentalNavigationPathFetch [] fetches )

Runs a batch of requests and returns when all of them are finished. Each request keeps its own result, which is taken from it individually.
### Arguments

- *[ExperimentalNavigationPathFetch](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_cs.md)[]* **fetches** - Requests to be executed.

## bool FetchForce ( vec3 from , vec3 to )

Sets both endpoints and runs the request on the calling thread in one call.
### Arguments

- *vec3* **from** - Start point in world coordinates.
- *vec3* **to** - Target point in world coordinates.

### Return value

true if a path was built; otherwise, false.
## ExperimentalNavigationMesh GetExcludeNavigationMesh ( int num )

Returns a navigation mesh from the exclusion list of the request.
### Arguments

- *int* **num** - Number of the navigation mesh in the exclusion list.

### Return value

Excluded navigation mesh.
## void RemoveExcludeNavigationMesh ( ExperimentalNavigationMesh navigation_mesh )

Removes a navigation mesh from the list of the meshes this request skips.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md)* **navigation_mesh** - Navigation mesh to be made eligible again.

## void SetFrom ( vec3 from )

Sets the start point of the request. The point is snapped onto a navigation mesh when the request runs; if the snap finds nothing, the path fails with [FAILURE_START_OUTSIDE](../../../api/library/pathfinding/class.experimentalnavigationpath_cs.md#FAILURE_START_OUTSIDE).
### Arguments

- *vec3* **from** - Start point in world coordinates.

## void SetFrom ( ExperimentalNavigationMesh navigation_mesh , long polygon , vec3 from )

Sets the start point together with the anchor it lies on, skipping the snap. Use it when the anchor is already known from an earlier query � this also removes the ambiguity of a point that sits between two overlapping navigation meshes.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md)* **navigation_mesh** - Navigation mesh the start polygon belongs to.
- *long* **polygon** - Start polygon.
- *vec3* **from** - Start point in world coordinates.

## void SetTo ( vec3 to )

Sets the target point of the request. The point is snapped onto a navigation mesh when the request runs; if the snap finds nothing, the path fails with [FAILURE_TARGET_OUTSIDE](../../../api/library/pathfinding/class.experimentalnavigationpath_cs.md#FAILURE_TARGET_OUTSIDE).
### Arguments

- *vec3* **to** - Target point in world coordinates.

## void SetTo ( ExperimentalNavigationMesh navigation_mesh , long polygon , vec3 to )

Sets the target point together with the anchor it lies on, skipping the snap.
### Arguments

- *[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cs.md)* **navigation_mesh** - Navigation mesh the target polygon belongs to.
- *long* **polygon** - Target polygon.
- *vec3* **to** - Target point in world coordinates.

## ExperimentalNavigationPath TakePath ( )

Takes the result out of the request. The request keeps no copy afterwards, so the path must be taken once and kept by the caller.
### Return value

Path produced by the request. The caller owns it from this moment on.
## void WaitForce ( )

Blocks the calling thread until an asynchronous request finishes. Returns immediately if nothing is running.
