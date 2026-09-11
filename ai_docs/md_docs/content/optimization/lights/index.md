# Lights Optimization


Light sources in the scene are resource-consuming (especially, if there are a lot of them). For example, depending on the light source type, calculation of shadows cast by the lit objects may require up to **6** rendering passes. Some type-specific settings of light sources can affect the performance, as well.


The article describes basic light optimization techniques.


> **Notice:** Light and shadow settings for each surface can be monitored using the [Surfaces](../../../editor2/assets_optimize/content_profiler/surface_profiler.md) tab of the [Content Profiler](../../../editor2/assets_optimize/content_profiler/index.md) tool.


## Common Lighting Optimizations


Some optimization approaches differ depending on the type of the light source. However, there are several common optimizations that can be applied to all light sources in the scene.


### Disabling Shadows for Surfaces


You can disable shadow rendering for some surfaces or materials. For example, it can be done for the farthest LOD surface (when the shadows don't matter).


To disable shadow rendering for a **surface**:


1. In the *[World Hierarchy](../../../editor2/interface/index.md#world_hierarchy)* window, choose the node and go to the *Surfaces* section in the *Node* tab of the *Parameters* window.
2. Select the required surfaces and toggle the *Cast Proj and Omni Shadows* parameter off. To disable shadows from the world light, toggle the *Cast World Shadows* parameter off. ![](shadows_checkboxes.png)


To disable shadow rendering for a **material**:


1. In the *[Materials Hierarchy](../../../editor2/interface/index.md#materials_hierarchy)* window, choose the material and go to the *Common* tab of the *Parameters* window.
2. Toggle the *Cast Proj and Omni Shadow* parameter off. To disable shadows from the World Light, toggle the *Cast World Shadow* parameter off. ![](mat_shadows.png)


### Enabling Static Lighting and Shadows


Dynamic lighting ensures that all shadows from moving light sources cast by moving objects are rendered correctly. This approach implies that geometry of your scene is rendered one more time each frame to calculate shadows for each *Projected* light source (or six more times � for each *Omni*). Using multiple dynamic lights in the scene and calculating shadows for them on the fly may cause a performance drop, especially when the scene contains complex geometry with lots of polygons. It can be a terrible waste of resources, when most objects and lights are static.


It�s better to avoid dynamic shadows and use baked ones for everything static wherever possible. You can replace dynamic *Omni* and *Projected* Light sources with static ones (shadows for them are precomputed and stored in depth textures).


Types of shadows to be rendered are defined by the [light�s mode](../../../objects/lights/parameters/index.md#light_mode) and shadow modes set for both [lights](../../../objects/lights/parameters/index.md#shadow_mode) and [object surfaces](../../../editor2/node_parameters/visual_representation/index.md#shadow_mode).


![](shadow_mode.png)


Depending on your needs, you can choose to render baked shadows only, or combine rendering of both baked and dynamic ones. The table below shows all possible variants of shadow settings.


![](table_shadows.png)


Thus, for a **Dynamic** light, shadows from all lit objects are rendered as dynamic.


For a **Static** light in **Static** shadow mode, only baked shadows from objects with *Mixed* shadow mode are rendered; dynamic shadows are not rendered at all.


For a **Static** light in **Mixed** shadow mode, both types of shadows are rendered: baked (from surfaces with *Mixed* shadow mode) and dynamic (from surfaces with *Dynamic* shadow mode).


Mixed mode implies that the dynamic shadow map is copied into the static [depth texture](../../../objects/lights/parameters/index.md#depth_texture) and the result is rendered. If you select a higher [resolution](../../../objects/lights/parameters/index.md#resolution), the process of copying the shadow map can take time and affect performance. Therefore, 4K resolution in the *Mixed* shadow mode makes sense if the scene has more than 1.5 million triangles, otherwise *Dynamic* mode may be faster. Moreover, pay attention to video memory consumption, as a single 4K resolution depth texture for an omni light takes about 400 MB.


> **Notice:** If shadows from static light sources are not rebaked automatically, use the *[Bake Lighting](../../../editor2/lighting/lights/shadows.md#cached)* tool.


The ***[World Light](../../../objects/lights/world/index.md)*** source works in a similar way, but it uses [shadow cascades](../../../objects/lights/world/index.md#shadow_cascade_mode). In **Dynamic** mode, shadow cascades are built dynamically relative to the camera's position, while in **Static**, they are baked and have their area defined by the light source's position. **Static** mode of the World Light is suitable as a performance optimization technique for small-area ArchViz projects where shadow cascades can be divided into two sections: walkable area with high-resolution shadows (as they're observed closely) and non-walkable area with low-resolution shadows (as they're observed from a distance). Note that changing the time of day is not available in **Static** mode, as shadow cascades are baked.


> **Notice:** The [![](../youtube_link.png)Cached Shadows](https://youtu.be/pNRIedBIyUw) video tutorial illustrates how to set and use dynamic and static shadows.


### Using Shadow Masks


A *[Shadow](../../../principles/bit_masking/index.md)* mask allows you to control rendering of shadows. You can specify which surfaces lit by a light source should cast shadows:


1. For a light source, specify the *Shadow* mask: open the *[World Hierarchy](../../../editor2/interface/index.md#world_hierarchy)* window and select your light source. In the *Shadow Mask* section of the *Node* tab in the *Parameters* window, specify the shadow mask. ![](light_source_mask.png)
2. For all surfaces that are lit by the light source and should cast shadows, specify the *[Shadow](../../../editor2/node_parameters/visual_representation/index.md#shadow_mask)* mask that matches the light source's *Shadow* mask (one bit at least).
3. For all materials applied to such surfaces, specify the matching shadow mask as well.


> **Notice:** An example of using shadow masks is available in the [![](../youtube_link.png)Content Optimization](https://youtu.be/Iqsr3fEvnis?t=702) video tutorial.


Another way to reduce perfomance load is to use simplified geometry for shadow casting:


- Create a simplified low-poly surface of an object (or use the object's final *[LOD](../../../principles/world_management/index.md#lods)*)
- Use a *[Viewport Mask](../../../principles/bit_masking/index.md#viewport)* to hide the surface from the camera
- Disable shadow casting for the original object via the *[Shadow Mask](../../../principles/bit_masking/index.md#shadow_mask)*
- Enable *[shadows](../../../principles/bit_masking/index.md#shadow_mask)* for the low-poly version so it casts the shadow instead.


![](shadow_lod.gif)


![](shadow_lod_diff.png)

*Original object casting shadows (on the left) vs. simplified shadow geometry (on the right)*


### Using Screen Space Shadows


For all types of light sources, [screen-space shadows](../../../editor2/settings/render_settings/shadows/index.md#screen_space_shadows) can be rendered instead of the shadow maps at large distances. It improves the performance, as such shadows don't depend on complexity of the geometry.


> **Notice:** Screen-space shadows depend on the screen resolution: the higher the resolution, the more accurate shadows are.


You can enable screen-space shadows in one of the following ways:


- In the Menu Bar, choose *Rendering -> Shadows -> Screen Space Shadows*.
- In the Menu Bar, choose *Windows -> Settings* and then go to the *[Shadows](../../../editor2/settings/render_settings/shadows/index.md)* section. Here you can toggle the *Screen Space Shadows* parameter on.


You can also set up per-light screen space shadows in the type-specific tabs (*Light World, Light Omni*, etc.) of the *Parameters* window.


![](ssshadows_lightomni.png)

*Screen Space Shadow Settings of Omni Light*


### Reducing Size of Light Source


All *[Omni](#omni_light)* and *[Projected](#proj_light)* light sources are subject to a common deferred optimization technique � the *Scissor Test*: for each light source a scissor rectangle is found to define its bounds and, therefore, the area of its influence. The scissor rectangle defines the size of the render target for the current light source, since everything that falls outside that region is not affected by the light at the current moment.


Enable the **[Scissors](../../../editor2/using_visual_helpers/index.md#scissors)** visual helper or use the `render_show_scissors 1` console command to enable visualization of the *Scissor Test*.


![](scissor_rectangle.png)

*Scissor rectangles for Omni light sources*


Therefore, the [size](../../../objects/lights/parameters/index.md#attenuation_distance) of a light source significantly affects the performance: the larger the screen area where the illuminated surface is rendered, the lower the light performance is. So, keep the size as small as possible.


### Engaging Interleaved Lights Rendering


In this mode lighting is rendered during the Deferred pass in half resolution (1/4 of all pixels) with subsequent reconstruction of neighboring pixels using the data from previous frames, making it possible to reduce rendering load.


![](interleaved_settings.png)

*Interleaved Lights Rendering settings*


For more details refer to the **[Interleaved Lights Rendering](../../../principles/render/interleaved_rendering/index.md)** article.


### Setting Up Visibility Distances


You can control rendering of light sources and cast shadows by specifying the *visibility distances*.


The global settings for all light sources (*[World](../../../objects/lights/world/index.md), [Omni](../../../objects/lights/omni/index.md), [Projected](../../../objects/lights/proj/index.md)*) can be specified in the *[Visibility Distances](../../../editor2/settings/render_settings/visibility_distances/index.md)* section of the *[Settings](../../../editor2/settings/index.md)* window.


![](visibility_distances.png)


For shadows - by adjusting the *[Max Visibility Distance](../../../editor2/settings/render_settings/shadows/index.md#distance)* slider in the *[Shadows](../../../editor2/settings/render_settings/shadows/index.md)* section of the *[Settings](../../../editor2/settings/index.md)* window.


![](shadow_distance_.png)

*Shadow Max Visibility Distance Parameter*


Additionally, you can set the [visibility distance](../../../objects/lights/parameters/index.md#visibility_settings) for individual light sources (*Omni, Projected*, and both *Voxel* and *Environment* probes) in the node's *Parameters* tab.


### Setting Limits For Transparent Objects


[Non-opaque](../../../editor2/materials_settings/index.md#blending) geometry is shaded on the **[Forward](../../../principles/render/sequence/index.md#transparent)** pass of the Rendering Sequence. Since all light sources are applied to each transparent surface in a cycle, it is highly recommended to keep the number of lights affecting transparent objects as low as possible for optimal performance.


Global Lights Settings include ***[Forward Per-Object Limits](../../../editor2/settings/render_settings/lights/index.md#forward_limits)*** where you can limit the number of certain light sources that affect each transparent object at a time.


![](forward.png)


To ensure a specific light renders on transparent surfaces, set its *[Rendering Transparent Order](../../../objects/lights/parameters/index.md#rendering_transparent_order)* priority in the *Parameters* tab. Rendering on transparent surfaces from lights with lower priority will be skipped if they fall outside the [limit](../../../editor2/settings/render_settings/lights/index.md#forward_limits), as the engine prioritizes higher-importance lights to avoid excessive performance cost.


![](rendering_transparent_order.png)


### Rendering Lights on Water


If your scene contains water object(s), you can disable rendering the light from the light source on them. It will significantly increase the performance.


1. Select a light source in the *World Hierarchy*. ![](select_light.png)
2. In the *Parameters* window, go to the *Render* section and toggle the *Water* parameter off. ![](disable_water.png)


## World Light


The [World Light](../../../objects/lights/world/index.md) source illuminates all objects that are positioned along the [shadows visibility distance](#visibility) thus increasing the number of calculations of shadows. So it is recommended to keep the number of *[World Light](../../../objects/lights/world/index.md)* objects**in the scene as low as possible**. For most purposes, other [light sources](../../../objects/lights/index.md) (*[Projected Light](../../../objects/lights/proj/index.md)*, etc.) are more suitable in terms of project performance.


For the *World Light*, the Engine creates [cascaded shadow maps](../../../objects/lights/world/index.md#shadow_cascade_mode) (maximum 4 cascades). Each cascade requires a separate rendering pass.


![](world_light_cascades.png)

*4 Shadow Cascades*


You can affect performance by toggling **[Static](#static_light)** mode on and decreasing the [number](../../../objects/lights/world/index.md#number_of_cascades) of rendered cascades as well as their size ([cascade borders](../../../objects/lights/world/index.md#cascadee_border)) in the *Parameters* window. However, changing the number of cascades also affects the rendered image quality, so try to find a balance.


## Omni Light


*[Omni](../../../objects/lights/omni/index.md)* light sources emit light in all directions, which allows reproducing realistic shadow casting.


![](omni_light.png)

*Omni Light in Scene*


The *Omni* light source uses **6 cameras** that generate shadow maps, so shadowing by this light source requires **6 rendering passes** and can sufficiently decrease the performance. So, keep the number of such light sources as low as possible. For better performance, you can [disable rendering of shadows created by the *Omni* light in certain directions](../../../objects/lights/omni/index.md#shadow_side) or use *[Projected](../../../objects/lights/proj/index.md)* light sources instead of the *Omni* ones.


![](omni_shadow_directions.png)

*Rendering of shadows in certain directions can be disabled*


However, there is a way to use a lot of *Omni* light sources in the scene without negative impact on the performance: **disable shadows** for them (except for [screen-space shadows](../../../editor2/settings/render_settings/shadows/index.md#screen_space_shadows)).


You can also control rendering of *Omni* lights and cast shadows by specifying [visibility distances](#visibility) for the light sources. When the camera is located at a given distance from the light source, it is turned off. The same can be specified for the cast shadows:


1. Open the *[World Hierarchy](../../../editor2/interface/index.md#world_hierarchy)* window and select an *Omni* light source.
2. In the *Parameters* window, specify the *[Distance Visibility Settings](../../../objects/lights/parameters/index.md#visibility_settings)*.


## Projected Light


*[Projected](../../../objects/lights/proj/index.md)* light sources cast light from a single point forming a light pyramid. Such light sources produces shadows that require only **1** rendering pass, so they are performance-cheap.


![](proj_light.png)

*Projected Light in Scene*


However, the influence of these light sources on performance can be also reduced by:


1. Specifying [visibility distances](#visibility) for the light sources and the cast shadows.
2. Adjusting the beam length ([attenuation distance](../../../objects/lights/parameters/index.md#attenuation_distance)) in the light's *Parameters* tab to limit the area affected by the light.


![](proj_light_attenuation.png)


## Voxel and Environment Probes


The *[Voxel Probe](../../../objects/lights/voxelprobe/index.md)* light source provides static voxel lighting and shading on an object inside the *Probe* by using a prebaked 3D lighting map. *Voxel Probe* is a required object for [baking indirect lighting from light sources in static mode](../../../editor2/lighting/gi/bake_lighting/index.md).


> **Notice:** Resolution of a 3D lighting map that the *Voxel Probe* projects, has no influence on performance. Therefore, you can use any resolution you want.


Using a *Voxel Probe* as an inset inside another *Voxel Probe* with the same size decreases performance, while the visual result will be the same as if you add a single *Voxel Probe*. However, nesting *Voxel Probes*, applying higher resolution to smaller inner probes and lower resolution to outer probes, where higher quality would be unnecessary, can reduce performance costs.


The main performance overhead in *Voxel Probe* comes from *[Cubic Filtering](../../../objects/lights/voxelprobe/index.md#ambient_parameters)*. Disable it if the linear filtering for ambient lighting is enough.


![](cubic_filtering.png)


One more setting that affects the performance is *[Reflections](../../../objects/lights/voxelprobe/index.md#reflections_enabled)*. When toggled on, *Voxel Probe* is used for both [ambient lighting](../../../objects/lights/voxelprobe/index.md#ambient_parameters) and [reflections](../../../objects/lights/voxelprobe/index.md#reflections_parameters). We recommend you to use *[Environment Probe](../../../objects/lights/envprobe/index.md)* for reflections simulation. However, if you choose to use *Voxel Probe* for this purpose, disabling the *[Cubic Filtering](../../../objects/lights/voxelprobe/index.md#reflections_parameters)* parameter in this section will also help reduce performance load.


![](cubic_filtering_specular.png)


The *[Environment Probe](../../../objects/lights/envprobe/index.md)* light source provides [ambient lighting and reflections](../../../objects/lights/envprobe/index.md#light_reflection_parameters) on an object inside the *Probe* by using a cubemap. However, the main purpose of *Environment Probe* is reflection rendering. For lighting, we recommend using *[Voxel Probe](../../../objects/lights/voxelprobe/index.md)*: just toggle the *[Indirect Diffuse](../../../objects/lights/envprobe/index.md#light_reflection_parameters)* lighting off in the *Parameters* window.


> **Notice:** At that, the *[Reflections](../../../objects/lights/voxelprobe/index.md#reflections_enabled)* should be toggled off for *Voxel Probe*.


![](voxel_probe_ambient_light.png) ![](environment_probe_reflection.png)


This approach allows improving the application performance without loss of visual quality: using both the *Environment* and *Voxel Probes* for ambient lighting and reflections rarely gives notable visual improvement.


![](probes_final_result.png)

*Voxel Probe Ambient Light + Environment Probe Reflections*


Just like with *Voxel Probes*, *[Cubic Filtering](../../../objects/lights/envprobe/index.md#cubic_filtering)* is the main performance drain when using *Environment Probes*. For better efficiency, only enable it when linear filtering isn't enough.


![](cubic_filtering_envprobe.png)


## Fake Lighting


When you need only the visualization of a light source without illumination, you can use one of the tricks described below.


### Using Billboards


*[Billboards](../../../objects/objects/billboards/index.md)* can be used to simulate small light sources observed from large distances. In such cases, only visualization of light sources matters. For example, you can use *Billboards* for takeoff runway lights. They don't produce any light, but look like real lights.


[![](light_billboards_2sm.png)](light_billboards.png)

*Billboards Used for Takeoff Runway Lights*


To create *Billboard* that replaces a real light source, perform the following:


1. Add a *Billboard* object to the scene by choosing *Create -> Billboards -> Base* in the Menu Bar and place it somewhere in the world. ![](../../../objects/objects/billboards/billboards_create.png)
2. Assign a material inherited from the *[billboards_base](../../../content/materials/library/billboards_base/index.md)* material.
3. Specify the following settings for this material:

  1. In the *[Common](../../../editor2/materials_settings/index.md#common_tab)* tab, set the blending *Preset* to Additive and toggle the *Depth Write* parameter off to avoid obstructing objects behind the *Billboard*. ![](billboards_blending.png)
  2. In the *[States](../../../editor2/materials_settings/index.md#states_tab)* tab, disable writing into the *Deferred Buffers* and enable the following states: ![](billboards_states.png)

    - *[Emission](../../../content/materials/library/billboards_base/index.md#emission)* to provide the emission effect by using the corresponding texture.
    - *[Geometry Inflation](../../../content/materials/library/billboards_base/index.md)* to limit the minimum *Billboard* screen size to a fixed value and, therefore, to provide visibility from far distances.
    - *[Soft Interaction](../../../content/materials/library/billboards_base/index.md)* to make interaction of the *Billboard* with other objects in the scene softer and avoid artifacts.
  3. In the *[Textures](../../../editor2/materials_settings/index.md#textures_tab)* tab, specify the *Diffuse* and *Emission* textures. ![](billboards_textures.png)
  4. In the *[Parameters](../../../editor2/materials_settings/index.md#parameters_tab)* window, specify the following values: ![](billboards_parameters.png)

    - Set the *[Diffuse](../../../content/materials/library/billboards_base/index.md#base_param_diffuse)* color multiplier to **black**, so that *Billboard* become fully transparent.
    - Increase the *[Emission Scale](../../../content/materials/library/billboards_base/index.md#emission_param_scale)* to make *Billboard* brighter.
    - Increase the [Geometry Parameters](../../../content/materials/library/billboards_base/index.md#param_geometry) to scale the size of *Billboard* and limit the minimum size of *Billboard*.
    - Correct the *Soft Interaction* value, if necessary.


As a result, you get the *Billboard* that can be used to simulate a small light source at far distances. You can add any required number of *Billboards* to the existing *Billboard* object: in the *Parameters* window, select the created *Billboard* in the list and click **Add**.


![](light_billboards_0.png)

*Lights Simulated by Billboards*


### Using Volumetric Objects


*[Volumetric](../../../objects/effects/volumetrics/index.md)* objects can be used to simulate visible light volumes instead of using real light sources. Such objects should be used when you don't need illumination. For example, by using *Volumetric* objects, you can create light [spheres](../../../objects/effects/volumetrics/volume_sphere.md), [beams](../../../objects/effects/volumetrics/volume_proj.md), or [volumes](../../../objects/effects/volumetrics/volume_omni.md), imitate [sun beams](../../../objects/effects/volumetrics/volume_box.md) falling into a room through openings, and so on.


![](volume_light.png)

*Light sphere and beam simulated instead of real light source*


To create such light volumes, perform the following:


1. Add the *Volume Sphere* object by choosing *Create -> Volume -> Sphere Light* in the Menu Bar and make it a child of the node that should emit the light. ![](volume_sphere_hierarchy.png)
2. In the *Volume Sphere* section of the *Parameters* window, change the size of the sphere to 0.15.
3. In the *Node* tab of the *Parameters* window, set coordinates of the volume sphere to the parent node and then slightly correct the sphere position, so that it looks realistic. ![](default_volume_sphere.png)
4. Assign a material inherited from the *[volume_light_base](../../../content/materials/library/volume_light_base/index.md)* base material and specify the required values in the *Parameters* tab. For example, you can set the [color](../../../content/materials/library/volume_light_base/index.md#parameter_diffuse) of the light sphere and [scale the density](../../../content/materials/library/volume_light_base/index.md#parameter_multiplier) of the light. ![](volume_light_base.png)
5. Add the *Volume Projected* object by choosing *Create -> Volume -> Projected* in the Menu Bar and make it a child of the node that should emit the light. ![](volume_proj_hierarchy.png)
6. In the *Node* tab of the *Parameters* window, reset the position and rotation of the *Volume Projected* to the parent node ones. ![](default_volume_proj.png)
7. In the *Volume Projected* section of the *Parameters* window, specify the required parameters of the light beam. For example, change its [size, radius, field of view, and step](../../../objects/effects/volumetrics/volume_proj.md#volume_proj_parameters). ![](volume_proj_settings.png)
8. Assign a material inherited from the *[volume_proj_base](../../../content/materials/library/volume_proj_base/index.md)* base material.
9. In the *Parameters* window of the material, set the [color](../../../content/materials/library/volume_proj_base/index.md#parameter_diffuse) of the light beam the same as for the *Volume Sphere* and decrease the [diffuse scale](../../../content/materials/library/volume_proj_base/index.md#parameter_diffuse_scale) to 0.5 to make the color less bright. ![](volume_proj_base.png)


As a result, you get a light sphere and a beam imitating the real light source.


![](light_volume.png)

*Light simulated byVolume SphereandVolume Projobjects*
