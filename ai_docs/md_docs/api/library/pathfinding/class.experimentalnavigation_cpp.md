# Unigine::ExperimentalNavigation Class (CPP)

**Header:** #include <UnigineExperimentalNavigation.h>

> **Notice:** This class is a singleton.


> **Notice:** Not to be confused with the legacy [Navigation](../../../api/library/pathfinding/class.navigation_cpp.md) node class: despite the similar name they are unrelated.


World-wide settings of the navigation system: the registry of areas and flags, the budgets that pace tile streaming, and the memory the navigation data is allowed to hold.


The registry is what gives numbers meaning. A polygon carries a six-bit area index and a set of flags, and nothing more; the name behind index 4, what crossing it costs, and which flags it implies all live here, in one place shared by the whole world. Areas are the traversal cost � mud is three times a road � while flags are the yes-or-no rights a query filters on. There are 64 areas and 16 flags, and two indices are reserved: one for the default area and one for the polygons cut away by obstacles.


## ExperimentalNavigation Class

### Members

## int getCutAreaIndex () const

Returns the area index reserved for the polygons cut away by obstacles and carving volumes. Such polygons stay in the data but are marked with this area, so a query can tell a hole from ordinary ground.
### Return value

reserved cut area index.
## int getDefaultAreaIndex () const

Returns the area index every polygon gets unless something assigns it another one � a surface marked on an object, a detail mask, or an area volume.
### Return value

default area index.
## void setInvalidateBudget ( float budget )

Sets a new time per frame the engine may spend rebuilding the tiles that area volumes and moved obstacles have made dirty. It bounds the frame cost of a world that keeps changing. Mapped to the *navigation_invalidate_budget* console variable.
### Arguments

- *float* **budget** - The invalidation budget, in seconds. The default value is 0.004.

## float getInvalidateBudget () const

Returns the current time per frame the engine may spend rebuilding the tiles that area volumes and moved obstacles have made dirty. It bounds the frame cost of a world that keeps changing. Mapped to the *navigation_invalidate_budget* console variable.
### Return value

Current invalidation budget, in seconds. The default value is 0.004.
## bool isStreamingMemoryLimitReached () const

Returns the current value indicating if the navigation data has hit the memory limit. Once it has, tiles stop being loaded, and queries in the affected region start failing for lack of data rather than for lack of a route.
### Return value

**true** if the memory limit is reached; otherwise **false**.
## int getNumActiveTasks () const

Returns the current number of navigation tasks the workers are running right now � path searches, tile builds, and avoidance batches alike.
### Return value

Current number of active tasks.
## int getNumAreas () const

Returns the current size of the area registry. The limit comes from the six bits a polygon has to store its area index in.
### Return value

Current number of areas. Always 64.
## int getNumFlags () const

Returns the current size of the flag registry.
### Return value

Current number of flags. Always 16.
## int getNumNavigationMeshes () const

Returns the current number of navigation meshes present in the world.
### Return value

Current number of navigation meshes.
## void setStreamingBudget ( float budget )

Sets a new time per frame the engine may spend loading and unloading navigation mesh tiles. It bounds what streaming costs when an invoker moves fast through a large world. Mapped to the *navigation_streaming_budget* console variable.
### Arguments

- *float* **budget** - The streaming budget, in seconds. The default value is 0.002.

## float getStreamingBudget () const

Returns the current time per frame the engine may spend loading and unloading navigation mesh tiles. It bounds what streaming costs when an invoker moves fast through a large world. Mapped to the *navigation_streaming_budget* console variable.
### Return value

Current streaming budget, in seconds. The default value is 0.002.
## void setStreamingMemoryLimit ( int limit )

Sets a new amount of memory the tiles and voxels of every navigation mesh together are allowed to hold. Mapped to the *navigation_streaming_memory_limit* console variable.
### Arguments

- *int* **limit** - The memory limit, in megabytes. The default value is 0, which means no limit.

## int getStreamingMemoryLimit () const

Returns the current amount of memory the tiles and voxels of every navigation mesh together are allowed to hold. Mapped to the *navigation_streaming_memory_limit* console variable.
### Return value

Current memory limit, in megabytes. The default value is 0, which means no limit.
## Event<int> getEventAreaChanged () const

event triggered when the name, cost, or flags of an area change. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int area_index)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the AreaChanged event handler
void areachanged_event_handler(int area_index)
{
	Log::message("\Handling AreaChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections areachanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventAreaChanged().connect(areachanged_event_connections, areachanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventAreaChanged().connect(areachanged_event_connections, [](int area_index) {
		Log::message("\Handling AreaChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
areachanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection areachanged_event_connection;

// subscribe to the AreaChanged event with a handler function keeping the connection
publisher->getEventAreaChanged().connect(areachanged_event_connection, areachanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
areachanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
areachanged_event_connection.setEnabled(true);

// ...

// remove subscription to the AreaChanged event via the connection
areachanged_event_connection.disconnect();

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

	// A AreaChanged event handler implemented as a class member
	void event_handler(int area_index)
	{
		Log::message("\Handling AreaChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventAreaChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId areachanged_handler_id;

// subscribe to the AreaChanged event with a lambda handler function and keeping connection ID
areachanged_handler_id = publisher->getEventAreaChanged().connect(e_connections, [](int area_index) {
		Log::message("\Handling AreaChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventAreaChanged().disconnect(areachanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all AreaChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventAreaChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventAreaChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<int> getEventFlagChanged () const

event triggered when the name of a flag changes. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(int flag_index)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FlagChanged event handler
void flagchanged_event_handler(int flag_index)
{
	Log::message("\Handling FlagChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections flagchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventFlagChanged().connect(flagchanged_event_connections, flagchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventFlagChanged().connect(flagchanged_event_connections, [](int flag_index) {
		Log::message("\Handling FlagChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
flagchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection flagchanged_event_connection;

// subscribe to the FlagChanged event with a handler function keeping the connection
publisher->getEventFlagChanged().connect(flagchanged_event_connection, flagchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
flagchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
flagchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the FlagChanged event via the connection
flagchanged_event_connection.disconnect();

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

	// A FlagChanged event handler implemented as a class member
	void event_handler(int flag_index)
	{
		Log::message("\Handling FlagChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventFlagChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId flagchanged_handler_id;

// subscribe to the FlagChanged event with a lambda handler function and keeping connection ID
flagchanged_handler_id = publisher->getEventFlagChanged().connect(e_connections, [](int flag_index) {
		Log::message("\Handling FlagChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventFlagChanged().disconnect(flagchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FlagChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventFlagChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventFlagChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<> getEventRegistryChanged () const

event triggered when the registry of areas and flags changes as a whole, for instance after the settings are loaded from a file. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the RegistryChanged event handler
void registrychanged_event_handler()
{
	Log::message("\Handling RegistryChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections registrychanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventRegistryChanged().connect(registrychanged_event_connections, registrychanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventRegistryChanged().connect(registrychanged_event_connections, []() {
		Log::message("\Handling RegistryChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
registrychanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection registrychanged_event_connection;

// subscribe to the RegistryChanged event with a handler function keeping the connection
publisher->getEventRegistryChanged().connect(registrychanged_event_connection, registrychanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
registrychanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
registrychanged_event_connection.setEnabled(true);

// ...

// remove subscription to the RegistryChanged event via the connection
registrychanged_event_connection.disconnect();

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

	// A RegistryChanged event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling RegistryChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventRegistryChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId registrychanged_handler_id;

// subscribe to the RegistryChanged event with a lambda handler function and keeping connection ID
registrychanged_handler_id = publisher->getEventRegistryChanged().connect(e_connections, []() {
		Log::message("\Handling RegistryChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventRegistryChanged().disconnect(registrychanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all RegistryChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventRegistryChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventRegistryChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## Math:: vec4 getAreaColor ( int area_index )

Returns the color an area is drawn with by the navigation mesh visualizer. Colors are what make areas legible on screen � mud, road, and water are told apart by eye rather than by index.
### Arguments

- *int* **area_index** - Area index.

### Return value

Color of the area.
## float getAreaCost ( int area_index )

Returns the traversal cost shared by the whole world for an area. A single query can depart from it via the area cost override of its filter.
### Arguments

- *int* **area_index** - Area index.

### Return value

Traversal cost of the area.
## int getAreaFlags ( int area_index )

Returns the flags every polygon of an area carries. Tying flags to an area saves marking each polygon by hand: making an area impassable for swimmers is one setting rather than a pass over the data.
### Arguments

- *int* **area_index** - Area index.

### Return value

Flags implied by the area.
## int getAreaIndex ( const char * name )

Returns the index of a named area. Looking the index up by name keeps game code free of the numbers the registry happens to use.
### Arguments

- *const char ** **name** - Area name.

### Return value

Area index, or -1 if no area carries that name.
## const char * getAreaName ( int area_index )

Returns the name of an area. Names exist for the editor and for lookups; the engine itself only ever works with the index.
### Arguments

- *int* **area_index** - Area index.

### Return value

Area name, or an empty string if the area is unnamed.
## Math:: vec4 getDefaultAreaColor ( int area_index )

Returns the color an area is given before anything overrides it.
### Arguments

- *int* **area_index** - Area index.

### Return value

Default color of the area.
## int getFlagIndex ( const char * name )

Returns the index of a named flag.
### Arguments

- *const char ** **name** - Flag name.

### Return value

Flag index, or -1 if no flag carries that name.
## int getFlagMask ( const char * name )

Returns the bit of a named flag as a ready-made mask. It is what goes into the include and exclude masks of a filter, so the shift does not have to be written out by hand.
### Arguments

- *const char ** **name** - Flag name.

### Return value

Mask with the bit of the flag set, or 0 if no flag carries that name.
## const char * getFlagName ( int flag_index )

Returns the name of a flag.
### Arguments

- *int* **flag_index** - Flag index.

### Return value

Flag name, or an empty string if the flag is unnamed.
## Ptr < ExperimentalNavigationMesh > getNavigationMesh ( int num )

Returns a navigation mesh of the world by its number. Together with the count above it lets the whole set be walked without searching the node tree.
### Arguments

- *int* **num** - Navigation mesh number.

### Return value

Navigation mesh in the world.
## bool isInitialized ( )

Returns a value indicating if the navigation system is initialized.
### Return value

true if the navigation system is initialized; otherwise, false.
## bool loadSettings ( const char * path )

Loads the registry of areas and flags from a file, replacing the current one. Keeping the registry in a file lets several worlds share one set of area definitions.
### Arguments

- *const char ** **path** - Path to the settings file.

### Return value

true if the settings were loaded; otherwise, false.
## bool restoreState ( const Ptr < Stream > & stream )

Restores the state of the navigation system from a stream.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to restore the state from.

### Return value

true if the state was restored; otherwise, false.
## bool saveSettings ( const char * path )

Saves the registry of areas and flags to a file.
### Arguments

- *const char ** **path** - Path to the settings file.

### Return value

true if the settings were saved; otherwise, false.
## bool saveState ( const Ptr < Stream > & stream )

Saves the state of the navigation system into a stream. Baked tiles are not part of it � they are rebuilt or reloaded rather than stored in a save.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **stream** - Stream to save the state into.

### Return value

true if the state was saved; otherwise, false.
## void setAreaColor ( int area_index , const Math:: vec4 & color )

Sets the color an area is drawn with by the navigation mesh visualizer.
### Arguments

- *int* **area_index** - Area index.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color to draw the area with.

## void setAreaCost ( int area_index , float cost )

Sets the traversal cost of an area for the whole world. Costs below 1 make the search prefer the area and require the heuristic scale to be adjusted, otherwise the result stops being optimal.
### Arguments

- *int* **area_index** - Area index.
- *float* **cost** - Traversal cost multiplier. The higher the cost, the more willingly the search routes around the area.

## void setAreaFlags ( int area_index , int flags )

Sets the flags implied by an area.
### Arguments

- *int* **area_index** - Area index.
- *int* **flags** - Flags every polygon of the area carries.

## void setAreaName ( int area_index , const char * name )

Gives an area a name it can be looked up by.
### Arguments

- *int* **area_index** - Area index.
- *const char ** **name** - Name to be given to the area.

## void setFlagName ( int flag_index , const char * name )

Gives a flag a name it can be looked up by.
### Arguments

- *int* **flag_index** - Flag index.
- *const char ** **name** - Name to be given to the flag.
