# Unigine.TerrainGlobalDetail Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage details of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalDetail Class

### Members

## void setDisplacementOffset ( float offset )

Sets a new displacement offset within the [-1.0f; 1.0f] range. this parameter controls the direction of displacement (inward or outward):
- **positive value** - outward displacement.
- **0** - points corresponding to [height texture](#setHeightTextureName_cstr_void) values less than 0.5 are displaced inwards, others are displaced outwards.
- **negative value** - inward displacement.


### Arguments

- *float* **offset** - The displacement offset

## float getDisplacementOffset () const

Returns the current displacement offset within the [-1.0f; 1.0f] range. this parameter controls the direction of displacement (inward or outward):
- **positive value** - outward displacement.
- **0** - points corresponding to [height texture](#setHeightTextureName_cstr_void) values less than 0.5 are displaced inwards, others are displaced outwards.
- **negative value** - inward displacement.


### Return value

Current displacement offset
## void setDisplacement ( float displacement )

Sets a new scale of displacement mapping according to the [height texture](#setHeightTextureName_cstr_void). Higher values produce a greater displacement effect.
### Arguments

- *float* **displacement** - The scale of displacement mapping according to the height texture

## float getDisplacement () const

Returns the current scale of displacement mapping according to the [height texture](#setHeightTextureName_cstr_void). Higher values produce a greater displacement effect.
### Return value

Current scale of displacement mapping according to the height texture
## void setNormalScale ( float scale )

Sets a new intensity scale of the detail normal texture.
### Arguments

- *float* **scale** - The intensity scale of the detail normal texture

## float getNormalScale () const

Returns the current intensity scale of the detail normal texture.
### Return value

Current intensity scale of the detail normal texture
## void setRoughnessScale ( float scale )

Sets a new intensity scale of the detail roughness texture.
### Arguments

- *float* **scale** - The intensity scale of the detail roughness texture

## float getRoughnessScale () const

Returns the current intensity scale of the detail roughness texture.
### Return value

Current intensity scale of the detail roughness texture
## void setAlbedoScale ( float scale )

Sets a new intensity scale of the detail albedo texture, within the [0.0f; 1.0f] range.
### Arguments

- *float* **scale** - The intensity scale of the detail albedo texture

## float getAlbedoScale () const

Returns the current intensity scale of the detail albedo texture, within the [0.0f; 1.0f] range.
### Return value

Current intensity scale of the detail albedo texture
## void setRoughness ( float roughness )

Sets a new roughness value multiplier for the detail.
### Arguments

- *float* **roughness** - The roughness value multiplier for the detail

## float getRoughness () const

Returns the current roughness value multiplier for the detail.
### Return value

Current roughness value multiplier for the detail
## void setAlbedoColor ( vec4 color )

Sets a new albedo color multiplier for the detail.
### Arguments

- *vec4* **color** - The albedo color multiplier for the detail

## vec4 getAlbedoColor () const

Returns the current albedo color multiplier for the detail.
### Return value

Current albedo color multiplier for the detail
## void setHeightTextureName ( string name )

Sets a new path to the height texture of the detail.
### Arguments

- *string* **name** - The path to the height texture of the detail

## const char * getHeightTextureName () const

Returns the current path to the height texture of the detail.
### Return value

Current path to the height texture of the detail
## void setNormalTextureName ( string name )

Sets a new path to the normal texture of the detail.
### Arguments

- *string* **name** - The path to the normal texture of the detail

## const char * getNormalTextureName () const

Returns the current path to the normal texture of the detail.
### Return value

Current path to the normal texture of the detail
## void setRoughnessTextureName ( string name )

Sets a new path to the roughness texture of the detail.
### Arguments

- *string* **name** - The path to the roughness texture of the detail

## const char * getRoughnessTextureName () const

Returns the current path to the roughness texture of the detail.
### Return value

Current path to the roughness texture of the detail
## void setAlbedoTextureName ( string name )

Sets a new path to the albedo texture of the detail.
### Arguments

- *string* **name** - The path to the albedo texture of the detail

## const char * getAlbedoTextureName () const

Returns the current path to the albedo texture of the detail.
### Return value

Current path to the albedo texture of the detail
## void setMaskContrast ( float contrast )

Sets a new contrast of the detail mask.
### Arguments

- *float* **contrast** - The contrast of the detail mask

## float getMaskContrast () const

Returns the current contrast of the detail mask.
### Return value

Current contrast of the detail mask
## void setMaskWidth ( float width )

Sets a new width of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide wider areas. Blending is performed according to the detail's mask.
### Arguments

- *float* **width** - The width of blending of detail's

## float getMaskWidth () const

Returns the current width of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide wider areas. Blending is performed according to the detail's mask.
### Return value

Current width of blending of detail's
## void setMaskThreshold ( float threshold )

Sets a new threshold that controls smoothness of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide smoother results. Blending is performed according to the detail's mask.
### Arguments

- *float* **threshold** - The threshold that controls smoothness of blending of detail's

## float getMaskThreshold () const

Returns the current threshold that controls smoothness of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide smoother results. Blending is performed according to the detail's mask.
### Return value

Current threshold that controls smoothness of blending of detail's
## void setBlendTriplanar ( float triplanar )

Sets a new threshold value that controls smoothness of blending between the different projections of triplanar texture mapping, within the [0.0f; 1.0f] range. **Lower** values produce sharper transitions between projections, while **higher** values make it smoother.
> **Notice:** This parameter is used only when triplanar texture mapping is [enabled](#setTriplanar_int_void) for the detail.

### Arguments

- *float* **triplanar** - The threshold value that controls smoothness of blending between the different projections of triplanar texture mapping

## float getBlendTriplanar () const

Returns the current threshold value that controls smoothness of blending between the different projections of triplanar texture mapping, within the [0.0f; 1.0f] range. **Lower** values produce sharper transitions between projections, while **higher** values make it smoother.
> **Notice:** This parameter is used only when triplanar texture mapping is [enabled](#setTriplanar_int_void) for the detail.

### Return value

Current threshold value that controls smoothness of blending between the different projections of triplanar texture mapping
## void setTriplanar ( int triplanar )

Sets a new value indicating if triplanar texture mapping is enabled for the detail.
### Arguments

- *int* **triplanar** - The value indicating if triplanar texture mapping is enabled for the detail

## int isTriplanar () const

Returns the current value indicating if triplanar texture mapping is enabled for the detail.
### Return value

Current value indicating if triplanar texture mapping is enabled for the detail
## void setDetail ( int detail )

Sets a new value indicating if the detail uses the mask of the parent detail.
### Arguments

- *int* **detail** - The value indicating if the detail uses the mask of the parent detail

## int isDetail () const

Returns the current value indicating if the detail uses the mask of the parent detail.
### Return value

Current value indicating if the detail uses the mask of the parent detail
## void setOverlap ( int overlap )

Sets a new value indicating if overlap mode is enabled for the detail.
### Arguments

- *int* **overlap** - The value indicating if overlap mode is enabled for the detail

## int isOverlap () const

Returns the current value indicating if overlap mode is enabled for the detail.
### Return value

Current value indicating if overlap mode is enabled for the detail
## void setMaxFadeDistance ( float distance )

Sets a new maximum fade-out distance of the detail. over this distance the detail smoothly becomes invisible due to alpha fading. it is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float). If a negative value is provided, 0 will be used instead.
### Arguments

- *float* **distance** - The maximum fade-out distance of the detail

## float getMaxFadeDistance () const

Returns the current maximum fade-out distance of the detail. over this distance the detail smoothly becomes invisible due to alpha fading. it is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float). If a negative value is provided, 0 will be used instead.
### Return value

Current maximum fade-out distance of the detail
## void setMinFadeDistance ( float distance )

Sets a new minimum fade-in distance of the detail. over this distance the detail smoothly becomes visible due to alpha fading. it is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float). If a negative value is provided, 0 will be used instead.
### Arguments

- *float* **distance** - The minimum fade-in distance of the detail

## float getMinFadeDistance () const

Returns the current minimum fade-in distance of the detail. over this distance the detail smoothly becomes visible due to alpha fading. it is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float). If a negative value is provided, 0 will be used instead.
### Return value

Current minimum fade-in distance of the detail
## void setMaxVisibleDistance ( float distance )

Sets a new maximum visibility distance of the detail. it is the distance, starting from which the detail begins to [fade out](#setMaxFadeHeight_float_void) until it becomes completely invisible. If a negative value is provided, 0 will be used instead. The default value is **inf**.
> **Notice:** This parameter can be used to improve performance and reduce the tiling effect when looking at the terrain from a large distance.

### Arguments

- *float* **distance** - The maximum visibility distance of the detail

## float getMaxVisibleDistance () const

Returns the current maximum visibility distance of the detail. it is the distance, starting from which the detail begins to [fade out](#setMaxFadeHeight_float_void) until it becomes completely invisible. If a negative value is provided, 0 will be used instead. The default value is **inf**.
> **Notice:** This parameter can be used to improve performance and reduce the tiling effect when looking at the terrain from a large distance.

### Return value

Current maximum visibility distance of the detail
## void setMinVisibleDistance ( float distance )

Sets a new minimum visibility distance of the detail. it is the distance, starting from which the detail begins to [fade in](#getMinFadeDistance_float) until it becomes completely visible. If a negative value is provided, 0 will be used instead. The default value is **-inf**.
> **Notice:** This parameter can be used to improve performance and reduce the tiling effect when looking at the terrain from a large distance.

### Arguments

- *float* **distance** - The minimum visibility distance of the detail

## float getMinVisibleDistance () const

Returns the current minimum visibility distance of the detail. it is the distance, starting from which the detail begins to [fade in](#getMinFadeDistance_float) until it becomes completely visible. If a negative value is provided, 0 will be used instead. The default value is **-inf**.
> **Notice:** This parameter can be used to improve performance and reduce the tiling effect when looking at the terrain from a large distance.

### Return value

Current minimum visibility distance of the detail
## void setMaxFadeHeight ( float height )

Sets a new fade out height range for the detail mask. over this height range above the [maximum height](#setMaxVisibleHeight_float_void) value the detail mask will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height. Higher values provide smoother fade out.
### Arguments

- *float* **height** - The fade out height range for the detail mask

## float getMaxFadeHeight () const

Returns the current fade out height range for the detail mask. over this height range above the [maximum height](#setMaxVisibleHeight_float_void) value the detail mask will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height. Higher values provide smoother fade out.
### Return value

Current fade out height range for the detail mask
## void setMinFadeHeight ( float height )

Sets a new fade in height range for the detail mask. over this height range below the [minimum height](#setMinVisibleHeight_float_void) value the detail mask will fade in until it is completely visible. This parameter is used to modulate the detail mask by height. Higher values provide smoother fade in.
### Arguments

- *float* **height** - The fade in height range for the detail mask

## float getMinFadeHeight () const

Returns the current fade in height range for the detail mask. over this height range below the [minimum height](#setMinVisibleHeight_float_void) value the detail mask will fade in until it is completely visible. This parameter is used to modulate the detail mask by height. Higher values provide smoother fade in.
### Return value

Current fade in height range for the detail mask
## void setMaxVisibleHeight ( float height )

Sets a new maximum height value for the detail mask, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - The maximum height value for the detail mask, starting from which the detail begins to fade out until it becomes completely invisible

## float getMaxVisibleHeight () const

Returns the current maximum height value for the detail mask, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
### Return value

Current maximum height value for the detail mask, starting from which the detail begins to fade out until it becomes completely invisible
## void setMinVisibleHeight ( float height )

Sets a new minimum height value for the detail mask, starting from which the detail begins to [fade in](#setMinFadeHeight_float_void) until it becomes completely visible. This parameter is used to modulate the detail mask by height. The default value is -inf.
### Arguments

- *float* **height** - The minimum height value for the detail mask, starting from which the detail begins to fade in until it becomes completely visible

## float getMinVisibleHeight () const

Returns the current minimum height value for the detail mask, starting from which the detail begins to [fade in](#setMinFadeHeight_float_void) until it becomes completely visible. This parameter is used to modulate the detail mask by height. The default value is -inf.
### Return value

Current minimum height value for the detail mask, starting from which the detail begins to fade in until it becomes completely visible
## void setTransform ( vec4 transform )

Sets a new transformation parameters of the detail (a [Vec4](../../../api/library/math/class.vec4_usc.md) value with the following components):
- X - **Tile size X** - texture tile size along the X axis, in units.
- Y - **Tile size Y** - texture tile size along the Y axis, in units.
- Z - **Offset X** - texture offset along the X axis.
- W - **Offset Y** - texture offset along the Y axis.


### Arguments

- *vec4* **transform** - The transformation parameters of the detail

## vec4 getTransform () const

Returns the current transformation parameters of the detail (a [Vec4](../../../api/library/math/class.vec4_usc.md) value with the following components):
- X - **Tile size X** - texture tile size along the X axis, in units.
- Y - **Tile size Y** - texture tile size along the Y axis, in units.
- Z - **Offset X** - texture offset along the X axis.
- W - **Offset Y** - texture offset along the Y axis.


### Return value

Current transformation parameters of the detail
## void setMaskColor ( vec4 color )

Sets a new color of the detail mask.
### Arguments

- *vec4* **color** - The color of the detail mask

## vec4 getMaskColor () const

Returns the current color of the detail mask.
### Return value

Current color of the detail mask
## void setMaskNumber ( int number )

Sets a new index of the mask used by the detail.
### Arguments

- *int* **number** - The index of the mask used by the detail

## int getMaskNumber () const

Returns the current index of the mask used by the detail.
### Return value

Current index of the mask used by the detail
## void setEnabled ( int enabled )

Sets a new value indicating if the detail is enabled.
### Arguments

- *int* **enabled** - The value indicating if the detail is enabled

## int isEnabled () const

Returns the current value indicating if the detail is enabled.
### Return value

Current value indicating if the detail is enabled
## void setName ( string name )

Sets a new name of the detail.
### Arguments

- *string* **name** - The name of the detail

## const char * getName () const

Returns the current name of the detail.
### Return value

Current name of the detail
