# Unigine.LandscapeMapFileCompression Class (CPP)

**Header:** #include <UnigineObjects.h>


Landscape Map File Compression class is used to compress and decompress `.lmap` file data using Zlib, LZ4, or Unigine's compression algorithm. The latter provides better compression results for 2D and 3D textures than LZ4 and Zlib without quality reduction.


## LandscapeMapFileCompression Class

### Members

## bool isCompressing () const

Returns the current value indicating if the compression is in progress.
### Return value

**true** if the compression is running; otherwise **false**.
## bool isDecompressing () const

Returns the current value indicating if the decompression is in progress.
### Return value

**true** if the decompression is running; otherwise **false**.
## int getProgress () const

Returns the current landscape map file compression progress.
### Return value

Current landscape map file compression progress (percentage).
## void setHeightCompressor ( Landscape::COMPRESSOR_TYPE compressor )

Sets a new type of the compressor used for height data compression.
### Arguments

- *[Landscape::COMPRESSOR_TYPE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#COMPRESSOR_TYPE)* **compressor** - The compression method used for the layer map.

## Landscape::COMPRESSOR_TYPE getHeightCompressor () const

Returns the current type of the compressor used for height data compression.
### Return value

Current compression method used for the layer map.
## void setAlbedoCompressor ( Landscape::COMPRESSOR_TYPE compressor )

Sets a new type of the compressor used for albedo data compression.
### Arguments

- *[Landscape::COMPRESSOR_TYPE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#COMPRESSOR_TYPE)* **compressor** - The compression method used for the layer map.

## Landscape::COMPRESSOR_TYPE getAlbedoCompressor () const

Returns the current type of the compressor used for albedo data compression.
### Return value

Current compression method used for the layer map.
## void setOpacityHeightCompressor ( Landscape::COMPRESSOR_TYPE compressor )

Sets a new type of the compressor used for compression of the opacity height data.
### Arguments

- *[Landscape::COMPRESSOR_TYPE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#COMPRESSOR_TYPE)* **compressor** - The compression method used for the layer map.

## Landscape::COMPRESSOR_TYPE getOpacityHeightCompressor () const

Returns the current type of the compressor used for compression of the opacity height data.
### Return value

Current compression method used for the layer map.
## void setEnabledAlbedoTextureCompression ( bool compression )

Sets a new value indicating if the compression of the albedo texture enabled.
### Arguments

- *bool* **compression** - Set **true** to enable the albedo texture compression; **false** - to disable it.

## bool isEnabledAlbedoTextureCompression () const

Returns the current value indicating if the compression of the albedo texture enabled.
### Return value

**true** if the albedo texture compression is enabled ; otherwise **false**.
## void setEnabledHeightTextureCompression ( bool compression )

Sets a new value indicating if the compression of the height texture enabled.
### Arguments

- *bool* **compression** - Set **true** to enable the height texture compression; **false** - to disable it.

## bool isEnabledHeightTextureCompression () const

Returns the current value indicating if the compression of the height texture enabled.
### Return value

**true** if the height texture compression is enabled ; otherwise **false**.
## void setEnabledOpacityHeightTextureCompression ( bool compression )

Sets a new value indicating if the compression of the opacity height texture enabled.
### Arguments

- *bool* **compression** - Set **true** to enable the opacity height texture compression; **false** - to disable it.

## bool isEnabledOpacityHeightTextureCompression () const

Returns the current value indicating if the compression of the opacity height texture enabled.
### Return value

**true** if the opacity height texture compression is enabled ; otherwise **false**.
## UGUID getGUID () const

Returns the current [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the `.lmap` file containing landscape map data.
### Return value

Current [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the `.lmap` file containing landscape map data.
## void setCacheDirectory ( const char * directory )

Sets a new path to the directory that is used to store the cache. By default the cache is located in the same place where the UnigineEditor's cache is (you can find it in the UnigineEditor *Settings* tab). If there is not enough memory, you can use another disk. A full copy of the current terrain will be temporarily stored in the cache directory, so you should take this into account when estimating the cache size. SSD is recommended for fast data copying.
### Arguments

- *const char ** **directory** - The path to the directory that stores the cache.

## const char * getCacheDirectory () const

Returns the current path to the directory that is used to store the cache. By default the cache is located in the same place where the UnigineEditor's cache is (you can find it in the UnigineEditor *Settings* tab). If there is not enough memory, you can use another disk. A full copy of the current terrain will be temporarily stored in the cache directory, so you should take this into account when estimating the cache size. SSD is recommended for fast data copying.
### Return value

Current path to the directory that stores the cache.
## Event<const Ptr < LandscapeMapFileCompression > &> getEventEnd () const

Event triggered on completion of the landscape map file compression. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<LandscapeMapFileCompression> & **compression**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the End event handler
void end_event_handler(const Ptr<LandscapeMapFileCompression> & compression)
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
publisher->getEventEnd().connect(end_event_connections, [](const Ptr<LandscapeMapFileCompression> & compression) {
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
	void event_handler(const Ptr<LandscapeMapFileCompression> & compression)
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
end_handler_id = publisher->getEventEnd().connect(e_connections, [](const Ptr<LandscapeMapFileCompression> & compression) {
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
## Event<const Ptr < LandscapeMapFileCompression > &> getEventProgress () const

Event triggered on the landscape map file compression progress. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<LandscapeMapFileCompression> & **compression**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Progress event handler
void progress_event_handler(const Ptr<LandscapeMapFileCompression> & compression)
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
publisher->getEventProgress().connect(progress_event_connections, [](const Ptr<LandscapeMapFileCompression> & compression) {
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
	void event_handler(const Ptr<LandscapeMapFileCompression> & compression)
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
progress_handler_id = publisher->getEventProgress().connect(e_connections, [](const Ptr<LandscapeMapFileCompression> & compression) {
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
## Event<const Ptr < LandscapeMapFileCompression > &> getEventBegin () const

Event triggered at the beginning of the landscape map file compression. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Ptr<LandscapeMapFileCompression> & **compression**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the Begin event handler
void begin_event_handler(const Ptr<LandscapeMapFileCompression> & compression)
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
publisher->getEventBegin().connect(begin_event_connections, [](const Ptr<LandscapeMapFileCompression> & compression) {
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
	void event_handler(const Ptr<LandscapeMapFileCompression> & compression)
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
begin_handler_id = publisher->getEventBegin().connect(e_connections, [](const Ptr<LandscapeMapFileCompression> & compression) {
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
---

## LandscapeMapFileCompression ( )

Constructor.
## bool compress ( bool is_safe )

Starts the landscape map file compression process.
### Arguments

- *bool* **is_safe** - true to make the Engine automatically call *filesClose()/fileOpen()* methods when performing operations (before modifying an `.lmap` file the Engine should release files via *filesClose()*, while after modification *fileOpen()* should be called), false � to call *filesClose()/fileOpen()* methods manually. The Landscape class has two overloads for the *filesClose()* method: > **Notice:** When **is_safe = true** the Engine shall always call *filesClose(reload_files)* with complete data reloading.

  - [*filesClose()*](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#filesClose_void) � to be called in case of moving an `.lmap` file (no data reloading is performed as the file itself was not modified � saves time on reloading data)
  - [*filesClose(reload_files)*](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#filesClose_VECUGUID_void) � to be called in case of deleting or modifying an `.lmap` file.

### Return value

true if the compression operation is successful; otherwise, false.
## bool decompress ( bool is_safe )

Starts the landscape map file decompression process.
### Arguments

- *bool* **is_safe** - true to make the Engine automatically call *filesClose()/fileOpen()* methods when performing operations (before modifying an `.lmap` file the Engine should release files via *filesClose()*, while after modification *fileOpen()* should be called), false � to call *filesClose()/fileOpen()* methods manually. The Landscape class has two overloads for the *filesClose()* method: > **Notice:** When **is_safe = true** the Engine shall always call *filesClose(reload_files)* with complete data reloading.

  - [*filesClose()*](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#filesClose_void) � to be called in case of moving an `.lmap` file (no data reloading is performed as the file itself was not modified � saves time on reloading data)
  - [*filesClose(reload_files)*](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#filesClose_VECUGUID_void) � to be called in case of deleting or modifying an `.lmap` file.

### Return value

true if the decompression operation is successful; otherwise, false.
## void stop ( )

Stops the landscape map file compression/decompression process.
## void setMaskCompressor ( int mask , Landscape::COMPRESSOR_TYPE compressor_type )

Sets the type of the compressor used for the specified mask.
### Arguments

- *int* **mask** - Mask number.
- *[Landscape::COMPRESSOR_TYPE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#COMPRESSOR_TYPE)* **compressor_type** - Compressor type:

  - 0 � None
  - 1 � Our Method
  - 2 � LZ4
  - 3 � Zlib

## void setMaskOpacityCompressor ( int mask , Landscape::COMPRESSOR_TYPE compressor_type )

Sets the type of the compressor used for the opacity data of the specified mask.
### Arguments

- *int* **mask** - Mask number.
- *[Landscape::COMPRESSOR_TYPE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#COMPRESSOR_TYPE)* **compressor_type** - Compressor type:

  - 0 � None
  - 1 � Our Method
  - 2 � LZ4
  - 3 � Zlib

## void setCompressorAll ( Landscape::COMPRESSOR_TYPE compressor_type )

Sets the type of the compressor used to compress all data.
### Arguments

- *[Landscape::COMPRESSOR_TYPE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#COMPRESSOR_TYPE)* **compressor_type** - Compressor type:

  - 0 � None
  - 1 � Our Method
  - 2 � LZ4
  - 3 � Zlib

## int getMaskCompressor ( int mask )

Returns the current type of the compressor used for the specified mask.
### Arguments

- *int* **mask** - Mask number.

### Return value

Compressor type:
- 0 � None
- 1 � Our Method
- 2 � LZ4
- 3 � Zlib


## int getMaskOpacityCompressor ( int mask )

Returns the current type of the compressor used for the opacity data of the specified mask.
### Arguments

- *int* **mask** - Mask number.

### Return value

Compressor type:
- 0 � None
- 1 � Our Method
- 2 � LZ4
- 3 � Zlib


## void setEnabledMaskTextureCompression ( int mask , bool enable )

Enables or disables compression of the specified mask texture.
### Arguments

- *int* **mask** - Mask number.
- *bool* **enable** - true to enable the mask texture compression; otherwise, false.

## void setEnabledMaskOpacityTextureCompression ( int mask , bool enable )

Enables or disables compression of the specified mask opacity texture.
### Arguments

- *int* **mask** - Mask number.
- *bool* **enable** - true to enable the compression of the mask opacity texture; otherwise, false.

## bool isEnabledMaskTextureCompression ( int mask )

Returns a value undicating if the mask texture compression is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

true if the mask texture compression is enabled; otherwise, false.
## bool isEnabledMaskOpacityTextureCompression ( int mask )

Returns the value indicating if the compression of the mask opacity texture is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

true if the mask opacity texture compression is enabled; otherwise, false.
