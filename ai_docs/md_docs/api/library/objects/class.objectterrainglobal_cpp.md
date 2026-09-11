# Unigine.ObjectTerrainGlobal Class (CPP)

**Header:** #include <UnigineObjects.h>

**Inherits from:** Object


This class is used to create a [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object representing a certain fragment of Earth's surface on the basis of available GIS data (elevation and imagery). The global terrain is rendered using pre-generated [tilesets](../../../objects/objects/terrain/terrain_global/index.md#tiling) which represent LODs for different [data layers](../../../objects/objects/terrain/terrain_global/index.md#terrain_structure) (heights, albedo, normals, and masks). Tilesets are managed via the [TileSet](../../../api/library/objects/class.tileset_cpp.md) class. Tileset data is stored in tileset files on the disk, these files are managed via the [TileSetFile](../../../api/library/objects/class.tilesetfile_cpp.md) class


### See Also


- *[TerrainGlobalDetail](../../../api/library/objects/class.terrainglobaldetail_cpp.md)* class to manage global terrain via C++, C# or UnigineScript API
- *[TerrainGlobalLod](../../../api/library/objects/class.terraingloballod_cpp.md)* class to manage a global terrain LOD via C++, C# or UnigineScript API
- *[TerrainGlobalLodHeight](../../../api/library/objects/class.terraingloballodheight_cpp.md)* class to manage a global terrain height LOD via C++, C# or UnigineScript API
- *[TerrainGlobalLods](../../../api/library/objects/class.terraingloballods_cpp.md)* class to manage a group of global terrain LODs via C++, C# or UnigineScript API
- *[Tileset](../../../api/library/objects/class.tileset_cpp.md)* class to manage tileset data of of the ObjectTerrainGlobal via C++, C# or UnigineScript API
- *[TilesetFile](../../../api/library/objects/class.tilesetfile_cpp.md)* class to manage tileset files of the ObjectTerrainGlobal via C++, C# or UnigineScript API
- UnigineScript sample


## ObjectTerrainGlobal Class

### Members

## void setForceIntersection ( bool intersection )

Sets a new value indicating if forced loading of terrain tiles for intersection detection is enabled.
> **Notice:** - When enabled, this option may significantly reduce performance. Thus, it is recommended to enable it, perform intersection check, and disable it again.
> - It is recommended to make two or more intersection requests to make sure you get the required result when necessary, as in some rare cases forced loading of tiles may not give you a 100% guarantee.

### Arguments

- *bool* **intersection** - value indicating if forced loading of terrain tiles for intersection detection is enabled

## bool isForceIntersection () const

Returns the current value indicating if forced loading of terrain tiles for intersection detection is enabled.
> **Notice:** - When enabled, this option may significantly reduce performance. Thus, it is recommended to enable it, perform intersection check, and disable it again.
> - It is recommended to make two or more intersection requests to make sure you get the required result when necessary, as in some rare cases forced loading of tiles may not give you a 100% guarantee.

### Return value

value indicating if forced loading of terrain tiles for intersection detection is enabled
## Ptr < Texture > getHeightTextureArray () const

Returns the current height textures array.
### Return value

Current height textures array
## void setHeightTextureArrayName ( const char * name )

Sets a new name of the height textures array.
### Arguments

- *const char ** **name** - The name of the height textures array

## const char * getHeightTextureArrayName () const

Returns the current name of the height textures array.
### Return value

Current name of the height textures array
## Ptr < Texture > getNormalTextureArray () const

Returns the current normal textures array.
### Return value

Current normal textures array
## void setNormalTextureArrayName ( const char * name )

Sets a new name of the normal textures array.
### Arguments

- *const char ** **name** - The name of the normal textures array

## const char * getNormalTextureArrayName () const

Returns the current name of the normal textures array.
### Return value

Current name of the normal textures array
## Ptr < Texture > getAlbedoTextureArray () const

Returns the current albedo textures array.
### Return value

Current albedo textures array
## void setAlbedoTextureArrayName ( const char * name )

Sets a new name of the albedo textures array.
### Arguments

- *const char ** **name** - The name of the albedo textures array

## const char * getAlbedoTextureArrayName () const

Returns the current name of the albedo textures array.
### Return value

Current name of the albedo textures array
## int getNumDetails () const

Returns the current total number of details.
### Return value

Current total number of details
## int getNumMasks () const

Returns the current total number of masks.
### Return value

Current total number of masks
---

## static ObjectTerrainGlobalPtr create ( )

Constructor. Creates a new empty global terrain object with default properties.
## void clear ( )

Clears all terrain data (lods, textures, details, masks etc.).
## static int type ( )

Returns the type of the object.
### Return value

[ObjectTerrainGlobal](../../../api/library/nodes/class.node_cpp.md#OBJECT_TERRAIN_GLOBAL) type identifier.
## Ptr < TerrainGlobalLods > getAlbedoLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_cpp.md) of terrain albedo LODs.
### Return value

Terrain albedo LODs group.
## int addDetail ( const char * name )

Adds a new detail to the vector of terrain details.
### Arguments

- *const char ** **name** - Detail name.

### Return value

Number of the new detail.
## int cloneDetail ( int num )

Clones the detail with the specified number.
### Arguments

- *int* **num** - Detail number.

### Return value

Number of the new cloned terrain detail.
## Ptr < TerrainGlobalDetail > getDetail ( int num )

Returns the terrain detail with the specified number.
### Arguments

- *int* **num** - Detail number.

### Return value

Terrain [detail](../../../api/library/objects/class.terrainglobaldetail_cpp.md).
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

## int addMask ( const char * name )

Adds a new mask to the vector of masks.
### Arguments

- *const char ** **name** - Mask name.

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

## void replaceMasks ( const Vector < String > & names )

Replaces the list of masks with a given one.
> **Notice:** If a mask used by some detail is missing in the new list, such detail will be considered as having no mask assigned, otherwise it will keep its mask.


### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [String](../../../api/library/common/class.string_cpp.md) > &* **names** - New list of masks.

## void resizeMasks ( int size )

Resizes the vector of masks.
### Arguments

- *int* **size** - New size.

## Ptr < TerrainGlobalLods > getMaskLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_cpp.md) of terrain mask LODs.
### Return value

Terrain mask LODs group.
## void setMaskName ( int num , const char * name )

Sets the name of the mask with the specified number.
### Arguments

- *int* **num** - Mask number.
- *const char ** **name** - New mask name.

## const char * getMaskName ( int num ) const

Returns the name for of mask with the specified number.
### Arguments

- *int* **num** - Mask number.

### Return value

Mask name.
## Ptr < TerrainGlobalLods > getHeightLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_cpp.md) of terrain height LODs.
### Return value

Terrain height LODs group.
## Ptr < TerrainGlobalLods > getNormalLods ( )

Returns the [group](../../../api/library/objects/class.terraingloballods_cpp.md) of terrain normal LODs.
### Return value

Terrain normal LODs group.
## int fetchTopologyData ( double x , double y , Math:: Vec3 & ret_point , Math:: vec3 & ret_normal , Math:: vec3 & ret_up , int force = 0 )

Returns topology data for a given terrain point.
### Arguments

- *double* **x** - X coordinate of the point.
- *double* **y** - Y coordinate of the point.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_point** - World coordinates of the point.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_normal** - Normal coordinates.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_up** - "Up" vector coordinates.
- *int* **force** - Force flag. Use 1 to load files in any case; otherwise, 0. The default value is 0.

### Return value

**1** if the topology data was fetched successfully; otherwise, 0.
