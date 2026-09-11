# Unigine.LandscapeMapFileSettings Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to load, modify, and apply [landscape map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_usc.md) settings stored in a `.lmap` file.


### See also


- C++ sample


## LandscapeMapFileSettings Class

### Members

## void setHeightBlending ( int blending )

Sets a new Blending mode used for heights data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive

### Arguments

- *int* **blending** - The Blending mode used for heights data

## int getHeightBlending () const

Returns the current Blending mode used for heights data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive

### Return value

Current Blending mode used for heights data
## void setAlbedoBlending ( int blending )

Sets a new Blending mode used for albedo data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive
- Overlay
- Multiplicative

### Arguments

- *int* **blending** - The Blending mode used for albedo data

## int getAlbedoBlending () const

Returns the current Blending mode used for albedo data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive
- Overlay
- Multiplicative

### Return value

Current Blending mode used for albedo data
## void setEnabledHeight ( int height )

Sets a new Value indicating if heights data of the landscape layer map is to be used.
### Arguments

- *int* **height** - The Value indicating if heights data of the landscape layer map is to be used

## int isEnabledHeight () const

Returns the current Value indicating if heights data of the landscape layer map is to be used.
### Return value

Current Value indicating if heights data of the landscape layer map is to be used
## void setEnabledAlbedo ( int albedo )

Sets a new Value indicating if albedo data of the landscape layer map is to be used.
### Arguments

- *int* **albedo** - The Value indicating if albedo data of the landscape layer map is to be used

## int isEnabledAlbedo () const

Returns the current Value indicating if albedo data of the landscape layer map is to be used.
### Return value

Current Value indicating if albedo data of the landscape layer map is to be used
## void setEnabledOpacityHeight ( int height )

Sets a new Value indicating if opacity information for heights data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **height** - The Value indicating if opacity information for heights data of the landscape layer map is to be used

## int isEnabledOpacityHeight () const

Returns the current Value indicating if opacity information for heights data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Return value

Current Value indicating if opacity information for heights data of the landscape layer map is to be used
## void setEnabledOpacityAlbedo ( int albedo )

Sets a new Value indicating if opacity information for albedo data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **albedo** - The Value indicating if opacity information for albedo data of the landscape layer map is to be used

## int isEnabledOpacityAlbedo () const

Returns the current Value indicating if opacity information for albedo data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Return value

Current Value indicating if opacity information for albedo data of the landscape layer map is to be used
## ivec2 getTilesSize () const

Returns the current Two-component vector (X, Y) representing the number of tiles in the landscape layer map along X and Y axes.
### Return value

Current Two-component vector (X, Y) representing the number of tiles in the landscape layer map along X and Y axes
## ivec2 getResolution () const

Returns the current Two-component vector (X, Y) representing landscape layer map resolution along X and Y axes, in pixels.
### Return value

Current Two-component vector (X, Y) representing landscape layer map resolution along X and Y axes, in pixels
## UGUID getGUID () const

Returns the current [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the `.lmap` file.
### Return value

Current [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the *.lmap* file
## int isLoaded () const

Returns the current value indicating if the landscape map file (`.lmap`) is loaded.
### Return value

Current the file is loaded
## void setAlbedoFadeAttenuation ( vec2 attenuation )

Sets a new Two-component vector **(X, Y)** defining the fade attenuation of the albedo data along X and Y axes.
### Arguments

- *vec2* **attenuation** - The Two-component vector

## vec2 getAlbedoFadeAttenuation () const

Returns the current Two-component vector **(X, Y)** defining the fade attenuation of the albedo data along X and Y axes.
### Return value

Current Two-component vector
## void setHeightFadeAttenuation ( vec2 attenuation )

Sets a new Two-component vector **(X, Y)** defining the fade attenuation of the hight data along X and Y axes.
### Arguments

- *vec2* **attenuation** - The Two-component vector

## vec2 getHeightFadeAttenuation () const

Returns the current Two-component vector **(X, Y)** defining the fade attenuation of the hight data along X and Y axes.
### Return value

Current Two-component vector
## int isEnabledAlbedoTextureCompression () const

Returns the current value indicating if albedo texture compression is enabled.
### Return value

Current albedo texture compression is enabled
## int isEnabledHeightTextureCompression () const

Returns the current value indicating if height texture compression is enabled.
### Return value

Current height texture compression is enabled
## int isEnabledOpacityHeightTextureCompression () const

Returns the current value indicating if opacity height texture compression is enabled.
### Return value

Current opacity height texture compression is enabled
## int isCompressed () const

Returns the current value indicating if the `.lmap` file is compressed.
### Return value

Current the file is compressed
## int getOpacityHeightCompressor () const

Returns the current type of compression currently used for opacity height data.
### Return value

Current type of compression currently used for opacity height data
## int getAlbedoCompressor () const

Returns the current type of compression currently used for opacity albedo data.
### Return value

Current type of compression currently used for opacity albedo data
## int getHeightCompressor () const

Returns the current type of compression currently used for height data.
### Return value

Current type of compression currently used for height data
---

## static LandscapeMapFileSettings ( )

The LandscapeMapFileSettings constructor.
## void setMaskBlending ( int mask , int blend )

Sets a new blending mode to be used for the data of the specified detail mask.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.
- *int* **blend** - Blending mode used for the data of the specified detail mask. One of the following values:

  - Alpha Blend
  - Additive
  - Overlay
  - Multiplicative

## int getMaskBlending ( int mask )

Returns the current blending mode used for the data of the specified detail mask.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.

### Return value

Blending mode used for the data of the specified detail mask. One of the following values:
- Alpha Blend
- Additive
- Overlay
- Multiplicative


## void setEnabledMask ( int mask , int enabled )

Sets a value indicating if the data of the detail mask with the specified number is to be used.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.
- *int* **enabled** - **1** to enable using the data of the specified detail mask, **0** - to disable it.

## int isEnabledMask ( int mask )

Returns a value indicating if the data of the detail mask with the specified number is to be used.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.

### Return value

**1** if the data of the detail mask with the specified number is to be used; otherwise, **0**.
## void setEnabledOpacityMask ( int mask , int enabled )

Sets a value indicating if opacity information for the heights data of the detail mask with the specified number is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.
- *int* **enabled** - **1** to enable using opacity information for the data of the specified detail mask, **0** - to disable it.

## int isEnabledOpacityMask ( int mask )

Returns a value indicating if opacity information for the data of the detail mask with the specified number is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.

### Return value

**1** if opacity information for the data of the detail mask with the specified number is to be used; otherwise, **0**.
## int load ( UGUID guid )

Loads landscape map settings from a file with the specified GUID.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the `.lmap` file containing landscape map data.

### Return value

**1** if landscape map settings were successfully loaded from the file with the specified GUID; otherwise, **0**.
## int apply ( )

Applies all settings stored in the landscape map file (`.lmap`).
### Return value

**1** if landscape map file settings were successfully applied; otherwise, **0**.
## void setMaskFadeAttenuation ( int mask , vec2 fade_attenuation )

Sets a new fade attenuation to be used for the data of the specified detail mask. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Arguments

- *int* **mask** - Mask number.
- *vec2* **fade_attenuation** - Two-component vector **(X, Y)** defining the fade attenuation of the detail mask data along X and Y axes.

## vec2 getMaskFadeAttenuation ( int mask )

Returns the current fade attenuation for the data of the specified detail mask. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Arguments

- *int* **mask** - Mask number.

### Return value

Two-component vector **(X, Y)** defining the fade attenuation of the detail mask data along X and Y axes.
## int getMaskCompressor ( int mask )

Returns the type of compression currently used for the data of the mask with the specified number.
### Arguments

- *int* **mask** - Mask number.

### Return value

Type of compression currently used for the data of the mask with the specified number.
## int getMaskOpacityCompressor ( int mask )

Returns the type of compression currently used for the opacity data of the mask with the specified number.
### Arguments

- *int* **mask** - Mask number.

### Return value

Type of compression currently used for the opacity data of the mask with the specified number.
## int isEnabledMaskTextureCompression ( int mask )

Returns a value indicating if compression of the mask texture for the mask with the specified number is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

**1** if compression of the mask texture for the mask with the specified number is enabled; otherwise, **0**.
## int isEnabledMaskOpacityTextureCompression ( int mask )

Returns a value indicating if compression of the opacity texture for the mask with the specified number is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

**1** if compression of the opacity texture for the mask with the specified number is enabled; otherwise, **0**.
