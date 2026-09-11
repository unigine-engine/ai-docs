# Unigine::LightVoxelProbe Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Light


This class allows creating and managing *[Voxel Probe](../../../objects/lights/voxelprobe/index.md)* sources.


## LightVoxelProbe Class

### Members

## void setTextureFilePath ( string path )

Sets a new file path for the lighting texture used for the *Voxel Probe*.
### Arguments

- *string* **path** - The path to the texture file.

## String getTextureFilePath () const

Returns the current file path for the lighting texture used for the *Voxel Probe*.
### Return value

Current path to the texture file.
## void setBakeVisibilityVoxelProbe ( int probe )

Sets a new value indicating if other *Voxel Probe* light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *int* **probe** - The baking of other *Voxel Probe* light sources to the *Voxel Probe*

## int isBakeVisibilityVoxelProbe () const

Returns the current value indicating if other *Voxel Probe* light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

Current baking of other *Voxel Probe* light sources to the *Voxel Probe*
## void setBakeVisibilityLightProj ( int proj )

Sets a new value indicating if projected light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *int* **proj** - The baking of projected light sources to the *Voxel Probe*

## int isBakeVisibilityLightProj () const

Returns the current value indicating if projected light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

Current baking of projected light sources to the *Voxel Probe*
## void setBakeVisibilityLightOmni ( int omni )

Sets a new value indicating if omni light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *int* **omni** - The baking of omni light sources to the *Voxel Probe*

## int isBakeVisibilityLightOmni () const

Returns the current value indicating if omni light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

Current baking of omni light sources to the *Voxel Probe*
## void setBakeVisibilityLightWorld ( int world )

Sets a new value indicating if world light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *int* **world** - The baking of world light sources to the *Voxel Probe*

## int isBakeVisibilityLightWorld () const

Returns the current value indicating if world light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

Current baking of world light sources to the *Voxel Probe*
## void setBakeVisibilitySky ( int sky )

Sets a new value indicating if lighting from the sky is to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *int* **sky** - The baking of lighting from the sky to the *Voxel Probe*

## int isBakeVisibilitySky () const

Returns the current value indicating if lighting from the sky is to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

Current baking of lighting from the sky to the *Voxel Probe*
## void setBakeVisibilityEmission ( int emission )

Sets a new value indicating if emission light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Arguments

- *int* **emission** - The baking of emission light sources to the *Voxel Probe*

## int isBakeVisibilityEmission () const

Returns the current value indicating if emission light sources are to be baked to the *Voxel Probe*. you can use this option together with [additive blending](#BLEND_ADDITIVE) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Voxel Probes* independent of each other and combine them to produce some sort of dynamic GI effect.
### Return value

Current baking of emission light sources to the *Voxel Probe*
## void setBakeVisibilityLightmap ( int lightmap )

Sets a new value indicating if the lightmapped surfaces are to be baked to the *Voxel Probe*.
### Arguments

- *int* **lightmap** - The baking of lightmapped surfaces to the *Voxel Probe*

## int isBakeVisibilityLightmap () const

Returns the current value indicating if the lightmapped surfaces are to be baked to the *Voxel Probe*.
### Return value

Current baking of lightmapped surfaces to the *Voxel Probe*
## void setBakeInternalVolume ( int volume )

Sets a new internal volume baking mode for the *Voxel Probe* (voxels that don't touch geometry).
> **Notice:** If internal volume baking is disabled, only the voxels covering geometry are baked while empty ones are skipped.


### Arguments

- *int* **volume** - The Internal volume baking mode to be set. One of the [LIGHT_VOXEL_PROBE_BAKE_INTERNAL_VOLUME_*](#BAKE_INTERNAL_VOLUME_HALF) values.

## int getBakeInternalVolume () const

Returns the current internal volume baking mode for the *Voxel Probe* (voxels that don't touch geometry).
> **Notice:** If internal volume baking is disabled, only the voxels covering geometry are baked while empty ones are skipped.


### Return value

Current Internal volume baking mode to be set. One of the [LIGHT_VOXEL_PROBE_BAKE_INTERNAL_VOLUME_*](#BAKE_INTERNAL_VOLUME_HALF) values.
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

Sets a new intensity of the material's original diffuse lighting, as if the *Translucent* parameter were set to 0. Fine-tuning the current parameter can help correct artifacts caused by , such as excessive darkening on materials.
### Arguments

- *float* **indirect** - The intensity of the original diffuse lighting on the material

## float getDiffuseTranslucentIndirect () const

Returns the current intensity of the material's original diffuse lighting, as if the *Translucent* parameter were set to 0. Fine-tuning the current parameter can help correct artifacts caused by , such as excessive darkening on materials.
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
## void setAttenuationDistance ( vec3 distance )

Sets a new distance from the light source shape, at which the light source doesn't illuminate anything.
### Arguments

- *vec3* **distance** - The distance from the light source shape, in units, at which the light source doesn't illuminate anything.

## vec3 getAttenuationDistance () const

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
## void setBoxSize ( vec3 size )

Sets a new size of the whole box-type *Voxel Probe*.
### Arguments

- *vec3* **size** - The box-type *Voxel Probe* size along X, Y and Z axes.

## vec3 getBoxSize () const

Returns the current size of the whole box-type *Voxel Probe*.
### Return value

Current box-type *Voxel Probe* size along X, Y and Z axes.
## void setBakeQuality ( int quality )

Sets a new baking quality for the *Voxel Probe*.
### Arguments

- *int* **quality** - The baking quality for the *Voxel Probe*, one of [BAKE_QUALITY](#BAKE_QUALITY) values.

## int getBakeQuality () const

Returns the current baking quality for the *Voxel Probe*.
### Return value

Current baking quality for the *Voxel Probe*, one of [BAKE_QUALITY](#BAKE_QUALITY) values.
## void setBlendMode ( int mode )

Sets a new blending mode for the *Voxel Probe*.
### Arguments

- *int* **mode** - The blending mode for the *Voxel Probe*, one of [BLEND](#BLEND) values.

## int getBlendMode () const

Returns the current blending mode for the *Voxel Probe*.
### Return value

Current blending mode for the *Voxel Probe*, one of [BLEND](#BLEND) values.
---

## static LightVoxelProbe ( )

Constructor. Creates a new *Voxel Probe* with default parameters.
## ivec3 getResolution ( )

Returns the resolution of the *Voxel Probe* according to the voxel size.
### Return value

Resolution of the *Voxel Probe* along X, Y and Z axis, in voxels.
## static int type ( )

Returns the type of the node.
### Return value

[LightVoxelProbe](../../../api/library/nodes/class.node_usc.md#LIGHT_VOXEL_PROBE) type identifier.
## long getVideoMemoryUsage ( )

Returns a value defining how much memory the light texture takes according to its size. The memory is calculated in accordance to the following formula: ***Memory** = **SizeX** � **SizeY** � **SizeZ** � **Sides** � **FormatMemory***
- **SizeX, SizeY, SizeZ** - the dimensions of the 3D light texture, in voxels.
- **Sides** - number of sides of each voxel, equal to 6.
- **FormatMemory** - a memory usage amount for the texture in RGBA16 format, equal to 8.


### Return value

A texture memory usage, in bytes.
