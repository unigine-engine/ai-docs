# Unigine::NodeTrigger Class (CPP)

**Header:** #include <UnigineNodes.h>

**Inherits from:** Node


A *[Trigger](../../../objects/nodes/trigger/index.md)* node is a zero-sized node that has no visual representation and triggers events when:


- It is enabled/disabled (the *Enabled* event is triggered).
- Its transformation is changed (the *Position* event is triggered).


The *Trigger* node is usually added as a child node to another node, so that the handler functions were executed on the parent node enabling/disabling or transforming.


For example, to detect if some node has been enabled (for example, a world clutter node that renders nodes only around the camera that has enabled it), the *Trigger* node is added as a child to this node and executes the corresponding function.


### Creating a Trigger Node


To create a *Trigger* node, simply call the NodeTrigger [constructor](#NodeTrigger) and then add the node as a child to another node, for which handlers should be executed.


```cpp
#include <UnigineLogic.h>

using namespace Unigine;

class AppWorldLogic : public Unigine::WorldLogic {

public:

	virtual int init();
	virtual int update();

	/*...*/

private:

	ObjectMeshStaticPtr object;
	NodeTriggerPtr trigger;

	// EventConnections class instance to manage event subscriptions
	EventConnections econnections;
};

```


```cpp
#include "AppWorldLogic.h"

using namespace Math;

int AppWorldLogic::init() {

	// create a mesh
	object = ObjectMeshStatic::create("core/meshes/box.mesh");
	// change material albedo color
	object->setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);

	// create a trigger node
	trigger = NodeTrigger::create();

	// add the trigger node to the static mesh as a child node
	object->addWorldChild(trigger);

	return 1;
}


```


### Editing a Trigger Node


Editing a trigger node includes implementing and specifying the *Enabled* and *Position* event handlers that are executed on enabling or positioning the *Trigger* node correspondingly.


The event handler must receive at least **1** argument of the *NodeTrigger* type. In addition, it can also take another 2 arguments of any type.


The event handlers are set via pointers specified when subscribing to the following events: *[EventEnabled](#getEventEnabled_Event)* and *[EventPosition](#getEventPosition_Event)*.


```cpp
#include <UnigineLogic.h>
#include <UnigineGame.h>

using namespace Unigine;

class AppWorldLogic : public Unigine::WorldLogic {

public:

	virtual int init();
	virtual int update();

	/*...*/

private:

	ObjectMeshStaticPtr object;
	NodeTriggerPtr trigger;

	// EventConnections class instance to manage event subscriptions
	EventConnections econnections;

	void position_event_handler(const NodeTriggerPtr &trigger)
	{
		Log::message("Object position has been changed. New position is: (%f %f %f)\n", trigger->getWorldPosition().x, trigger->getWorldPosition().y, trigger->getWorldPosition().z);
	}

	void enabled_event_handler(const NodeTriggerPtr &trigger)
	{
		Log::message("The enabled flag is %d\n", trigger->isEnabled());
	}
};

```


```cpp
#include "AppWorldLogic.h"

using namespace Math;

int AppWorldLogic::init() {

	// create a mesh
	object = ObjectMeshStatic::create("core/meshes/box.mesh");
	// change material albedo color
	object->setMaterialParameterFloat4("albedo_color", vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);

	// create a trigger node
	trigger = NodeTrigger::create();

	// add the trigger node to the static mesh as a child node
	object->addWorldChild(trigger);

	// subscribe for the Enabled and Position events
	trigger->getEventEnabled().connect(econnections, this, &AppWorldLogic::enabled_event_handler);
	trigger->getEventPosition().connect(econnections, this, &AppWorldLogic::position_event_handler);

	return 1;
}

int AppWorldLogic::update()
{

	float time = Game::getTime();
	Vec3 pos = Vec3(Math::sin(time) * 2.0f, Math::cos(time) * 2.0f, 0.0f);
	object->setEnabled(pos.x > 0.0f || pos.y > 0.0f);
	object->setWorldPosition(pos);

	return 1;
}


```


### See Also


- Video tutorial on [How To Use Node Triggers to Detect Changes in Node States](../../../videotutorials/how_to/how_to_cs/node_trigger.md)
- Article on [Event Handling](../../../code/fundamentals/events/index_cpp.md#triggers)
- C++ sample
- C# Component sample


## NodeTrigger Class

### Members

## Event<const Ptr < NodeTrigger > &> getEventPosition () const

Event triggered when the trigger node position has changed. The event handler must receive a *NodeTrigger* as its first argument. In addition, it can also take **2** arguments of any type. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<NodeTrigger> & **trigger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Position event handler
void position_event_handler(const Ptr<NodeTrigger> & trigger)
{
	Log::message("\Handling Position event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections position_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventPosition().connect(position_event_connections, position_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventPosition().connect(position_event_connections, [](const Ptr<NodeTrigger> & trigger) {
		Log::message("\Handling Position event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
position_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection position_event_connection;

// subscribe to the Position event with a handler function keeping the connection
publisher->getEventPosition().connect(position_event_connection, position_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
position_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
position_event_connection.setEnabled(true);

// ...

// remove subscription to the Position event via the connection
position_event_connection.disconnect();

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

	// A Position event handler implemented as a class member
	void event_handler(const Ptr<NodeTrigger> & trigger)
	{
		Log::message("\Handling Position event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventPosition().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId position_handler_id;

// subscribe to the Position event with a lambda handler function and keeping connection ID
position_handler_id = publisher->getEventPosition().connect(e_connections, [](const Ptr<NodeTrigger> & trigger) {
		Log::message("\Handling Position event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventPosition().disconnect(position_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Position events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventPosition().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventPosition().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < NodeTrigger > &> getEventEnabled () const

Event triggered when the trigger node is enabled or disabled. The event handler must receive a *NodeTrigger* as its first argument. In addition, it can also take **2** arguments of any type. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<NodeTrigger> & **trigger**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Enabled event handler
void enabled_event_handler(const Ptr<NodeTrigger> & trigger)
{
	Log::message("\Handling Enabled event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enabled_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEnabled().connect(enabled_event_connections, enabled_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEnabled().connect(enabled_event_connections, [](const Ptr<NodeTrigger> & trigger) {
		Log::message("\Handling Enabled event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
enabled_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection enabled_event_connection;

// subscribe to the Enabled event with a handler function keeping the connection
publisher->getEventEnabled().connect(enabled_event_connection, enabled_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
enabled_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
enabled_event_connection.setEnabled(true);

// ...

// remove subscription to the Enabled event via the connection
enabled_event_connection.disconnect();

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

	// A Enabled event handler implemented as a class member
	void event_handler(const Ptr<NodeTrigger> & trigger)
	{
		Log::message("\Handling Enabled event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEnabled().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId enabled_handler_id;

// subscribe to the Enabled event with a lambda handler function and keeping connection ID
enabled_handler_id = publisher->getEventEnabled().connect(e_connections, [](const Ptr<NodeTrigger> & trigger) {
		Log::message("\Handling Enabled event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEnabled().disconnect(enabled_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Enabled events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEnabled().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEnabled().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static NodeTriggerPtr create ( )

Constructor. Creates a new trigger node.
## void setEnabledCallbackName ( const char * name )

Sets a callback function to be fired when the trigger node is enabled. The callback function must be implemented in the world script (on the UnigineScript side). The callback function can take no arguments, a *[Node](../../../api/library/nodes/class.node_cpp.md)*or a *NodeTrigger*.
> **Notice:** The method allows for setting a callback with **0** or **1** argument only.

On UnigineScript side:
```cpp
// implement the enabled callback
void enabled_callback(Node node) {
	log.message("The enabled flag is %d\n", node.isEnabled());
}

```

 On C++ side:
```cpp
int AppWorldLogic::init() {

	// create a trigger node
	trigger = NodeTrigger::create();

	// set the enabled event handler function to be executed when the node is enabled/disabled

	trigger->setEnabledCallbackName("enabled_event_handler");

	return 1;
}


```


### Arguments

- *const char ** **name** - Name of the callback function implemented in the world script (UnigineScript side).

## const char * getEnabledCallbackName ( ) const

Returns the name of callback function to be fired on enabling the trigger node. This callback function is set via *[setEnabledCallbackName()](#setEnabledCallbackName_cstr_void)*.
### Return value

Name of the callback function implemented in the world script (UnigineScript side).
## void setPositionCallbackName ( const char * name )

Sets a callback function to be fired when the trigger node position has changed. The callback function must be implemented in the world script (on the UnigineScript side). The callback function can take no arguments, a *[Node](../../../api/library/nodes/class.node_cpp.md)*or a *NodeTrigger*.
> **Notice:** The method allows for setting a callback with **0** or **1** argument only.

On UnigineScript side:
```cpp
// implement the position callback
void position_changed(NodeTriggerPtr trigger) {
	log.message("A new position of the node is %s\n", typeinfo(node.getWorldPosition()));
}

```

 On C++ side:
```cpp
int AppWorldLogic::init() {

	// create a trigger node
	trigger = NodeTrigger::create();

	// set the position event handler function to be executed when the node position is changed

	trigger->setPositionCallbackName("position_event_handler");

	return 1;
}


```


### Arguments

- *const char ** **name** - Name of the callback function implemented in the world script (UnigineScript side).

## const char * getPositionCallbackName ( ) const

Returns the name of callback function to be fired on changing the trigger node position. This function is set by using the *[setPositionCallbackName()](#setPositionCallbackName_cstr_void)*function.
### Return value

Name of the callback function implemented in the world script (UnigineScript side).
## static int type ( )

Returns the type of the node.
### Return value

 *[NodeTrigger](../../../api/library/nodes/class.node_cpp.md#NODE_TRIGGER)*type identifier.
