# Unigine.TerrainDetail Class (CPP)

**Header:** #include <UnigineObjects.h>


This class is used to manage details of the [Landscape Terrain Object](../../../../objects/objects/terrain/landscape_terrain/index.md). Details, define terrain's appearance, each of them can have an unlimited number of children. Details are attached to [detail masks](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md) and are rendered in accordance with their rendering order (the one with the highest order shall be rendered above all others).


## TerrainDetail Class

### Members

---

## void setName ( const char * name )

Sets a new name for the detail.
### Arguments

- *const char ** **name** - New terrain detail name to be set.

## const char * getName ( ) const

Returns the name of the detail.
### Return value

Current name of the detail.
## void setEnabled ( bool enabled )

Sets a value indicating if the terrain detail is enabled.
### Arguments

- *bool* **enabled** - true to enable the terrain detail, false - to disable it.

## bool isEnabled ( ) const

Returns a value indicating if the terrain detail is enabled.
### Return value

true if the terrain detail is enabled; otherwise, false.
## bool isActive ( ) const

Returns a value indicating if the terrain detail is active.
### Return value

true if the terrain detail is active; otherwise, false.
## void setMaskByAlbedo ( const Math::vec4& albedo )

Sets a new color to be used as a mask for the detail. In this case, all areas on the terrain having selected color will be covered by the detail.
### Arguments

- *const  Math::vec4&* **albedo** - Four-component vector (R, G, B, A) representing a new color to be used as a mask for the detail.

## Math:: vec4 getMaskByAlbedo ( ) const

Returns the color currently used as a mask for the detail. In this case, all areas on the terrain having selected color will be covered by the detail.
### Return value

Four-component vector (R, G, B, A) representing a color currently used as a mask for the detail.
## void setMinVisibleHeight ( float height )

Sets the minimum height value for the detail, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Minimum height value for the detail, in units. The default value is -inf.

## float getMinVisibleHeight ( ) const

Returns the minimum height value for the detail, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by height.
### Return value

Minimum height value for the detail, in units.
## void setMaxVisibleHeight ( float height )

Sets the maximum height value for the detail, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Maximum height value for the detail, in units. The default value is inf.

## float getMaxVisibleHeight ( ) const

Returns the maximum height value for the detail, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
### Return value

Maximum height value for the detail, in units.
## void setMinFadeHeight ( float height )

Sets the fade in height range for the detail. Over this height range below the [minimum height value](#setMinVisibleHeight_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Fade in height range value for the detail, in units.

## float getMinFadeHeight ( ) const

Returns the current fade in height range for the detail. Over this height range below the [minimum height value](#setMinVisibleHeight_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
### Return value

Fade in height range value for the detail, in units.
## void setMaxFadeHeight ( float height )

Sets the fade out height range for the detail. Over this height range below the [maximum height value](#setMaxVisibleHeight_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Fade out height range value for the detail, in units.

## float getMaxFadeHeight ( ) const

Returns the current fade out height range for the detail. Over this height range below the [maximum height value](#setMaxVisibleHeight_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
### Return value

Fade out height range value for the detail, in units.
## void setMinVisibleTexelSize ( float size )

Sets the minimum texel size value for the detail, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - Minimum texel size value for the detail to be set.

## float getMinVisibleTexelSize ( ) const

Returns the minimum texel size value for the detail, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by texel size.
### Return value

Minimum texel size value for the detail.
## void setMaxVisibleTexelSize ( float size )

Sets the maximum texel size value for the detail, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - Maximum texel size value for the detail to be set.

## float getMaxVisibleTexelSize ( ) const

Returns the maximum texel size value for the detail, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by texel size.
### Return value

Maximum texel size value for the detail.
## void setMinFadeTexelSize ( float size )

Sets the fade in texel size range for the detail. Over this range below the [minimum texel size value](#setMinVisibleTexelSize_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - Fade in texel size range value for the detail to be set, in units.

## float getMinFadeTexelSize ( ) const

Returns the current fade in texel size range for the detail. Over this range below the [minimum texel size value](#setMinVisibleTexelSize_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by texel size.
### Return value

Fade in texel size range value for the detail, in units.
## void setMaxFadeTexelSize ( float size )

Sets the fade out texel size range for the detail. Over this range below the [maximum texel size value](#setMaxVisibleTexelSize_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - Fade out texel size range value for the detail to be set, in units.

## float getMaxFadeTexelSize ( ) const

Returns the current fade out texel size range for the detail. Over this range below the [maximum texel size value](#setMaxVisibleTexelSize_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by texel size.
### Return value

Fade out texel size range value for the detail, in units.
## void setMaskThreshold ( float threshold )

Sets a new mask threshold value for the detail. Control blending of the detail according to the mask. The Threshold parameter controls the spread intensity of the layer. Lower values provide bigger spread.
### Arguments

- *float* **threshold** - New mask threshold value to be set in the [0; 1] range.

## float getMaskThreshold ( ) const

Returns a mask threshold value for the detail. Control blending of the detail according to the mask. The Threshold parameter controls the spread intensity of the layer. Lower values provide bigger spread.
### Return value

Current mask threshold value in the [0; 1] range.
## void setMaskContrast ( float contrast )

Sets a new mask contrast value.
### Arguments

- *float* **contrast** - New mask contrast value to be set in the [0; 1] range.

## float getMaskContrast ( ) const

Returns a current mask contrast value.
### Return value

Current mask contrast value in the [0; 1] range.
## void setDetailMask ( const Ptr < TerrainDetailMask > & mask )

Sets the specified detail mask to be used for the detail.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md)> &* **mask** - [Detail mask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md) to be used for the detail.

## Ptr < TerrainDetailMask > getDetailMask ( ) const

Returns the detail mask currently used for the detail.
### Return value

[Detail mask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md) currently used for the detail.
## Ptr < Material > getMaterial ( ) const

Returns the detail material used for the detail.
### Return value

Material currently used for the detail.
## void setMaterial ( const Ptr < Material > & material )

Sets a new detail material to be used for the detail.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Material](../../../../api/library/rendering/class.material_cpp.md)> &* **material** - New material to be used for the detail.

## Ptr < TerrainDetail > copy ( const Ptr < TerrainDetail > & dest_detail ) const

Copies the detail to the specified destination detail (with all its children).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[TerrainDetail](../../../../api/library/objects/landscape_terrain/class.terraindetail_cpp.md)> &* **dest_detail** - Destination detail to which the detail is to be copied.

### Return value

Destination detail.
## Ptr < TerrainDetail > clone ( ) const

Clones the terrain detail (with all its children).
### Return value

Cloned detail.
## void setMaterialFilePath ( const char * path )

Sets the detail material by a given path.
### Arguments

- *const char ** **path** - Material file path.

## const char * getMaterialFilePath ( ) const

Returns the path of the assigned detail material.
### Return value

Material file path.
## void setMaterialGUID ( const UGUID& materialguid )

Sets the material by a [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const UGUID&* **materialguid** - Material [GUID](../../../../api/library/filesystem/class.uguid_cpp.md).

## UGUID getMaterialGUID ( ) const

Returns the [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the assigned detail material.
