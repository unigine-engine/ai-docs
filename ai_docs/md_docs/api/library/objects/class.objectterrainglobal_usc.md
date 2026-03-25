# Unigine.ObjectTerrainGlobal Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create a [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object representing a certain fragment of Earth's surface on the basis of available GIS data (elevation and imagery). The global terrain is rendered using pre-generated [tilesets](../../../objects/objects/terrain/terrain_global/index.md#tiling) which represent LODs for different [data layers](../../../objects/objects/terrain/terrain_global/index.md#terrain_structure) (heights, albedo, normals, and masks). Tilesets are managed via the [TileSet](../../../api/library/objects/class.tileset_usc.md) class. Tileset data is stored in tileset files on the disk, these files are managed via the [TileSetFile](../../../api/library/objects/class.tilesetfile_usc.md) class


### See Also


- *[TerrainGlobalDetail](../../../api/library/objects/class.terrainglobaldetail_usc.md)* class to manage global terrain via C++, C# or UnigineScript API
- *[TerrainGlobalLod](../../../api/library/objects/class.terraingloballod_usc.md)* class to manage a global terrain LOD via C++, C# or UnigineScript API
- *[TerrainGlobalLodHeight](../../../api/library/objects/class.terraingloballodheight_usc.md)* class to manage a global terrain height LOD via C++, C# or UnigineScript API
- *[TerrainGlobalLods](../../../api/library/objects/class.terraingloballods_usc.md)* class to manage a group of global terrain LODs via C++, C# or UnigineScript API
- *[Tileset](../../../api/library/objects/class.tileset_usc.md)* class to manage tileset data of of the ObjectTerrainGlobal via C++, C# or UnigineScript API
- *[TilesetFile](../../../api/library/objects/class.tilesetfile_usc.md)* class to manage tileset files of the ObjectTerrainGlobal via C++, C# or UnigineScript API
- UnigineScript sample


## ObjectTerrainGlobal Class

### Members

---

## static ObjectTerrainGlobal ( )

Constructor. Creates a new empty global terrain object with default properties.
## void clear ( )

Clears all terrain data (lods, textures, details, masks etc.).
## static int type ( )

Returns the type of the object.
### Return value

[ObjectTerrainGlobal](../../../api/library/nodes/class.node_usc.md#OBJECT_TERRAIN_GLOBAL) type identifier.
## TerrainGlobalLods getAlbedoLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_usc.md) of terrain albedo LODs.
### Return value

Terrain albedo LODs group.
## void setAlbedoTextureArrayName ( string name )

Sets the name of the albedo textures array.
### Arguments

- *string* **name** - Name of the albedo textures array.

## string getAlbedoTextureArrayName ( )

Returns the name of the albedo textures array.
### Return value

Name of the albedo textures array.
## int addDetail ( string name )

Adds a new detail to the vector of terrain details.
### Arguments

- *string* **name** - Detail name.

### Return value

Number of the new detail.
## int cloneDetail ( int num )

Clones the detail with the specified number.
### Arguments

- *int* **num** - Detail number.

### Return value

Number of the new cloned terrain detail.
## TerrainGlobalDetail getDetail ( int num )

Returns the terrain detail with the specified number.
### Arguments

- *int* **num** - Detail number.

### Return value

Terrain [detail](../../../api/library/objects/class.terrainglobaldetail_usc.md).
## void removeDetail ( int num )

Removes the detail with the specified number.
### Arguments

- *int* **num** - Detail number.

## void swapDetail ( int num_0 , int num_1 )

Swaps two details of the terrain.
### Arguments

- *int* **num_0** - Number of the first detail.
- *int* **num_1** - Number of the second detail.

## void resizeDetails ( int size )

Resizes the vector of terrain details.
### Arguments

- *int* **size** - New size.

## int getNumDetails ( )

Returns the total number of details.
### Return value

Number of details.
## void setForceIntersection ( int intersection )


Enables or disables forced loading of necessary terrain tiles to ensure correct intersection detection.


> **Notice:** - When enabled, this option may significantly reduce performance. Thus, it is recommended to enable it, perform intersection check, and disable it again.
> - It is recommended to make two or more intersection requests to make sure you get the required result when necessary, as in some rare cases forced loading of tiles may not give you a 100% guarantee.


### Arguments

- *int* **intersection** - **1** to load necessary terrain tiles for intersection detection; otherwise, **0**. The default value is **0**.

## int isForceIntersection ( )

Returns a value indicating if forced loading of terrain tiles for intersection detection is enabled.
> **Notice:** This option is used to enable force loading of terrain tiles to ensure correct intersection detection.


### Return value

**1** if forced loading of terrain tiles for intersection detection is enabled; otherwise, **0**.
## int addMask ( string name )

Adds a new mask to the vector of masks.
### Arguments

- *string* **name** - Mask name.

### Return value

Number of the new mask, if the mask was added successfully; otherwise, -1.
## int cloneMask ( int num )

Clones the mask with the specified number.
### Arguments

- *int* **num** - Mask number.

### Return value

Number of the new cloned mask.
## void removeMask ( int num )

Removes the mask with the specified number from the vector of masks.
### Arguments

- *int* **num** - Mask number.

## void swapMask ( int num_0 , int num_1 )

Swaps two masks.
### Arguments

- *int* **num_0** - Number of the first mask.
- *int* **num_1** - Number of the second mask.

## void replaceMasks ( Vector<String> names )

Replaces the list of masks with a given one.
> **Notice:** If a mask used by some detail is missing in the new list, such detail will be considered as having no mask assigned, otherwise it will keep its mask.


### Arguments

- *Vector<String>* **names** - New list of masks.

## void resizeMasks ( int size )

Resizes the vector of masks.
### Arguments

- *int* **size** - New size.

## int getNumMasks ( )

Returns the total number of masks.
### Return value

Number of masks.
## TerrainGlobalLods getMaskLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_usc.md) of terrain mask LODs.
### Return value

Terrain mask LODs group.
## void setMaskName ( int num , string name )

Sets the name of the mask with the specified number.
### Arguments

- *int* **num** - Mask number.
- *string* **name** - New mask name.

## string getMaskName ( int num )

Returns the name for of mask with the specified number.
### Arguments

- *int* **num** - Mask number.

### Return value

Mask name.
## TerrainGlobalLods getHeightLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_usc.md) of terrain height LODs.
### Return value

Terrain height LODs group.
## void setHeightTextureArrayName ( string name )

Sets the name of the height textures array.
### Arguments

- *string* **name** - Name of the height textures array.

## string getHeightTextureArrayName ( )

Returns the name of the height textures array.
### Return value

Name of the height textures array.
## TerrainGlobalLods getNormalLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_usc.md) of terrain normal LODs.
### Return value

Terrain normal LODs group.
## void setNormalTextureArrayName ( string name )

Sets the name of the normal textures array.
### Arguments

- *string* **name** - Name of the normal textures array.

## string getNormalTextureArrayName ( )

Returns the name of the normal textures array.
### Return value

Name of the normal textures array.
## Vec3 fetchTopologyPoint ( Scalar x , Scalar y )

Returns topology data for a given terrain point.
### Arguments

- *Scalar* **x** - X coordinate of the point.
- *Scalar* **y** - Y coordinate of the point.

### Return value

World coordinates of the point.
