# Content Optimization


The main part of any virtual scene is geometry: meshes imported from 3rd party editor and objects created by means of UnigineEditor and built-in tools (e.g., *Terrain, Grass, Water*). Using objects with complex geometry and/or a great number of objects as is usually leads to application performance drop. In addition, irrational use of light sources can also raise performance issues.


Articles in this section describe main methods that can be used to optimize geometry and lighting in your scene, and, therefore, increase the performance of your project.


> **Notice:** To check the performance status of the current scene, use the [Performance Profiling Tools](../../tools/profiling/index.md) and [Content Profiler](../../editor2/assets_optimize/content_profiler/index.md). These tools can give you a hint of what you should do to improve the performance.


### See Also


Video Tutorial on [Content Optimization](../../videotutorials/essentials/content_optimization.md):


## Optimization Workflow


Before you start optimizing your scene, you need to know where the problem is.


1. **Enable profiler in runtime.** Decide on the [profiler](../../tools/profiling/index.md) you are going to run: Enabling [profilers](../../tools/profiling/index.md) in the editor is also possible and may be helpful for the content-related assessment. However, running the profiling tool in **runtime** provides a more reliable assessment.

  - [Performance Profiler](../../tools/profiling/profiler/index.md) may be enough for general assessment and first look. Run the application instance and use the console command `show_profiler 1`.
  - [Microprofile](../../tools/profiling/microprofile/index_cpp.md) should be used for a more detailed research. [Enable it in the project options](../../tools/profiling/microprofile/index_cpp.md#enable_disable) before running the application instance or use the console command `microprofile_enabled`. To visualize the profiling data, follow [these instructions](../../tools/profiling/microprofile/index_cpp.md#web_browser_visualization).
2. **Define the target.** The most common optimization marker is that each frame should take no more than 16.66 ms, which means that your application aims to run at 60 frames per second (fps). Compare it with the current values available in profilers. ![Data in Performance Profiler](totals.png) *Data in Performance Profiler*
3. **Detect the problem side: CPU or GPU.** In Performance Profiler, check the *Total CPU* and *Total GPU* [Performance Profiler](../../tools/profiling/profiler/index.md#generic) values. In Microprofile, assess the time spent by the engine on [CPU and GPU](../../tools/profiling/microprofile/index_cpp.md#performance_data). If the time spent on either of these sides exceeds the target time limit, it definitely requires a closer look.

  - If the issue is CPU-bound, [add markers to code](../../tools/profiling/microprofile/index_cpp.md#app_logic_cpp) to make the details visible in Microprofile as well, detect bottlenecks in your code and optimize the logic.
  - If the issue is GPU-bound, apply the suitable content optimizations available in this section.


Some of the recommendations may be inapplicable to your project and some of them may not provide the desired results, therefore use common sense and compare the results before and after optimization activities to make sure that they are useful for your case.


### Check the number of triangles


These values are provided by the *[Rendering](../../tools/profiling/profiler/index.md#render)* section of Performance Profiler.


![](triangles.png)


For a faster scene the total number of triangles should tend to a possible minimum (in practice, not exceeding several millions of triangles).


If your scene is well beyond these limits, you might consider applying some of the optimization techniques listed here.


> **Notice:** Keep in mind that even if you don't see a 3D model in the viewport, it doesn't necessarily mean that this model is not rendered. That is, it still might be rendered and take the resources that otherwise may be released and used for something else.


#### Visibility Settings


Use common sense and personal experience to decide on what values should be set for various objects in your scene: for example, small objects are not discernible at a big distance, why setting an infinite visibility for them. Based on this you can:


- Configure visibility distance for all objects [globally](../../editor2/settings/render_settings/visibility_distances/index.md) or [individually](../../principles/world_management/index.md#visible).
- Configure [levels of detail](../../content/optimization/geometry/lods/index.md) to simplify a model at a distance, thus reducing the rendered number of triangles.
- Consider using [occlusion culling](../../content/optimization/geometry/culling/index.md) to avoid rendering of objects that are hidden behind a bigger object.


#### Optimize Your Model


Assess the approach that was used at creating the models and consider if they can be optimized for a better performance when rendered in real time:


- Don't create one inseparable mesh for a big model (such as a building) uniting a great number of elements (doors, poles, stairs, etc.), otherwise you won't be able to use various optimization tools available in the engine (such as [clusters and clutters](../../content/optimization/geometry/cluster_clutter/index.md) that can speed up rendering of numerous identical parts and reduce performance costs).
- Use [impostors](../../content/optimization/geometry/impostors/index.md) wherever applicable (background/distant vegetation and some other distant objects quite often don't require geometry, so you can just replace the model with a flat square photo of the model � just two triangles, it's definitely less than any model that you have).
- Make sure that the potential of a material is used to the full extent: for example, small bumps and curves may be implemented not as the object geometry, but using the normal map ([displacement sample](../../content/materials/graph/samples/displacement/index.md)). Check [Art Samples](../../content/samples/index.md) to find more ideas.
- Inspect the content in your scene carefully, you might have added objects that you don't use (hidden somewhere inside a building or underneath the scene). Remove them, otherwise they'll also affect performance.


#### Simplify Shadows


The number of triangles rendered for shadows also can be significally reduced in a number of ways:


- A shadow is a projection of a model that's why a shadow cast by a model contains the same number of triangles as the model. But any shadow definitely doesn't require so many details. Use the most simplified LOD to cast shadows: enable shadow casting by that LOD and disable it for all other LODs.
- Shadows are not necessarily required in the distance. Configure the shadows visibility distance.
- Disable shadows cast by objects and enable screen-space shadows to check if they will be enough for your project. If you are dissatisfied by screen-space shadows at a short range, consider using them starting from a certain distance and configure shadow casting for all objects correspondingly.
- Use [static shadows](../../content/optimization/lights/index.md#static_light) for objects that won't change their position, and the light source won't also change its position.
- Use shadow settings sparingly (such as [Filter noise and Penumbra noise](../../editor2/settings/render_settings/shadows/index.md))


#### Optimize Light


Dynamic lights affect performance, therefore develop a habit of replacing them with static lights or even faking them wherever possible. This is primarily applicable in indoor scenes and scenes with unchanging light conditions. UNIGINE has a set of tools and approaches for that:


- [Voxel Probes](../../objects/lights/voxelprobe/index.md) contain indirect light baked from static light sources, so that an object moving inside the probe is shaded appropriately.
- [Billboards](../../objects/objects/billboards/index.md), [Volumetric Objects](../../objects/effects/volumetrics/index.md) may [represent a light source visually](../../content/optimization/lights/index.md#fake_lighting), but without providing any actual illumination.
- [Static Lighting](../../content/optimization/lights/index.md#static_light) may be used for night scenes. You can find a simplified example for that in the *[Lighting](../../content/samples/lighting_samples/lights.md)* section of *Art Samples*.
- [Lightmaps](../../editor2/lighting/gi/lightmaps.md) store brightness and reflected color of lit surfaces and can be used in static scenes.


### Use Proper Shaders


Use shaders sparingly and only for intended use: for example, using the Alpha Blend shader would cost you more performance than using a shader for non-transparent materials, and if your material is actually non-transparent you'll use extra resources in vain.


You can use the corresponding helper to highlight the surfaces in the scene that use transparent materials (*Helpers -> Transparent*).


- Use non-transparent materials as much as possible.
- To imitate elements that have holes (such as wire mesh or picket fence, or torn fabric) use Alpha Test material.
- Use Alpha Blend for glass only.


### Water


It makes no sense to use the *[Global Water](../../objects/objects/water/water_object.md)* object when you only need a small pond or a river, and you'll never go underwater � the object will consume resources, but you won't make the benefit of the features it provides. *[Water Mesh](../../objects/objects/water/water_mesh.md)* will be enough in this case.


If your scene indeed needs the Global Water features, use the corresponding [optimization techniques](../../content/optimization/water/index.md).


### Other Rendering Optimizations


- [Optimize landscape terrain](../../content/optimization/terrain/index.md), consider using [compression for the Landscape Layer Map](../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md#lmap_compression) to ensure smooth streaming.
- Configure global settings appropriately: for example, set the render settings to the minimum acceptable ones, do not use ultra settings for the options you don't use in your project at all.
- [Configure streaming settings](../../principles/data_streaming/index.md#usage_limits): limit the memory available to the application to avoid crashes and find the balance between performance and memory consumption (*Settings -> Streaming*).
- Disable buffers that you don't use.
- Use the [Cleaner](../../editor2/cleaner/index.md) tool to detect unused resources stored in your project folder and remove them to reduce the project size.


## Articles in This Section

- [Geometry Optimization](../../content/optimization/geometry/index.md)

  - [Working with Large Number of Objects](../../content/optimization/geometry/cluster_clutter/index.md)
  - [Setting Up LODs](../../content/optimization/geometry/lods/index.md)
  - [Optimizing Vertex Density](../../content/optimization/geometry/vertex_density/index.md)
  - [Analyzing Quad Overdraw](../../content/optimization/geometry/quad_overdraw/index.md)
  - [Using Impostors](../../content/optimization/geometry/impostors/index.md)
  - [Switching Nodes On and Off](../../content/optimization/geometry/switcher/index.md)
  - [Occlusion Culling](../../content/optimization/geometry/culling/index.md)
  - [Optimizing Grass](../../content/optimization/geometry/grass/index.md)

- [Textures Optimization](../../content/optimization/textures/index.md)

- [Materials Optimization](../../content/optimization/materials/index.md)

- [Lights Optimization](../../content/optimization/lights/index.md)

- [Dynamic Reflections Optimization](../../content/optimization/reflections/index.md)

- [Water Optimization](../../content/optimization/water/index.md)

- [Terrain Optimization](../../content/optimization/terrain/index.md)

- [Physics Optimization](../../content/optimization/physics/index.md)
