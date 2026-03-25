# Unigine::FileSystemAssets Class (CPP)

**Header:** #include <UnigineFileSystem.h>

> **Notice:** This class is a singleton.


This class represents the subsystem of the Engine's [file system](../../../principles/filesystem/index_cpp.md) that is used to manage [assets and runtime files](../../../editor2/assets_workflow/assets_runtimes.md).


> **Notice:** This class is in the **Unigine** namespace.


You can use `assets_info`and `assets_list`console commands to view information on non-native assets and runtimes generated for them.


## FileSystemAssets Class

### Members

---

## bool isAsset ( const UGUID & any_guid )

Returns a value indicating whether the file with the specified GUID is a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (has [runtime files](../../../principles/filesystem/index_cpp.md#assets_runtimes) generated for it).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file with the specified GUID is a non-native asset; otherwise, false.
## bool isAsset ( const char * path )

Returns a value indicating whether the file with the specified path is a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (has [runtime files](../../../principles/filesystem/index_cpp.md#assets_runtimes) generated for it).
### Arguments

- *const char ** **path** - Path to a file.

### Return value

true if the file with the specified path is a non-native asset; otherwise, false.
## UGUID getAssetGUID ( const char * path )

Returns a GUID of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (having generated runtime file or files) for the specified path.
### Arguments

- *const char ** **path** - Path to a runtime or asset file.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a non-native asset corresponding to the specified path if it exists; otherwise, empty GUID.
> **Notice:** This method will return an empty GUID for any asset having no runtimes generated for it.


## UGUID getAssetGUID ( const UGUID & any_guid )

Returns a GUID of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (having generated runtime file or files) for the specified GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a non-native asset corresponding to the specified path if it exists; otherwise, empty GUID.
> **Notice:** This method will return an empty GUID for any asset having no runtimes generated for it.


## int getNumRuntimes ( const char * asset_path )

Returns a number of [runtime files](../../../editor2/assets_workflow/assets_runtimes.md) for a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) having the specified path.
### Arguments

- *const char ** **asset_path** - Path to an asset file.

### Return value

Number of runtime files generated for the specified asset.
## int getNumRuntimes ( const UGUID & asset_path )

Returns a number of [runtime files](../../../editor2/assets_workflow/assets_runtimes.md) for a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) having the specified GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_path** - Asset file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Number of runtime files generated for the specified asset.
## bool isPrimary ( const char * path )

Returns a value indicating whether the runtime file corresponding to the specified path is a [primary](../../../principles/filesystem/index_cpp.md#primary_runtime) one.
### Arguments

- *const char ** **path** - Path to a runtime file.

### Return value

true if the runtime file corresponding to the specified path is a primary one; otherwise, false.
## bool isPrimary ( const UGUID & any_guid )

Returns a value indicating whether the runtime file corresponding to the specified GUID is a [primary](../../../principles/filesystem/index_cpp.md#primary_runtime) one.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **any_guid** - Runtime file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the runtime file corresponding to the specified GUID is a primary one; otherwise, false.
## UGUID getPrimaryGUID ( const UGUID & any_guid )

Returns the GUID of the [primary runtime file](../../../principles/filesystem/index_cpp.md#primary_runtime) for the specified file GUID if it exists.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Return value is determined by the specified GUID in accordance with the following:
- Asset file GUID -> GUID of its primary runtime file, if any; otherwise empty GUID.
- Primary runtime file GUID -> GUID of this primary runtime file.
- Runtime file GUID -> GUID of the primary runtime file for its asset, if any; otherwise empty GUID.
- Any other file GUID -> empty GUID.


## UGUID getPrimaryGUID ( const char * path )

Returns the GUID of the [primary runtime file](../../../principles/filesystem/index_cpp.md#primary_runtime) for the specified file path if it exists.
### Arguments

- *const char ** **path** - Any file path.

### Return value

Return value is determined by the specified GUID in accordance with the following:
- Asset file path -> GUID of its primary runtime file, if any; otherwise empty GUID.
- Primary runtime file path -> GUID of this primary runtime file.
- Runtime file path -> GUID of the primary runtime file for its asset, if any; otherwise empty GUID.
- Any other file path -> empty GUID.


## bool isMeta ( const UGUID & any_guid )

Returns a value indicating whether the file with the specified GUID is a [`*.meta`](../../../editor2/assets_workflow/assets_runtimes.md) file.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file with the specified GUID is a `*.meta` file; otherwise, false.
## bool isRuntime ( const char * path )

Returns a value indicating whether the file corresponding to the specified path is a generated [runtime file](../../../principles/filesystem/index_cpp.md#assets_runtimes).
### Arguments

- *const char ** **path** - Any file path.

### Return value

true if the file corresponding to the specified path is a generated runtime file; otherwise, false.
> **Notice:** This method will return 0 for any [native asset](../../../editor2/assets_workflow/assets_runtimes.md).


## bool isRuntime ( const UGUID & any_guid )

Returns a value indicating whether the file corresponding to the specified GUID is a generated [runtime file](../../../principles/filesystem/index_cpp.md#assets_runtimes).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

true if the file corresponding to the specified path is a generated runtime file; otherwise, false.
> **Notice:** This method will return 0 for any [native asset](../../../editor2/assets_workflow/assets_runtimes.md).


## bool isRuntimePath ( const char * path )

Returns a value indicating whether the specified path is a path to a generated runtime file.
### Arguments

- *const char ** **path** - Any file path.

### Return value

true if the specified path is a path to a generated runtime file; otherwise, false.
## String getRuntimeAlias ( const char * runtime_path )

Returns the [alias](../../../principles/filesystem/index_cpp.md#alias) of the generated runtime file, specified by the given path.
### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index_cpp.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## String getRuntimeAlias ( const UGUID & runtime_guid )

Returns the [alias](../../../principles/filesystem/index_cpp.md#alias) of the generated runtime file, specified by the given GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index_cpp.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## String getRuntimeAlias ( String asset_path , int index )

Returns the [alias](../../../principles/filesystem/index_cpp.md#alias) of the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *[String](../../../api/library/common/class.string_cpp.md)* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index_cpp.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## String getRuntimeAlias ( const UGUID & asset_guid , int index )

Returns the [alias](../../../principles/filesystem/index_cpp.md#alias) of the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index_cpp.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## bool setRuntimeGUID ( const char * runtime_path , const UGUID & new_runtime_guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the generated runtime file with a given path.
### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - New GUID to be set.

### Return value

true if a new GUID is successfully set; otherwise, false.
## bool setRuntimeGUID ( const UGUID & runtime_guid , const UGUID & new_runtime_guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the generated runtime file with a given GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - New GUID to be set.

### Return value

true if a new GUID is successfully set; otherwise, false.
## bool setRuntimeGUID ( const char * asset_path , int index , const UGUID & new_runtime_guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *const char ** **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - New GUID to be set.

### Return value

true if a new GUID is successfully set; otherwise, false.
## bool setRuntimeGUID ( const UGUID & asset_guid , int index , const UGUID & new_runtime_guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - New GUID to be set.

### Return value

true if a new GUID is successfully set; otherwise, false.
## UGUID getRuntimeGUID ( const char * asset_path , int index )

Returns the current [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *const char ** **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.

### Return value

Current generated runtime file [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the given asset and runtime index, if any; otherwise, empty GUID.
## UGUID getRuntimeGUID ( const UGUID & asset_guid , int index )

Returns the current [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.

### Return value

Current generated runtime file [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the given asset and runtime index, if any; otherwise, empty GUID.
## UGUID addRuntime ( const char * asset_path , const char * alias , int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index_cpp.md#assets_runtimes) for the asset with a given path. A new GUID will be generated for the new runtime file.
### Arguments

- *const char ** **asset_path** - Path to the asset for which a new runtime is to be created.
- *const char ** **alias** - [Alias](../../../principles/filesystem/index_cpp.md#alias) for the new runtime file.
- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new created runtime, if it was successfully created, or an empty GUID, otherwise.
## UGUID addRuntime ( const UGUID & asset_guid , const char * alias , int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index_cpp.md#assets_runtimes) for the asset with a given GUID. A new GUID will be generated for the new runtime file.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a new runtime is to be created.
- *const char ** **alias** - [Alias](../../../principles/filesystem/index_cpp.md#alias) for the new runtime file.
- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new created runtime, if it was successfully created, or an empty GUID, otherwise.
## bool addRuntime ( const char * asset_path , const char * alias , const UGUID & runtime_guid , int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index_cpp.md#assets_runtimes) for the asset with a given path. The specified GUID will be assigned to the new runtime file.
### Arguments

- *const char ** **asset_path** - Path to the asset for which a new runtime is to be created.
- *const char ** **alias** - [Alias](../../../principles/filesystem/index_cpp.md#alias) for the new runtime file.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the new runtime file.
- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

true if a new runtime file is successfully created; otherwise, false.
## bool addRuntime ( const UGUID & asset_guid , const char * alias , const UGUID & runtime_guid , int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index_cpp.md#assets_runtimes) for the asset with a given GUID. The specified GUID will be assigned to the new runtime file.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a new runtime is to be created.
- *const char ** **alias** - [Alias](../../../principles/filesystem/index_cpp.md#alias) for the new runtime file.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) for the new runtime file.
- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

true if a new runtime file is successfully created; otherwise, false.
## bool clearRuntimes ( const char * asset_path )

Deletes all generated [runtime files](../../../principles/filesystem/index_cpp.md#assets_runtimes) for the asset with the specified path.
### Arguments

- *const char ** **asset_path** - Path to the asset for which all generated runtime files are to be deleted.

### Return value

true if all generated runtime files for the specified asset are successfully deleted; otherwise, false.
## bool clearRuntimes ( const UGUID & asset_guid )

Deletes all generated [runtime files](../../../principles/filesystem/index_cpp.md#assets_runtimes) for the asset with the specified GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which all generated runtime files are to be deleted.

### Return value

true if all generated runtime files for the specified asset are successfully deleted; otherwise, false.
## UGUID copyRuntime ( const char * runtime_path , const char * new_asset_path )

Adds a copy of the generated runtime file with the specified path to another asset with the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file to be copied.
- *const char ** **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( const char * runtime_path , const UGUID & new_asset_guid )

Adds a copy of the generated runtime file with the specified path to another asset having the specified GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file to be copied.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( const UGUID & runtime_guid , const char * new_asset_path )

Adds a copy of the generated runtime file with the specified path to another asset having the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file to be copied.
- *const char ** **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( const UGUID & runtime_guid , const UGUID & new_asset_guid )

Adds a copy of the generated runtime file with the specified GUID to another asset specified by GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file to be copied.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( const char * asset_path , int index , const char * new_asset_path )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *const char ** **asset_path** - Path to the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( const char * asset_path , int index , const UGUID & new_asset_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *const char ** **asset_path** - Path to the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( const UGUID & asset_guid , int index , const char * new_asset_path )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).
- *const char ** **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( const UGUID & asset_guid , int index , const UGUID & new_asset_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## bool copyRuntime ( const char * runtime_path , const char * new_asset_path , const UGUID & new_runtime_guid )

Adds a copy of the generated runtime file specified by path, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file to be copied.
- *const char ** **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( const char * runtime_path , const UGUID & new_asset_guid , const UGUID & new_runtime_guid )

Adds a copy of the generated runtime file specified by path, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file to be copied.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a copy of the generated runtime file is to be added.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( const UGUID & runtime_guid , const char * new_asset_path , const UGUID & new_runtime_guid )

Adds a copy of the generated runtime file specified by GUID, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset file to which the generated runtime file to be copied belongs.
- *const char ** **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( const UGUID & runtime_guid , const UGUID & new_asset_guid , const UGUID & new_runtime_guid )

Adds a copy of the generated runtime file specified by GUID, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file to be copied.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a copy of the generated runtime file is to be added.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( const char * asset_path , int index , const char * new_asset_path , const UGUID & new_runtime_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *const char ** **asset_path** - Path to the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( const char * asset_path , int index , const UGUID & new_asset_guid , const UGUID & new_runtime_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *const char ** **asset_path** - Path to the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a copy of the generated runtime file is to be added.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( const UGUID & asset_guid , int index , const char * new_asset_path , const UGUID & new_runtime_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).
- *const char ** **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( const UGUID & asset_guid , int index , const UGUID & new_asset_guid , const UGUID & new_runtime_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset for which a copy of the generated runtime file is to be added.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool removeRuntime ( const char * runtime_path )

Deletes the specified generated runtime file and removes it from the list of runtimes of the corresponding asset.
### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file to be deleted.

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## bool removeRuntime ( const UGUID & runtime_guid )

Deletes the specified generated runtime file and removes it from the list of runtimes of the corresponding asset.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file to be deleted.

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## bool removeRuntime ( const char * asset_path , int index )

Deletes the generated runtime file with the specified index, and removes it from the list of runtimes of the asset specified by path.
### Arguments

- *const char ** **asset_path** - Path to the asset file for which the specified generated runtime file is to be deleted.
- *int* **index** - Index of the generated runtime file to be deleted in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## bool removeRuntime ( const UGUID & asset_guid , int index )

Deletes the generated runtime file with the specified index, and removes it from the list of runtimes of the asset specified by GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset file for which the specified generated runtime file is to be deleted.
- *int* **index** - Index of the generated runtime file to be deleted in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## UGUID resolve ( const UGUID & any_guid )

Resolves a given GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Return GUID value is determined by the GUID specified in accordance with the following:
- [Non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) file GUID -> GUID of its primary runtime file, if any; otherwise, asset file GUID.
- Any other file GUID -> file GUID as is.


```cpp
// if there is a primary runtime generated
resolve(asset_guid);		//	-> primary_guid
resolve(primary_guid);		//	-> primary_guid
resolve(runtime_guid);		//	-> runtime_guid

// if there is no primary runtime generated
resolve(asset_guid);		//	-> asset_guid
resolve(primary_guid);		//	-> primary_guid
resolve(runtime_guid);		//	-> runtime_guid

```


## UGUID resolveAsset ( const UGUID & any_guid )

Resolves a given GUID to a corresponding asset GUID, if any, or keeps the specified GUID as is.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Return GUID value is determined by the GUID specified in accordance with the following:
- [Primary runtime file](../../../principles/filesystem/index_cpp.md#primary_runtime) GUID -> source asset file GUID.
- Generated runtime file GUID -> source asset file GUID.
- [Non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) file GUID -> GUID as is.
- Any other file GUID -> GUID as is.


```cpp
resolveAsset(asset_guid);		//	-> asset_guid
resolveAsset(primary_guid);		//	-> asset_guid
resolveAsset(runtime_guid);		//	-> asset_guid

```


## UGUID resolvePrimary ( const UGUID & any_guid )

Resolves a given GUID to a corresponding primary runtime GUID, if any.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

### Return value

Return GUID value is determined by the GUID specified in accordance with the following:
- Any generated runtime file GUID -> GUID of the primary runtime file for the source asset.
- [Non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) file GUID -> GUID of its primary runtime file, if any; otherwise, empty GUID.
- Any other file GUID -> empty GUID.


```cpp
// if there is a primary runtime generated
resolvePrimary(asset_guid);		//	-> primary_guid
resolvePrimary(primary_guid);	//	-> primary_guid
resolvePrimary(runtime_guid);	//	-> primary_guid

// if there is no primary runtime generated
resolvePrimary(asset_guid);			//	-> empty guid
resolvePrimary(runtime_guid);		//	-> empty guid

```


## UGUID resolveRuntimeAlias ( const char * path )

Resolves a given [alias](../../../principles/filesystem/index_cpp.md#alias) of a generated runtime file to a corresponding GUID, if any.
### Arguments

- *const char ** **path** - Runtime file [alias](../../../principles/filesystem/index_cpp.md#alias).

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file having the specified alias, af any; otherwise, empty GUID
## bool setRuntimeAlias ( const UGUID & asset_guid , int index , const char * new_alias )

Sets a new [alias](../../../principles/filesystem/index_cpp.md#alias) for the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *const char ** **new_alias** - New alias to be set.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool setRuntimeAlias ( const UGUID & runtime_guid , const char * new_alias )

Sets a new [alias](../../../principles/filesystem/index_cpp.md#alias) for the generated runtime file with a given GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file.
- *const char ** **new_alias** - New alias to be set.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool setRuntimeAlias ( const char * runtime_path , const char * new_alias )

Sets a new [alias](../../../principles/filesystem/index_cpp.md#alias) for the generated runtime file with a given path.
### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file.
- *const char ** **new_alias** - New alias to be set.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool setRuntimeAlias ( const char * asset_path , int index , const char * new_alias )

Sets a new [alias](../../../principles/filesystem/index_cpp.md#alias) for the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *const char ** **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *const char ** **new_alias** - New alias to be set.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool setRuntimePrimary ( const char * asset_path , int index , int primary )

Sets or unsets the generated runtime file, specified by the given non-native asset path and runtime index, as a [primary](../../../principles/filesystem/index_cpp.md#primary_runtime) one.
### Arguments

- *const char ** **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool setRuntimePrimary ( const char * runtime_path , int primary )

Sets or unsets the generated runtime file with a given path as a [primary](../../../principles/filesystem/index_cpp.md#primary_runtime) one.
### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool setRuntimePrimary ( const UGUID & runtime_guid , int primary )

Sets or unsets the generated runtime file with a given GUID as a [primary](../../../principles/filesystem/index_cpp.md#primary_runtime) one.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool setRuntimePrimary ( const UGUID & asset_guid , int index , int primary )

Sets or unsets the generated runtime file, specified by the given non-native asset GUID and runtime index, as a [primary](../../../principles/filesystem/index_cpp.md#primary_runtime) one.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool setRuntimeParameter ( const UGUID & asset_guid , int index , const char * parameter_name , const char * new_parameter_value )

Sets a new parameter with a given name and value for the generated runtime file specified by the non-native asset GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **parameter_name** - Name of the parameter to be set.
- *const char ** **new_parameter_value** - Value of the parameter to be set.

### Return value

true if a new parameter for the runtime is successfully set; otherwise, false.
## bool setRuntimeParameter ( const char * asset_path , int index , const char * parameter_name , const char * new_parameter_value )

Sets a new parameter with a given name and value for the generated runtime file specified by the given non-native asset path.
### Arguments

- *const char ** **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **parameter_name** - Name of the parameter to be set.
- *const char ** **new_parameter_value** - Value of the parameter to be set.

### Return value

true if a new parameter for the runtime is successfully set; otherwise, false.
## bool setRuntimeParameter ( const UGUID & runtime_guid , const char * parameter_name , const char * new_parameter_value )

Sets a new parameter with a given name and value for the generated runtime file with a given GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file.
- *const char ** **parameter_name** - Name of the parameter to be set.
- *const char ** **new_parameter_value** - Value of the parameter to be set.

### Return value

true if a new parameter for the runtime is successfully set; otherwise, false.
## bool setRuntimeParameter ( const char * runtime_path , const char * parameter_name , const char * new_parameter_value )

Sets a new parameter with a given name and value for the generated runtime file with the specified path.
### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file.
- *const char ** **parameter_name** - Name of the parameter to be set.
- *const char ** **new_parameter_value** - Value of the parameter to be set.

### Return value

true if a new parameter for the runtime is successfully set; otherwise, false.
## String getRuntimeParameter ( const UGUID & asset_guid , int index , const char * parameter_name ) const

Returns the value of the specified parameter of the specified runtime file, or an empty string if such parameter does not exist.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset file for the runtime file of which the parameter is returned.
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **parameter_name** - Name of the parameter to be returned.

### Return value

Value of the specified parameter, or an empty string if such parameter does not exist.
## String getRuntimeParameter ( const char * asset_path , int index , const char * parameter_name ) const

Returns the value of the specified parameter of the specified runtime file, or an empty string if such parameter does not exist.
### Arguments

- *const char ** **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **parameter_name** - Name of the parameter to be returned.

### Return value

Value of the specified parameter, or an empty string if such parameter does not exist.
## String getRuntimeParameter ( const UGUID & runtime_guid , const char * parameter_name ) const

Returns the value of the specified parameter of the specified runtime file, or an empty string if such parameter does not exist.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file.
- *const char ** **parameter_name** - Name of the parameter to be returned.

### Return value

Value of the specified parameter, or an empty string if such parameter does not exist.
## String getRuntimeParameter ( const char * runtime_path , const char * parameter_name ) const

Returns the value of the specified parameter of the specified runtime file, or an empty string if such parameter does not exist.
### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file.
- *const char ** **parameter_name** - Name of the parameter to be returned.

### Return value

Value of the specified parameter, or an empty string if such parameter does not exist.
## bool hasRuntimeParameter ( const UGUID & asset_guid , int index , const char * parameter_name ) const

Checks if the specified runtime file has the specified parameter.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset file for the runtime file of which the parameter is checked.
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **parameter_name** - Name of the parameter to be checked.

### Return value

true if the runtime file has the specified parameter; otherwise, false.
## bool hasRuntimeParameter ( const char * asset_path , int index , const char * parameter_name ) const

Checks if the specified runtime file has the specified parameter.
### Arguments

- *const char ** **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **parameter_name** - Name of the parameter to be checked.

### Return value

true if the runtime file has the specified parameter; otherwise, false.
## bool hasRuntimeParameter ( const UGUID & runtime_guid , const char * parameter_name ) const

Checks if the specified runtime file has the specified parameter.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file.
- *const char ** **parameter_name** - Name of the parameter to be checked.

### Return value

true if the runtime file has the specified parameter; otherwise, false.
## bool hasRuntimeParameter ( const char * runtime_path , const char * parameter_name ) const

Checks if the specified runtime file has the specified parameter.
### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file.
- *const char ** **parameter_name** - Name of the parameter to be checked.

### Return value

true if the runtime file has the specified parameter; otherwise, false.
## bool removeRuntimeParameter ( const UGUID & asset_guid , int index , const char * parameter_name ) const

Removes the specified parameter of the runtime file of the asset with the specified GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the asset file for the runtime file of which the parameter is removed.
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **parameter_name** - Name of the parameter to be removed.

### Return value

true if the specified parameter of the runtime file is successfully deleted; false if such parameter does not exist.
## bool removeRuntimeParameter ( const char * asset_path , int index , const char * parameter_name ) const

Removes the specified parameter of the runtime file of the asset with the specified path.
### Arguments

- *const char ** **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *const char ** **parameter_name** - Name of the parameter to be removed.

### Return value

true if the specified parameter of the runtime file is successfully deleted; false if such parameter does not exist.
## bool removeRuntimeParameter ( const UGUID & runtime_guid , const char * parameter_name ) const

Removes the specified parameter of the runtime file with the specified GUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the generated runtime file.
- *const char ** **parameter_name** - Name of the parameter to be removed.

### Return value

true if the specified parameter of the runtime file is successfully deleted; false if such parameter does not exist.
## bool removeRuntimeParameter ( const char * runtime_path , const char * parameter_name ) const

Removes the specified parameter of the runtime file with the specified path.
### Arguments

- *const char ** **runtime_path** - Path to the generated runtime file.
- *const char ** **parameter_name** - Name of the parameter to be removed.

### Return value

true if the specified parameter of the runtime file is successfully deleted; false if such parameter does not exist.
