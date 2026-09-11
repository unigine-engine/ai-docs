# Unigine.TerrainGlobalDetail Class (CS)


This class is used to manage details of the [global terrain](../../../objects/objects/terrain/terrain_global/index.md) object.


## TerrainGlobalDetail Class

### Properties

## float DisplacementOffset

The displacement offset within the [-1.0f; 1.0f] range. this parameter controls the direction of displacement (inward or outward):
- **positive value** - outward displacement.
- **0** - points corresponding to [height texture](#setHeightTextureName_cstr_void) values less than 0.5 are displaced inwards, others are displaced outwards.
- **negative value** - inward displacement.


## float Displacement

The scale of displacement mapping according to the [height texture](#setHeightTextureName_cstr_void). Higher values produce a greater displacement effect.
## float NormalScale

The intensity scale of the detail normal texture.
## float RoughnessScale

The intensity scale of the detail roughness texture.
## float AlbedoScale

The intensity scale of the detail albedo texture, within the [0.0f; 1.0f] range.
## float Roughness

The roughness value multiplier for the detail.
## vec4 AlbedoColor

The albedo color multiplier for the detail.
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

The threshold value that controls smoothness of blending between the different projections of triplanar texture mapping, within the [0.0f; 1.0f] range. **Lower** values produce sharper transitions between projections, while **higher** values make it smoother.
> **Notice:** This parameter is used only when triplanar texture mapping is [enabled](#setTriplanar_int_void) for the detail.

## bool Triplanar

The value indicating if triplanar texture mapping is enabled for the detail.
## bool Detail

The value indicating if the detail uses the mask of the parent detail.
## bool Overlap

The value indicating if overlap mode is enabled for the detail.
## float MaxFadeDistance

The maximum fade-out distance of the detail. over this distance the detail smoothly becomes invisible due to alpha fading. it is counted starting from the [maximum visibility distance](#getMaxVisibleDistance_float). If a negative value is provided, 0 will be used instead.
## float MinFadeDistance

The minimum fade-in distance of the detail. over this distance the detail smoothly becomes visible due to alpha fading. it is counted starting from the [minimum visibility distance](#getMinVisibleDistance_float). If a negative value is provided, 0 will be used instead.
## float MaxVisibleDistance

The maximum visibility distance of the detail. it is the distance, starting from which the detail begins to [fade out](#setMaxFadeHeight_float_void) until it becomes completely invisible. If a negative value is provided, 0 will be used instead. The default value is **inf**.
> **Notice:** This parameter can be used to improve performance and reduce the tiling effect when looking at the terrain from a large distance.

## float MinVisibleDistance

The minimum visibility distance of the detail. it is the distance, starting from which the detail begins to [fade in](#getMinFadeDistance_float) until it becomes completely visible. If a negative value is provided, 0 will be used instead. The default value is **-inf**.
> **Notice:** This parameter can be used to improve performance and reduce the tiling effect when looking at the terrain from a large distance.

## float MaxFadeHeight

The fade out height range for the detail mask. over this height range above the [maximum height](#setMaxVisibleHeight_float_void) value the detail mask will fade out until it is completely invisible. This parameter is used to modulate the detail mask by height. Higher values provide smoother fade out.
## float MinFadeHeight

The fade in height range for the detail mask. over this height range below the [minimum height](#setMinVisibleHeight_float_void) value the detail mask will fade in until it is completely visible. This parameter is used to modulate the detail mask by height. Higher values provide smoother fade in.
## float MaxVisibleHeight

The maximum height value for the detail mask, starting from which the detail begins to fade out until it becomes completely invisible. This parameter is used to modulate the detail mask by height.
## float MinVisibleHeight

The minimum height value for the detail mask, starting from which the detail begins to [fade in](#setMinFadeHeight_float_void) until it becomes completely visible. This parameter is used to modulate the detail mask by height. The default value is -inf.
## vec4 Transform

The transformation parameters of the detail (a [Vec4](../../../api/library/math/class.vec4_cs.md) value with the following components):
- X - **Tile size X** - texture tile size along the X axis, in units.
- Y - **Tile size Y** - texture tile size along the Y axis, in units.
- Z - **Offset X** - texture offset along the X axis.
- W - **Offset Y** - texture offset along the Y axis.


## vec4 MaskColor

The color of the detail mask.
## int MaskNumber

The index of the mask used by the detail.
## bool Enabled

The value indicating if the detail is enabled.
## string Name

The name of the detail.
