# Managing Assets in Editor Plugins


This article contains information on working with assets in user plugins for UnigineEditor. Here you will find a brief description of the basic concepts and terms of the Asset System and learn how to manage resources (assets) in your custom tools based on UnigineEditor functionality.


### See Also


- [Extending Editor Functionality](../../editor2/extensions/index.md) article to learn more about writing custom plugins for UnigineEditor.
- [Assets Workflow](../../editor2/assets_workflow/index.md) article for more information on assets and the Asset System.
- [Assets and Runtime Files](../../editor2/assets_workflow/assets_runtimes.md) article to learn more about native, non-native assets, and runtimes.
- *[Editor API Reference](/api/editor/index.md)* for more information on all available classes.


## Basic Concepts


**Asset** is the "unit of work" - any item that you can use within a project. Some assets are called [**native**](../../editor2/assets_workflow/assets_runtimes.md) (i.e. can be used by the Engine "as is"), while others ([**non-native**](../../editor2/assets_workflow/assets_runtimes.md)) require to be converted. The result of conversion is called a [**runtime file**](../../editor2/assets_workflow/assets_runtimes.md) (or simply runtime).


For a single asset one or multiple runtimes can be generated, one of the runtimes is called **primary** (uniquely assoсiated with the asset, acting like an implied reference), while others are considered auxiliary (e.g., a `model.fbx`-asset produces multiple runtimes - `.node, .mesh, .texture, .mat` runtimes, but only the `model.node` is considered primary). When there is only one runtime produced it is considered as *primary*.


A **metafile** (`.meta`) is generated for each asset, contains important information about it: version, parameters, hash, runtime information, and a *[GUID](../../principles/filesystem/index_cpp.md#guids) (globally unique identifier)* identifying its location in the project. GUIDs are used to refer to all assets and runtimes in the project instead of paths, giving you a lot of flexibility in managing resources, as you can rename or move assets and be sure that all links between them are kept.


Normally all your project's resources (files, metafiles, runtime files) are stored in the project's `data` folder, but UNIGINE's virtual File System enables you to add links to external storage locations or packages via [mount points](../../principles/filesystem/index_cpp.md#mount_points). A mount point can be created via the *[Asset Browser](../../editor2/assets_workflow/index.md#asset_browser)* (**Create Mount Point**) or via [API](../../api/library/filesystem/class.filesystemmount_cpp.md). It is represented as a `.umount` file in the JSON format that stores a reference to an external directory or package as an absolute path or a path relative to the current directory. Also `.umount` file stores version of UNIGINE SDK in which the mount has been created, along with access information. All folders inside the mount point are treated by the File System as usual folders with assets, runtimes, and metafiles inside the `data` directory.


## Asset Manager


Assets in UnigineEditor are managed... yes, by *Asset Manager*. It is a class that extends the functionality of the UNIGINE's *[File System](../../api/library/filesystem/class.filesystem_cpp.md)*. It enables you to check availability of a resource with a specific GUID, get its path, subscribe for the signals to perform certain actions when an asset is added, moved, updated, or deleted. *AssetManager* allows you to track assets changes in real time. You can modify your assets at any time after importing, the Asset System will notice when you save new changes to the file and will re-import it as necessary. In some cases it might be necessary to temporary change this behavior and block auto-refreshing (e.g. if you are building a custom integration with a version control system). You can do it using *[blockAutoRefresh()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a19afe126fc7e30115b120d97c15c6eed)* and *[unblockAutoRefresh()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a2db89f6bee70d0c4aef6843f3f619631)* functions.


AssetManager enables you to work with:


- assets and their events
- directories and their events
- mount points
- file system watchers
- process events
- utils


The UnigineEditor API for AssetManager is presented *[here](/api/editor/class_unigine_editor_1_1_asset_manager.md)*.


## AssetsPlugin


Most likely your custom tools that you develop on the basis of UnigineEditor's functionality will somehow manage assets. For your convenience there is a sample plugin demonstrating implementation of basic asset management operations using the *[AssetManager](/api/editor/class_unigine_editor_1_1_asset_manager.md)* class. It is called **AssetsPlugin** and can be used as a template for your tool.


![Assets Plugin](assetspl.png)

*AssetsPlugin*


**Implemented Functions**


This plugin template implements the basic functionality of the *Asset Manager*. The plugin interacts with the *Asset Manager* system and adds a widget to *Window Manager*. AssetsPlugin allows you to:


- [Import the asset with waiting for the completion](#import_new_asset_synchronously)
- [Import the asset in the background](#import_new_asset_asynchronously)
- [Remove the asset in the background](#remove_asset_asynchronously)
- [Move the asset between directories in the background](#move_asset_asynchronously)
- [Rename the asset in the background](#rename_asset_asynchronously)
- [Copy the asset in the background](#copy_asset_asynchronously)
- [Print paths and GUIDs of all known assets](#print_all_known_assets)
- [Print full information about the asset](#print_asset_information)
- [Create a new directory](#create_directory)
- [Remove the directory with copied assets in the background](#remove_directory_with_copied_assets_asynchronously)
- [Move the directory with copied assets in the background](#move_directory_with_copied_assets_asynchronously)
- [Rename the directory with copied assets in the background](#rename_directory_with_copied_assets_asynchronously)
- [Copy the directory with copied assets in the background](#copy_directory_with_copied_assets_asynchronously)
- [Print all known directory paths](#print_all_known_directories)
- [Print all directory paths for a certain directory](#print_directories_from_test_directory)
- [Create a mount point](#create_mount_point)
- [Remove the mount point](#remove_mount_point)
- [Print the mount point information](#print_mount_point_information)
- [Reimport a selected asset (Landscape Map)](#reimport_selected_landscape_map)


### Import New Assets Synchronously


The type of operation is used when imported asset(s) is critically important for the current execution of the application. The importing process is executed in the main thread of the application. It represents a blocking system call and the function will not return until the operation is complete.


This operation is implemented in the plugin as ***import_new_asset_synchronously()*** function.


<details>
<summary>import_new_asset_synchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method importing a new asset and waiting for the process to complete (blocking the thread)
void AssetsPlugin::import_new_asset_synchronously()
{
	// calling an auxiliary function to create a new asset and import it, displaying information on imported asset on success, or an error notification
	String result = create_and_import_new_asset_synchronously();
	if (!result.empty())
	{
		success_notification(
			String::format("Asset has imported successfully: \"%s\"", result.get()));

		// set current Editor selection to the imported asset and print information about it
		select_asset(result);

		print_asset_information(result);
	}
	else
	{
		error_notification(String::format("Can't import asset: \"%s\"", result.get()));
	}
}

// Method creating and importing an asset synchronously (blocking the thread until the operation is completed)
String AssetsPlugin::create_and_import_new_asset_synchronously() const
{
	String result;

	// making a base path for a new asset to be imported
	const StringStack<> &base_asset_path = String::joinPaths(DIRECTORY_FOR_NEW_ASSETS,
		String::basename(TEXTURE_PATH));

	// asking  the Asset Manager to generate a unique
	String new_texture_path = AssetManager::generateUniquePath(base_asset_path);
	if (!create_asset(TEXTURE_PATH, new_texture_path))
	{
		return result;
	}
	// waiting for the texture asset to be imported by the AssetManager and returning the result (new texture path on success of an empty string on failure)
	if (AssetManager::importAssetSync(new_texture_path))
	{
		result = std::move(new_texture_path);
	}

	return result;
}


```

</details>


### Import New Assets Asynchronously


This type of operation is used when imported asset(s) is not critically important for the current execution of the application and can be performed in the background of the working process (e.g. adding a library of textures or models to be used later by the user). It represents a non-blocking call, the function returns immediately as soon as the operation is put to a queue.


> **Notice:** There is only a notification about the start of the process, no information about its status or any errors occurred. To catch completion of the operation subscribe for an event via *[AssetManager::getEventProcessEnd()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a3d49cf5c30df30f11bc1e203f664ebcc)* method.


This operation is implemented in the plugin as ***import_new_asset_asynchronously()*** function.


<details>
<summary>import_new_asset_asynchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method importing an asset in the background (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::import_new_asset_asynchronously()
{
	// making a base target path for the asset and generating a unique virtual path for it
	const StringStack<> &base_asset_path = String::joinPaths(DIRECTORY_FOR_NEW_ASSETS,
		String::basename(TEXTURE_PATH));
	const String &new_texture_path = AssetManager::generateUniquePath(base_asset_path);
	if (!create_asset(TEXTURE_PATH, new_texture_path))
	{
		return;
	}

	// launching the importing process in the background (asynchronously, without blocking the main thread) and displaying a notification, if it has started successfully
	// to catch completion of the operation set a handler via AssetManager::getEventProcessEnd.connect() method (see method "process_end()" here)
	if (AssetManager::importAssetAsync(new_texture_path))
	{
		success_notification(String::format("Asset import process has started successfully: \"%s\"",
			new_texture_path.get()));
	}
	else
	{
		error_notification(
			String::format("Can't start asset import process: \"%s\"", new_texture_path.get()));
	}
}


```

</details>


### Remove Assets Asynchronously


This type of operation is used when removing of asset(s) is not critically important for the current execution of the application and can be performed in the background of the working process (e.g. removing a pack of unused textures). It represents a non-blocking call, the function returns immediately as soon as the operation is put to a queue.


> **Notice:** Removing the asset from a project means completely removing it from all of the project's elements referring to it. There is only a notification about the start of the process, no information about its status or any errors occurred. To catch completion of the operation subscribe for an event via *[AssetManager::getEventProcessEnd()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a3d49cf5c30df30f11bc1e203f664ebcc)* method.


This operation is implemented in the plugin as ***remove_asset_asynchronously()*** function.


<details>
<summary>remove_asset_asynchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method removing an asset in the background (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::remove_asset_asynchronously()
{
	// checking whether there are any assets in the source directory to remove (if not, report and return)
	const Vector<String> &asset_paths = AssetManager::getAssetPathsForDirectory(
		DIRECTORY_FOR_NEW_ASSETS);
	if (asset_paths.empty())
	{
		error_notification(String::format("There are no assets to remove: \"%s\"\n",
			DIRECTORY_FOR_NEW_ASSETS));
		return;
	}

	// launching the asset removal process in the background (asynchronously, without blocking the main thread) and displaying a notification, if it has started successfully
	// to catch completion of the operation set a handler via AssetManager::getEventProcessEnd.connect() method (see method "process_end()" here)
	const String &asset_path_to_remove = asset_paths.last();
	if (AssetManager::removeAssetAsync(asset_path_to_remove))
	{
		success_notification(String::format("Asset removal process has started successfully: \"%s\"",
			asset_path_to_remove.get()));
	}
	else
	{
		error_notification(
			String::format("Can't start asset removal process: \"%s\"", asset_path_to_remove.get()));
	}
}


```

</details>


### Move Assets Asynchronously


This type of operation is used when moving asset(s) is not critically important for the current execution of the application and can be performed in the background of the working process. It represents a non-blocking call, the function returns immediately as soon as the operation is put to a queue. It is used to manage files. All virtual paths of assets are kept protected.


> **Notice:** There is only a notification about the start of the process, no information about its status or any errors occurred. To catch completion of the operation subscribe for an event via *[AssetManager::getEventProcessEnd()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a3d49cf5c30df30f11bc1e203f664ebcc)* method.


This operation is implemented in the plugin as ***move_asset_asynchronously()*** function.


<details>
<summary>move_asset_asynchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method moving an asset to a new location in the background (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::move_asset_asynchronously()
{
	// checking whether there are any assets in the source directory to move (if not, report and return)
	const Vector<String> &asset_paths = AssetManager::getAssetPathsForDirectory(
		DIRECTORY_FOR_NEW_ASSETS);
	if (asset_paths.empty())
	{
		error_notification(String::format("There are no assets to move: \"%s\"\n",
			DIRECTORY_FOR_NEW_ASSETS));
		return;
	}

	// trying to create a destination directory and displaying error notification in case of failure
	if (!AssetManager::createDirectory(DIRECTORY_FOR_MOVED_ASSETS))
	{
		error_notification(
			String::format("Can't create directory: \"%s\"", DIRECTORY_FOR_MOVED_ASSETS));
		return;
	}

	// making a new asset path and generating a unique virtual path for it
	const String &asset_path_to_move = asset_paths.last();
	const StringStack<> &base_asset_path = String::joinPaths(DIRECTORY_FOR_MOVED_ASSETS,
		asset_path_to_move.basename());
	const String &new_asset_path = AssetManager::generateUniquePath(base_asset_path);

	// launching the "move asset" process in the background (asynchronously, without blocking the main thread) and displaying a notification, if it has started successfully
	// to catch completion of the operation set a handler via AssetManager::getEventProcessEnd.connect() method (see method "process_end()" here)
	if (AssetManager::moveAssetAsync(asset_path_to_move, new_asset_path))
	{
		success_notification(
			String::format("Asset moving process has started successfully: from \"%s\" to \"%s\"",
				asset_path_to_move.get(), new_asset_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start asset moving process: from \"%s\" to \"%s\"",
			asset_path_to_move.get(), new_asset_path.get()));
	}
}


```

</details>


### Rename Assets Asynchronously


This type of operation is used when renaming asset(s) is not critically important for the current execution of the application and can be performed in the background of the working process (e.g. adding a prefix for a set of textures in the library). It represents a non-blocking call, the function returns immediately as soon as the operation is put to a queue. It is used to manage files. All virtual paths of assets are kept protected.


> **Notice:** There is only a notification about the start of the process, no information about its status or any errors occurred. To catch completion of the operation subscribe for an event via *[AssetManager::getEventProcessEnd()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a3d49cf5c30df30f11bc1e203f664ebcc)* method.


This operation is implemented in the plugin as ***rename_asset_asynchronously()*** function.


<details>
<summary>rename_asset_asynchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method renaming an asset asynchronously (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::rename_asset_asynchronously()
{
	// getting paths for all assets in the directory and checking whether it is empty (if so, report and return)
	const Vector<String> &asset_paths = AssetManager::getAssetPathsForDirectory(
		DIRECTORY_FOR_NEW_ASSETS);
	if (asset_paths.empty())
	{
		error_notification(String::format("There are no assets to rename: \"%s\"\n",
			DIRECTORY_FOR_NEW_ASSETS));
		return;
	}

	// as an example, we rename the last file
	const String &asset_path_to_rename = asset_paths.last();

	const StringStack<> &new_asset_dir_path = String::dirname(asset_path_to_rename);
	const char *NEW_ASSET_FILE_NAME = "Renamed Asset";

	// making a new asset path and generating a unique virtual path for it
	StringStack<> new_asset_path = String::joinPaths(new_asset_dir_path, NEW_ASSET_FILE_NAME);
	new_asset_path += '.' + String::extension(asset_path_to_rename);

	new_asset_path = AssetManager::generateUniquePath(new_asset_path);

	// getting a base name for it to set while renaming
	const StringStack<> &new_asset_name = new_asset_path.basename();

	// putting a new "asset rename" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::renameAssetAsync(asset_path_to_rename, new_asset_name))
	{
		success_notification(
			String::format("Asset renaming process has started successfully: from \"%s\" to \"%s\"",
				asset_path_to_rename.get(), new_asset_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start asset renaming process: from \"%s\" to \"%s\"",
			asset_path_to_rename.get(), new_asset_path.get()));
	}
}


```

</details>


### Copy Assets Asynchronously


This type of operation is used when copying asset(s) is not critically important for the current execution of the application and can be performed in the background of the working process. It represents a non-blocking call, the function returns immediately as soon as the operation is put to a queue. Can be used, for example, if the same asset with different dimensional parameters is required or to perform some tests with a given world file.


> **Notice:** There is only a notification about the start of the process, no information about its status or any errors occurred. To catch completion of the operation subscribe for an event via *[AssetManager::getEventProcessEnd()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a3d49cf5c30df30f11bc1e203f664ebcc)* method.


This operation is implemented in the plugin as ***copy_asset_asynchronously()*** function.


<details>
<summary>copy_asset_asynchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method copying an asset asynchronously (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::copy_asset_asynchronously()
{
	// getting paths for all assets in the directory and checking whether it is empty (if so, report and return)
	const Vector<String> &asset_paths = AssetManager::getAssetPathsForDirectory(
		DIRECTORY_FOR_NEW_ASSETS);
	if (asset_paths.empty())
	{
		error_notification(String::format("There are no assets to copy: \"%s\"\n",
			DIRECTORY_FOR_NEW_ASSETS));
		return;
	}

	// as an example, we copy the last file
	const String &asset_path_to_copy = asset_paths.last();

	// creating a new directory
	if (!AssetManager::createDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Can't create directory: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// making a base path and generating a unique virtual path for a new copy of the asset
	const StringStack<> &base_asset_path = String::joinPaths(DIRECTORY_FOR_COPIED_ASSETS,
		asset_path_to_copy.basename());
	const String &new_asset_path = AssetManager::generateUniquePath(base_asset_path);

	// putting a new "asset copy" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::copyAssetAsync(asset_path_to_copy, new_asset_path))
	{
		success_notification(
			String::format("Asset copying process has started successfully: from \"%s\" to \"%s\"",
				asset_path_to_copy.get(), new_asset_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start asset copying process: from \"%s\" to \"%s\"",
			asset_path_to_copy.get(), new_asset_path.get()));
	}
}


```

</details>


### Print Paths and GUIDs of All Known Assets


Printing out the list of paths and GUIDs for all assets in the root project directory (including all subdirectories). This can be used to iterate over the assets in your project providing information on assets location.


This operation is implemented in the plugin as ***print_all_known_assets()*** function.


<details>
<summary>print_all_known_assets() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method printing out the list of paths and GUIDs for all assets in the root project directory (including all subdirectories)
void AssetsPlugin::print_all_known_assets()
{
	Log::message("[Assets Plugin] All asset paths:\n");
	for (const String &path : AssetManager::getAssetPaths())
	{
		Log::message("\t%s\n", path.get());
	}
	Log::message("\n[Assets Plugin] All asset GUIDs:\n");
	for (const UGUID &guid : AssetManager::getAssetGUIDs())
	{
		Log::message("\t%s\n", FileSystem::guidToPath(guid).get());
	}
	Log::message("\n");
}


```

</details>


### Print Full Information About The Asset


Printing out general information for the specified asset path including virtual path, file GUID, access mode, and information about runtimes generated for this asset (GUID, type, alias, and file GUID). You may need this information, for example, when building a dependency graph for your assets.


This operation is implemented in the plugin as ***print_asset_information()*** function.


<details>
<summary>print_asset_information() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method printing out general information for the specified asset path
void AssetsPlugin::print_asset_information(const char *asset_path)
{
	const UGUID &asset_guid = AssetManager::getAssetGUIDFromPath(asset_path);
	// It's only to demonstrate the usage of some API functions:
	Log::message("[Assets Plugin] Asset information:\n");
	Log::message("\tVirtual path: %s\n", AssetManager::getAssetPathFromGUID(asset_guid).get());
	Log::message("\tFile GUID: %s\n", FileSystem::guidToPath(asset_guid).get());
	Log::message("\tAccess: %s\n",
		AssetManager::isAssetWritable(asset_path) ? "read & write" : "read-only");
	auto get_import_parameters_as_string = [asset_path] {
		const CollectionPtr &parameters = AssetManager::getAssetImportParameters(asset_path);
		return convert_vector_to_flat_string(parameters->getNames());
	};
	Log::message("\tImport parameter names: %s\n", get_import_parameters_as_string().get());

	// getting the list of GUIDs for all runtimes generated for the asset path and displaying general information about them (if any)
	const Vector<UGUID> &runtime_guids = AssetManager::getRuntimeGUIDs(asset_path);
	if (runtime_guids.empty())
	{
		Log::message("\tNo runtimes\n");
	}
	else
	{
		Log::message("\tRuntimes:\n");
		for (int i = 0, count = runtime_guids.size(); i < count; ++i)
		{
			const UGUID &rt_guid = runtime_guids[i];
			Log::message("\t\tRuntime #%d is %s: Alias (%s) File GUID (%s)\n", i,
				AssetManager::isRuntimePrimary(rt_guid) ? "primary" : "non-primary",
				AssetManager::getRuntimeAlias(rt_guid).get(), FileSystem::guidToPath(rt_guid).get());
		}
	}
}


```

</details>


### Create a New Directory


New directory creation, used to manage files within the project.


This operation is implemented in the plugin as ***create_directory()*** function.


<details>
<summary>create_directory() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method creating a new directory
void AssetsPlugin::create_directory()
{
	// making a base path for a new directory and generating a unique virtual path for it
	const StringStack<> &base_path = String::joinPaths(DIRECTORY_FOR_NEW_DIRECTORIES,
		"New Directory");
	const String &new_path = AssetManager::generateUniquePath(base_path);

	// creating a new directory for the specified path and displaying the corresponding notification
	if (AssetManager::createDirectory(new_path))
	{
		success_notification(
			String::format("Directory has been created successfully: \"%s\"", new_path.get()));
		assert(AssetManager::isDirectoryWritable(new_path));
	}
	else
	{
		error_notification(String::format("Can't create directory: \"%s\"", new_path.get()));
	}
}


```

</details>


### Remove the Directory with Copied Assets Asynchronously


This type of operation is used when removing of the directory is not critically important for the current execution of the application and can be performed in the background of the working process (e.g. to remove a group of assets from the project). It represents a non-blocking call, the function returns immediately as soon as the operation is put to a queue.


> **Notice:** Removing a directory containing assets from a project means completely removing all these assets from all other project's elements referring to them. There is only a notification about the start of the process, no information about its status or any errors occurred. To catch completion of the operation subscribe for an event via *[AssetManager::getEventProcessEnd()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a3d49cf5c30df30f11bc1e203f664ebcc)* method.


This operation is implemented in the plugin as ***remove_directory_with_copied_assets_asynchronously()*** function.


<details>
<summary>remove_directory_with_copied_assets_asynchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method removing a directory with assets (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::remove_directory_with_copied_assets_asynchronously()
{
	// checking if the specified directory exists (if not, report and return)
	if (!AssetManager::isDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Directory doesn't exist: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// putting a new "remove directory" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::removeDirectoryAsync(DIRECTORY_FOR_COPIED_ASSETS))
	{
		success_notification(String::format("Directory removal process has started successfully: \"%s\"",
			DIRECTORY_FOR_COPIED_ASSETS));
	}
	else
	{
		error_notification(
			String::format("Can't start directory removal process: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
	}
}


```

</details>


### Move the Directory with Copied Assets Asynchronously


This type of operation is used when moving of the directory is not critically important for the current execution of the application and can be performed in the background of the working process (e.g. to move a group of assets to another location). It represents a non-blocking call, the function returns immediately as soon as the operation is put to a queue.


> **Notice:** There is only a notification about the start of the process, no information about its status or any errors occurred. To catch completion of the operation subscribe for an event via *[AssetManager::getEventProcessEnd()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a3d49cf5c30df30f11bc1e203f664ebcc)* method.


This operation is implemented in the plugin as ***move_directory_with_copied_assets_asynchronously()*** function.


<details>
<summary>move_directory_with_copied_assets_asynchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method moving a directory with assets to a new location (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::move_directory_with_copied_assets_asynchronously()
{
	// checking if the source directory exists (if not, report and return)
	if (!AssetManager::isDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Directory doesn't exist: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// making a base destination path and generating a unique virtual path for it
	const StringStack<> &base_path = String::joinPaths(DIRECTORY_FOR_NEW_DIRECTORIES,
		"New Directory");
	const String &new_path = AssetManager::generateUniquePath(base_path);

	// putting a new "move directory" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::moveDirectoryAsync(DIRECTORY_FOR_COPIED_ASSETS, new_path))
	{
		success_notification(
			String::format("Directory moving process has started successfully: from \"%s\" to \"%s\"",
				DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start directory moving process:  from \"%s\" to \"%s\"",
			DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
}


```

</details>


### Rename the Directory with Copied Assets Asynchronously


This type of operation is used when renaming of the directory is not critically important for the current execution of the application and can be performed in the background of the working process (e.g. to move a group of assets to another location). It represents a non-blocking call, the function returns immediately as soon as the operation is put to a queue. It is used to manage files. All virtual paths of assets are kept protected.


> **Notice:** There is only a notification about the start of the process, no information about its status or any errors occurred. To catch completion of the operation subscribe for an event via *[AssetManager::getEventProcessEnd()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a3d49cf5c30df30f11bc1e203f664ebcc)* method.


This operation is implemented in the plugin as ***rename_directory_with_copied_assets_asynchronously()*** function.


<details>
<summary>rename_directory_with_copied_assets_asynchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method renaming a directory with assets (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::rename_directory_with_copied_assets_asynchronously()
{
	// checking if the specified directory exists (if not, report and return)
	if (!AssetManager::isDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Directory doesn't exist: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// generating a unique virtual path for the destination directory and getting its base name to change it
	const String &new_path = AssetManager::generateUniquePath(DIRECTORY_FOR_COPIED_ASSETS);
	const StringStack<> &new_name = new_path.basename();

	// putting a new "rename directory" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::renameDirectoryAsync(DIRECTORY_FOR_COPIED_ASSETS, new_name))
	{
		success_notification(
			String::format("Directory renaming process has started successfully: from \"%s\" to \"%s\"",
				DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start directory renaming process: from \"%s\" to \"%s\"",
			DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
}


```

</details>


### Copy the Directory with Copied Assets Asynchronously


This type of operation is used when copying of the directory is not critically important for the current execution of the application and can be performed in the background of the working process (e.g. to move a group of assets to another location). It represents a non-blocking call, the function returns immediately as soon as the operation is put to a queue. It is used to manage files. All virtual paths of assets are kept protected.


> **Notice:** There is only a notification about the start of the process, no information about its status or any errors occurred. To catch completion of the operation subscribe for an event via *[AssetManager::getEventProcessEnd()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a3d49cf5c30df30f11bc1e203f664ebcc)* method.


This operation is implemented in the plugin as ***copy_directory_with_copied_assets_asynchronously()*** function.


<details>
<summary>copy_directory_with_copied_assets_asynchronously() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method copying a directory with assets to the specified path (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::copy_directory_with_copied_assets_asynchronously()
{
	// checking if the specified directory exists (if not, report and return)
	if (!AssetManager::isDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Directory doesn't exist: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// making the destination base path, to which the directory is to be copied, and generating a new unique virtual path for it
	const StringStack<> &base_path = String::joinPaths(DIRECTORY_FOR_NEW_DIRECTORIES,
		"New Directory");
	const String &new_path = AssetManager::generateUniquePath(base_path);

	// launching the copying process in the background (asynchronously, without blocking the main thread) and displaying a notification, if it has started successfully
	// to catch completion of the operation set a handler via AssetManager::getEventProcessEnd.connect() method (see method "process_end()" here)
	if (AssetManager::copyDirectoryAsync(DIRECTORY_FOR_COPIED_ASSETS, new_path))
	{
		success_notification(
			String::format("Directory copying process has started successfully: from \"%s\" to \"%s\"",
				DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start directory copying process: from \"%s\" to \"%s\"",
			DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
}


```

</details>


### Print All Known Directory Paths


Lists all directory paths known to the *Asset Manager*, this can be used to iterate over all directories in the project. The operation is implemented in the plugin as ***print_all_known_directories()*** function.


<details>
<summary>print_all_known_directories() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method listing all directories known to the AssetManager
void AssetsPlugin::print_all_known_directories()
{
	Log::message("\n[Assets Plugin] All directory paths:\n");
	for (const String &path : AssetManager::getDirectoryPathsAll())
	{
		Log::message("\t%s\n", path.get());
	}
	Log::message("\n");
}


```

</details>


### Print All Directory Paths for Specified Directory


Lists all subdirectories for the specified directory. Can be used to iterate over subdirectories of the specified directory (e.g. when processing a well-structured pack of assets sorted by folders according to their types, usage logic, or otherwise). This operation is implemented in the plugin as ***print_directories_from_test_directory()*** function.


<details>
<summary>print_directories_from_test_directory() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method listing all subdirectories of the specified path, that are known to the AssetManager
void AssetsPlugin::print_directories_from_test_directory()
{
	Log::message("\n[Assets Plugin] Directory paths from \"%s\":\n", DIRECTORY_FOR_NEW_DIRECTORIES);
	for (const String &path : AssetManager::getDirectoryPaths(DIRECTORY_FOR_NEW_DIRECTORIES))
	{
		Log::message("\t%s\n", path.get());
	}
	Log::message("\n");
}


```

</details>


### Create a Mount Point


This operation can be used to add a link to an external folder, shared storage or package (e.g. a library of 3D models, VFX, etc.) to the project.


The parameters of the mount point are managed via an instance of the *[MountPointParameters](/api/editor/class_unigine_editor_1_1_mount_point_parameters.md)* class - first, we should create an instance and specify necessary settings (path, access mode, etc.) and then tell the *AssetManager* to create a mount point via the *[createMountPoint()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a7a6e8aeb8697ea7e34cc173714bca92f)* method. A corresponding `.umount` file is created in the project's `data` folder. This is a file in the JSON format that represents the root mount point.


This operation is implemented in the plugin as ***create_mount_point()*** function.


<details>
<summary>create_mount_point() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method creating a new mount point
void AssetsPlugin::create_mount_point()
{
	// checking if a path for a mount point to be created already exists and displaying the corresponding notifications
	if (AssetManager::isExist(DIRECTORY_FOR_MOUNT_POINT))
	{
		if (AssetManager::isAsset(DIRECTORY_FOR_MOUNT_POINT))
		{
			error_notification(
				String::format("Target path already contains a known asset: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		}
		else if (AssetManager::isMountPoint(DIRECTORY_FOR_MOUNT_POINT))
		{
			assert(AssetManager::isDirectory(DIRECTORY_FOR_MOUNT_POINT));	// Mount point is a directory
			success_notification(
				String::format("Mount point for the target path already exists: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		}
		else if (AssetManager::isDirectory(DIRECTORY_FOR_MOUNT_POINT))
		{
			error_notification(
				String::format("Target path already contains a known directory: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		}
		else
		{
			// May be some reserved file or directory already exists there
			error_notification(
				String::format("Target path already exists and may contain a reserved file or some directory: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		}
		return;
	}

	// making an absolute path to the mount
	StringStack<> abs_dir_path = String::normalizeDirPath(Engine::get()->getDataPath());
	abs_dir_path = abs_dir_path.trimLast("/");
	abs_dir_path = abs_dir_path.dirname();
	abs_dir_path = String::joinPaths(abs_dir_path, MOUNT_POINT_DIRECTORY_NAME);

	// getting an existing directory for the absolute path or creating it
	if (!Dir::mkdir(abs_dir_path))
	{
		error_notification(String::format("Can't create directory \"%s\"", abs_dir_path.get()));
		return;
	}

	// creating an instance of the MountPointParameters class to specify necessary settings for a new mount point to be created (path and access mode)
	MountPointParametersPtr mount_params = MountPointParameters::create();
	mount_params->setAbsolutePath(abs_dir_path);
	mount_params->setAccess(MountPointParameters::ACCESS_READWRITE);

	// trying to create a new mount point for the specified path and parameters, displaying a notification depending on the result
	if (AssetManager::createMountPoint(DIRECTORY_FOR_MOUNT_POINT, mount_params))
	{
		success_notification(String::format("Mount point has been created successfully: \"%s\"",
			DIRECTORY_FOR_MOUNT_POINT));
		assert(AssetManager::isMountPoint(DIRECTORY_FOR_MOUNT_POINT));
	}
	else
	{
		error_notification(
			String::format("Can't create mount point: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
	}
}


```

</details>


### Remove a Mount Point


This operation can be used to disconnect from a shared storage.


> **Notice:** Removing a mount point containing assets used in the project means completely removing all these assets from all other project's elements referring to them.


This operation is implemented in the plugin as ***remove_mount_point()*** function.


<details>
<summary>remove_mount_point() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method removing a mount point
void AssetsPlugin::remove_mount_point()
{
	// checking if the specified mount point exists
	if (!AssetManager::isMountPoint(DIRECTORY_FOR_MOUNT_POINT))
	{
		error_notification(
			String::format("Mount point doesn't exist \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		return;
	}

	// trying to remove the specified mount point via the AssetManager, displaying a notification depending on the result
	if (AssetManager::removeMountPoint(DIRECTORY_FOR_MOUNT_POINT))
	{
		success_notification(String::format("Mount point has been removed successfully: \"%s\"",
			DIRECTORY_FOR_MOUNT_POINT));
	}
	else
	{
		error_notification(
			String::format("Can't remove mount point: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
	}
}


```

</details>


### Print Mount Point Information


This operation can be used to obtain information about a mount point (virtual path, absolute path, access, filters). The parameters of the mount point are managed via an instance of the *[MountPointParameters](/api/editor/class_unigine_editor_1_1_mount_point_parameters.md)* class - first, we call the *[getMountPointParameters()](/api/editor/class_unigine_editor_1_1_asset_manager.md#a9017b4027f778345fd9c43b747957316)* method to fill this instance with necessary data and then use the instance to print information. This is a sample code demonstrating the use of public API.


This operation is implemented in the plugin as ***print_mount_point_information()*** function.


<details>
<summary>print_mount_point_information() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method printing complete information about the mount point (virtual path, access, and filters)
void AssetsPlugin::print_mount_point_information()
{
	// checking if the specified mount point exists
	if (!AssetManager::isMountPoint(DIRECTORY_FOR_MOUNT_POINT))
	{
		Log::message("[Assets Plugin] Mount point doesn't exist: \"%s\"\n",
			DIRECTORY_FOR_MOUNT_POINT);
		return;
	}

	Log::message("[Assets Plugin] Mount point information\n\n");
	Log::message("\tVirtual path: \"%s\"\n", DIRECTORY_FOR_MOUNT_POINT);

	// retrieving parameters of the specified mount point to a MountPointParameters class instance and print information using its data
	const MountPointParametersPtr mount_params = AssetManager::getMountPointParameters(
		DIRECTORY_FOR_MOUNT_POINT);

	Log::message("\tAbsolute path: \"%s\"\n", mount_params->getAbsolutePath());
	Log::message("\tAccess: \"%s\"\n",
		(mount_params->getAccess() == MountPointParameters::ACCESS_READONLY) ? "read-only"
																			 : "read & write");

	// retrieving exclusive filters of the specified mount point to a vector and printing its contents or a corresponding message in case filters are not set
	const Vector<String> &exclusive_filters = mount_params->getExclusiveFilters();
	if (exclusive_filters.empty())
	{
		Log::message("\tNo exclusive filters\n");
	}
	else
	{
		Log::message("\tExclusive filters: %s\n", convert_vector_to_flat_string(exclusive_filters));
	}

	// retrieving ignore filters of the specified mount point to a vector and printing its contents or a corresponding message in case filters are not set
	const Vector<String> &ignore_filters = mount_params->getIgnoreFilters();
	if (ignore_filters.empty())
	{
		Log::message("\tNo ignore filters\n");
	}
	else
	{
		Log::message("\tIgnore filters: %s\n", convert_vector_to_flat_string(ignore_filters));
	}

	Log::message("\n");
}


```

</details>


### Reimport Selected Landscape Map


This opreation reimports the selected *Landscape Map* asset after changing its import parameters. Can be used to reimport an asset existing in the project with a new set of import parameters.


This operation is implemented in the plugin as ***reimport_selected_landscape_map()*** function. This function uses the auxiliary function ***find_selected_lmap_file()*** which iterates over the current selection and finds the path to the `.lmap` asset to be reimported.


<details>
<summary>reimport_selected_landscape_map() | Close</summary>

`AssetsPlugin.cpp`


```cpp
// Method reimporting the selected Landscape Map (.lmap) asset
void AssetsPlugin::reimport_selected_landscape_map()
{
	// trying to get an .lmap-file in the current selection
	const String &lmap_path = find_selected_lmap_file();
	if (lmap_path.empty())
	{
		return;
	}

	// getting current import parameters for the .lmap asset to an instance of the Collection class
	CollectionPtr source_import_parameters = AssetManager::getAssetImportParameters(lmap_path);
	LandscapeMapImportParametersPtr lmap_import_parameters = LandscapeMapImportParameters::create();
	lmap_import_parameters->load(source_import_parameters);

	// switching the data filling mode import parameter for the asset
	using DataMode = LandscapeMapImportParameters::DATA_FILLING_MODE;
	DataMode mode = lmap_import_parameters->getDataFillingMode();
	switch (mode)
	{
	case DataMode::DATA_FILLING_MODE_FROM_TILESET: mode = DataMode::DATA_FILLING_MODE_MANUAL; break;
	case DataMode::DATA_FILLING_MODE_MANUAL: mode = DataMode::DATA_FILLING_MODE_FROM_TILESET; break;
	}
	lmap_import_parameters->setDataFillingMode(mode);

	// saving new import parameters and using them to reimport asset asynchronously with corresponding notification on starting the process
	CollectionPtr dest_import_parameters = lmap_import_parameters->save();
	if (AssetManager::reimportAssetAsync(lmap_path, dest_import_parameters))
	{
		success_notification(String::format(
			"Asset reimport process has started successfully: \"%s\"", lmap_path.get()));
	}
	else
	{
		error_notification(
			String::format("Can't start asset reimport process: \"%s\"", lmap_path.get()));
	}
}

// Auxiliary method iterating over the current selection and finds the path to the first .lmap asset in the current Editor selection.
String AssetsPlugin::find_selected_lmap_file() const
{
	String lmap_path;

	// getting guids of runtimes for all currently selected assets, returning an empty string if nothing is selected
	const SelectorGUIDs *selector = Selection::getSelectorRuntimes();
	if (!selector || selector->empty())
	{
		return lmap_path;
	}

	// getting guids of all currently selected assets
	const Vector<UGUID> &selected_guids = selector->guids();
	for (const UGUID &guid : selected_guids)
	{
		// obtaining asset path by its GUID and checking if the path corresponds to a registered asset
		String virtual_path = AssetManager::getAssetPathFromGUID(guid);
		if (!AssetManager::isAsset(virtual_path))
		{
			Log::message("[Assets Plugin] Invalid asset path: %s\n", virtual_path.get());
			continue;
		}

		// getting an extension for the asset file and return the virtual path if it is an .lmap asset
		const StringStack<> &extension = virtual_path.extension().getLower();
		if (!String::equal(extension, "lmap"))
		{
			continue;
		}

		lmap_path = std::move(virtual_path);
		break;
	}

	return lmap_path;
}


```

</details>


## Complete Source Code


The complete source code of the ***Assets*** plugin with comments is given below.


<details>
<summary>AssetsPlugin.h | Close</summary>

`AssetsPlugin.h`


```cpp
#pragma once

#include <editor/UniginePlugin.h>
#include <editor/UnigineEngineGuiWindow.h>

#include <UnigineVector.h>
#include <UnigineWidgets.h>

class QAction;

class AssetsPlugin final
	: public QObject
	, public ::UnigineEditor::Plugin
{
	Q_OBJECT
	Q_DISABLE_COPY(AssetsPlugin)
	Q_PLUGIN_METADATA(IID UNIGINE_EDITOR_PLUGIN_IID FILE "AssetsPlugin.json")
	Q_INTERFACES(UnigineEditor::Plugin)

public:
	AssetsPlugin() = default;

	bool init() override;
	void shutdown() override;

private:
	void activate();
	void deactivate();
	bool is_activated() const { return static_cast<bool>(window_); }

	void create_window();
	void destroy_window();
	// Auxiliary method creating the GUI of the Assets Plugin
	void build_gui();
	// Auxiliary method adding button elements to the GUI of the Assets Plugin
	void add_buttons(const Unigine::WidgetWindowPtr &main_window);
	// Auxiliary method setting up window title and update policy
	void setup_window();

	// Auxiliary method setting up handlers for various events (assets, directories, processing)
	void make_connections_to_asset_manager();
	// Auxiliary methods removing added AssetManager event subscriptions
	void destroy_connections_from_asset_manager();

	// Auxiliary method subscribing for tracking selection changes in the UnigineEditor
	void make_connection_to_selection();
	// Auxiliary methods removing added selection event subscriptions
	void destroy_connection_from_selection();

	// Method importing a new asset and waiting for the process to complete (blocking the thread)
	void import_new_asset_synchronously();
	// Method importing an asset in the background (non-blocking, returns immediately without waiting for operation completion)
	void import_new_asset_asynchronously();
	// Method removing an asset in the background (non-blocking, returns immediately without waiting for operation completion)
	void remove_asset_asynchronously();
	// Method moving an asset in the background (non-blocking, returns immediately without waiting for operation completion)
	void move_asset_asynchronously();
	// Method renaming an asset in the background (non-blocking, returns immediately without waiting for operation completion)
	void rename_asset_asynchronously();

	// Method copying an asset in the background (non-blocking, returns immediately without waiting for operation completion)
	void copy_asset_asynchronously();
	// Method printing out the list of paths and GUIDs for all assets in the root project directory (including all subdirectories)
	void print_all_known_assets();
	// Method printing out general information for the specified asset path
	void print_asset_information(const char *asset_path);

	// Method creating a new directory
	void create_directory();
	// Method removing a directory with assets (non-blocking, returns immediately without waiting for operation completion)
	void remove_directory_with_copied_assets_asynchronously();
	// Method moving a directory with assets to a new location (non-blocking, returns immediately without waiting for operation completion)
	void move_directory_with_copied_assets_asynchronously();
	// Method renaming a directory with assets (non-blocking, returns immediately without waiting for operation completion)
	void rename_directory_with_copied_assets_asynchronously();
	// Method copying a directory with assets to the specified path (non-blocking, returns immediately without waiting for operation completion)
	void copy_directory_with_copied_assets_asynchronously();
	// Method listing all directories known to the AssetManager
	void print_all_known_directories();
	// Method listing all subdirectories for the specified path, that are known to the AssetManager
	void print_directories_from_test_directory();

	// Method creating a new mount point
	void create_mount_point();
	// Method removing a mount point
	void remove_mount_point();
	// Method printing complete information about the mount point (virtual path, access, and filters)
	void print_mount_point_information();

	// Method reimporting the selected Landscape Map (.lmap) asset
	void reimport_selected_landscape_map();

	// Auxiliary method setting the current Editor selection to an asset having the specified path
	void select_asset(const char *asset_path);

	// Auxiliary method displaying a success message
	void success_notification(const char *message) const;
	// Auxiliary method displaying an error message
	void error_notification(const char *message) const;
	// Auxiliary method displaying a generic notification message using the specified color
	void notification(const char *message, const Unigine::Math::vec4 &color) const;

	// Method creating and importing an asset synchronously (blocking the thread until the operation is completed)
	Unigine::String create_and_import_new_asset_synchronously() const;
	// Auxiliary method creating an asset with the specified destination path for the specified source path
	bool create_asset(const char *source_path, const char *dest_path) const;
	// Auxiliary method iterating over the current selection and finds the path to the first .lmap asset in the current Editor selection.
	Unigine::String find_selected_lmap_file() const;

	// Event handlers from AssetManager:

	// Function to be executed on adding a new asset
	void asset_added(const char *path);
	// Function to be executed before removing an asset
	void asset_before_remove(const char *path);
	// Function to be executed after removing an asset
	void asset_removed(const char *path);
	// Function to be executed on changing an asset
	void asset_changed(const char *path);
	// Function to be executed on moving an asset to a new location
	void asset_moved(const char *path_from, const char *path_to);
	// Function to be executed on adding a new directory
	void directory_added(const char *path);
	// Function to be executed before removing a directory
	void directory_before_remove(const char *path);
	// Function to be executed after removing a directory
	void directory_removed(const char *path);
	// Function to be executed on moving a directory to a new location
	void directory_moved(const char *path_from, const char *path_to);
	// Function to be executed on beginning of asynchronous asset processing by the Asset Manager (e.g., validation, import, reimport, removal, copying, conversion, migration etc.)
	void process_begin();
	// Function to be executed on completion of asynchronous asset processing by the Asset Manager (e.g., validation, import, reimport, removal, copying, conversion, migration etc.)
	void process_end();

	// Event handler from Selection:

	// Function to be executed on changing selection in the Editor
	void selection_changed();

private:
	QAction *action_{};
	::UnigineEditor::EngineGuiWindow *window_{};
	Unigine::GuiPtr gui_;
	Unigine::WidgetLabelPtr label_notification_;
	Unigine::WidgetButtonPtr button_lmap_reimporting_;

	Unigine::EventConnections connections_;
	QMetaObject::Connection connection_selection_;
};


```

</details>


<details>
<summary>AssetsPlugin.cpp | Close</summary>

`AssetsPlugin.cpp`


```cpp
#include "AssetsPlugin.h"

#include <UnigineDir.h>
#include <UnigineEngine.h>
#include <UnigineFileSystem.h>
#include <UnigineStreams.h>

#include <editor/UnigineActions.h>
#include <editor/UnigineAssetManager.h>
#include <editor/UnigineAssetImportParameters.h>
#include <editor/UnigineConstants.h>
#include <editor/UnigineWindowManager.h>
#include <editor/UnigineSelection.h>
#include <editor/UnigineSelector.h>

#include <QMenu>
#include <QTimer>

using namespace Unigine;
using namespace UnigineEditor;

namespace
{
// test directories to be used
const char DIRECTORY_FOR_NEW_ASSETS[] = "Assets Plugin - Tests/Textures";
const char DIRECTORY_FOR_MOVED_ASSETS[] = "Assets Plugin - Tests/Moved Assets";
const char DIRECTORY_FOR_COPIED_ASSETS[] = "Assets Plugin - Tests/Copied Assets";
const char DIRECTORY_FOR_NEW_DIRECTORIES[] = "Assets Plugin - Tests/Directories";
const char DIRECTORY_FOR_MOUNT_POINT[] = "Assets Plugin - Tests/Mount Point";

// name of the directory to be mounted
const char MOUNT_POINT_DIRECTORY_NAME[] = "Assets Plugin - Test Mount Point";

// path to a test asset
const char TEXTURE_PATH[] = "core/textures/world_light/celestial_body_moon.png";

String convert_vector_to_flat_string(const Vector<String> &v)
{
	String result;
	const int size = std::accumulate(v.begin(), v.end(), 0,
		[](int val, const String &s) { return val + s.size() + 3; });
	result.reserve(size + 1);
	for (const String &s : v)
	{
		result += "\"";
		result += s;
		result += "\" ";
	}
	return result;
}

} // anonymous namespace

bool AssetsPlugin::init()
{
	assert(AssetManager::isInitialized());

	// checking if the test asset file exists
	if (!FileSystem::isFileExist(TEXTURE_PATH))
	{
		Log::error("[Assets Plugin] The required resource is missing: %s\n", TEXTURE_PATH);
	}

	// adding an item for the Assets Plugin to the Windows menu of the UnigineEditor
	QMenu *menu = WindowManager::findMenu(Constants::MM_WINDOWS);
	action_ = menu->addAction("Assets Plugin", this, &AssetsPlugin::activate);

	connect(WindowManager::instance(), &WindowManager::windowHidden, this, [this](QWidget *w) {
		if (w == window_)
		{
			// Postpone destroying, otherwise other receivers will get a dead object
			QTimer::singleShot(0, this, &AssetsPlugin::deactivate);
		}
	});

	return true;
}

void AssetsPlugin::shutdown()
{
	disconnect(WindowManager::instance(), nullptr, this, nullptr);

	delete action_;
	action_ = nullptr;

	deactivate();
}

void AssetsPlugin::activate()
{
	if (is_activated())
	{
		WindowManager::show(window_);
		return;
	}

	create_window();
	make_connections_to_asset_manager();
	make_connection_to_selection();
}

void AssetsPlugin::deactivate()
{
	destroy_connection_from_selection();
	destroy_connections_from_asset_manager();
	destroy_window();
}

void AssetsPlugin::create_window()
{
	assert(nullptr == window_);
	window_ = new EngineGuiWindow;

	setup_window();
	build_gui();

	// To refresh button states
	selection_changed();

	WindowManager::add(window_, WindowManager::NEW_FLOATING_AREA);
	WindowManager::show(window_);
}

void AssetsPlugin::destroy_window()
{
	label_notification_.clear();
	button_lmap_reimporting_.clear();
	gui_.clear();

	if (window_)
	{
		connections_.disconnectAll();
		WindowManager::remove(window_);
		delete window_;
		window_ = nullptr;
	}
}

// Auxiliary method creating the GUI of the Assets Plugin
void AssetsPlugin::build_gui()
{
	gui_ = window_->getGui();

	WidgetWindowPtr main_window = WidgetWindow::create(gui_, "Assets Window");
	gui_->addChild(main_window, Gui::ALIGN_OVERLAP);

	constexpr int DEFAULT_WIDTH = 800;
	constexpr int DEFAULT_HEIGHT = 400;
	main_window->setWidth(DEFAULT_WIDTH);
	main_window->setHeight(DEFAULT_HEIGHT);
	main_window->setSizeable(true);

	add_buttons(main_window);

	label_notification_ = WidgetLabel::create(gui_);
	main_window->addChild(label_notification_, Gui::ALIGN_EXPAND);
}

// Auxiliary method adding button elements to the GUI of the Assets Plugin
void AssetsPlugin::add_buttons(const WidgetWindowPtr &main_window)
{
	auto create_button = [&main_window, this](const char *name, void (AssetsPlugin::*p)()) {
		WidgetButtonPtr button = WidgetButton::create(gui_, name);
		button->getEventClicked().connect(this, p);
		main_window->addChild(button);
		return button;
	};

	// assets
	create_button("Import new asset synchronously", &AssetsPlugin::import_new_asset_synchronously);
	create_button("Import new asset asynchronously",
		&AssetsPlugin::import_new_asset_asynchronously);
	create_button("Remove asset", &AssetsPlugin::remove_asset_asynchronously);
	create_button("Move asset", &AssetsPlugin::move_asset_asynchronously);
	create_button("Rename asset", &AssetsPlugin::rename_asset_asynchronously);
	create_button("Copy asset", &AssetsPlugin::copy_asset_asynchronously);
	create_button("Print all known assets", &AssetsPlugin::print_all_known_assets);
	create_button("Create directory", &AssetsPlugin::create_directory);
	create_button("Remove directory with copied assets",
		&AssetsPlugin::remove_directory_with_copied_assets_asynchronously);
	create_button("Move directory with copied assets",
		&AssetsPlugin::move_directory_with_copied_assets_asynchronously);
	create_button("Rename directory with copied assets",
		&AssetsPlugin::rename_directory_with_copied_assets_asynchronously);
	create_button("Copy directory with copied assets",
		&AssetsPlugin::copy_directory_with_copied_assets_asynchronously);
	create_button("Print all known directories", &AssetsPlugin::print_all_known_directories);
	StringStack<> button_name = String::format("Print all known directories from \"%s\"",
		DIRECTORY_FOR_NEW_DIRECTORIES);
	create_button(button_name, &AssetsPlugin::print_directories_from_test_directory);
	create_button("Create mount point", &AssetsPlugin::create_mount_point);
	create_button("Remove mount point", &AssetsPlugin::remove_mount_point);
	create_button("Print mount point information", &AssetsPlugin::print_mount_point_information);

	button_lmap_reimporting_ = create_button("", &AssetsPlugin::reimport_selected_landscape_map);
}

// Auxiliary method setting up window title and update policy
void AssetsPlugin::setup_window()
{
	window_->setWindowTitle("Plugin - Assets");
	// setting a policy to update window when it's visible to ensure that the status of the Landscape Map Reimport button is refreshed as we select an asset
	window_->setRenderingPolicy(EngineGuiWindow::RENDERING_POLICY_WINDOW_VISIBLE);
}

// Auxiliary method setting up handlers for various events (assets, directories, processing)
void AssetsPlugin::make_connections_to_asset_manager()
{
	using AM = AssetManager;

	assert(connections_.empty());
	// assets
	AM::getEventAssetAdded().connect(connections_, this, &AssetsPlugin::asset_added);
	AM::getEventAssetBeforeRemove().connect(connections_, this, &AssetsPlugin::asset_before_remove);
	AM::getEventAssetRemoved().connect(connections_, this, &AssetsPlugin::asset_removed);
	AM::getEventAssetChanged().connect(connections_, this, &AssetsPlugin::asset_changed);
	AM::getEventAssetMoved().connect(connections_, this, &AssetsPlugin::asset_moved);
	// directories
	AM::getEventDirectoryAdded().connect(connections_, this, &AssetsPlugin::directory_added);
	AM::getEventDirectoryBeforeRemove().connect(connections_, this, &AssetsPlugin::directory_before_remove);
	AM::getEventDirectoryRemoved().connect(connections_, this, &AssetsPlugin::directory_removed);
	AM::getEventDirectoryMoved().connect(connections_, this, &AssetsPlugin::directory_moved);
	// processing
	AM::getEventProcessBegin().connect(connections_, this, &AssetsPlugin::process_begin);
	AM::getEventProcessEnd().connect(connections_, this, &AssetsPlugin::process_end);
}

// Auxiliary method setting up an event handler for tracking selection changes in the UnigineEditor
void AssetsPlugin::make_connection_to_selection()
{
	Selection *selection = Selection::instance();
	connection_selection_ = connect(selection, &Selection::changed, this,
		&AssetsPlugin::selection_changed);
}

// Auxiliary methods removing event subscriptions
void AssetsPlugin::destroy_connection_from_selection()
{
	disconnect(connection_selection_);
}

void AssetsPlugin::destroy_connections_from_asset_manager()
{
	connections_.disconnectAll();
}

// Method importing a new asset and waiting for the process to complete (blocking the thread)
void AssetsPlugin::import_new_asset_synchronously()
{
	// calling an auxiliary function to create a new asset and import it, displaying information on imported asset on success, or an error notification
	String result = create_and_import_new_asset_synchronously();
	if (!result.empty())
	{
		success_notification(
			String::format("Asset has imported successfully: \"%s\"", result.get()));

		// set current Editor selection to the imported asset and print information about it
		select_asset(result);

		print_asset_information(result);
	}
	else
	{
		error_notification(String::format("Can't import asset: \"%s\"", result.get()));
	}
}

// Method importing an asset in the background (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::import_new_asset_asynchronously()
{
	// making a base target path for the asset and generating a unique virtual path for it
	const StringStack<> &base_asset_path = String::joinPaths(DIRECTORY_FOR_NEW_ASSETS,
		String::basename(TEXTURE_PATH));
	const String &new_texture_path = AssetManager::generateUniquePath(base_asset_path);
	if (!create_asset(TEXTURE_PATH, new_texture_path))
	{
		return;
	}

	// launching the importing process in the background (asynchronously, without blocking the main thread) and displaying a notification, if it has started successfully
	// to catch completion of the operation set a handler via AssetManager::getEventProcessEnd.connect() method (see method "process_end()" here)
	if (AssetManager::importAssetAsync(new_texture_path))
	{
		success_notification(String::format("Asset import process has started successfully: \"%s\"",
			new_texture_path.get()));
	}
	else
	{
		error_notification(
			String::format("Can't start asset import process: \"%s\"", new_texture_path.get()));
	}
}

// Method removing an asset in the background (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::remove_asset_asynchronously()
{
	// checking whether there are any assets in the source directory to remove (if not, report and return)
	const Vector<String> &asset_paths = AssetManager::getAssetPathsForDirectory(
		DIRECTORY_FOR_NEW_ASSETS);
	if (asset_paths.empty())
	{
		error_notification(String::format("There are no assets to remove: \"%s\"\n",
			DIRECTORY_FOR_NEW_ASSETS));
		return;
	}

	// launching the asset removal process in the background (asynchronously, without blocking the main thread) and displaying a notification, if it has started successfully
	// to catch completion of the operation set a handler via AssetManager::getEventProcessEnd.connect() method (see method "process_end()" here)
	const String &asset_path_to_remove = asset_paths.last();
	if (AssetManager::removeAssetAsync(asset_path_to_remove))
	{
		success_notification(String::format("Asset removal process has started successfully: \"%s\"",
			asset_path_to_remove.get()));
	}
	else
	{
		error_notification(
			String::format("Can't start asset removal process: \"%s\"", asset_path_to_remove.get()));
	}
}

// Method moving an asset to a new location in the background (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::move_asset_asynchronously()
{
	// checking whether there are any assets in the source directory to move (if not, report and return)
	const Vector<String> &asset_paths = AssetManager::getAssetPathsForDirectory(
		DIRECTORY_FOR_NEW_ASSETS);
	if (asset_paths.empty())
	{
		error_notification(String::format("There are no assets to move: \"%s\"\n",
			DIRECTORY_FOR_NEW_ASSETS));
		return;
	}

	// trying to create a destination directory and displaying error notification in case of failure
	if (!AssetManager::createDirectory(DIRECTORY_FOR_MOVED_ASSETS))
	{
		error_notification(
			String::format("Can't create directory: \"%s\"", DIRECTORY_FOR_MOVED_ASSETS));
		return;
	}

	// making a new asset path and generating a unique virtual path for it
	const String &asset_path_to_move = asset_paths.last();
	const StringStack<> &base_asset_path = String::joinPaths(DIRECTORY_FOR_MOVED_ASSETS,
		asset_path_to_move.basename());
	const String &new_asset_path = AssetManager::generateUniquePath(base_asset_path);

	// launching the "move asset" process in the background (asynchronously, without blocking the main thread) and displaying a notification, if it has started successfully
	// to catch completion of the operation set a handler via AssetManager::getEventProcessEnd.connect() method (see method "process_end()" here)
	if (AssetManager::moveAssetAsync(asset_path_to_move, new_asset_path))
	{
		success_notification(
			String::format("Asset moving process has started successfully: from \"%s\" to \"%s\"",
				asset_path_to_move.get(), new_asset_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start asset moving process: from \"%s\" to \"%s\"",
			asset_path_to_move.get(), new_asset_path.get()));
	}
}

// Method renaming an asset asynchronously (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::rename_asset_asynchronously()
{
	// getting paths for all assets in the directory and checking whether it is empty (if so, report and return)
	const Vector<String> &asset_paths = AssetManager::getAssetPathsForDirectory(
		DIRECTORY_FOR_NEW_ASSETS);
	if (asset_paths.empty())
	{
		error_notification(String::format("There are no assets to rename: \"%s\"\n",
			DIRECTORY_FOR_NEW_ASSETS));
		return;
	}

	// as an example, we rename the last file
	const String &asset_path_to_rename = asset_paths.last();

	const StringStack<> &new_asset_dir_path = String::dirname(asset_path_to_rename);
	const char *NEW_ASSET_FILE_NAME = "Renamed Asset";

	// making a new asset path and generating a unique virtual path for it
	StringStack<> new_asset_path = String::joinPaths(new_asset_dir_path, NEW_ASSET_FILE_NAME);
	new_asset_path += '.' + String::extension(asset_path_to_rename);

	new_asset_path = AssetManager::generateUniquePath(new_asset_path);

	// getting a base name for it to set while renaming
	const StringStack<> &new_asset_name = new_asset_path.basename();

	// putting a new "asset rename" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::renameAssetAsync(asset_path_to_rename, new_asset_name))
	{
		success_notification(
			String::format("Asset renaming process has started successfully: from \"%s\" to \"%s\"",
				asset_path_to_rename.get(), new_asset_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start asset renaming process: from \"%s\" to \"%s\"",
			asset_path_to_rename.get(), new_asset_path.get()));
	}
}

// Method copying an asset asynchronously (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::copy_asset_asynchronously()
{
	// getting paths for all assets in the directory and checking whether it is empty (if so, report and return)
	const Vector<String> &asset_paths = AssetManager::getAssetPathsForDirectory(
		DIRECTORY_FOR_NEW_ASSETS);
	if (asset_paths.empty())
	{
		error_notification(String::format("There are no assets to copy: \"%s\"\n",
			DIRECTORY_FOR_NEW_ASSETS));
		return;
	}

	// as an example, we copy the last file
	const String &asset_path_to_copy = asset_paths.last();

	// creating a new directory
	if (!AssetManager::createDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Can't create directory: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// making a base path and generating a unique virtual path for a new copy of the asset
	const StringStack<> &base_asset_path = String::joinPaths(DIRECTORY_FOR_COPIED_ASSETS,
		asset_path_to_copy.basename());
	const String &new_asset_path = AssetManager::generateUniquePath(base_asset_path);

	// putting a new "asset copy" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::copyAssetAsync(asset_path_to_copy, new_asset_path))
	{
		success_notification(
			String::format("Asset copying process has started successfully: from \"%s\" to \"%s\"",
				asset_path_to_copy.get(), new_asset_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start asset copying process: from \"%s\" to \"%s\"",
			asset_path_to_copy.get(), new_asset_path.get()));
	}
}

// Method printing out the list of paths and GUIDs for all assets in the root project directory (including all subdirectories)
void AssetsPlugin::print_all_known_assets()
{
	Log::message("[Assets Plugin] All asset paths:\n");
	for (const String &path : AssetManager::getAssetPaths())
	{
		Log::message("\t%s\n", path.get());
	}
	Log::message("\n[Assets Plugin] All asset GUIDs:\n");
	for (const UGUID &guid : AssetManager::getAssetGUIDs())
	{
		Log::message("\t%s\n", FileSystem::guidToPath(guid).get());
	}
	Log::message("\n");
}

// Method printing out general information for the specified asset path
void AssetsPlugin::print_asset_information(const char *asset_path)
{
	const UGUID &asset_guid = AssetManager::getAssetGUIDFromPath(asset_path);
	// It's only to demonstrate the usage of some API functions:
	Log::message("[Assets Plugin] Asset information:\n");
	Log::message("\tVirtual path: %s\n", AssetManager::getAssetPathFromGUID(asset_guid).get());
	Log::message("\tFile GUID: %s\n", FileSystem::guidToPath(asset_guid).get());
	Log::message("\tAccess: %s\n",
		AssetManager::isAssetWritable(asset_path) ? "read & write" : "read-only");
	auto get_import_parameters_as_string = [asset_path] {
		const CollectionPtr &parameters = AssetManager::getAssetImportParameters(asset_path);
		return convert_vector_to_flat_string(parameters->getNames());
	};
	Log::message("\tImport parameter names: %s\n", get_import_parameters_as_string().get());

	// getting the list of GUIDs for all runtimes generated for the asset path and displaying general information about them (if any)
	const Vector<UGUID> &runtime_guids = AssetManager::getRuntimeGUIDs(asset_path);
	if (runtime_guids.empty())
	{
		Log::message("\tNo runtimes\n");
	}
	else
	{
		Log::message("\tRuntimes:\n");
		for (int i = 0, count = runtime_guids.size(); i < count; ++i)
		{
			const UGUID &rt_guid = runtime_guids[i];
			Log::message("\t\tRuntime #%d is %s: Alias (%s) File GUID (%s)\n", i,
				AssetManager::isRuntimePrimary(rt_guid) ? "primary" : "non-primary",
				AssetManager::getRuntimeAlias(rt_guid).get(), FileSystem::guidToPath(rt_guid).get());
		}
	}
}

// Method creating a new directory
void AssetsPlugin::create_directory()
{
	// making a base path for a new directory and generating a unique virtual path for it
	const StringStack<> &base_path = String::joinPaths(DIRECTORY_FOR_NEW_DIRECTORIES,
		"New Directory");
	const String &new_path = AssetManager::generateUniquePath(base_path);

	// creating a new directory for the specified path and displaying the corresponding notification
	if (AssetManager::createDirectory(new_path))
	{
		success_notification(
			String::format("Directory has been created successfully: \"%s\"", new_path.get()));
		assert(AssetManager::isDirectoryWritable(new_path));
	}
	else
	{
		error_notification(String::format("Can't create directory: \"%s\"", new_path.get()));
	}
}

// Method removing a directory with assets (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::remove_directory_with_copied_assets_asynchronously()
{
	// checking if the specified directory exists (if not, report and return)
	if (!AssetManager::isDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Directory doesn't exist: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// putting a new "remove directory" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::removeDirectoryAsync(DIRECTORY_FOR_COPIED_ASSETS))
	{
		success_notification(String::format("Directory removal process has started successfully: \"%s\"",
			DIRECTORY_FOR_COPIED_ASSETS));
	}
	else
	{
		error_notification(
			String::format("Can't start directory removal process: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
	}
}

// Method moving a directory with assets to a new location (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::move_directory_with_copied_assets_asynchronously()
{
	// checking if the source directory exists (if not, report and return)
	if (!AssetManager::isDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Directory doesn't exist: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// making a base destination path and generating a unique virtual path for it
	const StringStack<> &base_path = String::joinPaths(DIRECTORY_FOR_NEW_DIRECTORIES,
		"New Directory");
	const String &new_path = AssetManager::generateUniquePath(base_path);

	// putting a new "move directory" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::moveDirectoryAsync(DIRECTORY_FOR_COPIED_ASSETS, new_path))
	{
		success_notification(
			String::format("Directory moving process has started successfully: from \"%s\" to \"%s\"",
				DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start directory moving process:  from \"%s\" to \"%s\"",
			DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
}

// Method renaming a directory with assets (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::rename_directory_with_copied_assets_asynchronously()
{
	// checking if the specified directory exists (if not, report and return)
	if (!AssetManager::isDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Directory doesn't exist: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// generating a unique virtual path for the destination directory and getting its base name to change it
	const String &new_path = AssetManager::generateUniquePath(DIRECTORY_FOR_COPIED_ASSETS);
	const StringStack<> &new_name = new_path.basename();

	// putting a new "rename directory" task to a queue and displaying the corresponding notification depending on the result
	if (AssetManager::renameDirectoryAsync(DIRECTORY_FOR_COPIED_ASSETS, new_name))
	{
		success_notification(
			String::format("Directory renaming process has started successfully: from \"%s\" to \"%s\"",
				DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start directory renaming process: from \"%s\" to \"%s\"",
			DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
}

// Method copying a directory with assets to the specified path (non-blocking, returns immediately without waiting for operation completion)
void AssetsPlugin::copy_directory_with_copied_assets_asynchronously()
{
	// checking if the specified directory exists (if not, report and return)
	if (!AssetManager::isDirectory(DIRECTORY_FOR_COPIED_ASSETS))
	{
		error_notification(
			String::format("Directory doesn't exist: \"%s\"", DIRECTORY_FOR_COPIED_ASSETS));
		return;
	}

	// making the destination base path, to which the directory is to be copied, and generating a new unique virtual path for it
	const StringStack<> &base_path = String::joinPaths(DIRECTORY_FOR_NEW_DIRECTORIES,
		"New Directory");
	const String &new_path = AssetManager::generateUniquePath(base_path);

	// launching the copying process in the background (asynchronously, without blocking the main thread) and displaying a notification, if it has started successfully
	// to catch completion of the operation set a handler via AssetManager::getEventProcessEnd.connect() method (see method "process_end()" here)
	if (AssetManager::copyDirectoryAsync(DIRECTORY_FOR_COPIED_ASSETS, new_path))
	{
		success_notification(
			String::format("Directory copying process has started successfully: from \"%s\" to \"%s\"",
				DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
	else
	{
		error_notification(String::format("Can't start directory copying process: from \"%s\" to \"%s\"",
			DIRECTORY_FOR_COPIED_ASSETS, new_path.get()));
	}
}

// Method listing all directories known to the AssetManager
void AssetsPlugin::print_all_known_directories()
{
	Log::message("\n[Assets Plugin] All directory paths:\n");
	for (const String &path : AssetManager::getDirectoryPathsAll())
	{
		Log::message("\t%s\n", path.get());
	}
	Log::message("\n");
}

// Method listing all subdirectories of the specified path, that are known to the AssetManager
void AssetsPlugin::print_directories_from_test_directory()
{
	Log::message("\n[Assets Plugin] Directory paths from \"%s\":\n", DIRECTORY_FOR_NEW_DIRECTORIES);
	for (const String &path : AssetManager::getDirectoryPaths(DIRECTORY_FOR_NEW_DIRECTORIES))
	{
		Log::message("\t%s\n", path.get());
	}
	Log::message("\n");
}

// Method creating a new mount point
void AssetsPlugin::create_mount_point()
{
	// checking if a path for a mount point to be created already exists and displaying the corresponding notifications
	if (AssetManager::isExist(DIRECTORY_FOR_MOUNT_POINT))
	{
		if (AssetManager::isAsset(DIRECTORY_FOR_MOUNT_POINT))
		{
			error_notification(
				String::format("Target path already contains a known asset: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		}
		else if (AssetManager::isMountPoint(DIRECTORY_FOR_MOUNT_POINT))
		{
			assert(AssetManager::isDirectory(DIRECTORY_FOR_MOUNT_POINT));	// Mount point is a directory
			success_notification(
				String::format("Mount point for the target path already exists: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		}
		else if (AssetManager::isDirectory(DIRECTORY_FOR_MOUNT_POINT))
		{
			error_notification(
				String::format("Target path already contains a known directory: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		}
		else
		{
			// May be some reserved file or directory already exists there
			error_notification(
				String::format("Target path already exists and may contain a reserved file or some directory: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		}
		return;
	}

	// making an absolute path to the mount
	StringStack<> abs_dir_path = String::normalizeDirPath(Engine::get()->getDataPath());
	abs_dir_path = abs_dir_path.trimLast("/");
	abs_dir_path = abs_dir_path.dirname();
	abs_dir_path = String::joinPaths(abs_dir_path, MOUNT_POINT_DIRECTORY_NAME);

	// getting an existing directory for the absolute path or creating it
	if (!Dir::mkdir(abs_dir_path))
	{
		error_notification(String::format("Can't create directory \"%s\"", abs_dir_path.get()));
		return;
	}

	// creating an instance of the MountPointParameters class to specify necessary settings for a new mount point to be created (path and access mode)
	MountPointParametersPtr mount_params = MountPointParameters::create();
	mount_params->setAbsolutePath(abs_dir_path);
	mount_params->setAccess(MountPointParameters::ACCESS_READWRITE);

	// trying to create a new mount point for the specified path and parameters, displaying a notification depending on the result
	if (AssetManager::createMountPoint(DIRECTORY_FOR_MOUNT_POINT, mount_params))
	{
		success_notification(String::format("Mount point has been created successfully: \"%s\"",
			DIRECTORY_FOR_MOUNT_POINT));
		assert(AssetManager::isMountPoint(DIRECTORY_FOR_MOUNT_POINT));
	}
	else
	{
		error_notification(
			String::format("Can't create mount point: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
	}
}

// Method removing a mount point
void AssetsPlugin::remove_mount_point()
{
	// checking if the specified mount point exists
	if (!AssetManager::isMountPoint(DIRECTORY_FOR_MOUNT_POINT))
	{
		error_notification(
			String::format("Mount point doesn't exist \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
		return;
	}

	// trying to remove the specified mount point via the AssetManager, displaying a notification depending on the result
	if (AssetManager::removeMountPoint(DIRECTORY_FOR_MOUNT_POINT))
	{
		success_notification(String::format("Mount point has been removed successfully: \"%s\"",
			DIRECTORY_FOR_MOUNT_POINT));
	}
	else
	{
		error_notification(
			String::format("Can't remove mount point: \"%s\"", DIRECTORY_FOR_MOUNT_POINT));
	}
}

// Method printing complete information about the mount point (virtual path, access, and filters)
void AssetsPlugin::print_mount_point_information()
{
	// checking if the specified mount point exists
	if (!AssetManager::isMountPoint(DIRECTORY_FOR_MOUNT_POINT))
	{
		Log::message("[Assets Plugin] Mount point doesn't exist: \"%s\"\n",
			DIRECTORY_FOR_MOUNT_POINT);
		return;
	}

	Log::message("[Assets Plugin] Mount point information\n\n");
	Log::message("\tVirtual path: \"%s\"\n", DIRECTORY_FOR_MOUNT_POINT);

	// retrieving parameters of the specified mount point to a MountPointParameters class instance and print information using its data
	const MountPointParametersPtr mount_params = AssetManager::getMountPointParameters(
		DIRECTORY_FOR_MOUNT_POINT);

	Log::message("\tAbsolute path: \"%s\"\n", mount_params->getAbsolutePath());
	Log::message("\tAccess: \"%s\"\n",
		(mount_params->getAccess() == MountPointParameters::ACCESS_READONLY) ? "read-only"
																			 : "read & write");

	// retrieving exclusive filters of the specified mount point to a vector and printing its contents or a corresponding message in case filters are not set
	const Vector<String> &exclusive_filters = mount_params->getExclusiveFilters();
	if (exclusive_filters.empty())
	{
		Log::message("\tNo exclusive filters\n");
	}
	else
	{
		Log::message("\tExclusive filters: %s\n", convert_vector_to_flat_string(exclusive_filters));
	}

	// retrieving ignore filters of the specified mount point to a vector and printing its contents or a corresponding message in case filters are not set
	const Vector<String> &ignore_filters = mount_params->getIgnoreFilters();
	if (ignore_filters.empty())
	{
		Log::message("\tNo ignore filters\n");
	}
	else
	{
		Log::message("\tIgnore filters: %s\n", convert_vector_to_flat_string(ignore_filters));
	}

	Log::message("\n");
}

// Method reimporting the selected Landscape Map (.lmap) asset
void AssetsPlugin::reimport_selected_landscape_map()
{
	// trying to get an .lmap-file in the current selection
	const String &lmap_path = find_selected_lmap_file();
	if (lmap_path.empty())
	{
		return;
	}

	// getting current import parameters for the .lmap asset to an instance of the Collection class
	CollectionPtr source_import_parameters = AssetManager::getAssetImportParameters(lmap_path);
	LandscapeMapImportParametersPtr lmap_import_parameters = LandscapeMapImportParameters::create();
	lmap_import_parameters->load(source_import_parameters);

	// switching the data filling mode import parameter for the asset
	using DataMode = LandscapeMapImportParameters::DATA_FILLING_MODE;
	DataMode mode = lmap_import_parameters->getDataFillingMode();
	switch (mode)
	{
	case DataMode::DATA_FILLING_MODE_FROM_TILESET: mode = DataMode::DATA_FILLING_MODE_MANUAL; break;
	case DataMode::DATA_FILLING_MODE_MANUAL: mode = DataMode::DATA_FILLING_MODE_FROM_TILESET; break;
	}
	lmap_import_parameters->setDataFillingMode(mode);

	// saving new import parameters and using them to reimport asset asynchronously with corresponding notification on starting the process
	CollectionPtr dest_import_parameters = lmap_import_parameters->save();
	if (AssetManager::reimportAssetAsync(lmap_path, dest_import_parameters))
	{
		success_notification(String::format(
			"Asset reimport process has started successfully: \"%s\"", lmap_path.get()));
	}
	else
	{
		error_notification(
			String::format("Can't start asset reimport process: \"%s\"", lmap_path.get()));
	}
}

// auxiliary method setting the current Editor selection to an asset having the specified path
void AssetsPlugin::select_asset(const char *asset_path)
{
	// checking if an asset with the specified path exists and getting its guid
	assert(AssetManager::isAsset(asset_path));
	const UGUID &asset_guid = AssetManager::getAssetGUIDFromPath(asset_path);
	if (asset_guid.isEmpty())
	{
		error_notification(String::format("Invalid path for asset: \"%s\"", asset_path));
		return;
	}

	// setting the current Editor selection to an asset with the specified guid
	SelectionAction::applySelection(SelectorGUIDs::createRuntimesSelector({asset_guid}));
}
// auxiliary method displaying a success message
void AssetsPlugin::success_notification(const char *message) const
{
	notification(message, Math::vec4_green);
}

// auxiliary method displaying an error message
void AssetsPlugin::error_notification(const char *message) const
{
	notification(message, Math::vec4_red);
}

// auxiliary method displaying a generic notification message using the specified color
void AssetsPlugin::notification(const char *message, const Math::vec4 &color) const
{
	if (label_notification_)
	{
		label_notification_->setFontColor(color);
		label_notification_->setText(message);
	}
	Log::message(color, "[Assets Plugin] %s\n", message);
}
// Method creating and importing an asset synchronously (blocking the thread until the operation is completed)
String AssetsPlugin::create_and_import_new_asset_synchronously() const
{
	String result;

	// making a base path for a new asset to be imported
	const StringStack<> &base_asset_path = String::joinPaths(DIRECTORY_FOR_NEW_ASSETS,
		String::basename(TEXTURE_PATH));

	// asking  the Asset Manager to generate a unique
	String new_texture_path = AssetManager::generateUniquePath(base_asset_path);
	if (!create_asset(TEXTURE_PATH, new_texture_path))
	{
		return result;
	}
	// waiting for the texture asset to be imported by the AssetManager and returning the result (new texture path on success of an empty string on failure)
	if (AssetManager::importAssetSync(new_texture_path))
	{
		result = std::move(new_texture_path);
	}

	return result;
}
// Auxiliary method creating an asset with the specified destination path for the specified source path
bool AssetsPlugin::create_asset(const char *source_path, const char *dest_path) const
{
	// retrieving a path to destination directory and creating it via the AssetManager (the corresponding handler shall be executed)
	const StringStack<> &dir_path = String::dirname(dest_path);
	if (!AssetManager::createDirectory(dir_path))
	{
		error_notification(String::format("Can't create directory: \"%s\"", dir_path.get()));
		return false;
	}

	// opening the source file for reading data
	FilePtr source_asset = File::create(source_path, "rb");
	if (!source_asset->isOpened())
	{
		error_notification(String::format("Can't open asset for reading: \"%s\"", source_path));
		return false;
	}

	// opening the destination asset file for writing data
	FilePtr dest_asset = File::create(dest_path, "wb");
	if (!dest_asset->isOpened())
	{
		error_notification(String::format("Can't open asset for writing: \"%s\"", dest_path));
		return false;
	}

	// declaring a 32Kb buffer for transferring data
	const size_t MEMORY_SIZE = 1024 * 32;
	Vector<unsigned char> memory(MEMORY_SIZE);
	// reading and writing data from the source file to the destination asset
	while (0 == source_asset->eof())
	{
		const size_t bytes_read = source_asset->read(&memory[0], memory.size());
		const size_t bytes_written = dest_asset->write(&memory[0], bytes_read);
		if (bytes_read != bytes_written)
		{
			dest_asset->close();
			dest_asset.clear();
			Dir::remove(dest_path);
			error_notification(String::format("Can't write data to asset: \"%s\"", dest_path));
			return false;
		}
	}

	return true;
}

// Auxiliary method iterating over the current selection and finds the path to the first .lmap asset in the current Editor selection.
String AssetsPlugin::find_selected_lmap_file() const
{
	String lmap_path;

	// getting guids of runtimes for all currently selected assets, returning an empty string if nothing is selected
	const SelectorGUIDs *selector = Selection::getSelectorRuntimes();
	if (!selector || selector->empty())
	{
		return lmap_path;
	}

	// getting guids of all currently selected assets
	const Vector<UGUID> &selected_guids = selector->guids();
	for (const UGUID &guid : selected_guids)
	{
		// obtaining asset path by its GUID and checking if the path corresponds to a registered asset
		String virtual_path = AssetManager::getAssetPathFromGUID(guid);
		if (!AssetManager::isAsset(virtual_path))
		{
			Log::message("[Assets Plugin] Invalid asset path: %s\n", virtual_path.get());
			continue;
		}

		// getting an extension for the asset file and return the virtual path if it is an .lmap asset
		const StringStack<> &extension = virtual_path.extension().getLower();
		if (!String::equal(extension, "lmap"))
		{
			continue;
		}

		lmap_path = std::move(virtual_path);
		break;
	}

	return lmap_path;
}

// function to be executed on adding a new asset
void AssetsPlugin::asset_added(const char *path)
{
	Log::message("[Assets Plugin] Asset added: %s\n", path);
	// Add your custom handling code here...
}

// function to be executed before removing an asset
void AssetsPlugin::asset_before_remove(const char *path)
{
	Log::message("[Assets Plugin] Asset before removing: %s\n", path);
	// Add your custom handling code here...
}

// function to be executed after removing an asset
void AssetsPlugin::asset_removed(const char *path)
{
	Log::message("[Assets Plugin] Asset removed: %s\n", path);
	// Add your custom handling code here...
}

// function to be executed on changing an asset
void AssetsPlugin::asset_changed(const char *path)
{
	Log::message("[Assets Plugin] Asset changed: %s\n", path);
	// Add your custom handling code here...
}

// function to be executed on moving an asset to a new location
void AssetsPlugin::asset_moved(const char *path_from, const char *path_to)
{
	Log::message("[Assets Plugin] Asset moved from \"%s\" to \"%s\"\n", path_from, path_to);
	// Add your custom handling code here...
}

// function to be executed on adding a new directory
void AssetsPlugin::directory_added(const char *path)
{
	Log::message("[Assets Plugin] Directory added: %s\n", path);
	// Add your custom handling code here...
}

// function to be executed before removing a directory
void AssetsPlugin::directory_before_remove(const char *path)
{
	Log::message("[Assets Plugin] Directory before removing: %s\n", path);
	// Add your custom handling code here...
}

// function to be executed after removing a directory
void AssetsPlugin::directory_removed(const char *path)
{
	Log::message("[Assets Plugin] Directory removed: %s\n", path);
	// Add your custom handling code here...
}

// function to be executed on moving a directory to a new location
void AssetsPlugin::directory_moved(const char *path_from, const char *path_to)
{
	Log::message("[Assets Plugin] Directory moved from \"%s\" to \"%s\"\n", path_from, path_to);
	// Add your custom handling code here...
}

// function to be executed on beginning of asynchronous asset processing by the Asset Manager (e.g., validation, import, reimport, removal, copying, conversion, migration etc.)
void AssetsPlugin::process_begin()
{
	Log::message("[Assets Plugin] Processing started\n");
	// Add your custom handling code here...
}

// function to be executed on completion of asynchronous asset processing by the Asset Manager (e.g., validation, import, reimport, removal, copying, conversion, migration etc.)
void AssetsPlugin::process_end()
{
	Log::message("[Assets Plugin] Processing completed\n");
	// Add your custom handling code here...
}

// function to be executed on changing selection in the Editor
void AssetsPlugin::selection_changed()
{
	// trying to get an .lmap-file in the current selection
	const String &lmap_path = find_selected_lmap_file();

	// updating the button text and status depending on the result
	const char BUTTON_LMAP_REIMPORT_NAME[] = "Reimport Landscape Map";
	const StringStack<> &button_name = String::format("%s%s%s", BUTTON_LMAP_REIMPORT_NAME,
		lmap_path.empty() ? "" : " - ", lmap_path.get());
	button_lmap_reimporting_->setText(button_name);
	button_lmap_reimporting_->setEnabled(lmap_path.size() > 0);
}

```

</details>
