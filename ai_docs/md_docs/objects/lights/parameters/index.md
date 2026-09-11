# Light Sources Parameters


This article contains parameters common for the **[Omni](../../../objects/lights/omni/index.md), [Projected](../../../objects/lights/proj/index.md)**, and **[World](../../../objects/lights/world/index.md)** light sources, **[Environment Probe](../../../objects/lights/envprobe/index.md)**, and **[Voxel Probe](../../../objects/lights/voxelprobe/index.md)**. Each light source also has unique parameters, which are described in the corresponding articles. Note that not all the parameters described in this article are available for each type of the light source.


## Light Settings


[![](light_settings.png)](light_settings.png)


### Common Settings


| Mode | Mode that defines rendering of the light source. It also affects [rendering of shadows](../../../editor2/lighting/lights/shadows.md) from the light source, and defines the impact of the light source on the [light baking](../../../editor2/lighting/gi/index.md#light_baking) process. - **Dynamic** � the light source provides direct real-time lighting only. It is turned off while light baking is being calculated. Only dynamic shadows are rendered. - **Static** � the light source contributes to light baking and remains enabled all the time providing the direct real-time lighting. Shadow types rendered in this case are defined by *[Shadow Mode](#shadow_mode)* (or *[Shadow Cascade Mode](../../../objects/lights/world/index.md#shadow_cascade_mode)* for *World Light*). |  |  |  |  |
|---|---|---|---|---|---|
| Shadow Mask | The [shadow mask](../../../principles/bit_masking/index.md#shadow_mask) controls rendering of a shadow cast by an object lit by the light source. |  |  |  |  |
| Viewport Mask | For the light to be rendered, its viewport mask should match the camera's [viewport mask](../../../principles/bit_masking/index.md#viewport). |  |  |  |  |
| Color Mode | Color calculation mode for the light source. The following mode are available: - **Classic** mode. The light source color is defined by the [Color](#color) value. - **Temperature** mode. The light source color is defined by the [color temperature](#temperature) and [color filter](#color_filter) values. |  |  |  |  |
| Color | Color of the light in the RGBA format. By default, the light is **white**. \| ![](omni_color_0.png) \| ![](omni_color_1.png) \| \|---\|---\| \| ![](omni_color_white.png) \| ![](omni_color_yellow.png) \| | ![](omni_color_0.png) | ![](omni_color_1.png) | ![](omni_color_white.png) | ![](omni_color_yellow.png) |
| ![](omni_color_0.png) | ![](omni_color_1.png) |  |  |  |  |
| ![](omni_color_white.png) | ![](omni_color_yellow.png) |  |  |  |  |
| Color Filter | Color multiplier for the light source color (calculated using the color temperature value). This can be used to imitate colored glass. The parameter is available only when the *Temperature* [color mode](#color_mode) is set. |  |  |  |  |
| Temperature | Light source temperature used for light color calculation. The maximum value is 40000. \| ![](temperature_0.jpg) \| ![](temperature_1.jpg) \| \|---\|---\| \| *Temperature = 1000* \| *Temperature = 40000* \| | ![](temperature_0.jpg) | ![](temperature_1.jpg) | *Temperature = 1000* | *Temperature = 40000* |
| ![](temperature_0.jpg) | ![](temperature_1.jpg) |  |  |  |  |
| *Temperature = 1000* | *Temperature = 40000* |  |  |  |  |
| Intensity | Multiplier for the light color used to control color intensity. The *higher* the value, the brighter the light is. - The minimum value of 1 corresponds to the least saturated light color. - The maximum value of 100 equals the most bright and intense color. \| ![](omni_color_0.png) \| ![](omni_multiplier_1.png) \| \|---\|---\| \| *Intensity = 7* \| *Intensity = 12* \| | ![](omni_color_0.png) | ![](omni_multiplier_1.png) | *Intensity = 7* | *Intensity = 12* |
| ![](omni_color_0.png) | ![](omni_multiplier_1.png) |  |  |  |  |
| *Intensity = 7* | *Intensity = 12* |  |  |  |  |
| Lux | Intensity of the light color (as perceived by the human eye) in lux. In UNIGINE, all light sources have the [intensity](#intensity) of 1 by default, which is equal to 100000 lux. |  |  |  |  |


### Attenuation Settings


| Power | Light attenuation power used to simulate light intensity gradual fading. This parameter determines how fast the intensity decreases up to the attenuation distance set for the light source. - If the attenuation power is set to 0 or close to it, the edge between illuminated and non-illuminated areas will be sharp. - *Increasing* the value up to the maximum of 1 will render softly dispersed light at the non-illuminated areas border. \| ![](omni_attenuation_0.png) *LightOmni power = 0.001* \| ![](omni_attenuation_1.png) *LightOmni power = 0.5* \| ![](omni_attenuation_2.png) *LightOmni power = 1* \| \|---\|---\|---\| \| ![](proj_attenuation_0.png) *LightProj power = 0.001* \| ![](proj_attenuation_1.png) *LightProj power = 0.5* \| ![](proj_attenuation_2.png) *LightProj power = 1* \| \|---\|---\|---\| | ![](omni_attenuation_0.png) *LightOmni power = 0.001* | ![](omni_attenuation_1.png) *LightOmni power = 0.5* | ![](omni_attenuation_2.png) *LightOmni power = 1* | ![](proj_attenuation_0.png) *LightProj power = 0.001* | ![](proj_attenuation_1.png) *LightProj power = 0.5* | ![](proj_attenuation_2.png) *LightProj power = 1* |
|---|---|---|---|---|---|---|---|
| ![](omni_attenuation_0.png) *LightOmni power = 0.001* | ![](omni_attenuation_1.png) *LightOmni power = 0.5* | ![](omni_attenuation_2.png) *LightOmni power = 1* |  |  |  |  |  |
| ![](proj_attenuation_0.png) *LightProj power = 0.001* | ![](proj_attenuation_1.png) *LightProj power = 0.5* | ![](proj_attenuation_2.png) *LightProj power = 1* |  |  |  |  |  |
| Distance | Distance from the light source [shape](#shape), after which the light source doesn't illuminate anything. In other words, this parameter determines the outer border of the area illuminated by the light source. \| ![](omni_distance_0.png) \| ![](omni_distance_1.png) \| \|---\|---\| \| *Distance = 1* \| *Distance = 1.5* \| | ![](omni_distance_0.png) | ![](omni_distance_1.png) | *Distance = 1* | *Distance = 1.5* |  |  |
| ![](omni_distance_0.png) | ![](omni_distance_1.png) |  |  |  |  |  |  |
| *Distance = 1* | *Distance = 1.5* |  |  |  |  |  |  |
| Near Attenuation | Distance from the light source within which the light intensity is equal to 0. If an object is located within this distance from the light source, it won't be illuminated. In other words, this parameter determines the inner border of the area illuminated by the light source. |  |  |  |  |  |  |
| Near Attenuation Gradient | The length of the gradient that makes the *[Near Attenuation](#near_attenuation)* border smoother. |  |  |  |  |  |  |


### Shape Settings


| Type | Shape of the light source. The following shapes are available: \| ![](omni_shape_0.png) \| ![](omni_shape_1.png) \| \|---\|---\| \| *Point shape* \| *Sphere shape* \| \| ![](omni_shape_2.png) \| ![](omni_shape_3.png) \| \| *Capsule shape* \| *Rectangle shape* \| By using this parameter, you can create an *area light* that illuminates objects in different directions at once. Besides, a light source of each shape provides a physically correct speck on illuminated surfaces. > **Notice:** A light source of the rectangular shape produces the light and the speck in a form of a rounded rectangle. | ![](omni_shape_0.png) | ![](omni_shape_1.png) | *Point shape* | *Sphere shape* | ![](omni_shape_2.png) | ![](omni_shape_3.png) | *Capsule shape* | *Rectangle shape* |
|---|---|---|---|---|---|---|---|---|---|
| ![](omni_shape_0.png) | ![](omni_shape_1.png) |  |  |  |  |  |  |  |  |
| *Point shape* | *Sphere shape* |  |  |  |  |  |  |  |  |
| ![](omni_shape_2.png) | ![](omni_shape_3.png) |  |  |  |  |  |  |  |  |
| *Capsule shape* | *Rectangle shape* |  |  |  |  |  |  |  |  |
| Radius | Radius of the spherical, capsule-shaped or rectangular light source. |  |  |  |  |  |  |  |  |
| Length | Length of the capsule-shaped or rectangular light source. |  |  |  |  |  |  |  |  |
| Height | Height of the rectangular light source. |  |  |  |  |  |  |  |  |


### Distance Visibility Settings


| Light | Distance at which the light source starts fading. If the distance is set to inf, the source is always rendered. |
|---|---|
| Light Fade | Distance at which the light gradually disappears. This parameter enables to render the light with decreasing radiance after the **[Light](#visibility_light)** distance is past. |
| Shadow | Distance up to which the cast shadows completely fade out. |
| Shadow Fade | Distance at which the shadow gradually disappears. This parameter enables to render the shadows with decreasing transparency after the **[Shadow](#visibility_light)** distance is past. |


### Rendering Settings


| Render On Water | Indicates whether to render the light source on the water surface. |
|---|---|
| Render On Transparent | Indicates whether to render the light source on the transparent surfaces. |
| Rendering Transparent Order | Sets the priority of the light source when affecting transparent objects. A higher value means a higher priority. The total number of light sources affecting a transparent object is set by the [Forward Per-Object Limits](../../../editor2/settings/render_settings/lights/index.md#forward_limits). If the number of light sources with equal priority exceeds the limit, the affecting lights are selected randomly. This option is useful for cases when a transparent object (for example, raindrops) may be illuminated by numerous lights, and a specific light source (like headlights of the car) should be for all means taken into account. > **Notice:** This setting is not available for *World Light*. |


## Shadow Settings


![](shadow_settings.png)


| Enabled | Toggles rendering of shadows from the light source on and off. ![](omni_shadows.png) *Shadows fromLight Omnienabled (the left cube) and disabled (the right cube)* |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| Mode | Is available when the *[Static](#light_mode)* light mode is enabled. Two shadow modes are available: - **Mixed**. Shadows from surfaces with both static and dynamic [shadow mode](../../../editor2/node_parameters/visual_representation/index.md#shadow_mode) are rendered as follows: the dynamic shadow map is merged with the static [depth texture](#depth_texture) and the result is rendered. - **Static**. Only shadows from surfaces with the static [shadow mode](../../../editor2/node_parameters/visual_representation/index.md#shadow_mode) enabled are rendered. These shadows are stored in the [depth texture](#depth_texture). For fine-tuning static light and shadows, see the [optimization recommendations](../../../content/optimization/lights/index.md#static_light). |  |  |  |  |  |  |  |  |
| Depth Texture | The R32F texture that stores the shadow map: a 2D texture array for the *World* and *Omni* light sources, or a 2D texture for the *Projected* light source. |  |  |  |  |  |  |  |  |
| Resolution | Size of the shadow map that defines the shadow quality. - The *higher* the resolution, the smoother and true to life the result is. - The *lower* the resolution, the more blocky and jagged the shadow outline appears. \| ![](omni_resolution_0.png) \| ![](omni_resolution_1.png) \| \|---\|---\| \| *Shadow resolution = 64* \| *Shadow resolution = 512* \| > **Notice:** A shadow map is a 32-bit texture (in case of *Light Omni*, it's a 2D texture array ), and higher resolution significantly increases memory consumption. Moreover, heavy 4K shadow maps for lights with *[Mixed](#shadow_mode)* shadow mode enabled may significantly affect performance due to blending of baked and dynamicshadow maps. | ![](omni_resolution_0.png) | ![](omni_resolution_1.png) | *Shadow resolution = 64* | *Shadow resolution = 512* |  |  |  |  |
| ![](omni_resolution_0.png) | ![](omni_resolution_1.png) |  |  |  |  |  |  |  |  |
| *Shadow resolution = 64* | *Shadow resolution = 512* |  |  |  |  |  |  |  |  |
| Bias | Shadow bias that is used to correct inexact shadowing of the scene objects. It controls the depth offset added to the current depth value stored in the shadow map. Such offset is adaptively calculated taking into account the slope angle of the light source, its resolution, and the distance to the light source at shadow map application. - If the shadow acne appears, the bias value should be *increased*. This procedure eliminates the self-shadowing effect, as the points will appear closer to light source when compared to the map depth value. - If the bias value is set *too high*, the shadow will look detached from the object casting it (see the 3rd picture below). \| [![](proj_bias_0_sm.png)](proj_bias_0.png) *Bias = 0; Normal bias = 1* \| [![](proj_bias_1_sm.png)](proj_bias_1.png) *Bias = 4; Normal bias = 1* \| [![](proj_bias_2_sm.png)](proj_bias_2.png) *Bias = 30; Normal bias = 1* \| \|---\|---\|---\| | [![](proj_bias_0_sm.png)](proj_bias_0.png) *Bias = 0; Normal bias = 1* | [![](proj_bias_1_sm.png)](proj_bias_1.png) *Bias = 4; Normal bias = 1* | [![](proj_bias_2_sm.png)](proj_bias_2.png) *Bias = 30; Normal bias = 1* |  |  |  |  |  |
| [![](proj_bias_0_sm.png)](proj_bias_0.png) *Bias = 0; Normal bias = 1* | [![](proj_bias_1_sm.png)](proj_bias_1.png) *Bias = 4; Normal bias = 1* | [![](proj_bias_2_sm.png)](proj_bias_2.png) *Bias = 30; Normal bias = 1* |  |  |  |  |  |  |  |
| Normal bias | Shadow bias that is achieved by shifting the surface on which the shadow falls. The surface is shifted along normals stored in the normal map. \| ![](proj_normal_bias_0.png) \| ![](proj_normal_bias_1.png) \| \|---\|---\| \| *Normal bias = 0; Bias = 1* \| *Normal bias = 2; Bias = 1* \| Depending on the normal map of the surface, the shadow may differ for the same values of **Normal Bias**. \| ![](proj_normal_3.png) \| ![](proj_normal_1.png) \| \|---\|---\| \| *Normal bias = 2* \| *Normal bias = 2* \| | ![](proj_normal_bias_0.png) | ![](proj_normal_bias_1.png) | *Normal bias = 0; Bias = 1* | *Normal bias = 2; Bias = 1* | ![](proj_normal_3.png) | ![](proj_normal_1.png) | *Normal bias = 2* | *Normal bias = 2* |
| ![](proj_normal_bias_0.png) | ![](proj_normal_bias_1.png) |  |  |  |  |  |  |  |  |
| *Normal bias = 0; Bias = 1* | *Normal bias = 2; Bias = 1* |  |  |  |  |  |  |  |  |
| ![](proj_normal_3.png) | ![](proj_normal_1.png) |  |  |  |  |  |  |  |  |
| *Normal bias = 2* | *Normal bias = 2* |  |  |  |  |  |  |  |  |
| Near Clipping | The distance from the light source, within which the object doesn't cast shadow under this light source. |  |  |  |  |  |  |  |  |
| Filter Mode | Filtering mode to be used to reduce the stair-step effect for soft shadows making the edges smoother. - **Global** � [filtering mode selected globally](../../../editor2/settings/render_settings/shadows/index.md#filter_mode) in the *Settings* window is to be used for shadows. - **Disabled** � filtering for shadows is disabled, the stair-step effect is clearly seen at the edges of shadows. - **Low, Medium, High, Ultra** � filtering quality modes from the lightest to the heaviest one, which best reduces the stair-step effect but has a more significant impact on performance. ![](shadow_filter_off.jpg) ![](shadow_filter_on.jpg) |  |  |  |  |  |  |  |  |
| Filter | Filtering intensity for the selected mode. The *higher* the value the less noticeable the stair-step effect at the edges of shadows will be. |  |  |  |  |  |  |  |  |
| Penumbra Mode | Quality mode to be used for penumbra rendering. This mode enables simulation of real-world shadows by keeping sharp contact shadows closer to the base and softening the farther the shadow stretches away. - **Global** � [quality mode selected globally](../../../editor2/settings/render_settings/shadows/index.md#penumbra_mode) in the *Settings* window is to be used for penumbra rendering. - **Disabled** � penumbra rendering is disabled, shadow edges are crisp and sharp (no soft shadows at all). - **Low, Medium, High, Ultra** � quality modes from the lowest to the best one, which has a more significant impact on performance. ![](shadow_filter_on.jpg) ![](shadow_penumbra_on.jpg) |  |  |  |  |  |  |  |  |
| Penumbra | Intensity of penumbra for the selected mode: - *Low* values correspond to sharper shadow edges. - Higher values increase penumbra size. ![](shadow_penumbra_02.jpg) ![](shadow_penumbra_on.jpg) |  |  |  |  |  |  |  |  |


## Screen Space Shadow Settings


![](ss_shadow_settings.png)


> **Notice:** Enable the *[Screen Space Shadows](../../../editor2/settings/render_settings/shadows/index.md#screen_space_shadows)* feature in the *Shadows Settings*.


| Enabled | Enables or disables screen space shadows from the light source. ![](ss_shadow_enabled.png) *Screen Space Shadows fromLight Omnion (the left cube) and off (the right cube). Shadows are disabled.* |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| Number of Rays | Number of rays used in screen space ray tracing. The higher the number of rays, the more accurate the computation of pixel shading is. \| ![](ss_shadow_numrays_0.png) \| ![](ss_shadow_numrays_1.png) \| \|---\|---\| \| *Number of Rays = 1* \| *Number of Rays = 15* \| | ![](ss_shadow_numrays_0.png) | ![](ss_shadow_numrays_1.png) | *Number of Rays = 1* | *Number of Rays = 15* |  |  |  |  |
| ![](ss_shadow_numrays_0.png) | ![](ss_shadow_numrays_1.png) |  |  |  |  |  |  |  |  |
| *Number of Rays = 1* | *Number of Rays = 15* |  |  |  |  |  |  |  |  |
| Number of Steps | Number of steps each ray traces. The higher the number of steps, the more accurate the computation of pixel shading is. \| ![](ss_shadow_numsteps_0.png) \| ![](ss_shadow_numsteps_1.png) \| \|---\|---\| \| *Number of Steps = 4; Number of Rays = 1* \| *Number of Steps = 32; Number of Rays = 1* \| | ![](ss_shadow_numsteps_0.png) | ![](ss_shadow_numsteps_1.png) | *Number of Steps = 4; Number of Rays = 1* | *Number of Steps = 32; Number of Rays = 1* |  |  |  |  |
| ![](ss_shadow_numsteps_0.png) | ![](ss_shadow_numsteps_1.png) |  |  |  |  |  |  |  |  |
| *Number of Steps = 4; Number of Rays = 1* | *Number of Steps = 32; Number of Rays = 1* |  |  |  |  |  |  |  |  |
| Noise Ray | Ray tracing dispersion. The higher the noise, the more chaotic the direction of rays is. \| ![](ss_shadow_noiseray_0.png) \| ![](ss_shadow_noiseray_1.png) \| \|---\|---\| \| *Noise Ray = 0.5* \| *Noise Ray = 0* \| | ![](ss_shadow_noiseray_0.png) | ![](ss_shadow_noiseray_1.png) | *Noise Ray = 0.5* | *Noise Ray = 0* |  |  |  |  |
| ![](ss_shadow_noiseray_0.png) | ![](ss_shadow_noiseray_1.png) |  |  |  |  |  |  |  |  |
| *Noise Ray = 0.5* | *Noise Ray = 0* |  |  |  |  |  |  |  |  |
| Noise Step | Dispersion of steps. The higher the noise, the more scattering the steps are. \| ![](ss_shadow_noiseray_0.png) \| ![](ss_shadow_noisestep_0.png) \| \|---\|---\| \| *Noise Step = 0.5; Noise Ray = 0.5* \| *Noise Step = 0; Noise Ray = 0.5* \| Depending on the value of the [Noise Ray](#noise_ray) parameter, the shadow may differ for the same values of **Noise Step**. \| ![](ss_shadow_noiseray_1.png) \| ![](ss_shadow_noisestep_1.png) \| \|---\|---\| \| *Noise Step = 0.5; Noise Ray = 0* \| *Noise Step = 0; Noise Ray = 0* \| | ![](ss_shadow_noiseray_0.png) | ![](ss_shadow_noisestep_0.png) | *Noise Step = 0.5; Noise Ray = 0.5* | *Noise Step = 0; Noise Ray = 0.5* | ![](ss_shadow_noiseray_1.png) | ![](ss_shadow_noisestep_1.png) | *Noise Step = 0.5; Noise Ray = 0* | *Noise Step = 0; Noise Ray = 0* |
| ![](ss_shadow_noiseray_0.png) | ![](ss_shadow_noisestep_0.png) |  |  |  |  |  |  |  |  |
| *Noise Step = 0.5; Noise Ray = 0.5* | *Noise Step = 0; Noise Ray = 0.5* |  |  |  |  |  |  |  |  |
| ![](ss_shadow_noiseray_1.png) | ![](ss_shadow_noisestep_1.png) |  |  |  |  |  |  |  |  |
| *Noise Step = 0.5; Noise Ray = 0* | *Noise Step = 0; Noise Ray = 0* |  |  |  |  |  |  |  |  |
| Near Step Size | Length of each step used in ray-traced shadows within *[Near Step Size Distance](#near_step_size_distance)*. - *Low* values cause the closest pixels to shade. - Higher values lengthen the shadow spreading. - Too high values can provoke shadow gaps. \| ![](ss_shadow_stepsize_0.png) \| ![](ss_shadow_stepsize_1.png) \| \|---\|---\| \| *Step Size = 0.5* \| *Step Size = 20* \| | ![](ss_shadow_stepsize_0.png) | ![](ss_shadow_stepsize_1.png) | *Step Size = 0.5* | *Step Size = 20* |  |  |  |  |
| ![](ss_shadow_stepsize_0.png) | ![](ss_shadow_stepsize_1.png) |  |  |  |  |  |  |  |  |
| *Step Size = 0.5* | *Step Size = 20* |  |  |  |  |  |  |  |  |
| Far Step Size | Length of each step used in ray-traced shadows (see the [description](#near_step_size) above) starting from *[Far Step Size Distance](#far_step_size_distance)*. |  |  |  |  |  |  |  |  |
| Near Step Size Distance | Distance from the camera, in units. Up to this distance, *[Near Step Size](#near_step_size)* is used for screen-space shadows. |  |  |  |  |  |  |  |  |
| Far Step Size Distance | Distance from the camera, in units. After this distance, *[Far Step Size](#far_step_size)* is used for screen-space shadows. For the space between *Near Step Size Distance* and *Far Step Size Distance*, the step size interpolates from *Near Step Size* to *Far Step Size*. |  |  |  |  |  |  |  |  |
| Near Threshold | Threshold value for *[Near Step Size](#near_step_size)*. This value defines the limit of samples passing the screen-space shadowing. - *Low* values let pass more samples which causes the shading of inappropriate pixels. - Higher values can also cause inaccurate shading by limiting appropriate samples. \| ![](ss_shadow_threshold_0.png) *Threshold = 0* \| ![](ss_shadow_threshold_1.png) *Threshold = 1* \| ![](ss_shadow_threshold_2.png) *Threshold = 4* \| \|---\|---\|---\| | ![](ss_shadow_threshold_0.png) *Threshold = 0* | ![](ss_shadow_threshold_1.png) *Threshold = 1* | ![](ss_shadow_threshold_2.png) *Threshold = 4* |  |  |  |  |  |
| ![](ss_shadow_threshold_0.png) *Threshold = 0* | ![](ss_shadow_threshold_1.png) *Threshold = 1* | ![](ss_shadow_threshold_2.png) *Threshold = 4* |  |  |  |  |  |  |  |
| Far Threshold | Threshold value (see the [description](#near_threshold) above) for *[Far Step Size](#far_step_size)*. |  |  |  |  |  |  |  |  |
| Near Threshold Distance | Distance from the camera, in units. Up to this distance, *[Near Threshold](#near_threshold)* is used. |  |  |  |  |  |  |  |  |
| Far Threshold Distance | Distance from the camera, in units. After this distance, *[Far Threshold](#far_threshold)* is used for screen-space shadows. For the space between *Near Threshold Distance* and *Far Threshold Distance*, the threshold value interpolates from *Near Threshold* to *Far Threshold*. |  |  |  |  |  |  |  |  |
| Softness | Size of the blur applied to the shadow edge. - *Low* softness values corresponds to the crisp and sharp shadow edges. - Higher softness values serve to accentuate the effect of soft indirect lighting. \| ![](ss_shadow_softness_0.png) \| ![](ss_shadow_softness_1.png) \| \|---\|---\| \| *Softness = 0* \| *Softness = 0.5* \| | ![](ss_shadow_softness_0.png) | ![](ss_shadow_softness_1.png) | *Softness = 0* | *Softness = 0.5* |  |  |  |  |
| ![](ss_shadow_softness_0.png) | ![](ss_shadow_softness_1.png) |  |  |  |  |  |  |  |  |
| *Softness = 0* | *Softness = 0.5* |  |  |  |  |  |  |  |  |
| Noise Translucent | Makes translucent shadows smoother by adding noise. The higher the value the more intense and noticeable the noise is. > **Notice:** This option affects performance, so use it only in case it noticeably improves the result. |  |  |  |  |  |  |  |  |
| Translucent Depth | This parameter indicates how much the light passes through screen-space shadows on translucent materials (with **Translucence** option enabled): the *higher* the value the *deeper* the light penetrates translucent objects shifting the shadow. |  |  |  |  |  |  |  |  |
| Translucent Depth Perspective Compensation | Perspective compensation for the *[Translucent Depth](#sss_translucent_depth)* value above: - 0 - the *Translucent Depth* value does not depend on the distance from the camera to the surface. - 1 - the *Translucent Depth* value linearly depends on the distance from the camera to the surface. This effect is used to make tree crowns located far from the camera more translucent than the grass nearby. |  |  |  |  |  |  |  |  |
| Translucent View Bias | This parameter can be used to create an effect of fuzziness for vegetation (e.g. to simulate leaves of saintpaulia or provide a sponge-like look for tree crowns). - By the value of 0 the effect is disabled - the value of 1 corresponds to the maximum effect. |  |  |  |  |  |  |  |  |


## Lens Flares Settings


**Lens Flares** simulate the effect of lights refracting inside camera lens. They are used to represent very bright lights or to add more atmosphere to your scene. The settings described below are used per-light, you can also use the [lens flares camera effect](../../../editor2/settings/render_settings/camera_effects/index.md#lens), which is applied to all lights and bright objects (e.g. having an [emissive material](../../../content/materials/library/mesh_base/index.md#option_emission) with high intensity assigned).


Lens Flares are rendered as [billboards](#lens_billboards_settings), each associated with a part of a [single texture](#lens_texture) and having a set of [parameters](#lens_billboards_settings), that determine its appearance and behavior. So, you can customize and fine tune your lens flares to fit your needs.


> **Notice:** This feature is available only for: *[Light Omni](../../../objects/lights/omni/index.md), [Light Projected](../../../objects/lights/proj/index.md)* and *[Light World](../../../objects/lights/world/index.md)*.


![](lens_flares_settings.png)


| Enabled | Enables or disables lens flares from the light source. By default this effect is disabled. > **Notice:** The maximum number of lights on the scene for which the per-light flares will be rendered is **32**. |  |  |  |  |
|---|---|---|---|---|---|
| Texture | A texture used to render [billboards](#lens_billboards_settings) representing lens flares. The default texture is shown in the image below. For each billboard you can specify [*UV* coordinates](#lens_billboard_ll_x) within this texture to determine its appearance. You can set your own texture, that contains the appearance for all the billboards to be used. ![](lens_texture.png) |  |  |  |  |
| Intensity | Intensity of per-light lens flares. Higher values make the effect more pronounced. |  |  |  |  |
| Occlusion Fade | Lens flare occlusion fade value for the cases when the light source becomes occluded by an object. By the value of 0.0f, lens flares disappear abruptly, as the light source becomes occluded by an object. If 1.0f is set, lens flares will fade out gradually. > **Notice:** Transparent objects are currently treated as opaque ones (i.e. they won't occlude flares). |  |  |  |  |
| Occlusion Fade Border | Lens flare occlusion fade value for the cases when the light source becomes occluded by the edges of the screen. By the value of 0.0f, lens flares disappear abruptly, as the light source becomes occluded by the edges of the screen. If 1.0f is set, lens flares will fade out gradually. |  |  |  |  |
| Position Offset | An offset of the center of lens flares from the world position of the light source. > **Notice:** This parameter is not available for *[Light World](../../../objects/lights/world/index.md)* \| ![](lens_offset_0.png) \| ![](lens_offset_1.png) \| \|---\|---\| \| *Position Offset = (0.0, 0.0, 0.0)* \| *Position Offset = (2.0, -3.0, 0.0)* \| | ![](lens_offset_0.png) | ![](lens_offset_1.png) | *Position Offset = (0.0, 0.0, 0.0)* | *Position Offset = (2.0, -3.0, 0.0)* |
| ![](lens_offset_0.png) | ![](lens_offset_1.png) |  |  |  |  |
| *Position Offset = (0.0, 0.0, 0.0)* | *Position Offset = (2.0, -3.0, 0.0)* |  |  |  |  |
| Use Light Color | When enabled, the lens flares will have the same color as the light source. |  |  |  |  |


### Lens Flares Billboards Settings


Each flare is represented by a separate billboard, The default number of billboards is 30, but you can change it if necessary by adding, removing, or cloning selected billboards in the list via the corresponding buttons.


As you select a billboard in the list, its parameters become available for editing in the fields below.


![](billboards.png)


> **Notice:** You can enable visualization of lens flare billboards via *Helpers -> Show Wireframe*.


| Color | Color multiplier for the selected billboard. [Texture](#lens_texture) colors will be multiplied by this value. By default the color is white. \| ![](billboard_offset_1.png) \| ![](billboard_color_1.png) \| \|---\|---\| \| ![](omni_color_white.png) \| ![](omni_color_yellow.png) \| | ![](billboard_offset_1.png) | ![](billboard_color_1.png) | ![](omni_color_white.png) | ![](omni_color_yellow.png) |
|---|---|---|---|---|---|
| ![](billboard_offset_1.png) | ![](billboard_color_1.png) |  |  |  |  |
| ![](omni_color_white.png) | ![](omni_color_yellow.png) |  |  |  |  |
| Size | This parameter controls the size of the selected billboard. \| ![](billboard_size_1.png) \| ![](billboard_offset_1.png) \| \|---\|---\| \| *Size = 1.5* \| *Size = 5* \| | ![](billboard_size_1.png) | ![](billboard_offset_1.png) | *Size = 1.5* | *Size = 5* |
| ![](billboard_size_1.png) | ![](billboard_offset_1.png) |  |  |  |  |
| *Size = 1.5* | *Size = 5* |  |  |  |  |
| Intensity | Multiplier for the billboard color used to control color intensity. The *higher* the value, the brighter the billboard is. \| ![](billboard_offset_1.png) \| ![](billboard_intensity_5.png) \| \|---\|---\| \| *Intensity = 1* \| *Intensity = 5* \| | ![](billboard_offset_1.png) | ![](billboard_intensity_5.png) | *Intensity = 1* | *Intensity = 5* |
| ![](billboard_offset_1.png) | ![](billboard_intensity_5.png) |  |  |  |  |
| *Intensity = 1* | *Intensity = 5* |  |  |  |  |
| Offset | Offset determines the distance between the light source and the billboard along the vector oriented from the light source to the screen center. The lower the absolute value is, the closer to the light source the billboard will be. Negative values indicate that the distance is measured in the opposite direction. \| ![](billboard_offset_0.png) \| ![](billboard_offset_1.png) \| \|---\|---\| \| *Offset = 0.3* \| *Offset = 0.9* \| | ![](billboard_offset_0.png) | ![](billboard_offset_1.png) | *Offset = 0.3* | *Offset = 0.9* |
| ![](billboard_offset_0.png) | ![](billboard_offset_1.png) |  |  |  |  |
| *Offset = 0.3* | *Offset = 0.9* |  |  |  |  |
| Offset Scale | Determines how the billboard changes its scale depending on the distance from the light source. As the [offset](#lens_billboard_offset) from the light source increases: - Values **less** than 1.0f will make the billboard shrink. - Values **greater** than 1.0f will make the billboard grow. \| ![](billboard_offset_1.png) \| ![](billboard_offset_scale_4.png) \| \|---\|---\| \| *Offset Scale= 1.0* \| *Offset Scale = 4.0* \| | ![](billboard_offset_1.png) | ![](billboard_offset_scale_4.png) | *Offset Scale= 1.0* | *Offset Scale = 4.0* |
| ![](billboard_offset_1.png) | ![](billboard_offset_scale_4.png) |  |  |  |  |
| *Offset Scale= 1.0* | *Offset Scale = 4.0* |  |  |  |  |
| Lower Left X | X coordinate of the lower left corner of the selected billboard in the [lens flares texture](#lens_texture), in the range [0.0, 1.0], e.g., the value equal to 0.5 corresponds to the middle of the texture. |  |  |  |  |
| Lower Left Y | Y coordinate of the lower left corner of the selected billboard in the [lens flares texture](#lens_texture), in the range [0.0, 1.0], e.g., the value equal to 0.5 corresponds to the middle of the texture. |  |  |  |  |
| Upper Right X | X coordinate of the upper right corner of the selected billboard in the [lens flares texture](#lens_texture), in the range [0.0, 1.0], e.g., the value equal to 0.5 corresponds to the middle of the texture. |  |  |  |  |
| Upper Right Y | Y coordinate of the upper right corner of the selected billboard in the [lens flares texture](#lens_texture), in the range [0.0, 1.0], e.g., the value equal to 0.5 corresponds to the middle of the texture. |  |  |  |  |
| Rotate | Enables or disables rotation of the lens flare billboard. When enabled the top of the billboard will always face the center of the screen. |  |  |  |  |
