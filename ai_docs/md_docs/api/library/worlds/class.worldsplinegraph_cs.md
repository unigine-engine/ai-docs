# Unigine.WorldSplineGraph Class (CS)

**Inherits from:** Node


> **Warning:** This feature is an experimental one and is not recommended for production use.


This class is used to generate specified nodes (called **source nodes**) along a [spline graph](../../../objects/worlds/world_spline_graph/index.md).


UNIGINE's 3D spline system has a wide range of applications, particularly procedural content generation (rivers, roads, pipelines etc.).


![](../../../code/formats/spline.png)


A spline graph is determined by a set of [points](../../../api/library/worlds/class.splinepoint_cs.md) **p0, p 1, ... p n** and a set of segments (cubic Bezier splines), that connect some or all of these points.


Each [**segment**](../../../api/library/worlds/class.splinesegment_cs.md) is determined by the indices of the starting (**pSTART**) and ending (**pEND**) points and tangent vector coordinates at these points, which determine the form of the segment (**tSTART** and **tEND** respectively).


Coordinates of the **"up" vector** are additionally stored for each point of the segment. You can specify this vector to define orientation of geometry or objects, that can be [stretched or tiled along the segments](#intro) of the spline graph. By default this vector is parallel to the **Z** axis. The "up" vector does not affect the form of the spline segment.


It is possible to obtain an interpolated value for any point belonging to a segment, this can be used for various purposes (e.g. to change road profile). Interpolated "up" vector can be calculated as follows (pseudocode):


```cpp
vec3 lerpUpVector(vec3 start_up, vec3 end_up, float t) const
{
	float angle = acos(dot(start_up, end_up)) * RAD2DEG;
	vec3 rotation_axis = cross(start_up, end_up);

	return rotateAxisAngle(rotation_axis, angle * t) * start_up;
}

```


A world spline graph consists of segments and has a list of source nodes (currently [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md), [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md), and [DecalProj](../../../api/library/decals/class.decalproj_cs.md)) that can be placed at points and along the segments of the spline graph. Each point and segment can have a single or a set of source nodes assigned. An arbitrary number of WorldSplineGraph nodes can be added to the scene.


WorldSplineGraph has the following features:


- Points of the spline graph are managed via the [SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md) class.
- Segments of the spline graph are managed via the [SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md) class.
- 3 modes are supported:

  - **stretching**: source nodes are stretched along the spline segment.
  - **tiling**: source nodes are duplicated along the spline segment.
  - **adaptive** - represents a combination of the first two: source nodes are duplicated along the spline segment, but the length of each node (stretching) is determined by the curvature of the corresponding part of the segment. Thus, long nodes are placed along the straight parts of segments, while short ones - along the curved parts, providing a reasonable balance between the plausible look and performance.
- Forward axis selection for stretching/tiling source nodes.


### See Also


- Article on the [World Spline Graph](../../../objects/worlds/world_spline_graph/index.md) object
- C++ sample
- UnigineScript samples:

  -
  -


## WorldSplineGraph Class

### Properties

## 🔒︎ int NumSplineSegments

The total number of [spline segments](../../../api/library/worlds/class.splinesegment_cs.md) in the world spline graph.
## 🔒︎ int NumSplinePoints

The total number of [spline points](../../../api/library/worlds/class.splinepoint_cs.md) in the world spline graph.
## 🔒︎ bool IsCurved

The value indicating if the world spline graph is curved.
## 🔒︎ Event< WorldSplineGraph > EventRebuildingFinished

The event triggered after the world spline graph is rebuilt. The world spline graph uses a deferred rebuild. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WorldSplineGraph **spline_graph**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the RebuildingFinished event handler
void rebuildingfinished_event_handler(WorldSplineGraph spline_graph)
{
	Log.Message("\Handling RebuildingFinished event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections rebuildingfinished_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventRebuildingFinished.Connect(rebuildingfinished_event_connections, rebuildingfinished_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventRebuildingFinished.Connect(rebuildingfinished_event_connections, (WorldSplineGraph spline_graph) => {
		Log.Message("Handling RebuildingFinished event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
rebuildingfinished_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the RebuildingFinished event with a handler function
publisher.EventRebuildingFinished.Connect(rebuildingfinished_event_handler);

// remove subscription to the RebuildingFinished event later by the handler function
publisher.EventRebuildingFinished.Disconnect(rebuildingfinished_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection rebuildingfinished_event_connection;

// subscribe to the RebuildingFinished event with a lambda handler function and keeping the connection
rebuildingfinished_event_connection = publisher.EventRebuildingFinished.Connect((WorldSplineGraph spline_graph) => {
		Log.Message("Handling RebuildingFinished event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
rebuildingfinished_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
rebuildingfinished_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
rebuildingfinished_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring RebuildingFinished events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventRebuildingFinished.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventRebuildingFinished.Enabled = true;

```

</details>

## 🔒︎ Event< WorldSplineGraph , SplineSegment > EventSegmentRemoved

The event triggered when a segment of the world spline graph is removed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WorldSplineGraph **spline_graph**, SplineSegment **segment**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the SegmentRemoved event handler
void segmentremoved_event_handler(WorldSplineGraph spline_graph,  SplineSegment segment)
{
	Log.Message("\Handling SegmentRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections segmentremoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventSegmentRemoved.Connect(segmentremoved_event_connections, segmentremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventSegmentRemoved.Connect(segmentremoved_event_connections, (WorldSplineGraph spline_graph,  SplineSegment segment) => {
		Log.Message("Handling SegmentRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
segmentremoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the SegmentRemoved event with a handler function
publisher.EventSegmentRemoved.Connect(segmentremoved_event_handler);

// remove subscription to the SegmentRemoved event later by the handler function
publisher.EventSegmentRemoved.Disconnect(segmentremoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection segmentremoved_event_connection;

// subscribe to the SegmentRemoved event with a lambda handler function and keeping the connection
segmentremoved_event_connection = publisher.EventSegmentRemoved.Connect((WorldSplineGraph spline_graph,  SplineSegment segment) => {
		Log.Message("Handling SegmentRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
segmentremoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
segmentremoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
segmentremoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring SegmentRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventSegmentRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventSegmentRemoved.Enabled = true;

```

</details>

## 🔒︎ Event< WorldSplineGraph , SplineSegment > EventSegmentChanged

The event triggered when a segment of the world spline graph is modified. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WorldSplineGraph **spline_graph**, SplineSegment **segment**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the SegmentChanged event handler
void segmentchanged_event_handler(WorldSplineGraph spline_graph,  SplineSegment segment)
{
	Log.Message("\Handling SegmentChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections segmentchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventSegmentChanged.Connect(segmentchanged_event_connections, segmentchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventSegmentChanged.Connect(segmentchanged_event_connections, (WorldSplineGraph spline_graph,  SplineSegment segment) => {
		Log.Message("Handling SegmentChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
segmentchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the SegmentChanged event with a handler function
publisher.EventSegmentChanged.Connect(segmentchanged_event_handler);

// remove subscription to the SegmentChanged event later by the handler function
publisher.EventSegmentChanged.Disconnect(segmentchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection segmentchanged_event_connection;

// subscribe to the SegmentChanged event with a lambda handler function and keeping the connection
segmentchanged_event_connection = publisher.EventSegmentChanged.Connect((WorldSplineGraph spline_graph,  SplineSegment segment) => {
		Log.Message("Handling SegmentChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
segmentchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
segmentchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
segmentchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring SegmentChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventSegmentChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventSegmentChanged.Enabled = true;

```

</details>

## 🔒︎ Event< WorldSplineGraph , SplineSegment > EventSegmentAdded

The event triggered when a segment is added to the world spline graph. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WorldSplineGraph **spline_graph**, SplineSegment **segment**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the SegmentAdded event handler
void segmentadded_event_handler(WorldSplineGraph spline_graph,  SplineSegment segment)
{
	Log.Message("\Handling SegmentAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections segmentadded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventSegmentAdded.Connect(segmentadded_event_connections, segmentadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventSegmentAdded.Connect(segmentadded_event_connections, (WorldSplineGraph spline_graph,  SplineSegment segment) => {
		Log.Message("Handling SegmentAdded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
segmentadded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the SegmentAdded event with a handler function
publisher.EventSegmentAdded.Connect(segmentadded_event_handler);

// remove subscription to the SegmentAdded event later by the handler function
publisher.EventSegmentAdded.Disconnect(segmentadded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection segmentadded_event_connection;

// subscribe to the SegmentAdded event with a lambda handler function and keeping the connection
segmentadded_event_connection = publisher.EventSegmentAdded.Connect((WorldSplineGraph spline_graph,  SplineSegment segment) => {
		Log.Message("Handling SegmentAdded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
segmentadded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
segmentadded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
segmentadded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring SegmentAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventSegmentAdded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventSegmentAdded.Enabled = true;

```

</details>

## 🔒︎ Event< WorldSplineGraph , SplinePoint > EventPointRemoved

The event triggered when a point of the world spline graph is removed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WorldSplineGraph **spline_graph**, SplinePoint **point**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PointRemoved event handler
void pointremoved_event_handler(WorldSplineGraph spline_graph,  SplinePoint point)
{
	Log.Message("\Handling PointRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pointremoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventPointRemoved.Connect(pointremoved_event_connections, pointremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventPointRemoved.Connect(pointremoved_event_connections, (WorldSplineGraph spline_graph,  SplinePoint point) => {
		Log.Message("Handling PointRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
pointremoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PointRemoved event with a handler function
publisher.EventPointRemoved.Connect(pointremoved_event_handler);

// remove subscription to the PointRemoved event later by the handler function
publisher.EventPointRemoved.Disconnect(pointremoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection pointremoved_event_connection;

// subscribe to the PointRemoved event with a lambda handler function and keeping the connection
pointremoved_event_connection = publisher.EventPointRemoved.Connect((WorldSplineGraph spline_graph,  SplinePoint point) => {
		Log.Message("Handling PointRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
pointremoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
pointremoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
pointremoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PointRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventPointRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventPointRemoved.Enabled = true;

```

</details>

## 🔒︎ Event< WorldSplineGraph , SplinePoint > EventPointChanged

The event triggered when a point of the world spline graph is modified. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WorldSplineGraph **spline_graph**, SplinePoint **point**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PointChanged event handler
void pointchanged_event_handler(WorldSplineGraph spline_graph,  SplinePoint point)
{
	Log.Message("\Handling PointChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pointchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventPointChanged.Connect(pointchanged_event_connections, pointchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventPointChanged.Connect(pointchanged_event_connections, (WorldSplineGraph spline_graph,  SplinePoint point) => {
		Log.Message("Handling PointChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
pointchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PointChanged event with a handler function
publisher.EventPointChanged.Connect(pointchanged_event_handler);

// remove subscription to the PointChanged event later by the handler function
publisher.EventPointChanged.Disconnect(pointchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection pointchanged_event_connection;

// subscribe to the PointChanged event with a lambda handler function and keeping the connection
pointchanged_event_connection = publisher.EventPointChanged.Connect((WorldSplineGraph spline_graph,  SplinePoint point) => {
		Log.Message("Handling PointChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
pointchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
pointchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
pointchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PointChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventPointChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventPointChanged.Enabled = true;

```

</details>

## 🔒︎ Event< WorldSplineGraph , SplinePoint > EventPointAdded

The event triggered when a point is added to the world spline graph. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(WorldSplineGraph **spline_graph**, SplinePoint **point**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the PointAdded event handler
void pointadded_event_handler(WorldSplineGraph spline_graph,  SplinePoint point)
{
	Log.Message("\Handling PointAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pointadded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventPointAdded.Connect(pointadded_event_connections, pointadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventPointAdded.Connect(pointadded_event_connections, (WorldSplineGraph spline_graph,  SplinePoint point) => {
		Log.Message("Handling PointAdded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
pointadded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the PointAdded event with a handler function
publisher.EventPointAdded.Connect(pointadded_event_handler);

// remove subscription to the PointAdded event later by the handler function
publisher.EventPointAdded.Disconnect(pointadded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection pointadded_event_connection;

// subscribe to the PointAdded event with a lambda handler function and keeping the connection
pointadded_event_connection = publisher.EventPointAdded.Connect((WorldSplineGraph spline_graph,  SplinePoint point) => {
		Log.Message("Handling PointAdded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
pointadded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
pointadded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
pointadded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring PointAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventPointAdded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventPointAdded.Enabled = true;

```

</details>

### Members

---

## WorldSplineGraph ( )

Default constructor. Creates an empty world spline graph.
## WorldSplineGraph ( string name )

Constructor. Creates an empty world spline graph with a given name.
### Arguments

- *string* **name** - World spline graph name.

## void SetSplineGraphName ( string name , bool force_load = 0 )

Sets the name of the world spline graph.
### Arguments

- *string* **name** - World spline graph name.
- *bool* **force_load** - true to load the world spline graph immediately from a file, false to update only the world spline graph name.

## string GetSplineGraphName ( )

Returns the name of the world spline graph.
### Return value

World spline graph name.
## void LoadSegmentNodes ( int segment_index = -1 )

Loads source nodes assigned to the specified spline segment immediately.
### Arguments

- *int* **segment_index** - Segment index. If no segment index is specified, the method loads source nodes assigned to all segments.

## void Clear ( )

Clears the world spline graph.
## void MakeCurved ( )


Curves the world spline graph using its geodetic pivot. The spline file is saved upon completion of the curving operation.


> **Notice:** The world spline graph must be a child of a [Geodetic Pivot](../../../api/library/geodetics/class.geodeticpivot_cs.md) node.


## void MakeFlat ( )


Flattens the world spline graph using its geodetic pivot. The spline file is saved upon completion of the flattening operation.


> **Notice:** The world spline graph must be a child of a [Geodetic Pivot](../../../api/library/geodetics/class.geodeticpivot_cs.md) node.


## bool Load ( string name )

Loads a spline graph from the specified XML-file.
### Arguments

- *string* **name** - Name of the XML-file to load the spline graph from.

### Return value

true if the spline graph was successfully loaded; otherwise, false.
## bool Save ( string name )

Saves a spline graph to the specified XML-file.
### Arguments

- *string* **name** - Name of the XML-file to save the spline graph to.

### Return value

true if the spline graph was successfully saved; otherwise, false.
## static int type ( )

Returns the type of the node.
### Return value

[WorldSplineGraph](../../../api/library/nodes/class.node_cs.md#WORLD_SPLINE_GRAPH) type identifier.
## void GetSegmentNodeMesh ( Mesh mesh , SplineSegment segment , int node_index , bool bake_transform = 0 )

Gets a mesh used by a node with the specified index, placed along the specified [spline segment](../../../api/library/worlds/class.splinesegment_cs.md), and puts it to the specified target [Mesh](../../../api/library/rendering/class.mesh_cs.md) instance.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Target mesh instance to which the obtained mesh is to be put.
- *[SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md)* **segment** - [Spline segment](../../../api/library/worlds/class.splinesegment_cs.md) for which the mesh is to be returned.
- *int* **node_index** - Number of the node instance placed along the spline segment.
- *bool* **bake_transform** - true to use baked mesh transformation, false - to use default (the mesh will be placed at the origin). The default value is false.

## void GetPointNodeMesh ( Mesh mesh , SplinePoint point , int node_index , bool bake_transform = false )


Exports a mesh with the specified index placed as the specified [spline point](../../../api/library/worlds/class.splinepoint_cs.md) to the specified target mesh.


> **Notice:** Due to the nature of the mesh, there will be visual artifacts connected with the float precision, in case an exported node is located very far from the origin (around 10,000 m and further). In this case we advise exporting it without baking transformation.


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Target mesh to store the desired mesh placed at the specified spline point.
- *[SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md)* **point** - Spline point for which a mesh is to be retrieved.
- *int* **node_index** - Number of the desired node in a row of nodes placed at the specified point, in the range from 0 to the [total number of nodes placed at the point](../../../api/library/worlds/class.splinepoint_cs.md#getNumNodes_int). > **Notice:** The node must be an [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md) or an [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cs.md), otherwise an error occurs.
- *bool* **bake_transform** -  *Bake Transform* flag: true - to export the mesh preserving the current coordinates (can be useful when splitting large *WorldSplineGraph* objects to keep relative positions of meshes); or false - to reset the position of the exported mesh to origin (0,0,0) with zero-rotation.

## SplinePoint CreateSplinePoint ( vec3 position )

Creates a new [spline point](../../../api/library/worlds/class.splinepoint_cs.md) with the specified parameters and attaches it to the world spline graph.
### Arguments

- *vec3* **position** - Position coordinates for the new splint point.

### Return value

New [spline point](../../../api/library/worlds/class.splinepoint_cs.md).
## void RemoveSplinePoint ( SplinePoint point , bool merge = 0 )


Removes the specified spline point from the world spline graph. You can set the *merge* flag to merge [spline segments](../../../api/library/worlds/class.splinesegment_cs.md) sharing this point as their start and end points.


> **Notice:** Segment merging is available only when the point to be removed is shared by two segments, otherwise the *merge* flag is ignored and all segments sharing this point are also removed.


### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md)* **point** - [Spline point](../../../api/library/worlds/class.splinepoint_cs.md) to be removed.
- *bool* **merge** - true to merge spline segments sharing this point as their start and end points, false to remove all segments sharing this point. The default value is false.

## void GetSplinePoints ( SplinePoint [] OUT_points )

Returns the list of all points of the world spline graph and puts them to the specified array of [SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md) elements.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md)[]* **OUT_points** - Array to store the list of all points of the world spline graph. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## SplineSegment CreateSplineSegment ( SplinePoint start_point , vec3 start_tangent , vec3 start_up , SplinePoint end_point , vec3 end_tangent , vec3 end_up )

Creates a new [spline segment](../../../api/library/worlds/class.splinesegment_cs.md) with the specified parameters and attaches it to the world spline graph.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md)* **start_point** - Start [point](../../../api/library/worlds/class.splinepoint_cs.md) of the spline segment.
- *vec3* **start_tangent** - Tangent coordinates for the start point of the spline segment.
- *vec3* **start_up** - Coordinates of the ["up" vector](#up) for the start point of the spline segment.
- *[SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md)* **end_point** - End [point](../../../api/library/worlds/class.splinepoint_cs.md) of the segment.
- *vec3* **end_tangent** - Tangent coordinates for the end point of the spline segment.
- *vec3* **end_up** - Coordinates of the ["up" vector](#up) for the end point of the spline segment.

### Return value

New [spline segment](../../../api/library/worlds/class.splinesegment_cs.md) connecting two specified points.
## void RemoveSplineSegment ( SplineSegment segment , bool with_points = 0 )

Removes the specified spline segment from the world spline graph. You can set the *with_points* flag to remove the segment together with its start and end points.
### Arguments

- *[SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md)* **segment** - [Spline segment](../../../api/library/worlds/class.splinesegment_cs.md) to be removed.
- *bool* **with_points** - true to remove the segment with its start and end points, false to keep points. The default value is false.

## void GetSplineSegments ( SplineSegment [] OUT_segments )

Returns the list of all segments of the world spline graph and puts them to the specified array of [SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md) elements.
### Arguments

- *[SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md)[]* **OUT_segments** - Array to store the list of all segments of the world spline graph. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void Rebuild ( int try_force = 0 )

Rebuilds the world spline graph. This method is to be called after making any changes to spline segments (mode, etc.), point positions, tangents, or "up" vectors, as well as after changing [source node](#source_node) assignments and/or other parameters (UV tiling, gap, etc.)
### Arguments

- *int* **try_force** - Forced rebuild flag: set 1 to try and force rebuild the world spline graph.

## int IsRebuilding ( )

Returns a value indicating if the world spline graph is currently being rebuilt. The world spline graph uses a deferred rebuild.
### Return value

1 if the world spline graph is currently being rebuilt; otherwise 0.
## void SplitSplineSegment ( SplineSegment segment , float new_point_t )

Splits the specified [spline segment](../../../api/library/worlds/class.splinesegment_cs.md) into two parts by inserting a new point placed at the parametrically specified point on the T (times axis) in the **[0.0f, 1.0f]** range from the segment's start point.
![](../math/cubic_bezier.gif)


### Arguments

- *[SplineSegment](../../../api/library/worlds/class.splinesegment_cs.md)* **segment** - Spline segment to be split.
- *float* **new_point_t** - Coordinate of the splitting point of the segment along the horizontal *T* (times) axis in the range **[0.0f, 1.0f]**.

## void BreakSplinePoint ( SplinePoint point )

Breaks the specified [spline point](../../../api/library/worlds/class.splinepoint_cs.md) shared by several [spline segments](../../../api/library/worlds/class.splinesegment_cs.md) into a set of separate ones, so that each of the segments gets its own point.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md)* **point** - Spline point to be broken. > **Notice:** The point must be shared by a least 2 segments.

## void WeldSplinePoints ( SplinePoint [] OUT_points )

Joins all [spline points](../../../api/library/worlds/class.splinepoint_cs.md) specified in the list into a single one, so that this point is shared by all spline segments having the specified points as starting or ending ones.
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md)[]* **OUT_points** - List of spline points to be joined into a single one. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool IsLinked ( SplinePoint point )

Returns a value indicating if the specified [spline point](../../../api/library/worlds/class.splinepoint_cs.md) is linked to any [spline segment](../../../api/library/worlds/class.splinesegment_cs.md).
### Arguments

- *[SplinePoint](../../../api/library/worlds/class.splinepoint_cs.md)* **point** - Spline point to be checked.

### Return value

true if the specified spline point is linked to any spline segment; otherwise, false.
