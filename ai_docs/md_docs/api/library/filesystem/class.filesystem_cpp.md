# Unigine::FileSystem Class (CPP)

**Header:** #include <UnigineFileSystem.h>

> **Notice:** This class is a singleton.


On the [Engine file system](../../../principles/filesystem/index_cpp.md) initialization, all files and packages stored in the `data` folder are added to the virtual file system automatically. At that, content of the ZIP and UNG packages is loaded into RAM as is (so, you'd better not store heavy content (e.g. terrains) in the packages).


Files and packages stored outside the `data` directory are also added to the virtual file system, if they are [mounted](../../../principles/filesystem/index_cpp.md#mount_points) (i.e. referenced by a mount point).

> **Notice:** If you add new files at run time, the Engine won't know anything about such files. To add the files to the virtual file system, use *[addVirtualFile()](#addVirtualFile_cstr_UGUID_bool_bool)*.


File System functions:


- Provide control over [asynchronous loading](../../../api/library/filesystem/class.asyncqueue_cpp.md) of files/meshes/images/nodes on demand under the `data` directory, including files in ZIP and UNG packages. Such packages are [automatically handled](../../../principles/filesystem/index_cpp.md#file_packages) by the Engine and all their files are automatically added to the file system.
- Allow adding directories (even with ZIP and UNG packages) that are [outside](../../../principles/filesystem/index_cpp.md#mount_points) the `data` directory and provide [control over loading](../../../api/library/filesystem/class.asyncqueue_cpp.md) such files.
- Allow adding ZIP and UNG packages that are [outside the `data`](../../../principles/filesystem/index_cpp.md#mount_points) directory. After that, files in such packages are accessed in a usual way, by specifying a path to the file only inside the package.
- Allow [caching](#addCacheFile_cstr_bool) files in the memory and [adding files to blobs](#addBlobFile_cstr_bool) if they are accessed or modified multiple times at run time.


Also methods of the FileSystem class can be used when implementing your own importer from an external format to UNIGINE-native ones. For example, you can store only the original file on the disk, files in UNIGINE-native formats can be stored in the virtual file system only.


> **Notice:** This class is in the **Unigine** namespace.


### Getting the Asset Filename


Using the [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of an asset or the path to the source file on a disk, you can get access to the filename the following way:


```cpp
String input = "guid://857e03518c10647cb16975abc15f0f0e66a04b15"; // asset should be referenced with a GUID

// for a texture there may be two possible filenames to be returned
//String input = ".runtimes/de/857e03518c10647cb16975abc15f0f0e66a04b15.texture"; // the texture may have a runtime version
//String input = "test/test.png"; // or the source version may be used as a runtime

// getting the virtual path
const UGUID &guid = FileSystem::getGUID(input); // GUID for the given file
const UGUID &asset_guid = FileSystemAssets::resolveAsset(guid); // corresponding asset GUID
const String &asset_virtual_filepath = FileSystem::getVirtualPath(asset_guid); // virtual path for the given file GUID

// getting and outputting the filename
Log::message("Filepath: %s\n", asset_virtual_filepath.get()); // virtual path
Log::message("Filename: %s\n", asset_virtual_filepath.filename().get()); // filename without the extension
Log::message("Basename: %s\n", asset_virtual_filepath.basename().get()); // filename with the extension

```


### See also


- [AsyncQueue Class](../../../api/library/filesystem/class.asyncqueue_cpp.md) to manage loading resources (files, images, meshes, and nodes) on demand.


## FileSystem Class

### Members

## int getNumModifiers () const

Returns the current total number of file modifiers registered in the file system.
### Return value

Current total number of file modifiers registered in the file system.
## static Event<const UGUID &, const char *> getEventFileChanged () const

Event triggered when the file is changed using the FileSystem API. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const UGUID & **guid**, const char * **path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FileChanged event handler
void filechanged_event_handler(const UGUID & guid,  const char * path)
{
	Log::message("\Handling FileChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections filechanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem::getEventFileChanged().connect(filechanged_event_connections, filechanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem::getEventFileChanged().connect(filechanged_event_connections, [](const UGUID & guid,  const char * path) {
		Log::message("\Handling FileChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
filechanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection filechanged_event_connection;

// subscribe to the FileChanged event with a handler function keeping the connection
FileSystem::getEventFileChanged().connect(filechanged_event_connection, filechanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
filechanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
filechanged_event_connection.setEnabled(true);

// ...

// remove subscription to the FileChanged event via the connection
filechanged_event_connection.disconnect();

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

	// A FileChanged event handler implemented as a class member
	void event_handler(const UGUID & guid,  const char * path)
	{
		Log::message("\Handling FileChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
FileSystem::getEventFileChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId filechanged_handler_id;

// subscribe to the FileChanged event with a lambda handler function and keeping connection ID
filechanged_handler_id = FileSystem::getEventFileChanged().connect(e_connections, [](const UGUID & guid,  const char * path) {
		Log::message("\Handling FileChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
FileSystem::getEventFileChanged().disconnect(filechanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FileChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem::getEventFileChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
FileSystem::getEventFileChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const UGUID &, const char *> getEventFileRemoved () const

Event triggered when the file is removed using the FileSystem API. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const UGUID & **guid**, const char * **path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FileRemoved event handler
void fileremoved_event_handler(const UGUID & guid,  const char * path)
{
	Log::message("\Handling FileRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fileremoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem::getEventFileRemoved().connect(fileremoved_event_connections, fileremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem::getEventFileRemoved().connect(fileremoved_event_connections, [](const UGUID & guid,  const char * path) {
		Log::message("\Handling FileRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
fileremoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection fileremoved_event_connection;

// subscribe to the FileRemoved event with a handler function keeping the connection
FileSystem::getEventFileRemoved().connect(fileremoved_event_connection, fileremoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
fileremoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
fileremoved_event_connection.setEnabled(true);

// ...

// remove subscription to the FileRemoved event via the connection
fileremoved_event_connection.disconnect();

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

	// A FileRemoved event handler implemented as a class member
	void event_handler(const UGUID & guid,  const char * path)
	{
		Log::message("\Handling FileRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
FileSystem::getEventFileRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId fileremoved_handler_id;

// subscribe to the FileRemoved event with a lambda handler function and keeping connection ID
fileremoved_handler_id = FileSystem::getEventFileRemoved().connect(e_connections, [](const UGUID & guid,  const char * path) {
		Log::message("\Handling FileRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
FileSystem::getEventFileRemoved().disconnect(fileremoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FileRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem::getEventFileRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
FileSystem::getEventFileRemoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const UGUID &, const char *> getEventFileAdded () const

Event triggered when the file is added using the FileSystem API. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const UGUID & **guid**, const char * **path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FileAdded event handler
void fileadded_event_handler(const UGUID & guid,  const char * path)
{
	Log::message("\Handling FileAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fileadded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem::getEventFileAdded().connect(fileadded_event_connections, fileadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem::getEventFileAdded().connect(fileadded_event_connections, [](const UGUID & guid,  const char * path) {
		Log::message("\Handling FileAdded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
fileadded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection fileadded_event_connection;

// subscribe to the FileAdded event with a handler function keeping the connection
FileSystem::getEventFileAdded().connect(fileadded_event_connection, fileadded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
fileadded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
fileadded_event_connection.setEnabled(true);

// ...

// remove subscription to the FileAdded event via the connection
fileadded_event_connection.disconnect();

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

	// A FileAdded event handler implemented as a class member
	void event_handler(const UGUID & guid,  const char * path)
	{
		Log::message("\Handling FileAdded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
FileSystem::getEventFileAdded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId fileadded_handler_id;

// subscribe to the FileAdded event with a lambda handler function and keeping connection ID
fileadded_handler_id = FileSystem::getEventFileAdded().connect(e_connections, [](const UGUID & guid,  const char * path) {
		Log::message("\Handling FileAdded event (lambda).\n");
	}
);

// remove the subscription later using the ID
FileSystem::getEventFileAdded().disconnect(fileadded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FileAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem::getEventFileAdded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
FileSystem::getEventFileAdded().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Vector <FilePath> &> getEventFilesChanged () const

Event triggered at the end of the *Engine::update()* containing the files changed during the frame. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Vector<FilePath> & **paths**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FilesChanged event handler
void fileschanged_event_handler(const Vector<FilePath> & paths)
{
	Log::message("\Handling FilesChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fileschanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem::getEventFilesChanged().connect(fileschanged_event_connections, fileschanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem::getEventFilesChanged().connect(fileschanged_event_connections, [](const Vector<FilePath> & paths) {
		Log::message("\Handling FilesChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
fileschanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection fileschanged_event_connection;

// subscribe to the FilesChanged event with a handler function keeping the connection
FileSystem::getEventFilesChanged().connect(fileschanged_event_connection, fileschanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
fileschanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
fileschanged_event_connection.setEnabled(true);

// ...

// remove subscription to the FilesChanged event via the connection
fileschanged_event_connection.disconnect();

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

	// A FilesChanged event handler implemented as a class member
	void event_handler(const Vector<FilePath> & paths)
	{
		Log::message("\Handling FilesChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
FileSystem::getEventFilesChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId fileschanged_handler_id;

// subscribe to the FilesChanged event with a lambda handler function and keeping connection ID
fileschanged_handler_id = FileSystem::getEventFilesChanged().connect(e_connections, [](const Vector<FilePath> & paths) {
		Log::message("\Handling FilesChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
FileSystem::getEventFilesChanged().disconnect(fileschanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FilesChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem::getEventFilesChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
FileSystem::getEventFilesChanged().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Vector <FilePath> &> getEventFilesRemoved () const

Event triggered at the end of the *Engine::update()* containing the files removed during the frame. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Vector<FilePath> & **paths**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FilesRemoved event handler
void filesremoved_event_handler(const Vector<FilePath> & paths)
{
	Log::message("\Handling FilesRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections filesremoved_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem::getEventFilesRemoved().connect(filesremoved_event_connections, filesremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem::getEventFilesRemoved().connect(filesremoved_event_connections, [](const Vector<FilePath> & paths) {
		Log::message("\Handling FilesRemoved event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
filesremoved_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection filesremoved_event_connection;

// subscribe to the FilesRemoved event with a handler function keeping the connection
FileSystem::getEventFilesRemoved().connect(filesremoved_event_connection, filesremoved_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
filesremoved_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
filesremoved_event_connection.setEnabled(true);

// ...

// remove subscription to the FilesRemoved event via the connection
filesremoved_event_connection.disconnect();

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

	// A FilesRemoved event handler implemented as a class member
	void event_handler(const Vector<FilePath> & paths)
	{
		Log::message("\Handling FilesRemoved event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
FileSystem::getEventFilesRemoved().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId filesremoved_handler_id;

// subscribe to the FilesRemoved event with a lambda handler function and keeping connection ID
filesremoved_handler_id = FileSystem::getEventFilesRemoved().connect(e_connections, [](const Vector<FilePath> & paths) {
		Log::message("\Handling FilesRemoved event (lambda).\n");
	}
);

// remove the subscription later using the ID
FileSystem::getEventFilesRemoved().disconnect(filesremoved_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FilesRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem::getEventFilesRemoved().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
FileSystem::getEventFilesRemoved().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const Vector <FilePath> &> getEventFilesAdded () const

Event triggered at the end of the *Engine::update()* containing the files added during the frame. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const Vector<FilePath> & **paths**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the FilesAdded event handler
void filesadded_event_handler(const Vector<FilePath> & paths)
{
	Log::message("\Handling FilesAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections filesadded_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem::getEventFilesAdded().connect(filesadded_event_connections, filesadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem::getEventFilesAdded().connect(filesadded_event_connections, [](const Vector<FilePath> & paths) {
		Log::message("\Handling FilesAdded event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
filesadded_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection filesadded_event_connection;

// subscribe to the FilesAdded event with a handler function keeping the connection
FileSystem::getEventFilesAdded().connect(filesadded_event_connection, filesadded_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
filesadded_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
filesadded_event_connection.setEnabled(true);

// ...

// remove subscription to the FilesAdded event via the connection
filesadded_event_connection.disconnect();

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

	// A FilesAdded event handler implemented as a class member
	void event_handler(const Vector<FilePath> & paths)
	{
		Log::message("\Handling FilesAdded event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
FileSystem::getEventFilesAdded().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId filesadded_handler_id;

// subscribe to the FilesAdded event with a lambda handler function and keeping connection ID
filesadded_handler_id = FileSystem::getEventFilesAdded().connect(e_connections, [](const Vector<FilePath> & paths) {
		Log::message("\Handling FilesAdded event (lambda).\n");
	}
);

// remove the subscription later using the ID
FileSystem::getEventFilesAdded().disconnect(filesadded_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all FilesAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem::getEventFilesAdded().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
FileSystem::getEventFilesAdded().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## Ptr < FileSystemMount > getMount ( const char * path ) const

Returns a [mount point](../../../principles/filesystem/index_cpp.md#mount_points) for the specified path.
> **Notice:** This method will return the [root mount](#getRootMount_FileSystemMount) for all files located directly in the `data` folder or its subfolders.


### Arguments

- *const char ** **path** - File path, for which a mount point is to be found. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cpp.md) class smart pointer on success; otherwise, **nullptr**.
## Ptr < FileSystemMount > getMount ( const UGUID & guid ) const

Returns a [mount point](../../../principles/filesystem/index_cpp.md#mount_points) for the specified [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
> **Notice:** This method will return the [root mount](#getRootMount_FileSystemMount) for all files located directly in the `data` folder or its subfolders.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for which a mount point is to be found.

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cpp.md) class smart pointer on success; otherwise, **nullptr**.
## void getMounts ( Vector < Ptr < FileSystemMount >> & OUT_container ) const

Returns a list of all [mount points](../../../principles/filesystem/index_cpp.md#mount_points) currently used by the file system and puts the to the specified output buffer.
> **Notice:** This list will not include the [root mount](#getRootMount_FileSystemMount).


### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cpp.md)>> &* **OUT_container** - Output buffer to store the list of all currently used [mount points](../../../api/library/filesystem/class.filesystemmount_cpp.md). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Ptr < FileSystemMount > getRootMount ( ) const

Returns the root mount of the file system. It mounts the `data` folder to the root of the virtual file system. The root mount cannot be unmounted.
### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cpp.md) class smart pointer for the root mount of the virtual file system.
## Ptr < FileSystemMount > createMount ( const char * absolute_path , const char * virtual_path , int access , const Vector < String > & exclusive_filters = {} , const Vector < String > & ignore_filters = {} , const Vector < String > & guidsdb_ignore_filters = {} , bool save_file = true )

Adds a new [mount point](../../../principles/filesystem/index_cpp.md#mount_points) for the specified external folder/package, virtual path and access mode. All mounted files are automatically added as known to the virtual file system.
### Arguments

- *const char ** **absolute_path** - Absolute path to the mounted folder/package.
- *const char ** **virtual_path** - [Virtual path](../../../principles/filesystem/index_cpp.md#virtual_paths) to the folder to which the contents of the external folder/package is to be mounted.
- *int* **access** - Mount point access mode, one of the *[FileSystemMount::ACCESS_*](../../../api/library/filesystem/class.filesystemmount_cpp.md#ACCESS_READONLY)* values.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **exclusive_filters** - List of wildcards (e.g., *"*.jpg", "some_folder_*/", "dir*/*1*.world", "editor_[1-9]*.log"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)) to be used to filter files in the mounted folder/package.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **ignore_filters** - List of wildcards (e.g., *"*.tmp", "cache_*/", "dir*/*1*.world", "editor_[1-9]*.log"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)) to be used to filter out files to be ignored in the mounted folder/package.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **guidsdb_ignore_filters** - List of wildcards (e.g., *"*.tmp", "cache_*/", "dir*/*1*.world", "editor_[1-9]*.log"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)) to be used to exclude files or directories from the GUIDs database.
- *bool* **save_file** - A flag indicating whether a `.umount` file should be written to disk.

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cpp.md) class smart pointer, if it was created successfully; otherwise, **nullptr**.
## Ptr < FileSystemMount > addMount ( const char * umount_path )

 Adds a new [mount point](../../../principles/filesystem/index_cpp.md#mount_points) using the data from the specified `*.umount` file.All mounted files are automatically added as known to the virtual file system.
### Arguments

- *const char ** **umount_path** - Absolute path to a `*.umount` file.

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cpp.md) class smart pointer, if it was created successfully; otherwise, **nullptr**.
## bool saveMountFile ( const char * umount_path ) const

Saves the specified `*.umount` file.
### Arguments

- *const char ** **umount_path** - [Mount point](../../../principles/filesystem/index_cpp.md#mount_points) file path.

### Return value

true if the specified `*.umount` file is saved successfully; otherwise, false.
## bool removeMount ( const char * path )

 Unmounts a [mount point](../../../principles/filesystem/index_cpp.md#mount_points) with a given path.
> **Notice:** The [root mount](#getRootMount_FileSystemMount) cannot be removed.


### Arguments

- *const char ** **path** - Absolute path to the mounted folder/package.

### Return value

true if the mount point with a given path is successfully unmounted; otherwise, false.
## void clearMounts ( )

 Unmounts all [mount points](../../../principles/filesystem/index_cpp.md#mount_points).
> **Notice:** This method does not remove the [root mount](#getRootMount_FileSystemMount).


## bool loadPackage ( const char * path )

 Loads an UNG or ZIP package into the file system. Note that the package should be [mounted](../../../principles/filesystem/index_cpp.md#mount_points), otherwise it won't be loaded.
> **Notice:** UNG packages without password protection can be loaded even if the engine has built-in password for the file system packages. For example, it is possible to load both the `core.ung` package without a password and the `my_assets.ung` package protected with a password.


### Arguments

- *const char ** **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).

### Return value

**true** if the package is loaded; otherwise, **false**.
## bool loadPackage ( const char * path , const char * extension )

 Loads a package with the specified extension (ung, zip, or pak) into the file system. Note that the package should be [mounted](../../../principles/filesystem/index_cpp.md#mount_points), otherwise it won't be loaded.
> **Notice:** UNG packages without password protection can be loaded even if the engine has built-in password for the file system packages. For example, it is possible to load both the `core.ung` package without a password and the `my_assets.ung` package protected with a password.


### Arguments

- *const char ** **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).
- *const char ** **extension** - Extension of a custom package, one of the following values:

  - ung
  - zip
  - pak

### Return value

**true** if the package is loaded; otherwise, **false**.
## bool removePackage ( const char * path )

Unloads an UNG or ZIP package from the file system.
### Arguments

- *const char ** **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).

### Return value

true if the package is removed; otherwise, false.
## void getSupportedPackagesExtensions ( Vector < String > & OUT_extensions ) const

Returns a list of registered extensions that can be loaded as a package.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_extensions** - An array to store registered extensions. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void getPackageVirtualFiles ( const char * path , Vector < String > & OUT_files ) const

Saves the list of names for all virtual files stored in the specified package to the specified string buffer.
### Arguments

- *const char ** **path** - Path to a custom package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_files** - String buffer to store the list of names for all virtual files stored in the specified package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void getPackageVirtualFiles ( const char * path , const char * extension , Vector < String > & OUT_files ) const

Saves the list of names for all virtual files stored in a package with the specified name and extension to the specified string buffer.
### Arguments

- *const char ** **path** - Path to a custom package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).
- *const char ** **extension** - Extension of a custom package, one of the following values:

  - ung
  - zip
  - pak
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_files** - String buffer to store the list of names for all virtual files stored in the specified package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void preloadExternPackage ( Package * package )

Loads the custom package before the file system initialization. The method should be called before the Engine init.
```cpp
// preload package
FileSystem::preloadExternPackage(new MyPackage());
// init engine
EnginePtr engine(argc, argv);

```


### Arguments

- *[Package](../../../api/library/filesystem/class.package_cpp.md) ** **package** - Custom package instance.

## void preloadExternPackage ( const char * virtual_path , Package * package )

Loads the custom package before the file system initialization and sets a virtual path to it. The method should be called before the Engine init.
### Arguments

- *const char ** **virtual_path** - Virtual path to a custom package.
- *[Package](../../../api/library/filesystem/class.package_cpp.md) ** **package** - Custom package instance.

## void clearPreloadedExternPackages ( )

Clears all [preloaded](#preloadExternPackage_Package_void) custom packages (packages loaded before the file system initialization).
## bool addExternPackage ( Package * package )

Adds a custom package to the virtual file system.
### Arguments

- *[Package](../../../api/library/filesystem/class.package_cpp.md) ** **package** - Custom package instance.

### Return value

true if the package is added successfully; otherwise, false.
## bool addExternPackage ( const char * path , Package * package )

Adds a custom package to the virtual file system and assigns a virtual path to it. The virtual path is obtained by using the given path.
### Arguments

- *const char ** **path** - Path to a custom package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).
- *[Package](../../../api/library/filesystem/class.package_cpp.md) ** **package** - Custom package instance.

### Return value

true if the package is added successfully; otherwise, false.
## void getVirtualFiles ( Vector < String > & OUT_files ) const

Saves the list of names for all known files registered in the file system to the specified string buffer.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_files** - String buffer to store the list of names for all known virtual files. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void getVirtualFiles ( Vector < UGUID > & OUT_files ) const

Saves the list of [GUIDs](../../../api/library/filesystem/class.uguid_cpp.md) for all known files registered in the file system to the specified string buffer.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[UGUID](../../../api/library/filesystem/class.uguid_cpp.md)> &* **OUT_files** - String buffer to store the list of GUIDs for all known virtual files. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool isVirtualFile ( const char * path ) const

Checks if the given file is known to the virtual file system.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).

### Return value

true if the file is known to the virtual file system; otherwise, false.
## bool isVirtualFile ( const UGUID & guid ) const

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) is known to the virtual file system and has a virtual path registered.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file is known to the virtual file system; otherwise, false.
## bool addVirtualFile ( const char * path , const UGUID & guid , bool must_exist = false )

Registers the regular file name as known virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) and appends it to the map used for fast searching. This method should be used when you need to add, for example, a new content to the project.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
- *bool* **must_exist** - A flag indicating whether the specified file must [exist](#isFileExist_cstr_bool).

### Return value

true if the file name is appended successfully; otherwise, false.
## UGUID addVirtualFile ( const char * path , bool must_exist = false )

Registers the regular file name as known virtual file and appends it to the map used for fast searching. This method should be used when you need to add, for example, a new content to the project.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *bool* **must_exist** - A flag indicating whether the specified file must [exist](#isFileExist_cstr_bool).

### Return value

File [GUID](../../../api/library/filesystem/class.uguid_cpp.md) if it was registered successfully or an empty GUID, otherwise.
## bool renameVirtualFile ( const char * path , const char * new_path )

Renames the specified known virtual file.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *const char ** **new_path** - New path for the file.

### Return value

true if the file is renamed successfully; otherwise, false.
## bool renameVirtualFile ( const char * path , const char * new_path , const UGUID & new_guid )

Renames the specified known file and assigns it the specified new [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *const char ** **new_path** - New path for the file.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_guid** - New [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the file.

### Return value

true if the file is renamed successfully; otherwise, false.
## bool renameVirtualFile ( const UGUID & guid , const char * new_path )

Renames the known virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
- *const char ** **new_path** - New path for the file.

### Return value

true if the file is renamed successfully; otherwise, false.
## bool renameVirtualFile ( const UGUID & guid , const char * new_path , const UGUID & new_guid )

Renames the known virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) and assigns it the specified new [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
- *const char ** **new_path** - New path for the file.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_guid** - New [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the file.

### Return value

true if the file is renamed successfully; otherwise, false.
## bool removeVirtualFile ( const char * path )

Removes the virtual file with the given name.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is removed successfully; otherwise, false.
## bool removeVirtualFile ( const UGUID & guid )

Removes the virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the known virtual file to remove.

### Return value

true if the file is removed successfully; otherwise, false.
## bool changeVirtualFile ( const char * path )

Marks the virtual file with the given name as modified. The corresponding *CALLBACK_FILE_CHANGED* signal is emitted. This method is used to notify the Engine that a resource has been modified and needs to be updated.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is successfully marked as modified; otherwise, false.
## bool changeVirtualFile ( const UGUID & guid )

Marks the virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) as modified. The corresponding *CALLBACK_FILE_CHANGED* signal is emitted. This method is used to notify the Engine that a resource has been modified and needs to be updated.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the known virtual file to remove.

### Return value

true if the file is successfully marked as modified; otherwise, false.
## void removeNonExistingVirtualFiles ( )

Removes all non-existing virtual files from the File System. These files aren't physically exist on the disk, however, they are added to the virtual file system. For example, it can be a blob or a cache file.
## bool isBlobFile ( const char * path ) const

Checks if the given file is [loaded](#addBlobFile_cstr_bool) to a blob.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is loaded to a blob successfully; otherwise, false.
## bool isBlobFile ( const UGUID & guid ) const

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) is [loaded](#addBlobFile_UGUID_bool) to a blob.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file is loaded to a blob successfully; otherwise, false.
## bool addBlobFile ( const char * path )

Adds a file into a blob. It can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is successfully added into a blob; otherwise, false.
## bool addBlobFile ( const UGUID & guid )

Adds a file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) into a blob. It can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file is successfully added into a blob; otherwise, false.
## bool removeBlobFile ( const char * path )

Removes a file from the blob. Blobbing can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is removed successfully; otherwise, false.
## bool removeBlobFile ( const UGUID & guid )

Removes a file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) from the blob. Blobbing can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file is removed successfully; otherwise, false.
## bool isCacheFile ( const char * path ) const

Checks if the given file is loaded into cache.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is added into cache; otherwise, false.
## bool isCacheFile ( const UGUID & guid ) const

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) is loaded into cache.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file is added into cache; otherwise, false.
## bool addCacheFile ( const char * path )

Caches a file in the memory. It can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is successfully added to cache; otherwise, false.
## bool addCacheFile ( const UGUID & guid )

Caches a file in the memory with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md). It can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file is successfully added to cache; otherwise, false.
## bool removeCacheFile ( const char * path )

Removes a cached file from the memory. Caching can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is successfully removed from cache; otherwise, false.
## bool removeCacheFile ( const UGUID & guid )

Removes a cached file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) from the memory. Caching can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file is successfully removed from cache; otherwise, false.
## bool isDiskFile ( const char * path ) const

Returns a value indicating if the specified file path is a path to a file on disk (i.e. not a package, a blob, or a cache file).
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the specified file path is a path to a file on disk; otherwise, false.
## bool isDiskFile ( const UGUID & guid ) const

Returns a value indicating if the file with the specified [GUID](../../../api/library/filesystem/class.uguid_cpp.md) is a file on disk.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file with the specified GUID is a file on disk; otherwise, false.
## bool isPackageFile ( const char * path ) const

Returns a value indicating if the specified file path is a path to a file inside a ZIP or UNG package.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).

### Return value

true if the specified file path is a path to a file inside a ZIP or UNG package; otherwise, false.
## bool isPackageFile ( const UGUID & guid ) const

Returns a value indicating if the file with the specified [GUID](../../../api/library/filesystem/class.uguid_cpp.md) is file inside a ZIP or UNG package.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file with the specified GUID is file inside a ZIP or UNG package; otherwise, false.
## String resolvePartialVirtualPath ( const char * path ) const

Converts the given [partial path](../../../principles/filesystem/index_cpp.md#partial) to a full virtual one.
> **Notice:** If the file isn't added to the virtual file system, the full virtual path won't be returned.

 For example, if you have the `data/project/image_1.tga` and want to use the partial virtual path `image_1.tga`, you should get the full virtual path first:
```cpp
// convert partial virtual to full virtual path
String full_virtual_path = FileSystem::resolvePartialVirtualPath("image_1.tga"); // project/image_1.tga is returned
// use the converted path
Image::create(full_virtual_path);

```


### Arguments

- *const char ** **path** - Partial path to be resolved.

### Return value

Full virtual path.
## String getVirtualPath ( const char * path ) const

Resolves a virtual path for the given file path. The following examples show particular cases of the method usage:
- If the given path is known for the virtual file system, the following can be returned: ```cpp String s1, s2, s3, s4; // absolute path to the folder s1 = FileSystem::getVirtualPath("D:/Unigine/data");			// an empty string s2 = FileSystem::getVirtualPath("D:/Unigine/data/");		// an empty string // path to assets in the folder s3 = FileSystem::getVirtualPath("asset://D:/Unigine/data");	// an empty string s4 = FileSystem::getVirtualPath("asset://D:/Unigine/data/");// an empty string ``` In all cases, an empty string is returned: a virtual path is always returned relative to the data directory, and in the example, the data directory itself is specified. If you specify a known file inside it, the corresponding virtual path will be returned: ```cpp String s = FileSystem::getVirtualPath("D:/Unigine/data/1.tga");		// "1.tga" ```
- If the given path is unknown for the virtual file system, the following can be returned: ```cpp // absolute path to the folder s1 = FileSystem::getVirtualPath("C:/temp");			// "C:/temp" s2 = FileSystem::getVirtualPath("C:/temp/");		// "C:/temp" // path to assets in the folder s3 = FileSystem::getVirtualPath("asset://C:/temp");	// "C:/temp" s4 = FileSystem::getVirtualPath("asset://C:/temp/");// "C:/temp" ``` In all cases, the normalized path to the folder is returned, as the specified folder is unknown for the virtual file system, and, therefore, no virtual path can be returned. The same is for files, for example: ```cpp s = FileSystem::getVirtualPath("C:/temp/1.tga");			// "C:/temp/1.tga" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index_cpp.md#mount_points) file. Here `mount_1` is the `mount_1.umount` mount point. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the virtual path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```cpp // virtual path to the file specified as an absolute one s1 = FileSystem::getVirtualPath("D:/Unigine/data/mounts/mount_1/1.tga");// "mounts/mount_1/1.tga" // absolute path to the file s2 = FileSystem::getVirtualPath("D:/extern_content/1.tga");				// "mounts/mount_1/1.tga" // full virtual path to the file s3 = FileSystem::getVirtualPath("mounts/mount_1/1.tga");				// "mounts/mount_1/1.tga" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index_cpp.md#mount_points) file stored in the nested mount points. Here `mount_1` and `mount_2` are the `mount_1.umount` and `mount_2.umount` mount points correspondingly. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the virtual path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```cpp // virtual path to the file specified as an absolute one s1 = FileSystem::getVirtualPath("D:/Unigine/data/mounts/mount_1/mount_2/1.tga");	// "mounts/mount_1/mount_2/1.tga" // absolute path to the file s2 = FileSystem::getVirtualPath("D:/extern_content_2/1.tga");						// "mounts/mount_1/mount_2/1.tga" // full virtual path to the file s3 = FileSystem::getVirtualPath("mounts/mount_1/mount_2/1.tga");					// "mounts/mount_1/mount_2/1.tga" ```


### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths), including a path to a folder. > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

Virtual path to the file relative to the `data` folder.
## String getVirtualPath ( const UGUID & guid ) const

Resolves a virtual path for the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Virtual path to the file relative to the `data` folder.
## String getAbsolutePath ( const char * path ) const

Resolves an absolute path for the given file path. The following examples show particular cases of the method usage:
- If the given path is known for the virtual file system, the following can be returned: ```cpp String s1, s2, s3, s4; // absolute path to the folder s1 = FileSystem::getAbsolutePath("D:/Unigine/data");			// "D:/Unigine/data" s2 = FileSystem::getAbsolutePath("D:/Unigine/data/");			// "D:/Unigine/data" // absolute path to assets in the folder s3 = FileSystem::getAbsolutePath("asset://D:/Unigine/data");	// "D:/Unigine/data" s4 = FileSystem::getAbsolutePath("asset://D:/Unigine/data/");	// "D:/Unigine/data" ```
- If the given path is unknown for the virtual file system, the following can be returned: ```cpp // absolute path to the folder s1 = FileSystem::getAbsolutePath("C:/temp");				// "C:/temp" s2 = FileSystem::getAbsolutePath("C:/temp/");				// "C:/temp" // absolute path to assets in the folder s3 = FileSystem::getAbsolutePath("asset://C:/temp");		// "C:/temp" s4 = FileSystem::getAbsolutePath("asset://C:/temp/");		// "C:/temp" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index_cpp.md#mount_points) file. Here `mount_1` is the `mount_1.umount` mount point. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the absolute path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```cpp // virtual path specified as an absolute one s1 = FileSystem::getAbsolutePath("D:/Unigine/data/mounts/mount_1/1.tga");		// "D:/extern_content/1.tga" // absolute path s2 = FileSystem::getAbsolutePath("D:/extern_content/1.tga");					// "D:/extern_content/1.tga" // virtual path s3 = FileSystem::getAbsolutePath("mounts/mount_1/1.tga");						// "D:/extern_content/1.tga" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index_cpp.md#mount_points) file stored in the nested mount points. Here `mount_1` and `mount_2` are the `mount_1.umount` and `mount_2.umount` mount points correspondingly. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the absolute path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```cpp // virtual path specified as an absolute one s1 = FileSystem::getAbsolutePath("D:/UnigineGIT/data/mounts/mount_1/mount_2/1.tga");// "D:/extern_content_2/1.tga" // absolute path s2 = FileSystem::getAbsolutePath("D:/extern_content_2/1.tga");						// "D:/extern_content_2/1.tga" // virtual path s3 = FileSystem::getAbsolutePath("mounts/mount_1/mount_2/1.tga");					// "D:/extern_content_2/1.tga" ```
- If the given path is a network path: ```cpp s1 = FileSystem::getAbsolutePath("//studio/work/shared_content/images.zip");			// "//studio/work/shared_content/images.zip" s2 = FileSystem::getAbsolutePath("\\\\studio\\work\\shared_content\\images.zip");		// "//studio/work/shared_content/images.zip" ```


### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths), including a path to a folder. > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

Absolute path to the file.
## String getAbsolutePath ( const UGUID & guid ) const


Resolves an absolute path for the given file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Absolute path to the file.
## String getPackageVirtualPath ( const char * path ) const

Resolves a virtual path for the given path to the package.
### Arguments

- *const char ** **path** - Path to a package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).

### Return value

Virtual path to the package.
## String getPackageVirtualPath ( const UGUID & guid ) const

Resolves a virtual path for the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Package [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Virtual path to the package.
## String getPackageAbsolutePath ( const char * path ) const

Resolves an absolute path for the given path to the package.
### Arguments

- *const char ** **path** - Path to a package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).

### Return value

Absolute path to the package.
## String getPackageAbsolutePath ( const UGUID & guid ) const


Resolves an absolute path for the given package [GUID](../../../api/library/filesystem/class.uguid_cpp.md).


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Package [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Absolute path to the package.
## String getExtension ( const char * path ) const

Returns the extension for the given file.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

File extension in lower case, if any; otherwise, an empty string.
## String getExtension ( const UGUID & guid ) const

Returns the extension for a file with the specified [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the file for which extension is to be returned.

### Return value

File extension in lower case if any; otherwise, an empty string.
## bool isFileExist ( const char * path ) const

Checks if the given file actually exists on the disk.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file exists; otherwise, false.
## bool isFileExist ( const UGUID & guid ) const

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_cpp.md) actually exists.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file exists; otherwise, false.
## bool isGUIDPath ( const char * path ) const

Returns a value indicating if the given path has a valid GUID path format (e.g. "guid://e231e15beff2309b8f87c30b2c105cc4d2399973)".
### Arguments

- *const char ** **path** - Path to be checked.

### Return value

true if the given path has a valid GUID path format; otherwise, false.
## bool isAssetPath ( const char * path ) const

Returns a value indicating if the given path has a valid [asset path format](../../../principles/filesystem/index_cpp.md#access_path) (e.g. `asset://1.tga`).
### Arguments

- *const char ** **path** - Path to be checked.

### Return value

true if the given path has a valid asset path format; otherwise, false.
## long long getMTime ( const char * path ) const

Returns the time of the last modification of the given file.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

Time of the last file modification. If there is no such file, **-1** will be returned.
## long long getMTime ( const UGUID & guid ) const

Returns the time of the last modification of the file with the specified GUID.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Time of the last file modification. If there is no such file, **-1** will be returned.
## bool loadGUIDs ( const char * path )

Loads file system [GUIDs](../../../api/library/filesystem/class.uguid_cpp.md) from the specified file.
### Arguments

- *const char ** **path** - Path to the file, where file system GUIDs are stored.

### Return value

true if file system GUIDs are loaded successfully; otherwise, false.
## bool saveGUIDs ( const char * path , bool binary = false ) const

Saves all file system [GUIDs](../../../api/library/filesystem/class.uguid_cpp.md) to the specified file in the specified format (json or binary).
### Arguments

- *const char ** **path** - Path to the file, where file system GUIDs are to be stored.
- *bool* **binary** - Binary file format flag. When the flag is set to true, the file system will save GUIDs to a binary file; otherwise, to a JSON file.

### Return value

true if all file system GUIDs are saved successfully; otherwise, false.
## UGUID generateGUID ( ) const

Generates a new [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Return value

New filesystem GUID if is was generated successfully; otherwise, an empty GUID.
## bool setGUID ( const char * path , const UGUID & guid )

Sets the specified [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the given file.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to be set for the file.

### Return value

true if the [GUID](../../../api/library/filesystem/class.uguid_cpp.md) is set successfully; otherwise, false.
## UGUID getGUID ( const char * path ) const

Returns the [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the specified path if this path is registered in the File System.
> **Notice:** In case you pass a guid-string *(guid://)*, this method will give you back the guid you specified (**without checking whether it is registered in the File System or not**).

### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

File [GUID](../../../api/library/filesystem/class.uguid_cpp.md) this path is registered in the File System; otherwise, an [empty GUID](../../../api/library/filesystem/class.uguid_cpp.md#empty).
## long long getFileSize ( const char * path ) const

Returns the size of the specified file.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

File size in bytes.
## long long getFileSize ( const UGUID & guid ) const

Returns the size of the file with the specified [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md)

### Return value

File size in bytes.
## String getModifier ( int num ) const

Returns the name of the given modifier.
### Arguments

- *int* **num** - ID number of the modifier.

### Return value

Modifier name.
## void addModifier ( const char * name )

Registers a new modifier in the file system.
### Arguments

- *const char ** **name** - Modifier name.

## void removeModifier ( const char * name )

Unregisters a given modifier in the file system.
### Arguments

- *const char ** **name** - Modifier name.

## void clearModifiers ( )

Unregister all modifiers in the file system.
## String guidToPath ( const UGUID & guid ) const

Returns the path to the file with the specified GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md)

### Return value

File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).
## UGUID pathToGuid ( const char * path )

Returns the GUID of the file to which the path is specified.
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (`asset://`). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

File [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
## bool isExternalFile ( const char * path ) const

Checks whether the given file path refers to an external file (located outside the `data`).
### Arguments

- *const char ** **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).

### Return value

true if the file is external; otherwise, false.
## bool isExternalFile ( const UGUID & guid ) const

Checks whether the given file path GUID refers to an external file (located outside the `data`).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cpp.md)

### Return value

true if the file is external; otherwise, false.
## bool isPackageLoaded ( const char * path )

Returns a value indicating if the specified package is loaded in the file system.
### Arguments

- *const char ** **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cpp.md#paths).

### Return value

true if the package is loaded; otherwise, false.
## void getPackagesVirtualPaths ( Vector < String > & OUT_packages_virtual_paths ) const

Returns virtual paths of all packages currently loaded in the file system.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_packages_virtual_paths** - An array to store virtual paths of all loaded packages. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
