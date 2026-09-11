# Environment Probe


*Environment Probe* is a light source which also provides reflections on an object inside the probe by using a cubemap (pre-baked or dynamically changing each frame). In UNIGINE, *Environment Probe* has three types of projections:


- **Box Projection** � works better for indoor scenes (when the room has a 3D box shape) or box-shaped outdoor scenes (back alley between buildings).
- **Spherical Projection** � works better for spherical-shape cases.
- **Raymarching** � works for all other cases, the probe renders reflections taking various shapes of surrounding surfaces into account. Lighting is calculated using physically-correct formulas ensuring that reflections as well as diffuse lighting become more realistic in comparison with Box and Sphere projections, and consequently more resource-consuming.


With *Environment Probe* you can create reflections instead of creating reflection materials.


> **Notice:** By default *Environment Probe* is used for reflections only; as for lighting, it is recommended to simulate it using *[Voxel Probe](../../../objects/lights/voxelprobe/index.md)* and [Lightmaps](../../../editor2/lighting/gi/lightmaps.md). This approach ensures the best result, however you can still [use *Environment Probe* for ambient lighting](#light_reflection_parameters).


### See Also


- The article on [Using *Environment Probe*](../../../editor2/lighting/gi/env_probes.md)
- The article on [Light Sources Parameters](../../../objects/lights/parameters/index.md)
- The *[LightEnvironmentProbe](../../../api/library/lights/class.lightenvironmentprobe_cpp.md)* class to manage *Environment Probe* via API


## Overview


*Environment Probe* is a great thing to increase performance, decrease the number of materials and make the life of content designers easier.


*Environment Probe* uses cubemaps that were baked (or grabbed with a special tool). The cubemap will play the role of the reflection and the light simulation. Here is an example:


We have two houses with different color of the interior and put same objects (with reflection material, for example, metal) into these houses. What will happen?


![](envprobe_houses.png)


If we don't speak about the dynamic reflections, you'll need to reflect the interior on each object. But interiors have different ambient color, and that is why you'll need to create 2 different materials for them. Not optimized at all.


*Environment Probe* removes this flaw. Once you added an object, you don't think about the reflection material for it. *Environment Probe* will map the cubemap to the object.


![](envprobe_projection.png)


There is a difference in mapping cubemaps to transparent and non-transparent objects:


- If an object is transparent, the *Environment Probe* maps the cubemap to the entire object as long as any part of it is within the probe radius.
- If an object is non-transparent, the *Environment Probe* maps the cubemap to the part of the object that is inside the radius of the probe.


| ![](envprobe_transparent_object.png) | ![](envprobe_nontransparent_object.png) |
|---|---|
| *Transparent object affected byEnvironment Probe* | *Non-transparent object affected byEnvironment Probe* |


If you put several *Environment Probe* nodes that affect a non-transparent object (rendered in the [deferred pass](../../../principles/render/sequence/index.md#opaque_deferred)) their cubemaps will be blended smoothly. Here is an example, a long corridor which has walls painted in different colors.


![](envprobe_lerp.png)


We put two *Environment Probe* nodes and they both affect the object (when the object is in the intercrossing area). If you have large locations, you should use several *Environment Probe* nodes instead of one to make the final image more realistic.


The *[SSR](../../../editor2/settings/render_settings/ssr/index.md)* (Screen Space Reflections) effect makes the final image more realistic, because it appends reflections that cannot be baked into cubemaps. Using *Environment Probe* and *SSR* is a great method for pretty fast imitation of reflections with dynamic lighting.


### Multiple Environment Probe for Transparent Objects


The *[Multiple Environment Probes](../../../content/materials/library/mesh_base/index.md#multiple_env_probes)* option set for a transparent object (rendered in the [forward pass](../../../principles/render/sequence/index.md#transparent)) allows several *Environment Probe* nodes affect the object and map their cubemaps to it.


- When the option is disabled, only the last set *Environment Probe* will affect the object. At that, the entire object must be inside the radius of *Environment Probe*. Otherwise, it won't be affected by this *Environment Probe* at all.
- When the option is enabled, the object will be lit by the whole *Environment Probe*: each probe will affect the part of the object, which is inside the probe. Cubemaps of *Environment Probe* nodes will be blended in the intercrossing areas.


> **Notice:** Rendering of multiple *Environment Probe* nodes must be enabled via *Rendering -> Transparent -> Multiple Environment Probes*.


| ![](envprobe_multiple_off.png) | ![](envprobe_multiple_on.png) |
|---|---|
| *Multiple Environment Probesis off: only the left cubemap is mapped to the object* | *Multiple Environment Probesis on: both cubemaps are mapped and blended* |


## Adding Environment Probe


To add an *Environment Probe* node to the scene via UnigineEditor, do the following:


1. [Run](../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Lights* and select the required *Environment Probe*: Box, Sphere, or Raymarching. The [projection shape](#common_params) can be changed after it is created via the *Parameters* window. ![](envprobe_create.png)
3. Place *Environment Probe*.
4. Grab the cubemap texture for *Environment Probe*. You can grab it via the *[Parameters](../../../editor2/node_parameters/index.md)* window or use the *[Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md)* tool.
5. Adjust the *Environment Probe* [settings](#settings).


> **Notice:** - You can't bake realtime lights (*[Omni Light](../../../objects/lights/omni/index.md), [Projected Light](../../../objects/lights/proj/index.md)*, etc.) to *Environment Probe*. The best you can do is to place spheres with emission materials instead of lights, adjust emission intensity and then bake lighting. However, the result will look worse than you'd have with realtime lights.
> - Use the *[**Bake to Environment Probes**](../../../editor2/node_parameters/visual_representation/index.md#bake_to_environment_probes)* option to define if a surface should have its reflections baked to *Environment Probe*.


When *Environment Probe* is selected in the UnigineEditor viewport, reference spheres are visualized in the center of the probe:


- Indirect Specular sphere helps in estimating the reflection provided by the probe.
- Indirect Diffuse sphere helps in estimating the ambient lighting provided by the probe (requires [Indirect Diffuse](#indirect_diffuse) lighting to be enabled).


![](visualize_ambient.png)


## Environment Probe Settings


The *Environment Probe* settings can be found in the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window. This tab contains both the [parameters attributable to all light sources](../../../objects/lights/parameters/index.md) and the parameters specific for *Environment Probe*. The specific parameters are described below.


### Common Parameters


![](common_params.png)


| Projection Type used by *Environment Probe*: | - **Box Projection** � works better for indoor scenes (when the room has a 3D box shape) or box-shaped outdoor scenes (back alley between buildings). - **Sphere Projection** � works better for spherical-shape cases. - **Raymarching** � works for all other cases, the probe renders reflections taking various shapes of surrounding surfaces into account. Lighting is calculated using physically-correct formulas ensuring that reflections as well as diffuse lighting become more realistic in comparison with Box and Sphere projections, and consequently more resource-consuming. |
|---|---|
| Box Projection Size | Specifies the size of the box projection. |
| Attenuation Distance | Sets the [attenuation distance](../../../objects/lights/parameters/index.md#attenuation_distance) for *Environment Probe*. |
| Attenuation Power | Sets the [attenuation power](../../../objects/lights/parameters/index.md#attenuation_power) for *Environment Probe*. |


### Render Parameters


![](render_params.png)


| Color | Sets the light [color](../../../objects/lights/parameters/index.md#color) in the RGBA format. The color defines both the plausibility of virtual representation and its aesthetic component. |
|---|---|
| Intensity | Sets the light color [multiplier](../../../objects/lights/parameters/index.md#intensity), which provides fine control over color intensity of the emitted light: - The minimum value of 1 corresponds to the least saturated light color. - The maximum value of 100 equals the most bright and intense color. |
| Shadow Mask | The *[Shadow](../../../principles/bit_masking/index.md#shadow_mask)* mask controls rendering of a shadow cast by an object lit by a light source. |
| Viewport Mask | Sets the *[Viewport](../../../objects/lights/parameters/index.md#viewport_mask)* mask for the light. |
| Visibility Distance | Distance from the camera, in units, up to which *Environment Probe* will be rendered. |
| Fade Distance | Distance from the camera, in units, starting from which *Environment Probe* starts to fade out gradually. |
| Render On Water | Renders *Environment Probe* on the water surface. |
| Render On Transparent | Renders *Environment Probe* on transparent surfaces. |
| Multiply By Sky Color | Enables the influence of [sun light color](../../../editor2/settings/render_settings/environment/index.md#light_lut) on *Environment Probe*. > **Notice:** When enabled, this option makes the *Environment Probe* color black at night, or orange at sunset. |
| Additive Blending | Enables the additive blending mode for *Environment Probe*. This option offers more flexibility in lighting and reflections control. You can use it to blend lighting and reflections of several *Environment Probe* nodes together and control them separately. |
| Rendering Order | Order in which multiple *Environment Probes* are rendered. A higher value means a higher priority. |
| Render Above Voxel Probes | Toggles rendering of the Environment Probe above Voxel Probes (or other Environment Probes) to imitate the GI bounce from the sun. If enabled, the *Environment Probe* is additively blended with Voxel Probes (or other Environment Probes). In case of several Environment Probes having this setting enabled, they are rendered according to the specified [Rendering Order](#rendering_order). |
| Noise Frames Number | The number of variations of the noise pattern, which is changed every frame. Higher values result in a more dynamic noise effect, but a significant temporal accumulation of frames will make the image look like more rays are used. Smaller values result in a more static noise pattern. |
| Secondary Bounce Projection | Specifies the type of the secondary bounce projection used for dynamic reflections. It determines how secondary light bounces are calculated and projected, impacting the quality of dynamic reflections. The following projection types are available: - **Sphere Projection** - this type uses a spherical approximation to calculate secondary light bounces. It offers significantly higher performance than **Raymarching** and allows you to avoid noise in the secondary bounce. - **Raymarching** - this type calculates secondary light bounces by tracing rays through the scene. While this method is more physically correct, it has low performance and introduces noise into the secondary bounce. |
| Last Step Cubemap | Allows selecting the cubemap to be used for the last raymarching step: - **Environment Probe** � the cubemap used for the last step is the same as for all previous steps. - **Only Sky** � the cubemap contains the sky and clouds only. This option is designed to fix the incorrect parallax that may occur in reflections due to the infinite length of the last step. |


### Indirect Diffuse and Specular Parameters


In general there are two groups of parameters:


| Indirect Diffuse | Enables indirect diffuse (ambient) lighting for *Environment Probe*. By default, *Environment Probe* is used for reflections only; as for lighting, it is recommended to simulate it using *[Voxel Probe](../../../objects/lights/voxelprobe/index.md)* and [Lightmaps](../../../editor2/lighting/gi/lightmaps.md) � this approach ensures the best result. However, you can still use *Environment Probe* for indirect diffuse lighting by enabling this option. |
|---|---|
| Indirect Specular | Toggles specular lighting for *Environment Probe*. |


The parameters differ depending on the *Environment Probe* type.


#### Sphere Projection


![Sphere Projection Parameters](sphere_params.png)


| Contrast | Sets the contrast of indirect diffuse lighting. |
|---|---|
| Parallax | Enables rendering of reflections taking into account the camera's position. When this option is disabled, reflection cubemaps are simply projected onto objects, and do not follow the viewer's perspective. - 0 (minimum) � parallax correction is disabled (reflections will look like objects are infinitely distant). - 1 (maximum) � parallax correction is enabled (reflections will look like objects are at the distance close to the radius of *Environment Probe*). - Values in-between represent a linear interpolation factor for parallax correction and are to be set when *Environment Probe* is used to fit a medium or small object into the environment for additional correction, if necessary. > **Notice:** Parallax correction does not affect reflections on transparent objects. ![](parallax_0.jpg) ![](parallax_1.jpg) |
| **Cubic Filtering** | Enables bicubic interpolation for the Enviropment Probe cubemap instead of the standard bilinear interpolation. This effect is only applicable to reflected lighting and calculated if a pixel has a low *[Roughness](../../../content/materials/library/mesh_base/index.md#parameter_roughness)* value. Modifications are applied only to the first mip of the cubemap. The effect visually represents slight blurring of neighboring pixels. However, this is not antialiasing and might affect the visual quality of high-resolution probes. This option may be combined with *[sRGB Filtering Correction](#srgb_filtering_correction)* to achieve a better gradient between pixels. > **Notice:** - Enabling this option affects performance, thus it is recommended to enable it only for Environment Probes affecting a big number of reflective/mirror pixels, especially if it is a realtime low-resolution Probe. > - For this option to have an effect on a **transparent** sufrace, the *[Reflection Cubic Filtering](../../../content/materials/library/mesh_base/index.md#option_reflection_cubic_filtering)* state should be enabled for the material (for non-transparent materials the option is applied automatically). > - The option does not affect [Impostors](../../../editor2/tools/impostors_creator/index.md). |


#### Box Projection


![Box Projection Parameters](box_params.png)


| Ambient Parallax | Enables the global illumination simulation. *Environment Probe* generates fake GI by using the cubemap. |
|---|---|
| Contrast | Sets the contrast of indirect diffuse lighting. |
| Gloss Corners | The intensity of reflection gloss near the box projection corners. |
| Cubic Filtering | See [above](#cubic_filtering). |


#### Raymarching


| [![Raymarching Parameters for Indirect Diffuse](raymarching_params_diffuse.png)](raymarching_params_diffuse.png) | [![Raymarching Parameters for Indirect Specular](raymarching_params_specular.png)](raymarching_params_specular.png) |
|---|---|


| Num Rays | The number of rays per pixel that are used to calculate diffuse/specular reflections from rough surfaces. Using more rays provides more precise reflection roughness calculation, however, it is more expensive. |
|---|---|
| Num Steps | The number of steps per ray that are used for trace calculation. The number of steps defines accuracy of indirect light / reflections and causes a reasonable performance impact. The higher the value, the more accurate obstacles between objects are taken into account. |
| Step Size | The size of the trace step used for the diffuse/specular reflection calculation. Higher values result in longer traces (however, tiny objects may become missing), lower values produce more detailed reflections of tiny objects. |
| Num Steps Roughness Threshold | The roughness value at which the number of steps (*Num Steps*) equals to 1. This is required for optimization, as calculating matte reflections as correctly as possible may be unnecessary. |
| Information Lost Rays Multiplier | The multiplier for the number of rays (*Num Rays*) in the areas where the ghosting effect usually occurs. Increasing this value reduces the ghosting, but the more ghosting cases are, the more it affects performance. |
| Mip Offset | The mipmap offset for the cubemap that is used for the diffuse light / specular reflections calculation. Increasing the value affects performance, lighting turns to be less detailed and realistic, small objects on the cubemap may be lost. The 0 value provides the most visually credible result, but more rays are required to eliminate the noise. |
| Threshold | The threshold used for the diffuse light / specular reflections calculation to limit imitation of reflections in areas where information can't be obtained. Higher values make the effect less pronounced. |
| Threshold Occlusion | The value that limits imitation of environment cubemap occlusion in areas where information can't be obtained. Higher values make the effect less pronounced. This parameter is mainly used for indoor environment to correct false reflections on occluded areas (false reflections are replaced with black color). For outdoor environment, higher values of this parameter are recommended. |
| Reconstruction Samples Screen | The number of iterations required for a more accurate detection of the screen-space ray-surface intersection. Higher values define the intersection more precisely, however significantly affect performance. |
| Threshold Binary Search | Threshold value used for the intersection detection that defines the depth of the ray penetration under the surface. Higher values may cause more false intersections, but make the process of intersection detection easier. |
| Perspective Compensation | Perspective compensation for the raymarching step size. 0 means that the raymarching step size is bound to the World Space, and 1 means that it is bound to the Screen Space. As a result, at the value of 1, the ray length at the distance from the camera will be more than at a closer distance, which makes sense for large objects, but the details on small objects in the distance may will be lost. |
| Non Linear Step Size | Raymarching step size adjustment value. The value of 0 means that the step size is the same for each step, and at the value of 1 each subsequent raymarching step is twice wider than the previous one. |
| AO Intensity | Ambient occlusion intensity. Keep in mind that ambient occlusion doesn't exist in the real world, this is a method to imitate shadows between objects. For photorealistic visualization, we recommend keeping this value equal to 0. |
| AO Radius | Radius of sample pixels used in the Ambient Occlusion effect, controlling the extent of the darkened area. |
| Translucent Anisotropy | The value defining the extent of the light penetration through transparent surfaces. - 0 � light does not penetrate through surfaces. - 0.5 � light is distributed equally on both sides of the surface (along the ray direction and towards the light source) - 1.0 � all light passes through the surface along the ray direction. |
| Replace With Diffuse Roughness Threshold | The rougness value starting from which *Indirect Specular* stops being calculated and is replaced with *Indirect Diffuse*. This setting is used to optimize matte reflections. |
| BRDF | The light distribution model for matte surfaces. GGX is more realistic, though increases noise and slightly reduces performance. |
| Cubic Filtering | See [above](#cubic_filtering). |


### Baking Settings


| [![Baking Settings for Baked Mode](baking_settings_baked.png)](baking_settings_baked.png) | [![Baking Settings for Realtime Update Mode](baking_settings_realtime.png)](baking_settings_realtime.png) |
|---|---|


> **Notice:** Re-grab the cubemap texture, when you make changes to these parameters.


| Mode | Specifies if the reflection is updated in realtime or baked into a [texture](#texture). > **Notice:** For the Realtime Update mode, the *Dynamic Reflections* option should be enabled: ***Rendering -> Features -> Dynamic Reflections***. |
|---|---|
| Faces Per Frame | Cubemap update interval: - 1 � Refresh only one face every frame. - 2 � Refresh two faces every frame. - 3 � Refresh three faces every frame. - 4 � Refresh four faces every frame. - 5 � Refresh five faces every frame. - 6 � Refresh all six faces every frame. > **Notice:** Available for the [Realtime Update mode](#mode) or Raymarching environment probes. |
| Grab by Bake Lighting | Specifies if the cubemap texture is to be modified by the *[Bake Lighting](../../../editor2/lighting/gi/bake_lighting/index.md)* Tool. |
| Reflection Viewport Mask | The [mask](../../../principles/bit_masking/index.md#reflection_mask) that controls rendering of the *Environment Probe*'s reflections into the reflection camera viewport. |
| Resolution | Resolution of the reflection texture, in pixels. > **Notice:** Setting too high resolution on a low-performance GPU with low memory capacity may cause engine crash. |
| Supersampling | Number of samples per pixel used for image grabbing supersampling. |
| Mipmaps Quality | The quality of mipmaps for environment reflections on rough surfaces. Quality modes differ in the number of rays used to create a reflection on a rough surface. > **Notice:** - Setting too high quality on a low-performance GPU with low memory capacity may cause engine crash. > - Available for the [Realtime Update mode](#mode) or Raymarching environment probes. |
| Distance Scale | Global distance multiplier within the range of [0.0f; 1.0f] for the reflection LODs visibility distance. *Distance Scale* is applied to the distance measured from the reflection camera to the node (surface) bound. > **Notice:** Available for the [Realtime Update mode](#mode) or Raymarching environment probes. |
| Near Clipping | Distance to the near clipping plane for image grabbing. |
| Far Clipping | Distance to the far clipping plane for image grabbing. > **Notice:** An extremely big difference between the Near and Far Clipping Planes can cause baking the space into black. Therefore, if the required *Far Clipping* value is outside the range, adjust the *Near Clipping* value proportionately. |
| Environment Ambient Intensity | Intensity of the environment ambient lighting. > **Notice:** Available for the [Realtime Update mode](#mode) or Raymarching environment probes. |
| Environment Reflection Intensity | Intensity of the environment reflection. > **Notice:** Available for the [Realtime Update mode](#mode) or Raymarching environment probes. |
| Sky Cutout | Cut out sky rendering in *Environment Probe* and renders dynamic reflection instead of the sky. > **Notice:** This parameter can be used to render changes of the sky gradient in a window, when the time of the day changes. |
| Local Space | Enable local space (local coordinates) for *Environment Probe*. Can be used for scenes with moving objects. > **Notice:** It is recommended to use this parameter, if you plan to rotate the *Environment Probe* after baking. |
| > **Notice:** You can use the following 7 visibility options together with [additive blending](#additive_blending) to provide more flexibility in [light baking](../../../editor2/lighting/gi/bake_lighting/index.md). Thus, you can make *Environment Probe* nodes independent of each other and combine them to produce some sort of dynamic GI effect. |  |
| Visibility Sky | Enables baking of [lighting from the sky](../../../editor2/lighting/environment.md) to *Environment Probe*. |
| Visibility Light World | Enables baking of *[World Light](../../../objects/lights/world/index.md)* sources to *Environment Probe*. |
| Visibility Light Omni | Enables baking of *[Omni Light](../../../objects/lights/omni/index.md)* sources to *Environment Probe*. |
| Visibility Light Proj | Enables baking of *[Projected Light](../../../objects/lights/proj/index.md)* sources to *Environment Probe*. |
| Visibility Haze | Enables baking of [haze](../../../editor2/lighting/environment.md#haze) to *Environment Probe*. |
| Visibility Voxel Probe | Enables baking of other *[Voxel Probe](../../../objects/lights/voxelprobe/index.md)* light sources to *Environment Probe*. |
| Visibility *Environment Probe* | Enables baking of *Environment Probe* light sources to the *Environment Probe*. |
| Visibility Emission | Enables baking of [emission](../../../content/materials/library/mesh_base/index.md#option_emission) light sources to *Environment Probe*. |
| Visibility Lightmap | Enables baking of [lightmapped surfaces](../../../editor2/lighting/gi/lightmaps.md) to *Environment Probe*. |
| Visibility Clouds | Enables baking of [clouds](../../../objects/objects/cloud_layer/index.md) to *Environment Probe*. |
| Texture | Cubemap texture for reflection. > **Notice:** Every bake lighting procedure makes changes to the asset selected in this field when the *[Grab by Bake Lighting](#grab_by_bake)* mode is enabled. > > > You can leave the field **empty** to avoid losing content. In this case a new generated lighting texture will be set for this parameter after the bake lighting procedure. Generated textures are stored in the `data/bake_lighting` folder. |
| Cutout By Shadow | Enables clipping of reflections occluded by obstacles (located in shadowed areas relative to the light source). This feature uses the [depth texture](#depth_texture) grabbed for *Environment Probe* to determine reflections that should be visible. > **Notice:** - This feature does not work with the *[Realtime Update](#mode)* mode enabled and does not clip reflections for transparent objects. > - The feature takes into account only the shadows cast by surfaces using the **[Cast Environment Probe Shadows](../../../editor2/node_parameters/visual_representation/index.md#cast_envprobe_shadows)** option. When enabled, the three parameters listed below (*[Bias](#bias), [Normal Bias](#normal_bias)*, and *[Depth Texture](#depth_texture)*) are available. ![](cutout_by_shadow_0.jpg) ![](cutout_by_shadow_1.jpg) |
| sRGB Filtering Correction | Toggles conversion of the baked cubemap or realtime calculation to sRGB color model and modifying it to a lower dynamic range. Applying this option ensures correct linear gradient between the neighboring pixels in the probe and makes transition between extremely bright pixels and other pixels smoother. Visually improves low-resolution probes by making them less pixelated and makes bright or constant pixels less prominent. This option modifies the cubemap, thus the state should remain unchanged after the cubemap for the static probe has been baked. If a static Environment Probe reuses a cubemap that has been baked with this option enabled, it should be enabled for this probe as well. Otherwise, the difference in brightness of light sources will be obvious. This option may be combined with [Cubic Filtering](#cubic_filtering) to achieve a better gradient between pixels. |
| Bias | Bias that is used to correct inexact shadowing of the scene objects for the *[Cutout By Shadow](#cutout_by_shadow)* feature. It controls the depth offset added to the current depth value stored in the shadow map. Similar to the *[Bias](../../../objects/lights/parameters/index.md#bias)* parameter for shadows. |
| Normal Bias | Bias obtained for the *[Cutout By Shadow](#cutout_by_shadow)* feature by shifting the surface on which the shadow falls. The surface is shifted along normals stored in the normal map. Similar to the *[Normal Bias](../../../objects/lights/parameters/index.md#normal_bias)* parameter for shadows. |
| Depth Texture | Depth texture used for clipping reflections occluded by obstacles. > **Notice:** This texture is static and requires re-generation each time the *Environment Probe* position or size is changed. To grab the depth texture for clipping perform the following steps: 1. Place *Environment Probe* to the desired location and adjust its size, if necessary. 2. Disable all nodes that should not be taken into account when calculating occluded (shadowed) areas. 3. Enable the *[Cutout By Shadow](#cutout_by_shadow)* feature and make sure that the *[Grab by Bake Lighting](#grab_by_bake)* mode is also enabled. 4. Click **Show Bake Lighting** and in the window that appears click **Bake Selected Probe**. 5. After the textures are generated, you can enable or disable clipping at run time. > **Notice:** Every bake lighting procedure makes changes to the asset selected in this field when the *[Grab by Bake Lighting](#grab_by_bake)* mode together with the *[Cutout By Shadow](#cutout_by_shadow)* mode are enabled. > > > You can leave the field **empty** to avoid losing content. In this case a new generated depth texture will be set for this parameter after the bake lighting procedure. Generated textures are stored in the `data/bake_lighting` folder. |
