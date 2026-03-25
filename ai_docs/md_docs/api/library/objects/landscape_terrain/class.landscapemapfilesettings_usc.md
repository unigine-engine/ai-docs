# Unigine.LandscapeMapFileSettings Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to load, modify, and apply [landscape map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_usc.md) settings stored in a `.lmap` file.


### See also


- C++ sample


## LandscapeMapFileSettings Class

### Members

---

## static LandscapeMapFileSettings ( )

The LandscapeMapFileSettings constructor.
## void setHeightBlending ( int blending )

Sets a new blending mode to be used for heights data of the landscape map.
### Arguments

- *int* **blending** - Blending mode to be used for heights data. One of the following values:

  - Alpha Blend
  - Additive

## int getHeightBlending ( )

Returns the current blending mode used for heights data of the landscape map.
### Return value

Blending mode used for heights data. One of the following values:
- Alpha Blend
- Additive


## void setAlbedoBlending ( int blending )

Sets a new blending mode to be used for albedo data of the landscape map.
### Arguments

- *int* **blending** - Blending mode to be used for albedo data. One of the following values:

  - Alpha Blend
  - Additive
  - Overlay
  - Multiplicative

## int getAlbedoBlending ( )

Returns the current blending mode used for albedo data of the landscape map.
### Return value

Blending mode used for albedo data. One of the following values:
- Alpha Blend
- Additive
- Overlay
- Multiplicative


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


## void setEnabledHeight ( int height )

Sets a value indicating if heights data of the landscape layer map is to be used.
### Arguments

- *int* **height** - **1** to enable using heights data of the landscape layer map, **0** - to disable it.

## int isEnabledHeight ( )

Returns a value indicating if heights data of the landscape layer map is to be used.
### Return value

**1** if heights data of the landscape layer map is to be used; otherwise, **0**.
## void setEnabledAlbedo ( int albedo )

Sets a value indicating if albedo data of the landscape layer map is to be used.
### Arguments

- *int* **albedo** - **1** to enable using albedo data of the landscape layer map, **0** - to disable it.

## int isEnabledAlbedo ( )

Returns a value indicating if albedo data of the landscape layer map is to be used.
### Return value

**1** if albedo data of the landscape layer map is to be used; otherwise, **0**.
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
## void setEnabledOpacityHeight ( int height )

Sets a value indicating if opacity information for heights data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **height** - **1** to enable using opacity information for heights data of the landscape layer map, **0** - to disable it.

## int isEnabledOpacityHeight ( )

Returns a value indicating if opacity information for heights data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Return value

**1** if opacity information for heights data of the landscape layer map is to be used; otherwise, **0**.
## void setEnabledOpacityAlbedo ( int albedo )

Sets a value indicating if opacity information for albedo data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **albedo** - **1** to enable using opacity information for albedo data of the landscape layer map, **0** - to disable it.

## int isEnabledOpacityAlbedo ( )

Returns a value indicating if opacity information for the albedo data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
### Return value

**1** if opacity information for the albedo data of the landscape layer map is to be used; otherwise, **0**.
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
## ivec2 getTilesSize ( )

Returns the size of the landscape map tiles.
### Return value

Two-component vector (X, Y) representing the number of tiles in the landscape layer map along X and Y axes.
## ivec2 getResolution ( )

Returns the landscape layer map resolution.
### Return value

Two-component vector (X, Y) representing landscape layer map resolution along X and Y axes, in pixels.
## UGUID getGUID ( )

Returns a [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the `.lmap` file containing landscape map data.
### Return value

[GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the `.lmap` file.
## int isLoaded ( )

Returns a value indicating if the landscape map file (`.lmap`) is loaded.
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
## void setHeightFadeAttenuation ( vec2 attenuation )

Sets a new fade attenuation to be used for heights data of the landscape map. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Arguments

- *vec2* **attenuation** - Two-component vector **(X, Y)** defining the fade attenuation of the height data along X and Y axes.

## vec2 getHeightFadeAttenuation ( )

Returns the current fade attenuation for heights data of the landscape map. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Return value

Two-component vector **(X, Y)** defining the fade attenuation of the height data along X and Y axes.
## void setAlbedoFadeAttenuation ( vec2 attenuation )

Sets a new fade attenuation to be used for albedo data of the landscape map. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Arguments

- *vec2* **attenuation** - Two-component vector **(X, Y)** defining the fade attenuation of the albedo data along X and Y axes.

## vec2 getAlbedoFadeAttenuation ( )

Returns the current fade attenuation for albedo data of the landscape map. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Return value

Two-component vector **(X, Y)** defining the fade attenuation of the albedo data along X and Y axes.
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
## int getHeightCompressor ( )

Returns the type of compression currently used for height data.
### Return value

Type of compression currently used for height data.
## int getAlbedoCompressor ( )

Returns the type of compression currently used for albedo data.
### Return value

Type of compression currently used for albedo data.
## int getOpacityHeightCompressor ( )

Returns the type of compression currently used for opacity height data.
### Return value

Type of compression currently used for opacity height data.
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
## int isCompressed ( )

Returns the value indicating if the `.lmap` file is compressed.
### Return value

**1** if the file is compressed; otherwise, **0**.
## int isEnabledAlbedoTextureCompression ( )

Returns a value indicating if albedo texture compression is enabled.
### Return value

**1** if albedo texture compression is enabled; otherwise, **0**.
## int isEnabledHeightTextureCompression ( )

Returns a value indicating if height texture compression is enabled.
### Return value

**1** if height texture compression is enabled; otherwise, **0**.
## int isEnabledOpacityHeightTextureCompression ( )

Returns a value indicating if opacity height texture compression is enabled.
### Return value

**1** if opacity height texture compression is enabled; otherwise, **0**.
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
