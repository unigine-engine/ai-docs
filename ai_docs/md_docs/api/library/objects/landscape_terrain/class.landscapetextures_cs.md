# Unigine.LandscapeTextures Class (CS)


This class is used to manage a fragment of terrain data on the GPU side (e.g. modify heights, albedo, or masks, etc.). Actually it represents a data container for a fragment of terrain area of the specified resolution. This class can be used, for example, when implementing GPU-based brushes.


## LandscapeTextures Class

### Properties

## 🔒︎ int NumMipmaps

The total number of mipmaps for the textures (maximum value among all data layers).
## 🔒︎ ivec2 Resolution

The texture resolution.
## 🔒︎ RenderTarget RenderTarget

The [render target](../../../../api/library/rendering/class.rendertarget_cs.md) containing terrain data.
## 🔒︎ Texture OpacityHeight

The Opacity information for height data as an r32f texture.
## 🔒︎ Texture Albedo

The Albedo data as an rgba8 texture. opacity data is stored in the alpha-channel.
## 🔒︎ Texture Height

The Height data as an r32f texture.
### Members

---

## LandscapeTextures LandscapeTextures ( ivec2 resolution )

Creates a new LandscapeTextures object to store the data for a terrain area of the specified resolution.
### Arguments

- *ivec2* **resolution** - Two-component vector containing texture resolution along X and Y axes.

## Texture GetMask ( int num )

Returns mask data as an RGBA8 texture.
> **Notice:** Each detail mask can be represented by a single-channel texture. For optimization purposes detail mask data is stored in blocks - RGBA8 textures (each containing 4 masks, one mask per each channel). There are 5 blocks, as the terrain has 20 detail masks available. Thus, the data of the **9**th detail mask shall be stored in the R-channel of the third block (index = 2).

### Arguments

- *int* **num** - Masks data block index.

### Return value

Texture (RGBA8) containing mask data.
## Texture GetOpacityMask ( int num )

Returns opacity information for mask data as an RGBA8 texture.
> **Notice:** Each mask can be represented by a single-channel texture. For optimization purposes opacity information for mask data is stored in blocks - RGBA8 textures (each containing 4 masks, one mask per each channel). There are 5 blocks, as the terrain has 20 detail masks available. Thus, the data of the **9**th detail mask shall be stored in the R-channel of the third block (index = 2).

### Arguments

- *int* **num** - Masks data block index.

### Return value

Texture (RGBA8) containing opacity information for mask data.
## Texture Get ( int type )

Returns the texture of the specified type.
### Arguments

- *int* **type** - Landscape map data type identifier. One of the [*LANDSCAPE_TYPE_FILE_DATA_**](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#TYPE_FILE_DATA_HEIGHT) values.

### Return value

Texture of the specified type.
## void CreateMipmaps ( )

Generates mipmaps for the textures of all data layers.
## void ClearBuffers ( )

Clears all levels of the textures of all data layers (fills all elements with 0-values).
