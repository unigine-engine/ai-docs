# Unigine::FileSystem Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


On the [Engine file system](../../../principles/filesystem/index.md) initialization, all files and packages stored in the `data` folder are added to the virtual file system automatically. At that, content of the ZIP and UNG packages is loaded into RAM as is (so, you'd better not store heavy content (e.g. terrains) in the packages).


Files and packages stored outside the `data` directory are also added to the virtual file system, if they are [mounted](../../../principles/filesystem/index.md#mount_points) (i.e. referenced by a mount point).

> **Notice:** If you add new files at run time, the Engine won't know anything about such files. To add the files to the virtual file system, use *[addVirtualFile()](#addVirtualFile_cstr_UGUID_bool_bool)*.


File System functions:


- Provide control over [asynchronous loading](../../../api/library/filesystem/class.asyncqueue_usc.md) of files/meshes/images/nodes on demand under the `data` directory, including files in ZIP and UNG packages. Such packages are [automatically handled](../../../principles/filesystem/index.md#file_packages) by the Engine and all their files are automatically added to the file system.
- Allow adding directories (even with ZIP and UNG packages) that are [outside](../../../principles/filesystem/index.md#mount_points) the `data` directory and provide [control over loading](../../../api/library/filesystem/class.asyncqueue_usc.md) such files.
- Allow adding ZIP and UNG packages that are [outside the `data`](../../../principles/filesystem/index.md#mount_points) directory. After that, files in such packages are accessed in a usual way, by specifying a path to the file only inside the package.
- Allow [caching](#addCacheFile_cstr_bool) files in the memory and [adding files to blobs](#addBlobFile_cstr_bool) if they are accessed or modified multiple times at run time.


Also methods of the FileSystem class can be used when implementing your own importer from an external format to UNIGINE-native ones. For example, you can store only the original file on the disk, files in UNIGINE-native formats can be stored in the virtual file system only.


### Getting the Asset Filename


Using the [GUID](../../../api/library/filesystem/class.uguid_usc.md) of an asset or the path to the source file on a disk, you can get access to the filename the following way:


### See also


- [engine.async Class](../../../api/library/filesystem/class.asyncqueue_usc.md) to manage loading resources (files, images, meshes, and nodes) on demand.
- A set of UnigineScript API samples located in the `<UnigineSDK>/data/samples/systems/` folder:

  - modifiers_00
  - packages_00
  - packages_01


## FileSystem Class

### Members

## int getNumModifiers () const

Returns the current total number of file modifiers registered in the file system.
### Return value

Current total number of file modifiers registered in the file system.
## static getEventFileChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventFileRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventFileAdded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventFilesChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventFilesRemoved () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventFilesAdded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## engine.filesystem. getMount ( )

Returns a [mount point](../../../principles/filesystem/index.md#mount_points) for the specified path.
> **Notice:** This method will return the [root mount](#getRootMount_FileSystemMount) for all files located directly in the `data` folder or its subfolders.


### Arguments

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_usc.md) class instance on success; otherwise, **nullptr**.
## engine.filesystem. getMount ( )

Returns a [mount point](../../../principles/filesystem/index.md#mount_points) for the specified [GUID](../../../api/library/filesystem/class.uguid_usc.md).
> **Notice:** This method will return the [root mount](#getRootMount_FileSystemMount) for all files located directly in the `data` folder or its subfolders.


### Arguments

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_usc.md) class instance on success; otherwise, **nullptr**.
## void engine.filesystem. getMounts ( )

Returns a list of all [mount points](../../../principles/filesystem/index.md#mount_points) currently used by the file system and puts the to the specified output buffer.
> **Notice:** This list will not include the [root mount](#getRootMount_FileSystemMount).


### Arguments

## FileSystemMount engine.filesystem. getRootMount ( )

Returns the root mount of the file system. It mounts the `data` folder to the root of the virtual file system. The root mount cannot be unmounted.
### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_usc.md) class instance for the root mount of the virtual file system.
## FileSystemMount engine.filesystem. addMount ( string umount_path )

 Adds a new [mount point](../../../principles/filesystem/index.md#mount_points) using the data from the specified `*.umount` file.All mounted files are automatically added as known to the virtual file system.
### Arguments

- *string* **umount_path** - Absolute path to a `*.umount` file.

### Return value

[FileSystemMount](../../../api/library/filesystem/class.filesystemmount_usc.md) class instance, if it was created successfully; otherwise, **nullptr**.
## bool engine.filesystem. saveMountFile ( string umount_path )

Saves the specified `*.umount` file.
### Arguments

- *string* **umount_path** - [Mount point](../../../principles/filesystem/index.md#mount_points) file path.

### Return value

true if the specified `*.umount` file is saved successfully; otherwise, false.
## bool engine.filesystem. removeMount ( string path )

 Unmounts a [mount point](../../../principles/filesystem/index.md#mount_points) with a given path.
> **Notice:** The [root mount](#getRootMount_FileSystemMount) cannot be removed.


### Arguments

- *string* **path** - Absolute path to the mounted folder/package.

### Return value

true if the mount point with a given path is successfully unmounted; otherwise, false.
## void engine.filesystem. clearMounts ( )

 Unmounts all [mount points](../../../principles/filesystem/index.md#mount_points).
> **Notice:** This method does not remove the [root mount](#getRootMount_FileSystemMount).


## bool engine.filesystem. loadPackage ( string path )

 Loads an UNG or ZIP package into the file system. Note that the package should be [mounted](../../../principles/filesystem/index.md#mount_points), otherwise it won't be loaded.
> **Notice:** UNG packages without password protection can be loaded even if the engine has built-in password for the file system packages. For example, it is possible to load both the `core.ung` package without a password and the `my_assets.ung` package protected with a password.


### Arguments

- *string* **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index.md#paths).

### Return value

**true** if the package is loaded; otherwise, **false**.
## bool engine.filesystem. loadPackage ( string path , string extension )

 Loads a package with the specified extension (ung, zip, or pak) into the file system. Note that the package should be [mounted](../../../principles/filesystem/index.md#mount_points), otherwise it won't be loaded.
> **Notice:** UNG packages without password protection can be loaded even if the engine has built-in password for the file system packages. For example, it is possible to load both the `core.ung` package without a password and the `my_assets.ung` package protected with a password.


### Arguments

- *string* **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index.md#paths).
- *string* **extension** - Extension of a custom package, one of the following values:

  - ung
  - zip
  - pak

### Return value

**true** if the package is loaded; otherwise, **false**.
## bool engine.filesystem. removePackage ( string path )

Unloads an UNG or ZIP package from the file system.
### Arguments

- *string* **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index.md#paths).

### Return value

true if the package is removed; otherwise, false.
## void engine.filesystem. getSupportedPackagesExtensions ( Vector<String>& OUT_extensions )

Returns a list of registered extensions that can be loaded as a package.
### Arguments

- *Vector<String>&* **OUT_extensions** - An array to store registered extensions. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void engine.filesystem. getPackageVirtualFiles ( )

Saves the list of names for all virtual files stored in the specified package to the specified string buffer.
### Arguments

## void engine.filesystem. getPackageVirtualFiles ( )

Saves the list of names for all virtual files stored in a package with the specified name and extension to the specified string buffer.
### Arguments

## void engine.filesystem. getVirtualFiles ( )

Saves the list of names for all known files registered in the file system to the specified string buffer.
### Arguments

## bool engine.filesystem. isVirtualFile ( )

Checks if the given file is known to the virtual file system.
### Arguments

### Return value

true if the file is known to the virtual file system; otherwise, false.
## bool engine.filesystem. isVirtualFile ( )

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) is known to the virtual file system and has a virtual path registered.
### Arguments

### Return value

true if the file is known to the virtual file system; otherwise, false.
## bool engine.filesystem. addVirtualFile ( string path , UGUID guid , bool must_exist = false )

Registers the regular file name as known virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) and appends it to the map used for fast searching. This method should be used when you need to add, for example, a new content to the project.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - File [GUID](../../../api/library/filesystem/class.uguid_usc.md).
- *bool* **must_exist** - A flag indicating whether the specified file must [exist](#isFileExist_cstr_bool).

### Return value

true if the file name is appended successfully; otherwise, false.
## UGUID engine.filesystem. addVirtualFile ( bool must_exist = false )

Registers the regular file name as known virtual file and appends it to the map used for fast searching. This method should be used when you need to add, for example, a new content to the project.
### Arguments

- *bool* **must_exist** - A flag indicating whether the specified file must [exist](#isFileExist_cstr_bool).

### Return value

File [GUID](../../../api/library/filesystem/class.uguid_usc.md) if it was registered successfully or an empty GUID, otherwise.
## bool engine.filesystem. renameVirtualFile ( )

Renames the specified known virtual file.
### Arguments

### Return value

true if the file is renamed successfully; otherwise, false.
## bool engine.filesystem. renameVirtualFile ( )

Renames the specified known file and assigns it the specified new [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

### Return value

true if the file is renamed successfully; otherwise, false.
## bool engine.filesystem. renameVirtualFile ( )

Renames the known virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

### Return value

true if the file is renamed successfully; otherwise, false.
## bool engine.filesystem. renameVirtualFile ( )

Renames the known virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) and assigns it the specified new [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

### Return value

true if the file is renamed successfully; otherwise, false.
## bool engine.filesystem. removeVirtualFile ( )

Removes the virtual file with the given name.
### Arguments

### Return value

true if the file is removed successfully; otherwise, false.
## bool engine.filesystem. removeVirtualFile ( )

Removes the virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

### Return value

true if the file is removed successfully; otherwise, false.
## bool engine.filesystem. changeVirtualFile ( )

Marks the virtual file with the given name as modified. The corresponding *CALLBACK_FILE_CHANGED* signal is emitted. This method is used to notify the Engine that a resource has been modified and needs to be updated.
### Arguments

### Return value

true if the file is successfully marked as modified; otherwise, false.
## bool engine.filesystem. changeVirtualFile ( )

Marks the virtual file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) as modified. The corresponding *CALLBACK_FILE_CHANGED* signal is emitted. This method is used to notify the Engine that a resource has been modified and needs to be updated.
### Arguments

### Return value

true if the file is successfully marked as modified; otherwise, false.
## void engine.filesystem. removeNonExistingVirtualFiles ( )

Removes all non-existing virtual files from the File System. These files aren't physically exist on the disk, however, they are added to the virtual file system. For example, it can be a blob or a cache file.
## bool engine.filesystem. isBlobFile ( )

Checks if the given file is [loaded](#addBlobFile_cstr_bool) to a blob.
### Arguments

### Return value

true if the file is loaded to a blob successfully; otherwise, false.
## bool engine.filesystem. isBlobFile ( )

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) is [loaded](#addBlobFile_UGUID_bool) to a blob.
### Arguments

### Return value

true if the file is loaded to a blob successfully; otherwise, false.
## bool engine.filesystem. addBlobFile ( )

Adds a file into a blob. It can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

### Return value

true if the file is successfully added into a blob; otherwise, false.
## bool engine.filesystem. addBlobFile ( )

Adds a file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) into a blob. It can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

### Return value

true if the file is successfully added into a blob; otherwise, false.
## bool engine.filesystem. removeBlobFile ( )

Removes a file from the blob. Blobbing can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

### Return value

true if the file is removed successfully; otherwise, false.
## bool engine.filesystem. removeBlobFile ( )

Removes a file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) from the blob. Blobbing can be used for files that are frequently modified at run time (for example, images). After such file is loaded from a disk and written into a blob in the memory, its modifications can be saved fast into this blob.
### Arguments

### Return value

true if the file is removed successfully; otherwise, false.
## bool engine.filesystem. isCacheFile ( )

Checks if the given file is loaded into cache.
### Arguments

### Return value

true if the file is added into cache; otherwise, false.
## bool engine.filesystem. isCacheFile ( )

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) is loaded into cache.
### Arguments

### Return value

true if the file is added into cache; otherwise, false.
## bool engine.filesystem. addCacheFile ( )

Caches a file in the memory. It can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

### Return value

true if the file is successfully added to cache; otherwise, false.
## bool engine.filesystem. addCacheFile ( )

Caches a file in the memory with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md). It can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

### Return value

true if the file is successfully added to cache; otherwise, false.
## bool engine.filesystem. removeCacheFile ( )

Removes a cached file from the memory. Caching can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

### Return value

true if the file is successfully removed from cache; otherwise, false.
## bool engine.filesystem. removeCacheFile ( )

Removes a cached file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) from the memory. Caching can be used for files that are accessed multiple times at run time (for example, textures are read two times in a row). Such files are loaded into the memory for faster reading.
### Arguments

### Return value

true if the file is successfully removed from cache; otherwise, false.
## bool engine.filesystem. isDiskFile ( )

Returns a value indicating if the specified file path is a path to a file on disk (i.e. not a package, a blob, or a cache file).
### Arguments

### Return value

true if the specified file path is a path to a file on disk; otherwise, false.
## bool engine.filesystem. isPackageFile ( )

Returns a value indicating if the specified file path is a path to a file inside a ZIP or UNG package.
### Arguments

### Return value

true if the specified file path is a path to a file inside a ZIP or UNG package; otherwise, false.
## String engine.filesystem. resolvePartialVirtualPath ( string path )

Converts the given [partial path](../../../principles/filesystem/index.md#partial) to a full virtual one.
> **Notice:** If the file isn't added to the virtual file system, the full virtual path won't be returned.

 For example, if you have the `data/project/image_1.tga` and want to use the partial virtual path `image_1.tga`, you should get the full virtual path first:
```cpp
// convert partial virtual to full virtual path
string full_virtual_path = engine.FileSystem.resolvePartialVirtualPath("image_1.tga"); // project/image_1.tga is returned
// use the converted path
Image(full_virtual_path);

```


### Arguments

- *string* **path** - Partial path to be resolved.

### Return value

Full virtual path.
## engine.filesystem. getVirtualPath ( )

Resolves a virtual path for the given file path. The following examples show particular cases of the method usage:
- If the given path is known for the virtual file system, the following can be returned: ```cpp string s1, s2, s3; // absolute path to the folder s1 = engine.FileSystem.getVirtualPath("D:/Unigine/data");			// an empty string s2 = engine.FileSystem.getVirtualPath("D:/Unigine/data/");			// an empty string // path to assets in the folder s3 = engine.FileSystem.getVirtualPath("asset://D:/Unigine/data");	// an empty string s4 = engine.FileSystem.getVirtualPath("asset://D:/Unigine/data/");	// an empty string ``` In all cases, an empty string is returned: a virtual path is always returned relative to the data directory, and in the example, the data directory itself is specified. If you specify a known file inside it, the corresponding virtual path will be returned: ```cpp string s = engine.FileSystem.getVirtualPath("D:/Unigine/data/1.tga");	// "1.tga" ```
- If the given path is unknown for the virtual file system, the following can be returned: ```cpp // absolute path to the folder s1 = engine.FileSystem.getVirtualPath("C:/temp");			// "C:/temp" s2 = engine.FileSystem.getVirtualPath("C:/temp/");			// "C:/temp" // path to assets in the folder s3 = engine.FileSystem.getVirtualPath("asset://C:/temp");	// "C:/temp" s4 = engine.FileSystem.getVirtualPath("asset://C:/temp/");	// "C:/temp" ``` In all cases, the normalized path to the folder is returned, as the specified folder is unknown for the virtual file system, and, therefore, no virtual path can be returned. The same is for files, for example: ```cpp s = engine.FileSystem.getVirtualPath("C:/temp/1.tga");		// "C:/temp/1.tga" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index.md#mount_points) file. Here `mount_1` is the `mount_1.umount` mount point. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the virtual path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```cpp // virtual path to the file specified as an absolute one s1 = engine.FileSystem.getVirtualPath("D:/Unigine/data/mounts/mount_1/1.tga");	// "mounts/mount_1/1.tga" // absolute path to the file s2 = engine.FileSystem.getVirtualPath("D:/extern_content/1.tga");				// "mounts/mount_1/1.tga" // full virtual path to the file s3 = engine.FileSystem.getVirtualPath("mounts/mount_1/1.tga");					// "mounts/mount_1/1.tga" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index.md#mount_points) file stored in the nested mount points. Here `mount_1` and `mount_2` are the `mount_1.umount` and `mount_2.umount` mount points correspondingly. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the virtual path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```cpp // virtual path to the file specified as an absolute one s1 = engine.FileSystem.getVirtualPath("D:/Unigine/data/mounts/mount_1/mount_2/1.tga");	// "mounts/mount_1/mount_2/1.tga" // absolute path to the file s2 = engine.FileSystem.getVirtualPath("D:/extern_content_2/1.tga");						// "mounts/mount_1/mount_2/1.tga" // full virtual path to the file s3 = engine.FileSystem.getVirtualPath("mounts/mount_1/mount_2/1.tga");					// "mounts/mount_1/mount_2/1.tga" ```


### Arguments

### Return value

Virtual path to the file relative to the `data` folder.
## engine.filesystem. getVirtualPath ( )

Resolves a virtual path for the given [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

### Return value

Virtual path to the file relative to the `data` folder.
## engine.filesystem. getAbsolutePath ( )

Resolves an absolute path for the given file path. The following examples show particular cases of the method usage:
- If the given path is known for the virtual file system, the following can be returned: ```cpp string s1, s2, s3, s4; // absolute path to the folder s1 = engine.FileSystem.getAbsolutePath("D:/Unigine/data");			// "D:/Unigine/data" s2 = engine.FileSystem.getAbsolutePath("D:/Unigine/data/");			// "D:/Unigine/data" // absolute path to assets in the folder s3 = engine.FileSystem.getAbsolutePath("asset://D:/Unigine/data");	// "D:/Unigine/data" s4 = engine.FileSystem.getAbsolutePath("asset://D:/Unigine/data/");	// "D:/Unigine/data" ```
- If the given path is unknown for the virtual file system, the following can be returned: ```cpp // absolute path to the folder s1 = engine.FileSystem.getAbsolutePath("C:/temp");				// "C:/temp" s2 = engine.FileSystem.getAbsolutePath("C:/temp/");				// "C:/temp" // absolute path to assets in the folder s3 = engine.FileSystem.getAbsolutePath("asset://C:/temp");		// "C:/temp" s4 = engine.FileSystem.getAbsolutePath("asset://C:/temp/");		// "C:/temp" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index.md#mount_points) file. Here `mount_1` is the `mount_1.umount` mount point. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the absolute path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```cpp // virtual path specified as an absolute one s1 = engine.FileSystem.getAbsolutePath("D:/Unigine/data/mounts/mount_1/1.tga");		// "D:/extern_package/1.tga" // absolute path s2 = engine.FileSystem.getAbsolutePath("D:/extern_package/1.tga");					// "D:/extern_package/1.tga" // virtual path s3 = engine.FileSystem.getAbsolutePath("mounts/mount_1/1.tga");						// "D:/extern_package/1.tga" ```
- If the given path is the path to a [mounted](../../../principles/filesystem/index.md#mount_points) file stored in the nested mount points. Here `mount_1` and `mount_2` are the `mount_1.umount` and `mount_2.umount` mount points correspondingly. Note that in the example below, the `1.tga` asset has no runtime files. If an asset has a runtime file, the absolute path to this runtime file (stored in the `.runtimes` folder of the mount point) will be returned. ```cpp // virtual path specified as an absolute one s1 = engine.FileSystem.getAbsolutePath("D:/Unigine/data/mounts/mount_1/mount_2/1.tga");	// "D:/extern_content_2/1.tga" // absolute path s2 = engine.FileSystem.getAbsolutePath("D:/extern_content_2/1.tga");					// "D:/extern_content_2/1.tga" // virtual path s3 = engine.FileSystem.getAbsolutePath("mounts/mount_1/mount_2/1.tga");					// "D:/extern_content_2/1.tga" ```
- If the given path is a network path: ```cpp s1 = engine.FileSystem.getAbsolutePath("//studio/work/shared_content/images.zip");			// "//studio/work/shared_content/images.zip" s2 = engine.FileSystem.getAbsolutePath("\\\\studio\\work\\shared_content\\images.zip");		// "//studio/work/shared_content/images.zip" ```


### Arguments

### Return value

Absolute path to the file.
## engine.filesystem. getAbsolutePath ( )


Resolves an absolute path for the given file [GUID](../../../api/library/filesystem/class.uguid_usc.md).


### Arguments

### Return value

Absolute path to the file.
## engine.filesystem. getExtension ( )

Returns the extension for the given file.
### Arguments

### Return value

File extension in lower case, if any; otherwise, an empty string.
## engine.filesystem. getExtension ( )

Returns the extension for a file with the specified [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

### Return value

File extension in lower case if any; otherwise, an empty string.
## bool engine.filesystem. isFileExist ( )

Checks if the given file actually exists on the disk.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

### Return value

true if the file exists; otherwise, false.
## bool engine.filesystem. isFileExist ( )

Checks if a file with the given [GUID](../../../api/library/filesystem/class.uguid_usc.md) actually exists.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

### Return value

true if the file exists; otherwise, false.
## bool engine.filesystem. isGUIDPath ( string path )

Returns a value indicating if the given path has a valid GUID path format (e.g. "guid://e231e15beff2309b8f87c30b2c105cc4d2399973)".
### Arguments

- *string* **path** - Path to be checked.

### Return value

true if the given path has a valid GUID path format; otherwise, false.
## bool engine.filesystem. isAssetPath ( string path )

Returns a value indicating if the given path has a valid [asset path format](../../../principles/filesystem/index.md#access_path) (e.g. `asset://1.tga`).
### Arguments

- *string* **path** - Path to be checked.

### Return value

true if the given path has a valid asset path format; otherwise, false.
## engine.filesystem. getMTime ( )

Returns the time of the last modification of the given file.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

### Return value

Time of the last file modification. If there is no such file, **-1** will be returned.
## engine.filesystem. getMTime ( )

Returns the time of the last modification of the file with the specified GUID.
> **Notice:** Calling this method every frame in the main thread, especially for multiple files, may cause a performance hit. It is better to optimize such checks and move them to a separate thread.


### Arguments

### Return value

Time of the last file modification. If there is no such file, **-1** will be returned.
## bool engine.filesystem. loadGUIDs ( string path )

Loads file system [GUIDs](../../../api/library/filesystem/class.uguid_usc.md) from the specified file.
### Arguments

- *string* **path** - Path to the file, where file system GUIDs are stored.

### Return value

true if file system GUIDs are loaded successfully; otherwise, false.
## bool engine.filesystem. saveGUIDs ( string path , bool binary = false )

Saves all file system [GUIDs](../../../api/library/filesystem/class.uguid_usc.md) to the specified file in the specified format (json or binary).
### Arguments

- *string* **path** - Path to the file, where file system GUIDs are to be stored.
- *bool* **binary** - Binary file format flag. When the flag is set to true, the file system will save GUIDs to a binary file; otherwise, to a JSON file.

### Return value

true if all file system GUIDs are saved successfully; otherwise, false.
## UGUID engine.filesystem. generateGUID ( )

Generates a new [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Return value

New filesystem GUID if is was generated successfully; otherwise, an empty GUID.
## bool engine.filesystem. setGUID ( string path , UGUID guid )

Sets the specified [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the given file.
### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.
- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - [GUID](../../../api/library/filesystem/class.uguid_usc.md) to be set for the file.

### Return value

true if the [GUID](../../../api/library/filesystem/class.uguid_usc.md) is set successfully; otherwise, false.
## UGUID engine.filesystem. getGUID ( string path )

Returns the [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the specified path if this path is registered in the File System.
> **Notice:** In case you pass a guid-string *(guid://)*, this method will give you back the guid you specified (**without checking whether it is registered in the File System or not**).

### Arguments

- *string* **path** - File path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index.md#paths). > **Notice:** If you want to specify a path to an asset, you should use the asset path format (asset://). Otherwise, if you specify the regular path to the asset, it will be treated as the path to its runtime file (if any) from the `.runtimes` folder.

### Return value

File [GUID](../../../api/library/filesystem/class.uguid_usc.md) this path is registered in the File System; otherwise, an [empty GUID](../../../api/library/filesystem/class.uguid_usc.md#empty).
## String engine.filesystem. getModifier ( int num )

Returns the name of the given modifier.
### Arguments

- *int* **num** - ID number of the modifier.

### Return value

Modifier name.
## void engine.filesystem. addModifier ( string name )

Registers a new modifier in the file system.
### Arguments

- *string* **name** - Modifier name.

## void engine.filesystem. removeModifier ( string name )

Unregisters a given modifier in the file system.
### Arguments

- *string* **name** - Modifier name.

## void engine.filesystem. clearModifiers ( )

Unregister all modifiers in the file system.
## bool engine.filesystem. isPackageLoaded ( string path )

Returns a value indicating if the specified package is loaded in the file system.
### Arguments

- *string* **path** - Package path. It can be a relative, absolute, network, or virtual [path](../../../principles/filesystem/index.md#paths).

### Return value

true if the package is loaded; otherwise, false.
## void engine.filesystem. getPackagesVirtualPaths ( Vector<String>& OUT_packages_virtual_paths )

Returns virtual paths of all packages currently loaded in the file system.
### Arguments

- *Vector<String>&* **OUT_packages_virtual_paths** - An array to store virtual paths of all loaded packages. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
