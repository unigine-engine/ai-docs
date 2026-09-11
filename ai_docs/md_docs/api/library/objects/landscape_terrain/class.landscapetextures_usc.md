# Unigine.LandscapeTextures Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage a fragment of terrain data on the GPU side (e.g. modify heights, albedo, or masks, etc.). Actually it represents a data container for a fragment of terrain area of the specified resolution. This class can be used, for example, when implementing GPU-based brushes.


## LandscapeTextures Class

### Members

## int getNumMipmaps () const

Returns the current total number of mipmaps for the textures (maximum value among all data layers).
### Return value

Current total number of mipmaps for the textures (maximum value among all data layers)
## ivec2 getResolution () const

Returns the current texture resolution.
### Return value

Current texture resolution
## RenderTarget getRenderTarget () const

Returns the current [render target](../../../../api/library/rendering/class.rendertarget_usc.md) containing terrain data.
### Return value

Current [render target](../../../../api/library/rendering/class.rendertarget_usc.md) containing terrain data
## Texture getOpacityHeight () const

Returns the current Opacity information for height data as an r32f texture.
### Return value

Current Opacity information for height data as an r32f texture
## Texture getAlbedo () const

Returns the current Albedo data as an rgba8 texture. opacity data is stored in the alpha-channel.
### Return value

Current Albedo data as an rgba8 texture
## Texture getHeight () const

Returns the current Height data as an r32f texture.
### Return value

Current Height data as an r32f texture
---

## LandscapeTextures LandscapeTextures ( ivec2 resolution )

Creates a new LandscapeTextures object to store the data for a terrain area of the specified resolution.
### Arguments

- *ivec2* **resolution** - Two-component vector containing texture resolution along X and Y axes.

## Texture getMask ( int num )

Returns mask data as an RGBA8 texture.
> **Notice:** Each detail mask can be represented by a single-channel texture. For optimization purposes detail mask data is stored in blocks - RGBA8 textures (each containing 4 masks, one mask per each channel). There are 5 blocks, as the terrain has 20 detail masks available. Thus, the data of the **9**th detail mask shall be stored in the R-channel of the third block (index = 2).

### Arguments

- *int* **num** - Masks data block index.

### Return value

Texture (RGBA8) containing mask data.
## Texture getOpacityMask ( int num )

Returns opacity information for mask data as an RGBA8 texture.
> **Notice:** Each mask can be represented by a single-channel texture. For optimization purposes opacity information for mask data is stored in blocks - RGBA8 textures (each containing 4 masks, one mask per each channel). There are 5 blocks, as the terrain has 20 detail masks available. Thus, the data of the **9**th detail mask shall be stored in the R-channel of the third block (index = 2).

### Arguments

- *int* **num** - Masks data block index.

### Return value

Texture (RGBA8) containing opacity information for mask data.
## Texture get ( int type )

Returns the texture of the specified type.
### Arguments

- *int* **type** - Landscape map data type identifier. One of the [*LANDSCAPE_TYPE_FILE_DATA_**](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#TYPE_FILE_DATA_HEIGHT) values.

### Return value

Texture of the specified type.
## void createMipmaps ( )

Generates mipmaps for the textures of all data layers.
## void clearBuffers ( )

Clears all levels of the textures of all data layers (fills all elements with 0-values).
