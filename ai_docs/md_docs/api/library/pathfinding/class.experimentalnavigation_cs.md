# Unigine::ExperimentalNavigation Class (CS)

> **Notice:** This class is a singleton.


> **Notice:** Not to be confused with the legacy [Navigation](../../../api/library/pathfinding/class.navigation_cs.md) node class: despite the similar name they are unrelated.


World-wide settings of the navigation system: the registry of areas and flags, the budgets that pace tile streaming, and the memory the navigation data is allowed to hold.


The registry is what gives numbers meaning. A polygon carries a six-bit area index and a set of flags, and nothing more; the name behind index 4, what crossing it costs, and which flags it implies all live here, in one place shared by the whole world. Areas are the traversal cost � mud is three times a road � while flags are the yes-or-no rights a query filters on. There are 64 areas and 16 flags, and two indices are reserved: one for the default area and one for the polygons cut away by obstacles.


## ExperimentalNavigation Class

### Properties

## 🔒︎ int CutAreaIndex

The Returns the area index reserved for the polygons cut away by obstacles and carving volumes. Such polygons stay in the data but are marked with this area, so a query can tell a hole from ordinary ground.
## 🔒︎ int DefaultAreaIndex

The Returns the area index every polygon gets unless something assigns it another one � a surface marked on an object, a detail mask, or an area volume.
## float InvalidateBudget

The time per frame the engine may spend rebuilding the tiles that area volumes and moved obstacles have made dirty. It bounds the frame cost of a world that keeps changing. Mapped to the *navigation_invalidate_budget* console variable.
## 🔒︎ bool IsStreamingMemoryLimitReached

The value indicating if the navigation data has hit the memory limit. Once it has, tiles stop being loaded, and queries in the affected region start failing for lack of data rather than for lack of a route.
## 🔒︎ int NumActiveTasks

The number of navigation tasks the workers are running right now � path searches, tile builds, and avoidance batches alike.
## 🔒︎ int NumAreas

The size of the area registry. The limit comes from the six bits a polygon has to store its area index in.
## 🔒︎ int NumFlags

The size of the flag registry.
## 🔒︎ int NumNavigationMeshes

The number of navigation meshes present in the world.
## float StreamingBudget

The time per frame the engine may spend loading and unloading navigation mesh tiles. It bounds what streaming costs when an invoker moves fast through a large world. Mapped to the *navigation_streaming_budget* console variable.
## int StreamingMemoryLimit

The amount of memory the tiles and voxels of every navigation mesh together are allowed to hold. Mapped to the *navigation_streaming_memory_limit* console variable.
## 🔒︎ Event<int> EventAreaChanged

The event triggered when the name, cost, or flags of an area change. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int area_index)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the AreaChanged event handler
void areachanged_event_handler(int area_index)
{
	Log.Message("\Handling AreaChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections areachanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventAreaChanged.Connect(areachanged_event_connections, areachanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventAreaChanged.Connect(areachanged_event_connections, (int area_index) => {
		Log.Message("Handling AreaChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
areachanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the AreaChanged event with a handler function
publisher.EventAreaChanged.Connect(areachanged_event_handler);

// remove subscription to the AreaChanged event later by the handler function
publisher.EventAreaChanged.Disconnect(areachanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection areachanged_event_connection;

// subscribe to the AreaChanged event with a lambda handler function and keeping the connection
areachanged_event_connection = publisher.EventAreaChanged.Connect((int area_index) => {
		Log.Message("Handling AreaChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
areachanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
areachanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
areachanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring AreaChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventAreaChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventAreaChanged.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventFlagChanged

The event triggered when the name of a flag changes. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int flag_index)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FlagChanged event handler
void flagchanged_event_handler(int flag_index)
{
	Log.Message("\Handling FlagChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections flagchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventFlagChanged.Connect(flagchanged_event_connections, flagchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventFlagChanged.Connect(flagchanged_event_connections, (int flag_index) => {
		Log.Message("Handling FlagChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
flagchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FlagChanged event with a handler function
publisher.EventFlagChanged.Connect(flagchanged_event_handler);

// remove subscription to the FlagChanged event later by the handler function
publisher.EventFlagChanged.Disconnect(flagchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection flagchanged_event_connection;

// subscribe to the FlagChanged event with a lambda handler function and keeping the connection
flagchanged_event_connection = publisher.EventFlagChanged.Connect((int flag_index) => {
		Log.Message("Handling FlagChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
flagchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
flagchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
flagchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FlagChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventFlagChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventFlagChanged.Enabled = true;

```

</details>

## 🔒︎ Event<> EventRegistryChanged

The event triggered when the registry of areas and flags changes as a whole, for instance after the settings are loaded from a file. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the RegistryChanged event handler
void registrychanged_event_handler()
{
	Log.Message("\Handling RegistryChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections registrychanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventRegistryChanged.Connect(registrychanged_event_connections, registrychanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventRegistryChanged.Connect(registrychanged_event_connections, () => {
		Log.Message("Handling RegistryChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
registrychanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the RegistryChanged event with a handler function
publisher.EventRegistryChanged.Connect(registrychanged_event_handler);

// remove subscription to the RegistryChanged event later by the handler function
publisher.EventRegistryChanged.Disconnect(registrychanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection registrychanged_event_connection;

// subscribe to the RegistryChanged event with a lambda handler function and keeping the connection
registrychanged_event_connection = publisher.EventRegistryChanged.Connect(() => {
		Log.Message("Handling RegistryChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
registrychanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
registrychanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
registrychanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring RegistryChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventRegistryChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventRegistryChanged.Enabled = true;

```

</details>

### Members

---

## vec4 GetAreaColor ( int area_index )

Returns the color an area is drawn with by the navigation mesh visualizer. Colors are what make areas legible on screen � mud, road, and water are told apart by eye rather than by index.
### Arguments

- *int* **area_index** - Area index.

### Return value

Color of the area.
## float GetAreaCost ( int area_index )

Returns the traversal cost shared by the whole world for an area. A single query can depart from it via the area cost override of its filter.
### Arguments

- *int* **area_index** - Area index.

### Return value

Traversal cost of the area.
## int GetAreaFlags ( int area_index )

Returns the flags every polygon of an area carries. Tying flags to an area saves marking each polygon by hand: making an area impassable for swimmers is one setting rather than a pass over the data.
### Arguments

- *int* **area_index** - Area index.

### Return value

Flags implied by the area.
## int GetAreaIndex ( string name )

Returns the index of a named area. Looking the index up by name keeps game code free of the numbers the registry happens to use.
### Arguments

- *string* **name** - Area name.

### Return value

Area index, or -1 if no area carries that name.
## string GetAreaName ( int area_index )

Returns the name of an area. Names exist for the editor and for lookups; the engine itself only ever works with the index.
### Arguments

- *int* **area_index** - Area index.

### Return value

Area name, or an empty string if the area is unnamed.
## vec4 GetDefaultAreaColor ( int area_index )

Returns the color an area is given before anything overrides it.
### Arguments

- *int* **area_index** - Area index.

### Return value

Default color of the area.
## int GetFlagIndex ( string name )

Returns the index of a named flag.
### Arguments

- *string* **name** - Flag name.

### Return value

Flag index, or -1 if no flag carries that name.
## int GetFlagMask ( string name )

Returns the bit of a named flag as a ready-made mask. It is what goes into the include and exclude masks of a filter, so the shift does not have to be written out by hand.
### Arguments

- *string* **name** - Flag name.

### Return value

Mask with the bit of the flag set, or 0 if no flag carries that name.
## string GetFlagName ( int flag_index )

Returns the name of a flag.
### Arguments

- *int* **flag_index** - Flag index.

### Return value

Flag name, or an empty string if the flag is unnamed.
## ExperimentalNavigationMesh GetNavigationMesh ( int num )

Returns a navigation mesh of the world by its number. Together with the count above it lets the whole set be walked without searching the node tree.
### Arguments

- *int* **num** - Navigation mesh number.

### Return value

Navigation mesh in the world.
## bool LoadSettings ( string path )

Loads the registry of areas and flags from a file, replacing the current one. Keeping the registry in a file lets several worlds share one set of area definitions.
### Arguments

- *string* **path** - Path to the settings file.

### Return value

true if the settings were loaded; otherwise, false.
## bool RestoreState ( Stream stream )

Restores the state of the navigation system from a stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to restore the state from.

### Return value

true if the state was restored; otherwise, false.
## bool SaveSettings ( string path )

Saves the registry of areas and flags to a file.
### Arguments

- *string* **path** - Path to the settings file.

### Return value

true if the settings were saved; otherwise, false.
## bool SaveState ( Stream stream )

Saves the state of the navigation system into a stream. Baked tiles are not part of it � they are rebuilt or reloaded rather than stored in a save.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to save the state into.

### Return value

true if the state was saved; otherwise, false.
## void SetAreaColor ( int area_index , vec4 color )

Sets the color an area is drawn with by the navigation mesh visualizer.
### Arguments

- *int* **area_index** - Area index.
- *vec4* **color** - Color to draw the area with.

## void SetAreaCost ( int area_index , float cost )

Sets the traversal cost of an area for the whole world. Costs below 1 make the search prefer the area and require the heuristic scale to be adjusted, otherwise the result stops being optimal.
### Arguments

- *int* **area_index** - Area index.
- *float* **cost** - Traversal cost multiplier. The higher the cost, the more willingly the search routes around the area.

## void SetAreaFlags ( int area_index , int flags )

Sets the flags implied by an area.
### Arguments

- *int* **area_index** - Area index.
- *int* **flags** - Flags every polygon of the area carries.

## void SetAreaName ( int area_index , string name )

Gives an area a name it can be looked up by.
### Arguments

- *int* **area_index** - Area index.
- *string* **name** - Name to be given to the area.

## void SetFlagName ( int flag_index , string name )

Gives a flag a name it can be looked up by.
### Arguments

- *int* **flag_index** - Flag index.
- *string* **name** - Name to be given to the flag.
