# Unigine.TerrainDetail Class (CPP)

**Header:** #include <UnigineObjects.h>


This class is used to manage details of the [Landscape Terrain Object](../../../../objects/objects/terrain/landscape_terrain/index.md). Details, define terrain's appearance, each of them can have an unlimited number of children. Details are attached to [detail masks](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md) and are rendered in accordance with their rendering order (the one with the highest order shall be rendered above all others).


## TerrainDetail Class

### Members

## void setName ( const char * name )

Sets a new name of the detail.
### Arguments

- *const char ** **name** - The name of the detail

## const char * getName () const

Returns the current name of the detail.
### Return value

Current name of the detail
## void setEnabled ( bool enabled )

Sets a new value indicating if the terrain detail is enabled.
### Arguments

- *bool* **enabled** - value indicating if the terrain detail is enabled

## bool isEnabled () const

Returns the current value indicating if the terrain detail is enabled.
### Return value

value indicating if the terrain detail is enabled
## bool isActive () const

Returns the current value indicating if the terrain detail is active.
### Return value

**true** if the terrain detail is active; otherwise **false**.
## void setMinVisibleHeight ( float height )

Sets a new minimum height value for the detail, in units, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by height. The default value is -inf.
### Arguments

- *float* **height** - The minimum height value for the detail, in units

## float getMinVisibleHeight () const

Returns the current minimum height value for the detail, in units, starting from which the detail begins to fade in until it becomes completely visible. This parameter is used to modulate the detail mask by height. The default value is -inf.
### Return value

Current minimum height value for the detail, in units
## void setMaxVisibleHeight ( float height )

Sets a new maximum height value for the detail, in units.
### Arguments

- *float* **height** - The maximum height value for the detail, in units

## float getMaxVisibleHeight () const

Returns the current maximum height value for the detail, in units.
### Return value

Current maximum height value for the detail, in units
## void setMinFadeHeight ( float height )

Sets a new fade in height range value for the detail, in units. Over this height range below the [minimum height value](#setMinVisibleHeight_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - The fade in height range value for the detail, in units

## float getMinFadeHeight () const

Returns the current fade in height range value for the detail, in units. Over this height range below the [minimum height value](#setMinVisibleHeight_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
### Return value

Current fade in height range value for the detail, in units
## void setMaxFadeHeight ( float height )

Sets a new fade out height range value for the detail, in units. Over this height range below the [maximum height value](#setMaxVisibleHeight_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - The fade out height range value for the detail, in units

## float getMaxFadeHeight () const

Returns the current fade out height range value for the detail, in units. Over this height range below the [maximum height value](#setMaxVisibleHeight_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
### Return value

Current fade out height range value for the detail, in units
## void setMaskByAlbedo ( const Math:: vec4 & albedo )

Sets a new four-component vector (R, G, B, A) representing a color used as a mask for the detail. In this case, all areas on the terrain having selected color will be covered by the detail.
### Arguments

- *const  Math::[vec4](../../../../api/library/math/class.vec4_cpp.md)&* **albedo** - The color used as a mask for the detail, as a four-component vector (R, G, B, A)

## Math:: vec4 getMaskByAlbedo () const

Returns the current four-component vector (R, G, B, A) representing a color used as a mask for the detail. In this case, all areas on the terrain having selected color will be covered by the detail.
### Return value

Current color used as a mask for the detail, as a four-component vector (R, G, B, A)
## void setMaskThreshold ( float threshold )

Sets a new mask threshold value in the [0; 1] range. Control blending of the detail according to the mask. The Threshold parameter controls the spread intensity of the layer. Lower values provide bigger spread.
### Arguments

- *float* **threshold** - The mask threshold value in the [0; 1] range

## float getMaskThreshold () const

Returns the current mask threshold value in the [0; 1] range. Control blending of the detail according to the mask. The Threshold parameter controls the spread intensity of the layer. Lower values provide bigger spread.
### Return value

Current mask threshold value in the [0; 1] range
## void setMaskContrast ( float contrast )

Sets a new mask contrast value in the [0; 1] range.
### Arguments

- *float* **contrast** - The mask contrast value in the [0; 1] range

## float getMaskContrast () const

Returns the current mask contrast value in the [0; 1] range.
### Return value

Current mask contrast value in the [0; 1] range
## void setDetailMask ( const Ptr < TerrainDetailMask >& mask )

Sets a new [detail mask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md) used for the detail.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md)>&* **mask** - The detail mask used for the detail

## Ptr < TerrainDetailMask > getDetailMask () const

Returns the current [detail mask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md) used for the detail.
### Return value

Current detail mask used for the detail
## void setMaxFadeTexelSize ( float size )

Sets a new fade out texel size range value for the detail, in units. Over this range below the [maximum texel size value](#setMaxVisibleTexelSize_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - The fade out texel size range value for the detail, in units

## float getMaxFadeTexelSize () const

Returns the current fade out texel size range value for the detail, in units. Over this range below the [maximum texel size value](#setMaxVisibleTexelSize_float_void) the detail will fade out until it is completely invisible. This parameter is used to modulate the detail mask by texel size.
### Return value

Current fade out texel size range value for the detail, in units
## void setMinFadeTexelSize ( float size )

Sets a new fade in texel size range value for the detail, in units. Over this range below the [minimum texel size value](#setMinVisibleTexelSize_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by texel size.
### Arguments

- *float* **size** - The fade in texel size range value for the detail, in units

## float getMinFadeTexelSize () const

Returns the current fade in texel size range value for the detail, in units. Over this range below the [minimum texel size value](#setMinVisibleTexelSize_float_void) the detail will fade in until it is completely visible. This parameter is used to modulate the detail mask by texel size.
### Return value

Current fade in texel size range value for the detail, in units
## void setMaxVisibleTexelSize ( float size )

Sets a new maximum texel size value for the detail.
### Arguments

- *float* **size** - The maximum texel size value for the detail

## float getMaxVisibleTexelSize () const

Returns the current maximum texel size value for the detail.
### Return value

Current maximum texel size value for the detail
## void setMinVisibleTexelSize ( float size )

Sets a new minimum texel size value for the detail.
### Arguments

- *float* **size** - The minimum texel size value for the detail

## float getMinVisibleTexelSize () const

Returns the current minimum texel size value for the detail.
### Return value

Current minimum texel size value for the detail
## void setMaterial ( const Ptr < Material >& material )

Sets a new detail material used for the detail.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Material](../../../../api/library/rendering/class.material_cpp.md)>&* **material** - The detail material used for the detail

## Ptr < Material > getMaterial () const

Returns the current detail material used for the detail.
### Return value

Current detail material used for the detail
## void setMaterialGUID ( UGUID guid )

Sets a new [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the material currently used for the detail.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cpp.md)* **guid** - The [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the material currently used for the detail

## UGUID getMaterialGUID () const

Returns the current [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the material currently used for the detail.
### Return value

Current [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the material currently used for the detail
## void setMaterialFilePath ( String path )

Sets a new path of the material file currently used for the detail.
### Arguments

- *[String](../../../../api/library/common/class.string_cpp.md)* **path** - The path of the material file currently used for the detail

## const char * getMaterialFilePath () const

Returns the current path of the material file currently used for the detail.
### Return value

Current path of the material file currently used for the detail
---

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
