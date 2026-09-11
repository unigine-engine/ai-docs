# Unigine.TerrainGlobalLods Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage a group of [LODs](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalLods Class

### Members

## int getNumLods () const

Returns the current total number of lods in the group.
### Return value

Current total number of lods in the group
## void setNumLayers ( int layers )

Sets a new number of layers of the lod group.
### Arguments

- *int* **layers** - The number of layers of the lod group

## int getNumLayers () const

Returns the current number of layers of the lod group.
### Return value

Current number of layers of the lod group
## int getMaskFormat () const

Returns the current value indicating current image format for the tile mask. One of the [Image::FORMAT_*](../../../api/library/common/class.image_usc.md) values.
### Return value

Current value indicating current image format for the tile mask
## int getDataFormat () const

Returns the current value indicating current image format for the tile data. One of the [Image::FORMAT_*](../../../api/library/common/class.image_usc.md#FORMAT_ATI1) values.
### Return value

Current value indicating current image format for the tile data
## int getDataType () const

Returns the current value indicating current image type for the tile data. One of the [Image::IMAGE_*](../../../api/library/common/class.image_usc.md#IMAGE_2D) values.
### Return value

Current value indicating current image format for the tile data
## int getType () const

Returns the current type of lods.
### Return value

Current type of lods
## const char * getName () const

Returns the current name of the lod group.
### Return value

Current name of the lod group
---

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
