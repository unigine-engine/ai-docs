# Unigine::FileSystemAssets Class (CS)

> **Notice:** This class is a singleton.


This class represents the subsystem of the Engine's [file system](../../../principles/filesystem/index_cs.md) that is used to manage [assets and runtime files](../../../editor2/assets_workflow/assets_runtimes.md).


> **Notice:** This class is in the **Unigine** namespace.


You can use `assets_info`and `assets_list`console commands to view information on non-native assets and runtimes generated for them.


## FileSystemAssets Class

### Members

---

## bool IsAsset ( UGUID any_guid )

Returns a value indicating whether the file with the specified GUID is a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (has [runtime files](../../../principles/filesystem/index_cs.md#assets_runtimes) generated for it).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file with the specified GUID is a non-native asset; otherwise, false.
## bool IsAsset ( string path )

Returns a value indicating whether the file with the specified path is a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (has [runtime files](../../../principles/filesystem/index_cs.md#assets_runtimes) generated for it).
### Arguments

- *string* **path** - Path to a file.

### Return value

true if the file with the specified path is a non-native asset; otherwise, false.
## UGUID GetAssetGUID ( string path )

Returns a GUID of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (having generated runtime file or files) for the specified path.
### Arguments

- *string* **path** - Path to a runtime or asset file.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of a non-native asset corresponding to the specified path if it exists; otherwise, empty GUID.
> **Notice:** This method will return an empty GUID for any asset having no runtimes generated for it.


## UGUID GetAssetGUID ( UGUID any_guid )

Returns a GUID of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (having generated runtime file or files) for the specified GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of a non-native asset corresponding to the specified path if it exists; otherwise, empty GUID.
> **Notice:** This method will return an empty GUID for any asset having no runtimes generated for it.


## int GetNumRuntimes ( string asset_path )

Returns a number of [runtime files](../../../editor2/assets_workflow/assets_runtimes.md) for a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) having the specified path.
### Arguments

- *string* **asset_path** - Path to an asset file.

### Return value

Number of runtime files generated for the specified asset.
## int GetNumRuntimes ( UGUID asset_path )

Returns a number of [runtime files](../../../editor2/assets_workflow/assets_runtimes.md) for a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) having the specified GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_path** - Asset file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Number of runtime files generated for the specified asset.
## bool IsPrimary ( string path )

Returns a value indicating whether the runtime file corresponding to the specified path is a [primary](../../../principles/filesystem/index_cs.md#primary_runtime) one.
### Arguments

- *string* **path** - Path to a runtime file.

### Return value

true if the runtime file corresponding to the specified path is a primary one; otherwise, false.
## bool IsPrimary ( UGUID any_guid )

Returns a value indicating whether the runtime file corresponding to the specified GUID is a [primary](../../../principles/filesystem/index_cs.md#primary_runtime) one.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **any_guid** - Runtime file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the runtime file corresponding to the specified GUID is a primary one; otherwise, false.
## UGUID GetPrimaryGUID ( UGUID any_guid )

Returns the GUID of the [primary runtime file](../../../principles/filesystem/index_cs.md#primary_runtime) for the specified file GUID if it exists.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Return value is determined by the specified GUID in accordance with the following:
- Asset file GUID -> GUID of its primary runtime file, if any; otherwise empty GUID.
- Primary runtime file GUID -> GUID of this primary runtime file.
- Runtime file GUID -> GUID of the primary runtime file for its asset, if any; otherwise empty GUID.
- Any other file GUID -> empty GUID.


## UGUID GetPrimaryGUID ( string path )

Returns the GUID of the [primary runtime file](../../../principles/filesystem/index_cs.md#primary_runtime) for the specified file path if it exists.
### Arguments

- *string* **path** - Any file path.

### Return value

Return value is determined by the specified GUID in accordance with the following:
- Asset file path -> GUID of its primary runtime file, if any; otherwise empty GUID.
- Primary runtime file path -> GUID of this primary runtime file.
- Runtime file path -> GUID of the primary runtime file for its asset, if any; otherwise empty GUID.
- Any other file path -> empty GUID.


## bool IsMeta ( UGUID any_guid )

Returns a value indicating whether the file with the specified GUID is a [`*.meta`](../../../editor2/assets_workflow/assets_runtimes.md) file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file with the specified GUID is a `*.meta` file; otherwise, false.
## bool IsRuntime ( string path )

Returns a value indicating whether the file corresponding to the specified path is a generated [runtime file](../../../principles/filesystem/index_cs.md#assets_runtimes).
### Arguments

- *string* **path** - Any file path.

### Return value

true if the file corresponding to the specified path is a generated runtime file; otherwise, false.
> **Notice:** This method will return 0 for any [native asset](../../../editor2/assets_workflow/assets_runtimes.md).


## bool IsRuntime ( UGUID any_guid )

Returns a value indicating whether the file corresponding to the specified GUID is a generated [runtime file](../../../principles/filesystem/index_cs.md#assets_runtimes).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

true if the file corresponding to the specified path is a generated runtime file; otherwise, false.
> **Notice:** This method will return 0 for any [native asset](../../../editor2/assets_workflow/assets_runtimes.md).


## bool IsRuntimePath ( string path )

Returns a value indicating whether the specified path is a path to a generated runtime file.
### Arguments

- *string* **path** - Any file path.

### Return value

true if the specified path is a path to a generated runtime file; otherwise, false.
## string GetRuntimeAlias ( string runtime_path )

Returns the [alias](../../../principles/filesystem/index_cs.md#alias) of the generated runtime file, specified by the given path.
### Arguments

- *string* **runtime_path** - Path to the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index_cs.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## string GetRuntimeAlias ( UGUID runtime_guid )

Returns the [alias](../../../principles/filesystem/index_cs.md#alias) of the generated runtime file, specified by the given GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index_cs.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## string GetRuntimeAlias ( string asset_path , int index )

Returns the [alias](../../../principles/filesystem/index_cs.md#alias) of the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *string* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index_cs.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## string GetRuntimeAlias ( UGUID asset_guid , int index )

Returns the [alias](../../../principles/filesystem/index_cs.md#alias) of the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index_cs.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## bool SetRuntimeGUID ( string runtime_path , UGUID new_runtime_guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the generated runtime file with a given path.
### Arguments

- *string* **runtime_path** - Path to the generated runtime file.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - New GUID to be set.

### Return value

true if a new GUID is successfully set; otherwise, false.
## bool SetRuntimeGUID ( UGUID runtime_guid , UGUID new_runtime_guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the generated runtime file with a given GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - New GUID to be set.

### Return value

true if a new GUID is successfully set; otherwise, false.
## bool SetRuntimeGUID ( string asset_path , int index , UGUID new_runtime_guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *string* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - New GUID to be set.

### Return value

true if a new GUID is successfully set; otherwise, false.
## bool SetRuntimeGUID ( UGUID asset_guid , int index , UGUID new_runtime_guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - New GUID to be set.

### Return value

true if a new GUID is successfully set; otherwise, false.
## UGUID GetRuntimeGUID ( string asset_path , int index )

Returns the current [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *string* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.

### Return value

Current generated runtime file [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the given asset and runtime index, if any; otherwise, empty GUID.
## UGUID GetRuntimeGUID ( UGUID asset_guid , int index )

Returns the current [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.

### Return value

Current generated runtime file [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the given asset and runtime index, if any; otherwise, empty GUID.
## UGUID AddRuntime ( string asset_path , string alias , int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index_cs.md#assets_runtimes) for the asset with a given path. A new GUID will be generated for the new runtime file.
### Arguments

- *string* **asset_path** - Path to the asset for which a new runtime is to be created.
- *string* **alias** - [Alias](../../../principles/filesystem/index_cs.md#alias) for the new runtime file.
- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new created runtime, if it was successfully created, or an empty GUID, otherwise.
## UGUID AddRuntime ( UGUID asset_guid , string alias , int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index_cs.md#assets_runtimes) for the asset with a given GUID. A new GUID will be generated for the new runtime file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a new runtime is to be created.
- *string* **alias** - [Alias](../../../principles/filesystem/index_cs.md#alias) for the new runtime file.
- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new created runtime, if it was successfully created, or an empty GUID, otherwise.
## bool AddRuntime ( string asset_path , string alias , UGUID runtime_guid , int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index_cs.md#assets_runtimes) for the asset with a given path. The specified GUID will be assigned to the new runtime file.
### Arguments

- *string* **asset_path** - Path to the asset for which a new runtime is to be created.
- *string* **alias** - [Alias](../../../principles/filesystem/index_cs.md#alias) for the new runtime file.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the new runtime file.
- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

true if a new runtime file is successfully created; otherwise, false.
## bool AddRuntime ( UGUID asset_guid , string alias , UGUID runtime_guid , int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index_cs.md#assets_runtimes) for the asset with a given GUID. The specified GUID will be assigned to the new runtime file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a new runtime is to be created.
- *string* **alias** - [Alias](../../../principles/filesystem/index_cs.md#alias) for the new runtime file.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) for the new runtime file.
- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

true if a new runtime file is successfully created; otherwise, false.
## bool ClearRuntimes ( string asset_path )

Deletes all generated [runtime files](../../../principles/filesystem/index_cs.md#assets_runtimes) for the asset with the specified path.
### Arguments

- *string* **asset_path** - Path to the asset for which all generated runtime files are to be deleted.

### Return value

true if all generated runtime files for the specified asset are successfully deleted; otherwise, false.
## bool ClearRuntimes ( UGUID asset_guid )

Deletes all generated [runtime files](../../../principles/filesystem/index_cs.md#assets_runtimes) for the asset with the specified GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which all generated runtime files are to be deleted.

### Return value

true if all generated runtime files for the specified asset are successfully deleted; otherwise, false.
## UGUID CopyRuntime ( string runtime_path , string new_asset_path )

Adds a copy of the generated runtime file with the specified path to another asset with the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *string* **runtime_path** - Path to the generated runtime file to be copied.
- *string* **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID CopyRuntime ( string runtime_path , UGUID new_asset_guid )

Adds a copy of the generated runtime file with the specified path to another asset having the specified GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *string* **runtime_path** - Path to the generated runtime file to be copied.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID CopyRuntime ( UGUID runtime_guid , string new_asset_path )

Adds a copy of the generated runtime file with the specified path to another asset having the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file to be copied.
- *string* **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID CopyRuntime ( UGUID runtime_guid , UGUID new_asset_guid )

Adds a copy of the generated runtime file with the specified GUID to another asset specified by GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file to be copied.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID CopyRuntime ( string asset_path , int index , string new_asset_path )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *string* **asset_path** - Path to the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID CopyRuntime ( string asset_path , int index , UGUID new_asset_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *string* **asset_path** - Path to the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID CopyRuntime ( UGUID asset_guid , int index , string new_asset_path )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).
- *string* **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID CopyRuntime ( UGUID asset_guid , int index , UGUID new_asset_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a copy of the generated runtime file is to be added.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## bool CopyRuntime ( string runtime_path , string new_asset_path , UGUID new_runtime_guid )

Adds a copy of the generated runtime file specified by path, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *string* **runtime_path** - Path to the generated runtime file to be copied.
- *string* **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool CopyRuntime ( string runtime_path , UGUID new_asset_guid , UGUID new_runtime_guid )

Adds a copy of the generated runtime file specified by path, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *string* **runtime_path** - Path to the generated runtime file to be copied.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a copy of the generated runtime file is to be added.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool CopyRuntime ( UGUID runtime_guid , string new_asset_path , UGUID new_runtime_guid )

Adds a copy of the generated runtime file specified by GUID, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset file to which the generated runtime file to be copied belongs.
- *string* **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool CopyRuntime ( UGUID runtime_guid , UGUID new_asset_guid , UGUID new_runtime_guid )

Adds a copy of the generated runtime file specified by GUID, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file to be copied.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a copy of the generated runtime file is to be added.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool CopyRuntime ( string asset_path , int index , string new_asset_path , UGUID new_runtime_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *string* **asset_path** - Path to the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool CopyRuntime ( string asset_path , int index , UGUID new_asset_guid , UGUID new_runtime_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *string* **asset_path** - Path to the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a copy of the generated runtime file is to be added.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool CopyRuntime ( UGUID asset_guid , int index , string new_asset_path , UGUID new_runtime_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).
- *string* **new_asset_path** - Path to another asset for which a copy of the generated runtime file is to be added.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool CopyRuntime ( UGUID asset_guid , int index , UGUID new_asset_guid , UGUID new_runtime_guid )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset file to which the generated runtime file to be copied belongs.
- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset for which a copy of the generated runtime file is to be added.
- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **new_runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) to be set for the new runtime file copy.

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool RemoveRuntime ( string runtime_path )

Deletes the specified generated runtime file and removes it from the list of runtimes of the corresponding asset.
### Arguments

- *string* **runtime_path** - Path to the generated runtime file to be deleted.

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## bool RemoveRuntime ( UGUID runtime_guid )

Deletes the specified generated runtime file and removes it from the list of runtimes of the corresponding asset.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file to be deleted.

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## bool RemoveRuntime ( string asset_path , int index )

Deletes the generated runtime file with the specified index, and removes it from the list of runtimes of the asset specified by path.
### Arguments

- *string* **asset_path** - Path to the asset file for which the specified generated runtime file is to be deleted.
- *int* **index** - Index of the generated runtime file to be deleted in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## bool RemoveRuntime ( UGUID asset_guid , int index )

Deletes the generated runtime file with the specified index, and removes it from the list of runtimes of the asset specified by GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset file for which the specified generated runtime file is to be deleted.
- *int* **index** - Index of the generated runtime file to be deleted in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## UGUID Resolve ( UGUID any_guid )

Resolves a given GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

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


## UGUID ResolveAsset ( UGUID any_guid )

Resolves a given GUID to a corresponding asset GUID, if any, or keeps the specified GUID as is.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

### Return value

Return GUID value is determined by the GUID specified in accordance with the following:
- [Primary runtime file](../../../principles/filesystem/index_cs.md#primary_runtime) GUID -> source asset file GUID.
- Generated runtime file GUID -> source asset file GUID.
- [Non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) file GUID -> GUID as is.
- Any other file GUID -> GUID as is.


```cpp
resolveAsset(asset_guid);		//	-> asset_guid
resolveAsset(primary_guid);		//	-> asset_guid
resolveAsset(runtime_guid);		//	-> asset_guid

```


## UGUID ResolvePrimary ( UGUID any_guid )

Resolves a given GUID to a corresponding primary runtime GUID, if any.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_cs.md).

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


## UGUID ResolveRuntimeAlias ( string path )

Resolves a given [alias](../../../principles/filesystem/index_cs.md#alias) of a generated runtime file to a corresponding GUID, if any.
### Arguments

- *string* **path** - Runtime file [alias](../../../principles/filesystem/index_cs.md#alias).

### Return value

[GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file having the specified alias, af any; otherwise, empty GUID
## bool SetRuntimeAlias ( UGUID asset_guid , int index , string new_alias )

Sets a new [alias](../../../principles/filesystem/index_cs.md#alias) for the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *string* **new_alias** - New alias to be set.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool SetRuntimeAlias ( UGUID runtime_guid , string new_alias )

Sets a new [alias](../../../principles/filesystem/index_cs.md#alias) for the generated runtime file with a given GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file.
- *string* **new_alias** - New alias to be set.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool SetRuntimeAlias ( string runtime_path , string new_alias )

Sets a new [alias](../../../principles/filesystem/index_cs.md#alias) for the generated runtime file with a given path.
### Arguments

- *string* **runtime_path** - Path to the generated runtime file.
- *string* **new_alias** - New alias to be set.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool SetRuntimeAlias ( string asset_path , int index , string new_alias )

Sets a new [alias](../../../principles/filesystem/index_cs.md#alias) for the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *string* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *string* **new_alias** - New alias to be set.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool SetRuntimePrimary ( string asset_path , int index , int primary )

Sets or unsets the generated runtime file, specified by the given non-native asset path and runtime index, as a [primary](../../../principles/filesystem/index_cs.md#primary_runtime) one.
### Arguments

- *string* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool SetRuntimePrimary ( string runtime_path , int primary )

Sets or unsets the generated runtime file with a given path as a [primary](../../../principles/filesystem/index_cs.md#primary_runtime) one.
### Arguments

- *string* **runtime_path** - Path to the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool SetRuntimePrimary ( UGUID runtime_guid , int primary )

Sets or unsets the generated runtime file with a given GUID as a [primary](../../../principles/filesystem/index_cs.md#primary_runtime) one.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool SetRuntimePrimary ( UGUID asset_guid , int index , int primary )

Sets or unsets the generated runtime file, specified by the given non-native asset GUID and runtime index, as a [primary](../../../principles/filesystem/index_cs.md#primary_runtime) one.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool SetRuntimeParameter ( UGUID asset_guid , int index , string parameter_name , string new_parameter_value )

Sets a new parameter with a given name and value for the generated runtime file specified by the non-native asset GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **parameter_name** - Name of the parameter to be set.
- *string* **new_parameter_value** - Value of the parameter to be set.

### Return value

true if a new parameter for the runtime is successfully set; otherwise, false.
## bool SetRuntimeParameter ( string asset_path , int index , string parameter_name , string new_parameter_value )

Sets a new parameter with a given name and value for the generated runtime file specified by the given non-native asset path.
### Arguments

- *string* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **parameter_name** - Name of the parameter to be set.
- *string* **new_parameter_value** - Value of the parameter to be set.

### Return value

true if a new parameter for the runtime is successfully set; otherwise, false.
## bool SetRuntimeParameter ( UGUID runtime_guid , string parameter_name , string new_parameter_value )

Sets a new parameter with a given name and value for the generated runtime file with a given GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file.
- *string* **parameter_name** - Name of the parameter to be set.
- *string* **new_parameter_value** - Value of the parameter to be set.

### Return value

true if a new parameter for the runtime is successfully set; otherwise, false.
## bool SetRuntimeParameter ( string runtime_path , string parameter_name , string new_parameter_value )

Sets a new parameter with a given name and value for the generated runtime file with the specified path.
### Arguments

- *string* **runtime_path** - Path to the generated runtime file.
- *string* **parameter_name** - Name of the parameter to be set.
- *string* **new_parameter_value** - Value of the parameter to be set.

### Return value

true if a new parameter for the runtime is successfully set; otherwise, false.
## string GetRuntimeParameter ( UGUID asset_guid , int index , string parameter_name )

Returns the value of the specified parameter of the specified runtime file, or an empty string if such parameter does not exist.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset file for the runtime file of which the parameter is returned.
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **parameter_name** - Name of the parameter to be returned.

### Return value

Value of the specified parameter, or an empty string if such parameter does not exist.
## string GetRuntimeParameter ( string asset_path , int index , string parameter_name )

Returns the value of the specified parameter of the specified runtime file, or an empty string if such parameter does not exist.
### Arguments

- *string* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **parameter_name** - Name of the parameter to be returned.

### Return value

Value of the specified parameter, or an empty string if such parameter does not exist.
## string GetRuntimeParameter ( UGUID runtime_guid , string parameter_name )

Returns the value of the specified parameter of the specified runtime file, or an empty string if such parameter does not exist.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file.
- *string* **parameter_name** - Name of the parameter to be returned.

### Return value

Value of the specified parameter, or an empty string if such parameter does not exist.
## string GetRuntimeParameter ( string runtime_path , string parameter_name )

Returns the value of the specified parameter of the specified runtime file, or an empty string if such parameter does not exist.
### Arguments

- *string* **runtime_path** - Path to the generated runtime file.
- *string* **parameter_name** - Name of the parameter to be returned.

### Return value

Value of the specified parameter, or an empty string if such parameter does not exist.
## bool HasRuntimeParameter ( UGUID asset_guid , int index , string parameter_name )

Checks if the specified runtime file has the specified parameter.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset file for the runtime file of which the parameter is checked.
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **parameter_name** - Name of the parameter to be checked.

### Return value

true if the runtime file has the specified parameter; otherwise, false.
## bool HasRuntimeParameter ( string asset_path , int index , string parameter_name )

Checks if the specified runtime file has the specified parameter.
### Arguments

- *string* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **parameter_name** - Name of the parameter to be checked.

### Return value

true if the runtime file has the specified parameter; otherwise, false.
## bool HasRuntimeParameter ( UGUID runtime_guid , string parameter_name )

Checks if the specified runtime file has the specified parameter.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file.
- *string* **parameter_name** - Name of the parameter to be checked.

### Return value

true if the runtime file has the specified parameter; otherwise, false.
## bool HasRuntimeParameter ( string runtime_path , string parameter_name )

Checks if the specified runtime file has the specified parameter.
### Arguments

- *string* **runtime_path** - Path to the generated runtime file.
- *string* **parameter_name** - Name of the parameter to be checked.

### Return value

true if the runtime file has the specified parameter; otherwise, false.
## bool RemoveRuntimeParameter ( UGUID asset_guid , int index , string parameter_name )

Removes the specified parameter of the runtime file of the asset with the specified GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **asset_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the asset file for the runtime file of which the parameter is removed.
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **parameter_name** - Name of the parameter to be removed.

### Return value

true if the specified parameter of the runtime file is successfully deleted; false if such parameter does not exist.
## bool RemoveRuntimeParameter ( string asset_path , int index , string parameter_name )

Removes the specified parameter of the runtime file of the asset with the specified path.
### Arguments

- *string* **asset_path** - Path to a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md).
- *int* **index** - Index of the generated runtime file in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).
- *string* **parameter_name** - Name of the parameter to be removed.

### Return value

true if the specified parameter of the runtime file is successfully deleted; false if such parameter does not exist.
## bool RemoveRuntimeParameter ( UGUID runtime_guid , string parameter_name )

Removes the specified parameter of the runtime file with the specified GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the generated runtime file.
- *string* **parameter_name** - Name of the parameter to be removed.

### Return value

true if the specified parameter of the runtime file is successfully deleted; false if such parameter does not exist.
## bool RemoveRuntimeParameter ( string runtime_path , string parameter_name )

Removes the specified parameter of the runtime file with the specified path.
### Arguments

- *string* **runtime_path** - Path to the generated runtime file.
- *string* **parameter_name** - Name of the parameter to be removed.

### Return value

true if the specified parameter of the runtime file is successfully deleted; false if such parameter does not exist.
