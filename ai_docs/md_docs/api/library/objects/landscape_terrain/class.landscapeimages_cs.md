# Unigine.LandscapeImages Class (CS)

This class is used to manage a fragment of terrain data on the CPU side (e.g. modify heights, albedo, or masks, etc.). Actually it represents a data container for a fragment of terrain area of the specified resolution. This class can be used, for example, when implementing CPU-based brushes.


## LandscapeImages Class

### Properties

## 🔒︎ ivec2 Resolution

The image resolution.
### Members

---

## LandscapeImages LandscapeImages ( ivec2 resolution )

Creates a new LandscapeImages object to store the data for a terrain area of the specified resolution.
### Arguments

- *ivec2* **resolution** - Two-component vector containing image resolution along X and Y axes.

### Return value

LandscapeImages instance - a data container for a terrain area of the specified size.
## Image GetHeight ( )

Returns height data as an image.
### Return value

Image (R32F) containing height data.
## Image GetAlbedo ( )

Returns albedo data as an RGBA8 image. Opacity data is stored in the alpha-channel.
### Return value

Image (RGBA8) containing albedo data.
## Image GetMask ( int num )

Returns mask data as an RGBA8 image.
> **Notice:** Each detail mask can be represented by a single-channel image. For optimization purposes detail mask data is stored in blocks - RGBA8 images (each containing 4 masks, one mask per each channel). There are 5 blocks, as the terrain has 20 detail masks available. Thus, the data of the **9**th detail mask shall be stored in the R-channel of the third block (index = 2).

### Arguments

- *int* **num** - Masks data block index.

### Return value

Image (RGBA8) containing mask data.
## Image GetOpacityHeight ( )

Returns opacity information for height data as an R32F image.
### Return value

Image (R32F) containing opacity information for height data.
## Image GetOpacityMask ( int num )

Returns opacity information for mask data as an RGBA8 image.
> **Notice:** Each mask can be represented by a single-channel image. For optimization purposes opacity information for mask data is stored in blocks - RGBA8 images (each containing 4 masks, one mask per each channel). There are 5 blocks, as the terrain has 20 detail masks available. Thus, the data of the **9**th detail mask shall be stored in the R-channel of the third block (index = 2).

### Arguments

- *int* **num** - Masks data block index.

### Return value

Image (RGBA8) containing opacity information for mask data.
## Image Get ( int type )

Returns the image of the specified type.
### Arguments

- *int* **type** - Landscape map data type identifier. One of the [*LANDSCAPE_TYPE_FILE_DATA_**](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#TYPE_FILE_DATA_HEIGHT) values.

### Return value

Image of the specified type.
## void Resize ( ivec2 new_resolution )

Sets a new image resolution.
### Arguments

- *ivec2* **new_resolution** - Two-component vector containing new image resolution along X and Y axes to be set.

## LandscapeImages Copy ( LandscapeImages image )

Copies this LandscapeImages buffer to the specified one (all data layers).
### Arguments

- *[LandscapeImages](../../../../api/library/objects/landscape_terrain/class.landscapeimages_cs.md)* **image** - Destination LandscapeImages buffer to which this one is to be copied.

### Return value

Destination LandscapeImages buffer.
## LandscapeImages Clone ( )

Clones the LandscapeImages buffer (all data layers).
### Return value

Cloned LandscapeImages buffer.
