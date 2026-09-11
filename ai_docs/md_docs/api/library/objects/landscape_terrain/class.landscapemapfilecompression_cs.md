# Unigine.LandscapeMapFileCompression Class (CS)


Landscape Map File Compression class is used to compress and decompress `.lmap` file data using Zlib, LZ4, or Unigine's compression algorithm. The latter provides better compression results for 2D and 3D textures than LZ4 and Zlib without quality reduction.


## LandscapeMapFileCompression Class

### Properties

## 🔒︎ bool IsCompressing

The value indicating if the compression is in progress.
## 🔒︎ bool IsDecompressing

The value indicating if the decompression is in progress.
## 🔒︎ int Progress

The landscape map file compression progress.
## Landscape.COMPRESSOR_TYPE HeightCompressor

The type of the compressor used for height data compression.
## Landscape.COMPRESSOR_TYPE AlbedoCompressor

The type of the compressor used for albedo data compression.
## Landscape.COMPRESSOR_TYPE OpacityHeightCompressor

The type of the compressor used for compression of the opacity height data.
## bool EnabledAlbedoTextureCompression

The value indicating if the compression of the albedo texture enabled.
## bool EnabledHeightTextureCompression

The value indicating if the compression of the height texture enabled.
## bool EnabledOpacityHeightTextureCompression

The value indicating if the compression of the opacity height texture enabled.
## 🔒︎ UGUID GUID

The [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the `.lmap` file containing landscape map data.
## string CacheDirectory

The path to the directory that is used to store the cache. By default the cache is located in the same place where the UnigineEditor's cache is (you can find it in the UnigineEditor *Settings* tab). If there is not enough memory, you can use another disk. A full copy of the current terrain will be temporarily stored in the cache directory, so you should take this into account when estimating the cache size. SSD is recommended for fast data copying.
## 🔒︎ Event< LandscapeMapFileCompression > EventEnd

The Event triggered on completion of the landscape map file compression. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(LandscapeMapFileCompression **compression**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the End event handler
void end_event_handler(LandscapeMapFileCompression compression)
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
publisher.EventEnd.Connect(end_event_connections, (LandscapeMapFileCompression compression) => {
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
end_event_connection = publisher.EventEnd.Connect((LandscapeMapFileCompression compression) => {
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

## 🔒︎ Event< LandscapeMapFileCompression > EventProgress

The Event triggered on the landscape map file compression progress. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(LandscapeMapFileCompression **compression**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Progress event handler
void progress_event_handler(LandscapeMapFileCompression compression)
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
publisher.EventProgress.Connect(progress_event_connections, (LandscapeMapFileCompression compression) => {
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
progress_event_connection = publisher.EventProgress.Connect((LandscapeMapFileCompression compression) => {
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

## 🔒︎ Event< LandscapeMapFileCompression > EventBegin

The Event triggered at the beginning of the landscape map file compression. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(LandscapeMapFileCompression **compression**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Begin event handler
void begin_event_handler(LandscapeMapFileCompression compression)
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
publisher.EventBegin.Connect(begin_event_connections, (LandscapeMapFileCompression compression) => {
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
begin_event_connection = publisher.EventBegin.Connect((LandscapeMapFileCompression compression) => {
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

### Members

---

## LandscapeMapFileCompression ( )

Constructor.
## bool Compress ( bool is_safe )

Starts the landscape map file compression process.
### Arguments

- *bool* **is_safe** - true to make the Engine automatically call *filesClose()/fileOpen()* methods when performing operations (before modifying an `.lmap` file the Engine should release files via *filesClose()*, while after modification *fileOpen()* should be called), false � to call *filesClose()/fileOpen()* methods manually. The Landscape class has two overloads for the *filesClose()* method: > **Notice:** When **is_safe = true** the Engine shall always call *filesClose(reload_files)* with complete data reloading.

  - [*filesClose()*](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#filesClose_void) � to be called in case of moving an `.lmap` file (no data reloading is performed as the file itself was not modified � saves time on reloading data)
  - [*filesClose(reload_files)*](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#filesClose_VECUGUID_void) � to be called in case of deleting or modifying an `.lmap` file.

### Return value

true if the compression operation is successful; otherwise, false.
## bool Decompress ( bool is_safe )

Starts the landscape map file decompression process.
### Arguments

- *bool* **is_safe** - true to make the Engine automatically call *filesClose()/fileOpen()* methods when performing operations (before modifying an `.lmap` file the Engine should release files via *filesClose()*, while after modification *fileOpen()* should be called), false � to call *filesClose()/fileOpen()* methods manually. The Landscape class has two overloads for the *filesClose()* method: > **Notice:** When **is_safe = true** the Engine shall always call *filesClose(reload_files)* with complete data reloading.

  - [*filesClose()*](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#filesClose_void) � to be called in case of moving an `.lmap` file (no data reloading is performed as the file itself was not modified � saves time on reloading data)
  - [*filesClose(reload_files)*](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#filesClose_VECUGUID_void) � to be called in case of deleting or modifying an `.lmap` file.

### Return value

true if the decompression operation is successful; otherwise, false.
## void Stop ( )

Stops the landscape map file compression/decompression process.
## void SetMaskCompressor ( int mask , Landscape.COMPRESSOR_TYPE compressor_type )

Sets the type of the compressor used for the specified mask.
### Arguments

- *int* **mask** - Mask number.
- *[Landscape.COMPRESSOR_TYPE](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#COMPRESSOR_TYPE)* **compressor_type** - Compressor type:

  - 0 � None
  - 1 � Our Method
  - 2 � LZ4
  - 3 � Zlib

## void SetMaskOpacityCompressor ( int mask , Landscape.COMPRESSOR_TYPE compressor_type )

Sets the type of the compressor used for the opacity data of the specified mask.
### Arguments

- *int* **mask** - Mask number.
- *[Landscape.COMPRESSOR_TYPE](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#COMPRESSOR_TYPE)* **compressor_type** - Compressor type:

  - 0 � None
  - 1 � Our Method
  - 2 � LZ4
  - 3 � Zlib

## void SetCompressorAll ( Landscape.COMPRESSOR_TYPE compressor_type )

Sets the type of the compressor used to compress all data.
### Arguments

- *[Landscape.COMPRESSOR_TYPE](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#COMPRESSOR_TYPE)* **compressor_type** - Compressor type:

  - 0 � None
  - 1 � Our Method
  - 2 � LZ4
  - 3 � Zlib

## int GetMaskCompressor ( int mask )

Returns the current type of the compressor used for the specified mask.
### Arguments

- *int* **mask** - Mask number.

### Return value

Compressor type:
- 0 � None
- 1 � Our Method
- 2 � LZ4
- 3 � Zlib


## int GetMaskOpacityCompressor ( int mask )

Returns the current type of the compressor used for the opacity data of the specified mask.
### Arguments

- *int* **mask** - Mask number.

### Return value

Compressor type:
- 0 � None
- 1 � Our Method
- 2 � LZ4
- 3 � Zlib


## void SetEnabledMaskTextureCompression ( int mask , bool enable )

Enables or disables compression of the specified mask texture.
### Arguments

- *int* **mask** - Mask number.
- *bool* **enable** - true to enable the mask texture compression; otherwise, false.

## void SetEnabledMaskOpacityTextureCompression ( int mask , bool enable )

Enables or disables compression of the specified mask opacity texture.
### Arguments

- *int* **mask** - Mask number.
- *bool* **enable** - true to enable the compression of the mask opacity texture; otherwise, false.

## bool IsEnabledMaskTextureCompression ( int mask )

Returns a value undicating if the mask texture compression is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

true if the mask texture compression is enabled; otherwise, false.
## bool IsEnabledMaskOpacityTextureCompression ( int mask )

Returns the value indicating if the compression of the mask opacity texture is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

true if the mask opacity texture compression is enabled; otherwise, false.
