# Unigine::FileSystem Class (CS)

> **Notice:** This class is a singleton.


On the [Engine file system](../../../principles/filesystem/index_cs.md) initialization, all files and packages stored in the `data` folder are added to the virtual file system automatically. At that, content of the ZIP and UNG packages is loaded into RAM as is (so, you'd better not store heavy content (e.g. terrains) in the packages).


Files and packages stored outside the `data` directory are also added to the virtual file system, if they are [mounted](../../../principles/filesystem/index_cs.md#mount_points) (i.e. referenced by a mount point).

> **Notice:** If you add new files at run time, the Engine won't know anything about such files. To add the files to the virtual file system, use *[addVirtualFile()](#addVirtualFile_cstr_UGUID_bool_bool)*.


File System functions:


- Provide control over [asynchronous loading](../../../api/library/filesystem/class.asyncqueue_cs.md) of files/meshes/images/nodes on demand under the `data` directory, including files in ZIP and UNG packages. Such packages are [automatically handled](../../../principles/filesystem/index_cs.md#file_packages) by the Engine and all their files are automatically added to the file system.
- Allow adding directories (even with ZIP and UNG packages) that are [outside](../../../principles/filesystem/index_cs.md#mount_points) the `data` directory and provide [control over loading](../../../api/library/filesystem/class.asyncqueue_cs.md) such files.
- Allow adding ZIP and UNG packages that are [outside the `data`](../../../principles/filesystem/index_cs.md#mount_points) directory. After that, files in such packages are accessed in a usual way, by specifying a path to the file only inside the package.
- Allow [caching](#addCacheFile_cstr_bool) files in the memory and [adding files to blobs](#addBlobFile_cstr_bool) if they are accessed or modified multiple times at run time.


Also methods of the FileSystem class can be used when implementing your own importer from an external format to UNIGINE-native ones. For example, you can store only the original file on the disk, files in UNIGINE-native formats can be stored in the virtual file system only.


> **Notice:** This class is in the **Unigine** namespace.


### Getting the Asset Filename


Using the [GUID](../../../api/library/filesystem/class.uguid_cs.md) of an asset or the path to the source file on a disk, you can get access to the filename the following way:


```csharp
String input = "guid://a428fd98ab66641782c2328a2fe88061d7dd1e4c"; // asset should be referenced with a GUID

// for a texture there may be two possible filenames to be returned
//String input = ".runtimes/de/a428fd98ab66641782c2328a2fe88061d7dd1e4c.texture"; // the texture may have a runtime version
//String input = "test/test.png"; // or the source version may be used as a runtime

// getting the virtual path
UGUID guid = FileSystem.GetGUID(input); // GUID for the given file
UGUID asset_guid = FileSystemAssets.ResolveAsset(guid); // corresponding asset GUID
String asset_virtual_filepath = FileSystem.GetVirtualPath(asset_guid); // virtual path for the given file GUID

// getting and outputting the filename
Log.Message("Filepath: {0}\n", asset_virtual_filepath); // virtual path
Log.Message("Filename: {0}\n", System.IO.Path.GetFileNameWithoutExtension(asset_virtual_filepath)); // filename without the extension
Log.Message("Basename: {0}\n", System.IO.Path.GetFileName(asset_virtual_filepath)); // filename with the extension

```


### See also


- [AsyncQueue Class](../../../api/library/filesystem/class.asyncqueue_cs.md) to manage loading resources (files, images, meshes, and nodes) on demand.


## FileSystem Class

### Properties

## 🔒︎ int NumModifiers

The total number of file modifiers registered in the file system.
## 🔒︎ Event< UGUID , string> EventFileChanged

The Event triggered when the file is changed using the FileSystem API. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(UGUID **guid**, string **path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FileChanged event handler
void filechanged_event_handler(UGUID guid,  string path)
{
	Log.Message("\Handling FileChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections filechanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem.EventFileChanged.Connect(filechanged_event_connections, filechanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem.EventFileChanged.Connect(filechanged_event_connections, (UGUID guid,  string path) => {
		Log.Message("Handling FileChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
filechanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FileChanged event with a handler function
FileSystem.EventFileChanged.Connect(filechanged_event_handler);

// remove subscription to the FileChanged event later by the handler function
FileSystem.EventFileChanged.Disconnect(filechanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection filechanged_event_connection;

// subscribe to the FileChanged event with a lambda handler function and keeping the connection
filechanged_event_connection = FileSystem.EventFileChanged.Connect((UGUID guid,  string path) => {
		Log.Message("Handling FileChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
filechanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
filechanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
filechanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FileChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem.EventFileChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
FileSystem.EventFileChanged.Enabled = true;

```

</details>

## 🔒︎ Event< UGUID , string> EventFileRemoved

The Event triggered when the file is removed using the FileSystem API. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(UGUID **guid**, string **path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FileRemoved event handler
void fileremoved_event_handler(UGUID guid,  string path)
{
	Log.Message("\Handling FileRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fileremoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem.EventFileRemoved.Connect(fileremoved_event_connections, fileremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem.EventFileRemoved.Connect(fileremoved_event_connections, (UGUID guid,  string path) => {
		Log.Message("Handling FileRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
fileremoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FileRemoved event with a handler function
FileSystem.EventFileRemoved.Connect(fileremoved_event_handler);

// remove subscription to the FileRemoved event later by the handler function
FileSystem.EventFileRemoved.Disconnect(fileremoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection fileremoved_event_connection;

// subscribe to the FileRemoved event with a lambda handler function and keeping the connection
fileremoved_event_connection = FileSystem.EventFileRemoved.Connect((UGUID guid,  string path) => {
		Log.Message("Handling FileRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
fileremoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
fileremoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
fileremoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FileRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem.EventFileRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
FileSystem.EventFileRemoved.Enabled = true;

```

</details>

## 🔒︎ Event< UGUID , string> EventFileAdded

The Event triggered when the file is added using the FileSystem API. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(UGUID **guid**, string **path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FileAdded event handler
void fileadded_event_handler(UGUID guid,  string path)
{
	Log.Message("\Handling FileAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fileadded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem.EventFileAdded.Connect(fileadded_event_connections, fileadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem.EventFileAdded.Connect(fileadded_event_connections, (UGUID guid,  string path) => {
		Log.Message("Handling FileAdded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
fileadded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FileAdded event with a handler function
FileSystem.EventFileAdded.Connect(fileadded_event_handler);

// remove subscription to the FileAdded event later by the handler function
FileSystem.EventFileAdded.Disconnect(fileadded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection fileadded_event_connection;

// subscribe to the FileAdded event with a lambda handler function and keeping the connection
fileadded_event_connection = FileSystem.EventFileAdded.Connect((UGUID guid,  string path) => {
		Log.Message("Handling FileAdded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
fileadded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
fileadded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
fileadded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FileAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem.EventFileAdded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
FileSystem.EventFileAdded.Enabled = true;

```

</details>

## 🔒︎ Event< UGUID , string> EventFilesChanged

The Event triggered at the end of the Engine's *Update()* containing the files changed during the frame. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(FilePath[] **paths**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FilesChanged event handler
void fileschanged_event_handler(FilePath[] paths)
{
	Log.Message("\Handling FilesChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections fileschanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem.EventFilesChanged.Connect(fileschanged_event_connections, fileschanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem.EventFilesChanged.Connect(fileschanged_event_connections, (FilePath[] paths) => {
		Log.Message("Handling FilesChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
fileschanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FilesChanged event with a handler function
FileSystem.EventFilesChanged.Connect(fileschanged_event_handler);

// remove subscription to the FilesChanged event later by the handler function
FileSystem.EventFilesChanged.Disconnect(fileschanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection fileschanged_event_connection;

// subscribe to the FilesChanged event with a lambda handler function and keeping the connection
fileschanged_event_connection = FileSystem.EventFilesChanged.Connect((FilePath[] paths) => {
		Log.Message("Handling FilesChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
fileschanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
fileschanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
fileschanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FilesChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem.EventFilesChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
FileSystem.EventFilesChanged.Enabled = true;

```

</details>

## 🔒︎ Event< UGUID , string> EventFilesRemoved

The Event triggered at the end of the Engine's *Update()* containing the files removed during the frame. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(FilePath[] **paths**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FilesRemoved event handler
void filesremoved_event_handler(FilePath[] paths)
{
	Log.Message("\Handling FilesRemoved event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections filesremoved_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem.EventFilesRemoved.Connect(filesremoved_event_connections, filesremoved_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem.EventFilesRemoved.Connect(filesremoved_event_connections, (FilePath[] paths) => {
		Log.Message("Handling FilesRemoved event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
filesremoved_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FilesRemoved event with a handler function
FileSystem.EventFilesRemoved.Connect(filesremoved_event_handler);

// remove subscription to the FilesRemoved event later by the handler function
FileSystem.EventFilesRemoved.Disconnect(filesremoved_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection filesremoved_event_connection;

// subscribe to the FilesRemoved event with a lambda handler function and keeping the connection
filesremoved_event_connection = FileSystem.EventFilesRemoved.Connect((FilePath[] paths) => {
		Log.Message("Handling FilesRemoved event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
filesremoved_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
filesremoved_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
filesremoved_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FilesRemoved events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem.EventFilesRemoved.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
FileSystem.EventFilesRemoved.Enabled = true;

```

</details>

## 🔒︎ Event< UGUID , string> EventFilesAdded

The Event triggered at the end of the Engine's *Update()* containing the files added during the frame. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(FilePath[] **paths**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the FilesAdded event handler
void filesadded_event_handler(FilePath[] paths)
{
	Log.Message("\Handling FilesAdded event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections filesadded_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
FileSystem.EventFilesAdded.Connect(filesadded_event_connections, filesadded_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
FileSystem.EventFilesAdded.Connect(filesadded_event_connections, (FilePath[] paths) => {
		Log.Message("Handling FilesAdded event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
filesadded_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the FilesAdded event with a handler function
FileSystem.EventFilesAdded.Connect(filesadded_event_handler);

// remove subscription to the FilesAdded event later by the handler function
FileSystem.EventFilesAdded.Disconnect(filesadded_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection filesadded_event_connection;

// subscribe to the FilesAdded event with a lambda handler function and keeping the connection
filesadded_event_connection = FileSystem.EventFilesAdded.Connect((FilePath[] paths) => {
		Log.Message("Handling FilesAdded event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
filesadded_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
filesadded_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
filesadded_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring FilesAdded events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
FileSystem.EventFilesAdded.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
FileSystem.EventFilesAdded.Enabled = true;

```

</details>

### Members

---

## FileSystemMount GetMount ( string path )

Returns a [mount point](../../../principles/filesystem/index_cs.md#mount_points) for the specified path.
> **Notice:** This method will return the [root mount](#getRootMount_FileSystemMount) for all files located directly in the `data` folder or its subfolders.


### Arguments

- *string* **path** - File path, for which a mount point is to be found. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cs.md) class instance on success; otherwise, **nullptr**.
## FileSystemMount GetMount ( UGUID guid )

Returns a [mount point](../../../principles/filesystem/index_cs.md#mount_points) for the specified [GUID](../../../api/library/filesystem/class.uguid_cs.md).
> **Notice:** This method will return the [root mount](#getRootMount_FileSystemMount) for all files located directly in the `data` folder or its subfolders.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md) for which a mount point is to be found.

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cs.md) class instance on success; otherwise, **nullptr**.
## void GetMounts ( FileSystemMount [] OUT_container )

Returns a list of all [mount points](../../../principles/filesystem/index_cs.md#mount_points) currently used by the file system and puts the to the specified output buffer.
> **Notice:** This list will not include the [root mount](#getRootMount_FileSystemMount).


### Arguments

- *[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cs.md)[]* **OUT_container** - Output buffer to store the list of all currently used [mount points](../../../api/library/filesystem/class.filesystemmount_cs.md). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## FileSystemMount GetRootMount ( )

Returns the root mount of the file system. It mounts the `data` folder to the root of the virtual file system. The root mount cannot be unmounted.
### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cs.md) class instance for the root mount of the virtual file system.
## FileSystemMount CreateMount ( string absolute_path , string virtual_path , int access , string[] exclusive_filters = {} , string[] ignore_filters = {} , string[] guidsdb_ignore_filters = {} , bool save_file = true )

Adds a new [mount point](../../../principles/filesystem/index_cs.md#mount_points) for the specified external folder/package, virtual path and access mode. All mounted files are automatically added as known to the virtual file system.
### Arguments

- *string* **absolute_path** - Absolute path to the mounted folder/package.
- *string* **virtual_path** - [Virtual path](../../../principles/filesystem/index_cs.md#virtual_paths) to the folder to which the contents of the external folder/package is to be mounted.
- *int* **access** - Mount point access mode, one of the *[FileSystemMount.ACCESS_*](../../../api/library/filesystem/class.filesystemmount_cs.md#ACCESS_READONLY)* values.
- *string[]* **exclusive_filters** - List of wildcards (e.g., *"*.jpg", "some_folder_*/", "dir*/*1*.world", "editor_[1-9]*.log"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)) to be used to filter files in the mounted folder/package.
- *string[]* **ignore_filters** - List of wildcards (e.g., *"*.tmp", "cache_*/", "dir*/*1*.world", "editor_[1-9]*.log"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)) to be used to filter out files to be ignored in the mounted folder/package.
- *string[]* **guidsdb_ignore_filters** - List of wildcards (e.g., *"*.tmp", "cache_*/", "dir*/*1*.world", "editor_[1-9]*.log"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)) to be used to exclude files or directories from the GUIDs database.
- *bool* **save_file** - A flag indicating whether a `.umount` file should be written to disk.

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cs.md) class instance, if it was created successfully; otherwise, **nullptr**.
## FileSystemMount AddMount ( string umount_path )

 Adds a new [mount point](../../../principles/filesystem/index_cs.md#mount_points) using the data from the specified `*.umount` file.All mounted files are automatically added as known to the virtual file system.
### Arguments

- *string* **umount_path** - Absolute path to a `*.umount` file.

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_cs.md) class instance, if it was created successfully; otherwise, **nullptr**.
## bool SaveMountFile ( string umount_path )

Saves the specified `*.umount` file.
### Arguments

- *string* **umount_path** - [Mount point](../../../principles/filesystem/index_cs.md#mount_points) file path.

### Return value

true if the specified `*.umount` file is saved successfully; otherwise, false.
## bool RemoveMount ( string path )

 Unmounts a [mount point](../../../principles/filesystem/index_cs.md#mount_points) with a given path.
> **Notice:** The [root mount](#getRootMount_FileSystemMount) cannot be removed.


### Arguments

- *string* **path** - Absolute path to the mounted folder/package.

### Return value

true if the mount point with a given path is successfully unmounted; otherwise, false.
## void ClearMounts ( )

 Unmounts all [mount points](../../../principles/filesystem/index_cs.md#mount_points).
> **Notice:** This method does not remove the [root mount](#getRootMount_FileSystemMount).


## bool LoadPackage ( string path )

 Loads an UNG or ZIP package into the file system. Note that the package should be [mounted](../../../principles/filesystem/index_cs.md#mount_points), otherwise it won't be loaded.
> **Notice:** UNG packages without password protection can be loaded even if the engine has built-in password for the file system packages. For example, it is possible to load both the `core.ung` package without a password and the `my_assets.ung` package protected with a password.


### Arguments

- *string* **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).

### Return value

**true** if the package is loaded; otherwise, **false**.
## bool LoadPackage ( string path , string extension )

 Loads a package with the specified extension (ung, zip, or pak) into the file system. Note that the package should be [mounted](../../../principles/filesystem/index_cs.md#mount_points), otherwise it won't be loaded.
> **Notice:** UNG packages without password protection can be loaded even if the engine has built-in password for the file system packages. For example, it is possible to load both the `core.ung` package without a password and the `my_assets.ung` package protected with a password.


### Arguments

- *string* **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).
- *string* **extension** - Extension of a custom package, one of the following values:

  - ung
  - zip
  - pak

### Return value

**true** if the package is loaded; otherwise, **false**.
## bool RemovePackage ( string path )

Unloads an UNG or ZIP package from the file system.
### Arguments

- *string* **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).

### Return value

true if the package is removed; otherwise, false.
## void GetSupportedPackagesExtensions ( string[] OUT_extensions )

Returns a list of registered extensions that can be loaded as a package.
### Arguments

- *string[]* **OUT_extensions** - An array to store registered extensions. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void GetPackageVirtualFiles ( string path , string[] OUT_files )

Saves the list of names for all virtual files stored in the specified package to the specified string buffer.
### Arguments

- *string* **path** - Path to a custom package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).
- *string[]* **OUT_files** - String buffer to store the list of names for all virtual files stored in the specified package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void GetPackageVirtualFiles ( string path , string extension , string[] OUT_files )

Saves the list of names for all virtual files stored in a package with the specified name and extension to the specified string buffer.
### Arguments

- *string* **path** - Path to a custom package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).
- *string* **extension** - Extension of a custom package, one of the following values:

  - ung
  - zip
  - pak
- *string[]* **OUT_files** - String buffer to store the list of names for all virtual files stored in the specified package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void preloadExternPackage ( Package package )

Loads the custom package before the file system initialization. The method should be called before the Engine init.
```csharp
// preload package
MyPackage package = new MyPackage();
FileSystem.preloadExternPackage(package);
// init engine
Engine engine = Engine.init(Engine.VERSION, args);

```


### Arguments

- *[Package](../../../api/library/filesystem/class.package_cs.md)* **package** - Custom package instance.

## void preloadExternPackage ( string virtual_path , Package package )

Loads the custom package before the file system initialization and sets a virtual path to it. The method should be called before the Engine init.
### Arguments

- *string* **virtual_path** - Virtual path to a custom package.
- *[Package](../../../api/library/filesystem/class.package_cs.md)* **package** - Custom package instance.

## void clearPreloadedExternPackages ( )

Clears all [preloaded](#preloadExternPackage_Package_void) custom packages (packages loaded before the file system initialization).
## bool addExternPackage ( Package package )

Adds a custom package to the virtual file system.
### Arguments

- *[Package](../../../api/library/filesystem/class.package_cs.md)* **package** - Custom package instance.

### Return value

true if the package is added successfully; otherwise, false.
## bool addExternPackage ( string path , Package package )

Adds a custom package to the virtual file system and assigns a virtual path to it. The virtual path is obtained by using the given path.
### Arguments

- *string* **path** - Path to a custom package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).
- *[Package](../../../api/library/filesystem/class.package_cs.md)* **package** - Custom package instance.

### Return value

true if the package is added successfully; otherwise, false.
## void GetVirtualFiles ( string[] OUT_files )

Saves the list of names for all known files registered in the file system to the specified string buffer.
### Arguments

- *string[]* **OUT_files** - String buffer to store the list of names for all known virtual files. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void GetVirtualFiles ( UGUID [] OUT_files )

Saves the list of [GUIDs](../../../api/library/filesystem/class.uguid_cs.md) for all known files registered in the file system to the specified string buffer.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)[]* **OUT_files** - String buffer to store the list of GUIDs for all known virtual files. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool IsVirtualFile ( string path )

Checks if the given file is known to the virtual file system.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).

### Return value

true if the file is known to the virtual file system; otherwise, false.
## bool IsVirtualFile ( UGUID guid )

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) is known to the virtual file system and has a virtual path registered.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file is known to the virtual file system; otherwise, false.
## bool AddVirtualFile ( string path , UGUID guid , bool must_exist = false )

Registers the regular file name as known virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) and appends it to the map used for fast searching. This method should be used when you need to add, for example, a new content to the project.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).
- *bool* **must_exist** - A flag indicating whether the specified file must [exist](#isFileExist_cstr_bool).

### Return value

true if the file name is appended successfully; otherwise, false.
## UGUID AddVirtualFile ( string path , bool must_exist = false )

Registers the regular file name as known virtual file and appends it to the map used for fast searching. This method should be used when you need to add, for example, a new content to the project.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *bool* **must_exist** - A flag indicating whether the specified file must [exist](#isFileExist_cstr_bool).

### Return value

File [GUID](../../../api/library/filesystem/class.uguid_cs.md) if it was registered successfully or an empty GUID, otherwise.
## bool RenameVirtualFile ( string path , string new_path )

Renames the specified known virtual file.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *string* **new_path** - New path for the file.

### Return value

true if the file is renamed successfully; otherwise, false.
## bool RenameVirtualFile ( string path , string new_path , UGUID new_guid )

Renames the specified known file and assigns it the specified new [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *string* **new_path** - New path for the file.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_guid** - New [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the file.

### Return value

true if the file is renamed successfully; otherwise, false.
## bool RenameVirtualFile ( UGUID guid , string new_path )

Renames the known virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).
- *string* **new_path** - New path for the file.

### Return value

true if the file is renamed successfully; otherwise, false.
## bool RenameVirtualFile ( UGUID guid , string new_path , UGUID new_guid )

Renames the known virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) and assigns it the specified new [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).
- *string* **new_path** - New path for the file.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_guid** - New [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the file.

### Return value

true if the file is renamed successfully; otherwise, false.
## bool RemoveVirtualFile ( string path )

Removes the virtual file with the given name.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is removed successfully; otherwise, false.
## bool RemoveVirtualFile ( UGUID guid )

Removes the virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the known virtual file to remove.

### Return value

true if the file is removed successfully; otherwise, false.
## bool ChangeVirtualFile ( string path )

Marks the virtual file with the given name as modified. The corresponding *CALLBACK_FILE_CHANGED* signal is emitted. This method is used to notify the Engine that a resource has been modified and needs to be updated.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is successfully marked as modified; otherwise, false.
## bool ChangeVirtualFile ( UGUID guid )

Marks the virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) as modified. The corresponding *CALLBACK_FILE_CHANGED* signal is emitted. This method is used to notify the Engine that a resource has been modified and needs to be updated.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the known virtual file to remove.

### Return value

true if the file is successfully marked as modified; otherwise, false.
## void RemoveNonExistingVirtualFiles ( )

Removes all non-existing virtual files from the File System. These files aren't physically exist on the disk, however, they are added to the virtual file system. For example, it can be a blob or a cache file.
## bool IsBlobFile ( string path )

Checks if the given file is [loaded](#addBlobFile_cstr_bool) to a blob.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is loaded to a blob successfully; otherwise, false.
## bool IsBlobFile ( UGUID guid )

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) is [loaded](#addBlobFile_UGUID_bool) to a blob.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file is loaded to a blob successfully; otherwise, false.
## bool AddBlobFile ( string path )

Adds a file into a blob. It can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is successfully added into a blob; otherwise, false.
## bool AddBlobFile ( UGUID guid )

Adds a file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) into a blob. It can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file is successfully added into a blob; otherwise, false.
## bool RemoveBlobFile ( string path )

Removes a file from the blob. Blobbing can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is removed successfully; otherwise, false.
## bool RemoveBlobFile ( UGUID guid )

Removes a file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) from the blob. Blobbing can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file is removed successfully; otherwise, false.
## bool IsCacheFile ( string path )

Checks if the given file is loaded into cache.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is added into cache; otherwise, false.
## bool IsCacheFile ( UGUID guid )

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) is loaded into cache.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file is added into cache; otherwise, false.
## bool AddCacheFile ( string path )

Caches a file in the memory. It can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is successfully added to cache; otherwise, false.
## bool AddCacheFile ( UGUID guid )

Caches a file in the memory with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md). It can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file is successfully added to cache; otherwise, false.
## bool RemoveCacheFile ( string path )

Removes a cached file from the memory. Caching can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file is successfully removed from cache; otherwise, false.
## bool RemoveCacheFile ( UGUID guid )

Removes a cached file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) from the memory. Caching can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file is successfully removed from cache; otherwise, false.
## bool IsDiskFile ( string path )

Returns a value indicating if the specified file path is a path to a file on disk (i.e. not a package, a blob, or a cache file).
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the specified file path is a path to a file on disk; otherwise, false.
## bool IsDiskFile ( UGUID guid )

Returns a value indicating if the file with the specified [GUID](../../../api/library/filesystem/class.uguid_cs.md) is a file on disk.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file with the specified GUID is a file on disk; otherwise, false.
## bool IsPackageFile ( string path )

Returns a value indicating if the specified file path is a path to a file inside a ZIP or UNG package.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).

### Return value

true if the specified file path is a path to a file inside a ZIP or UNG package; otherwise, false.
## bool IsPackageFile ( UGUID guid )

Returns a value indicating if the file with the specified [GUID](../../../api/library/filesystem/class.uguid_cs.md) is file inside a ZIP or UNG package.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file with the specified GUID is file inside a ZIP or UNG package; otherwise, false.
## string ResolvePartialVirtualPath ( string path )

Converts the given [partial path](../../../principles/filesystem/index_cs.md#partial) to a full virtual one.
> **Notice:** If the file isn't added to the virtual file system, the full virtual path won't be returned.

 For example, if you have the `data/project/image_1.tga` and want to use the partial virtual path `image_1.tga`, you should get the full virtual path first:
```csharp
// convert partial virtual to full virtual path
String full_virtual_path = FileSystem.ResolvePartialVirtualPath("image_1.tga"); // project/image_1.tga is returned
// use the converted path
Image MyImage = new Image(full_virtual_path);

```


### Arguments

- *string* **path** - Partial path to be resolved.

### Return value

Full virtual path.
## string GetVirtualPath ( string path )

Resolves a virtual path for the given file path. The following examples show particular cases of the method usage:
- If the given path is known for the virtual file system, the following can be returned: ```csharp String s1, s2, s3, s4; // absolute path to the folder s1 = FileSystem.GetVirtualPath("D:/Unigine/data");			// an empty string s2 = FileSystem.GetVirtualPath("D:/Unigine/data/");			// an empty string // path to assets in the folder s3 = FileSystem.GetVirtualPath("asset://D:/Unigine/data");	// an empty string s4 = FileSystem.GetVirtualPath("asset://D:/Unigine/data/");	// an empty string ``` In all cases, an empty string is returned: a virtual path is always returned relative to the data directory, and in the example, the data directory itself is specified. If you specify a known file inside it, the corresponding virtual path will be returned: ```csharp String s = FileSystem.GetVirtualPath("D:/Unigine/data/1.tga");		// "1.tga" ```
- If the given path is unknown for the virtual file system, the following can be returned: ```csharp // absolute path to the folder s1 = FileSystem.GetVirtualPath("C:/temp");			// "C:/temp" s2 = FileSystem.GetVirtualPath("C:/temp/");			// "C:/temp" // path to assets in the folder s3 = FileSystem.GetVirtualPath("asset://C:/temp");	// "C:/temp" s4 = FileSystem.GetVirtualPath("asset://C:/temp/");	// "C:/temp" ``` In all cases, the normalized path to the folder is returned, as the specified folder is unknown for the virtual file system, and, therefore, no virtual path can be returned. The same is for files, for example: ```cpp s = FileSystem.GetVirtualPath("C:/temp/1.tga");		// "C:/temp/1.tga" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index_cs.md#mount_points) file. Here `mount_1` is the `mount_1.umount` mount point. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the virtual path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```csharp // virtual path to the file specified as an absolute one s1 = FileSystem.GetVirtualPath("D:/Unigine/data/mounts/mount_1/1.tga");	// "mounts/mount_1/1.tga" // absolute path to the file s2 = FileSystem.GetVirtualPath("D:/extern_content/1.tga");				// "mounts/mount_1/1.tga" // full virtual path to the file s3 = FileSystem.GetVirtualPath("mounts/mount_1/1.tga");					// "mounts/mount_1/1.tga" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index_cs.md#mount_points) file stored in the nested mount points. Here `mount_1` and `mount_2` are the `mount_1.umount` and `mount_2.umount` mount points correspondingly. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the virtual path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```csharp // virtual path to the file specified as an absolute one s1 = FileSystem.GetVirtualPath("D:/UnigineGIT/data/mounts/mount_1/mount_2/1.tga");	// "mounts/mount_1/mount_2/1.tga" // absolute path to the file s2 = FileSystem.GetVirtualPath("D:/extern_content_2/1.tga");						// "mounts/mount_1/mount_2/1.tga" // full virtual path to the file s3 = FileSystem.GetVirtualPath("mounts/mount_1/mount_2/1.tga");						// "mounts/mount_1/mount_2/1.tga" ```


### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths), including a path to a folder. > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

Virtual path to the file relative to the `data` folder.
## string GetVirtualPath ( UGUID guid )

Resolves a virtual path for the given [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Virtual path to the file relative to the `data` folder.
## string GetAbsolutePath ( string path )

Resolves an absolute path for the given file path. The following examples show particular cases of the method usage:
- If the given path is known for the virtual file system, the following can be returned: ```csharp String s1, s2, s3, s4; // absolute path to the folder s1 = FileSystem.GetAbsolutePath("D:/Unigine/data");			// "D:/Unigine/data" s2 = FileSystem.GetAbsolutePath("D:/Unigine/data/");		// "D:/Unigine/data" // absolute path to assets in the folder s3 = FileSystem.GetAbsolutePath("asset://D:/Unigine/data");	// "D:/Unigine/data" s4 = FileSystem.GetAbsolutePath("asset://D:/Unigine/data/");// "D:/Unigine/data" ```
- If the given path is unknown for the virtual file system, the following can be returned: ```csharp // absolute path to the folder s1 = FileSystem.GetAbsolutePath("C:/temp");				// "C:/temp" s2 = FileSystem.GetAbsolutePath("C:/temp/");			// "C:/temp" // absolute path to assets in the folder s3 = FileSystem.GetAbsolutePath("asset://C:/temp");		// "C:/temp" s4 = FileSystem.GetAbsolutePath("asset://C:/temp/");	// "C:/temp" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index_cs.md#mount_points) file. Here `mount_1` is the `mount_1.umount` mount point. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the absolute path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```csharp // virtual path specified as an absolute one s1 = FileSystem.GetAbsolutePath("D:/Unigine/data/mounts/mount_1/1.tga");	// "D:/extern_content/1.tga" // absolute path s2 = FileSystem.GetAbsolutePath("D:/extern_content/1.tga");					// "D:/extern_content/1.tga" // virtual path s3 = FileSystem.GetAbsolutePath("mounts/mount_1/1.tga");					// "D:/extern_content/1.tga" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index_cs.md#mount_points) file stored in the nested mount points. Here `mount_1` and `mount_2` are the `mount_1.umount` and `mount_2.umount` mount points correspondingly. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the absolute path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```csharp // virtual path specified as an absolute one s1 = FileSystem.GetAbsolutePath("D:/Unigine/data/mounts/mount_1/mount_2/1.tga");	// "D:/extern_content_2/1.tga" // absolute path s2 = FileSystem.GetAbsolutePath("D:/extern_content_2/1.tga");						// "D:/extern_content_2/1.tga" // virtual path s3 = FileSystem.GetAbsolutePath("mounts/mount_1/mount_2/1.tga");					// "D:/extern_content_2/1.tga" ```
- If the given path is a network path: ```csharp s1 = FileSystem.GetAbsolutePath("//studio/work/shared_content/images.zip");			// "//studio/work/shared_content/images.zip" s2 = FileSystem.GetAbsolutePath("\\\\studio\\work\\shared_content\\images.zip");	// "//studio/work/shared_content/images.zip" ```


### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths), including a path to a folder. > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

Absolute path to the file.
## string GetAbsolutePath ( UGUID guid )


Resolves an absolute path for the given file [GUID](../../../api/library/filesystem/class.uguid_cs.md).


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Absolute path to the file.
## string GetPackageVirtualPath ( string path )

Resolves a virtual path for the given path to the package.
### Arguments

- *string* **path** - Path to a package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).

### Return value

Virtual path to the package.
## string GetPackageVirtualPath ( UGUID guid )

Resolves a virtual path for the given [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Package [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Virtual path to the package.
## string GetPackageAbsolutePath ( string path )

Resolves an absolute path for the given path to the package.
### Arguments

- *string* **path** - Path to a package. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).

### Return value

Absolute path to the package.
## string GetPackageAbsolutePath ( UGUID guid )


Resolves an absolute path for the given package [GUID](../../../api/library/filesystem/class.uguid_cs.md).


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Package [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Absolute path to the package.
## string GetExtension ( string path )

Returns the extension for the given file.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

File extension in lower case, if any; otherwise, an empty string.
## string GetExtension ( UGUID guid )

Returns the extension for a file with the specified [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the file for which extension is to be returned.

### Return value

File extension in lower case if any; otherwise, an empty string.
## bool IsFileExist ( string path )

Checks if the given file actually exists on the disk.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

true if the file exists; otherwise, false.
## bool IsFileExist ( UGUID guid )

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_cs.md) actually exists.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file exists; otherwise, false.
## bool IsGUIDPath ( string path )

Returns a value indicating if the given path has a valid GUID path format (e.g. "guid://e231e15beff2309b8f87c30b2c105cc4d2399973)".
### Arguments

- *string* **path** - Path to be checked.

### Return value

true if the given path has a valid GUID path format; otherwise, false.
## bool IsAssetPath ( string path )

Returns a value indicating if the given path has a valid [asset path format](../../../principles/filesystem/index_cs.md#access_path) (e.g. `asset://1.tga`).
### Arguments

- *string* **path** - Path to be checked.

### Return value

true if the given path has a valid asset path format; otherwise, false.
## long GetMTime ( string path )

Returns the time of the last modification of the given file.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

Time of the last file modification. If there is no such file, **-1** will be returned.
## long GetMTime ( UGUID guid )

Returns the time of the last modification of the file with the specified GUID.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Time of the last file modification. If there is no such file, **-1** will be returned.
## bool LoadGUIDs ( string path )

Loads file system [GUIDs](../../../api/library/filesystem/class.uguid_cs.md) from the specified file.
### Arguments

- *string* **path** - Path to the file, where file system GUIDs are stored.

### Return value

true if file system GUIDs are loaded successfully; otherwise, false.
## bool SaveGUIDs ( string path , bool binary = false )

Saves all file system [GUIDs](../../../api/library/filesystem/class.uguid_cs.md) to the specified file in the specified format (json or binary).
### Arguments

- *string* **path** - Path to the file, where file system GUIDs are to be stored.
- *bool* **binary** - Binary file format flag. When the flag is set to true, the file system will save GUIDs to a binary file; otherwise, to a JSON file.

### Return value

true if all file system GUIDs are saved successfully; otherwise, false.
## UGUID GenerateGUID ( )

Generates a new [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Return value

New filesystem GUID if is was generated successfully; otherwise, an empty GUID.
## bool SetGUID ( string path , UGUID guid )

Sets the specified [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the given file.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) to be set for the file.

### Return value

true if the [GUID](../../../api/library/filesystem/class.uguid_cs.md) is set successfully; otherwise, false.
## UGUID GetGUID ( string path )

Returns the [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the specified path if this path is registered in the File System.
> **Notice:** In case you pass a guid-string *(guid://)*, this method will give you back the guid you specified (**without checking whether it is registered in the File System or not**).

### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

File [GUID](../../../api/library/filesystem/class.uguid_cs.md) this path is registered in the File System; otherwise, an [empty GUID](../../../api/library/filesystem/class.uguid_cs.md#empty).
## long GetFileSize ( string path )

Returns the size of the specified file.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

File size in bytes.
## long GetFileSize ( UGUID guid )

Returns the size of the file with the specified [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md)

### Return value

File size in bytes.
## string GetModifier ( int num )

Returns the name of the given modifier.
### Arguments

- *int* **num** - ID number of the modifier.

### Return value

Modifier name.
## void AddModifier ( string name )

Registers a new modifier in the file system.
### Arguments

- *string* **name** - Modifier name.

## void RemoveModifier ( string name )

Unregisters a given modifier in the file system.
### Arguments

- *string* **name** - Modifier name.

## void ClearModifiers ( )

Unregister all modifiers in the file system.
## string GuidToPath ( UGUID guid )

Returns the path to the file with the specified GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md)

### Return value

File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).
## UGUID PathToGuid ( string path )

Returns the GUID of the file to which the path is specified.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (`asset://`). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

File [GUID](../../../api/library/filesystem/class.uguid_cs.md).
## bool IsExternalFile ( string path )

Checks whether the given file path refers to an external file (located outside the `data`).
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).

### Return value

true if the file is external; otherwise, false.
## bool IsExternalFile ( UGUID guid )

Checks whether the given file path GUID refers to an external file (located outside the `data`).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_cs.md)

### Return value

true if the file is external; otherwise, false.
## bool IsPackageLoaded ( string path )

Returns a value indicating if the specified package is loaded in the file system.
### Arguments

- *string* **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index_cs.md#paths).

### Return value

true if the package is loaded; otherwise, false.
## void GetPackagesVirtualPaths ( string[] OUT_packages_virtual_paths )

Returns virtual paths of all packages currently loaded in the file system.
### Arguments

- *string[]* **OUT_packages_virtual_paths** - An array to store virtual paths of all loaded packages. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
