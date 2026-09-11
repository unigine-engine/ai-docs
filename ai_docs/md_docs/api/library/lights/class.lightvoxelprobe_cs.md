# Unigine::LightVoxelProbe Class (CS)

**Inherits from:** Light


This class allows creating and managing *[Voxel Probe](../../../objects/lights/voxelprobe/index.md)* sources.


## LightVoxelProbe Class

### Enums

## BAKE_INTERNAL_VOLUME

| Name | Description |
|---|---|
| **HALF** = 0 | Bake internal volume (voxels that don't touch geometry) in half resolution. |
| **FULL** = 1 | Bake internal volume (voxels that don't touch geometry) in full resolution. |

## BAKE_QUALITY

Light baking quality preset of the *Voxel Probe*. Each preset includes recommended common baking quality settings, such as number of light rays simulated and sampling quality, that affect the time consumption of light baking and the final quality.
| Name | Description |
|---|---|
| **DRAFT** = 0 | The lowest sampling quality and number of rays simulated but the highest iterativity. |
| **LOW** = 1 | Low sampling quality and number of light rays simulated. |
| **MEDIUM** = 2 | Stable quality level is good for most cases. |
| **HIGH** = 3 | High sampling quality and number of light rays simulated is quite enough for release production. |
| **ULTRA** = 4 | Ultra baking quality might be useful to get rid of small inconsistencies on the release production. |

## BLEND

| Name | Description |
|---|---|
| **ALPHA_BLEND** = 0 | The alpha blend mode of light blending. |
| **ADDITIVE** = 1 | The additive mode of light blending. This option offers more flexibility in lighting control. you can use it to blend lighting of several *Voxel Probes* together and control them separately (e.g. make a separate *Voxel Probe* for an indoor emissive light source and blend it with another *Voxel Probe* with lighting baked from the sky, having the ability to enable and disable them separately). > **Notice:** Voxel probes with additive blending enabled cannot be used to add lighting details (e.g. creating a small high-detail *Voxel Probe* inside a large low-detail one). Such probes do not replace each other, as they are blended instead. |
| **MULTIPLICATIVE** = 2 | The multiplicative mode of light blending. |

### Properties

## string TextureFilePath

The file path for the lighting texture used for the *Voxel Probe*.
## bool BakeVisibilityVoxelProbe

The value indicating if other *Voxel Probe* light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
## bool BakeVisibilityLightProj

The value indicating if projected light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
## bool BakeVisibilityLightOmni

The value indicating if omni light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
## bool BakeVisibilityLightWorld

The value indicating if world light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
## bool BakeVisibilitySky

The value indicating if lighting from the sky is to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
## bool BakeVisibilityEmission

The value indicating if emission light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
## bool BakeVisibilityLightmap

The value indicating if the lightmapped surfaces are to be baked to the *Voxel Probe*.
## LightVoxelProbe.BAKE_INTERNAL_VOLUME BakeInternalVolume

The internal volume baking mode for the *Voxel Probe* (voxels that don't touch geometry).
> **Notice:** If internal volume baking is disabled, only the voxels covering geometry are baked while empty ones are skipped.


## float BakeZFar

The distance to the far clipping plane used for every voxel during light baking.
## int BakeViewportMask

The mask that specifies materials taking part in baking.
## bool SpecularCubicFiltering

The value indicating if cubic filtering is applied to specular reflections textures.
> **Notice:** If cubic filtering is disabled, **linear** texture filtering is used.

## float SpecularReflectionBias

The specular reflections offset along the reflection vector.
## float SpecularNormalBias

The specular reflections offset along the normal to the surface.
## float SpecularTangentBias

The additional offset for specular reflections along the surface tangents. Adjusting this setting can help reduce reflection leaking in dark areas.
## float SpecularVisibilityRoughnessMax

The higher bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible.
## float SpecularVisibilityRoughnessMin

The lower bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible.
## bool SpecularEnabled

The value indicating if specular reflections are enabled for the *Voxel Probe*.
## bool DiffuseCubicFiltering

The value indicating if cubic filtering is applied to *Voxel Probe* diffuse lighting.
## float DiffuseNormalBias

The bias of ambient lighting implemented as voxel projection offset along the normal to the surface.
## float DiffuseTangentBias

The additional offset for voxel projection along the surface tangents. Adjusting this setting can help reduce light leaking in dark areas.
## float DiffuseTranslucentIndirect

The intensity of the material's original diffuse lighting, as if the *Translucent* parameter were set to 0. Fine-tuning the current parameter can help correct artifacts caused by [*DiffuseTranslucentSoftIndirect*](#DiffuseTranslucentSoftIndirect), such as excessive darkening on materials.
## float DiffuseTranslucentSoftIndirect

The intensity of soft diffuse lighting calculated as the average illumination from all six directions. With such approach to lighting surface normals are not taken into account, thus increasing this value may result in a darker appearance than expected. However, this approach often produces a more realistic look, similar to the appearance of wax figures.
## bool UseSkyColor

The value indicating if sky color modulation for the *Voxel Probe* is enabled.
## float AttenuationPower

The power of light attenuation used to simulate intensity gradual fading. This parameter determines how fast the intensity decreases up to the attenuation distance set for the light source.
## vec3 AttenuationDistance

The distance from the light source shape, at which the light source doesn't illuminate anything.
## float VoxelSize

The size of each voxel in the *Voxel Probe*.
## vec3 BoxSize

The size of the whole box-type *Voxel Probe*.
## LightVoxelProbe.BAKE_QUALITY BakeQuality

The baking quality for the *Voxel Probe*.
## LightVoxelProbe.BLEND BlendMode

The blending mode for the *Voxel Probe*.
### Members

---

## LightVoxelProbe ( )

Constructor. Creates a new *Voxel Probe* with default parameters.
## ivec3 GetResolution ( )

Returns the resolution of the *Voxel Probe* according to the voxel size.
### Return value

Resolution of the *Voxel Probe* along X, Y and Z axis, in voxels.
## static int type ( )

Returns the type of the node.
### Return value

[LightVoxelProbe](../../../api/library/nodes/class.node_cs.md#LIGHT_VOXEL_PROBE) type identifier.
## long GetVideoMemoryUsage ( )

Returns a value defining how much memory the light texture takes according to its size. The memory is calculated in accordance to the following formula: ***Memory** = **SizeX** � **SizeY** � **SizeZ** � **Sides** � **FormatMemory***
- **SizeX, SizeY, SizeZ** - the dimensions of the 3D light texture, in voxels.
- **Sides** - number of sides of each voxel, equal to 6.
- **FormatMemory** - a memory usage amount for the texture in RGBA16 format, equal to 8.


### Return value

A texture memory usage, in bytes.
