# Unigine::WorldTrigger Class (CPP)

**Header:** #include <UnigineWorlds.h>

**Inherits from:** Node


***World Trigger*** triggers events when any nodes (colliders or not) get inside or outside it. The trigger can detect a node of any type by its bounding box.


> **Notice:** **[World Triggers](../../../objects/worlds/world_trigger/index.md)** detect only the nodes with *Triggers Interaction* enabled - either in the Editor or via API using *[setTriggerInteractionEnabled()](../../../api/library/nodes/class.node_cpp.md#setTriggerInteractionEnabled_int_void)*.


You can either [specify a list of nodes](#setTargetNodes_SETNode_void), for which the event handlers will be executed, or let the trigger react to all nodes (default behavior). In the latter case, the list of target nodes should be empty. There can be also specified a [list of nodes](#setExcludeNodes_SETNode_void) that are skipped by the trigger and are free to pass unnoticed.


The handler function of *World Trigger* is actually executed only when the next engine function is called: that is, before *[updatePhysics()](../../../code/fundamentals/execution_sequence/main_loop.md#physics_updatePhysics)* (in the current frame) or before *[update()](../../../code/fundamentals/execution_sequence/main_loop.md#world_update)* (in the next frame) � whatever comes first.


> **Notice:** If you have moved some nodes and want to execute event handlers based on changed positions in the same frame, you need to call *[World::updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* first.


### Example


The example below allows creating a line of boxes moving in and out of the World Trigger area and triggering the events. Getting inside the World Trigger enables emission for the boxes, and getting out of it disables the emission.


```cpp
// AppWorldLogic.cpp
/* .. */
#include "AppWorldLogic.h"
#include <UnigineObjects.h>
#include <UnigineGame.h>
#include <UnigineVisualizer.h>

using namespace Unigine;

using namespace Math;

WorldTriggerPtr trigger;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

const int MAX_OBJECTS = 10;
Vector<ObjectMeshStaticPtr> objects;

static void set_state(const NodePtr& node, const char* name, int value)
{
	ObjectPtr object = checked_ptr_cast<Object>(node);
	if (object.get() == NULL)
		return;

	for (int i = 0; i < object->getNumSurfaces(); i++)
	{
		MaterialPtr material = object->getMaterialInherit(i);
		if (material.get() == NULL)
			continue;
		int id = material->findState(name);
		if (id != -1)
			material->setState(id, value);
	}
}

static void trigger_enter(const NodePtr &node)
{
	set_state(node, "emission", 1);
}

static void trigger_leave(const NodePtr &node)
{
	set_state(node, "emission", 0);
}

int AppWorldLogic::init()
{

	// create trigger
	trigger = WorldTrigger::create(vec3(3.0f));

	trigger->getEventEnter().connect(econnections, &trigger_enter);
	trigger->getEventLeave().connect(econnections, &trigger_leave);

	// create objects
	for (int i = 0; i < MAX_OBJECTS; i++)
	{
		ObjectMeshStaticPtr mesh = ObjectMeshStatic::create("cbox.mesh");
		mesh->setTriggerInteractionEnabled(true);
		mesh->setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);
		objects.append(mesh);
	}

	// enable the visualizer
	Visualizer::setEnabled(true);

	return 1;
}

int AppWorldLogic::update()
{

	trigger->renderVisualizer();
	float time = Game::getTime();

	float hsize = objects.size() / 2.0f;

	for (int i = 0; i < objects.size(); i++)
	{
		float x = Math::sin(time) * hsize - hsize + i;
		objects[i]->setWorldTransform(translate(Vec3(x, -x, 0.0f)));
	}

	return 1;
}

int AppWorldLogic::shutdown()
{

	objects.clear();

	// removing all event subscriptions somewhere on shutdown
	econnections.disconnectAll();

	return 1;
}


```


### See Also


- Video tutorial on [How To Use World Triggers to Detect Nodes by Their Bounds](../../../videotutorials/how_to/how_to_cs/world_trigger.md)
- Article on [Event Handling](../../../code/fundamentals/events/index_cpp.md#triggers)
- C++ sample
- C# Component sample
- UnigineScript samples:

  -
  -
  -


## WorldTrigger Class

### Members

## void setLeaveCallbackName ( const char * name )

Sets a new name of the handler function name to be executed on leaving the world trigger. This handler function is set via [getEventLeave()](#getEventLeave_Event).
### Arguments

- *const char ** **name** - The name of the handler function name to be executed on leaving the world trigger.

## const char * getLeaveCallbackName () const

Returns the current name of the handler function name to be executed on leaving the world trigger. This handler function is set via [getEventLeave()](#getEventLeave_Event).
### Return value

Current name of the handler function name to be executed on leaving the world trigger.
## void setEnterCallbackName ( const char * name )

Sets a new name of handler function to be executed on entering the world trigger. This handler function is set via [getEventEnter()](#getEventEnter_Event).
### Arguments

- *const char ** **name** - The world script function name.

## const char * getEnterCallbackName () const

Returns the current name of handler function to be executed on entering the world trigger. This handler function is set via [getEventEnter()](#getEventEnter_Event).
### Return value

Current world script function name.
## int getNumNodes () const

Returns the current number of nodes contained in the world trigger.
### Return value

Current number of nodes contained in the world trigger.
## void setSize ( const Math:: vec3 & size )

Sets a new current dimensions of the world trigger.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The current dimensions of the world trigger.

## Math:: vec3 getSize () const

Returns the current current dimensions of the world trigger.
### Return value

Current current dimensions of the world trigger.
## void setTouch ( bool touch )

Sets a new value indicating if a touch mode is enabled for the trigger. With this mode on, the trigger will react to the node by partial contact. When set to off, the trigger reacts only if the whole bounding sphere/box gets inside or outside of it.
### Arguments

- *bool* **touch** - Set **true** to enable the touch mode for the trigger; **false** - to disable it.

## bool isTouch () const

Returns the current value indicating if a touch mode is enabled for the trigger. With this mode on, the trigger will react to the node by partial contact. When set to off, the trigger reacts only if the whole bounding sphere/box gets inside or outside of it.
### Return value

**true** if the touch mode for the trigger is enabled ; otherwise **false**.
## Event<const Ptr < Node > &> getEventLeave () const

event triggered when a node leaves the world trigger. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Leave event handler
void leave_event_handler(const Ptr<Node> & node)
{
	Log::message("\Handling Leave event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections leave_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventLeave().connect(leave_event_connections, leave_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventLeave().connect(leave_event_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling Leave event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
leave_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection leave_event_connection;

// subscribe to the Leave event with a handler function keeping the connection
publisher->getEventLeave().connect(leave_event_connection, leave_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
leave_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
leave_event_connection.setEnabled(true);

// ...

// remove subscription to the Leave event via the connection
leave_event_connection.disconnect();

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

	// A Leave event handler implemented as a class member
	void event_handler(const Ptr<Node> & node)
	{
		Log::message("\Handling Leave event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventLeave().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId leave_handler_id;

// subscribe to the Leave event with a lambda handler function and keeping connection ID
leave_handler_id = publisher->getEventLeave().connect(e_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling Leave event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventLeave().disconnect(leave_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Leave events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventLeave().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventLeave().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < Node > &> getEventEnter () const

event triggered when a node enters the world trigger. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Node> & **node**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Enter event handler
void enter_event_handler(const Ptr<Node> & node)
{
	Log::message("\Handling Enter event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enter_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEnter().connect(enter_event_connections, enter_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEnter().connect(enter_event_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling Enter event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
enter_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection enter_event_connection;

// subscribe to the Enter event with a handler function keeping the connection
publisher->getEventEnter().connect(enter_event_connection, enter_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
enter_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
enter_event_connection.setEnabled(true);

// ...

// remove subscription to the Enter event via the connection
enter_event_connection.disconnect();

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

	// A Enter event handler implemented as a class member
	void event_handler(const Ptr<Node> & node)
	{
		Log::message("\Handling Enter event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEnter().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId enter_handler_id;

// subscribe to the Enter event with a lambda handler function and keeping connection ID
enter_handler_id = publisher->getEventEnter().connect(e_connections, [](const Ptr<Node> & node) {
		Log::message("\Handling Enter event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEnter().disconnect(enter_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Enter events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEnter().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEnter().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static WorldTriggerPtr create ( const Math:: vec3 & size )

Constructor. Creates a new world trigger with given dimensions.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Dimensions of the new world trigger. If negative values are provided, **0** will be used instead of them.

## void setExcludeNodes ( const Set < Ptr < Node >> & nodes )

Sets a list of excluded nodes, on which the world trigger will not react.
### Arguments

- *const [Set](../../../api/library/containers/class.set_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - Exclude nodes vector.

## Set < Ptr < Node >> getExcludeNodes ( ) const

Returns the current list of excluded nodes, on which the world trigger does not react.
### Arguments

## void setExcludeTypes ( const Set <int> & types )

Sets a list of excluded node types, on which the world trigger will not react.
### Arguments

- *const [Set](../../../api/library/containers/class.set_cpp.md)<int> &* **types** - Exclude node types vector.

## Set <int> getExcludeTypes ( ) const

Returns the current list of excluded node types, on which the world trigger does not react.
### Arguments

## Ptr < Node > getNode ( int num ) const

Returns a specified node contained in the world trigger.
```cpp
#include <UnigineWorlds.h>

#include <UnigineInput.h>

using namespace Unigine;

WorldTriggerPtr trigger;

int AppWorldLogic::init()
{

	// create a world trigger node
	trigger = WorldTrigger::create(Math::vec3(3.0f));

	return 1;
}

int AppWorldLogic::update()
{
	// press the i key to get the info about nodes inside the trigger
	if (trigger && Input::isKeyDown(Input::KEY_I))
	{
		//get the number of nodes inside the trigger
		int numNodes = trigger->getNumNodes();
		Log::message("The number of nodes inside the trigger is %i \n", numNodes);

		//loop through all nodes to print their names and types
		for (int i = 0; i < numNodes; i++)
		{
			NodePtr node = trigger->getNode(i);
			Log::message("The type of the %f node is %f \n", node->getName(), node->getType());
		}
	}
	return 1;
}


```


### Arguments

- *int* **num** - Node number in range from 0 to the total number of nodes.

### Return value

Node pointer.
## Vector < Ptr < Node >> getNodes ( ) const

Gets nodes contained in the trigger.
### Arguments

## void setTargetNodes ( const Set < Ptr < Node >> & nodes )

Sets a list of target nodes, which will fire callbacks. If this list is empty, all nodes fire callbacks.
### Arguments

- *const [Set](../../../api/library/containers/class.set_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **nodes** - Target nodes vector.

## Set < Ptr < Node >> getTargetNodes ( ) const

Returns the current list of target nodes, which fire callbacks. If this list is empty, all nodes fire callbacks.
### Arguments

## void setTargetTypes ( const Set <int> & types )

Sets a list of target node types, which will fire callbacks. If this list is empty, all nodes fire callbacks.
### Arguments

- *const [Set](../../../api/library/containers/class.set_cpp.md)<int> &* **types** - Target node types vector.

## Set <int> getTargetTypes ( ) const

Returns the current list of target node types, which fire callbacks. If this list is empty, all nodes fire callbacks.
### Arguments

## static int type ( )

Returns the type of the node.
### Return value

[World](../../../api/library/engine/class.world_cpp.md) type identifier.
