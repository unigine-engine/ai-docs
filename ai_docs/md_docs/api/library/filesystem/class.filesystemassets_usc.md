# Unigine::FileSystemAssets Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class represents the subsystem of the Engine's [file system](../../../principles/filesystem/index.md) that is used to manage [assets and runtime files](../../../editor2/assets_workflow/assets_runtimes.md).


## FileSystemAssets Class

### Members

---

## bool isAsset ( )

Returns a value indicating whether the file with the specified GUID is a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (has [runtime files](../../../principles/filesystem/index.md#assets_runtimes) generated for it).
### Arguments

### Return value

true if the file with the specified GUID is a non-native asset; otherwise, false.
## bool isAsset ( )

Returns a value indicating whether the file with the specified path is a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (has [runtime files](../../../principles/filesystem/index.md#assets_runtimes) generated for it).
### Arguments

### Return value

true if the file with the specified path is a non-native asset; otherwise, false.
## UGUID getAssetGUID ( )

Returns a GUID of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (having generated runtime file or files) for the specified path.
### Arguments

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of a non-native asset corresponding to the specified path if it exists; otherwise, empty GUID.
> **Notice:** This method will return an empty GUID for any asset having no runtimes generated for it.


## UGUID getAssetGUID ( )

Returns a GUID of a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) (having generated runtime file or files) for the specified GUID.
### Arguments

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of a non-native asset corresponding to the specified path if it exists; otherwise, empty GUID.
> **Notice:** This method will return an empty GUID for any asset having no runtimes generated for it.


## int getNumRuntimes ( )

Returns a number of [runtime files](../../../editor2/assets_workflow/assets_runtimes.md) for a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) having the specified path.
### Arguments

### Return value

Number of runtime files generated for the specified asset.
## int getNumRuntimes ( )

Returns a number of [runtime files](../../../editor2/assets_workflow/assets_runtimes.md) for a [non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) having the specified GUID.
### Arguments

### Return value

Number of runtime files generated for the specified asset.
## bool isPrimary ( )

Returns a value indicating whether the runtime file corresponding to the specified path is a [primary](../../../principles/filesystem/index.md#primary_runtime) one.
### Arguments

### Return value

true if the runtime file corresponding to the specified path is a primary one; otherwise, false.
## bool isPrimary ( )

Returns a value indicating whether the runtime file corresponding to the specified GUID is a [primary](../../../principles/filesystem/index.md#primary_runtime) one.
### Arguments

### Return value

true if the runtime file corresponding to the specified GUID is a primary one; otherwise, false.
## UGUID getPrimaryGUID ( )

Returns the GUID of the [primary runtime file](../../../principles/filesystem/index.md#primary_runtime) for the specified file GUID if it exists.
### Arguments

### Return value

Return value is determined by the specified GUID in accordance with the following:
- Asset file GUID -> GUID of its primary runtime file, if any; otherwise empty GUID.
- Primary runtime file GUID -> GUID of this primary runtime file.
- Runtime file GUID -> GUID of the primary runtime file for its asset, if any; otherwise empty GUID.
- Any other file GUID -> empty GUID.


## UGUID getPrimaryGUID ( )

Returns the GUID of the [primary runtime file](../../../principles/filesystem/index.md#primary_runtime) for the specified file path if it exists.
### Arguments

### Return value

Return value is determined by the specified GUID in accordance with the following:
- Asset file path -> GUID of its primary runtime file, if any; otherwise empty GUID.
- Primary runtime file path -> GUID of this primary runtime file.
- Runtime file path -> GUID of the primary runtime file for its asset, if any; otherwise empty GUID.
- Any other file path -> empty GUID.


## bool isMeta ( UGUID any_guid )

Returns a value indicating whether the file with the specified GUID is a [`*.meta`](../../../editor2/assets_workflow/assets_runtimes.md) file.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_usc.md).

### Return value

true if the file with the specified GUID is a `*.meta` file; otherwise, false.
## bool isRuntime ( )

Returns a value indicating whether the file corresponding to the specified path is a generated [runtime file](../../../principles/filesystem/index.md#assets_runtimes).
### Arguments

### Return value

true if the file corresponding to the specified path is a generated runtime file; otherwise, false.
> **Notice:** This method will return 0 for any [native asset](../../../editor2/assets_workflow/assets_runtimes.md).


## bool isRuntime ( )

Returns a value indicating whether the file corresponding to the specified GUID is a generated [runtime file](../../../principles/filesystem/index.md#assets_runtimes).
### Arguments

### Return value

true if the file corresponding to the specified path is a generated runtime file; otherwise, false.
> **Notice:** This method will return 0 for any [native asset](../../../editor2/assets_workflow/assets_runtimes.md).


## bool isRuntimePath ( string path )

Returns a value indicating whether the specified path is a path to a generated runtime file.
### Arguments

- *string* **path** - Any file path.

### Return value

true if the specified path is a path to a generated runtime file; otherwise, false.
## getRuntimeAlias ( )

Returns the [alias](../../../principles/filesystem/index.md#alias) of the generated runtime file, specified by the given path.
### Arguments

### Return value

[Alias](../../../principles/filesystem/index.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## getRuntimeAlias ( )

Returns the [alias](../../../principles/filesystem/index.md#alias) of the generated runtime file, specified by the given GUID.
### Arguments

### Return value

[Alias](../../../principles/filesystem/index.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## getRuntimeAlias ( int index )

Returns the [alias](../../../principles/filesystem/index.md#alias) of the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *int* **index** - Index of the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## getRuntimeAlias ( int index )

Returns the [alias](../../../principles/filesystem/index.md#alias) of the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *int* **index** - Index of the generated runtime file.

### Return value

[Alias](../../../principles/filesystem/index.md#alias) set for the specified generated runtime file, if it exists; otherwise nullptr.
## bool setRuntimeGUID ( )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the generated runtime file with a given path.
### Arguments

### Return value

true if a new GUID is successfully set; otherwise, false.
## bool setRuntimeGUID ( )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the generated runtime file with a given GUID.
### Arguments

### Return value

true if a new GUID is successfully set; otherwise, false.
## bool setRuntimeGUID ( int index )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *int* **index** - Index of the generated runtime file.

### Return value

true if a new GUID is successfully set; otherwise, false.
## bool setRuntimeGUID ( int index )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *int* **index** - Index of the generated runtime file.

### Return value

true if a new GUID is successfully set; otherwise, false.
## UGUID getRuntimeGUID ( int index )

Returns the current [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *int* **index** - Index of the generated runtime file.

### Return value

Current generated runtime file [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the given asset and runtime index, if any; otherwise, empty GUID.
## UGUID getRuntimeGUID ( int index )

Returns the current [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *int* **index** - Index of the generated runtime file.

### Return value

Current generated runtime file [GUID](../../../api/library/filesystem/class.uguid_usc.md) for the given asset and runtime index, if any; otherwise, empty GUID.
## UGUID addRuntime ( int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index.md#assets_runtimes) for the asset with a given path. A new GUID will be generated for the new runtime file.
### Arguments

- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new created runtime, if it was successfully created, or an empty GUID, otherwise.
## UGUID addRuntime ( int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index.md#assets_runtimes) for the asset with a given GUID. A new GUID will be generated for the new runtime file.
### Arguments

- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new created runtime, if it was successfully created, or an empty GUID, otherwise.
## bool addRuntime ( int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index.md#assets_runtimes) for the asset with a given path. The specified GUID will be assigned to the new runtime file.
### Arguments

- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

true if a new runtime file is successfully created; otherwise, false.
## bool addRuntime ( int primary = 0 )

Creates a new [runtime file](../../../principles/filesystem/index.md#assets_runtimes) for the asset with a given GUID. The specified GUID will be assigned to the new runtime file.
### Arguments

- *int* **primary** - Use 1 to create a new runtime as a primary one; otherwise, 0.

### Return value

true if a new runtime file is successfully created; otherwise, false.
## bool clearRuntimes ( )

Deletes all generated [runtime files](../../../principles/filesystem/index.md#assets_runtimes) for the asset with the specified path.
### Arguments

### Return value

true if all generated runtime files for the specified asset are successfully deleted; otherwise, false.
## bool clearRuntimes ( )

Deletes all generated [runtime files](../../../principles/filesystem/index.md#assets_runtimes) for the asset with the specified GUID.
### Arguments

### Return value

true if all generated runtime files for the specified asset are successfully deleted; otherwise, false.
## UGUID copyRuntime ( )

Adds a copy of the generated runtime file with the specified path to another asset with the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( )

Adds a copy of the generated runtime file with the specified path to another asset having the specified GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( )

Adds a copy of the generated runtime file with the specified path to another asset having the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( )

Adds a copy of the generated runtime file with the specified GUID to another asset specified by GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( int index )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( int index )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( int index )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified path.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## UGUID copyRuntime ( int index )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified GUID.
> **Notice:** A new GUID will be generated for the created runtime file copy.


### Arguments

- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the new runtime file copy, if it is created successfully; otherwise, empty GUID.
## bool copyRuntime ( )

Adds a copy of the generated runtime file specified by path, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( )

Adds a copy of the generated runtime file specified by path, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( )

Adds a copy of the generated runtime file specified by GUID, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( )

Adds a copy of the generated runtime file specified by GUID, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( int index )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( int index )

Adds a copy of the runtime file with the specified index, generated for the asset specified by path, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( int index )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified path.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool copyRuntime ( int index )

Adds a copy of the runtime file with the specified index, generated for the asset specified by GUID, to another asset having the specified GUID.
> **Notice:** The created runtime file copy will have the specified runtime GUID assigned.


### Arguments

- *int* **index** - Index of the generated runtime file to be copied in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).

### Return value

true if the specified runtime file is successfully copied; otherwise, false.
## bool removeRuntime ( )

Deletes the specified generated runtime file and removes it from the list of runtimes of the corresponding asset.
### Arguments

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## bool removeRuntime ( )

Deletes the specified generated runtime file and removes it from the list of runtimes of the corresponding asset.
### Arguments

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## bool removeRuntime ( int index )

Deletes the generated runtime file with the specified index, and removes it from the list of runtimes of the asset specified by path.
### Arguments

- *int* **index** - Index of the generated runtime file to be deleted in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_cstr_int).

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## bool removeRuntime ( int index )

Deletes the generated runtime file with the specified index, and removes it from the list of runtimes of the asset specified by GUID.
### Arguments

- *int* **index** - Index of the generated runtime file to be deleted in the range from 0 to the [total number of runtimes generated for the asset](#getNumRuntimes_UGUID_int).

### Return value

true if the specified runtime file is successfully deleted; otherwise, false.
## UGUID resolve ( UGUID any_guid )

Resolves a given GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_usc.md).

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


## UGUID resolveAsset ( UGUID any_guid )

Resolves a given GUID to a corresponding asset GUID, if any, or keeps the specified GUID as is.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_usc.md).

### Return value

Return GUID value is determined by the GUID specified in accordance with the following:
- [Primary runtime file](../../../principles/filesystem/index.md#primary_runtime) GUID -> source asset file GUID.
- Generated runtime file GUID -> source asset file GUID.
- [Non-native asset](../../../editor2/assets_workflow/assets_runtimes.md) file GUID -> GUID as is.
- Any other file GUID -> GUID as is.


```cpp
resolveAsset(asset_guid);		//	-> asset_guid
resolveAsset(primary_guid);		//	-> asset_guid
resolveAsset(runtime_guid);		//	-> asset_guid

```


## UGUID resolvePrimary ( UGUID any_guid )

Resolves a given GUID to a corresponding primary runtime GUID, if any.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **any_guid** - Any file [GUID](../../../api/library/filesystem/class.uguid_usc.md).

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


## UGUID resolveRuntimeAlias ( string path )

Resolves a given [alias](../../../principles/filesystem/index.md#alias) of a generated runtime file to a corresponding GUID, if any.
### Arguments

- *string* **path** - Runtime file [alias](../../../principles/filesystem/index.md#alias).

### Return value

[GUID](../../../api/library/filesystem/class.uguid_usc.md) of the generated runtime file having the specified alias, af any; otherwise, empty GUID
## bool setRuntimeAlias ( int index )

Sets a new [alias](../../../principles/filesystem/index.md#alias) for the generated runtime file, specified by the given non-native asset GUID and runtime index.
### Arguments

- *int* **index** - Index of the generated runtime file.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool setRuntimeAlias ( )

Sets a new [alias](../../../principles/filesystem/index.md#alias) for the generated runtime file with a given GUID.
### Arguments

### Return value

true if a new alias is successfully set; otherwise, false.
## bool setRuntimeAlias ( )

Sets a new [alias](../../../principles/filesystem/index.md#alias) for the generated runtime file with a given path.
### Arguments

### Return value

true if a new alias is successfully set; otherwise, false.
## bool setRuntimeAlias ( int index )

Sets a new [alias](../../../principles/filesystem/index.md#alias) for the generated runtime file, specified by the given non-native asset path and runtime index.
### Arguments

- *int* **index** - Index of the generated runtime file.

### Return value

true if a new alias is successfully set; otherwise, false.
## bool setRuntimePrimary ( int index , int primary )

Sets or unsets the generated runtime file, specified by the given non-native asset path and runtime index, as a [primary](../../../principles/filesystem/index.md#primary_runtime) one.
### Arguments

- *int* **index** - Index of the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool setRuntimePrimary ( int primary )

Sets or unsets the generated runtime file with a given path as a [primary](../../../principles/filesystem/index.md#primary_runtime) one.
### Arguments

- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool setRuntimePrimary ( int primary )

Sets or unsets the generated runtime file with a given GUID as a [primary](../../../principles/filesystem/index.md#primary_runtime) one.
### Arguments

- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.


## bool setRuntimePrimary ( int index , int primary )

Sets or unsets the generated runtime file, specified by the given non-native asset GUID and runtime index, as a [primary](../../../principles/filesystem/index.md#primary_runtime) one.
### Arguments

- *int* **index** - Index of the generated runtime file.
- *int* **primary** - 1 to make the runtime file primary; 0 to unmake, if it is already set.

### Return value

true if the runtime file is successfully set as a primary one; otherwise, false.
> **Notice:** There can be the only one primary runtime file, so when a new runtime file is set as the primary, the previous one is unset.
