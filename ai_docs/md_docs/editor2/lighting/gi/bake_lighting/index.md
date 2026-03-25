# Bake Lighting Window


*Bake Lighting* is a tool that incorporates all light baking tasks. It is used for the following operations:


- Calculate and bake global illumination into [lightmaps](../../../../editor2/lighting/gi/lightmaps.md) assigned to surfaces.
- Calculate static [voxel-based GI](../../../../editor2/lighting/gi/voxel_probes.md) and put it into generated voxel lighting maps.
- Calculate reflection cubemaps and cutout depth textures for *[Environment Probes](../../../../editor2/lighting/gi/env_probes.md)* in static mode.
- Calculate [shadow maps](../../../../editor2/lighting/lights/shadows.md) for light sources in static mode.


The *Bake Lighting* tool enables you to improve performance by dropping the most of light and shadow computations.


> **Notice:** To open the *Bake Lighting* window, choose *Tools -> Bake Lighting* in the Menu Bar or click the gear icon in the upper-right corner of the UnigineEditor.
> To learn how to use the tool, watch [this video tutorial](#video_tutorial).


![](tool_ui.png)

*Bake Lighting Tool*


### See Also


- Light baking is available via code by using the [BakeLighting](../../../../api/library/lights/class.bakelighting_cpp.md) Class.
- [Video Tutorial: Global Illumination](../../../../videotutorials/essentials/global_illumination.md).


## Workflow


Basically, light baking is available if there is at least one of the following entities is in the scene:


- [Voxel Probe](../../../../editor2/lighting/gi/voxel_probes.md)
- *[Environment Probe](../../../../editor2/lighting/gi/env_probes.md)* in Static mode with **Grab by Bake Lighting** enabled.
- *Mesh Static* with at least one surface that has **[Lightmaps](../../../../editor2/node_parameters/visual_representation/index.md#surface_lightmaps)** enabled and the **Bake Unique Texture** mode selected.
- Light source in *[Static](../../../../editor2/lighting/gi/index.md#bake_modes)* mode.


To get the lighting baked, perform the following steps:


1. Prepare the scene: set up lighting and emissive geometry, select the [Light Baking Mode](../../../../editor2/lighting/gi/index.md#bake_modes) and [Lighting Modes](../../../../editor2/lighting/gi/index.md#lighting_modes) for surfaces, hide or exclude unnecessary and dynamic objects from calculations via [masking](../../../../objects/lights/voxelprobe/index.md#viewport_mask) and/or adjusting [surface flags](../../../../editor2/node_parameters/visual_representation/index.md#cast_gi), enable **Lightmaps** and select the **[Lightmaps Mode](../../../../editor2/node_parameters/visual_representation/index.md#lightmaps_mode)** for surfaces of Mesh Static objects intended to be lightmapped. [![](workflow_1_sm.png)](workflow_1.png)
2. Create and place [voxel probes](../../../../objects/lights/voxelprobe/index.md) at the places where the lighting remains relatively static (e.g. interiors, outdoor buildings, and immovable objects). Select **Half** or **Full** **[Bake Internal Volume](../../../../objects/lights/voxelprobe/index.md#bake_volume)** mode for voxel probes to illuminate dynamic objects that move within their volume. [![](workflow_2_sm.png)](workflow_2.png) > **Notice:** Place voxel probes inside other voxel probes to create insets defining the areas that require higher detail. Note that voxel probes with the [additive blending](../../../../objects/lights/voxelprobe/index.md#additive_blending) mode enabled cannot be used for this purpose, as they are blended instead of replacing each other.
3. Create non-dynamic [environment probes](../../../../objects/lights/envprobe/index.md) and cover the areas which require appropriate reflections on reflective materials. [![](workflow_3_sm.png)](workflow_3.png) > **Notice:** Disable the [Grab by Bake Lighting](../../../../objects/lights/envprobe/index.md#grab_by_bake) parameter for probes, the cubemap texture of which should not be modified by the Bake Lighting tool. This is applicable for cases when you do not want to modify your assets.
4. Adjust the *[Baking Settings](../../../../objects/lights/voxelprobe/index.md#bake_params)* of probes and the [settings of the *Bake Lighting* tool](#settings).
5. Click **Bake** to begin light baking for all enabled objects and light sources (or **Bake selected lights** to affect only selected objects and light sources) and wait for the process to complete. You can also click **Bake All Lighting** in the right corner of the top toolbar. ![](open_tool.png) At this stage, the Bake Lighting tool performs the following: All generated textures will be saved to the `bake_lighting` folder of your data project's folder. > **Notice:** You can stop the process at any moment and you will be prompted to keep the achieved result or restore the previous textures.

  - **For each enabled *[Omni](../../../../objects/lights/omni/index.md)* and *[Projected](../../../../objects/lights/proj/index.md)* light source in the [Static](../../../../objects/lights/parameters/index.md#light_mode) mode** the [shadow map is grabbed](../../../../editor2/lighting/lights/shadows.md#cached) and saved in the *Depth Texture* asset.
  - **For each enabled *[World](../../../../objects/lights/world/index.md)* light source in the *[Static Shadow Cascade](../../../../objects/lights/world/index.md#shadow_cascade_mode)* mode** the [shadow map is grabbed](../../../../editor2/lighting/lights/shadows.md#cached) and saved in the *Depth Texture* asset.
  - **For each *Mesh Static* surface with [Lightmaps](../../../../editor2/node_parameters/visual_representation/index.md#lightmaps_enabled) enabled and [Bake Unique Texture](../../../../editor2/node_parameters/visual_representation/index.md#lightmaps_mode) mode selected**, lighting is baked into a [lightmap texture](../../../../editor2/lighting/gi/lightmaps.md).
  - **For each enabled *[Environment Probe](../../../../objects/lights/envprobe/index.md)***, a cubemap is grabbed from the center point of the probe depending on its parameters. If the environment probe has the **[Cutout By Shadow](../../../../objects/lights/envprobe/index.md#cutout_by_shadow)** option enabled, a depth texture is grabbed for the probe as well.
  - **For each enabled *[Voxel Probe](../../../../objects/lights/voxelprobe/index.md)***, a cycle over all the voxels is performed in order to grab lighting from 6 faces of a voxel and append it to the resulting 3D lighting map. ![](workflow_5.png)
6. Enable post and camera effects. [![](workflow_4_sm.png)](workflow_4.png)


## Bake Lighting Settings


### Bake Static Shadows For Lights


![](settings_shadows.png)


| Bake Static Shadows For Lights | Enable baking of [cached shadows](../../../../editor2/lighting/lights/shadows.md#cached) for static light sources. |
|---|---|
| Automatic Rebake | Enable auto-rebake of shadows on transforming a static light source or changing its parameters. |


### Bake Lightmaps For Surfaces


![](settings_lightmaps.png)


| Bake Lightmaps For Surfaces | Enable baking of [lightmaps](../../../../editor2/lighting/gi/lightmaps.md) for surfaces. |
|---|---|
| Baking Viewport Masks | For the light or surface to contribute to static GI, their viewport masks should match the Baking *[Viewport Mask](../../../../principles/bit_masking/index.md#viewport)*. |
| Quality | Baking quality preset. |
| Far Clipping | Far clipping distance for light rays. |


### Bake Voxel Probes


![](settings_voxel.png)


| Bake Voxel Probes | Enable baking of [voxel-based GI](../../../../editor2/lighting/gi/voxel_probes.md) to voxel probes. |
|---|---|
| Voxel Size Multiplier | Multiplier for the *[Voxel Size](../../../../objects/lights/voxelprobe/index.md#voxel_size)* parameter for each voxel probe. |


### Bake Environment Probes


![](settings_env.png)


| Bake Environment Probes | Enable baking of [reflection cubemaps](../../../../editor2/lighting/gi/env_probes.md) to environment probes. |
|---|---|
| Automatic Rebake | Enable auto-rebake of the cubemap of an Environment Probe on transforming it or changing its parameters. |


### Common Settings


![](settings_common.png)


| Number of Bounces | Number of light ray bounces. |
|---|---|
| Samples per Frame | Number of sampling units processed and visualized simultaneously each frame (samples for lightmaps and voxels for Voxel Probes): - **Auto** - the number of samples is adjusted automatically to optimize performance of baking process. - **Manual** - the number of samples is set manually. > **Notice:** The parameter is available for changing during the baking process. Higher values cause longer user interface response but accelerate the calculations. |


### Buttons


| Bake Selected | Starts baking for the *selected* static lights, probes and lightmapped surfaces regardless of whether they are enabled or not. |
|---|---|
| Bake/Stop | Starts baking for all *enabled* static lights, probes and lightmapped surfaces in the scene. |


### Progress Bars


The following progress bars are shown in the viewport during the process of light baking:


![](progress_bars.png)


| Node/Surface | Progress of light baking for the current node/surface at the moment. |
|---|---|
| Bounce | Progress of calculating the current bounce. |
| Overall | Overall progress of light baking for all nodes in the scene. |


## Video Tutorial


Watch the video below to learn how to work with the Bake Lighting tool.
