# Unigine.BakeLighting Class (CS)

> **Notice:** This class is a singleton.


This class allows you to [bake lighting](../../../editor2/lighting/gi/bake_lighting/index.md).


> **Warning:** **Backward compatibility for this class is not guaranteed!** Although it is exposed to public API, it is mainly intended for internal use (inside UnigineEditor). If you use it, you do this at your own risk.


## BakeLighting Class

### Enums

## LIGHTMAP_QUALITY

Light baking quality preset.
| Name | Description |
|---|---|
| **DRAFT** = 0 | Ultra baking quality. Provides the highest iterativity with the lowest sampling quality and number of rays. |
| **LOW** = 1 | Ultra baking quality. Provides low sampling quality and number of light rays. |
| **MEDIUM** = 2 | Ultra baking quality. Corresponds to stable quality level which is good for most cases. |
| **HIGH** = 3 | Ultra baking quality. Corresponds to high sampling quality and number of light rays simulated intended for release production. |
| **ULTRA** = 4 | Ultra baking quality. Might be useful to get rid of even small inconsistencies. Intended for the release production. |

### Properties

## 🔒︎ int Progress

The Overall progress of light baking.
> **Notice:** If the process of baking is not being performed at the moment, 0 is returned.


## 🔒︎ int ProgressBounce

The A value showing progress of calculating current bounce.
## 🔒︎ int ProgressLight

The Progress of light baking for the current [LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_cs.md) at the moment.
## 🔒︎ int CurrentBounce

The A bounce being calculated at the moment.
> **Notice:** If the process of baking is not being performed at the moment, 1 is returned.


## 🔒︎ Light CurrentLight

The An instance of the [LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_cs.md) being calculated at the moment.
## 🔒︎ float Timer

The time elapsed from the start of the process of baking.
## float VoxelSizeMultiplier

***Console*:**`bake_lighting_voxel_size_multiplier`The value of the voxel size multiplier parameter. by default, it is equal to 1.0f.
## int Bounces

***Console*:**`bake_lighting_bounces`The Number of all bounces.
## 🔒︎ bool IsBaking

The A value indicating if the process of baking is being performed at the moment.
## 🔒︎ int CurrentSurface

The Index of the surface during lightmaps baking; otherwise, -1.
## 🔒︎ Object CurrentObject

The Object pointer during lightmaps baking; otherwise, nullptr.
## string CacheDir

The Path to the cache folder.
## float LightmapZFar

***Console*:**`bake_lightmap_zfar`The Far clipping distance.
## int LightmapViewportMask

The Viewport mask (integer, each bit of which is used to represent a mask).
## BakeLighting.LIGHTMAP_QUALITY LightmapQuality

***Console*:**`bake_lightmap_quality`The [LIGHTMAP_QUALITY](#LIGHTMAP_QUALITY) preset.
## int SamplesPerFrame

The Number of samples.
### Members

---

## void Bake ( LightVoxelProbe [] voxel_lights , LightEnvironmentProbe [] env_lights , Light [] shadow_lights , ObjectMeshStatic [] objects , int[] surfaces )

Starts the process of light baking for all voxel and environment probes, shadow baking for light sources in static light mode and lightmaps baking for surfaces of Mesh Static objects in the given list.
### Arguments

- *[LightVoxelProbe](../../../api/library/lights/class.lightvoxelprobe_cs.md)[]* **voxel_lights** - List of voxel probes for which the process of light baking is to be performed. The order of nodes added for baking is not important.
- *[LightEnvironmentProbe](../../../api/library/lights/class.lightenvironmentprobe_cs.md)[]* **env_lights** - List of environment probes for which the process of light baking is to be performed. The order of nodes added for baking is not important.
- *[Light](../../../api/library/lights/class.light_cs.md)[]* **shadow_lights** - List of light sources in static light mode for which the process of shadow baking is to be performed. The order of lights added for baking is not important.
- *[ObjectMeshStatic](../../../api/library/objects/class.objectmeshstatic_cs.md)[]* **objects** - List of Mesh Static objects for which the process of lightmaps baking is to be performed.
- *int[]* **surfaces** - List of surfaces of Mesh Static **objects** for which the process of lightmaps baking is to be performed. > **Notice:** The number of **objects** and **surfaces** added for baking must be equal.

## void BakeAll ( bool voxel_probes = true , bool env_probes = true , bool shadow = true , bool lightmap = true )

Starts the process of light baking for all enabled voxel and environment probes, shadow baking for eanbled light sources in static light mode and lightmaps baking for enabled surfaces of Mesh Static objects in the scene.
### Arguments

- *bool* **voxel_probes** - true to enable light baking for voxel probes; otherwise, false.
- *bool* **env_probes** - true to enable light baking for environment probes; otherwise, false.
- *bool* **shadow** - true to enable shadow baking for light sources in static light mode; otherwise, false.
- *bool* **lightmap** - true to enable lightmaps baking for surfaces of Mesh Static objects; otherwise, false.

## void Stop ( bool save_results = false )

***Console*:**`bake_lighting_stop`Interrupts the process of light baking, if it is in performing state.
### Arguments

- *bool* **save_results** - true to save the obtained result; false to restore the previous content.

## void AddReadOnlyTexture ( UGUID guid )

Adds a read-only texture with the specified [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the read-only texture to be added.

## void RemoveReadOnlyTexture ( UGUID guid )

Removes the read-only texture with the specified [GUID](../../../api/library/filesystem/class.uguid_cs.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the read-only texture to be removed.

## void SetSamplesPerFrame ( int frame )

***Console*:**`bake_lighting_samples_per_frame`Sets number of voxels for voxel probes and samples for environment probes, light sources and surfaces computed and visualized per single frame.
### Arguments

- *int* **frame** - Number of samples per frame within the [1, 500] range. The default value is 1. > **Notice:** High values cause longer user interface response.

## int GetSamplesPerFrame ( )

Returns number of voxels for voxel probes and samples for environment probes, light sources and surfaces computed and visualized per single frame.
### Return value

Number of samples.
## void SetLightmapQuality ( BakeLighting.LIGHTMAP_QUALITY quality )

***Console*:**`bake_lightmap_quality`Sets the global baking quality for lightmaps.
### Arguments

- *[BakeLighting.LIGHTMAP_QUALITY](../../../api/library/lights/class.bakelighting_cs.md#LIGHTMAP_QUALITY)* **quality** - One of [LIGHTMAP_QUALITY](#LIGHTMAP_QUALITY) values.

## BakeLighting.LIGHTMAP_QUALITY GetLightmapQuality ( )

***Console*:**`bake_lightmap_quality`Returns the current global baking quality for lightmaps.
### Return value

[LIGHTMAP_QUALITY](#LIGHTMAP_QUALITY) preset.
## void SetLightmapViewportMask ( int mask )

***Console*:**`bake_lightmap_viewport_mask`Sets the [viewport mask](../../../editor2/lighting/gi/bake_lighting/index.md#lightmaps) for the lightmapper. For a light or surface to contribute to static GI, their viewport masks should match the baking [viewport mask](../../../principles/bit_masking/index.md#viewport).
### Arguments

- *int* **mask** - Viewport mask (integer, each bit of which is used to represent a mask).

## int GetLightmapViewportMask ( )

Returns the current [viewport mask](../../../editor2/lighting/gi/bake_lighting/index.md#lightmaps) set for lightmapper.
### Return value

Viewport mask (integer, each bit of which is used to represent a mask).
## void SetLightmapZFar ( float zfar )

***Console*:**`bake_lightmap_zfar`Sets the far clipping distance for light rays used when baking lightmaps.
### Arguments

- *float* **zfar** - Far clipping distance.

## float GetLightmapZFar ( )

***Console*:**`bake_lightmap_zfar`Returns the far clipping distance for light rays.
### Return value

Far clipping distance.
## void SetCacheDir ( string dir )

Sets the path to the directory that stores temporary cache textures during lightmaps baking process. By default, the `bin/unigine_bake_lighting_cache` project's folder is set.
> **Notice:** It is recommended to specify a path to a non-existing folder to avoid losing files.

### Arguments

- *string* **dir** - An absolute path or a relative path to the `bin` folder.

## string GetCacheDir ( )

Returns the current path set for the directory that stores temporary cache textures during lightmaps baking process. By default, the `bin/unigine_bake_lighting_cache` project's folder is set.
### Return value

Path to the cache folder.
## Object GetCurrentObject ( )

Returns the object currently being processed when baking lightmaps.
### Return value

Object pointer during lightmaps baking; otherwise, nullptr.
## int GetCurrentSurface ( )

Returns the index of the surface currently being processed when baking lightmaps.
### Return value

Index of the surface during lightmaps baking; otherwise, -1.
