# Unigine.TerrainGlobalLods Class (CS)


This class is used to manage a group of [LODs](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalLods Class

### Properties

## 🔒︎ int NumLods

The total number of lods in the group.
## int NumLayers

The number of layers of the lod group.
## 🔒︎ int MaskFormat

The A value indicating current image format for the tile mask.
## 🔒︎ int DataFormat

The A value indicating current image format for the tile data.
## 🔒︎ int DataType

The A value indicating current image format for the tile data.
## 🔒︎ int Type

The type of lods.
## 🔒︎ string Name

The name of the lod group.
### Members

---

## int AddLod ( )

Adds a new LOD.
### Return value

Index of the last added LOD.
## void InsertLod ( int num )

Inserts a new LOD at the specified position.
### Arguments

- *int* **num** - Position to insert a new LOD at.

## void RemoveLod ( int num )

Removes the LOD with the specified number.
### Arguments

- *int* **num** - LOD number.

## void ClearLods ( )

Removes all LODs.
## int Fetch ( BoundSphere bs , BoundBox bb , int force = 0 )

Loads the data of all LODs for the tiles within a given bounding box and a bounding sphere.
### Arguments

- *[BoundSphere](../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.
- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.
- *int* **force** - Force flag. Use 1 to load files in any case; otherwise, 0. The default value is 0.

### Return value

**1** if the data of all LODs was fetched successfully; otherwise, 0.
## TerrainGlobalLod GetLod ( int num )

Returns the LOD with a given number.
### Arguments

- *int* **num** - LOD number.

### Return value

TerrainGlobalLod instance.
## string GetVideoMemoryUsage ( )

Returns information about the total video memory usage for all LODs in the group.
### Return value

Total video memory usage for all LODs.
