# Unigine.TerrainGlobalDetail Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is used to manage details of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalDetail Class

### Members

---

## void setAlbedoColor ( vec4 color )

Sets the albedo color multiplier for the detail.
### Arguments

- *vec4* **color** - Albedo color multiplier.

## vec4 getAlbedoColor ( )

Returns the current albedo color multiplier for the detail.
### Return value

Albedo color multiplier.
## void setAlbedoScale ( float scale )

Sets the intensity scale of the detail albedo texture.
### Arguments

- *float* **scale** - Albedo texture intensity scale value within the [0.0f; 1.0f] range.

## float getAlbedoScale ( )

Returns the intensity scale of the detail albedo texture.
### Return value

Albedo texture intensity scale value within the [0.0f; 1.0f] range.
## void setAlbedoTextureName ( string name )

Sets the path to the albedo texture of the detail.
### Arguments

- *string* **name** - Path to the albedo texture.

## string getAlbedoTextureName ( )

Returns the path to the albedo texture of the detail.
### Return value

Path to the albedo texture.
## void setBlendTriplanar ( float triplanar )

Sets the threshold value that controls smoothness of blending between the different projections of triplanar texture mapping.
> **Notice:** This parameter is used only when triplanar texture mapping is [enabled](#setTriplanar_int_void) for the detail.


### Arguments

- *float* **triplanar** - Triplanar blending value within the [0.0f; 1.0f] range. **Lower** values produce sharper transitions between projections, while **higher** values make it smoother.

## float getBlendTriplanar ( )

Returns the threshold value that controls smoothness of blending between the different projections of triplanar texture mapping.
> **Notice:** This parameter is used only when triplanar texture mapping is [enabled](#setTriplanar_int_void) for the detail.


### Return value

Triplanar blending value within the [0.0f; 1.0f] range.
## void setDetail ( int detail )

Sets the value indicating if the detail uses the mask of the parent detail.
### Arguments

- *int* **detail** - **1** to use the mask of the parent detail or the one generated on its basis; **0** to use own mask.

## int isDetail ( )

Returns the value indicating if the detail uses the mask of the parent detail.
### Return value

**1** if the detail uses the mask of the parent detail or the one generated on its basis; otherwise, **0**.
## void setDisplacement ( float displacement )

Sets the scale of displacement mapping according to the [height texture](#setHeightTextureName_cstr_void).
### Arguments

- *float* **displacement** - Displacement scale value within the [0.0f; 1.0f] range. Higher values produce a greater displacement effect.

## float getDisplacement ( )

Returns the scale of displacement mapping according to the [height texture](#setHeightTextureName_cstr_void).
### Return value

Displacement scale value within the [0.0f; 1.0f] range. Higher values produce a greater displacement effect.
## void setDisplacementOffset ( float offset )

Sets the displacement offset. This parameter controls the direction of displacement (inward or outward).
### Arguments

- *float* **offset** - Displacement offset value within the [-1.0f; 1.0f] range.

  - **positive value** - outward displacement.
  - **0** - points corresponding to [height texture](#setHeightTextureName_cstr_void) values less than 0.5 are displaced inwards, others are displaced outwards.
  - **negative value** - inward displacement.

## float getDisplacementOffset ( )

Returns the displacement offset. This parameter controls the direction of displacement (inward or outward).
### Return value

Displacement offset value within the [-1.0f; 1.0f] range.
- **positive value** - outward displacement.
- **0** - points corresponding to [height texture](#setHeightTextureName_cstr_void) values less than 0.5 are displaced inwards, others ar edisplaced outwards.
- **negative value** - inward displacement.


## void setEnabled ( int enabled )

Enables or disables the detail.
### Arguments

- *int* **enabled** - **1** to enable the detail; **0** to disable it.

## int isEnabled ( )

Returns a value indicating if the detail is enabled.
### Return value

**1** if the detail is enabled; otherwise, **0**.
## void setHeightTextureName ( string name )

Sets the path to the height texture of the detail.
### Arguments

- *string* **name** - Path to the height texture.

## string getHeightTextureName ( )

Returns the path to the height texture of the detail.
### Return value

Path to the height texture.
## void setMaskColor ( vec4 color )

Sets the color of the detail mask.
### Arguments

- *vec4* **color** - Detail mask color.

## vec4 getMaskColor ( )

Returns the color of the detail mask.
### Return value

Detail mask color.
## void setMaskContrast ( float contrast )

Sets the contrast of the detail mask.
### Arguments

- *float* **contrast** - Detail mask contrast value within the [0.0f; 1.0f] range.

## float getMaskContrast ( )

Returns the contrast of the detail mask.
### Return value

Detail mask contrast value within the [0.0f; 1.0f] range.
## void setMaskNumber ( int number )

Sets the index of the mask used by the detail.
### Arguments

- *int* **number** - Mask number.

## int getMaskNumber ( )

Returns the index of the mask used by the detail.
### Return value

Mask number.
## void setMaskThreshold ( float threshold )

Sets the threshold that controls smoothness of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide smoother results. Blending is performed according to the detail's mask.
### Arguments

- *float* **threshold** - Blending threshold value within the [0.0f; 1.0f] range.

## float getMaskThreshold ( )

Returns the threshold that controls smoothness of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide smoother results. Blending is performed according to the detail's mask.
### Return value

Blending threshold value within the [0.0f; 1.0f] range.
## void setMaskWidth ( float width )

Sets the width of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide wider areas. Blending is performed according to the detail's mask.
### Arguments

- *float* **width** - Blending width value within the [0.0f; 1.0f] range.

## float getMaskWidth ( )

Returns the width of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide wider areas. Blending is performed according to the detail's mask.
### Return value

Blending width value within the [0.0f; 1.0f] range.
## void setMaxFadeDistance ( float distance )

Sets the maximum fade-out distance of the detail. Over this distance the detail smoothly becomes invisible due to alpha fading. It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float).
### Arguments

- *float* **distance** - Maximum fade-out distance, in units. If a negative value is provided, 0 will be used instead. The default value is **0**.

## float getMaxFadeDistance ( )

Returns the maximum fade-out distance of the detail. Over this distance the detail smoothly becomes invisible due to alpha fading. It is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float).
### Return value

Maximum fade-out distance, in units.
## void setMaxFadeHeight ( float height )

Sets the fade out height range for the detail mask. Over this height range above the [maximum height](#setMaxVisibleHeight_float_void) value the detail mask will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Fade out height range value for the mask, in units. The default value is 0. Higher values provide smoother fade out.

## float getMaxFadeHeight ( )

Returns the fade out height range for the detail mask. Over this height range above the [maximum height](#setMaxVisibleHeight_float_void) value the detail mask will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
### Return value

Fade out height range value for the mask, in units.
## void setMaxVisibleDistance ( float distance )

Sets the maximum visibility distance of the detail. It is the distance, starting from which the detail begins to [fade out](#setMaxFadeHeight_float_void) until it becomes completely invisible.
> **Notice:** This parameter can be used to improve performance and reduce the tiling effect when looking at the terrain from a large distance.


### Arguments

- *float* **distance** - Maximum visibility distance, in units. If a negative value is provided, 0 will be used instead. The default value is **inf**.

## float getMaxVisibleDistance ( )

Returns the maximum visibility distance of the detail. It is the distance, starting from which the detail begins to [fade out](#setMaxFadeHeight_float_void) until it becomes completely invisible.
### Return value

Maximum visibility distance, in units.
## void setMaxVisibleHeight ( float height )

Sets the maximum height value for the detail mask, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Maximum height value for the mask, in units. The default value is inf.

## float getMaxVisibleHeight ( )

Sets the maximum height value for the detail mask, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
### Return value

Maximum height value for the mask, in units.
## void setMinFadeDistance ( float distance )

Sets the minimum fade-in distance of the detail. Over this distance the detail smoothly becomes visible due to alpha fading. It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float).
### Arguments

- *float* **distance** - Minimum fade-in distance, in units. If a negative value is provided, 0 will be used instead. The default value is 0.

## float getMinFadeDistance ( )

Returns the minimum fade-in distance of the detail. Over this distance the detail smoothly becomes visible due to alpha fading. It is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float).
### Return value

Minimum fade-in distance, in units.
## void setMinFadeHeight ( float height )

Sets the fade in height range for the detail mask. Over this height range below the [minimum height](#setMinVisibleHeight_float_void) value the detail mask will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Fade in height range value for the mask, in units. The default value is 0. Higher values provide smoother fade in.

## float getMinFadeHeight ( )

Returns the fade in height range for the detail mask. Over this height range below the [minimum height](#setMinVisibleHeight_float_void) value the detail mask will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
### Return value

Fade in height range value for the mask, in units.
## void setMinVisibleDistance ( float distance )

Sets the minimum visibility distance of the detail. It is the distance, starting from which the detail begins to [fade in](#getMinFadeDistance_float) until it becomes completely visible.
> **Notice:** This parameter can be used to improve performance and reduce the tiling effect when looking at the terrain from a large distance.


### Arguments

- *float* **distance** - Minimum visibility distance, in units. If a negative value is provided, 0 will be used instead. The default value is **-inf**.

## float getMinVisibleDistance ( )

Returns the minimum visibility distance of the detail. It is the distance, starting from which the detail begins to [fade in](#getMinFadeDistance_float) until it becomes completely visible.
### Return value

Minimum visibility distance, in units.
## void setMinVisibleHeight ( float height )

Sets the minimum height value for the detail mask, starting from which the detail begins to [fade in](#setMinFadeHeight_float_void) until it becomes completely visible. This parameter is used to modulate the detail mask by height.
### Arguments

- *float* **height** - Minimum height value for the mask, in units. The default value is -inf.

## float getMinVisibleHeight ( )

Returns the minimum height value for the detail mask, starting from which the detail begins to [fade in](#setMinFadeHeight_float_void) until it becomes completely visible. This parameter is used to modulate the detail mask by height.
### Return value

Minimum height value for the mask, in units.
## void setName ( string name )

Sets the name of the detail.
### Arguments

- *string* **name** - Detail name.

## string getName ( )

Returns the name of the detail.
### Return value

Detail name.
## void setNormalScale ( float scale )

Sets the intensity scale of the detail normal texture.
### Arguments

- *float* **scale** - Normal texture intensity scale value within the [0.0f; 1.0f] range.

## float getNormalScale ( )

Returns the intensity scale of the detail normal texture.
### Return value

Normal texture intensity scale value within the [0.0f; 1.0f] range.
## void setNormalTextureName ( string name )

Sets the path to the normal texture of the detail.
### Arguments

- *string* **name** - Path to the normal texture.

## string getNormalTextureName ( )

Returns the path to the normal texture of the detail.
### Return value

Path to the normal texture.
## void setOverlap ( int overlap )

Enables or disables overlap mode for the detail.
### Arguments

- *int* **overlap** - **1** to enable overlap mode for the detail; **0** to use overlay mode instead.

## int isOverlap ( )

Returns a value indicating if overlap mode is enabled for the detail.
### Return value

**1** if overlap mode is enabled for the detail; otherwise, **0** (overlay mode is used).
## void setRoughness ( float roughness )

Sets the roughness value multiplier for the detail.
### Arguments

- *float* **roughness** - Roughness value multiplier within the [0.0f; 1.0f] range.

## float getRoughness ( )

Returns the roughness value multiplier for the detail.
### Return value

Roughness value multiplier within the [0.0f; 1.0f] range.
## void setRoughnessScale ( float scale )

Sets the intensity scale of the detail roughness texture.
### Arguments

- *float* **scale** - Roughness texture intensity scale value within the [0.0f; 1.0f] range.

## float getRoughnessScale ( )

Returns the intensity scale of the detail roughness texture.
### Return value

Roughness texture intensity scale value within the [0.0f; 1.0f] range.
## void setRoughnessTextureName ( string name )

Sets the path to the roughness texture of the detail.
### Arguments

- *string* **name** - Path to the roughness texture.

## string getRoughnessTextureName ( )

Returns the path to the roughness texture of the detail.
### Return value

Path to the roughness texture.
## void setTransform ( vec4 transform )

Sets the transformation parameters of the detail.
### Arguments

- *vec4* **transform** - [Vec4](../../../api/library/math/class.vec4_usc.md) transformation vector with the following components:

  - X - **Tile size X** - texture tile size along the X axis, in units.
  - Y - **Tile size Y** - texture tile size along the Y axis, in units.
  - Z - **Offset X** - texture offset along the X axis.
  - W - **Offset Y** - texture offset along the Y axis.

## vec4 getTransform ( )

Returns the current transformation parameters of the detail.
### Return value

[Vec4](../../../api/library/math/class.vec4_usc.md) transformation vector with the following components:
- X - **Tile size X** - texture tile size along the X axis, in units.
- Y - **Tile size Y** - texture tile size along the Y axis, in units.
- Z - **Offset X** - texture offset along the X axis.
- W - **Offset Y** - texture offset along the Y axis.


## void setTriplanar ( int triplanar )

Enables or disables triplanar texture mapping for the detail.
### Arguments

- *int* **triplanar** - **1** to enable triplanar texture mapping for the detail; **0** to use planar UV mapping instead.

## int isTriplanar ( )

Returns a value indicating if triplanar texture mapping is enabled for the detail.
### Return value

**1** if triplanar texture mapping is enabled for the detail; otherwise, **0** (planar UV mapping is used).
