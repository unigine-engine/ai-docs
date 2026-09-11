# Unigine::Properties Class (CS)

> **Notice:** This class is a singleton.


The functions below are used to control property loading and management within the project: you can [get](#getProperty_int_Property), [clone](#cloneProperty_UGUID_cstr_cstr_Property), [inherit](#inheritProperty_UGUID_cstr_cstr_Property), or [remove](#removeProperty_UGUID_int_int_int) any property within the project. [Reparenting](#reparentProperty_UGUID_UGUID_int_int) is supported for all [non-manual](../../../api/library/common/class.property_cs.md#isManual_int) and [editable](../../../api/library/common/class.property_cs.md#isEditable_int) properties.


> **Notice:** To modify a single property, use functions of the *[Property](../../../api/library/common/class.property_cs.md)* class.


### Handling Events


You can subscribe for events to track any changes made to any property and perform certain actions. The signature of the handler function must be as follows:


```csharp
void handler_function_name(Property property);
```


Here is an example of tracking property removal via events:


```csharp
		public void property_removed(Property property)
		{
			Log.Message("Property \"{0}\" was removed.\n", property.Name);
		}

		// somewhere in the code

		// inherit a new property named "new_property_1" from the base property "surface_base"
		Properties.FindManualProperty("surface_base").Inherit("new_property_1");

		// subscribing for property removal event
		Properties.EventRemoved.Connect(property_removed);

		// remove the property named "new_property_1"
		Properties.RemoveProperty(Properties.FindProperty("new_property_1").GUID);

```


## Properties Class

### Properties

## 🔒︎ int NumProperties

The total number of properties loaded for the project.
## 🔒︎ Event< Property > EventRemoved

The event triggered when a property is removed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Removed event handler
void removed_event_handler(Property property)
{
	Log.Message("\Handling Removed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections removed_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties.EventRemoved.Connect(removed_event_connections, removed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties.EventRemoved.Connect(removed_event_connections, (Property property) => {
		Log.Message("Handling Removed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
removed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Removed event with a handler function
Properties.EventRemoved.Connect(removed_event_handler);

// remove subscription to the Removed event later by the handler function
Properties.EventRemoved.Disconnect(removed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection removed_event_connection;

// subscribe to the Removed event with a lambda handler function and keeping the connection
removed_event_connection = Properties.EventRemoved.Connect((Property property) => {
		Log.Message("Handling Removed event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
removed_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
removed_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
removed_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Removed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties.EventRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Properties.EventRemoved.Enabled = true;

```

</details>

## 🔒︎ Event< Property > EventReparented

The event triggered when the parent of a property is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Reparented event handler
void reparented_event_handler(Property property)
{
	Log.Message("\Handling Reparented event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections reparented_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties.EventReparented.Connect(reparented_event_connections, reparented_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties.EventReparented.Connect(reparented_event_connections, (Property property) => {
		Log.Message("Handling Reparented event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
reparented_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Reparented event with a handler function
Properties.EventReparented.Connect(reparented_event_handler);

// remove subscription to the Reparented event later by the handler function
Properties.EventReparented.Disconnect(reparented_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection reparented_event_connection;

// subscribe to the Reparented event with a lambda handler function and keeping the connection
reparented_event_connection = Properties.EventReparented.Connect((Property property) => {
		Log.Message("Handling Reparented event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
reparented_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
reparented_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
reparented_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Reparented events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties.EventReparented.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Properties.EventReparented.Enabled = true;

```

</details>

## 🔒︎ Event< Property > EventRenamed

The event triggered when the [name](../../../api/library/common/class.property_cs.md#name_path) of a property is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Renamed event handler
void renamed_event_handler(Property property)
{
	Log.Message("\Handling Renamed event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections renamed_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties.EventRenamed.Connect(renamed_event_connections, renamed_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties.EventRenamed.Connect(renamed_event_connections, (Property property) => {
		Log.Message("Handling Renamed event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
renamed_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Renamed event with a handler function
Properties.EventRenamed.Connect(renamed_event_handler);

// remove subscription to the Renamed event later by the handler function
Properties.EventRenamed.Disconnect(renamed_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection renamed_event_connection;

// subscribe to the Renamed event with a lambda handler function and keeping the connection
renamed_event_connection = Properties.EventRenamed.Connect((Property property) => {
		Log.Message("Handling Renamed event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
renamed_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
renamed_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
renamed_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Renamed events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties.EventRenamed.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Properties.EventRenamed.Enabled = true;

```

</details>

## 🔒︎ Event< Property > EventMoved

The event triggered when the [path](../../../api/library/common/class.property_cs.md#name_path) of a property is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Moved event handler
void moved_event_handler(Property property)
{
	Log.Message("\Handling Moved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections moved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties.EventMoved.Connect(moved_event_connections, moved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties.EventMoved.Connect(moved_event_connections, (Property property) => {
		Log.Message("Handling Moved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
moved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Moved event with a handler function
Properties.EventMoved.Connect(moved_event_handler);

// remove subscription to the Moved event later by the handler function
Properties.EventMoved.Disconnect(moved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection moved_event_connection;

// subscribe to the Moved event with a lambda handler function and keeping the connection
moved_event_connection = Properties.EventMoved.Connect((Property property) => {
		Log.Message("Handling Moved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
moved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
moved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
moved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Moved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties.EventMoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Properties.EventMoved.Enabled = true;

```

</details>

## 🔒︎ Event< Property > EventCreated

The event triggered when a new property is created. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(Property **property**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Created event handler
void created_event_handler(Property property)
{
	Log.Message("\Handling Created event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections created_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Properties.EventCreated.Connect(created_event_connections, created_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Properties.EventCreated.Connect(created_event_connections, (Property property) => {
		Log.Message("Handling Created event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
created_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Created event with a handler function
Properties.EventCreated.Connect(created_event_handler);

// remove subscription to the Created event later by the handler function
Properties.EventCreated.Disconnect(created_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection created_event_connection;

// subscribe to the Created event with a lambda handler function and keeping the connection
created_event_connection = Properties.EventCreated.Connect((Property property) => {
		Log.Message("Handling Created event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
created_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
created_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
created_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Created events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Properties.EventCreated.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Properties.EventCreated.Enabled = true;

```

</details>

## bool ValidationEnabled

The value indicating if validation for properties is enabled. Can be used to temporarily disable property validation to prevent various issues (e.g., during property generation).
### Members

---

## Property GetProperty ( int num )

Returns a property by its number. The returned property can be modified by using methods of the *[Property](../../../api/library/common/class.property_cs.md)* class.
```csharp
Property[] my_properties = new Property[properties.getNumProperties()];
for (int i = 0; i < properties.getNumProperties(); i++)
{
	my_properties[i] = properties.getProperty(i);
}

```


### Arguments

- *int* **num** - Number of the property in range from 0 to the [total number of properties](#getNumProperties_int).

### Return value

[Property](../../../api/library/common/class.property_cs.md) instance if it exists or NULL.
## bool IsProperty ( string name )

Checks if a property with the given name exists.
### Arguments

- *string* **name** - Name of the property.

### Return value

true if a property with the given name exists; otherwise, false.
## bool IsProperty ( UGUID guid )

Checks if a property with the given GUID exists.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property.

### Return value

true if a property with the given GUID exists; otherwise, false.
## bool IsManualProperty ( string name )

Checks if a property with the given name exists.
### Arguments

- *string* **name** - Name of the manual property.

### Return value

true if a manual property with the given name exists; otherwise, false.
## string GetPropertyName ( int num )

Returns the name of the property by its number.
### Arguments

- *int* **num** - Number of the property in range from 0 to the [total number of properties](#getNumProperties_int).

### Return value

Name of the property.
> **Notice:** If the property with the specified number is internal and has a parent, the parent's name will be returned.


## Property CloneProperty ( UGUID guid , string name = 0 , string path = 0 )


Clones the property and assigns the specified name and path to the clone.


> **Notice:** Without a name the cloned property won't be displayed in the properties hierarchy, without a path it won't be saved when *[saveProperties()](#saveProperties_int)* is called.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to clone.
- *string* **name** - Cloned property name.
- *string* **path** - Path to save the cloned property.

### Return value

[Property](../../../api/library/common/class.property_cs.md) instance if the property with the specified GUID exists or nullptr.
## Property FindProperty ( string name )

Searches for a property with the given name. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cs.md)* class.
### Arguments

- *string* **name** - Property name.

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cs.md)* class); otherwise, nullptr.
## Property FindManualProperty ( string name )

Searches for a manual property with the given name. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cs.md)* class.
### Arguments

- *string* **name** - Manual property name.

### Return value

Manual property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cs.md)* class); otherwise, nullptr.
## Property FindPropertyByGUID ( UGUID guid )

Searches for a property with the given GUID. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cs.md)* class.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Property [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cs.md)* class); otherwise, nullptr.
## Property FindPropertyByPath ( string path )

Searches for a property with the given path. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cs.md)* class.
### Arguments

- *string* **path** - Property [path](../../../api/library/common/class.property_cs.md#name_path).

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cs.md)* class); otherwise, nullptr.
## Property FindPropertyByFileGUID ( UGUID guid )

Searches for a property with the given `*.prop` file GUID. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cs.md)* class.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Property file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Property, if it is found (an instance of the *[Property](../../../api/library/common/class.property_cs.md)* class); otherwise, nullptr.
## Property LoadProperty ( string path )

Loads a property from the specified `*.prop` file. The returned property can be managed using the methods of the *[Property](../../../api/library/common/class.property_cs.md)* class.
### Arguments

- *string* **path** - Path to the `*.prop` file to load a property from.

### Return value

Property, if it is loaded successfully (an instance of the *[Property](../../../api/library/common/class.property_cs.md)* class); otherwise, nullptr.
## Property InheritProperty ( UGUID guid , string name = 0 , string path = 0 )


Inherits a property from the given property and assigns the specified name and path to the new property.


> **Notice:** Without a name the inherited property won't be displayed in the properties hierarchy, without a path it won't be saved when *[saveProperties()](#saveProperties_int)* is called.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to inherit from.
- *string* **name** - Inherited property name.
- *string* **path** - Path to save the inherited property.

### Return value

[Property](../../../api/library/common/class.property_cs.md) instance if the property with the specified GUID exists or nullptr.
## bool RemoveProperty ( UGUID guid , bool remove_file = 0 , bool remove_children = 1 )


Removes the property with the specified GUID.


> **Notice:** A root property (the property that has no parent) or a [non-editable](../../../api/library/common/class.property_cs.md#isEditable_int) property cannot be removed using this function.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to remove.
- *bool* **remove_file** - Flag indicating if the corresponding `*.prop` file will be deleted. Set 1 to delete the file, or 0 to keep it.
- *bool* **remove_children** - Flag indicating if all children of the property will be deleted. Set 1 to delete all children of the property, or 0 to link all children to the parent.

### Return value

true if the property is removed successfully; otherwise, false.
## bool RenameProperty ( UGUID guid , string new_name )


Changes the [name](../../../api/library/common/class.property_cs.md#name_path) of the property with the specified GUID.


> **Notice:** - The name of the `*.prop` file is not affected.
> - This method is not available for the [manual](../../../api/library/common/class.property_cs.md#isManual_int) and [non-editable](../../../api/library/common/class.property_cs.md#isEditable_int) properties.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to be renamed.
- *string* **new_name** - New name for the property to be set.

### Return value

true if the property is renamed successfully; otherwise, false.
## bool ReplaceProperty ( Property property , Property new_property )

Replaces the specified property with a new one for all nodes and surfaces. The new property that replaces the specified one must exist. For example, if you have 3 nodes with the same property, calling this method will change this property to the specified one for all these nodes.
### Arguments

- *[Property](../../../api/library/common/class.property_cs.md)* **property** - Property to be replaced.
- *[Property](../../../api/library/common/class.property_cs.md)* **new_property** - New property.

### Return value

true if the property is replaced successfully; otherwise, false.
## bool ReparentProperty ( UGUID guid , UGUID new_parent , bool save_all_values = 0 )


Sets a new parent for the specified property. Both properties with given GUIDs must exist.


> **Notice:** The method isn't available for the [manual](../../../api/library/common/class.property_cs.md#isManual_int) and [non-editable](../../../api/library/common/class.property_cs.md#isEditable_int) properties.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property whose parent is to be changed.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_parent** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the property to be set as a new parent.
- *bool* **save_all_values** - Flag indicating if parameter values of the specified property will be saved after reparenting.

### Return value

true if the parent for the property is changed successfully; otherwise, false.
## void ReloadProperties ( )


Reloads all `*.prop` files from all data folders.


> **Notice:** If new `*.prop` files are found, they will be loaded automatically. The hierarchy will be rebuilt if necessary, while keeping all overridden parameter values.


## int SaveProperties ( )


Saves all properties that can be saved to corresponding `*.prop` files.


> **Notice:** This method will save only the properties that:
> - are not [manual](../../../api/library/common/class.property_cs.md#isManual_int)
> - are [editable](../../../api/library/common/class.property_cs.md#isEditable_int)
> - have a name (not [internal](../../../api/library/common/class.property_cs.md#isInternal_int))
> - have a [path](../../../api/library/common/class.property_cs.md#name_path)


### Return value

1 if all properties are saved successfully; otherwise, 0.
