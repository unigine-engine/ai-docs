# Unigine::FileSystemMount Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents a [**mount point**](../../../principles/filesystem/index.md#mount_points) that is used to extend the Engine's [file system](../../../principles/filesystem/index.md). Mount point is a sort of a symlink enabling you to extend the virtual file system of your project by adding any external folders and packages to the **data** directory.


## FileSystemMount Class

### Members

## int getAccess () const

Returns the current mount point access mode, one of the [ACCESS_*](#ACCESS_READONLY) values.
### Return value

Current mount point access mode.
## const char * getDataPath () const

Returns the current absolute path to the mounted folder/package.
### Return value

Current absolute path to the mounted folder/package.
## const char * getName () const

Returns the current name of the mount point.
### Return value

Current name of the mount point.
## const char * getUMountPath () const

Returns the current absolute path to the `*.umount` file.
### Return value

Current absolute path to the `*.umount` file.
## const char * getVirtualPath () const

Returns the current [virtual path](../../../principles/filesystem/index.md#virtual_paths) to the folder to which the contents of the external folder/package is mounted.
### Return value

Current virtual path to the folder.
---

## void setExclusiveFilters ( Vector<String>& OUT_filters )

Sets the list of exclusive filters (exceptions from the ignore list specified by *[setIgnoreFilters()()](../../...md#setIgnoreFilters_VECString_void)*) to be used to include only specific files when mounting. The filters are defined as wildcard masks (e.g., *"*.jpg", "some_folder_*/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and allow restricting the visible file set to those matching the specified patterns.
> **Notice:** A **trailing slash** ('/') is required at the end of **directory wildcards** !

### Arguments

- *Vector<String>&* **OUT_filters** - List of wildcards to be used to filter files in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void getExclusiveFilters ( Vector<String>& OUT_filters )

Returns the list of exclusive filters (exceptions from the ignore list specified by *[setIgnoreFilters()()](../../...md#setIgnoreFilters_VECString_void)*) used to include only specific files when mounting. The filters are defined as wildcard masks (e.g., *"*.jpg", "some_folder_*/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and allow restricting the visible file set to those matching the specified patterns.
### Arguments

- *Vector<String>&* **OUT_filters** - List of wildcards currently used to filter files in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setIgnoreFilters ( Vector<String>& OUT_filters )

Sets the list of ignore filters (blacklist) to be used to exclude certain files or directories from being stored in the GUIDs database. The filters are defined as wildcard masks **with full support for standard wildcard patterns** (e.g., *"*.tmp", "cache_*/", "**/.git/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and help prevent unnecessary files from being tracked or assigned GUIDs.
> **Notice:** A **trailing slash** ('/') is required at the end of **directory wildcards** !

### Arguments

- *Vector<String>&* **OUT_filters** - List of wildcards to be used to filter out files to be ignored in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void getIgnoreFilters ( Vector<String>& OUT_filters )

Returns the list of ignore filters (blacklist) used to exclude certain files or directories from being stored in the GUIDs database. The filters are defined as wildcard masks **with full support for standard wildcard patterns** (e.g., *"*.tmp", "cache_*/", "**/.git/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and help prevent unnecessary files from being tracked or assigned GUIDs.
### Arguments

- *Vector<String>&* **OUT_filters** - List of wildcards currently used to filter out files to be ignored in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void getVirtualFiles ( Vector<String>& OUT_files )

Returns the list of [virtual paths](../../../principles/filesystem/index.md#virtual_paths) to all files in the mounted folder/package.
> **Notice:** Contents of nested mount points inside the mounted folder will not be included in the list.


### Arguments

- *Vector<String>&* **OUT_files** - Output vector to store the list of files stored in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool isPathFilteredOut ( string path )

Returns a value indicating whether the specified path is filtered out by the [ignore](#getIgnoreFilters_VECString_void) and [exclusive](#getExclusiveFilters_VECString_void) filters.
### Arguments

- *string* **path** - Any file path.

### Return value

true if the specified path is filtered out after applying ignore and exclusive filters if any; otherwise, false.
## void getGuidsDBIgnoreFilters ( Vector<String>& OUT_filters )

Returns the list of [GUIDs database](../../../principles/filesystem/index.md#guids) (`guids.db`) ignore filters (blacklist) used to exclude certain files or directories from being stored in the GUIDs database. The filters are defined as wildcard masks **with full support for standard wildcard patterns** (e.g., *"*.tmp", "cache_*/", "**/.git/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and help prevent unnecessary or temporary files from being tracked or assigned GUIDs, keeping your `guids.db` file organized and relevant, without unnecessary bloating.
### Arguments

- *Vector<String>&* **OUT_filters** - Output list of wildcards currently used to exclude files or directories from the GUIDs database. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
