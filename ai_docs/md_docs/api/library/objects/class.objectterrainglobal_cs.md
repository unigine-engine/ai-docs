# Unigine.ObjectTerrainGlobal Class (CS)

**Inherits from:** Object


This class is used to create a [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object representing a certain fragment of Earth's surface on the basis of available GIS data (elevation and imagery). The global terrain is rendered using pre-generated [tilesets](../../../objects/objects/terrain/terrain_global/index.md#tiling) which represent LODs for different [data layers](../../../objects/objects/terrain/terrain_global/index.md#terrain_structure) (heights, albedo, normals, and masks). Tilesets are managed via the [TileSet](../../../api/library/objects/class.tileset_cs.md) class. Tileset data is stored in tileset files on the disk, these files are managed via the [TileSetFile](../../../api/library/objects/class.tilesetfile_cs.md) class


### See Also


- *[TerrainGlobalDetail](../../../api/library/objects/class.terrainglobaldetail_cs.md)* class to manage global terrain via C++, C# or UnigineScript API
- *[TerrainGlobalLod](../../../api/library/objects/class.terraingloballod_cs.md)* class to manage a global terrain LOD via C++, C# or UnigineScript API
- *[TerrainGlobalLodHeight](../../../api/library/objects/class.terraingloballodheight_cs.md)* class to manage a global terrain height LOD via C++, C# or UnigineScript API
- *[TerrainGlobalLods](../../../api/library/objects/class.terraingloballods_cs.md)* class to manage a group of global terrain LODs via C++, C# or UnigineScript API
- *[Tileset](../../../api/library/objects/class.tileset_cs.md)* class to manage tileset data of of the ObjectTerrainGlobal via C++, C# or UnigineScript API
- *[TilesetFile](../../../api/library/objects/class.tilesetfile_cs.md)* class to manage tileset files of the ObjectTerrainGlobal via C++, C# or UnigineScript API
- UnigineScript sample


## ObjectTerrainGlobal Class

### Properties

## bool ForceIntersection

The value indicating if forced loading of terrain tiles for intersection detection is enabled.
> **Notice:** - When enabled, this option may significantly reduce performance. Thus, it is recommended to enable it, perform intersection check, and disable it again.
> - It is recommended to make two or more intersection requests to make sure you get the required result when necessary, as in some rare cases forced loading of tiles may not give you a 100% guarantee.

## 🔒︎ Texture HeightTextureArray

The height textures array.
## string HeightTextureArrayName

The name of the height textures array.
## 🔒︎ Texture NormalTextureArray

The normal textures array.
## string NormalTextureArrayName

The name of the normal textures array.
## 🔒︎ Texture AlbedoTextureArray

The albedo textures array.
## string AlbedoTextureArrayName

The name of the albedo textures array.
## 🔒︎ int NumDetails

The total number of details.
## 🔒︎ int NumMasks

The total number of masks.
### Members

---

## ObjectTerrainGlobal ( )

Constructor. Creates a new empty global terrain object with default properties.
## void Clear ( )

Clears all terrain data (lods, textures, details, masks etc.).
## static int type ( )

Returns the type of the object.
### Return value

[ObjectTerrainGlobal](../../../api/library/nodes/class.node_cs.md#OBJECT_TERRAIN_GLOBAL) type identifier.
## TerrainGlobalLods GetAlbedoLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_cs.md) of terrain albedo LODs.
### Return value

Terrain albedo LODs group.
## int AddDetail ( string name )

Adds a new detail to the vector of terrain details.
### Arguments

- *string* **name** - Detail name.

### Return value

Number of the new detail.
## int CloneDetail ( int num )

Clones the detail with the specified number.
### Arguments

- *int* **num** - Detail number.

### Return value

Number of the new cloned terrain detail.
## TerrainGlobalDetail GetDetail ( int num )

Returns the terrain detail with the specified number.
### Arguments

- *int* **num** - Detail number.

### Return value

Terrain [detail](../../../api/library/objects/class.terrainglobaldetail_cs.md).
## void RemoveDetail ( int num )

Removes the detail with the specified number.
### Arguments

- *int* **num** - Detail number.

## void SwapDetail ( int num_0 , int num_1 )

Swaps two details of the terrain.
### Arguments

- *int* **num_0** - Number of the first detail.
- *int* **num_1** - Number of the second detail.

## void ResizeDetails ( int size )

Resizes the vector of terrain details.
### Arguments

- *int* **size** - New size.

## int AddMask ( string name )

Adds a new mask to the vector of masks.
### Arguments

- *string* **name** - Mask name.

### Return value

Number of the new mask, if the mask was added successfully; otherwise, -1.
## int CloneMask ( int num )

Clones the mask with the specified number.
### Arguments

- *int* **num** - Mask number.

### Return value

Number of the new cloned mask.
## void RemoveMask ( int num )

Removes the mask with the specified number from the vector of masks.
### Arguments

- *int* **num** - Mask number.

## void SwapMask ( int num_0 , int num_1 )

Swaps two masks.
### Arguments

- *int* **num_0** - Number of the first mask.
- *int* **num_1** - Number of the second mask.

## void ReplaceMasks ( string[] names )

Replaces the list of masks with a given one.
> **Notice:** If a mask used by some detail is missing in the new list, such detail will be considered as having no mask assigned, otherwise it will keep its mask.


### Arguments

- *string[]* **names** - New list of masks.

## void ResizeMasks ( int size )

Resizes the vector of masks.
### Arguments

- *int* **size** - New size.

## TerrainGlobalLods GetMaskLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_cs.md) of terrain mask LODs.
### Return value

Terrain mask LODs group.
## void SetMaskName ( int num , string name )

Sets the name of the mask with the specified number.
### Arguments

- *int* **num** - Mask number.
- *string* **name** - New mask name.

## string GetMaskName ( int num )

Returns the name for of mask with the specified number.
### Arguments

- *int* **num** - Mask number.

### Return value

Mask name.
## TerrainGlobalLods GetHeightLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_cs.md) of terrain height LODs.
### Return value

Terrain height LODs group.
## TerrainGlobalLods GetNormalLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_cs.md) of terrain normal LODs.
### Return value

Terrain normal LODs group.
## int FetchTopologyData ( double x , double y , out Vec3 ret_point , out vec3 ret_normal , out vec3 ret_up , int force = 0 )

Returns topology data for a given terrain point.
### Arguments

- *double* **x** - X coordinate of the point.
- *double* **y** - Y coordinate of the point.
- *out Vec3* **ret_point** - World coordinates of the point.
- *out vec3* **ret_normal** - Normal coordinates.
- *out vec3* **ret_up** - "Up" vector coordinates.
- *int* **force** - Force flag. Use 1 to load files in any case; otherwise, 0. The default value is 0.

### Return value

**1** if the topology data was fetched successfully; otherwise, 0.
