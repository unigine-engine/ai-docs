# Event Handling (CPP)


When writing your application logic, one of the biggest challenges you're likely to face is connecting the various changing elements in a way that works. For example, making a character move, jump, or adding up the score can be relatively easy to do on its own. But connecting all things that happen in your game or application without making it confusing to work with can be very challenging.


The ***Event System*** enables you to create application logic that is executed when an **event** is triggered during the application execution. It allows objects to subscribe one or more of their own functions to a subject's event. Then, when the subject triggers the event, the objects' functions are called in response. Such functions are also known as **event handlers**.


The Event System features the following:


- *Strict type checking for signatures*: you can see how many and which exactly arguments an event handler function requires.
- *Compile-time checking*: it ensures that argument types match event types, preventing runtime errors.
- *Simple subscription/unsubscription to events with [lambda functions](#lambda_functions)* with no need to perform internal type conversions.
- *Automatic event unsubscription*.
- *Temporary event deactivation*: particular events can be temporarily disabled to perform specific actions without triggering them.
- *Batch management*: you can unsubscribe from several subscriptions in a single function call.


## Events


An **event** is represented by the abstract *Event* class. It serves as an interface for interaction with the event. Typically, you get this interface via a reference as **Event<args...>**, where *args* represents a list of arguments the event will pass to a handler function.


For example, **[Body::getEventPosition()](../../../api/library/physics/class.body_cpp.md#getEventPosition_Event)** returns the event with the following signature:


```cpp
Event<const Ptr<Body>&>

```


It means the handler function must receive an argument of the same type when connected with the event.


### Emulating Events


Sometimes, it is necessary to emulate events. For custom events, you can use the ***EventInvoker::run()*** function that receives the same arguments as the event and invokes its handler functions.


The following example shows how to create your event and then run it when necessary:


```cpp
class MyEventClass
{
public:

	Event<int> &getEvent() { return event; }

	void runEvent()
	{
		num_runs++;
		event.run(num_runs);
	}

private:

	int num_runs = 0;
	EventInvoker<int> event;
};

int main()
{
	MyEventClass my_class;
	EventConnections e_conn;

	my_class.getEvent().connect(
		e_conn,
		[](int n)
		{
			printf("n = %d\n", n);
		}
	);

	my_class.runEvent();
	my_class.runEvent();

	return 0;
}

```


The existing events that are implemented for built-in objects and available through API can be emulated using the corresponding ***runEvent*()*** methods (without having to use ***EventInvoker::run()***). For example, to emulate the *Show* event for a [widget](../../../api/library/gui/class.widget_cpp.md), call **[Widget::runEventShow()](../../../api/library/gui/class.widget_cpp.md#runEventShow_void)**.


```cpp
widget->runEventShow();

```


## Event Handlers


The event handler functions can receive **no more than 5** arguments.


In addition, the Event System performs strict type checking for handler function signatures: you can subscribe to the event only if the types of the function arguments match the event types. For example, in the case of the event with a single *int* argument, you are only able to link it with a handler that also accepts a single integer argument. Even if the types can be implicitly converted (as in the example), subscribing is not permitted.


```cpp
Event<int> event;	// event sugnature
void on_event(int a);	// types match, subscription is allowed
void on_event(long a);	// type mismatch, no subscription

```


This restriction also applies to the *&, const*, and *const&* modifiers. For instance, when the event type is a user class with no modifiers:


```cpp
Event<MyClass> event;
void on_event(MyClass a);			// types match, subscription is allowed
void on_event(MyClass a&);		// type mismatch
void on_event(const MyClass a&);// type mismatch

```


### Discarding Arguments


In most cases, not all arguments passed to the handler function by the event are necessary. So, events allow for **discarding unnecessary arguments** when functions subscribe to them. You can only discard one argument at a time, starting with the last one. For example, the following handler functions can subscribe to the event:


```cpp
// the event
Event<int, float, const char *, vec3, const MyClass &> event;

// the event handlers with discarded arguments
on_event(int a, float b, const char *s, vec3 v, const MyClass &c);
on_event(int a, float b, const char *s, vec3 v);
on_event(int a, float b, const char *s);
on_event(int a, float b);
on_event(int a);
on_event();

```


### Receiving Additional Arguments


To receive an additional user argument in the handler function, you need to add the required argument to the end of the handler arguments list and pass its value to the **connect()** function.


> **Notice:** There is a limitation: using references as additional arguments is not allowed. This restriction is associated with the fact that a copy of the argument is made in the [*CallbackBase*](../../../api/library/common/callbacks/class.callbackbase_cpp.md) class.


```cpp
class UserClass
{
	{ /* ... */ }
};

Event<int, float> event;
EventConnections e_conn;

void on_event_0(int a, float b, int my_var) { /* ... */ }

void on_event_1(int a, float b, UserClass c) { /* ... */ }

void on_event_2(int a, float b, UserClass *c_ptr) { /* ... */ }

void on_event(float f, const char *str) { /* ... */ }

UserClass user_class;

int main()
{
	// pass the value of the additional "my_var" argument to the handler function
	event.connect(e_conn, on_event_0, 33);
	// pass the value of the additional "c" argument to the handler function
	event.connect(e_conn, on_event_1, user_class);
	// pass the value of the additional "c_ptr" argument to the handler function
	event.connect(e_conn, on_event_2, &user_class);
	// discard the int and float handler arguments, add the custom float and const char* and pass them to connect()
	event.connect(e_conn, on_event, 33.3f, "test");

	return 0;
}

```


## Subscribing to Events


For convenience, the Event System provides the *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes that allow simple event subscription/unsubscription. Let's go through them in detail.


### Single Subscription with EventConnection


The *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* class keeps a connection between an event and its handler. For example, the connection between the event and the *free handler function* can be set as follows:


```cpp
EventConnection connection;

// a handler function
void on_event()
{
	Log::message("\Handling the event\n");
}

void init()
{
	//connect the handler function with the event by using EventConnection
	getSomeEvent().connect(connection, this, on_event);

}

```


You can temporarily **turn the event off** to perform specific actions without triggering it.


```cpp
// disable the event
getSomeEvent().setEnabled(false);

/* perform some actions */

// and enable it again
getSomeEvent().setEnabled(true);

```


Moreover, you can **toggle individual connections on and off** (*EventConnection* instances), providing flexibility when working with events.


```cpp
EventConnection connection;
/* ... */

// disable the connection
connection.setEnabled(false);

/* perform some actions */

// and enable it back when necessary
connection.setEnabled(true);

```


Later, you can unsubscribe from the event via *EventConnection* as follows:


> **Notice:** You cannot unsubscribe using the pointer to the handler function if the connection was created via *EventConnection*.


```cpp
void shutdown()
{
	// break the connection by using EventConnection
	connection.disconnect();
}

```


If *a class handles the event*, you can declare the *EventConnection* instance as a class member and use it for events subscription. In this case, all linked subscriptions will be automatically removed when the class destructor is called. For example:


<details>
<summary>Handler Class | Close</summary>

```cpp
// a class handling the event
class SomeClass
{
public:

	// instance of the EventConnection class as a class member
	EventConnection connection;

	// an event handler implemented as a class member
	void on_event()
	{
		Log::message("\Handling the event\n");
	}
};

// create a class instance
SomeClass *obj = new SomeClass();

// connect the handler function with the event by using EventConnection;
// specify the class instance as the event handler belongs to the class
getSomeEvent().connect(obj->connection, obj, &SomeClass::on_event);

/* ... */

// the instance of the handler class is deleted with all its subscriptions;
// subscriptions are removed automatically in the destructor
delete obj;

```

</details>


### Multiple Subscriptions with EventConnections


The *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* class is a container for the *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* instances. Multiple subscriptions to a single event or **different events** can be linked to a single *EventConnections* instance.


For example, you can create multiple subscriptions to a single event as follows:


```cpp
EventConnections connections;

// event handlers
static void on_some_event_0() { Log::message("\Handling the 1st event\n"); }
static void on_some_event_1() { Log::message("\Handling the 2nd event\n"); }

static void Main(string[] args)
{
	// add two handlers for the event
	// and link it to an EventConnections instance to remove a pack of subscriptions later
	getSomeEvent().connect(connections, this, on_some_event_0);
	getSomeEvent().connect(connections, this, on_some_event_1);

}

```


Also, you can create multiple subscriptions to different events:


```cpp
EventConnections connections;

// event handlers
static void on_some_event_0() { Log::message("\Handling the 1st event\n"); }
static void on_some_event_1() { Log::message("\Handling the 2nd event\n"); }
static void on_some_event_2() { Log::message("\Handling the 3rd event\n"); }

static void Main(string[] args)
{
	// subscribe for different events with handlers to be executed when the events are triggered;
	// here multiple subscriptions are linked to a single EventConnections class instance
	getSomeEvent0().connect(connections, this, on_some_event_0);
	getSomeEvent1().connect(connections, this, on_some_event_1);
	getSomeEvent2().connect(connections, this, on_some_event_2);
}

```


Later, you can unsubscribe from the events via *EventConnections* as follows:


> **Notice:** You cannot unsubscribe by using the pointer to the handler function if the connection was created via *EventConnections*.


```cpp
// break the connection by using EventConnections
// all instances of EventConnection will be removed from the EventConnections container
connections.disconnectAll();

```


If *a class handles the event*, you can declare the *EventConnections* instance as a class member and use it for events subscription. In this case, all linked subscriptions will be automatically removed when the class destructor is called. See the example provided [above](#handler_class) � the same applies to *EventConnections*.


#### Inheriting from EventConnections


There is another way to automatically unsubscribe from the event handled by a class: you can inherit it from *EventConnections*. In this case, the event will interact with the user class in the same way as with *EventConnections*. All linked subscriptions will be removed automatically in the user class destructor.


```cpp
class UserClass : public EnventConnections
{
public:

	void init(Event<int, float> &event)
	{
		event.connect(this, &UserClass::on_event);
	}

	void on_event(int a, float b)
	{
		Log::message("\Handling the event\n");
	}
};

int main()
{
	UserClass *user_class = new UserClass();
	user_class->init(getSomeEvent());
	delete user_class; // my_class will automatically unsubscribe from all of the events in the destructor

	return 0;
}

```


### Using Lambda Functions


You can pass a lambda function as an argument to the **connect()** function to handle the event: there is no need to perform internal type conversions. All features available for the handler functions are also applicable to lambda functions, except additional arguments.


```cpp
int main()
{
	// EventConnections class instance to manage event subscriptions
	EventConnections connections;

	auto l = [](int a, float b) {};

	event.connect(connections, l);

	event.connect(connections, [](int a, float b) {});

	event.connect(connections, [](int a {}));

	return 0;
}

```


### Connection Descriptors


When subscribing to the event, a connection descriptor *EventConnectionId* is returned. You can save it and use it later to unsubscribe.


> **Notice:** We do not recommend this approach. It is provided for informational purposes only.


```cpp
// EventConnections class instance to manage event subscriptions
EventConnections econnections;

// subscribe for the Contacts event with a lambda handler function and keeping connection ID
EventConnectionId contacts_handler_id = body->getEventContacts().connect(econnections, [](const Ptr<Body> & body) {
		Log::message("\Handling Contacts event (lambda).\n");
	}
);

// remove the subscription later using the ID
body->getEventContacts().disconnect(contacts_handler_id);

```


In some cases using a connection descriptor leads to a failure:


- If you are subscribed to the event via *EventConnection*, it will become invalid when unsubscribing using the connection descriptor.
- If you have multiple subscriptions linked to *EventConnections*, unsubscribing from a single event using the connection descriptor will not remove the *EventConnection* instance from the container.


## Direct Unsafe Subscription


You can subscribe to events directly via the *connectUnsafe()* function, without specifying an istance of the *EventConnection/EventConnections* class, and unsubscribe via *disconnect()*:


- The *connectUnsafe()* function is used to connect the event and the event handler. The number of function arguments may vary.
- The *disconnect()* function is used to break the connection between the event and its handler. It receives a pointer to the handler function or a connection descriptor as an argument.


```cpp
// a handler function
void on_event(int a, float b)
{
	Log::message("\Handling the event\n");
}

void init()
{
	// connect the handler function with the event directly
	getSomeEvent().connectUnsafe(on_event);

	// disconnect the handler function and the event by using the pointer to this function
	getSomeEvent().disconnect(on_event);

	// ...

	// direct connect using a lambda expression
	// and keeping a connection descriptor to remove the subscription later
	EventConnectionId connection_id = event.connectUnsafe([](int a, float b) {});

	// disconnect the handler function and the event by using connection descriptor
	getSomeEvent().disconnect(connection_id);

	return 0;
}

```


If *a class handles the event*, you should pass the class instance as an argument to the *connect()* and *disconnect()* functions. For example:


<details>
<summary>Handler Class | Close</summary>

```cpp
// a class handling the event
class SomeClass
{
public:

	// an event handler implemented as a class member
	void on_event()
	{
		Log::message("\Handling the event\n");
	}
};

// create a class instance
SomeClass *obj = new SomeClass();

// connect the handler function with the event;
// specify the class instance as the event handler belongs to the class
getSomeEvent().connectUnsafe(obj, &SomeClass::on_event);

/* ... */

// remove the subscription
getSomeEvent().disconnect(obj, &SomeClass::on_event);

```

</details>


## Using Predefined Events


Some Unigine API members have several predefined events that can be handled in specific cases. The following chapters showcase the practical use of the concepts described above.


### Triggers


Triggers are used to detect changes in nodes position or state. Unigine offers three types of built-in triggers:


- *[**NodeTrigger**](../../../api/library/nodes/class.nodetrigger_cpp.md)* triggers events when the trigger node is [enabled](../../../api/library/nodes/class.nodetrigger_cpp.md#getEventEnabled_Event) or its [position](../../../api/library/nodes/class.nodetrigger_cpp.md#getEventPosition_Event) has changed.
- *[**WorldTrigger**](../../../api/library/worlds/class.worldtrigger_cpp.md)* triggers events when any node (collider or not) gets [inside](../../../api/library/worlds/class.worldtrigger_cpp.md#getEventEnter_Event) or [outside](../../../api/library/worlds/class.worldtrigger_cpp.md#getEventLeave_Event) it. > **Notice:** **World Triggers** detect only the nodes with *Triggers Interaction* enabled - either in the Editor or via API using *[setTriggerInteractionEnabled()](../../../api/library/nodes/class.node_cpp.md#setTriggerInteractionEnabled_int_void)*.
- *[**PhysicalTrigger**](../../../api/library/physics/class.physicaltrigger_cpp.md)* triggers events when physical objects get [inside](../../../api/library/physics/class.physicaltrigger_cpp.md#getEventEnter_Event) or [outside](../../../api/library/physics/class.physicaltrigger_cpp.md#getEventLeave_Event) it.


Here is a simple *NodeTrigger* usage example. The event handlers are set via pointers specified when subscribing to the following events: *[EventEnabled](../../../api/library/nodes/class.nodetrigger_cpp.md#getEventEnabled_Event)* and *[EventPosition](../../../api/library/nodes/class.nodetrigger_cpp.md#getEventPosition_Event)*.


<details>
<summary>AppWorldLogic.h | Close</summary>

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

</details>


<details>
<summary>AppWorldLogic.cpp | Close</summary>

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

</details>


And here is an example of *WorldTrigger* that demonstrates how to subscribe to the *Enter* and *Leave* events with a corresponding handler and keep this connection to unsubscribe later.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

```cpp
WorldTriggerPtr trigger;
EventConnections event_connections;

// implement the Enter event handler
void AppWorldLogic::enter_event_handler(const NodePtr &node)
{
	Log::message("\nA node named %s has entered the trigger\n", node->getName());
}

// implement the Leave event handler
void AppWorldLogic::leave_event_handler1(const NodePtr &node)
{
	Log::message("\nA node named %s has left the trigger\n", node->getName());
}

// implement an additional Leave event handler
void AppWorldLogic::leave_event_handler2(const NodePtr &node)
{
	Log::message("\nAdditional Leave event handler.\n");
}

int AppWorldLogic::init()
{

	// create a world trigger node
	trigger = WorldTrigger::create(Math::vec3(3.0f));

	// add the Enter event handler to be executed when a node enters the world trigger
	// and attaching it to EventConnections instance to remove a pack of subscriptions later
	trigger->getEventEnter().connect(event_connections, this, &AppWorldLogic::enter_event_handler);
	// adding two handlers for the Leave event to be executed when a node leaves the world trigger
	// and attaching it to the same EventConnections instance as well
	trigger->getEventLeave().connect(event_connections, this, &AppWorldLogic::leave_event_handler1);
	trigger->getEventLeave().connect(event_connections, this, &AppWorldLogic::leave_event_handler2);

	return 1;
}

```

</details>


To remove subscriptions to the events, use the following code:


```cpp
// remove all subscriptions to the Leave and Enter events
event_connections.disconnectAll();


```


### Widgets


The widgets base class *[**Widget**](../../../api/library/gui/class.widget_cpp.md)* allows subscribing to events.


The example below demonstrates how to subscribe for the widget's *Clicked* event.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
// event handler function
int AppWorldLogic::onButtonClicked()
{
	Log::message("\nThe widget button has been clicked\n");

	return 1;
}

// EventConnections class instance to manage event subscriptions
EventConnections e_conn;

int AppWorldLogic::init()
{

	// get a pointer to the system GUI
	GuiPtr gui = Gui::getCurrent();
	// create a button widget and set its caption
	WidgetButtonPtr widget_button = WidgetButton::create(gui, "Press me");
	// set a tooltip
	widget_button->setToolTip("Click this button");
	// rearrange a button size
	widget_button->arrange();
	// set a button position
	widget_button->setPosition(10, 10);
	// set the onButtonClicked function to handle the CLICKED event
	widget_button->getEventClicked().connect(e_conn, this, &AppWorldLogic::onButtonClicked);
	// add the created button widget to the system GUI
	gui->addChild(widget_button, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

	return 1;
}

```

</details>


### Physics


You can track certain events of the physics-related [Bodies](../../../api/library/physics/class.body_cpp.md) and [Joints](../../../api/library/physics/class.joint_cpp.md):


- ****[Body::getEventFrozen()](../../../api/library/physics/class.body_cpp.md#getEventFrozen_Event)**** to track an event when a body freezes.
- ****[Body::getEventPosition()](../../../api/library/physics/class.body_cpp.md#getEventPosition_Event)**** to track an event when a body changes its position.
- ****[Body::getEventContactEnter()](../../../api/library/physics/class.body_cpp.md#getEventContactEnter_Event)**** to track an event when a contact emerges (body starts touching another body or collidable surface).
- ****[Body::getEventContactLeave()](../../../api/library/physics/class.body_cpp.md#getEventContactLeave_Event)**** to track an event when a contact ends (body stops touching another body or collidable surface).
- ****[Body::getEventContacts()](../../../api/library/physics/class.body_cpp.md#getEventContacts_Event)**** to get **all contacts** of the body including new ones (*enter*) and the ending ones (*leave*). Leave contacts are removed after the callback execution stage, so this is the only point where you can still get them.
- ****[Joint::getEventBroken()](../../../api/library/physics/class.joint_cpp.md#getEventBroken_Event)**** to track an event when a joint breaks.


The following code example shows how to subscribe to the Body events.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
// set the node's albedo color to red on the freezing event
int AppWorldLogic::frozen_event_handler(const BodyPtr &body)
{
	body->getObject()->setMaterialParameterFloat4("albedo_color", Math::vec4(1.0f, 0.0f, 0.0f, 1.0f), 0);

	return 1;
}

// set the node's albedo color to blue on the position change event
int AppWorldLogic::position_event_handler(const BodyPtr &body)
{
	body->getObject()->setMaterialParameterFloat4("albedo_color", Math::vec4(0.0f, 0.0f, 1.0f, 1.0f), 0);

	return 1;
}

// set the node's albedo color to yellow on each contact
int AppWorldLogic::contact_enter_event_handler(const BodyPtr &body, int num)
{
	body->getObject()->setMaterialParameterFloat4("albedo_color", Math::vec4(1.0f, 1.0f, 0.0f, 1.0f), 0);

	return 1;
}

// EventConnections class instance to manage event subscriptions
EventConnections e_conn;

int AppWorldLogic::init()
{

	// create a box
	ObjectMeshStaticPtr meshStatic = ObjectMeshStatic::create("core/meshes/box.mesh");
	meshStatic->setPosition(Math::Vec3(0, 0, 5.0f));
	// add a rigid body to the box
	BodyRigidPtr body = BodyRigid::create(meshStatic);
	// subscribe for body events
	body->getEventFrozen().connect(e_conn, this, &AppWorldLogic::frozen_event_handler);
	body->getEventPosition().connect(e_conn, this, &AppWorldLogic::position_event_handler);
	body->getEventContactEnter().connect(e_conn, this, &AppWorldLogic::contact_enter_event_handler);
	// add a shape to the body
	ShapeBoxPtr shape = ShapeBox::create(body, Math::vec3(1.0f));

	return 1;
}

```

</details>


> **Notice:** Physics-based events are executed in the main thread, as they are mainly used for creation, destruction or modification of other objects.


### Properties


Events can be used to determine actions to be performed when adding or removing node and surface properties as well as when swapping node properties. Here is an example demonstrating how to track adding a node property via events.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
void AppWorldLogic::node_property_added(const NodePtr &node, const PropertyPtr &property)
{
	Log::message("Property \"%s\" was added to the node named \"%s\".\n", property->getName(), node->getName());
}

void AppWorldLogic::parameter_changed(const PropertyPtr &property, int num)
{
	Log::message("Parameter \"%s\" of the property \"%s\" has changed its value.\n", property->getParameterPtr(num)->getName(), property->getName());
}

void AppWorldLogic::property_removed(const PropertyPtr &property)
{
	Log::message("Property \"%s\" was removed.\n", property->getName());
}

// EventConnections class instance to manage event subscriptions
EventConnections e_conn;

int AppWorldLogic::init()
{

	NodeDummyPtr node = NodeDummy::create();

	// search for a property named "new_property_0"
	PropertyPtr property = Properties::findProperty("new_property_0");

	// subscribing to the PropertyNodeAdd event (adding a node property)
	node->getEventPropertyNodeAdd().connect(e_conn, this, &AppWorldLogic::node_property_added);

	// add the property named "new_property_0" to the node
	node->addProperty("new_property_0");

	// subscribing to the ParameterChanged event (changing property parameter)
	property->getEventParameterChanged().connect(e_conn, this, &AppWorldLogic::parameter_changed);

	// change the value of the "my_int_param" parameter
	property->getParameterPtr("my_int_param")->setValueInt(3);

	// inherit a new property named "new_property_1" from the base property "surface_base"
	Properties::findManualProperty("surface_base")->inherit("new_property_1");

	// subscribing to property removal
	Properties::getEventRemoved().connect(e_conn, this, &AppWorldLogic::property_removed);

	// remove the property named "new_property_1"
	Properties::removeProperty(Properties::findProperty("new_property_1")->getGUID());

	return 1;
}

```

</details>
