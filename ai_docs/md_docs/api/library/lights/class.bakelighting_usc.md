# Unigine.BakeLighting Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class allows you to [bake lighting](../../../editor2/lighting/gi/bake_lighting/index.md).


> **Warning:** **Backward compatibility for this class is not guaranteed!** Although it is exposed to public API, it is mainly intended for internal use (inside UnigineEditor). If you use it, you do this at your own risk.


## BakeLighting Class

### Members

---

## void bake ( Vector< LightVoxelProbe > voxel_lights , Vector< LightEnvironmentProbe > env_lights , Vector< Light > shadow_lights , Vector< ObjectMeshStatic > objects , Vector<int> surfaces )

Starts the process of light baking for all voxel and environment probes, shadow baking for light sources in static light mode and lightmaps baking for surfaces of Mesh Static objects in the given list.
### Arguments

- *Vector<[LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_usc.md)>* **voxel_lights** - List of voxel probes for which the process of light baking is to be performed. The order of nodes added for baking is not important.
- *Vector<[LightEnvironmentProbe](../../../api/library/lights/class.lightenvironmentprobe_usc.md)>* **env_lights** - List of environment probes for which the process of light baking is to be performed. The order of nodes added for baking is not important.
- *Vector<[Light](../../../api/library/lights/class.light_usc.md)>* **shadow_lights** - List of light sources in static light mode for which the process of shadow baking is to be performed. The order of lights added for baking is not important.
- *Vector<[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_usc.md)>* **objects** - List of Mesh Static objects for which the process of lightmaps baking is to be performed.
- *Vector<int>* **surfaces** - List of surfaces of Mesh Static **objects** for which the process of lightmaps baking is to be performed. > **Notice:** The number of **objects** and **surfaces** added for baking must be equal.

## void bakeAll ( int voxel_probes = true , int env_probes = true , int shadow = true , int lightmap = true )

Starts the process of light baking for all enabled voxel and environment probes, shadow baking for eanbled light sources in static light mode and lightmaps baking for enabled surfaces of Mesh Static objects in the scene.
### Arguments

- *int* **voxel_probes** - **1** to enable light baking for voxel probes; otherwise, **0**.
- *int* **env_probes** - **1** to enable light baking for environment probes; otherwise, **0**.
- *int* **shadow** - **1** to enable shadow baking for light sources in static light mode; otherwise, **0**.
- *int* **lightmap** - **1** to enable lightmaps baking for surfaces of Mesh Static objects; otherwise, **0**.

## int isBaking ( )

Returns a value indicating if the process of baking is being performed at the moment.
### Return value

**1** if lighting is being baked; otherwise - **0**.
## int getCurrentBounce ( )

Returns a bounce being calculated at the moment.
> **Notice:** If the process of baking is not being performed at the moment, 1 is returned.


### Return value

Bounce number.
## int getBounces ( )

***Console*:**`bake_lighting_bounces`Returns number of all bounces.
### Return value

Number of bounces.
## int getProgress ( )

Returns overall progress of light baking.
> **Notice:** If the process of baking is not being performed at the moment, 0 is returned.


### Return value

Overall baking progress, in percents.
## int getProgressBounce ( )

Returns a value showing progress of calculating current bounce.
### Return value

Bounce calculating progress, in percents.
## float getVoxelSizeMultiplier ( )

***Console*:**`bake_lighting_voxel_size_multiplier`Returns the value of the voxel size multiplier parameter. By default, it is equal to 1.0f.
### Return value

Voxel size multiplier.
## void setBounces ( int bounces )

Sets number of bounces.
### Arguments

- *int* **bounces** - Number of bounces within the [1, 32] range. The default value is 1.

## int getProgressLight ( )

Returns progress of light baking for the current [LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_usc.md) at the moment.
### Return value

LightVoxelProbe progress, in percents.
## float getTimer ( )

Returns the time elapsed from the start of the process of baking.
### Return value

Elapsed time, in seconds.
## void setVoxelSizeMultiplier ( float multiplier )

***Console*:**`bake_lighting_voxel_size_multiplier`Sets the value of the voxel size multiplier parameter.
### Arguments

- *float* **multiplier** - Voxel size multiplier within the [0.0f, 8.0f] range. The default value is 1.

## void stop ( int save_results = false )

***Console*:**`bake_lighting_stop`Interrupts the process of light baking, if it is in performing state.
### Arguments

- *int* **save_results** - **1** to save the obtained result; **0** to restore the previous content.

## Light getCurrentLight ( )

Returns an instance of the [LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_usc.md) being calculated at the moment.
### Return value

Current LightVoxelProbe.
## void addReadOnlyTexture ( UGUID guid )

Adds a read-only texture with the specified [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the read-only texture to be added.

## void removeReadOnlyTexture ( UGUID guid )

Removes the read-only texture with the specified [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - GUID of the read-only texture to be removed.

## void setSamplesPerFrame ( int frame )

***Console*:**`bake_lighting_samples_per_frame`Sets number of voxels for voxel probes and samples for environment probes, light sources and surfaces computed and visualized per single frame.
### Arguments

- *int* **frame** - Number of samples per frame within the [1, 500] range. The default value is 1. > **Notice:** High values cause longer user interface response.

## int getSamplesPerFrame ( )

Returns number of voxels for voxel probes and samples for environment probes, light sources and surfaces computed and visualized per single frame.
### Return value

Number of samples.
## void setLightmapQuality ( int quality )

***Console*:**`bake_lightmap_quality`Sets the global baking quality for lightmaps.
### Arguments

- *int* **quality** - One of [LIGHTMAP_QUALITY](#LIGHTMAP_QUALITY) values.

## int getLightmapQuality ( )

***Console*:**`bake_lightmap_quality`Returns the current global baking quality for lightmaps.
### Return value

[LIGHTMAP_QUALITY](#LIGHTMAP_QUALITY) preset.
## void setLightmapViewportMask ( int mask )

***Console*:**`bake_lightmap_viewport_mask`Sets the [viewport mask](../../../editor2/lighting/gi/bake_lighting/index.md#lightmaps) for the lightmapper. For a light or surface to contribute to static GI, their viewport masks should match the baking [viewport mask](../../../principles/bit_masking/index.md#viewport).
### Arguments

- *int* **mask** - Viewport mask (integer, each bit of which is used to represent a mask).

## int getLightmapViewportMask ( )

Returns the current [viewport mask](../../../editor2/lighting/gi/bake_lighting/index.md#lightmaps) set for lightmapper.
### Return value

Viewport mask (integer, each bit of which is used to represent a mask).
## void setLightmapZFar ( float zfar )

***Console*:**`bake_lightmap_zfar`Sets the far clipping distance for light rays used when baking lightmaps.
### Arguments

- *float* **zfar** - Far clipping distance.

## float getLightmapZFar ( )

***Console*:**`bake_lightmap_zfar`Returns the far clipping distance for light rays.
### Return value

Far clipping distance.
## void setCacheDir ( string dir )

Sets the path to the directory that stores temporary cache textures during lightmaps baking process. By default, the `bin/unigine_bake_lighting_cache` project's folder is set.
> **Notice:** It is recommended to specify a path to a non-existing folder to avoid losing files.

### Arguments

- *string* **dir** - An absolute path or a relative path to the `bin` folder.

## string getCacheDir ( )

Returns the current path set for the directory that stores temporary cache textures during lightmaps baking process. By default, the `bin/unigine_bake_lighting_cache` project's folder is set.
### Return value

Path to the cache folder.
## Object getCurrentObject ( )

Returns the object currently being processed when baking lightmaps.
### Return value

Object pointer during lightmaps baking; otherwise, nullptr.
## int getCurrentSurface ( )

Returns the index of the surface currently being processed when baking lightmaps.
### Return value

Index of the surface during lightmaps baking; otherwise, -1.
