# Unigine.TileSet Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage a regular [tileset](../../../objects/objects/terrain/terrain_global/index.md#tiling) of the ObjectTerrainGlobal. The tileset can have an arbitrary number of tiles. Each tile is represented by the following elements:


- **Data** - an image with tile data.
- **Mask** - a single-channel image describing data weights. > **Notice:** In case if a tile has no mask, all weights are considered equal to 1.


## Tileset Class

---

## int getImageType ( )

Returns a numerical code of the image type used in the tileset.
### Return value

Image type identifier. See the [FORMAT_*](../../../api/library/common/class.image_usc.md#FORMAT_ATI1) variables.
## int setTileData ( const ivec2 & tile_coord , const Image & data )

Sets the data for the specified tile by copying from the source image.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).
- *const [Image](../../../api/library/common/class.image_usc.md) &* **data** - Source image containing a new tile data to be set.

### Return value

1 if the data of the tile was successfully set; otherwise, 0.
## int getTileData ( const ivec2 & tile_coord , Image & data , int force = 1 )

Copies the data of the specified tile to the given image instance.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).
- *[Image](../../../api/library/common/class.image_usc.md) &* **data** - Image to which the tile data is to be copied.
- *int* **force** - Force flag. > **Notice:** It is recommended to set this flag to 0 when possible to avoid spikes.

  - If 1 is specified, the data will be copied immediately.
  - If 0 is specified, data copy operation will be queued to a separate thread.

### Return value

1 if the tile data was successfully copied to the image; otherwise, 0.
## int getTileDataState ( const ivec2 & tile_coord )

Returns the state of the data for the tile with specified coordinates.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

Tile data state. One of the [TILE_STATE_*](#TILE_STATE_NONE) values.
## int getTileResolution ( )

Returns the tile resolution of the tileset.
### Return value

Tile resolution, in pixels.
> **Notice:** Tiles are square and have the same number of pixels in both dimensions.


## ivec2 getTileCoord ( const dvec2 & flat_position )

Returns the coordinates of the tile containing the given point on the terrain.
### Arguments

- *const dvec2 &* **flat_position** - Coordinates of the point on the terrain (X, Y).

### Return value

Tile coordinates in the tileset (X, Y).
## int reloadTileData ( const ivec2 & tile_coord )

Reloads the data for the tile with specified coordinates from the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if the tile data was successfully loaded from the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md); otherwise, 0.
## dvec2 getTilePixelFlatPosition ( const ivec2 & tile_coord , const vec2 & pixel_coord , int use_half_pixel_offset = 0 )

Returns the coordinates of the point on the terrain (X, Y) corresponding to the specified pixel of the given tile.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).
- *const vec2 &* **pixel_coord** - Pixel coordinates on the tile (X, Y).
- *int* **use_half_pixel_offset** - 1 to use half-pixel offset; 0 to use zero-offset.

### Return value

Coordinates of the point on the terrain (X, Y).
## int isTileMaskLoaded ( const ivec2 & tile_coord )

Returns a value indicating if a mask is loaded for the tile with the specified coordinates.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if a mask is loaded for the tile; otherwise, 0.
## vec2 getTilePixelCoord ( const dvec2 & flat_position , int use_half_pixel_offset = 0 )

Returns the local tile coordinates of the pixel corresponding to the specified point on the terrain. To determine the tile that contains this pixel use the [getTileCoord()](#getTileCoord_dvec2_ivec2) method.
### Arguments

- *const dvec2 &* **flat_position** - Coordinates of the point on the terrain (X, Y).
- *int* **use_half_pixel_offset** - 1 to use half-pixel offset; 0 to use zero-offset.

### Return value

Local tile coordinates of the pixel (X, Y).
## int saveTile ( const ivec2 & tile_coord , int force = 0 )

Saves changes of the specified tile to the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).
- *int* **force** - Force flag. > **Notice:** It is recommended to set this flag to 0 when possible to avoid spikes.

  - If 1 is specified, the changes will be saved immediately.
  - If 0 is specified, the saving operation will be queued to a separate thread.

### Return value

1 if changes of the specified tile were successfully saved to the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md); otherwise, 0.
## int saveAll ( int force = 1 )

Saves changes of all tiles to the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).
### Arguments

- *int* **force** - Force flag. > **Notice:** It is recommended to set this flag to 0 when possible to avoid spikes.

  - If 1 is specified, the changes will be saved immediately.
  - If 0 is specified, the saving operation will be queued to a separate thread.

### Return value

1 if all changes were successfully saved to the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md); otherwise, 0.
## float getLifeTime ( const ivec2 & tile_coord )

Returns the current lifetime of the tile. This parameter determines how long the specified tile will be kept in the RAM without being accessed.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

Tile lifetime, in seconds.
## int getDataFormat ( )

Returns a value indicating current image format for the tile data.
### Return value

Tile data image format. One of the [IMAGE_FORMAT_*](../../../api/library/common/class.image_usc.md#FORMAT_ATI1) values.
## int getMaskFormat ( )

Returns a value indicating current image format for the tile mask.
### Return value

Tile mask image format. One of the [IMAGE_FORMAT_*](../../../api/library/common/class.image_usc.md#FORMAT_ATI1) values.
## string getPath ( )

Returns the path to the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).
### Return value

Path to the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).
## int getTileMask ( const ivec2 & tile_coord , Image & mask , int force = 1 )

Copies the mask of the specified tile to the given image instance.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).
- *[Image](../../../api/library/common/class.image_usc.md) &* **mask** - Image to which the tile mask is to be copied.
- *int* **force** - Force flag. > **Notice:** It is recommended to set this flag to 0 when possible to avoid spikes.

  - If 1 is specified, the mask will be copied immediately.
  - If 0 is specified, mask copy operation will be queued to a separate thread.

### Return value

1 if the tile mask was successfully copied to the image; otherwise, 0.
## int removeTileMask ( const ivec2 & tile_coord )

Removes the mask of the tile with specified coordinates from the tileset.
> **Notice:** This method does not remove the mask from the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).


### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if the mask of the tile was successfully removed from the tileset; otherwise, 0.
## int setTileMask ( const ivec2 & tile_coord , const Image & mask )

Sets the mask for the specified tile by copying it from the source image.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).
- *const [Image](../../../api/library/common/class.image_usc.md) &* **mask** - Source image containing a new tile mask to be set.

### Return value

1 if the mask of the tile was successfully set; otherwise, 0.
## int reloadTileMask ( const ivec2 & tile_coord )

Reloads the mask for the tile with specified coordinates from the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if the tile mask was successfully loaded from the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md); otherwise, 0.
## float getTileDensity ( )

Returns the tile density (number of pixels per unit) of the tileset.
### Return value

Tile density, in pixels per unit.
## int hasTileFileMask ( const ivec2 & tile_coord )

Returns a value indicating if the tile with specified coordinates has a mask in the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if the specified tile has a mask in the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md); otherwise, 0.
## int hasTileMask ( const ivec2 & tile_coord )

Returns a value indicating if the tile with specified coordinates has a mask in the tileset.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if the specified tile has a mask in the tileset; otherwise, 0.
## int isTileDataLoaded ( const ivec2 & tile_coord )

Returns a value indicating if data is loaded for the tile with the specified coordinates.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if data is loaded for the tile; otherwise, 0.
## int getTileMaskState ( const ivec2 & tile_coord )

Returns the state of the mask for the tile with specified coordinates.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

Tile mask state. One of the [TILE_STATE_*](#TILE_STATE_NONE) values.
## float getTileSize ( )

Returns actual tile size in the tileset.
### Return value

Tile size, in units.
## int hasTile ( const ivec2 & tile_coord )

Returns a value indicating if there is a tile with specified coordinates in the tileset.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if there is a tile with specified coordinates in the tileset; otherwise, 0.
## int hasTileFile ( const ivec2 & tile_coord )

Returns a value indicating if there is a tile with specified coordinates in the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if there is a tile with specified coordinates in the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md); otherwise, 0.
## int removeTile ( const ivec2 & tile_coord )

Removes the tile with specified coordinates from the tileset.
> **Notice:** This method does not remove the tile from the [tileset file](../../../api/library/objects/class.tilesetfile_usc.md).


### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

1 if the tile was successfully removed from the tileset; otherwise, 0.
## int setLifeTime ( const ivec2 & tile_coord , float seconds )

Sets the lifetime for the specified tile This parameter determines how long the specified tile will be kept in the RAM without being accessed.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).
- *float* **seconds** - Tile lifetime, in seconds.

### Return value

1 if the lifetime for the specified tile was successfully set; otherwise, 0.
## dvec2 getTileFlatPosition ( const ivec2 & tile_coord )

Returns the coordinates of the point on the terrain (X, Y) corresponding to the top-left corner of the specified tile.
### Arguments

- *const ivec2 &* **tile_coord** - Tile coordinates in the tileset (X, Y).

### Return value

Coordinates of the point on the terrain (X, Y).
