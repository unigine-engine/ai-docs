# Unigine.BakeLighting Class (CPP)

**Header:** #include <UnigineRender.h>

> **Notice:** This class is a singleton.


This class allows you to [bake lighting](../../../editor2/lighting/gi/bake_lighting/index.md).


> **Warning:** **Backward compatibility for this class is not guaranteed!** Although it is exposed to public API, it is mainly intended for internal use (inside UnigineEditor). If you use it, you do this at your own risk.


## BakeLighting Class

### Enums

## LIGHTMAP_QUALITY

Light baking quality preset.
| Name | Description |
|---|---|
| **LIGHTMAP_QUALITY_DRAFT** = 0 | Ultra baking quality. Provides the highest iterativity with the lowest sampling quality and number of rays. |
| **LIGHTMAP_QUALITY_LOW** = 1 | Ultra baking quality. Provides low sampling quality and number of light rays. |
| **LIGHTMAP_QUALITY_MEDIUM** = 2 | Ultra baking quality. Corresponds to stable quality level which is good for most cases. |
| **LIGHTMAP_QUALITY_HIGH** = 3 | Ultra baking quality. Corresponds to high sampling quality and number of light rays simulated intended for release production. |
| **LIGHTMAP_QUALITY_ULTRA** = 4 | Ultra baking quality. Might be useful to get rid of even small inconsistencies. Intended for the release production. |

### Members

---

## void bake ( const Vector < Ptr < LightVoxelProbe > > & voxel_lights , const Vector < Ptr < LightEnvironmentProbe > > & env_lights , const Vector < Ptr < Light > > & shadow_lights , const Vector < Ptr < ObjectMeshStatic > > & objects , const Vector < int > & surfaces )

Starts the process of light baking for all voxel and environment probes, shadow baking for light sources in static light mode and lightmaps baking for surfaces of Mesh Static objects in the given list.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_cpp.md)> > &* **voxel_lights** - List of voxel probes for which the process of light baking is to be performed. The order of nodes added for baking is not important.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[LightEnvironmentProbe](../../../api/library/lights/class.lightenvironmentprobe_cpp.md)> > &* **env_lights** - List of environment probes for which the process of light baking is to be performed. The order of nodes added for baking is not important.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Light](../../../api/library/lights/class.light_cpp.md)> > &* **shadow_lights** - List of light sources in static light mode for which the process of shadow baking is to be performed. The order of lights added for baking is not important.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< [Ptr](../../../api/library/common/class.ptr_cpp.md)<[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cpp.md)> > &* **objects** - List of Mesh Static objects for which the process of lightmaps baking is to be performed.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)< int > &* **surfaces** - List of surfaces of Mesh Static **objects** for which the process of lightmaps baking is to be performed. > **Notice:** The number of **objects** and **surfaces** added for baking must be equal.

## void bakeAll ( bool voxel_probes = true , bool env_probes = true , bool shadow = true , bool lightmap = true )

Starts the process of light baking for all enabled voxel and environment probes, shadow baking for eanbled light sources in static light mode and lightmaps baking for enabled surfaces of Mesh Static objects in the scene.
### Arguments

- *bool* **voxel_probes** - true to enable light baking for voxel probes; otherwise, false.
- *bool* **env_probes** - true to enable light baking for environment probes; otherwise, false.
- *bool* **shadow** - true to enable shadow baking for light sources in static light mode; otherwise, false.
- *bool* **lightmap** - true to enable lightmaps baking for surfaces of Mesh Static objects; otherwise, false.

## bool isBaking ( ) const

Returns a value indicating if the process of baking is being performed at the moment.
### Return value

true if lighting is being baked; otherwise - false.
## int getCurrentBounce ( ) const

Returns a bounce being calculated at the moment.
> **Notice:** If the process of baking is not being performed at the moment, 1 is returned.


### Return value

Bounce number.
## int getBounces ( ) const

***Console*:**`bake_lighting_bounces`Returns number of all bounces.
### Return value

Number of bounces.
## int getProgress ( ) const

Returns overall progress of light baking.
> **Notice:** If the process of baking is not being performed at the moment, 0 is returned.


### Return value

Overall baking progress, in percents.
## int getProgressBounce ( ) const

Returns a value showing progress of calculating current bounce.
### Return value

Bounce calculating progress, in percents.
## float getVoxelSizeMultiplier ( ) const

***Console*:**`bake_lighting_voxel_size_multiplier`Returns the value of the voxel size multiplier parameter. By default, it is equal to 1.0f.
### Return value

Voxel size multiplier.
## void setBounces ( int bounces )

Sets number of bounces.
### Arguments

- *int* **bounces** - Number of bounces within the [1, 32] range. The default value is 1.

## int getProgressLight ( ) const

Returns progress of light baking for the current [LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_cpp.md) at the moment.
### Return value

LightVoxelProbe progress, in percents.
## float getTimer ( ) const

Returns the time elapsed from the start of the process of baking.
### Return value

Elapsed time, in seconds.
## void setVoxelSizeMultiplier ( float multiplier )

***Console*:**`bake_lighting_voxel_size_multiplier`Sets the value of the voxel size multiplier parameter.
### Arguments

- *float* **multiplier** - Voxel size multiplier within the [0.0f, 8.0f] range. The default value is 1.

## void stop ( bool save_results = false )

***Console*:**`bake_lighting_stop`Interrupts the process of light baking, if it is in performing state.
### Arguments

- *bool* **save_results** - true to save the obtained result; false to restore the previous content.

## Ptr < Light > getCurrentLight ( ) const

Returns an instance of the [LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_cpp.md) being calculated at the moment.
### Return value

Current LightVoxelProbe.
## void addReadOnlyTexture ( const UGUID & guid )

Adds a read-only texture with the specified [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the read-only texture to be added.

## void removeReadOnlyTexture ( const UGUID & guid )

Removes the read-only texture with the specified [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - GUID of the read-only texture to be removed.

## void setSamplesPerFrame ( int frame )

***Console*:**`bake_lighting_samples_per_frame`Sets number of voxels for voxel probes and samples for environment probes, light sources and surfaces computed and visualized per single frame.
### Arguments

- *int* **frame** - Number of samples per frame within the [1, 500] range. The default value is 1. > **Notice:** High values cause longer user interface response.

## int getSamplesPerFrame ( ) const

Returns number of voxels for voxel probes and samples for environment probes, light sources and surfaces computed and visualized per single frame.
### Return value

Number of samples.
## void setLightmapQuality ( BakeLighting::LIGHTMAP_QUALITY quality )

***Console*:**`bake_lightmap_quality`Sets the global baking quality for lightmaps.
### Arguments

- *[BakeLighting::LIGHTMAP_QUALITY](../../../api/library/lights/class.bakelighting_cpp.md#LIGHTMAP_QUALITY)* **quality** - One of [LIGHTMAP_QUALITY](#LIGHTMAP_QUALITY) values.

## BakeLighting::LIGHTMAP_QUALITY getLightmapQuality ( ) const

***Console*:**`bake_lightmap_quality`Returns the current global baking quality for lightmaps.
### Return value

[LIGHTMAP_QUALITY](#LIGHTMAP_QUALITY) preset.
## void setLightmapViewportMask ( int mask )

***Console*:**`bake_lightmap_viewport_mask`Sets the [viewport mask](../../../editor2/lighting/gi/bake_lighting/index.md#lightmaps) for the lightmapper. For a light or surface to contribute to static GI, their viewport masks should match the baking [viewport mask](../../../principles/bit_masking/index.md#viewport).
### Arguments

- *int* **mask** - Viewport mask (integer, each bit of which is used to represent a mask).

## int getLightmapViewportMask ( ) const

Returns the current [viewport mask](../../../editor2/lighting/gi/bake_lighting/index.md#lightmaps) set for lightmapper.
### Return value

Viewport mask (integer, each bit of which is used to represent a mask).
## void setLightmapZFar ( float zfar )

***Console*:**`bake_lightmap_zfar`Sets the far clipping distance for light rays used when baking lightmaps.
### Arguments

- *float* **zfar** - Far clipping distance.

## float getLightmapZFar ( ) const

***Console*:**`bake_lightmap_zfar`Returns the far clipping distance for light rays.
### Return value

Far clipping distance.
## void setCacheDir ( const char * dir )

Sets the path to the directory that stores temporary cache textures during lightmaps baking process. By default, the `bin/unigine_bake_lighting_cache` project's folder is set.
> **Notice:** It is recommended to specify a path to a non-existing folder to avoid losing files.

### Arguments

- *const char ** **dir** - An absolute path or a relative path to the `bin` folder.

## const char * getCacheDir ( ) const

Returns the current path set for the directory that stores temporary cache textures during lightmaps baking process. By default, the `bin/unigine_bake_lighting_cache` project's folder is set.
### Return value

Path to the cache folder.
## Ptr < Object > getCurrentObject ( ) const

Returns the object currently being processed when baking lightmaps.
### Return value

Object pointer during lightmaps baking; otherwise, nullptr.
## int getCurrentSurface ( ) const

Returns the index of the surface currently being processed when baking lightmaps.
### Return value

Index of the surface during lightmaps baking; otherwise, -1.
