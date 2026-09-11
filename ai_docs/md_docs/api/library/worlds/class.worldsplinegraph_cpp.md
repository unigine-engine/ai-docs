# Unigine.WorldSplineGraph Class (CPP)

**Header:** #include <UnigineWorlds.h>

**Inherits from:** Node


> **Warning:** This feature is an experimental one and is not recommended for production use.


This class is used to generate specified nodes (called **source nodes**) along a [spline graph](../../../objects/worlds/world_spline_graph/index.md).


UNIGINE's 3D spline system has a wide range of applications, particularly procedural content generation (rivers, roads, pipelines etc.).


![](../../../code/formats/spline.png)


A spline graph is determined by a set of [points](../../../api/library/worlds/class.splinepoint_cpp.md) **p0, p 1, ... p n** and a set of segments (cubic Bezier splines), that connect some or all of these points.


Each [**segment**](../../../api/library/worlds/class.splinesegment_cpp.md) is determined by the indices of the starting (**pSTART**) and ending (**pEND**) points and tangent vector coordinates at these points, which determine the form of the segment (**tSTART** and **tEND** respectively).


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


A world spline graph consists of segments and has a list of source nodes (currently [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md), [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md), and [DecalProj](../../../api/library/decals/class.decalproj_cpp.md)) that can be placed at points and along the segments of the spline graph. Each point and segment can have a single or a set of source nodes assigned. An arbitrary number of WorldSplineGraph nodes can be added to the scene.


WorldSplineGraph has the following features:


- Points of the spline graph are managed via the [SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md) class.
- Segments of the spline graph are managed via the [SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md) class.
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

### Members

## int getNumSplineSegments () const

Returns the current total number of [spline segments](../../../api/library/worlds/class.splinesegment_cpp.md) in the world spline graph.
### Return value

Current number of segments in the world spline graph.
## int getNumSplinePoints () const

Returns the current total number of [spline points](../../../api/library/worlds/class.splinepoint_cpp.md) in the world spline graph.
### Return value

Current number of spline points.
## bool isCurved () const

Returns the current value indicating if the world spline graph is curved.
### Return value

**true** if the world spline graph is curved; otherwise **false**.
## Event<const Ptr < WorldSplineGraph > &> getEventRebuildingFinished () const

event triggered after the world spline graph is rebuilt. The world spline graph uses a deferred rebuild. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<WorldSplineGraph> & **spline_graph**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the RebuildingFinished event handler
void rebuildingfinished_event_handler(const Ptr<WorldSplineGraph> & spline_graph)
{
	Log::message("\Handling RebuildingFinished event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections rebuildingfinished_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventRebuildingFinished().connect(rebuildingfinished_event_connections, rebuildingfinished_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventRebuildingFinished().connect(rebuildingfinished_event_connections, [](const Ptr<WorldSplineGraph> & spline_graph) {
		Log::message("\Handling RebuildingFinished event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
rebuildingfinished_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection rebuildingfinished_event_connection;

// subscribe to the RebuildingFinished event with a handler function keeping the connection
publisher->getEventRebuildingFinished().connect(rebuildingfinished_event_connection, rebuildingfinished_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
rebuildingfinished_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
rebuildingfinished_event_connection.setEnabled(true);

// ...

// remove subscription to the RebuildingFinished event via the connection
rebuildingfinished_event_connection.disconnect();

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

	// A RebuildingFinished event handler implemented as a class member
	void event_handler(const Ptr<WorldSplineGraph> & spline_graph)
	{
		Log::message("\Handling RebuildingFinished event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventRebuildingFinished().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId rebuildingfinished_handler_id;

// subscribe to the RebuildingFinished event with a lambda handler function and keeping connection ID
rebuildingfinished_handler_id = publisher->getEventRebuildingFinished().connect(e_connections, [](const Ptr<WorldSplineGraph> & spline_graph) {
		Log::message("\Handling RebuildingFinished event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventRebuildingFinished().disconnect(rebuildingfinished_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all RebuildingFinished events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventRebuildingFinished().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventRebuildingFinished().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < WorldSplineGraph > &, const Ptr < SplineSegment > &> getEventSegmentRemoved () const

event triggered when a segment of the world spline graph is removed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<WorldSplineGraph> & **spline_graph**, const Ptr<SplineSegment> & **segment**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the SegmentRemoved event handler
void segmentremoved_event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment)
{
	Log::message("\Handling SegmentRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections segmentremoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventSegmentRemoved().connect(segmentremoved_event_connections, segmentremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventSegmentRemoved().connect(segmentremoved_event_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment) {
		Log::message("\Handling SegmentRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
segmentremoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection segmentremoved_event_connection;

// subscribe to the SegmentRemoved event with a handler function keeping the connection
publisher->getEventSegmentRemoved().connect(segmentremoved_event_connection, segmentremoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
segmentremoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
segmentremoved_event_connection.setEnabled(true);

// ...

// remove subscription to the SegmentRemoved event via the connection
segmentremoved_event_connection.disconnect();

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

	// A SegmentRemoved event handler implemented as a class member
	void event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment)
	{
		Log::message("\Handling SegmentRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventSegmentRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId segmentremoved_handler_id;

// subscribe to the SegmentRemoved event with a lambda handler function and keeping connection ID
segmentremoved_handler_id = publisher->getEventSegmentRemoved().connect(e_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment) {
		Log::message("\Handling SegmentRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventSegmentRemoved().disconnect(segmentremoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all SegmentRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventSegmentRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventSegmentRemoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < WorldSplineGraph > &, const Ptr < SplineSegment > &> getEventSegmentChanged () const

event triggered when a segment of the world spline graph is modified. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<WorldSplineGraph> & **spline_graph**, const Ptr<SplineSegment> & **segment**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the SegmentChanged event handler
void segmentchanged_event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment)
{
	Log::message("\Handling SegmentChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections segmentchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventSegmentChanged().connect(segmentchanged_event_connections, segmentchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventSegmentChanged().connect(segmentchanged_event_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment) {
		Log::message("\Handling SegmentChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
segmentchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection segmentchanged_event_connection;

// subscribe to the SegmentChanged event with a handler function keeping the connection
publisher->getEventSegmentChanged().connect(segmentchanged_event_connection, segmentchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
segmentchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
segmentchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the SegmentChanged event via the connection
segmentchanged_event_connection.disconnect();

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

	// A SegmentChanged event handler implemented as a class member
	void event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment)
	{
		Log::message("\Handling SegmentChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventSegmentChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId segmentchanged_handler_id;

// subscribe to the SegmentChanged event with a lambda handler function and keeping connection ID
segmentchanged_handler_id = publisher->getEventSegmentChanged().connect(e_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment) {
		Log::message("\Handling SegmentChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventSegmentChanged().disconnect(segmentchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all SegmentChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventSegmentChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventSegmentChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < WorldSplineGraph > &, const Ptr < SplineSegment > &> getEventSegmentAdded () const

event triggered when a segment is added to the world spline graph. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<WorldSplineGraph> & **spline_graph**, const Ptr<SplineSegment> & **segment**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the SegmentAdded event handler
void segmentadded_event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment)
{
	Log::message("\Handling SegmentAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections segmentadded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventSegmentAdded().connect(segmentadded_event_connections, segmentadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventSegmentAdded().connect(segmentadded_event_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment) {
		Log::message("\Handling SegmentAdded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
segmentadded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection segmentadded_event_connection;

// subscribe to the SegmentAdded event with a handler function keeping the connection
publisher->getEventSegmentAdded().connect(segmentadded_event_connection, segmentadded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
segmentadded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
segmentadded_event_connection.setEnabled(true);

// ...

// remove subscription to the SegmentAdded event via the connection
segmentadded_event_connection.disconnect();

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

	// A SegmentAdded event handler implemented as a class member
	void event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment)
	{
		Log::message("\Handling SegmentAdded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventSegmentAdded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId segmentadded_handler_id;

// subscribe to the SegmentAdded event with a lambda handler function and keeping connection ID
segmentadded_handler_id = publisher->getEventSegmentAdded().connect(e_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplineSegment> & segment) {
		Log::message("\Handling SegmentAdded event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventSegmentAdded().disconnect(segmentadded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all SegmentAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventSegmentAdded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventSegmentAdded().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < WorldSplineGraph > &, const Ptr < SplinePoint > &> getEventPointRemoved () const

event triggered when a point of the world spline graph is removed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<WorldSplineGraph> & **spline_graph**, const Ptr<SplinePoint> & **point**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PointRemoved event handler
void pointremoved_event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point)
{
	Log::message("\Handling PointRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pointremoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventPointRemoved().connect(pointremoved_event_connections, pointremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventPointRemoved().connect(pointremoved_event_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point) {
		Log::message("\Handling PointRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
pointremoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection pointremoved_event_connection;

// subscribe to the PointRemoved event with a handler function keeping the connection
publisher->getEventPointRemoved().connect(pointremoved_event_connection, pointremoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
pointremoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
pointremoved_event_connection.setEnabled(true);

// ...

// remove subscription to the PointRemoved event via the connection
pointremoved_event_connection.disconnect();

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

	// A PointRemoved event handler implemented as a class member
	void event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point)
	{
		Log::message("\Handling PointRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventPointRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId pointremoved_handler_id;

// subscribe to the PointRemoved event with a lambda handler function and keeping connection ID
pointremoved_handler_id = publisher->getEventPointRemoved().connect(e_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point) {
		Log::message("\Handling PointRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventPointRemoved().disconnect(pointremoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PointRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventPointRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventPointRemoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < WorldSplineGraph > &, const Ptr < SplinePoint > &> getEventPointChanged () const

event triggered when a point of the world spline graph is modified. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<WorldSplineGraph> & **spline_graph**, const Ptr<SplinePoint> & **point**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PointChanged event handler
void pointchanged_event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point)
{
	Log::message("\Handling PointChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pointchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventPointChanged().connect(pointchanged_event_connections, pointchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventPointChanged().connect(pointchanged_event_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point) {
		Log::message("\Handling PointChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
pointchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection pointchanged_event_connection;

// subscribe to the PointChanged event with a handler function keeping the connection
publisher->getEventPointChanged().connect(pointchanged_event_connection, pointchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
pointchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
pointchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the PointChanged event via the connection
pointchanged_event_connection.disconnect();

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

	// A PointChanged event handler implemented as a class member
	void event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point)
	{
		Log::message("\Handling PointChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventPointChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId pointchanged_handler_id;

// subscribe to the PointChanged event with a lambda handler function and keeping connection ID
pointchanged_handler_id = publisher->getEventPointChanged().connect(e_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point) {
		Log::message("\Handling PointChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventPointChanged().disconnect(pointchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PointChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventPointChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventPointChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < WorldSplineGraph > &, const Ptr < SplinePoint > &> getEventPointAdded () const

event triggered when a point is added to the world spline graph. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<WorldSplineGraph> & **spline_graph**, const Ptr<SplinePoint> & **point**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the PointAdded event handler
void pointadded_event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point)
{
	Log::message("\Handling PointAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections pointadded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventPointAdded().connect(pointadded_event_connections, pointadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventPointAdded().connect(pointadded_event_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point) {
		Log::message("\Handling PointAdded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
pointadded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection pointadded_event_connection;

// subscribe to the PointAdded event with a handler function keeping the connection
publisher->getEventPointAdded().connect(pointadded_event_connection, pointadded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
pointadded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
pointadded_event_connection.setEnabled(true);

// ...

// remove subscription to the PointAdded event via the connection
pointadded_event_connection.disconnect();

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

	// A PointAdded event handler implemented as a class member
	void event_handler(const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point)
	{
		Log::message("\Handling PointAdded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventPointAdded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId pointadded_handler_id;

// subscribe to the PointAdded event with a lambda handler function and keeping connection ID
pointadded_handler_id = publisher->getEventPointAdded().connect(e_connections, [](const Ptr<WorldSplineGraph> & spline_graph,  const Ptr<SplinePoint> & point) {
		Log::message("\Handling PointAdded event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventPointAdded().disconnect(pointadded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all PointAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventPointAdded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventPointAdded().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static WorldSplineGraphPtr create ( )

Default constructor. Creates an empty world spline graph.
## static WorldSplineGraphPtr create ( const char * name )

Constructor. Creates an empty world spline graph with a given name.
### Arguments

- *const char ** **name** - World spline graph name.

## void setSplineGraphName ( const char * name , bool force_load = 0 )

Sets the name of the world spline graph.
### Arguments

- *const char ** **name** - World spline graph name.
- *bool* **force_load** - true to load the world spline graph immediately from a file, false to update only the world spline graph name.

## const char * getSplineGraphName ( ) const

Returns the name of the world spline graph.
### Return value

World spline graph name.
## void loadSegmentNodes ( int segment_index = -1 )

Loads source nodes assigned to the specified spline segment immediately.
### Arguments

- *int* **segment_index** - Segment index. If no segment index is specified, the method loads source nodes assigned to all segments.

## void clear ( )

Clears the world spline graph.
## void makeCurved ( )


Curves the world spline graph using its geodetic pivot. The spline file is saved upon completion of the curving operation.


> **Notice:** The world spline graph must be a child of a [Geodetic Pivot](../../../api/library/geodetics/class.geodeticpivot_cpp.md) node.


## void makeFlat ( )


Flattens the world spline graph using its geodetic pivot. The spline file is saved upon completion of the flattening operation.


> **Notice:** The world spline graph must be a child of a [Geodetic Pivot](../../../api/library/geodetics/class.geodeticpivot_cpp.md) node.


## bool load ( const char * name )

Loads a spline graph from the specified XML-file.
### Arguments

- *const char ** **name** - Name of the XML-file to load the spline graph from.

### Return value

true if the spline graph was successfully loaded; otherwise, false.
## bool save ( const char * name )

Saves a spline graph to the specified XML-file.
### Arguments

- *const char ** **name** - Name of the XML-file to save the spline graph to.

### Return value

true if the spline graph was successfully saved; otherwise, false.
## static int type ( )

Returns the type of the node.
### Return value

[WorldSplineGraph](../../../api/library/nodes/class.node_cpp.md#WORLD_SPLINE_GRAPH) type identifier.
## void getSegmentNodeMesh ( const Ptr < Mesh > & mesh , const Ptr < SplineSegment > & segment , int node_index , bool bake_transform = 0 )

Gets a mesh used by a node with the specified index, placed along the specified [spline segment](../../../api/library/worlds/class.splinesegment_cpp.md), and puts it to the specified target [Mesh](../../../api/library/rendering/class.mesh_cpp.md) instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Target mesh instance to which the obtained mesh is to be put.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md)> &* **segment** - [Spline segment](../../../api/library/worlds/class.splinesegment_cpp.md) for which the mesh is to be returned.
- *int* **node_index** - Number of the node instance placed along the spline segment.
- *bool* **bake_transform** - true to use baked mesh transformation, false - to use default (the mesh will be placed at the origin). The default value is false.

## void getPointNodeMesh ( const Ptr < Mesh > & mesh , const Ptr < SplinePoint > & point , int node_index , bool bake_transform = false )


Exports a mesh with the specified index placed as the specified [spline point](../../../api/library/worlds/class.splinepoint_cpp.md) to the specified target mesh.


> **Notice:** Due to the nature of the mesh, there will be visual artifacts connected with the float precision, in case an exported node is located very far from the origin (around 10,000 m and further). In this case we advise exporting it without baking transformation.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Target mesh to store the desired mesh placed at the specified spline point.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)> &* **point** - Spline point for which a mesh is to be retrieved.
- *int* **node_index** - Number of the desired node in a row of nodes placed at the specified point, in the range from 0 to the [total number of nodes placed at the point](../../../api/library/worlds/class.splinepoint_cpp.md#getNumNodes_int). > **Notice:** The node must be an [ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md) or an [ObjectMeshSkinnedLegacy](../../../api/library/objects/class.objectmeshskinnedlegacy_cpp.md), otherwise an error occurs.
- *bool* **bake_transform** -  *Bake Transform* flag: true - to export the mesh preserving the current coordinates (can be useful when splitting large *WorldSplineGraph* objects to keep relative positions of meshes); or false - to reset the position of the exported mesh to origin (0,0,0) with zero-rotation.

## Ptr < SplinePoint > createSplinePoint ( const Math:: Vec3 & position )

Creates a new [spline point](../../../api/library/worlds/class.splinepoint_cpp.md) with the specified parameters and attaches it to the world spline graph.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Position coordinates for the new splint point.

### Return value

New [spline point](../../../api/library/worlds/class.splinepoint_cpp.md).
## void removeSplinePoint ( const Ptr < SplinePoint > & point , bool merge = 0 )


Removes the specified spline point from the world spline graph. You can set the *merge* flag to merge [spline segments](../../../api/library/worlds/class.splinesegment_cpp.md) sharing this point as their start and end points.


> **Notice:** Segment merging is available only when the point to be removed is shared by two segments, otherwise the *merge* flag is ignored and all segments sharing this point are also removed.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)> &* **point** - [Spline point](../../../api/library/worlds/class.splinepoint_cpp.md) to be removed.
- *bool* **merge** - true to merge spline segments sharing this point as their start and end points, false to remove all segments sharing this point. The default value is false.

## void getSplinePoints ( Vector < Ptr < SplinePoint >> & OUT_points ) const

Returns the list of all points of the world spline graph and puts them to the specified vector of [SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md) elements.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)>> &* **OUT_points** - Vector to store the list of all points of the world spline graph. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Ptr < SplineSegment > createSplineSegment ( const Ptr < SplinePoint > & start_point , const Math:: vec3 & start_tangent , const Math:: vec3 & start_up , const Ptr < SplinePoint > & end_point , const Math:: vec3 & end_tangent , const Math:: vec3 & end_up )

Creates a new [spline segment](../../../api/library/worlds/class.splinesegment_cpp.md) with the specified parameters and attaches it to the world spline graph.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)> &* **start_point** - Start [point](../../../api/library/worlds/class.splinepoint_cpp.md) of the spline segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **start_tangent** - Tangent coordinates for the start point of the spline segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **start_up** - Coordinates of the ["up" vector](#up) for the start point of the spline segment.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)> &* **end_point** - End [point](../../../api/library/worlds/class.splinepoint_cpp.md) of the segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **end_tangent** - Tangent coordinates for the end point of the spline segment.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **end_up** - Coordinates of the ["up" vector](#up) for the end point of the spline segment.

### Return value

New [spline segment](../../../api/library/worlds/class.splinesegment_cpp.md) connecting two specified points.
## void removeSplineSegment ( const Ptr < SplineSegment > & segment , bool with_points = 0 )

Removes the specified spline segment from the world spline graph. You can set the *with_points* flag to remove the segment together with its start and end points.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md)> &* **segment** - [Spline segment](../../../api/library/worlds/class.splinesegment_cpp.md) to be removed.
- *bool* **with_points** - true to remove the segment with its start and end points, false to keep points. The default value is false.

## void getSplineSegments ( Vector < Ptr < SplineSegment >> & OUT_segments ) const

Returns the list of all segments of the world spline graph and puts them to the specified vector of [SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md) elements.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md)>> &* **OUT_segments** - Vector to store the list of all segments of the world spline graph. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void rebuild ( int try_force = 0 )

Rebuilds the world spline graph. This method is to be called after making any changes to spline segments (mode, etc.), point positions, tangents, or "up" vectors, as well as after changing [source node](#source_node) assignments and/or other parameters (UV tiling, gap, etc.)
### Arguments

- *int* **try_force** - Forced rebuild flag: set 1 to try and force rebuild the world spline graph.

## int isRebuilding ( ) const

Returns a value indicating if the world spline graph is currently being rebuilt. The world spline graph uses a deferred rebuild.
### Return value

1 if the world spline graph is currently being rebuilt; otherwise 0.
## void splitSplineSegment ( const Ptr < SplineSegment > & segment , float new_point_t )

Splits the specified [spline segment](../../../api/library/worlds/class.splinesegment_cpp.md) into two parts by inserting a new point placed at the parametrically specified point on the T (times axis) in the **[0.0f, 1.0f]** range from the segment's start point.
![](../math/cubic_bezier.gif)


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplineSegment](../../../api/library/worlds/class.splinesegment_cpp.md)> &* **segment** - Spline segment to be split.
- *float* **new_point_t** - Coordinate of the splitting point of the segment along the horizontal *T* (times) axis in the range **[0.0f, 1.0f]**.

## void breakSplinePoint ( const Ptr < SplinePoint > & point )

Breaks the specified [spline point](../../../api/library/worlds/class.splinepoint_cpp.md) shared by several [spline segments](../../../api/library/worlds/class.splinesegment_cpp.md) into a set of separate ones, so that each of the segments gets its own point.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)> &* **point** - Spline point to be broken. > **Notice:** The point must be shared by a least 2 segments.

## void weldSplinePoints ( Vector < Ptr < SplinePoint >> & OUT_points )

Joins all [spline points](../../../api/library/worlds/class.splinepoint_cpp.md) specified in the list into a single one, so that this point is shared by all spline segments having the specified points as starting or ending ones.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)>> &* **OUT_points** - List of spline points to be joined into a single one. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool isLinked ( const Ptr < SplinePoint > & point ) const

Returns a value indicating if the specified [spline point](../../../api/library/worlds/class.splinepoint_cpp.md) is linked to any [spline segment](../../../api/library/worlds/class.splinesegment_cpp.md).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[SplinePoint](../../../api/library/worlds/class.splinepoint_cpp.md)> &* **point** - Spline point to be checked.

### Return value

true if the specified spline point is linked to any spline segment; otherwise, false.
