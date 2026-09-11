# Unigine::LightVoxelProbe Class (CPP)

**Header:** #include <UnigineLights.h>

**Inherits from:** Light


This class allows creating and managing *[Voxel Probe](../../../objects/lights/voxelprobe/index.md)* sources.


## LightVoxelProbe Class

### Enums

## BAKE_INTERNAL_VOLUME

| Name | Description |
|---|---|
| **BAKE_INTERNAL_VOLUME_HALF** = 0 | Bake internal volume (voxels that don't touch geometry) in half resolution. |
| **BAKE_INTERNAL_VOLUME_FULL** = 1 | Bake internal volume (voxels that don't touch geometry) in full resolution. |

## BAKE_QUALITY

Light baking quality preset of the *Voxel Probe*. Each preset includes recommended common baking quality settings, such as number of light rays simulated and sampling quality, that affect the time consumption of light baking and the final quality.
| Name | Description |
|---|---|
| **BAKE_QUALITY_DRAFT** = 0 | The lowest sampling quality and number of rays simulated but the highest iterativity. |
| **BAKE_QUALITY_LOW** = 1 | Low sampling quality and number of light rays simulated. |
| **BAKE_QUALITY_MEDIUM** = 2 | Stable quality level is good for most cases. |
| **BAKE_QUALITY_HIGH** = 3 | High sampling quality and number of light rays simulated is quite enough for release production. |
| **BAKE_QUALITY_ULTRA** = 4 | Ultra baking quality might be useful to get rid of small inconsistencies on the release production. |

## BLEND

| Name | Description |
|---|---|
| **BLEND_ALPHA_BLEND** = 0 | The alpha blend mode of light blending. |
| **BLEND_ADDITIVE** = 1 | The additive mode of light blending. This option offers more flexibility in lighting control. you can use it to blend lighting of several *Voxel Probes* together and control them separately (e.g. make a separate *Voxel Probe* for an indoor emissive light source and blend it with another *Voxel Probe* with lighting baked from the sky, having the ability to enable and disable them separately). > **Notice:** Voxel probes with additive blending enabled cannot be used to add lighting details (e.g. creating a small high-detail *Voxel Probe* inside a large low-detail one). Such probes do not replace each other, as they are blended instead. |
| **BLEND_MULTIPLICATIVE** = 2 | The multiplicative mode of light blending. |

### Members

## void setTextureFilePath ( const char * path )

Sets a new file path for the lighting texture used for the *Voxel Probe*.
### Arguments

- *const char ** **path** - The path to the texture file.

## String getTextureFilePath () const

Returns the current file path for the lighting texture used for the *Voxel Probe*.
### Return value

Current path to the texture file.
## void setBakeVisibilityVoxelProbe ( bool probe )

Sets a new value indicating if other *Voxel Probe* light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **probe** - Set **true** to enable baking of other *Voxel Probe* light sources to the *Voxel Probe*; **false** - to disable it.

## bool isBakeVisibilityVoxelProbe () const

Returns the current value indicating if other *Voxel Probe* light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of other *Voxel Probe* light sources to the *Voxel Probe* is enabled ; otherwise **false**.
## void setBakeVisibilityLightProj ( bool proj )

Sets a new value indicating if projected light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **proj** - Set **true** to enable baking of projected light sources to the *Voxel Probe*; **false** - to disable it.

## bool isBakeVisibilityLightProj () const

Returns the current value indicating if projected light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of projected light sources to the *Voxel Probe* is enabled ; otherwise **false**.
## void setBakeVisibilityLightOmni ( bool omni )

Sets a new value indicating if omni light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **omni** - Set **true** to enable baking of omni light sources to the *Voxel Probe*; **false** - to disable it.

## bool isBakeVisibilityLightOmni () const

Returns the current value indicating if omni light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of omni light sources to the *Voxel Probe* is enabled ; otherwise **false**.
## void setBakeVisibilityLightWorld ( bool world )

Sets a new value indicating if world light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **world** - Set **true** to enable baking of world light sources to the *Voxel Probe*; **false** - to disable it.

## bool isBakeVisibilityLightWorld () const

Returns the current value indicating if world light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of world light sources to the *Voxel Probe* is enabled ; otherwise **false**.
## void setBakeVisibilitySky ( bool sky )

Sets a new value indicating if lighting from the sky is to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **sky** - Set **true** to enable baking of lighting from the sky to the *Voxel Probe*; **false** - to disable it.

## bool isBakeVisibilitySky () const

Returns the current value indicating if lighting from the sky is to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of lighting from the sky to the *Voxel Probe* is enabled ; otherwise **false**.
## void setBakeVisibilityEmission ( bool emission )

Sets a new value indicating if emission light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *bool* **emission** - Set **true** to enable baking of emission light sources to the *Voxel Probe*; **false** - to disable it.

## bool isBakeVisibilityEmission () const

Returns the current value indicating if emission light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

**true** if baking of emission light sources to the *Voxel Probe* is enabled ; otherwise **false**.
## void setBakeVisibilityLightmap ( bool lightmap )

Sets a new value indicating if the lightmapped surfaces are to be baked to the *Voxel Probe*.
### Arguments

- *bool* **lightmap** - Set **true** to enable baking of lightmapped surfaces to the *Voxel Probe*; **false** - to disable it.

## bool isBakeVisibilityLightmap () const

Returns the current value indicating if the lightmapped surfaces are to be baked to the *Voxel Probe*.
### Return value

**true** if baking of lightmapped surfaces to the *Voxel Probe* is enabled ; otherwise **false**.
## void setBakeInternalVolume ( LightVoxelProbe::BAKE_INTERNAL_VOLUME volume )

Sets a new internal volume baking mode for the *Voxel Probe* (voxels that don't touch geometry).
> **Notice:** If internal volume baking is disabled, only the voxels covering geometry are baked while empty ones are skipped.


### Arguments

- *[LightVoxelProbe::BAKE_INTERNAL_VOLUME](../../../api/library/lights/class.lightvoxelprobe_cpp.md#BAKE_INTERNAL_VOLUME)* **volume** - The Internal volume baking mode to be set. One of the [BAKE_INTERNAL_VOLUME_*](#BAKE_INTERNAL_VOLUME_HALF) values.

## LightVoxelProbe::BAKE_INTERNAL_VOLUME getBakeInternalVolume () const

Returns the current internal volume baking mode for the *Voxel Probe* (voxels that don't touch geometry).
> **Notice:** If internal volume baking is disabled, only the voxels covering geometry are baked while empty ones are skipped.


### Return value

Current Internal volume baking mode to be set. One of the [BAKE_INTERNAL_VOLUME_*](#BAKE_INTERNAL_VOLUME_HALF) values.
## void setBakeZFar ( float zfar )

Sets a new distance to the far clipping plane used for every voxel during light baking.
### Arguments

- *float* **zfar** - The distance to the far clipping plane.

## float getBakeZFar () const

Returns the current distance to the far clipping plane used for every voxel during light baking.
### Return value

Current distance to the far clipping plane.
## void setBakeViewportMask ( int mask )

Sets a new mask that specifies materials taking part in baking.
### Arguments

- *int* **mask** - The bake viewport mask (integer, each bit of which is used to represent a mask).

## int getBakeViewportMask () const

Returns the current mask that specifies materials taking part in baking.
### Return value

Current bake viewport mask (integer, each bit of which is used to represent a mask).
## void setSpecularCubicFiltering ( bool filtering )

Sets a new value indicating if cubic filtering is applied to specular reflections textures.
> **Notice:** If cubic filtering is disabled, **linear** texture filtering is used.

### Arguments

- *bool* **filtering** - Set **true** to enable cubic filtering for specular reflections textures; **false** - to disable it.

## bool isSpecularCubicFiltering () const

Returns the current value indicating if cubic filtering is applied to specular reflections textures.
> **Notice:** If cubic filtering is disabled, **linear** texture filtering is used.

### Return value

**true** if cubic filtering for specular reflections textures is enabled ; otherwise **false**.
## void setSpecularReflectionBias ( float bias )

Sets a new specular reflections offset along the reflection vector.
### Arguments

- *float* **bias** - The specular reflections offset along the reflection vector

## float getSpecularReflectionBias () const

Returns the current specular reflections offset along the reflection vector.
### Return value

Current specular reflections offset along the reflection vector
## void setSpecularNormalBias ( float bias )

Sets a new specular reflections offset along the normal to the surface.
### Arguments

- *float* **bias** - The specular reflections offset along the normal

## float getSpecularNormalBias () const

Returns the current specular reflections offset along the normal to the surface.
### Return value

Current specular reflections offset along the normal
## void setSpecularTangentBias ( float bias )

Sets a new additional offset for specular reflections along the surface tangents. Adjusting this setting can help reduce reflection leaking in dark areas.
### Arguments

- *float* **bias** - The offset for specular reflections along the surface tangents

## float getSpecularTangentBias () const

Returns the current additional offset for specular reflections along the surface tangents. Adjusting this setting can help reduce reflection leaking in dark areas.
### Return value

Current offset for specular reflections along the surface tangents
## void setSpecularVisibilityRoughnessMax ( float max )

Sets a new higher bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible.
### Arguments

- *float* **max** - The higher bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible

## float getSpecularVisibilityRoughnessMax () const

Returns the current higher bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible.
### Return value

Current higher bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible
## void setSpecularVisibilityRoughnessMin ( float min )

Sets a new lower bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible.
### Arguments

- *float* **min** - The lower bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible

## float getSpecularVisibilityRoughnessMin () const

Returns the current lower bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible.
### Return value

Current lower bound of the roughness range within which the specular reflections of the *Voxel Probe* are visible
## void setSpecularEnabled ( bool enabled )

Sets a new value indicating if specular reflections are enabled for the *Voxel Probe*.
### Arguments

- *bool* **enabled** - Set **true** to enable specular reflections for the *Voxel Probe*; **false** - to disable it.

## bool isSpecularEnabled () const

Returns the current value indicating if specular reflections are enabled for the *Voxel Probe*.
### Return value

**true** if specular reflections for the *Voxel Probe* is enabled ; otherwise **false**.
## void setDiffuseCubicFiltering ( bool filtering )

Sets a new value indicating if cubic filtering is applied to *Voxel Probe* diffuse lighting.
### Arguments

- *bool* **filtering** - Set **true** to enable cubic filtering for *Voxel Probe* diffuse lighting; **false** - to disable it.

## bool isDiffuseCubicFiltering () const

Returns the current value indicating if cubic filtering is applied to *Voxel Probe* diffuse lighting.
### Return value

**true** if cubic filtering for *Voxel Probe* diffuse lighting is enabled ; otherwise **false**.
## void setDiffuseNormalBias ( float bias )

Sets a new bias of ambient lighting implemented as voxel projection offset along the normal to the surface.
### Arguments

- *float* **bias** - The voxel projection offset along the normal

## float getDiffuseNormalBias () const

Returns the current bias of ambient lighting implemented as voxel projection offset along the normal to the surface.
### Return value

Current voxel projection offset along the normal
## void setDiffuseTangentBias ( float bias )

Sets a new additional offset for voxel projection along the surface tangents. Adjusting this setting can help reduce light leaking in dark areas.
### Arguments

- *float* **bias** - The offset for voxel projection along the surface tangents

## float getDiffuseTangentBias () const

Returns the current additional offset for voxel projection along the surface tangents. Adjusting this setting can help reduce light leaking in dark areas.
### Return value

Current offset for voxel projection along the surface tangents
## void setDiffuseTranslucentIndirect ( float indirect )

Sets a new intensity of the material's original diffuse lighting, as if the *Translucent* parameter were set to 0. Fine-tuning the current parameter can help correct artifacts caused by [*setDiffuseTranslucentSoftIndirect()*](#DiffuseTranslucentSoftIndirect), such as excessive darkening on materials.
### Arguments

- *float* **indirect** - The intensity of the original diffuse lighting on the material

## float getDiffuseTranslucentIndirect () const

Returns the current intensity of the material's original diffuse lighting, as if the *Translucent* parameter were set to 0. Fine-tuning the current parameter can help correct artifacts caused by [*setDiffuseTranslucentSoftIndirect()*](#DiffuseTranslucentSoftIndirect), such as excessive darkening on materials.
### Return value

Current intensity of the original diffuse lighting on the material
## void setDiffuseTranslucentSoftIndirect ( float indirect )

Sets a new intensity of soft diffuse lighting calculated as the average illumination from all six directions. With such approach to lighting surface normals are not taken into account, thus increasing this value may result in a darker appearance than expected. However, this approach often produces a more realistic look, similar to the appearance of wax figures.
### Arguments

- *float* **indirect** - The intensity of soft diffuse lighting

## float getDiffuseTranslucentSoftIndirect () const

Returns the current intensity of soft diffuse lighting calculated as the average illumination from all six directions. With such approach to lighting surface normals are not taken into account, thus increasing this value may result in a darker appearance than expected. However, this approach often produces a more realistic look, similar to the appearance of wax figures.
### Return value

Current intensity of soft diffuse lighting
## void setUseSkyColor ( bool color )

Sets a new value indicating if sky color modulation for the *Voxel Probe* is enabled.
### Arguments

- *bool* **color** - Set **true** to enable sky color modulation for the *Voxel Probe*; **false** - to disable it.

## bool isUseSkyColor () const

Returns the current value indicating if sky color modulation for the *Voxel Probe* is enabled.
### Return value

**true** if sky color modulation for the *Voxel Probe* is enabled ; otherwise **false**.
## void setAttenuationPower ( float power )

Sets a new power of light attenuation used to simulate intensity gradual fading. This parameter determines how fast the intensity decreases up to the attenuation distance set for the light source.
### Arguments

- *float* **power** - The attenuation power value.

## float getAttenuationPower () const

Returns the current power of light attenuation used to simulate intensity gradual fading. This parameter determines how fast the intensity decreases up to the attenuation distance set for the light source.
### Return value

Current attenuation power value.
## void setAttenuationDistance ( const Math:: vec3 & distance )

Sets a new distance from the light source shape, at which the light source doesn't illuminate anything.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **distance** - The distance from the light source shape, in units, at which the light source doesn't illuminate anything.

## Math:: vec3 getAttenuationDistance () const

Returns the current distance from the light source shape, at which the light source doesn't illuminate anything.
### Return value

Current distance from the light source shape, in units, at which the light source doesn't illuminate anything.
## void setVoxelSize ( float size )

Sets a new size of each voxel in the *Voxel Probe*.
### Arguments

- *float* **size** - The voxel size value, in units.

## float getVoxelSize () const

Returns the current size of each voxel in the *Voxel Probe*.
### Return value

Current voxel size value, in units.
## void setBoxSize ( const Math:: vec3 & size )

Sets a new size of the whole box-type *Voxel Probe*.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The box-type *Voxel Probe* size along X, Y and Z axes.

## Math:: vec3 getBoxSize () const

Returns the current size of the whole box-type *Voxel Probe*.
### Return value

Current box-type *Voxel Probe* size along X, Y and Z axes.
## void setBakeQuality ( LightVoxelProbe::BAKE_QUALITY quality )

Sets a new baking quality for the *Voxel Probe*.
### Arguments

- *[LightVoxelProbe::BAKE_QUALITY](../../../api/library/lights/class.lightvoxelprobe_cpp.md#BAKE_QUALITY)* **quality** - The baking quality for the *Voxel Probe*, one of [BAKE_QUALITY](#BAKE_QUALITY) values.

## LightVoxelProbe::BAKE_QUALITY getBakeQuality () const

Returns the current baking quality for the *Voxel Probe*.
### Return value

Current baking quality for the *Voxel Probe*, one of [BAKE_QUALITY](#BAKE_QUALITY) values.
## void setBlendMode ( LightVoxelProbe::BLEND mode )

Sets a new blending mode for the *Voxel Probe*.
### Arguments

- *[LightVoxelProbe::BLEND](../../../api/library/lights/class.lightvoxelprobe_cpp.md#BLEND)* **mode** - The blending mode for the *Voxel Probe*, one of [BLEND](#BLEND) values.

## LightVoxelProbe::BLEND getBlendMode () const

Returns the current blending mode for the *Voxel Probe*.
### Return value

Current blending mode for the *Voxel Probe*, one of [BLEND](#BLEND) values.
---

## static LightVoxelProbePtr create ( )

Constructor. Creates a new *Voxel Probe* with default parameters.
## Math:: ivec3 getResolution ( )

Returns the resolution of the *Voxel Probe* according to the voxel size.
### Return value

Resolution of the *Voxel Probe* along X, Y and Z axis, in voxels.
## static int type ( )

Returns the type of the node.
### Return value

[LightVoxelProbe](../../../api/library/nodes/class.node_cpp.md#LIGHT_VOXEL_PROBE) type identifier.
## long long getVideoMemoryUsage ( )

Returns a value defining how much memory the light texture takes according to its size. The memory is calculated in accordance to the following formula: ***Memory** = **SizeX** � **SizeY** � **SizeZ** � **Sides** � **FormatMemory***
- **SizeX, SizeY, SizeZ** - the dimensions of the 3D light texture, in voxels.
- **Sides** - number of sides of each voxel, equal to 6.
- **FormatMemory** - a memory usage amount for the texture in RGBA16 format, equal to 8.


### Return value

A texture memory usage, in bytes.
