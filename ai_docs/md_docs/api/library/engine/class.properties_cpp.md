# Unigine::Properties Class (CPP)

**Header:** #include <UnigineProperties.h>

> **Notice:** This class is a singleton.


The functions below are used to control property loading and management within the project: you can [get](#getProperty_int_Property), [clone](#cloneProperty_UGUID_cstr_cstr_Property), [inherit](#inheritProperty_UGUID_cstr_cstr_Property), or [remove](#removeProperty_UGUID_int_int_int) any property within the project. [Reparenting](#reparentProperty_UGUID_UGUID_int_int) is supported for all [non-manual](../../../api/library/common/class.property_cpp.md#isManual_int) and [editable](../../../api/library/common/class.property_cpp.md#isEditable_int) properties.


You can also [subscribe for such events](#callbacks) to handle them.


> **Notice:** To modify a single property, use functions of the *[Property](../../../api/library/common/class.property_cpp.md)* class.


### Handling Events


You can subscribe for events to track any changes made to any property and perform certain actions. The signature of the handler function must be as follows:


```cpp
void handler_function_name(const PropertyPtr &property);
```


Here is an example of tracking property removal via events:


```cpp
void AppWorldLogic::property_removed(const PropertyPtr &property)
{
	Log::message("Property \"%s\" was removed.\n", property->getName());
}

// somewhere in the code

// inherit a new property named "new_property_1" from the base property "surface_base"
Properties::findManualProperty("surface_base")->inherit("new_property_1");

// subscribing for property removal
Properties::getEventRemoved().connect(this, &AppWorldLogic::property_removed);

// remove the property named "new_property_1"
Properties::removeProperty(Properties::findProperty("new_property_1")->getGUID());

```


## Properties Class

### Members

## int getNumProperties () const

Returns the current total number of properties loaded for the project.
### Return value

Current total number of properties loaded for the project.
## static Event<const Ptr < Property > &> getEventRemoved () const

event triggered when a property is removed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Removed event handler
void removed_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Removed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections removed_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties::getEventRemoved().connect(removed_event_connections, removed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties::getEventRemoved().connect(removed_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Removed event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
removed_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection removed_event_connection;

// subscribe to the Removed event with a handler function keeping the connection
Properties::getEventRemoved().connect(removed_event_connection, removed_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
removed_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
removed_event_connection.setEnabled(true);

// ...

// remove subscription to the Removed event via the connection
removed_event_connection.disconnect();

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

	// A Removed event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Removed event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Properties::getEventRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId removed_handler_id;

// subscribe to the Removed event with a lambda handler function and keeping connection ID
removed_handler_id = Properties::getEventRemoved().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Removed event (lambda).\n");
	}
);

// remove the subscription later using the ID
Properties::getEventRemoved().disconnect(removed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Removed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties::getEventRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Properties::getEventRemoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Property > &> getEventReparented () const

event triggered when the parent of a property is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Reparented event handler
void reparented_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Reparented event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections reparented_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties::getEventReparented().connect(reparented_event_connections, reparented_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties::getEventReparented().connect(reparented_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Reparented event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
reparented_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection reparented_event_connection;

// subscribe to the Reparented event with a handler function keeping the connection
Properties::getEventReparented().connect(reparented_event_connection, reparented_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
reparented_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
reparented_event_connection.setEnabled(true);

// ...

// remove subscription to the Reparented event via the connection
reparented_event_connection.disconnect();

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

	// A Reparented event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Reparented event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Properties::getEventReparented().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId reparented_handler_id;

// subscribe to the Reparented event with a lambda handler function and keeping connection ID
reparented_handler_id = Properties::getEventReparented().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Reparented event (lambda).\n");
	}
);

// remove the subscription later using the ID
Properties::getEventReparented().disconnect(reparented_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Reparented events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties::getEventReparented().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Properties::getEventReparented().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Property > &> getEventRenamed () const

event triggered when the [name](../../../api/library/common/class.property_cpp.md#name_path) of a property is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Renamed event handler
void renamed_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Renamed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections renamed_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties::getEventRenamed().connect(renamed_event_connections, renamed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties::getEventRenamed().connect(renamed_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Renamed event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
renamed_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection renamed_event_connection;

// subscribe to the Renamed event with a handler function keeping the connection
Properties::getEventRenamed().connect(renamed_event_connection, renamed_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
renamed_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
renamed_event_connection.setEnabled(true);

// ...

// remove subscription to the Renamed event via the connection
renamed_event_connection.disconnect();

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

	// A Renamed event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Renamed event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Properties::getEventRenamed().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId renamed_handler_id;

// subscribe to the Renamed event with a lambda handler function and keeping connection ID
renamed_handler_id = Properties::getEventRenamed().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Renamed event (lambda).\n");
	}
);

// remove the subscription later using the ID
Properties::getEventRenamed().disconnect(renamed_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Renamed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties::getEventRenamed().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Properties::getEventRenamed().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Property > &> getEventMoved () const

event triggered when the [path](../../../api/library/common/class.property_cpp.md#name_path) of a property is changed. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Moved event handler
void moved_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Moved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections moved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties::getEventMoved().connect(moved_event_connections, moved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties::getEventMoved().connect(moved_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Moved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
moved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection moved_event_connection;

// subscribe to the Moved event with a handler function keeping the connection
Properties::getEventMoved().connect(moved_event_connection, moved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
moved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
moved_event_connection.setEnabled(true);

// ...

// remove subscription to the Moved event via the connection
moved_event_connection.disconnect();

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

	// A Moved event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Moved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Properties::getEventMoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId moved_handler_id;

// subscribe to the Moved event with a lambda handler function and keeping connection ID
moved_handler_id = Properties::getEventMoved().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Moved event (lambda).\n");
	}
);

// remove the subscription later using the ID
Properties::getEventMoved().disconnect(moved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Moved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties::getEventMoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Properties::getEventMoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Ptr < Property > &> getEventCreated () const

event triggered when a new property is created. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<Property> & **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Created event handler
void created_event_handler(const Ptr<Property> & property)
{
	Log::message("\Handling Created event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections created_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties::getEventCreated().connect(created_event_connections, created_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties::getEventCreated().connect(created_event_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Created event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
created_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection created_event_connection;

// subscribe to the Created event with a handler function keeping the connection
Properties::getEventCreated().connect(created_event_connection, created_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
created_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
created_event_connection.setEnabled(true);

// ...

// remove subscription to the Created event via the connection
created_event_connection.disconnect();

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

	// A Created event handler implemented as a class member
	void event_handler(const Ptr<Property> & property)
	{
		Log::message("\Handling Created event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Properties::getEventCreated().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId created_handler_id;

// subscribe to the Created event with a lambda handler function and keeping connection ID
created_handler_id = Properties::getEventCreated().connect(e_connections, [](const Ptr<Property> & property) {
		Log::message("\Handling Created event (lambda).\n");
	}
);

// remove the subscription later using the ID
Properties::getEventCreated().disconnect(created_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Created events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties::getEventCreated().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Properties::getEventCreated().setEnabled(true);

```

</details>

### Return value

Event instance.
## void setValidationEnabled ( bool enabled )

Sets a new value indicating if validation for properties is enabled. Can be used to temporarily disable property validation to prevent various issues (e.g., during property generation).
### Arguments

- *bool* **enabled** - Set **true** to enable validation for properties; **false** - to disable it.

## bool isValidationEnabled () const

Returns the current value indicating if validation for properties is enabled. Can be used to temporarily disable property validation to prevent various issues (e.g., during property generation).
### Return value

**true** if validation for properties is enabled ; otherwise **false**.
---

## Ptr < Property > getProperty ( int num ) const

Returns a property by its number. The returned property can be modified by using methods of the *[Property](../../../api/library/common/class.property_cpp.md)* class.
```cpp
Vector<PropertyPtr> my_properties;
for (int i = 0; i < Properties::getNumProperties(); i++) {
	my_properties.append(Properties::getProperty(i));
}

```


### Arguments

- *int* **num** - Number of the property in range from 0 to the [total number of properties](#getNumProperties_int).

### Return value

[Property](../../../api/library/common/class.property_cpp.md) smart pointer if it exists or NULL.
## bool isProperty ( const char * name ) const

Checks if a property with the given name exists.
### Arguments

- *const char ** **name** - Name of the property.

### Return value

true if a property with the given name exists; otherwise, false.
## bool isProperty ( const UGUID & guid ) const

Checks if a property with the given GUID exists.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property.

### Return value

true if a property with the given GUID exists; otherwise, false.
## bool isManualProperty ( const char * name ) const

Checks if a property with the given name exists.
### Arguments

- *const char ** **name** - Name of the manual property.

### Return value

true if a manual property with the given name exists; otherwise, false.
## const char * getPropertyName ( int num ) const

Returns the name of the property by its number.
### Arguments

- *int* **num** - Number of the property in range from 0 to the [total number of properties](#getNumProperties_int).

### Return value

Name of the property.
> **Notice:** If the property with the specified number is internal and has a parent, the parent's name will be returned.


## Ptr < Property > cloneProperty ( const UGUID & guid , const char * name = 0 , const char * path = 0 )


Clones the property and assigns the specified name and path to the clone.


> **Notice:** Without a name the cloned property won't be displayed in the properties hierarchy, without a path it won't be saved when *[saveProperties()](#saveProperties_int)* is called.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to clone.
- *const char ** **name** - Cloned property name.
- *const char ** **path** - Path to save the cloned property.

### Return value

[Property](../../../api/library/common/class.property_cpp.md) smart pointer if the property with the specified GUID exists or nullptr.
## Ptr < Property > findProperty ( const char * name ) const

Searches for a property with the given name. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cpp.md)* class.
### Arguments

- *const char ** **name** - Property name.

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cpp.md)* class); otherwise, nullptr.
## Ptr < Property > findManualProperty ( const char * name ) const

Searches for a manual property with the given name. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cpp.md)* class.
### Arguments

- *const char ** **name** - Manual property name.

### Return value

Manual property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cpp.md)* class); otherwise, nullptr.
## Ptr < Property > findPropertyByGUID ( const UGUID & guid ) const

Searches for a property with the given GUID. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cpp.md)* class.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Property [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cpp.md)* class); otherwise, nullptr.
## Ptr < Property > findPropertyByPath ( const char * path ) const

Searches for a property with the given path. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cpp.md)* class.
### Arguments

- *const char ** **path** - Property [path](../../../api/library/common/class.property_cpp.md#name_path).

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cpp.md)* class); otherwise, nullptr.
## Ptr < Property > findPropertyByFileGUID ( const UGUID & guid ) const

Searches for a property with the given `*.prop` file GUID. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cpp.md)* class.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Property file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cpp.md)* class); otherwise, nullptr.
## Ptr < Property > loadProperty ( const char * path )

Loads a property from the specified `*.prop` file. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cpp.md)* class.
### Arguments

- *const char ** **path** - Path to the `*.prop` file to load a property from.

### Return value

Property, if it is loaded successfully (an instance of the *[Property](../../../api/library/common/class.property_cpp.md)* class); otherwise, nullptr.
## Ptr < Property > inheritProperty ( const UGUID & guid , const char * name = 0 , const char * path = 0 )


Inherits a property from the given property and assigns the specified name and path to the new property.


> **Notice:** Without a name the inherited property won't be displayed in the properties hierarchy, without a path it won't be saved when *[saveProperties()](#saveProperties_int)* is called.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to inherit from.
- *const char ** **name** - Inherited property name.
- *const char ** **path** - Path to save the inherited property.

### Return value

[Property](../../../api/library/common/class.property_cpp.md) smart pointer if the property with the specified GUID exists or nullptr.
## bool removeProperty ( const UGUID & guid , bool remove_file = 0 , bool remove_children = 1 )


Removes the property with the specified GUID.


> **Notice:** A root property (the property that has no parent) or a [non-editable](../../../api/library/common/class.property_cpp.md#isEditable_int) property cannot be removed using this function.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to remove.
- *bool* **remove_file** - Flag indicating if the corresponding `*.prop` file will be deleted. Set 1 to delete the file, or 0 to keep it.
- *bool* **remove_children** - Flag indicating if all children of the property will be deleted. Set 1 to delete all children of the property, or 0 to link all children to the parent.

### Return value

true if the property is removed successfully; otherwise, false.
## bool renameProperty ( const UGUID & guid , const char * new_name )


Changes the [name](../../../api/library/common/class.property_cpp.md#name_path) of the property with the specified GUID.


> **Notice:** - The name of the `*.prop` file is not affected.
> - This method is not available for the [manual](../../../api/library/common/class.property_cpp.md#isManual_int) and [non-editable](../../../api/library/common/class.property_cpp.md#isEditable_int) properties.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to be renamed.
- *const char ** **new_name** - New name for the property to be set.

### Return value

true if the property is renamed successfully; otherwise, false.
## bool replaceProperty ( const Ptr < Property > & property , const Ptr < Property > & new_property )

Replaces the specified property with a new one for all nodes and surfaces. The new property that replaces the specified one must exist. For example, if you have 3 nodes with the same property, calling this method will change this property to the specified one for all these nodes.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **property** - Property to be replaced.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Property](../../../api/library/common/class.property_cpp.md)> &* **new_property** - New property.

### Return value

true if the property is replaced successfully; otherwise, false.
## bool reparentProperty ( const UGUID & guid , const UGUID & new_parent , bool save_all_values = 0 )


Sets a new parent for the specified property. Both properties with given GUIDs must exist.


> **Notice:** The method isn't available for the [manual](../../../api/library/common/class.property_cpp.md#isManual_int) and [non-editable](../../../api/library/common/class.property_cpp.md#isEditable_int) properties.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property whose parent is to be changed.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_parent** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the property to be set as a new parent.
- *bool* **save_all_values** - Flag indicating if parameter values of the specified property will be saved after reparenting.

### Return value

true if the parent for the property is changed successfully; otherwise, false.
## void reloadProperties ( )


Reloads all `*.prop` files from all data folders.


> **Notice:** If new `*.prop` files are found, they will be loaded automatically. The hierarchy will be rebuilt if necessary, while keeping all overridden parameter values.


## int saveProperties ( ) const


Saves all properties that can be saved to corresponding `*.prop` files.


> **Notice:** This method will save only the properties that:
> - are not [manual](../../../api/library/common/class.property_cpp.md#isManual_int)
> - are [editable](../../../api/library/common/class.property_cpp.md#isEditable_int)
> - have a name (not [internal](../../../api/library/common/class.property_cpp.md#isInternal_int))
> - have a [path](../../../api/library/common/class.property_cpp.md#name_path)


### Return value

1 if all properties are saved successfully; otherwise, 0.
