# debug_materials


A *debug_materials* material is a default [debug material](../../../../../content/materials/library/debug/index.md). By using this material, you can adjust visibility of rendering buffers, or check how the scene looks on a certain stage of image composition. For example, how it is rendered with or without reflections. The material doesn't change the image rendered in the viewport: it is rendered atop as the [debug image](#parameters_debug_image).


> **Notice:** A *debug_material* is inherited from the base *render_composite_deferred* material. It isn't available in the *Materials Editor*, however, it can be found in the `<UnigineSDK>/data/core/materials/default/render/` folder.

 Prior KnowledgeThis article assumes you have prior knowledge of the following topics. Please read them before proceeding:
- *[Setting Up Materials](../../../../../editor2/materials_settings/index.md)*
- *[Debug Materials](../../../../../content/materials/library/debug/index.md)*


## States


The states described below should be **disabled** in the following cases:

- If the debug material is used as a custom composite material that is used on the [Deferred Composite](../../../../../principles/render/sequence/index.md#deferred_composite) stage of the rendering sequence. > **Notice:** The composite material can be specified as an argument of the `render_composite_deferred_material` console command or in the *[Composite Materials](../../../../../editor2/settings/render_settings/custom_composite/index.md#composite_materials)* field of the *Settings* window. If the states will be enabled, sRGB correction and exposure will be rendered twice: first, on the Deferred Composite stage, and then, during the [corresponding passes](../../../../../principles/render/sequence/index.md#srgb_correction) of the rendering sequence.
- If the debug material renders buffers that don't require sRGB correction or exposure (for example, the [albedo colors buffer](#parameter_buffer_albedo)).


### sRGB


Toggles sRGB correction for the rendered image on and off.


![](srgb_0.jpg) ![](srgb_1.jpg)


### Auto-Exposure


Toggles automatic exposure for the rendered image on and off. When enabled, the *[Exposure](../../../../../editor2/settings/render_settings/camera_effects/index.md#exposure)* value specified via the *Settings* window is applied to the debug image.


This state isn't required when the material is used to visualize the [rendering buffers](#parameters_buffers).


For example, if the debug material renders the albedo colors buffer, there is no need to enable *Auto-Exposure*, as such material should visualize the albedo colors only, not more:

![](exposure_0.jpg) ![](exposure_1.jpg)


## Textures


### Mask Texture


**Mask** texture determines the area of the debug material rendering. The mask is one-channelled (R).


![](mask_0.jpg) ![](mask_1.jpg)


## Parameters


### Rendering Debug Image


The following parameters allow changing the *[debug image](../../../../../content/materials/library/debug/index.md#debug_image)*. For example, by adjusting these parameters, you can render several debug images with different debug materials in a single viewport.


![](debug_image.jpg)

*Several Debug Images in a Single Viewport*


#### Exposure


**Exposure** multiplier for the debug image.


#### X Offset


Multiplier for the **horizontal offset** of the debug image. Changing this value leads changing the position of the debug image relative to the viewport along the X axis.


The slider that allows changing the parameter value is limited to the range [0;1]. However, you can specify any value out of this range: both positive and negative values are allowed.


![](offset_x_0.jpg) ![](offset_x_1.jpg)


#### Y Offset


Multiplier for the **vertical offset** of the debug image. Changing this value leads changing the position of the debug image relative to the viewport along the Y axis.


The slider that allows changing the parameter value is limited to the range [0;1]. However, you can specify any value out of this range: both positive and negative values are allowed.


![](offset_y_0.jpg) ![](offset_y_1.jpg)


#### Width


Multiplier for the **width** of the debug image.


The slider that allows changing the parameter value is limited to the range [0;1]. However, you can specify any positive value out of this range.


![](width_1.jpg) ![](width_0.jpg)


#### Height


Multiplier for the **height** of the debug image.


The slider that allows changing the parameter value is limited to the range [0;1]. However, you can specify any positive value out of this range.


![](height_1.jpg) ![](height_0.jpg)


#### Intensity


**Intensity** of the debug image. This is the multiplier for the color of the debug image. The higher the value, the lighter and brighter the debug image is.


The intensity may be changed, for example, if the debug image is overexposed, or if it is too dark/bright to see all details of this image.


![](intensity_0.jpg) ![](intensity_1.jpg)


#### Transparency


**Transparency** of the debug image. When set to 1, the debug image is fully visible; at lower values, the debug image is blended with the final image rendered in the viewport or with the other debug material rendered before the current one (if several debug materials are [used](../../../../../content/materials/library/debug/index.md#several_materials)).


![](transparency_0.jpg) ![](transparency_1.jpg)


This parameter can be used, for example, to compare the debug image and the final image, or to create showreels.


### Mask UV Transform


Mask texture [coordinates transformation](../../../../../content/materials/library/mesh_base/index.md#texture_transform).


### Debug Parameters


The parameters described below allow specifying how much a certain component of the render affects the final image rendered in the viewport.

> **Notice:** The parameters don't actually change contents of the rendering buffers: the debug image displays the result as if the contents of the buffers has been changed.


#### Sky Color


**Sky color** multiplier allows changing the background color. You can also adjust the *alpha* channel of the color to specify transparency of the sky.


#### Albedo Color


**Albedo color** multiplier. Using this parameter in pair with *[Albedo Visibility](#parameter_albedo_visibility)* allows you to get the result as if the albedo colors buffer has been actually changed.


![](albedo_color_0.jpg) ![](albedo_color_1.jpg)


#### Albedo Visibility


Visibility factor for the [albedo color multiplier](#parameter_albedo_color) that specifies how much this multiplier affects the final image.


![](albedo_color_1.jpg) ![](albedo_visible_1.jpg)


#### Metalness


**Metalness** multiplier. By using this parameter, you can affect metalness of the scene: make all materials to be metals (*Metalness* = **1**) or dielectrics (*Metalness* = **0**). Using this parameter in pair with *[Metalness Visibility](#parameter_metalness_visibility)* allows you to get the result as if the metalness stored in the shading buffer has been actually changed.


For example, if *Metalness Visibility = 1*, the result will be the following:

![](metalness_visible_0.jpg) ![](metalness_visible_1.jpg)


#### Metalness Visibility


Visibility factor for the [metalness multiplier](#parameter_metalness) that specifies how much this multiplier affects the final image.


#### Baked Lightmap Visibility


Visibility factor for baked lightmaps. This value specifies how much [lightmaps](../../../../../principles/render/sequence/index.md#light_map) affect the final image.

> **Notice:** If you need to show the [baked lightmap buffer](#parameter_buffer_baked_lightmap), this value should be greater than 0.


![](lightmaps_0.jpg) ![](original.jpg)


#### Baked AO Visibility


Visibility factor for baked ambient occlusion stored in the [albedo colors buffer](../../../../../principles/render/sequence/index.md#albedo).

> **Notice:** If you need to show the [baked ambient occlusion buffer](#parameter_buffer_baked_ao), this value should be greater than 0.


![](ao_0.jpg) ![](original.jpg)


#### SSAO Visibility


Visibility factor for the SSAO effect.

> **Notice:** If you need to show the [SSAO buffer](#parameter_buffer_ssao), this value should be greater than 0.


![](ssao_0.jpg) ![](original.jpg)


#### SSR Visibility


Visibility factor for the SSR effect.

> **Notice:** If you need to show the [SSR buffer](#parameter_buffer_ssr), this value should be greater than 0.


![](ssr_0.jpg) ![](original.jpg)


#### SSGI Visibility


Visibility factor for the SSGI effect.

> **Notice:** If you need to show the [SSGI buffer](#parameter_buffer_ssgi), this value should be greater than 0.


![](ssgi_0.jpg) ![](original.jpg)


#### Haze Visibility


Visibility factor for the atmosphere haze.


![](haze_0.jpg) ![](original.jpg)


#### Environment Ambient Visibility


Visibility factor for the environment probe ambient lighting.


![](env_ambient_0.jpg) ![](original.jpg)


This parameter can be used to create a debug material that renders ambient lighting in the scene (check the preconfigured *debug_ambient_light* material as an example).


#### Environment Reflection Visibility


Visibility factor for the environment probe reflections.


![](env_reflection_0.jpg) ![](original.jpg)


This parameter can be used to create a debug material that renders reflections in the scene (check the preconfigured *debug_reflections* material as an example), or that renders the environment probes cubemaps (the preconfigured *debug_cubemaps* material).


#### Diffuse Lighting Visibility


Visibility factor for diffuse lighting.


![](diffuse_light_0.jpg) ![](original.jpg)


This parameter can be used to create a debug material that renders diffuse lighting in the scene (check the preconfigured *debug_diffuse_light* material as an example).


#### Specular Lighting Visibility


Visibility factor for specular lighting.


![](specular_light_0.jpg) ![](original.jpg)


This parameter can be used to create a debug material that shows how highlights in the scene are rendered (check the preconfigured *debug_highlights* material as an example).


### Rendering Buffers Parameters


The *Buffers* group of the *debug_material* includes visibility parameters for all rendering buffers that are filled during image generation. These parameters allow specifying visibility of a rendering buffer on the current debug image.


![](debug_materials_buffers.png)

*Rendering Buffers Parameters*


By default, all rendering buffers are invisible. By using these parameters, you can check how a certain buffer is rendered, or blend several buffers on the single debug image.

> **Notice:** All buffers are blended by using alpha blending.


#### Albedo Visibility


Visibility factor for the albedo colors buffer. By using this parameter, you can blend the albedo colors buffer with the current debug image. When set to 1, the buffer is fully visible.

> **Notice:** If the [Albedo Visibility](#parameter_albedo_visibility) parameter is greater than 0, the ["changed"](#parameter_albedo_color) albedo colors buffer will be rendered.


![](albedo_buffer_0.jpg) ![](albedo_buffer.jpg)


#### Roughness Visibility


Visibility factor for the roughness buffer. By using this parameter, you can blend the roughness buffer with the current debug image. When set to 1, the buffer is fully visible.


![](roughness_buffer_0.jpg) ![](roughness_buffer.jpg)


Check the preconfigured *debug_roughness* material as an example.


#### Metalness Visibility


Visibility factor for the metalness buffer. By using this parameter, you can blend the metalness buffer with the current debug image. When set to 1, the buffer is fully visible.

> **Notice:** If the [Metalness Visibility](#parameter_baked_lightmap_visibility) parameter is greater than 0, the ["changed"](#parameter_metalness) metalness buffer will be rendered.


![](metalness_buffer_0.jpg) ![](metalness_buffer.jpg)


Check the preconfigured *debug_metalness* material as an example.


#### Specular Visibility


Visibility factor for the specular buffer. By using this parameter, you can blend the specular buffer with the current debug image. When set to 1, the buffer is fully visible.


![](specular_buffer_0.jpg) ![](specular_buffer_1.jpg)


#### Translucency Visibility


Visibility factor for the translucency buffer. By using this parameter, you can blend the translucency buffer with the current debug image. When set to 1, the buffer is fully visible.


![](translucency_buffer_0.jpg) ![](translucency_buffer_1.jpg)


#### Microfiber Visibility


Visibility factor for the microfiber buffer. By using this parameter, you can blend the microfiber buffer with the current debug image. When set to 1, the buffer is fully visible.


![](microfiber_buffer_0.jpg) ![](microfiber_buffer_1.jpg)


#### Normal Visibility


Visibility factor for the normal buffer. By using this parameter, you can blend the normal buffer with the current debug image. When set to 1, the buffer is fully visible.


![](normals_buffer_0.jpg) ![](normals_buffer.jpg)


Check the preconfigured *debug_normals* material as an example.


#### Auxiliary Visibility


Visibility factor for the auxiliary buffer. By using this parameter, you can blend the auxiliary buffer with the current debug image. When set to 1, the buffer is fully visible.


![](auxiliary_buffer_0.jpg) ![](auxiliary_buffer.jpg)


Check the preconfigured *debug_auxiliary* material as an example.


#### Curvature Visibility


Visibility factor for the curvature buffer. By using this parameter, you can blend the curvature buffer with the current debug image. When set to 1, the buffer is fully visible.


![](curvature_buffer_0.jpg) ![](curvature_buffer.jpg)


Check the preconfigured *debug_curvature* material as an example.


#### DoF Mask Visibility


Visibility factor for the DoF mask buffer. By using this parameter, you can blend the DoF mask buffer with the current debug image. When set to 1, the buffer is fully visible.


![](dofmask_buffer_0.jpg) ![](dofmask_buffer.jpg)


Check the preconfigured *debug_dof_mask* material as an example.


#### Velocity Visibility


Visibility factor for the velocity buffer. By using this parameter, you can blend the velocity buffer with the current debug image. When set to 1, the buffer is fully visible.


![](velocity_buffer.gif)


Check the preconfigured *debug_velocity* material as an example.


#### Water Normal Visibility


Visibility factor for the water normal buffer. Enable the ***Is Water*** option on the *States* tab for this parameter to work properly. When set to 1, the buffer is fully visible.


![](water_normal.gif)


Check the preconfigured *debug_water_normal* material as an example.


#### Screen Color Visibility


Visibility factor for the screen color buffer. By using this parameter, you can blend the screen color buffer with the current debug image. When set to 1, the buffer is fully visible.


![](screen_color_buffer_0.jpg) ![](screen_color_buffer.jpg)


#### Bent Normal Visibility


Visibility factor for the bent normal buffer. By using this parameter, you can blend the bent normal buffer with the current debug image. When set to 1, the buffer is fully visible.


Check the preconfigured *debug_bent_normals* material as an example.


![](bent_normal_buffer_0.jpg) ![](bent_normal_buffer_1.jpg)


#### Depth Visibility


Visibility factor for the depth buffer. By using this parameter, you can blend the depth buffer with the current debug image. When set to 1, the buffer is fully visible.


![](depth_buffer_0.jpg) ![](depth_buffer_1.jpg)


#### Opacity Depth Visibility


Visibility factor for the opacity depth buffer. By using this parameter, you can blend the opacity depth buffer with the current debug image. When set to 1, the buffer is fully visible.


![](opacity_depth_buffer_0.jpg) ![](opacity_depth_buffer.jpg)


Check the preconfigured *debug_opacity_depth* material as an example.


#### Bevel Visibility


Visibility factor for the bevel buffer. By using this parameter, you can blend the bevel buffer with the current debug image. When set to 1, the buffer is fully visible.


![](bevel_buffer_0.jpg) ![](bevel_buffer.jpg)


Check the preconfigured *debug_bevel* material as an example.


#### Baked Lightmap Visibility


Visibility factor for the baked lightmap buffer. By using this parameter, you can blend the baked lightmap buffer with the current debug image. When set to 1, the buffer is fully visible.

> **Notice:** The [Baked Lightmap Visibility](#parameter_baked_lightmap_visibility) parameter must be greater than 0; otherwise, the buffer won't be visible.


![](lightmap_buffer_0.jpg) ![](lightmap_buffer_1.jpg)


#### Baked AO Visibility


Visibility factor for the baked ambient occlusion buffer. By using this parameter, you can blend the baked ambient occlusion buffer with the current debug image. When set to 1, the buffer is fully visible.

> **Notice:** The [Baked AO Visibility](#parameter_baked_ao_visibility) parameter must be greater than 0; otherwise, the buffer won't be visible.


![](ao_buffer_0.jpg) ![](ao_buffer_1.jpg)


#### SSAO Visibility


Visibility factor for the screen space ambient occlusion buffer. By using this parameter, you can blend the SSAO buffer with the current debug image. When set to 1, the buffer is fully visible.

> **Notice:** The [SSAO Visibility](#parameter_ssao_visibility) parameter must be greater than 0; otherwise, the buffer won't be visible.


Check the preconfigured *debug_ssao* material as an example.


![](ssao_buffer_0.jpg) ![](ssao_buffer_1.jpg)


#### SSR Visibility


Visibility factor for the screen space reflections buffer. By using this parameter, you can blend the SSR buffer with the current debug image. When set to 1, the buffer is fully visible.

> **Notice:** The [SSR Visibility](#parameter_ssr_visibility) parameter must be greater than 0; otherwise, the buffer won't be visible.


Check the preconfigured *debug_ssr* material as an example.


![](ssr_buffer_0.jpg) ![](ssr_buffer_1.jpg)


#### SSGI Visibility


Visibility factor for the screen space global illumination buffer. By using this parameter, you can blend the SSGI buffer with the current debug image. When set to 1, the buffer is fully visible.

> **Notice:** The [SSGI Visibility](#parameter_ssgi_visibility) parameter must be greater than 0; otherwise, the buffer won't be visible.


Check the preconfigured *debug_ssgi* material as an example.


![](ssgi_buffer_0.jpg) ![](ssgi_buffer_1.jpg)
