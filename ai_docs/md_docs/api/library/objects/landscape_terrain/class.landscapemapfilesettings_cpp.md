# Unigine.LandscapeMapFileSettings Class (CPP)

**Header:** #include <UnigineObjects.h>


This class is used to load, modify, and apply [landscape map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) settings stored in a `.lmap` file.


### See also


- C++ sample


## LandscapeMapFileSettings Class

### Members

## void setHeightBlending ( Landscape::BLENDING_MODE blending )

Sets a new Blending mode used for heights data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive

### Arguments

- *[Landscape::BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#BLENDING_MODE)* **blending** - The Blending mode used for heights data

## Landscape::BLENDING_MODE getHeightBlending () const

Returns the current Blending mode used for heights data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive

### Return value

Current Blending mode used for heights data
## void setAlbedoBlending ( Landscape::BLENDING_MODE blending )

Sets a new Blending mode used for albedo data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive
- Overlay
- Multiplicative

### Arguments

- *[Landscape::BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#BLENDING_MODE)* **blending** - The Blending mode used for albedo data

## Landscape::BLENDING_MODE getAlbedoBlending () const

Returns the current Blending mode used for albedo data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive
- Overlay
- Multiplicative

### Return value

Current Blending mode used for albedo data
## void setEnabledHeight ( bool height )

Sets a new Value indicating if heights data of the landscape layer map is to be used.
### Arguments

- *bool* **height** - Value indicating if heights data of the landscape layer map is to be used

## bool isEnabledHeight () const

Returns the current Value indicating if heights data of the landscape layer map is to be used.
### Return value

Value indicating if heights data of the landscape layer map is to be used
## void setEnabledAlbedo ( bool albedo )

Sets a new Value indicating if albedo data of the landscape layer map is to be used.
### Arguments

- *bool* **albedo** - Value indicating if albedo data of the landscape layer map is to be used

## bool isEnabledAlbedo () const

Returns the current Value indicating if albedo data of the landscape layer map is to be used.
### Return value

Value indicating if albedo data of the landscape layer map is to be used
## void setEnabledOpacityHeight ( bool height )

Sets a new Value indicating if opacity information for heights data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *bool* **height** - Value indicating if opacity information for heights data of the landscape layer map is to be used

## bool isEnabledOpacityHeight () const

Returns the current Value indicating if opacity information for heights data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Return value

Value indicating if opacity information for heights data of the landscape layer map is to be used
## void setEnabledOpacityAlbedo ( bool albedo )

Sets a new Value indicating if opacity information for albedo data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *bool* **albedo** - Value indicating if opacity information for albedo data of the landscape layer map is to be used

## bool isEnabledOpacityAlbedo () const

Returns the current Value indicating if opacity information for albedo data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Return value

Value indicating if opacity information for albedo data of the landscape layer map is to be used
## Math:: ivec2 getTilesSize () const

Returns the current Two-component vector (X, Y) representing the number of tiles in the landscape layer map along X and Y axes.
### Return value

Current Two-component vector (X, Y) representing the number of tiles in the landscape layer map along X and Y axes
## Math:: ivec2 getResolution () const

Returns the current Two-component vector (X, Y) representing landscape layer map resolution along X and Y axes, in pixels.
### Return value

Current Two-component vector (X, Y) representing landscape layer map resolution along X and Y axes, in pixels
## UGUID getGUID () const

Returns the current [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the `.lmap` file.
### Return value

Current [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the *.lmap* file
## bool isLoaded () const

Returns the current value indicating if the landscape map file (`.lmap`) is loaded.
### Return value

**true** if the file is loaded; otherwise **false**.
## void setAlbedoFadeAttenuation ( const Math:: vec2 & attenuation )

Sets a new Two-component vector **(X, Y)** defining the fade attenuation of the albedo data along X and Y axes.
### Arguments

- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md)&* **attenuation** - The Two-component vector

## Math:: vec2 getAlbedoFadeAttenuation () const

Returns the current Two-component vector **(X, Y)** defining the fade attenuation of the albedo data along X and Y axes.
### Return value

Current Two-component vector
## void setHeightFadeAttenuation ( const Math:: vec2 & attenuation )

Sets a new Two-component vector **(X, Y)** defining the fade attenuation of the hight data along X and Y axes.
### Arguments

- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md)&* **attenuation** - The Two-component vector

## Math:: vec2 getHeightFadeAttenuation () const

Returns the current Two-component vector **(X, Y)** defining the fade attenuation of the hight data along X and Y axes.
### Return value

Current Two-component vector
## bool isEnabledAlbedoTextureCompression () const

Returns the current value indicating if albedo texture compression is enabled.
### Return value

**true** if albedo texture compression is enabled; otherwise **false**.
## bool isEnabledHeightTextureCompression () const

Returns the current value indicating if height texture compression is enabled.
### Return value

**true** if height texture compression is enabled; otherwise **false**.
## bool isEnabledOpacityHeightTextureCompression () const

Returns the current value indicating if opacity height texture compression is enabled.
### Return value

**true** if opacity height texture compression is enabled; otherwise **false**.
## bool isCompressed () const

Returns the current value indicating if the `.lmap` file is compressed.
### Return value

**true** if the file is compressed; otherwise **false**.
## Landscape::COMPRESSOR_TYPE getOpacityHeightCompressor () const

Returns the current type of compression currently used for opacity height data.
### Return value

Current type of compression currently used for opacity height data
## Landscape::COMPRESSOR_TYPE getAlbedoCompressor () const

Returns the current type of compression currently used for opacity albedo data.
### Return value

Current type of compression currently used for opacity albedo data
## Landscape::COMPRESSOR_TYPE getHeightCompressor () const

Returns the current type of compression currently used for height data.
### Return value

Current type of compression currently used for height data
---

## static LandscapeMapFileSettingsPtr create ( )

The LandscapeMapFileSettings constructor.
## void setMaskBlending ( int mask , Landscape::BLENDING_MODE blend )

Sets a new blending mode to be used for the data of the specified detail mask.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.
- *[Landscape::BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#BLENDING_MODE)* **blend** - Blending mode used for the data of the specified detail mask. One of the following values:

  - Alpha Blend
  - Additive
  - Overlay
  - Multiplicative

## Landscape::BLENDING_MODE getMaskBlending ( int mask ) const

Returns the current blending mode used for the data of the specified detail mask.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.

### Return value

Blending mode used for the data of the specified detail mask. One of the following values:
- Alpha Blend
- Additive
- Overlay
- Multiplicative


## void setEnabledMask ( int mask , bool enabled )

Sets a value indicating if the data of the detail mask with the specified number is to be used.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.
- *bool* **enabled** - true to enable using the data of the specified detail mask, false - to disable it.

## bool isEnabledMask ( int mask ) const

Returns a value indicating if the data of the detail mask with the specified number is to be used.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.

### Return value

true if the data of the detail mask with the specified number is to be used; otherwise, false.
## void setEnabledOpacityMask ( int mask , bool enabled )

Sets a value indicating if opacity information for the heights data of the detail mask with the specified number is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.
- *bool* **enabled** - true to enable using opacity information for the data of the specified detail mask, false - to disable it.

## bool isEnabledOpacityMask ( int mask ) const

Returns a value indicating if opacity information for the data of the detail mask with the specified number is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.

### Return value

true if opacity information for the data of the detail mask with the specified number is to be used; otherwise, false.
## bool load ( const UGUID & guid )

Loads landscape map settings from a file with the specified GUID.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the `.lmap` file containing landscape map data.

### Return value

true if landscape map settings were successfully loaded from the file with the specified GUID; otherwise, false.
## bool apply ( )

Applies all settings stored in the landscape map file (`.lmap`).
### Return value

true if landscape map file settings were successfully applied; otherwise, false.
## void setMaskFadeAttenuation ( int mask , const Math:: vec2 & fade_attenuation )

Sets a new fade attenuation to be used for the data of the specified detail mask. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Arguments

- *int* **mask** - Mask number.
- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) &* **fade_attenuation** - Two-component vector **(X, Y)** defining the fade attenuation of the detail mask data along X and Y axes.

## Math:: vec2 getMaskFadeAttenuation ( int mask ) const

Returns the current fade attenuation for the data of the specified detail mask. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Arguments

- *int* **mask** - Mask number.

### Return value

Two-component vector **(X, Y)** defining the fade attenuation of the detail mask data along X and Y axes.
## Landscape::COMPRESSOR_TYPE getMaskCompressor ( int mask )

Returns the type of compression currently used for the data of the mask with the specified number.
### Arguments

- *int* **mask** - Mask number.

### Return value

Type of compression currently used for the data of the mask with the specified number.
## Landscape::COMPRESSOR_TYPE getMaskOpacityCompressor ( int mask )

Returns the type of compression currently used for the opacity data of the mask with the specified number.
### Arguments

- *int* **mask** - Mask number.

### Return value

Type of compression currently used for the opacity data of the mask with the specified number.
## bool isEnabledMaskTextureCompression ( int mask )

Returns a value indicating if compression of the mask texture for the mask with the specified number is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

true if compression of the mask texture for the mask with the specified number is enabled; otherwise, false.
## bool isEnabledMaskOpacityTextureCompression ( int mask )

Returns a value indicating if compression of the opacity texture for the mask with the specified number is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

true if compression of the opacity texture for the mask with the specified number is enabled; otherwise, false.
