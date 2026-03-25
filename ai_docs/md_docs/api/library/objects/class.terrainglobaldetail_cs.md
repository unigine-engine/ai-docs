# Unigine.TerrainGlobalDetail Class (CS)


This class is used to manage details of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalDetail Class

### Properties

## float DisplacementOffset

The displacement offset. this parameter controls the direction of displacement (inward or outward).
## float Displacement

The scale of displacement mapping according to the [height texture](#setHeightTextureName_cstr_void).
## float NormalScale

The intensity scale of the detail normal texture.
## float RoughnessScale

The intensity scale of the detail roughness texture.
## float AlbedoScale

The intensity scale of the detail albedo texture.
## float Roughness

The roughness value multiplier for the detail.
## vec4 AlbedoColor

The current albedo color multiplier for the detail.
## string HeightTextureName

The path to the height texture of the detail.
## string NormalTextureName

The path to the normal texture of the detail.
## string RoughnessTextureName

The path to the roughness texture of the detail.
## string AlbedoTextureName

The path to the albedo texture of the detail.
## float MaskContrast

The contrast of the detail mask.
## float MaskWidth

The width of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide wider areas. Blending is performed according to the detail's mask.
## float MaskThreshold

The threshold that controls smoothness of blending of detail's [height texture](#setHeightTextureName_cstr_void). Higher values provide smoother results. Blending is performed according to the detail's mask.
## float BlendTriplanar

The threshold value that controls smoothness of blending between the different projections of triplanar texture mapping.
> **Notice:** This parameter is used only when triplanar texture mapping is [enabled](#setTriplanar_int_void) for the detail.


## bool Triplanar

The A value indicating if triplanar texture mapping is enabled for the detail.
## bool Detail

The value indicating if the detail uses the mask of the parent detail.
## bool Overlap

The A value indicating if overlap mode is enabled for the detail.
## float MaxFadeDistance

The maximum fade-out distance of the detail. over this distance the detail smoothly becomes invisible due to alpha fading. it is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float).
## float MinFadeDistance

The minimum fade-in distance of the detail. over this distance the detail smoothly becomes visible due to alpha fading. it is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float).
## float MaxVisibleDistance

The maximum visibility distance of the detail. it is the distance, starting from which the detail begins to [fade out](#setMaxFadeHeight_float_void) until it becomes completely invisible.
## float MinVisibleDistance

The minimum visibility distance of the detail. it is the distance, starting from which the detail begins to [fade in](#getMinFadeDistance_float) until it becomes completely visible.
## float MaxFadeHeight

The fade out height range for the detail mask. over this height range above the [maximum height](#setMaxVisibleHeight_float_void) value the detail mask will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height.
## float MinFadeHeight

The fade in height range for the detail mask. over this height range below the [minimum height](#setMinVisibleHeight_float_void) value the detail mask will fade in until it is completely visible. This parameter is used to modulate the detail mask by height.
## float MaxVisibleHeight

The Sets the maximum height value for the detail mask, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
## float MinVisibleHeight

The minimum height value for the detail mask, starting from which the detail begins to [fade in](#setMinFadeHeight_float_void) until it becomes completely visible. This parameter is used to modulate the detail mask by height.
## vec4 Transform

The current transformation parameters of the detail.
## vec4 MaskColor

The color of the detail mask.
## int MaskNumber

The index of the mask used by the detail.
## bool Enabled

The A value indicating if the detail is enabled.
## string Name

The name of the detail.
### Members

---
