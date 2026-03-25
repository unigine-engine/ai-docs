# Unigine.TerrainGlobalLods Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage a group of [LODs](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalLods Class

### Members

---

## int getDataFormat ( )

Returns a value indicating current image format for the tile data.
### Return value

Tile data image format. One of the [IMAGE_FORMAT_*](../../../api/library/common/class.image_usc.md#FORMAT_ATI1) values.
## int getDataType ( )

Returns a value indicating current image format for the tile data.
### Return value

Tile data image type. One of the [IMAGE_*](../../../api/library/common/class.image_usc.md#IMAGE_2D) values.
## int getMaskFormat ( )

Returns a value indicating current image format for the tile mask.
### Return value

Tile mask image format. One of the [IMAGE_FORMAT_*](../../../api/library/common/class.image_usc.md#FORMAT_ATI1) values.
## void setNumLayers ( int layers )

Sets the number of layers of the LOD group.
### Arguments

- *int* **layers** - Number of layers.

## int getNumLayers ( )

Returns the number of layers of the LOD group.
### Return value

Number of layers.
## int getNumLods ( )

Returns the total number of LODs in the group.
### Return value

Total number of LODs.
## int addLod ( )

Adds a new LOD.
### Return value

Index of the last added LOD.
## void insertLod ( int num )

Inserts a new LOD at the specified position.
### Arguments

- *int* **num** - Position to insert a new LOD at.

## void removeLod ( int num )

Removes the LOD with the specified number.
### Arguments

- *int* **num** - LOD number.

## void clearLods ( )

Removes all LODs.
## int fetch ( BoundSphere bs , BoundBox bb , int force = 0 )

Loads the data of all LODs for the tiles within a given bounding box and a bounding sphere.
### Arguments

- *BoundSphere* **bs** - Bounding sphere.
- *BoundBox* **bb** - Bounding box.
- *int* **force** - Force flag. Use 1 to load files in any case; otherwise, 0. The default value is 0.

### Return value

**1** if the data of all LODs was fetched successfully; otherwise, 0.
## int getType ( )

Returns the type of LODs.
## string getName ( )

Returns the name of the LOD group.
### Return value

LOD group name.
## TerrainGlobalLod getLod ( int num )

Returns the LOD with a given number.
### Arguments

- *int* **num** - LOD number.

### Return value

TerrainGlobalLod instance.
## String getVideoMemoryUsage ( )

Returns information about the total video memory usage for all LODs in the group.
### Return value

Total video memory usage for all LODs.
