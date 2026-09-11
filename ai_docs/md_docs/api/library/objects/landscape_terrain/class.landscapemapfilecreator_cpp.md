# Unigine.LandscapeMapFileCreator Class (CPP)

**Header:** #include <UnigineObjects.h>


This class is used to generate a landscape map file (`.lmap`) to be used for [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) creation.


### Usage Example


```cpp
using namespace Math;
// EventConnections class instance to manage event subscriptions
EventConnections econnections;

// methods to be executed in the process of landscape map file creation
void create(const LandscapeMapFileCreatorPtr& creator)
{
	Log::message("Creating LMAP\n");
}
void progress(const LandscapeMapFileCreatorPtr& creator)
{
	Log::message("%d %f\n", int(creator->getProgress()), creator->getTimeSeconds());
}
void begin(const LandscapeMapFileCreatorPtr& creator)
{
	Log::message("%f\n", creator->getProgress());
}
void end(const LandscapeMapFileCreatorPtr& creator)
{
	Log::message("%f\n", creator->getTimeSeconds());
}

	// ...

	// defining grid size (2х2 tiles) and resolution
	ivec2 grid = ivec2(2, 2);
	ivec2 resolution = ivec2(2048) * grid;

	// creating a landscape map file creator and setting grid size, resolution, and path
	LandscapeMapFileCreatorPtr creator = LandscapeMapFileCreator::create();
	creator->setGrid(grid);
	creator->setResolution(resolution);
	creator->setPath("test.lmap");

	// subscribing to necessary events with our handlers
	creator->getEventCreate().connect(econnections, create);
	creator->getEventProgress().connect(econnections, progress);
	creator->getEventBegin().connect(econnections, begin);
	creator->getEventEnd().connect(econnections, end);

	// running the creator to generate a new "test.lmap" file
	creator->run();

	// ...

	// creating a new landscape layer map based on the created "test.lmap" file
	LandscapeLayerMapPtr landscape_map = LandscapeLayerMap::create();
	landscape_map->setPath("test.lmap");

	// ...

	// removing all event subscriptions somewhere on shutdown
	econnections.disconnectAll();


```


### See also


- C++ sample


## LandscapeMapFileCreator Class

### Members

## void setResolution ( const Math:: ivec2 & resolution )

Sets a new landscape map resolution.
### Arguments

- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md)&* **resolution** - The two-component vector (X, Y) representing landscape map resolution along X and Y axes, in pixels.

## Math:: ivec2 getResolution () const

Returns the current landscape map resolution.
### Return value

Current two-component vector (X, Y) representing landscape map resolution along X and Y axes, in pixels.
## void setGrid ( const Math:: ivec2 & grid )

Sets a new grid size for the landscape map.
### Arguments

- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md)&* **grid** - The two-component vector (X, Y) representing number of tiles of the landscape map along X and Y axes.

## Math:: ivec2 getGrid () const

Returns the current grid size for the landscape map.
### Return value

Current two-component vector (X, Y) representing number of tiles of the landscape map along X and Y axes.
## float getProgress () const

Returns the current landscape map file creation progress.
### Return value

Current landscape map file creation progress (percentage).
## double getTimeSeconds () const

Returns the current landscape map file creation time. You can use this method to get total file generation time when processing an End callback.
### Return value

Current landscape map file creation time, in seconds.
## void setPath ( const char * path )

Sets a new path to the generated `*.lmap` file.
### Arguments

- *const char ** **path** - The path to the generated `*.lmap` file.

## const char * getPath () const

Returns the current path to the generated `*.lmap` file.
### Return value

Current path to the generated `*.lmap` file.
## Event<const Ptr < LandscapeMapFileCreator > &> getEventEnd () const

Event triggered on completion of the landscape map file creation. The signature of the callback function must be as follows:
```cpp
void end_event_handler(const Ptr<LandscapeMapFileCreator> & creator)

```

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<LandscapeMapFileCreator> & **creator**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the End event handler
void end_event_handler(const Ptr<LandscapeMapFileCreator> & creator)
{
	Log::message("\Handling End event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections end_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventEnd().connect(end_event_connections, end_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventEnd().connect(end_event_connections, [](const Ptr<LandscapeMapFileCreator> & creator) {
		Log::message("\Handling End event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
end_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection end_event_connection;

// subscribe to the End event with a handler function keeping the connection
publisher->getEventEnd().connect(end_event_connection, end_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
end_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
end_event_connection.setEnabled(true);

// ...

// remove subscription to the End event via the connection
end_event_connection.disconnect();

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

	// A End event handler implemented as a class member
	void event_handler(const Ptr<LandscapeMapFileCreator> & creator)
	{
		Log::message("\Handling End event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventEnd().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId end_handler_id;

// subscribe to the End event with a lambda handler function and keeping connection ID
end_handler_id = publisher->getEventEnd().connect(e_connections, [](const Ptr<LandscapeMapFileCreator> & creator) {
		Log::message("\Handling End event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventEnd().disconnect(end_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all End events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventEnd().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventEnd().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < LandscapeMapFileCreator > &> getEventBegin () const

Event triggered at the beginning the landscape map file creation. The signature of the callback function must be as follows:
```cpp
void begin_event_handler(const Ptr<LandscapeMapFileCreator> & creator)

```

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<LandscapeMapFileCreator> & **creator**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Begin event handler
void begin_event_handler(const Ptr<LandscapeMapFileCreator> & creator)
{
	Log::message("\Handling Begin event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begin_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventBegin().connect(begin_event_connections, begin_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventBegin().connect(begin_event_connections, [](const Ptr<LandscapeMapFileCreator> & creator) {
		Log::message("\Handling Begin event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
begin_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection begin_event_connection;

// subscribe to the Begin event with a handler function keeping the connection
publisher->getEventBegin().connect(begin_event_connection, begin_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
begin_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
begin_event_connection.setEnabled(true);

// ...

// remove subscription to the Begin event via the connection
begin_event_connection.disconnect();

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

	// A Begin event handler implemented as a class member
	void event_handler(const Ptr<LandscapeMapFileCreator> & creator)
	{
		Log::message("\Handling Begin event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventBegin().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId begin_handler_id;

// subscribe to the Begin event with a lambda handler function and keeping connection ID
begin_handler_id = publisher->getEventBegin().connect(e_connections, [](const Ptr<LandscapeMapFileCreator> & creator) {
		Log::message("\Handling Begin event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventBegin().disconnect(begin_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Begin events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventBegin().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventBegin().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < LandscapeMapFileCreator > &> getEventProgress () const

Event triggered on landscape map file creation progress. The signature of the callback function must be as follows:
```cpp
void progress_event_handler(const Ptr<LandscapeMapFileCreator> & creator)

```

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<LandscapeMapFileCreator> & **creator**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Progress event handler
void progress_event_handler(const Ptr<LandscapeMapFileCreator> & creator)
{
	Log::message("\Handling Progress event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections progress_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventProgress().connect(progress_event_connections, progress_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventProgress().connect(progress_event_connections, [](const Ptr<LandscapeMapFileCreator> & creator) {
		Log::message("\Handling Progress event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
progress_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection progress_event_connection;

// subscribe to the Progress event with a handler function keeping the connection
publisher->getEventProgress().connect(progress_event_connection, progress_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
progress_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
progress_event_connection.setEnabled(true);

// ...

// remove subscription to the Progress event via the connection
progress_event_connection.disconnect();

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

	// A Progress event handler implemented as a class member
	void event_handler(const Ptr<LandscapeMapFileCreator> & creator)
	{
		Log::message("\Handling Progress event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventProgress().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId progress_handler_id;

// subscribe to the Progress event with a lambda handler function and keeping connection ID
progress_handler_id = publisher->getEventProgress().connect(e_connections, [](const Ptr<LandscapeMapFileCreator> & creator) {
		Log::message("\Handling Progress event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventProgress().disconnect(progress_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Progress events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventProgress().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventProgress().setEnabled(true);

```

</details>

### Return value

Event instance.
## Event<const Ptr < LandscapeMapFileCreator > &, const Ptr < LandscapeImages > &, int, int> getEventCreate () const

Event triggered on landscape layer map file creation. The signature of the callback function must be as follows:
```cpp
void create_event_handler(const Ptr<LandscapeMapFileCreator> & creator,  const Ptr<LandscapeImages> & images,  int x,  int y)

```

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<LandscapeMapFileCreator> & **creator**, const Ptr<LandscapeImages> & **images**, int **x**, int **y**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Create event handler
void create_event_handler(const Ptr<LandscapeMapFileCreator> & creator,  const Ptr<LandscapeImages> & images,  int x,  int y)
{
	Log::message("\Handling Create event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections create_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventCreate().connect(create_event_connections, create_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventCreate().connect(create_event_connections, [](const Ptr<LandscapeMapFileCreator> & creator,  const Ptr<LandscapeImages> & images,  int x,  int y) {
		Log::message("\Handling Create event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
create_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection create_event_connection;

// subscribe to the Create event with a handler function keeping the connection
publisher->getEventCreate().connect(create_event_connection, create_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
create_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
create_event_connection.setEnabled(true);

// ...

// remove subscription to the Create event via the connection
create_event_connection.disconnect();

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

	// A Create event handler implemented as a class member
	void event_handler(const Ptr<LandscapeMapFileCreator> & creator,  const Ptr<LandscapeImages> & images,  int x,  int y)
	{
		Log::message("\Handling Create event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventCreate().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId create_handler_id;

// subscribe to the Create event with a lambda handler function and keeping connection ID
create_handler_id = publisher->getEventCreate().connect(e_connections, [](const Ptr<LandscapeMapFileCreator> & creator,  const Ptr<LandscapeImages> & images,  int x,  int y) {
		Log::message("\Handling Create event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventCreate().disconnect(create_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all Create events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventCreate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventCreate().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## static LandscapeMapFileCreatorPtr create ( )

The LandscapeMapFileCreator constructor.
## void setDownscaleFilter ( Landscape::TYPE_FILE_DATA file_data_type , Image::FILTER filter )

Sets a new filtering type to be used for image downscaling performed for LODs of the specified file data type.
### Arguments

- *[Landscape::TYPE_FILE_DATA](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#TYPE_FILE_DATA)* **file_data_type** - File data type.
- *[Image::FILTER](../../../../api/library/common/class.image_cpp.md#FILTER)* **filter** - Filter type to be used for downscaling. See the [Unigine::Image Enumerations with FILTER_* prefixes](../../../../api/library/common/class.image_cpp.md#FILTER_LINEAR).

## Image::FILTER getDownscaleFilter ( Landscape::TYPE_FILE_DATA file_data_type ) const

Returns the current filtering type used for image downscaling performed for LODs of the specified file data type.
### Arguments

- *[Landscape::TYPE_FILE_DATA](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#TYPE_FILE_DATA)* **file_data_type** - File data type.

### Return value

Filter type used for image downscaling. See the [Unigine::Image Enumerations with FILTER_* prefixes](../../../../api/library/common/class.image_cpp.md#FILTER_LINEAR).
## bool run ( bool is_empty = false , bool is_safe = true )

Runs the landscape map file creation process. You can [set callbacks](#example) to be fired in the beginning, upon completion and during the process to monitor progress and display statistics. Creates the landscape map file path if it doesn�t exist yet (including subdirectories).
### Arguments

- *bool* **is_empty** - true to create an empty `.lmap` file (e.g., when you create a layer map to be manually sculpted from scratch using [brushes](../../../../editor2/brush_editor/index.md)), false - to get necessary data from the sources and put them to the generated `.lmap` file.
- *bool* **is_safe** - true to make the Engine automatically call *filesClose()/fileOpen()* methods when performing operations (before modifying an `.lmap` file the Engine should release files via *filesClose()*, while after modification *fileOpen()* should be called), false - to call *filesClose()/fileOpen()* methods manually. The Landscape class has two overloads for the *filesClose()* method: > **Notice:** When **is_safe = true** the Engine shall always call *filesClose(reload_files)* with complete data reloading.

  - [*filesClose()*](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#filesClose_void) - to be called in case of moving an `.lmap` file (no data reloading is performed as the file itself was not modified - saves time on reloading data)
  - [*filesClose(reload_files)*](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#filesClose_VECUGUID_void) - to be called in case of deleting or modifying an `.lmap` file.

### Return value

true if the operation is successful; otherwise, false.
