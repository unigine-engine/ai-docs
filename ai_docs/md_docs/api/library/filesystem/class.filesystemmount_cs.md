# Unigine::FileSystemMount Class (CS)


This class represents a [**mount point**](../../../principles/filesystem/index_cs.md#mount_points) that is used to extend the Engine's [file system](../../../principles/filesystem/index_cs.md). Mount point is a sort of a symlink enabling you to extend the virtual file system of your project by adding any external folders and packages to the **data** directory.


## FileSystemMount Class

### Properties

## 🔒︎ int Access

The mount point access mode, one of the [ACCESS_*](#ACCESS_READONLY) values.
## 🔒︎ string DataPath

The absolute path to the mounted folder/package.
## 🔒︎ string Name

The name of the mount point.
## 🔒︎ string UMountPath

The absolute path to the `*.umount` file.
## 🔒︎ string VirtualPath

The [virtual path](../../../principles/filesystem/index_cs.md#virtual_paths) to the folder to which the contents of the external folder/package is mounted.
### Members

---

## void SetExclusiveFilters ( string[] OUT_filters )

Sets the list of exclusive filters (exceptions from the ignore list specified by *[SetIgnoreFilters()](../../...md#setIgnoreFilters_VECString_void)*) to be used to include only specific files when mounting. The filters are defined as wildcard masks (e.g., *"*.jpg", "some_folder_*/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and allow restricting the visible file set to those matching the specified patterns.
> **Notice:** A **trailing slash** ('/') is required at the end of **directory wildcards** !

### Arguments

- *string[]* **OUT_filters** - List of wildcards to be used to filter files in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void GetExclusiveFilters ( string[] OUT_filters )

Returns the list of exclusive filters (exceptions from the ignore list specified by *[SetIgnoreFilters()](../../...md#setIgnoreFilters_VECString_void)*) used to include only specific files when mounting. The filters are defined as wildcard masks (e.g., *"*.jpg", "some_folder_*/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and allow restricting the visible file set to those matching the specified patterns.
### Arguments

- *string[]* **OUT_filters** - List of wildcards currently used to filter files in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## string[] GetExclusiveFilters ( )

Returns the list of exclusive filters (exceptions from the ignore list specified by *[SetIgnoreFilters()](../../...md#setIgnoreFilters_VECString_void)*) used to include only specific files when mounting. The filters are defined as wildcard masks (e.g., *"*.jpg", "some_folder_*/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and allow restricting the visible file set to those matching the specified patterns.
## void SetIgnoreFilters ( string[] OUT_filters )

Sets the list of ignore filters (blacklist) to be used to exclude certain files or directories from being stored in the GUIDs database. The filters are defined as wildcard masks **with full support for standard wildcard patterns** (e.g., *"*.tmp", "cache_*/", "**/.git/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and help prevent unnecessary files from being tracked or assigned GUIDs.
> **Notice:** A **trailing slash** ('/') is required at the end of **directory wildcards** !

### Arguments

- *string[]* **OUT_filters** - List of wildcards to be used to filter out files to be ignored in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void GetIgnoreFilters ( string[] OUT_filters )

Returns the list of ignore filters (blacklist) used to exclude certain files or directories from being stored in the GUIDs database. The filters are defined as wildcard masks **with full support for standard wildcard patterns** (e.g., *"*.tmp", "cache_*/", "**/.git/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and help prevent unnecessary files from being tracked or assigned GUIDs.
### Arguments

- *string[]* **OUT_filters** - List of wildcards currently used to filter out files to be ignored in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## string[] GetIgnoreFilters ( )

Returns the list of ignore filters (blacklist) used to exclude certain files or directories from being stored in the GUIDs database. The filters are defined as wildcard masks **with full support for standard wildcard patterns** (e.g., *"*.tmp", "cache_*/", "**/.git/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and help prevent unnecessary files from being tracked or assigned GUIDs.
## void GetVirtualFiles ( string[] OUT_files )

Returns the list of [virtual paths](../../../principles/filesystem/index_cs.md#virtual_paths) to all files in the mounted folder/package.
> **Notice:** Contents of nested mount points inside the mounted folder will not be included in the list.


### Arguments

- *string[]* **OUT_files** - Output vector to store the list of files stored in the mounted folder/package. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## bool IsPathFilteredOut ( string path )

Returns a value indicating whether the specified path is filtered out by the [ignore](#getIgnoreFilters_VECString_void) and [exclusive](#getExclusiveFilters_VECString_void) filters.
### Arguments

- *string* **path** - Any file path.

### Return value

true if the specified path is filtered out after applying ignore and exclusive filters if any; otherwise, false.
## void SetGuidsDBIgnoreFilters ( string[] filters )

Sets the list of [GUIDs database](../../../principles/filesystem/index_cs.md#guids) (`guids.db`) ignore filters (blacklist) to be used to exclude certain files or directories from being stored in the GUIDs database. The filters are defined as wildcard masks **with full support for standard wildcard patterns** (e.g., *"*.tmp", "cache_*/", "**/.git/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and help prevent unnecessary or temporary files from being tracked or assigned GUIDs, keeping your `guids.db` file organized and relevant, without unnecessary bloating.
> **Notice:** A **trailing slash** ('/') is required at the end of **directory wildcards** !

### Arguments

- *string[]* **filters** - List of wildcards to be used to exclude files or directories from the GUIDs database.

## void GetGuidsDBIgnoreFilters ( string[] OUT_filters )

Returns the list of [GUIDs database](../../../principles/filesystem/index_cs.md#guids) (`guids.db`) ignore filters (blacklist) used to exclude certain files or directories from being stored in the GUIDs database. The filters are defined as wildcard masks **with full support for standard wildcard patterns** (e.g., *"*.tmp", "cache_*/", "**/.git/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and help prevent unnecessary or temporary files from being tracked or assigned GUIDs, keeping your `guids.db` file organized and relevant, without unnecessary bloating.
### Arguments

- *string[]* **OUT_filters** - Output list of wildcards currently used to exclude files or directories from the GUIDs database. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## string[] GetGuidsDBIgnoreFilters ( )

Returns the list of [GUIDs database](../../../principles/filesystem/index_cs.md#guids) (`guids.db`) ignore filters (blacklist) used to exclude certain files or directories from being stored in the GUIDs database. The filters are defined as wildcard masks **with full support for standard wildcard patterns** (e.g., *"*.tmp", "cache_*/", "**/.git/"*, etc. - [read more about wildcards](../../../principles/filesystem/wildcards.md)), and help prevent unnecessary or temporary files from being tracked or assigned GUIDs, keeping your `guids.db` file organized and relevant, without unnecessary bloating.
