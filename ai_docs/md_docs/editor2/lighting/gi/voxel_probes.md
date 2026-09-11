# Voxel-Based GI


**Voxel-Based Global Illumination** is a static GI technique projecting a precalculated 3D lighting map into a box-shaped voxel volume. This approach uses spatial modulation, that is why there is no need in UV coordinates.


![](../../../migration/from_unity/unigine_voxel_gi.jpg)


Voxel-based GI is provided by *[Voxel Probes](../../../objects/lights/voxelprobe/index.md)*.


Light baking is performed using the *[Bake Lighting Tool](../../../editor2/lighting/gi/bake_lighting/index.md)*.


### See Also


- Light baking is available via code by using the *[BakeLighting](../../../api/library/lights/class.bakelighting_cpp.md)* Class.
- [Video Tutorial: Global Illumination](../../../videotutorials/essentials/global_illumination.md).
- Quick video guide: [How To Bake GI to Voxel Probes](../../../videotutorials/how_to/how_to_rendering/gi.md).


## Ambient Lighting


The primary application of Voxel Probes is ambient lighting. When baked, a Voxel Probes illuminates everything within its volume with ambient lighting providing a decent simulation of global illumination including ambient occlusion, light bounces and diffuse interreflections.


![](voxel_gi_1.png) ![](voxel_gi_0.png)


Voxel probe is highly useful for shading dynamic objects that move within its bounds. The [**Bake Internal Volume**](../../../objects/lights/voxelprobe/index.md#bake_volume) parameter enables to choose the quality and time required to bake GI for empty voxels (i.e. the voxels that do not cover any geometry).


![](../../../migration/from_unity/unigine_voxel_internal.gif)


## Workflow


To bake global illumination into a Voxel Probe, some preparations are needed.


### Preparing The Content


For a surface to contribute to static GI, it must have the [*Lighting Mode*](../../../editor2/lighting/gi/index.md#lighting_modes) set to **Static** or have the [**Cast Global Illumination**](../../../editor2/node_parameters/visual_representation/index.md#cast_gi) option enabled in the *Advanced Lighting Mode*. It must be turned off for dynamic surfaces.


![](lighting_mode_static.png) ![](cast_gi.png)


> **Notice:** [Lightmapped surfaces](../../../editor2/lighting/gi/lightmaps.md) are not shaded by Voxel Probes.


Set up light sources in the scene:


- For [light sources](../../../editor2/lighting/lights/index.md#lights) that should contribute to global illumination, select the **Static** mode. *Dynamic* lights will be ignored. Only indirect lighting from lights is baked, so light sources are to be kept enabled to provide direct lighting and specular highlights.
- For [emissive](../../../editor2/lighting/lights/index.md#emissive) surfaces (having *Emission* state in the material parameters enabled) also enable the *Emission Bake GI* option. Both direct and indirect (bounced) lighting from emissive materials is baked.


> **Notice:** It is not recommended to bake lighting for voxel probes stored in multiple [*Node References*](../../../objects/nodes/reference/index.md) that refer to the same `.node` asset � the assigned textures will be lost. However, you can save a voxel probe to a node reference after baking and clone, if needed.


### Creating Voxel Probes


1. Create and place one or several Voxel Probes at the places where the lighting remains relatively static (e.g. interiors, outdoor buldings, immovable objects). [![](bake_lighting/workflow_2_sm.png)](bake_lighting/workflow_2.png) > **Notice:** Place voxel probes inside other voxel probes to create insets defining the areas that require higher detail. Note that voxel probes with the [additive blending](../../../objects/lights/voxelprobe/index.md#additive_blending) mode enabled cannot be used for this purpose, as they are blended instead of replacing each other.
2. Set the [Common Settings](../../../objects/lights/voxelprobe/index.md#settings) of probes, such as the *Box Size* and the *Voxel Size*. By configuring these parameters you define the resolution of the voxel grid and the video memory consumed by the probe. > **Warning:** Do not use the **Scale** transform parameter to change the probe size as it causes visual artifacts.
3. Adjust the [Baking Settings](../../../objects/lights/voxelprobe/index.md#bake_params) of probes.


### Baking


![](bake_voxels.png)


1. Open the *[Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md)* window.
2. Enable **Bake Voxel Probes**. Adjust the *Voxel Size Multiplier*, if needed.
3. Adjust the Common settings:

  - Select the number of light ray bounces. Higher values will result in a brighter lighting since each voxel receives more photons.
  - Set the number of samples (voxels) calculated per frame. This parameter is available for adjustment during baking process.
4. Start baking process by clicking *Bake All Lighting* and wait for it to finish. Live preview is available. Several iterations (one per bounce) will be simulated for each Voxel Probe. ![](bake_lighting/workflow_5.png) > **Notice:** You can stop the process at any moment by using the **Stop** button and you will be prompted to keep the achieved result or restore the previous textures.
5. Upon completion, generated lightmaps will be saved in the `bake_lighting/voxel_probes` folder and assigned to the corresponding Voxel Probes.


You can check the result by selecting the **Indirect Lighting** mode in the *Rendering Debug*.


If you are not satisfied with results on certain objects, you can select surfaces and/or nodes and perform partial re-bake using different settings by clicking *Bake Selected*.


## Additional Features


### Diffuse Reflections


As each voxel of a Voxel Probe stores light data, a Voxel Probe is capable of providing *diffuse (blurred) reflections* at every spatial point within its volume provided **Bake Internal Volume** was enabled for baking. Control reflections by adjusting the [Reflections Parameters](../../../objects/lights/voxelprobe/index.md#reflections_parameters).


![](diff.gif)

*Diffuse reflections provided by a voxel probe.*


### Additive Blending


More flexibility in lighting control is available with the *[Additive Blending](../../../objects/lights/voxelprobe/index.md#additive_blending)* mode. You can use it to blend lighting of several voxel probes together and control them separately (e.g. make a separate Voxel Probe for an indoor emissive light source and blend it with another Voxel Probes with lighting baked from the sky, having the ability to enable and disable them separately).


![](additive.gif)

*Additive blending of two Voxel Probes.*


### Using Sun Color


A Voxel Probe is subject to multiplication by the sun light color if the *[Use Sun Color](../../../objects/lights/voxelprobe/index.md#sun_color)* option is enabled for it.


![](voxel_sun_color_0.png) ![](voxel_sun_color_1.png)
