# Unigine::ExperimentalNavigationPathFetch Class (CPP)

**Header:** #include <UnigineExperimentalNavigation.h>


A single path request. It carries the two endpoints, the [filter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md) describing the agent, and the budgets the search may spend; once it completes, the result is taken out as an [ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md). A fetch is a one-shot promise with a lifecycle, which is why the reusable per-agent settings live in the filter and not here.


Requests run either synchronously via [fetchForce()](#fetchForce_int) on the calling thread, or on workers via [fetchAsync()](#fetchAsync_void) with [EventReady](#EventReady) reporting completion. Both have batch versions that take many fetches at once � sending a whole squad in one call is cheaper than sending each agent separately.


Endpoints can be given as bare world positions, in which case the engine snaps them onto a navigation mesh, or as a mesh, polygon and position triple when the anchor is already known from an earlier query. The second form skips the snap and rules out the ambiguity of a point that sits between two overlapping meshes.


## ExperimentalNavigationPathFetch Class

### Enums

## PRIORITY

| Name | Description |
|---|---|
| **PRIORITY_LOW** = 0 | The request waits until no request of a higher priority is queued. |
| **PRIORITY_NORMAL** = 1 | Default priority. |
| **PRIORITY_HIGH** = 2 | The request is taken by the workers before the normal and low ones. |

### Members

## void setFilter ( const Ptr < ExperimentalNavigationMeshFilter >& filter )

Sets a new filter describing the agent the path is requested for. It decides which navigation meshes are eligible, which polygons are passable, and what each area costs.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMeshFilter](../../../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)>&* **filter** - The filter used by the request.

## Ptr < ExperimentalNavigationMeshFilter > getFilter () const

Returns the current filter describing the agent the path is requested for. It decides which navigation meshes are eligible, which polygons are passable, and what each area costs.
### Return value

Current filter used by the request.
## Math:: Vec3 getFrom () const

Returns the start point of the request in world coordinates.
### Return value

start point of the request.
## Ptr < ExperimentalNavigationMesh > getFromNavigationMesh () const

Returns the navigation mesh the start point is anchored to, if the anchor was given explicitly.
### Return value

navigation mesh of the start anchor, or NULL if the start point is resolved by snapping.
## long long getFromPolygon () const

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
## bool isFetching () const

Returns the current value indicating if the request is currently being processed.
### Return value

**true** if the request has been started and has not finished yet; otherwise **false**.
## bool isReady () const

Returns the current value indicating if the result of the request can be taken.
### Return value

**true** if the result is ready to be taken; otherwise **false**.
## void setMaxCost ( float cost )

Sets a new cost budget of the search. When the accumulated cost exceeds it, the search stops and the path comes back partial with [FAILURE_COST_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#FAILURE_COST_LIMIT).
### Arguments

- *float* **cost** - The maximum cost. The default value is 0, which means no cost limit.

## float getMaxCost () const

Returns the current cost budget of the search. When the accumulated cost exceeds it, the search stops and the path comes back partial with [FAILURE_COST_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#FAILURE_COST_LIMIT).
### Return value

Current maximum cost. The default value is 0, which means no cost limit.
## void setMaxSearchNodes ( int nodes )

Sets a new node budget of the search. When it is exhausted, the search stops and the path comes back partial with [FAILURE_SEARCH_NODES_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#FAILURE_SEARCH_NODES_LIMIT). It bounds the cost of a single request on a large navigation mesh.
### Arguments

- *int* **nodes** - The maximum number of search nodes. The default value is 2048.

## int getMaxSearchNodes () const

Returns the current node budget of the search. When it is exhausted, the search stops and the path comes back partial with [FAILURE_SEARCH_NODES_LIMIT](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#FAILURE_SEARCH_NODES_LIMIT). It bounds the cost of a single request on a large navigation mesh.
### Return value

Current maximum number of search nodes. The default value is 2048.
## void setNavigationMesh ( const Ptr < ExperimentalNavigationMesh >& mesh )

Sets a new navigation mesh the search is restricted to. When it is set, the eligible meshes are not looked up by the filter and the search runs on this mesh alone.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)>&* **mesh** - The navigation mesh of the request, or NULL if the mesh is chosen by the filter.

## Ptr < ExperimentalNavigationMesh > getNavigationMesh () const

Returns the current navigation mesh the search is restricted to. When it is set, the eligible meshes are not looked up by the filter and the search runs on this mesh alone.
### Return value

Current navigation mesh of the request, or NULL if the mesh is chosen by the filter.
## int getNumExcludeNavigationMeshes () const

Returns the current number of navigation meshes this request skips.
### Return value

Current number of excluded navigation meshes.
## void setPriority ( ExperimentalNavigationPathFetch::PRIORITY priority )

Sets a new priority of the request in the asynchronous queue. Higher-priority requests are taken by the workers first; the value has no effect on synchronous calls.
### Arguments

- *[ExperimentalNavigationPathFetch::PRIORITY](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_cpp.md#PRIORITY)* **priority** - The priority, one of the [PRIORITY_*](#PRIORITY_LOW) values. The default value is [PRIORITY_NORMAL](#PRIORITY_NORMAL).

## ExperimentalNavigationPathFetch::PRIORITY getPriority () const

Returns the current priority of the request in the asynchronous queue. Higher-priority requests are taken by the workers first; the value has no effect on synchronous calls.
### Return value

Current priority, one of the [PRIORITY_*](#PRIORITY_LOW) values. The default value is [PRIORITY_NORMAL](#PRIORITY_NORMAL).
## void setStraightMode ( ExperimentalNavigationPath::STRAIGHT_MODE mode )

Sets a new rule that decides where the straightened path gets its points. It trades the number of points against how much the agent knows about what it walks over.
### Arguments

- *[ExperimentalNavigationPath::STRAIGHT_MODE](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#STRAIGHT_MODE)* **mode** - The straightening mode, one of the [STRAIGHT_MODE_*](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#STRAIGHT_MODE_CORNERS) values of [ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md). The default value is [STRAIGHT_MODE_AREA_CROSSINGS](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#STRAIGHT_MODE_AREA_CROSSINGS).

## ExperimentalNavigationPath::STRAIGHT_MODE getStraightMode () const

Returns the current rule that decides where the straightened path gets its points. It trades the number of points against how much the agent knows about what it walks over.
### Return value

Current straightening mode, one of the [STRAIGHT_MODE_*](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#STRAIGHT_MODE_CORNERS) values of [ExperimentalNavigationPath](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md). The default value is [STRAIGHT_MODE_AREA_CROSSINGS](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#STRAIGHT_MODE_AREA_CROSSINGS).
## Math:: Vec3 getTo () const

Returns the target point of the request in world coordinates.
### Return value

target point of the request.
## Ptr < ExperimentalNavigationMesh > getToNavigationMesh () const

Returns the navigation mesh the target point is anchored to, if the anchor was given explicitly.
### Return value

navigation mesh of the target anchor, or NULL if the target point is resolved by snapping.
## long long getToPolygon () const

Returns the polygon the target point is anchored to, if the anchor was given explicitly.
### Return value

polygon of the target anchor, or 0 if the target point is resolved by snapping.
## Event<> getEventReady () const

event triggered when an asynchronous request finishes, whether it produced a path or failed. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Ready event handler
void ready_event_handler()
{
	Log::message("\Handling Ready event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections ready_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventReady().connect(ready_event_connections, ready_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventReady().connect(ready_event_connections, []() {
		Log::message("\Handling Ready event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
ready_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection ready_event_connection;

// subscribe to the Ready event with a handler function keeping the connection
publisher->getEventReady().connect(ready_event_connection, ready_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
ready_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
ready_event_connection.setEnabled(true);

// ...

// remove subscription to the Ready event via the connection
ready_event_connection.disconnect();

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

	// A Ready event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling Ready event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventReady().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId ready_handler_id;

// subscribe to the Ready event with a lambda handler function and keeping connection ID
ready_handler_id = publisher->getEventReady().connect(e_connections, []() {
		Log::message("\Handling Ready event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventReady().disconnect(ready_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Ready events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventReady().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventReady().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static ExperimentalNavigationPathFetchPtr create ( )

The ExperimentalNavigationPathFetch constructor. Creates an empty request with the default budgets.
## void addExcludeNavigationMesh ( const Ptr < ExperimentalNavigationMesh > & navigation_mesh )

Adds a navigation mesh that this request must not use, even when the filter makes it eligible.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)> &* **navigation_mesh** - Navigation mesh to be skipped.

## void clearExcludeNavigationMeshes ( )

Empties the list of the navigation meshes this request skips.
## void fetchAsync ( )

Queues the request for the workers and returns immediately. Completion is reported by [EventReady](#EventReady) and by [IsReady](#IsReady).
## static void fetchAsync ( const Vector < Ptr < ExperimentalNavigationPathFetch >> & fetches )

Queues a batch of requests for the workers at once. Sending a group of agents in a single call spreads them over the workers better than queueing each request separately.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationPathFetch](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_cpp.md)>> &* **fetches** - Requests to be queued.

## void fetchAsync ( const Math:: Vec3 & from , const Math:: Vec3 & to )

Sets both endpoints and queues the request for the workers in one call.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **from** - Start point in world coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **to** - Target point in world coordinates.

## bool fetchForce ( )

Runs the request on the calling thread and returns when it is finished. A partial path counts as a success � inspect the status of the path to tell the cases apart.
### Return value

true if a path was built; otherwise, false.
## static void fetchForce ( const Vector < Ptr < ExperimentalNavigationPathFetch >> & fetches )

Runs a batch of requests and returns when all of them are finished. Each request keeps its own result, which is taken from it individually.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationPathFetch](../../../api/library/pathfinding/class.experimentalnavigationpathfetch_cpp.md)>> &* **fetches** - Requests to be executed.

## bool fetchForce ( const Math:: Vec3 & from , const Math:: Vec3 & to )

Sets both endpoints and runs the request on the calling thread in one call.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **from** - Start point in world coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **to** - Target point in world coordinates.

### Return value

true if a path was built; otherwise, false.
## Ptr < ExperimentalNavigationMesh > getExcludeNavigationMesh ( int num )

Returns a navigation mesh from the exclusion list of the request.
### Arguments

- *int* **num** - Number of the navigation mesh in the exclusion list.

### Return value

Excluded navigation mesh.
## void removeExcludeNavigationMesh ( const Ptr < ExperimentalNavigationMesh > & navigation_mesh )

Removes a navigation mesh from the list of the meshes this request skips.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)> &* **navigation_mesh** - Navigation mesh to be made eligible again.

## void setFrom ( const Math:: Vec3 & from )

Sets the start point of the request. The point is snapped onto a navigation mesh when the request runs; if the snap finds nothing, the path fails with [FAILURE_START_OUTSIDE](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#FAILURE_START_OUTSIDE).
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **from** - Start point in world coordinates.

## void setFrom ( const Ptr < ExperimentalNavigationMesh > & navigation_mesh , long long polygon , const Math:: Vec3 & from )

Sets the start point together with the anchor it lies on, skipping the snap. Use it when the anchor is already known from an earlier query � this also removes the ambiguity of a point that sits between two overlapping navigation meshes.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)> &* **navigation_mesh** - Navigation mesh the start polygon belongs to.
- *long long* **polygon** - Start polygon.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **from** - Start point in world coordinates.

## void setTo ( const Math:: Vec3 & to )

Sets the target point of the request. The point is snapped onto a navigation mesh when the request runs; if the snap finds nothing, the path fails with [FAILURE_TARGET_OUTSIDE](../../../api/library/pathfinding/class.experimentalnavigationpath_cpp.md#FAILURE_TARGET_OUTSIDE).
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **to** - Target point in world coordinates.

## void setTo ( const Ptr < ExperimentalNavigationMesh > & navigation_mesh , long long polygon , const Math:: Vec3 & to )

Sets the target point together with the anchor it lies on, skipping the snap.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ExperimentalNavigationMesh](../../../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)> &* **navigation_mesh** - Navigation mesh the target polygon belongs to.
- *long long* **polygon** - Target polygon.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **to** - Target point in world coordinates.

## Ptr < ExperimentalNavigationPath > takePath ( )

Takes the result out of the request. The request keeps no copy afterwards, so the path must be taken once and kept by the caller.
### Return value

Path produced by the request. The caller owns it from this moment on.
## void waitForce ( )

Blocks the calling thread until an asynchronous request finishes. Returns immediately if nothing is running.
