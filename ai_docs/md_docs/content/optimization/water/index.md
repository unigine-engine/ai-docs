# Water Optimization


A *[Global Water](../../../objects/objects/water/water_object.md)* is another object that significantly affects the performance. Despite it is optimized so that the GPU is not overloaded, it still may require some additional optimizations.


> **Notice:** It is recommended to use only **1** global water object (*ObjectWaterGlobal*) in the scene, as it uses the *screen space projected grid* for the water surface.


When you create waves in [Layers](../../../objects/objects/water/water_object.md#layers_mode) or [Manual](../../../objects/objects/water/water_object.md#manual_mode) mode, the general rule is to keep the total number of waves as low as possible. It is recommended to use less than 100 waves as their number significantly affects performance.


## Setting Up Water Tessellation


Polygons of the *Global Water* surface are adaptively tessellated on the fly and displaced based on the Heightmap component of the Virtual Texture. The polygon mesh is split up to multiple levels of detail of various density depending on the distance from the camera. The [**Geometry**](../../../editor2/settings/render_settings/water_ssr/index.md#geometry_settings) settings provide much room for rendering optimization. They can be found in the *[Water](../../../editor2/settings/render_settings/water_ssr/index.md)* section of the *[Settings](../../../editor2/settings/index.md)* window.


![](water_geometry.png)


Pay attention to the following parameters:


- With lower values of [**Geometry Progression**](../../../editor2/settings/render_settings/water_ssr/index.md#geometry_progression) less polygons are generated at a distance. ![](tessellation_exponent_0.png) ![](tessellation_exponent_1.png)
- By configuring the [**Geometry Polygon Size**](../../../editor2/settings/render_settings/water_ssr/index.md#geometry_polygon_size) parameter you can define the minimum spatial size of polygons in case of excessive detail level. ![](tessellation_factor_0.png) ![](tessellation_factor_1.png)
- [**Geometry Subpixel Reduction**](../../../editor2/settings/render_settings/water_ssr/index.md#geometry_subpixel_reduction) parameter determines the minimum ratio of polygon size (in the screen space) to the area seen in the viewport. This parameter enables you to quickly decrease the number of polygons or simply remove too small polygons that are barely visible, in order to increase performance.
- Set a lower [**Visibility Distance**](../../../editor2/settings/render_settings/water_ssr/index.md#visibility_distance) to discard rendering of too remote polygons.


## Optimizing Rendering Settings


There is also a set of water rendering settings that may also reduce the performance. They can be found in the *[Water](../../../editor2/settings/render_settings/water_ssr/index.md)* section of the *[Settings](../../../editor2/settings/index.md)* window.


![](common1.png)


### Screen Space Reflections


For the water object, the [screen space reflections](../../../editor2/settings/render_settings/water_ssr/index.md#water_ssr_enabled) can be rendered instead of the [planar reflections](../../../objects/objects/water/water_object.md#planar_reflection) at large distances. It improves the performance, as such reflections don't depend on complexity of the reflected geometry.


You can enable the SSR effect for the water object in one of the following ways:


- In the Menu Bar, choose *Rendering -> Water -> SSR*.
- In the Menu Bar, choose *Windows -> Settings* and then go to the *[Water](../../../editor2/settings/render_settings/water_ssr/index.md)* section. Here you can toggle the *SSR Enabled* parameter on.


![](ssr_on.png) ![](ssr_off.png)


In the *Settings* window, you can also specify the additional settings for SSR: set the [quality](../../../editor2/settings/render_settings/water_ssr/index.md#water_ssr_quality) of reflections and enable/disable [increased accuracy](../../../editor2/settings/render_settings/water_ssr/index.md#water_ssr_increased_accuracy).


However, remember that these settings affect the performance as follows:


- The *higher* the quality of the reflections, the *lower* the performance is.
- *Enabling* the increased accuracy *reduces* the performance. However, some visual artifacts are reduced as well.


### Anisotropy Quality


The **Anisotropy Quality** parameter specifies the anisotropy level (degree of anisotropic filtering) of the water textures. Increasing the quality provides better texture detail over a distance, however, it has a great impact on the performance. So, find the most appropriate value to keep the balance of the visual quality and the performance.


![](anisotropy_quality_0.png) ![](anisotropy_quality_1.png)


### Refraction Quality


The **Refraction Quality** parameter specifies the quality of water refraction: the *higher* the quality, the *lower* the performance is.


![](refraction_quality_0.png) ![](refraction_quality_1.png)


### Shoreline Wetness


The wetness effect enabled for objects near the shoreline may also affect the performance. Try to disable it, if possible, to improve the performance of water rendering.


![](shoreline_wetness_0.jpg) ![](shoreline_wetness_1.jpg)


### Underwater Shafts


Rendering of the underwater shafts can be disabled if the camera never gets under the water.


![](underwater_shafts_0.jpg) ![](underwater_shafts_1.jpg)


### Rendering Lights on Water


You can disable rendering of all the light sources of the certain type on the water surface to increase the performance.


> **Notice:** To enable/disable rendering of a particular light source on the water, select it in the World Hierarchy, go to the *type-specific* tab of the *Parameters* window and check/uncheck the *Render Water* parameter.


- **Render Environment Probes** toggles on/off rendering of all environment probes on the water surface. ![](render_env_probes_0.png) ![](render_env_probes_1.png)
- **Render Voxel Probes** toggles on/off rendering of all voxel probes on the water surface. ![](render_voxel_probes_0.png) ![](render_voxel_probes_1.png)
- **Render Lights** toggles on/off rendering of all omni and projected light sources on the water surface. ![](render_lights_1.png) ![](render_lights_0.png)


### Field Objects


If interaction of water with FieldHeight and/or FieldShoreline objects is enabled in the [Global Water parameters](../../../objects/objects/water/water_object.md#fields_interaction), you can affect the performance by setting up the **resolution** of the *[Field Height](../../../objects/effects/fields/field_height/index.md)* and *[Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md)* textures in the *Settings* window: the *higher* the resolution, the *lower* the performance is.


![](field_height_0.png) ![](field_height_1.png)


![](field_shoreline_0.png) ![](field_shoreline_1.png)


Another fields-related setting is **Field Precision 32 bits**. It allows reducing the precision of textures used for field objects, therefore, increasing the performance.


#### Setting Up Shoreline Rendering


The shoreline areas created with the *[Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md)* object may reduce the water performance if set up improperly. *[Global Water](../../../objects/objects/water/water_object.md)* provides several shoreline-related parameters that can help to gain the performance.


The **[Normal](../../../objects/objects/water/water_object.md#fieldshoreline_normal)** and **[Geometry](../../../objects/objects/water/water_object.md#fieldshoreline_geometry)** options affect rendering of wave geometry of shoreline waves. Disable them, when the waves are hardly noticeable (e.g., if the shoreline is observed from above only). In some cases, using only the *Geometry* option is enough to simulate distortion of the water surface.


![](geometry_disabled.png) ![](geometry_enabled.png)


If both options are disabled, disable also the **[High Precision](../../../objects/objects/water/water_object.md#high_precision)** option that allows improving interpolation between the adjacent pixels of the shoreline texture. This option reduces stepping artifacts that are noticeable at the waterline separating overwater and underwater. However, if rendering of the wave geometry is disabled for the shoreline waves, there is no need in such additional calculations.


As it was noticed above, rendering of the waves geometry is usually disabled when the water surface is observed from above. Therefore, you can disable the **[Caustics Distortion](../../../objects/objects/water/water_object.md#caustics_distortion)** option that smooths caustics. It will gain the performance without visual losses.


> **Notice:** You can disable the caustic distortion in any other case, if necessary.


Another option that also affects the performance is **[Foam](../../../objects/objects/water/water_object.md#fieldshoreline_foam)**. It enables foam rendering for shoreline zones. If the foam simulation isn't necessary, disable the option to increase the performance.


Thus, you can simulate shoreline areas, viewed from a plane, by just enabling the foam effect while disabling geometry, caustics and improved interpolation as they are hardly noticeable with a significant increase of performance.


![](shoreline_no_optimization.png) ![](shoreline_optimized.png)


As you can see, there is almost no visual difference between shorelines on the pictures above.


## Setting Up Water Parameters


The *[Global Water](../../../objects/objects/water/water_object.md)* provides several parameters that can also affect the water performance:


- **[Steepness Scale](../../../objects/objects/water/water_object.md#steepness_scale)** affects the sharpness of the wave crests. The waves look more realistic, however, you can disable this effect if the water is observed from the large distance.
- **[Underwater DOF](../../../objects/objects/water/water_object.md#underwater_dof)** provides the DOF effect for underwater and overwater splice. It can also be disabled, if the camera never gets under the water.
- **[Caustics](../../../objects/objects/water/water_object.md#caustics)** enables rendering of light rays refracted by the water surface. It can be disabled, if the effect isn't required.
- **[Caustics Distortion](../../../objects/objects/water/water_object.md#caustics_distortion)** smooths caustics. It is available only when the **Caustics** is enabled for the water. If smoothing isn't required, the option can be disabled to gain the performance.


## Optimizing Planar Reflections


The *Global Water* object allows you to use [planar reflections](../../../objects/objects/water/water_object.md#planar_reflection) on the water surface.


> **Notice:** It is recommended to use planar reflections on undisturbed water (0-2 Beaufort).


However, planar reflections of a high resolution may significantly reduce the performance. So, you can try to lower the size of the planar reflection map: in the *[Planar Reflection](../../../objects/objects/water/water_object.md#planar_reflection)* section of the *Parameters*, specify the appropriate value for the **[Map Size](../../../objects/objects/water/water_object.md#map_size)**.


![](map_size.png)


However, remember that reflections of a low resolution rarely provide the expected visual result.


![](map_size_0.png) ![](map_size_1.png)


You can also use [reflection mask](../../../objects/objects/water/water_object.md#viewport_mask) to control rendering of the planar reflections into the camera viewport. For example, you can [render only certain planar reflections](../../../content/optimization/reflections/index.md#reflection_mask), and the other ones replace with [screen space reflections](#water_ssr).


## Culling Optimization


The polygons of the Global Water surface are subject to frustum culling optimization. If a polygon falls out of the camera frustum (i.e. its screen position is outside the viewport bounds), it is culled out for rendering. In the *[Water](../../../editor2/settings/render_settings/water_ssr/index.md)* section of the *[Settings](../../../editor2/settings/index.md)* window you can enable the **Aggressive Frustum Culling** mode that implies more strict requirements for polygons to be rendered and, therefore, higher performance.


![](culling.png)


Tweak the [**Culling**](../../../editor2/settings/render_settings/water_ssr/index.md#culling_settings) settings for more optimizations:


- Decrease the [**Culling Frustum Padding**](../../../editor2/settings/render_settings/water_ssr/index.md#culling_frustum_padding) to lower the size of the viewing frustum.
- Increase the [**Culling Oblique Frustum**](../../../editor2/settings/render_settings/water_ssr/index.md#culling_oblique_frustum) multiplier to cull out more polygons beyond the oblique frustum plane.
