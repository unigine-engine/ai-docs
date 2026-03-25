# Unigine.TerrainGlobalLods Class (CPP)

**Header:** #include <UnigineObjects.h>


This class is used to manage a group of [LODs](../../../objects/objects/terrain/terrain_global/index.md#lods) (level of detail) of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalLods Class

### Members

---

## int getDataFormat ( )

Returns a value indicating current image format for the tile data.
### Return value

Tile data image format. One of the [Image::FORMAT_*](../../../api/library/common/class.image_cpp.md#FORMAT_ATI1) values.
## int getDataType ( )

Returns a value indicating current image format for the tile data.
### Return value

Tile data image type. One of the [Image::IMAGE_*](../../../api/library/common/class.image_cpp.md#IMAGE_2D) values.
## int getMaskFormat ( )

Returns a value indicating current image format for the tile mask.
### Return value

Tile mask image format. One of the [Image::FORMAT_*](../../../api/library/common/class.image_cpp.md#FORMAT_ATI1) values.
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
## int fetch ( const BoundSphere & bs , const BoundBox & bb , int force = 0 )

Loads the data of all LODs for the tiles within a given bounding box and a bounding sphere.
### Arguments

- *const [BoundSphere](../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.
- *const [BoundBox](../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.
- *int* **force** - Force flag. Use 1 to load files in any case; otherwise, 0. The default value is 0.

### Return value

**1** if the data of all LODs was fetched successfully; otherwise, 0.
## int fetchData ( double x , double y , Pixel & ret_pixel , int layer , bool force )

Fetches the data for the point on the terrain with given coordinates and puts it to the specified output structure.
### Arguments

- *double* **x** - X coordinate of the point on the terrain.
- *double* **y** - Y coordinate of the point on the terrain.
- *Pixel &* **ret_pixel** - Output [Pixel structure](../../../api/library/common/class.image_cpp.md#pixel) to store the pixel color.
- *int* **layer** - Layer number.
- *bool* **force** - Force flag. > **Notice:** It is recommended to set this flag to 0 when possible to avoid spikes. .

  - If 1 is specified, the data will be fetched immediately.
  - If 0 is specified, the operation will be queued to a separate thread.

### Return value

**1** if the data for the specified pixel was fetched successfully; otherwise, 0.
## int getType ( )

Returns the type of LODs.
## const char * getName ( )

Returns the name of the LOD group.
### Return value

LOD group name.
## Ptr < TerrainGlobalLod > getLod ( int num )

Returns the LOD with a given number.
### Arguments

- *int* **num** - LOD number.

### Return value

Pointer to TerrainGlobalLod.
## String getVideoMemoryUsage ( )

Returns information about the total video memory usage for all LODs in the group.
### Return value

Total video memory usage for all LODs.
