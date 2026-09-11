# Global Illumination


Global Illumination (GI) is a set of techniques intended to simulate realistic light propagation in a virtual environment.


The following comparison shows the use of global illumination in a scene with two light sources: a red *[Omni Light](../../../objects/lights/omni/index.md)* and a *[World Light](../../../objects/lights/world/index.md)*.


The left image shows the scene illuminated with direct light only, so that we see only silhouettes of unlit objects and a large number of details is hidden in the darkness.


The right image shows the scene with both direct and indirect light, which makes it look way more realistic and consistent.


![](bake_lighting/lighting_direct.png) ![](bake_lighting/lighting_indirect.png)


UNIGINE provides both realtime and precomputed solutions for GI simulation.


### See Also


- [Video Tutorial: Global Illumination](../../../videotutorials/essentials/global_illumination.md).


## Static GI


Static Global Illumination is mainly applicable to static unchanging environments and implies baking of lighting in order to drop expensive calculations and keep the performance high.


### Light Baking


The computation of indirect lighting is a very expensive task for the processing unit, so it is usually performed once at the development stage (lighting is baked) and the results are used later for static lighting at run time.


*Baking of lighting* is the way of precomputing and storing data that describes how light rays bounce around static geometry causing *indirect lighting*. Adding indirect lighting to modelling helps significantly improve the realistic look of the scene.


The following approaches are available:


- [Lightmapping](../../../editor2/lighting/gi/lightmaps.md).
- [Voxel-based GI](../../../editor2/lighting/gi/voxel_probes.md).
- Using *[Environment Probes](../../../editor2/lighting/gi/env_probes.md#ambient)*.


You can [combine](#combining) these techniques to achieve the best results.


> **Notice:** Lighting from all types of [Light Sources](../../../editor2/lighting/lights/index.md) is baked, however, note that both *direct* and *indirect* (bounced) light is baked from *[emissive](../../../editor2/lighting/lights/index.md#emissive)* objects, while [light sources](../../../editor2/lighting/lights/index.md#lights) provide only *indirect* light for baking and are to be kept enabled to provide direct light and specular highlights.


Having configured the light sources and objects, you can start light baking by pressing the corresponding button on the top toolbar. Click the gear icon to open the *Bake Lighting* window.


![](bake_lighting/open_tool.png)


The [Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md) window provides the interface to light baking settings in UnigineEditor.


### Modes of Light Sources


*Omni, Projected*, and *World light* sources have the **[Mode](../../../objects/lights/parameters/index.md#light_mode)** parameter that defines their contribution to the light baking process and determines if [shadows](../../../editor2/lighting/lights/shadows.md) are to be baked.


The following modes are available:


- **Dynamic**. The light source provides direct realtime lighting only. It is considered disabled while light baking is being calculated, that is why the scene remains unlit when the light is turned off after light baking. No shadows are baked. | ![](bake_lighting/bake_modes/bake_mode_realtime_on.png) | ![](bake_lighting/bake_modes/bake_mode_realtime_off.png) | |---|---| | *Dynamic light source enabled. No GI is baked.* | *Dynamic light source disabled.* |
- **Static**. The light source contributes to light baking and remains enabled all the time providing direct realtime lighting while the indirect light is being baked. When lighting is baked, such light sources are not to be moved and modified. Changing them can make lighting inconsistent and require re-baking. Shadows for *Omni, Proj*, and *World* lights are [baked](../../../editor2/lighting/lights/shadows.md#cached). | ![](bake_lighting/bake_modes/bake_mode_mixed_on.png) | ![](bake_lighting/bake_modes/bake_mode_mixed_off.png) | |---|---| | *Static light source enabled.* | *Static light source disabled. Indirect light is baked into aVoxel Probe.* |


### Lighting Modes


Use the [**Lighting Mode**](../../../editor2/node_parameters/visual_representation/index.md#lighting_mode) parameter to define how a surface contributes to lighting. The following modes are available:


- The **Static** mode is optimized for use in static global illumination, reflections and shadows. ![](surface_lighting_mode_0.png) Surfaces in the Static lighting mode block and reflect light when baking lighting to [Voxel Probes](../../../editor2/lighting/gi/voxel_probes.md) and [lightmaps](../../../editor2/lighting/gi/lightmaps.md), visible for [static reflections](../../../editor2/lighting/gi/env_probes.md#static) provided by Environment Probes and cast [cached shadows](../../../editor2/lighting/lights/shadows.md#cached), [lightmapping](../../../editor2/lighting/gi/lightmaps.md) is available for them. This option is best suitable for immovable objects of static environment.
- The **Dynamic** mode excludes the surface from use in static lighting and is suitable for dynamic shadows. Use this option for dynamic objects. ![](surface_lighting_mode_1.png)
- The **Advanced** mode enables manual adjustment of all lighting-related settings:

  - [**Shadow Mode**](../../../editor2/node_parameters/visual_representation/index.md#shadow_mode);
  - [**Cast Global Illumination**](../../../editor2/node_parameters/visual_representation/index.md#cast_gi);
  - [**Bake to Environment Probes**](../../../editor2/node_parameters/visual_representation/index.md#bake_to_environment_probes);
  - [**Lightmaps Parameters**](../../../editor2/node_parameters/visual_representation/index.md#surface_lightmaps).


### Combining Lightmaps with Probes


Voxel probes and lightmaps serve for the same purpose � static baked global illumination. Each technique has its pros and cons:


- Lightmaps provide the best available lighting quality and applicable only to static meshes.
- The quality of lighting provided by voxel probes highly depends on the voxel size, higher values require much more video memory. However, a voxel probe has internal volume baked and enables to [shade dynamic objects within its bounds](../../../editor2/lighting/gi/voxel_probes.md#ambient).


Voxel and environment probes do not affect lightmapped surfaces, therefore you can freely combine global illumination provided by these techniques.


![](combine.gif)

*Lightmaps are used for the static interior, the dynamic object is illuminated by a voxel-based GI.*


## Realtime GI


For scenes that have moving light sources and changing environment, baking of lighting is inappropriate. The following realtime approaches of GI simulation are provided in UNIGINE:


- Ambient lighting from [dynamic environment probes](../../../editor2/lighting/gi/env_probes.md). ![](gi_probes.gif)
- The **[SSRTGI](../../../editor2/settings/render_settings/global_illumination/index.md) (Screen-Space Ray-Traced Global Illumination)** technology is a set of screen-space ray tracing techniques for GI simulation with the real-time performance level. It incorporates *Screen-Space Ambient Occlusion*, *Screen-Space Global Illumination* and *Bent Normals* features. The technology doesn't require light baking, so every object and light source can be freely moved. ![](ssrtgi.gif)
- The **PSDGI (Panorama Space Dynamic Global Illumination)** is an advanced high-quality dynamic GI technique that fits best for open-world scenes. You can think of it as Screen Space Global Illumination but for a 360-degree range. Lighting is calculated using physically-correct formulas (with emissive materials taken into account) ensuring that reflections as well as diffuse lighting will become much more realistic in comparison with traditional cubemap-based techniques. You can optionally use only diffuse lighting or only specular. For example, if you use lightmaps providing maximum diffuse lighting information, the *[Raymarching Environment Probe](../../../videotutorials/how_to/how_to_rendering/enable_psdgi.md)* will improve the quality of reflections pushing it close to ray tracing in terms of quality. ![](psdgi.gif) You can put a probe somewhere in your world like you usually do, or you can attach it as a child to a camera. In *Raymarching* mode the *[Environment Probe](../../../objects/lights/envprobe/index.md)* is always rendered **dynamically** - it has no static pre-baked mode.


## Articles in This Section

- [Bake Lighting Window](../../../editor2/lighting/gi/bake_lighting/index.md)

- [Lightmapping](../../../editor2/lighting/gi/lightmaps.md)

- [Voxel-Based GI](../../../editor2/lighting/gi/voxel_probes.md)

- [Environment Probes](../../../editor2/lighting/gi/env_probes.md)
