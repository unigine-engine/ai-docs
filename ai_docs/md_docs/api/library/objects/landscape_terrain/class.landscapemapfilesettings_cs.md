# Unigine.LandscapeMapFileSettings Class (CS)


This class is used to load, modify, and apply [landscape map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) settings stored in a `.lmap` file.


### See also


- C++ sample


## LandscapeMapFileSettings Class

### Properties

## Landscape.BLENDING_MODE HeightBlending

The Blending mode used for heights data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive

## Landscape.BLENDING_MODE AlbedoBlending

The Blending mode used for albedo data. One of the following *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#BLENDING_MODE)* values:
- Alpha Blend
- Additive
- Overlay
- Multiplicative

## bool EnabledHeight

The Value indicating if heights data of the landscape layer map is to be used.
## bool EnabledAlbedo

The Value indicating if albedo data of the landscape layer map is to be used.
## bool EnabledOpacityHeight

The Value indicating if opacity information for heights data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
## bool EnabledOpacityAlbedo

The Value indicating if opacity information for albedo data of the landscape layer map is to be used. Opacity information is required to blend data of several landscape layer maps.
## 🔒︎ ivec2 TilesSize

The Two-component vector (X, Y) representing the number of tiles in the landscape layer map along X and Y axes.
## 🔒︎ ivec2 Resolution

The Two-component vector (X, Y) representing landscape layer map resolution along X and Y axes, in pixels.
## 🔒︎ UGUID GUID

The [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the `.lmap` file.
## 🔒︎ bool IsLoaded

The value indicating if the landscape map file (`.lmap`) is loaded.
## vec2 AlbedoFadeAttenuation

The Two-component vector **(X, Y)** defining the fade attenuation of the albedo data along X and Y axes.
## vec2 HeightFadeAttenuation

The Two-component vector **(X, Y)** defining the fade attenuation of the hight data along X and Y axes.
## 🔒︎ bool IsEnabledAlbedoTextureCompression

The value indicating if albedo texture compression is enabled.
## 🔒︎ bool IsEnabledHeightTextureCompression

The value indicating if height texture compression is enabled.
## 🔒︎ bool IsEnabledOpacityHeightTextureCompression

The value indicating if opacity height texture compression is enabled.
## 🔒︎ bool IsCompressed

The value indicating if the `.lmap` file is compressed.
## 🔒︎ Landscape.COMPRESSOR_TYPE OpacityHeightCompressor

The type of compression currently used for opacity height data.
## 🔒︎ Landscape.COMPRESSOR_TYPE AlbedoCompressor

The type of compression currently used for opacity albedo data.
## 🔒︎ Landscape.COMPRESSOR_TYPE HeightCompressor

The type of compression currently used for height data.
### Members

---

## LandscapeMapFileSettings ( )

The LandscapeMapFileSettings constructor.
## void SetMaskBlending ( int mask , Landscape.BLENDING_MODE blend )

Sets a new blending mode to be used for the data of the specified detail mask.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.
- *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#BLENDING_MODE)* **blend** - Blending mode used for the data of the specified detail mask. One of the following values:

  - Alpha Blend
  - Additive
  - Overlay
  - Multiplicative

## Landscape.BLENDING_MODE GetMaskBlending ( int mask )

Returns the current blending mode used for the data of the specified detail mask.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.

### Return value

Blending mode used for the data of the specified detail mask. One of the following values:
- Alpha Blend
- Additive
- Overlay
- Multiplicative


## void SetEnabledMask ( int mask , bool enabled )

Sets a value indicating if the data of the detail mask with the specified number is to be used.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.
- *bool* **enabled** - true to enable using the data of the specified detail mask, false - to disable it.

## bool IsEnabledMask ( int mask )

Returns a value indicating if the data of the detail mask with the specified number is to be used.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.

### Return value

true if the data of the detail mask with the specified number is to be used; otherwise, false.
## void SetEnabledOpacityMask ( int mask , bool enabled )

Sets a value indicating if opacity information for the heights data of the detail mask with the specified number is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.
- *bool* **enabled** - true to enable using opacity information for the data of the specified detail mask, false - to disable it.

## bool IsEnabledOpacityMask ( int mask )

Returns a value indicating if opacity information for the data of the detail mask with the specified number is to be used. Opacity information is required to blend data of several landscape layer maps.
### Arguments

- *int* **mask** - Detail mask number in the **[0; 19]** range.

### Return value

true if opacity information for the data of the detail mask with the specified number is to be used; otherwise, false.
## bool Load ( UGUID guid )

Loads landscape map settings from a file with the specified GUID.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the `.lmap` file containing landscape map data.

### Return value

true if landscape map settings were successfully loaded from the file with the specified GUID; otherwise, false.
## bool Apply ( )

Applies all settings stored in the landscape map file (`.lmap`).
### Return value

true if landscape map file settings were successfully applied; otherwise, false.
## void SetMaskFadeAttenuation ( int mask , vec2 fade_attenuation )

Sets a new fade attenuation to be used for the data of the specified detail mask. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Arguments

- *int* **mask** - Mask number.
- *vec2* **fade_attenuation** - Two-component vector **(X, Y)** defining the fade attenuation of the detail mask data along X and Y axes.

## vec2 GetMaskFadeAttenuation ( int mask )

Returns the current fade attenuation for the data of the specified detail mask. This parameter defines the distance of the transparency attenuation, starting from the edge of the map.
### Arguments

- *int* **mask** - Mask number.

### Return value

Two-component vector **(X, Y)** defining the fade attenuation of the detail mask data along X and Y axes.
## Landscape.COMPRESSOR_TYPE GetMaskCompressor ( int mask )

Returns the type of compression currently used for the data of the mask with the specified number.
### Arguments

- *int* **mask** - Mask number.

### Return value

Type of compression currently used for the data of the mask with the specified number.
## Landscape.COMPRESSOR_TYPE GetMaskOpacityCompressor ( int mask )

Returns the type of compression currently used for the opacity data of the mask with the specified number.
### Arguments

- *int* **mask** - Mask number.

### Return value

Type of compression currently used for the opacity data of the mask with the specified number.
## bool IsEnabledMaskTextureCompression ( int mask )

Returns a value indicating if compression of the mask texture for the mask with the specified number is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

true if compression of the mask texture for the mask with the specified number is enabled; otherwise, false.
## bool IsEnabledMaskOpacityTextureCompression ( int mask )

Returns a value indicating if compression of the opacity texture for the mask with the specified number is enabled.
### Arguments

- *int* **mask** - Mask number.

### Return value

true if compression of the opacity texture for the mask with the specified number is enabled; otherwise, false.
