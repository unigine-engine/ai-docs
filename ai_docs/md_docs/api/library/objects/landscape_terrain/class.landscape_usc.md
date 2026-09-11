# Unigine.Landscape Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class is used to manage landscape terrain rendering and modification.


Terrain modification is performed in asynchronous mode on GPU side by calling a corresponding method, that commences a drawing operation. When calling such a method you should specify the GUID of an `.lmap` file [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_usc.md) to be modified, the coordinates of the upper-left corner and the resolution of the segment of data to be modified, you should also define which data layers are to be affected (heights, albedo, masks) via a set of [flags](#FLAGS_FILE_DATA_HEIGHT). The operation itself is to be implemented inside a callback handler.


### GPU-Based Terrain Modification


### See also


- C++ sample
- C++ sample
- C++ sample


## Landscape Class

### Members

## int isFilesClosed () const

Returns the current value indicating if `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_usc.md) are closed. Call this method before making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object to ensure that these files are not currently used by the Engine to avoid conflicts. If not, you can use the [*filesClose()*](#filesClose_void) method co close them.
### Return value

Current `.lmap` files for all landscape layer maps are closed
## static getEventSaveFile () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventApplyDiff () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventTextureDraw () const

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

## int terrainLoad ( WorldBoundBox bb )

Loads terrain data (tiles) for all landscape layer maps within the specified bounding box to cache.
### Arguments

- *WorldBoundBox* **bb** - Bounding box, defining landscape layer maps for which the data is to be loaded.

### Return value

**1** if terrain data was successfully loaded for all landscape layer maps within the specified bounding box; otherwise, **0**.
## void asyncApplyDiff ( int operation_id , UGUID file_guid , string path )

Applies the state of the landscape layer map stored in the specified file to the landscape layer map file with the specified GUID.
### Arguments

- *int* **operation_id** - [Operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the landscape layer map file to which a state stored at the specified path is to be applied.
- *string* **path** - Path to a file where the current landscape map modification state is stored.

## void asyncApplyDiff ( )

Applies the state of the landscape layer map stored in the specified file to the landscape layer map file with the specified GUID.
### Arguments

## void asyncSaveFile ( int operation_id , UGUID file_guid )

Saves the landscape layer map file with the specified GUID.
### Arguments

- *int* **operation_id** - [Operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the landscape layer map file.

## void asyncSaveFile ( )

Saves the landscape layer map file with the specified GUID.
### Arguments

## void asyncSaveFile ( int operation_id , UGUID file_guid , string path_new_diff , string path_old_diff )

Saves the specified landscape layer map file applying all changes along with saving old and new states (diff) to temporary files. These temporary files can be used to perform undo/redo operations via the [*applyDiff()*](#asyncApplyDiff_UGUID_cstr_void) method.
### Arguments

- *int* **operation_id** - [Operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the landscape layer map file.
- *string* **path_new_diff** - Path to a file to store the new landscape layer map state.
- *string* **path_old_diff** - Path to a file to store the old landscape layer map state.

## void asyncSaveFile ( )

Saves the specified landscape layer map file applying all changes along with saving old and new states (diff) to temporary files. These temporary files can be used to perform undo/redo operations via the [*applyDiff()*](#asyncApplyDiff_UGUID_cstr_void) method.
### Arguments

## void filesClose ( )

 Closes `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_usc.md).This method should be called before making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object to avoid conflicts, as these files are streamed continuosly by the Engine. Thus, by calling this method you inform the Engine that it should stop streaming terrain data. As you're done with modification you should call the [*filesOpen()*](#filesOpen_void) method to resume streaming operations.
## void filesOpen ( )

 Opens `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_usc.md).This method should be called after making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object. Prior to making such modifications the [*filesClose()*](#filesClose_void) method should be called.
## ObjectLandscapeTerrain getActiveTerrain ( )

Returns the current active [Landscape Terrain](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md) object.
> **Notice:** If a scene contains multiple Landscape Terrain objects, only one of them can be active (rendered).


### Return value

[Landscape Terrain](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_usc.md) object that is currently active.
## int generateOperationID ( )

Generates a new ID for the operation. This ID is used to manage operations.
```cpp
int id = Landscape::generateOperationID();
// user's code (bounding to ID)
Landscape::asyncTextureDraw(id, file_guid, coord, resolution, flags_file_data);

```


### Return value

New operation ID.
## void asyncResetModifications ( int operation_id , UGUID file_guid )

Asynchronously resets all unsaved modifications that were made to the landscape layer map identified by file GUID.
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the landscape layer map file to be restored.
