# Unigine.LandscapeMapFileCreator Class (CS)


This class is used to generate a landscape map file (`.lmap`) to be used for [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) creation.


### Usage Example


```csharp
// methods to be executed in the process of landscape map file creation
void create(LandscapeMapFileCreator creator)
{
	Log.Message("Creating LMAP\n");
}
void progress(LandscapeMapFileCreator creator)
{
	Log.Message("{0} {1} \n", creator.Progress, creator.TimeSeconds);
}
void begin(LandscapeMapFileCreator creator)
{
	Log.Message("{0}\n", creator.Progress);
}
void end(LandscapeMapFileCreator creator)
{
	Log.Message("{0}\n", creator.TimeSeconds);
}

	// ...
	// defining grid size (2х2 tiles) and resolution
	ivec2 grid = new ivec2(2, 2);
	ivec2 resolution = new ivec2(2048) * grid;

	// creating a landscape map file creator and setting grid size, resolution, and path
	LandscapeMapFileCreator creator = new LandscapeMapFileCreator();
	creator.Grid = grid;
	creator.Resolution = resolution;
	creator.Path = "test.lmap";

	// subscribing to necessary events with our handlers
	creator.EventCreate.Connect(create);
	creator.EventProgress.Connect(progress);
	creator.EventBegin.Connect(begin);
	creator.EventEnd.Connect(end);

	// running the creator to generate a new "test.lmap" file
	creator.Run();

	// ...

	// creating a new landscape layer map based on the created "test.lmap" file
	LandscapeLayerMap landscape_map = new LandscapeLayerMap();
	landscape_map.Path = "test.lmap";


```


### See also


- C++ sample


## LandscapeMapFileCreator Class

### Properties

## ivec2 Resolution

The landscape map resolution.
## ivec2 Grid

The grid size for the landscape map.
## 🔒︎ float Progress

The landscape map file creation progress.
## 🔒︎ double TimeSeconds

The landscape map file creation time. You can use this method to get total file generation time when processing an End callback.
## string Path

The path to the generated `*.lmap` file.
## 🔒︎ Event< LandscapeMapFileCreator > EventEnd

The Event triggered on completion of the landscape map file creation. The signature of the callback function must be as follows:
```csharp
void end_handler(LandscapeMapFileCreator creator)

```

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(LandscapeMapFileCreator **creator**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the End event handler
void end_event_handler(LandscapeMapFileCreator creator)
{
	Log.Message("\Handling End event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections end_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEnd.Connect(end_event_connections, end_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEnd.Connect(end_event_connections, (LandscapeMapFileCreator creator) => {
		Log.Message("Handling End event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
end_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the End event with a handler function
publisher.EventEnd.Connect(end_event_handler);

// remove subscription to the End event later by the handler function
publisher.EventEnd.Disconnect(end_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection end_event_connection;

// subscribe to the End event with a lambda handler function and keeping the connection
end_event_connection = publisher.EventEnd.Connect((LandscapeMapFileCreator creator) => {
		Log.Message("Handling End event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
end_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
end_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
end_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring End events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEnd.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEnd.Enabled = true;

```

</details>

## 🔒︎ Event< LandscapeMapFileCreator > EventBegin

The Event triggered at the beginning the landscape map file creation. The signature of the callback function must be as follows:
```csharp
void begin_handler(LandscapeMapFileCreator creator)

```

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(LandscapeMapFileCreator **creator**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Begin event handler
void begin_event_handler(LandscapeMapFileCreator creator)
{
	Log.Message("\Handling Begin event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begin_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBegin.Connect(begin_event_connections, begin_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBegin.Connect(begin_event_connections, (LandscapeMapFileCreator creator) => {
		Log.Message("Handling Begin event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begin_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Begin event with a handler function
publisher.EventBegin.Connect(begin_event_handler);

// remove subscription to the Begin event later by the handler function
publisher.EventBegin.Disconnect(begin_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begin_event_connection;

// subscribe to the Begin event with a lambda handler function and keeping the connection
begin_event_connection = publisher.EventBegin.Connect((LandscapeMapFileCreator creator) => {
		Log.Message("Handling Begin event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begin_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begin_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begin_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Begin events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBegin.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBegin.Enabled = true;

```

</details>

## 🔒︎ Event< LandscapeMapFileCreator > EventProgress

The Event triggered on landscape map file creation progress. The signature of the callback function must be as follows:
```csharp
void progress_handler(LandscapeMapFileCreator creator)

```

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(LandscapeMapFileCreator **creator**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Progress event handler
void progress_event_handler(LandscapeMapFileCreator creator)
{
	Log.Message("\Handling Progress event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections progress_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventProgress.Connect(progress_event_connections, progress_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventProgress.Connect(progress_event_connections, (LandscapeMapFileCreator creator) => {
		Log.Message("Handling Progress event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
progress_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Progress event with a handler function
publisher.EventProgress.Connect(progress_event_handler);

// remove subscription to the Progress event later by the handler function
publisher.EventProgress.Disconnect(progress_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection progress_event_connection;

// subscribe to the Progress event with a lambda handler function and keeping the connection
progress_event_connection = publisher.EventProgress.Connect((LandscapeMapFileCreator creator) => {
		Log.Message("Handling Progress event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
progress_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
progress_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
progress_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Progress events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventProgress.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventProgress.Enabled = true;

```

</details>

## 🔒︎ Event< LandscapeMapFileCreator , LandscapeImages , int, int> EventCreate

The Event triggered on landscape layer map file creation. The signature of the callback function must be as follows:
```csharp
void create_handler(LandscapeMapFileCreator creator,  LandscapeImages images,  int x,  int y)

```

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(LandscapeMapFileCreator **creator**, LandscapeImages **images**, int **x**, int **y**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Create event handler
void create_event_handler(LandscapeMapFileCreator creator,  LandscapeImages images,  int x,  int y)
{
	Log.Message("\Handling Create event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections create_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventCreate.Connect(create_event_connections, create_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventCreate.Connect(create_event_connections, (LandscapeMapFileCreator creator,  LandscapeImages images,  int x,  int y) => {
		Log.Message("Handling Create event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
create_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Create event with a handler function
publisher.EventCreate.Connect(create_event_handler);

// remove subscription to the Create event later by the handler function
publisher.EventCreate.Disconnect(create_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection create_event_connection;

// subscribe to the Create event with a lambda handler function and keeping the connection
create_event_connection = publisher.EventCreate.Connect((LandscapeMapFileCreator creator,  LandscapeImages images,  int x,  int y) => {
		Log.Message("Handling Create event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
create_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
create_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
create_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Create events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventCreate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventCreate.Enabled = true;

```

</details>

### Members

---

## LandscapeMapFileCreator ( )

The LandscapeMapFileCreator constructor.
## void SetDownscaleFilter ( Landscape.TYPE_FILE_DATA file_data_type , Image.FILTER filter )

Sets a new filtering type to be used for image downscaling performed for LODs of the specified file data type.
### Arguments

- *[Landscape.TYPE_FILE_DATA](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#TYPE_FILE_DATA)* **file_data_type** - File data type.
- *[Image.FILTER](../../../../api/library/common/class.image_cs.md#FILTER)* **filter** - Filter type to be used for downscaling. See the [Unigine::Image Enumerations with FILTER_* prefixes](../../../../api/library/common/class.image_cs.md#FILTER_LINEAR).

## Image.FILTER GetDownscaleFilter ( Landscape.TYPE_FILE_DATA file_data_type )

Returns the current filtering type used for image downscaling performed for LODs of the specified file data type.
### Arguments

- *[Landscape.TYPE_FILE_DATA](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#TYPE_FILE_DATA)* **file_data_type** - File data type.

### Return value

Filter type used for image downscaling. See the [Unigine::Image Enumerations with FILTER_* prefixes](../../../../api/library/common/class.image_cs.md#FILTER_LINEAR).
## bool Run ( bool is_empty = false , bool is_safe = true )

Runs the landscape map file creation process. You can [set callbacks](#example) to be fired in the beginning, upon completion and during the process to monitor progress and display statistics. Creates the landscape map file path if it doesn�t exist yet (including subdirectories).
### Arguments

- *bool* **is_empty** - true to create an empty `.lmap` file (e.g., when you create a layer map to be manually sculpted from scratch using [brushes](../../../../editor2/brush_editor/index.md)), false - to get necessary data from the sources and put them to the generated `.lmap` file.
- *bool* **is_safe** - true to make the Engine automatically call *filesClose()/fileOpen()* methods when performing operations (before modifying an `.lmap` file the Engine should release files via *filesClose()*, while after modification *fileOpen()* should be called), false - to call *filesClose()/fileOpen()* methods manually. The Landscape class has two overloads for the *filesClose()* method: > **Notice:** When **is_safe = true** the Engine shall always call *filesClose(reload_files)* with complete data reloading.

  - [*filesClose()*](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#filesClose_void) - to be called in case of moving an `.lmap` file (no data reloading is performed as the file itself was not modified - saves time on reloading data)
  - [*filesClose(reload_files)*](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#filesClose_VECUGUID_void) - to be called in case of deleting or modifying an `.lmap` file.

### Return value

true if the operation is successful; otherwise, false.
