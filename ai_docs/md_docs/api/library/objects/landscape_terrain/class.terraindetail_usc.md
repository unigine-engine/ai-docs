# Unigine.TerrainDetail Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage details of the [Landscape Terrain Object](../../../../objects/objects/terrain/landscape_terrain/index.md). Details, define terrain's appearance, each of them can have an unlimited number of children. Details are attached to [detail masks](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_usc.md) and are rendered in accordance with their rendering order (the one with the highest order shall be rendered above all others).


## TerrainDetail Class

### Members

---

## void setName ( string name )

Sets a new name for the detail.
### Arguments

- *string* **name** - New terrain detail name to be set.

## string getName ( )

Returns the name of the detail.
### Return value

Current name of the detail.
## void setEnabled ( int enabled )

Sets a value indicating if the terrain detail is enabled.
### Arguments

- *int* **enabled** - **1** to enable the terrain detail, **0** - to disable it.

## int isEnabled ( )

Returns a value indicating if the terrain detail is enabled.
### Return value

**1** if the terrain detail is enabled; otherwise, **0**.
## int isActive ( )

Returns a value indicating if the terrain detail is active.
### Return value

**1** if the terrain detail is active; otherwise, **0**.
## void setMaskByAlbedo ( vec4 albedo )

Sets a new color to be used as a mask for the detail. In this case, all areas on the terrain having selected color will be covered by the detail.
### Arguments

- *vec4* **albedo** - Four-component vector (R, G, B, A) representing a new color to be used as a mask for the detail.

## vec4 getMaskByAlbedo ( )

Returns the color currently used as a mask for the detail. In this case, all areas on the terrain having selected color will be covered by the detail.
### Return value

Four-component vector (R, G, B, A) representing a color currently used as a mask for the detail.
## void setMinVisibleHeight ( float height )

Sets the minimum height value for the detail, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Minimum height value for the detail, in units. The default value is -inf.

## float getMinVisibleHeight ( )

Returns the minimum height value for the detail, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by height.
### Return value

Minimum height value for the detail, in units.
## void setMaxVisibleHeight ( float height )

Sets the maximum height value for the detail, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Maximum height value for the detail, in units. The default value is inf.

## float getMaxVisibleHeight ( )

Returns the maximum height value for the detail, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
### Return value

Maximum height value for the detail, in units.
## void setMinFadeHeight ( float height )

Sets the fade in height range for the detail. Over this height range below the [minimum height value](#setMinVisibleHeight_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Fade in height range value for the detail, in units.

## float getMinFadeHeight ( )

Returns the current fade in height range for the detail. Over this height range below the [minimum height value](#setMinVisibleHeight_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
### Return value

Fade in height range value for the detail, in units.
## void setMaxFadeHeight ( float height )

Sets the fade out height range for the detail. Over this height range below the [maximum height value](#setMaxVisibleHeight_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Fade out height range value for the detail, in units.

## float getMaxFadeHeight ( )

Returns the current fade out height range for the detail. Over this height range below the [maximum height value](#setMaxVisibleHeight_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
### Return value

Fade out height range value for the detail, in units.
## void setMinVisibleTexelSize ( float size )

Sets the minimum texel size value for the detail, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - Minimum texel size value for the detail to be set.

## float getMinVisibleTexelSize ( )

Returns the minimum texel size value for the detail, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by texel size.
### Return value

Minimum texel size value for the detail.
## void setMaxVisibleTexelSize ( float size )

Sets the maximum texel size value for the detail, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - Maximum texel size value for the detail to be set.

## float getMaxVisibleTexelSize ( )

Returns the maximum texel size value for the detail, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by texel size.
### Return value

Maximum texel size value for the detail.
## void setMinFadeTexelSize ( float size )

Sets the fade in texel size range for the detail. Over this range below the [minimum texel size value](#setMinVisibleTexelSize_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - Fade in texel size range value for the detail to be set, in units.

## float getMinFadeTexelSize ( )

Returns the current fade in texel size range for the detail. Over this range below the [minimum texel size value](#setMinVisibleTexelSize_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by texel size.
### Return value

Fade in texel size range value for the detail, in units.
## void setMaxFadeTexelSize ( float size )

Sets the fade out texel size range for the detail. Over this range below the [maximum texel size value](#setMaxVisibleTexelSize_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - Fade out texel size range value for the detail to be set, in units.

## float getMaxFadeTexelSize ( )

Returns the current fade out texel size range for the detail. Over this range below the [maximum texel size value](#setMaxVisibleTexelSize_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by texel size.
### Return value

Fade out texel size range value for the detail, in units.
## void setMaskThreshold ( float threshold )

Sets a new mask threshold value for the detail. Control blending of the detail according to the mask. The Threshold parameter controls the spread intensity of the layer. Lower values provide bigger spread.
### Arguments

- *float* **threshold** - New mask threshold value to be set in the [0; 1] range.

## float getMaskThreshold ( )

Returns a mask threshold value for the detail. Control blending of the detail according to the mask. The Threshold parameter controls the spread intensity of the layer. Lower values provide bigger spread.
### Return value

Current mask threshold value in the [0; 1] range.
## void setMaskContrast ( float contrast )

Sets a new mask contrast value.
### Arguments

- *float* **contrast** - New mask contrast value to be set in the [0; 1] range.

## float getMaskContrast ( )

Returns a current mask contrast value.
### Return value

Current mask contrast value in the [0; 1] range.
## void setDetailMask ( TerrainDetailMask mask )

Sets the specified detail mask to be used for the detail.
### Arguments

- *[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_usc.md)* **mask** - [Detail mask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_usc.md) to be used for the detail.

## TerrainDetailMask getDetailMask ( )

Returns the detail mask currently used for the detail.
### Return value

[Detail mask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_usc.md) currently used for the detail.
## Material getMaterial ( )

Returns the detail material used for the detail.
### Return value

Material currently used for the detail.
## void setMaterial ( Material material )

Sets a new detail material to be used for the detail.
### Arguments

- *[Material](../../../../api/library/rendering/class.material_usc.md)* **material** - New material to be used for the detail.

## TerrainDetail copy ( TerrainDetail dest_detail )

Copies the detail to the specified destination detail (with all its children).
### Arguments

- *[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_usc.md)* **dest_detail** - Destination detail to which the detail is to be copied.

### Return value

Destination detail.
## TerrainDetail clone ( )

Clones the terrain detail (with all its children).
### Return value

Cloned detail.
## void setMaterialFilePath ( string path )

Sets the detail material by a given path.
### Arguments

- *string* **path** - Material file path.

## string getMaterialFilePath ( )

Returns the path of the assigned detail material.
### Return value

Material file path.
## void setMaterialGUID ( UGUID materialguid )

Sets the material by a [GUID](../../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_usc.md)* **materialguid** - Material [GUID](../../../../api/library/filesystem/class.uguid_usc.md).

## UGUID getMaterialGUID ( )

Returns the [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the assigned detail material.
