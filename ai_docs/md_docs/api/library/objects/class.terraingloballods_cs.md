# Unigine.TerrainGlobalLods Class (CS)


This class is used to manage a group of [LODs](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalLods Class

### Properties

## 🔒︎ int NumLods

The total number of lods in the group.
## int NumLayers

The number of layers of the lod group.
## 🔒︎ int MaskFormat

The value indicating current image format for the tile mask. One of the [Image::FORMAT_*](../../../api/library/common/class.image_cs.md) values.
## 🔒︎ int DataFormat

The value indicating current image format for the tile data. One of the [Image::FORMAT_*](../../../api/library/common/class.image_cs.md#FORMAT_ATI1) values.
## 🔒︎ int DataType

The value indicating current image type for the tile data. One of the [Image::IMAGE_*](../../../api/library/common/class.image_cs.md#IMAGE_2D) values.
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
## int FetchData ( double x , double y , Image.Pixel ret_pixel , int layer , bool force )

Fetches the data for the point on the terrain with given coordinates and puts it to the specified output structure.
### Arguments

- *double* **x** - X coordinate of the point on the terrain.
- *double* **y** - Y coordinate of the point on the terrain.
- *[Image.Pixel](../../../api/library/common/class.image_cs.md#Pixel)* **ret_pixel** - Output [Pixel structure](../../../api/library/common/class.image_cs.md#pixel) to store the pixel color.
- *int* **layer** - Layer number.
- *bool* **force** - Force flag. > **Notice:** It is recommended to set this flag to 0 when possible to avoid spikes. .

  - If 1 is specified, the data will be fetched immediately.
  - If 0 is specified, the operation will be queued to a separate thread.

### Return value

**1** if the data for the specified pixel was fetched successfully; otherwise, 0.
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
