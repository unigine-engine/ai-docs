# Global Water


**Global Water** is an infinitely spread mesh with auto-tessellation that represents a boundless ocean (the wireframe of the water is not scaled; regardless of the camera position it always stays the same). The object provides real-time water simulation based on **fast implementation of Gerstner waves model**. It is optimized so the GPU is not overloaded.


The list of features includes:


- realistic real-time water simulation based on fast implementation of Gerstner waves model;
- ability to create and control waves and wave groups (from largest to smallest), with the maximum of **256** simulated waves (recommended - **100**);
- ability to control every parameter [via API](../../../api/library/objects/class.objectwaterglobal_cpp.md) enabling you to apply results of calculations using different hydrodynamic models;
- practically no visible texture tiling effects at close and far distances;
- smooth change of sea states according to Beaufort scale;
- fast intersection detection and fetching water level at an arbitrary point at any moment of time;
- three wave-generation modes available, from fully automatic to fully customizable;
- flexible quality settings providing room for optimization.


The object has support for the **underwater** mode. However, it cannot have a body assigned, and thus does not provide proper physical interaction with scene objects. If you need to simulate the physics of buoyancy, you should use **[Physical Water](../../../objects/effects/physicals/physical_water/index.md)**. Also it is limited to a *single water level*. It means that the filling level of water always remains the same. So, if you need to create, for example, mountain lakes or water flows with height difference, you should use **[Water Mesh](../../../objects/objects/water/water_mesh.md)**.


With *Global Water* you can create waves using wave layers, Beaufort scale or manually and ensure smooth transitions between various states of the sea.


The *Global Water* object provides full control of the wave spectrum [through the API](../../../api/library/objects/class.objectwaterglobal_cpp.md). Unique characteristics of each wave system can be set independently through spectral parameters, wave direction, length, and amplitude, and the shape factor of waves at run time via API (as all the data is available on the CPU side).


> **Notice:** As the water object uses the *screenspace projected grid* for the water surface of the infinite size, it is recommended to use only one (1) water object in the scene.


[![](object_water_sm.png)](object_water.png)

*Ocean created with the Global Water object*


> **Notice:** To ensure optimal rendering of water as seen from different viewpoints, e.g., the shore or an airplane, use different *[Geometry Presets](../../../editor2/settings/render_settings/water_ssr/index.md#geometry_preset)* and *[Visibility Distance](../../../editor2/settings/render_settings/water_ssr/index.md#visibility_distance)* settings for the default *Global Water* Object (***Settings -> Water -> Geometry***).
>
>
> *Water [Visibility Distance](../../../editor2/settings/render_settings/water_ssr/index.md#visibility_distance)* should not exceed the *Camera visibility distance* (defined by its *[Far Clipping Plane](../../../editor2/camera_settings/index.md#far)*) for correct tile culling.


### See also


- The *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md)* class to edit *Global Water* via API
- A set of the **Water Global** samples included in the SDK demonstrate how to use API to control *Global Water* and [fetch water level](../../../objects/objects/water/water_object.md#fetch_intersection) at a given point:

  -
  -
  -
  -
  -
  -
- The *[water_global_base](../../../content/materials/library/water_global_base/index.md)* material


## Adding Water


To add infinite water to the scene via UnigineEditor:


1. On the Menu bar, click *Create -> Water -> Global*: ![](add_water1.png)
2. Place the water object in the scene: ![](added_water.png)


Infinite water will be added to the scene and you will be able to edit it via the *[Parameters](../../../editor2/node_parameters/index.md)* window.


## Editing Water


Water settings can be adjusted via the *[Parameters](../../../editor2/node_parameters/index.md)* window:


- On the *Node* tab, [water surfaces](../../../objects/objects/water/index.md#surfaces) that determine optical and dynamic behaviour of water can be adjusted.


## Creating Waves


There are three options for creating waves:


- **Layers mode** � you create layers on which waves will be randomly generated in a given range of wave parameters. All the layers are added together. > **Notice:** Wave layers are usually created through UnigineEditor, but you can also create and edit them [via code](../../../api/library/objects/class.objectwaterglobal_cpp.md).
- **Beauforts mode** � waves are generated based on the presets reproducing the state of the sea according to the Beaufort wind force scale (0 � Calm, 12 � Hurricane). In this mode, the parameters that define the main wave geometry will not be available for editing.
- **Manual mode** � you create your own individual waves and have full control over them. > **Notice:** This mode can only be set [via code](../../../api/library/objects/class.objectwaterglobal_cpp.md), you cannot do this in UnigineEditor.


When you enable the **Manual mode**, the list of generated waves is cleared and you can set up your own waves.


When you save the world, the layers will be saved, but the user-defined waves will not, since they are created [via code](../../../api/library/objects/class.objectwaterglobal_cpp.md).


## Wave Parameters


Wave parameters window in UnigineEditor is available on the *Node* tab and contains the following parts:


### Common


![](common1.png)


Parameters common for all wave layers:


| Water Mode | Wave generation mode. Two options are available: - **[Layers](#creating_waves)** mode - **[Beauforts](#creating_waves)** mode |
|---|---|
| Beauforts | Beaufort value from 0 (Calm) to 12 (Hurricane). > **Notice:** Available only in [Beauforts mode](#beauforts_mode). |
| Wind Direction | Angle that determines the wind direction, in degrees. |
| Wind Affect | Determines how much the wind direction affects the waves. The values are within the [0;1] range. If you set it to 1, all the waves will be directed along the wind direction. |
| Waves Speed Scale | Scale value that affects the speed of all the waves. |


### Waves Layers


> **Notice:** Available when the [Layers mode](#layers_mode) is selected.


![](waves_layers.png)


| Waves Count | Total number of waves on all layers. > **Notice:** We recommend keeping this value below **100** and use the minimum possible number. The maximum total number of waves is 256, but large numbers significantly affect performance. |
|---|---|


Parameters defined for each layer:


| Layer Weight | Weight of the wave layer determines how much the given layer affects the final wave form. |  |  |  |  |
|---|---|---|---|---|---|
| Waves Num | Number of waves on the layer. |  |  |  |  |
| Length Min | Lower limit of the wavelength range for the layer. |  |  |  |  |
| Length Max | Upper limit of the wavelength range for the layer. |  |  |  |  |
| Amplitude Min | Lower limit of the wave amplitude range for the layer. |  |  |  |  |
| Amplitude Max | Upper limit of the wave amplitude range for the layer. |  |  |  |  |
| Steepness Scale | The sharpness of the wave crests. To make waves look more plausible, the engine moves the vertices near the wave crest closer to the crest and recalculates their normals. This parameter specifies the force of the described contraction. Available range: [0; 1], default: 1. \| ![](choppy_0.png) \| ![](choppy_1.png) \| \|---\|---\| \| *Lower Steepness Scale* \| *Higher Steepness Scale* \| | ![](choppy_0.png) | ![](choppy_1.png) | *Lower Steepness Scale* | *Higher Steepness Scale* |
| ![](choppy_0.png) | ![](choppy_1.png) |  |  |  |  |
| *Lower Steepness Scale* | *Higher Steepness Scale* |  |  |  |  |
| Direction Angle Variance | Variance of the wave direction angle for the layer. If you set it to 90, the angles will be random between -90 and 90 relative to the wind direction. |  |  |  |  |


### Fields Interaction


![](fields_interaction.png)


Parameters defining interaction with *Field* objects:


| Field Spacer Enabled | Enables the effect of *[FieldSpacer](../../../objects/effects/fields/field_spacer/index.md)* object on the *Global Water* object. |
|---|---|
| Field Height Enabled | Enables the effect of *[FieldHeight](../../../objects/effects/fields/field_height/index.md)* object on the *Global Water* object. |
| Field Shoreline Enabled | Enables the effect of *[FieldShoreline](../../../objects/effects/fields/field_shoreline/index.md)* object on the *Global Water* object. |


### Normal


![](normal.png)


Parameters defining wave normals:


| Geometry Normal Intensity | Intensity of normals of the waves. |
|---|---|
| Texture Normal Blur | Blurring ratio for the procedurally generated normals. This parameter enables you to reduce pixelation of the normal map, and make it less pronounced. It is recommended to use small values for correction, when necessary. This affects the normals generated for [Field Height](../../../objects/effects/fields/field_height/index.md) and [Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md). |
| Texture Normal Intensity | Intensity of procedurally generated normals. This affects the normals generated for [Field Height](../../../objects/effects/fields/field_height/index.md) and [Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md). |


### Detail


![](detail.png)


Parameters defining normal detail texture:


| Normal Map | The **Normal Detail** map stores normal information required to achieve an additional (detail) effect of Normal Mapping. Normal map helps to create ripples (cat's-paw effect) on the water surface. The texture is 2-channeled: - *RG* values store two components of a surface normal. - *B* value is calculated based on the *R* and *G* values in run-time. \| ![](texture_n_0.png) \| ![](texture_n_1.png) \| \|---\|---\| \| *With absolutely white normal map* \| *With ripple-simulated normal map* \| | ![](texture_n_0.png) | ![](texture_n_1.png) | *With absolutely white normal map* | *With ripple-simulated normal map* |
|---|---|---|---|---|---|
| ![](texture_n_0.png) | ![](texture_n_1.png) |  |  |  |  |
| *With absolutely white normal map* | *With ripple-simulated normal map* |  |  |  |  |
| Detail 0 UV Transform | Specifies the UV transform for the first sample of the normal detail texture. The first two values are the scale texture coordinates along the X and Y axes. The third and forth specify the wind force and direction for the U and V axes. |  |  |  |  |
| Detail 0 Intensity | Intensity of the first sample of the normal detail texture. > **Notice:** Available only in [Layers mode](#layers_mode). |  |  |  |  |
| Detail 1 UV Transform | Specifies the UV transform for the second sample of the normal detail texture. The first two values are the scale texture coordinates along the X and Y axes. The third and forth specify the wind force and direction for the U and V axes. |  |  |  |  |
| Detail 1 Intensity | Intensity of the second sample of the normal detail texture. > **Notice:** Available only in [Layers mode](#layers_mode). |  |  |  |  |


### Distant Waves


*Global Water* has two parts: the waves on the inner part, which is close to the camera, are generated based on the wave spectrum, and all the rest � distant waves (simplified waves rendered starting at a certain distance from the camera to save performance), that are created by using a Normal map. The two parts are blended at a certain distance to ensure a smooth transition between them.


![](distant_waves1.png)


Parameters defining distant waves:


| Normal Map | The **Normal Map** texture is used to create ripples on the water surface for distant waves. The texture is 2-channeled: - *RG* � normal components. |
|---|---|
| UV Transform | UV transform for the distant waves normal map. The first two values (x,y) � represent the scale for texture coordinates along the X and Y axes, while the third and forth (z, w) � specify the speed of movement animation. |
| Intensity | Intensity value for the normal map of the distant waves. > **Notice:** Unavailable for modes with Beaufort levels blending. |
| Blend Min | Minimum amount of distant waves in the crossfade zone where the main geometry waves fade out and distant waves fade in (*Blend Distance*). The value is normalized in the [0, 1] range. |
| Blend Max | Maximum amount of distant waves in the crossfade zone where the main geometry waves fade out and distant waves fade in (*Blend Distance*). The value is normalized in the [0, 1] range. |
| Blend Distance Start | Fade-in start distance for distant waves. |
| Blend Distance End | Fade-in end distance for distant waves. |


### Foam


![](foam1.png)


Parameters defining the foam:


| Texture | This texture specifies foam on water. The engine samples the foam texture twice to create plausibility of the real world foam behavior. The texture is 3-channeled: - *RGB* values store the color. |
|---|---|
| Texture Affect | Visibility of the foam texture. It can be used to create additional effects, e.g., foam bubbles. |
| Patch 0 UV Size | Size of the first foam texture patch. |
| Patch 0 UV Speed | Speed of the first foam patch. |
| Patch 1 UV Size | Size of the second foam texture patch. |
| Patch 1 UV Speed | Speed of the second foam patch. |
| Peak Contrast | Foam contrast on the wave peaks. > **Notice:** Available only in [Layers mode](#layers_mode). |
| Peak Intensity | Foam intensity on the wave peaks. > **Notice:** Available only in [Layers mode](#layers_mode). |
| Whitecap Contrast | Foam contrast on the white caps. > **Notice:** Available only in [Layers mode](#layers_mode). |
| Whitecap Intensity | Foam intensity on the white caps. > **Notice:** Available only in [Layers mode](#layers_mode). |
| Wind Contrast | Contrast of the foam generated based on the wind direction. > **Notice:** Available only in [Layers mode](#layers_mode). |
| Wind Intensity | Intensity of the foam generated based on the wind direction. > **Notice:** Available only in [Layers mode](#layers_mode). |
| Contact Intensity | Foam intensity near shores or different objects in water. |


### Subsurface Scattering


![](subsurface_scattering.png)


Parameters defining the subsurface scattering:


| Color | Water subsurface scattering (**SSS**) color. \| ![](sss_color_0.png) \| ![](sss_color_1.png) \| \|---\|---\| \| ![](sss_color_param_0.png) \| ![](sss_color_param_1.png) \| | ![](sss_color_0.png) | ![](sss_color_1.png) | ![](sss_color_param_0.png) | ![](sss_color_param_1.png) |
|---|---|---|---|---|---|
| ![](sss_color_0.png) | ![](sss_color_1.png) |  |  |  |  |
| ![](sss_color_param_0.png) | ![](sss_color_param_1.png) |  |  |  |  |
| Ambient Intensity | Intensity of subsurface scattering for ambient lighting. The lower the value, the faster the light rays dissipate in water. \| ![](ambient_intensity_0.png) \| ![](ambient_intensity_1.png) \| \|---\|---\| \| ![](ambient_intensity_param_0.png) \| ![](ambient_intensity_param_1.png) \| | ![](ambient_intensity_0.png) | ![](ambient_intensity_1.png) | ![](ambient_intensity_param_0.png) | ![](ambient_intensity_param_1.png) |
| ![](ambient_intensity_0.png) | ![](ambient_intensity_1.png) |  |  |  |  |
| ![](ambient_intensity_param_0.png) | ![](ambient_intensity_param_1.png) |  |  |  |  |
| Intensity Through Waves | Intensity of light rays passing through waves. The lower the value, the faster the light rays dissipate in water. \| ![](intensity_tw_0.png) \| ![](intensity_tw_1.png) \| \|---\|---\| \| ![](intensity_tw_param_0.png) \| ![](intensity_tw_param_1.png) \| | ![](intensity_tw_0.png) | ![](intensity_tw_1.png) | ![](intensity_tw_param_0.png) | ![](intensity_tw_param_1.png) |
| ![](intensity_tw_0.png) | ![](intensity_tw_1.png) |  |  |  |  |
| ![](intensity_tw_param_0.png) | ![](intensity_tw_param_1.png) |  |  |  |  |
| Intensity Around Foam | Intensity of subsurface scattering near the foam areas. \| ![](intensity_af_0.png) \| ![](intensity_af_1.png) \| \|---\|---\| \| ![](intensity_af_param_0.png) \| ![](intensity_af_param_1.png) \| | ![](intensity_af_0.png) | ![](intensity_af_1.png) | ![](intensity_af_param_0.png) | ![](intensity_af_param_1.png) |
| ![](intensity_af_0.png) | ![](intensity_af_1.png) |  |  |  |  |
| ![](intensity_af_param_0.png) | ![](intensity_af_param_1.png) |  |  |  |  |
| Diffuse Intensity | Intensity of subsurface scattering for diffuse lighting. |  |  |  |  |


### Underwater


![](undwerwater_par.png)


The Underwater parameters adjust the underwater part of the Water Global object.


The final color of underwater is calculated using the following formula:


```text
FinalColor = FogColor * SunLighting^(1/FogSunLighting) + FogColor * EnvLighting^(1/FogEnvLighting)
```


*FogColor, FogSunLighting*, and *FogEnvLighting* are specified in the *Underwater* section. The other parameters (*Sun* and *Environment lighting*) are calculated according to the sun lighting and environment lighting of the scene. In fact, this formula defines how the sun and the environment lights affect the final underwater color.


| Underwater DOF | Adds an additional blur effect for underwater and overwater splice to make the waterline look more plausible. > **Notice:** You may need to adjust the [quality of waterline calculation](../../../editor2/settings/render_settings/water_ssr/index.md#waterline_accuracy) in case of medium and high Beaufort values, or if the camera is to be submerged underwater (to see the waterline). \| ![](hq_waterline_0.png) \| ![](hq_waterline_1.png) \| \|---\|---\| \| *Underwater DOF disabled* \| *Underwater DOF enabled* \| | ![](hq_waterline_0.png) | ![](hq_waterline_1.png) | *Underwater DOF disabled* | *Underwater DOF enabled* |
|---|---|---|---|---|---|
| ![](hq_waterline_0.png) | ![](hq_waterline_1.png) |  |  |  |  |
| *Underwater DOF disabled* | *Underwater DOF enabled* |  |  |  |  |
| Underwater DOF Distance | Focal distance for the underwater DOF effect. |  |  |  |  |
| Depth LUT | LUT texture that shows the color of the bottom. Depending on the depth, the engine chooses the color of the water and multiplies it by the depth LUT texture. This generated LUT shows how deep the photon goes through water until completely scattered. The texture is 4-channeled: - *RGB* values store color. - *A* value is used to create "transparent" water near the shore. In other words, it defines the fog density. |  |  |  |  |
| Fog Color | Underwater fog color. The Sun and Environment lighting affect this parameter to create the final underwater fog color. \| ![](fog_color_0.png) \| ![](fog_color_1.png) \| \|---\|---\| \| ![](fog_color_param_0.png) \| ![](fog_color_param_1.png) \| | ![](fog_color_0.png) | ![](fog_color_1.png) | ![](fog_color_param_0.png) | ![](fog_color_param_1.png) |
| ![](fog_color_0.png) | ![](fog_color_1.png) |  |  |  |  |
| ![](fog_color_param_0.png) | ![](fog_color_param_1.png) |  |  |  |  |
| Fog Transparency | Transparency of the underwater fog. The higher the value, the more transparent the underwater fog is. \| ![](fog_transparency_0.png) \| ![](fog_transparency_1.png) \| \|---\|---\| \| ![](fog_transparency_param_0.png) \| ![](fog_transparency_param_1.png) \| | ![](fog_transparency_0.png) | ![](fog_transparency_1.png) | ![](fog_transparency_param_0.png) | ![](fog_transparency_param_1.png) |
| ![](fog_transparency_0.png) | ![](fog_transparency_1.png) |  |  |  |  |
| ![](fog_transparency_param_0.png) | ![](fog_transparency_param_1.png) |  |  |  |  |
| Fog Lighting Depth | Distance from the water surface, in units, up to which the light affects the underwater color. \| ![](fog_depth_0.png) \| ![](fog_depth_1.png) \| \|---\|---\| \| ![](fog_depth_param_0.png) \| ![](fog_depth_param_1.png) \| | ![](fog_depth_0.png) | ![](fog_depth_1.png) | ![](fog_depth_param_0.png) | ![](fog_depth_param_1.png) |
| ![](fog_depth_0.png) | ![](fog_depth_1.png) |  |  |  |  |
| ![](fog_depth_param_0.png) | ![](fog_depth_param_1.png) |  |  |  |  |
| Lighting Offset | Height offset for lighting. |  |  |  |  |
| Fog Environment Lighting | Degree of impact of the environment lighting on the final underwater color. |  |  |  |  |
| Fog Sun Lighting | Degree of impact of the sun lighting on the final underwater color. |  |  |  |  |
| Shafts Intensity | Intensity of the underwater sun shafts. |  |  |  |  |
| Waterline Size | Size of the borderline between the overwater and underwater environments. > **Notice:** You may need to adjust the [quality of waterline calculation](../../../editor2/settings/render_settings/water_ssr/index.md#waterline_accuracy) in case of medium and high Beaufort values, or if the camera is to be submerged underwater (to see the waterline). \| ![](waterline_size_0.png) \| ![](waterline_size_1.png) \| \|---\|---\| \| ![](waterline_size_param_0.png) \| ![](waterline_size_param_1.png) \| | ![](waterline_size_0.png) | ![](waterline_size_1.png) | ![](waterline_size_param_0.png) | ![](waterline_size_param_1.png) |
| ![](waterline_size_0.png) | ![](waterline_size_1.png) |  |  |  |  |
| ![](waterline_size_param_0.png) | ![](waterline_size_param_1.png) |  |  |  |  |


### Planar Reflection


![](planar_reflection.png)


Parameters defining planar reflections:


| Planar Reflection | Enables the use of planar reflections on the water surface instead of SSR. It is better to use this option for undisturbed water (0-2 Beaufort). |
|---|---|
| Map Size | Size of the planar reflection map. The higher the value, the better the quality. |
| Viewport Mask | The [viewport mask](../../../principles/bit_masking/index.md#viewport) of the reflection camera. A surface has its reflection rendered, if its viewport mask and its material's viewport mask match this mask. |
| Distance | Distance from the reflection viewport camera to the reflected object. This distance sums up to the distance from the camera to the reflective surface plus the distance from object to reflective surface. |
| Pivot Offset | Position of the reflection pivot point. |


### Reflection


![](reflection.png)


Parameters defining environment reflections:


| Roughness | Environment reflection roughness of the water surface. The value is used for shading of the water surface: the higher the value, the more blurred environment reflections are. [Planar reflections](#planar_reflection_toggle) are blurred and attenuated by this value as well. > **Notice:** In the [Beauforts mode](#beauforts_mode), this parameter is set by the Beaufort preset automatically and is not available for editing. \| ![](env_reflection_0.png) \| ![](env_reflection_1.png) \| \|---\|---\| \| ![](env_reflection_param_0.png) \| ![](env_reflection_param_1.png) \| | ![](env_reflection_0.png) | ![](env_reflection_1.png) | ![](env_reflection_param_0.png) | ![](env_reflection_param_1.png) |
|---|---|---|---|---|---|
| ![](env_reflection_0.png) | ![](env_reflection_1.png) |  |  |  |  |
| ![](env_reflection_param_0.png) | ![](env_reflection_param_1.png) |  |  |  |  |
| Occlusion | \| The occlusion factor for environment reflections on parts of the water surface with negative normals. Using this parameter enables simulation of reflection of waves on the water surface removing too bright areas on waves close to the horizon. - By the minimum value of 0, no occlusion is performed for reflections of waves, no matter what normals the water surface has. - By the higher values, occlusion is performed for reflections on parts of the water surface with negative normals that have a certain [slope](#reflection_occlusion_slope). The higher the value, the less intensive reflections are on the surface parts with negative normals. \| \|---\| \| ![](reflection_occlusion_0.png) ![](reflection_occlusion_1.png) \| | The occlusion factor for environment reflections on parts of the water surface with negative normals. Using this parameter enables simulation of reflection of waves on the water surface removing too bright areas on waves close to the horizon. - By the minimum value of 0, no occlusion is performed for reflections of waves, no matter what normals the water surface has. - By the higher values, occlusion is performed for reflections on parts of the water surface with negative normals that have a certain [slope](#reflection_occlusion_slope). The higher the value, the less intensive reflections are on the surface parts with negative normals. | ![](reflection_occlusion_0.png) ![](reflection_occlusion_1.png) |  |  |
| The occlusion factor for environment reflections on parts of the water surface with negative normals. Using this parameter enables simulation of reflection of waves on the water surface removing too bright areas on waves close to the horizon. - By the minimum value of 0, no occlusion is performed for reflections of waves, no matter what normals the water surface has. - By the higher values, occlusion is performed for reflections on parts of the water surface with negative normals that have a certain [slope](#reflection_occlusion_slope). The higher the value, the less intensive reflections are on the surface parts with negative normals. |  |  |  |  |  |
| ![](reflection_occlusion_0.png) ![](reflection_occlusion_1.png) |  |  |  |  |  |
| Occlusion Slope | Slope of negative normals of the water surface, at which occlusion is performed for wave reflections. |  |  |  |  |


### Other


![](other.png)


Additional parameters:


| Refraction Scale | Scale of the water refraction. \| ![](refraction_scale_0.png) \| ![](refraction_scale_1.png) \| \|---\|---\| \| ![](refraction_scale_param_0.png) \| ![](refraction_scale_param_1.png) \| | ![](refraction_scale_0.png) | ![](refraction_scale_1.png) | ![](refraction_scale_param_0.png) | ![](refraction_scale_param_1.png) |
|---|---|---|---|---|---|
| ![](refraction_scale_0.png) | ![](refraction_scale_1.png) |  |  |  |  |
| ![](refraction_scale_param_0.png) | ![](refraction_scale_param_1.png) |  |  |  |  |
| Diffuse Distortion | Distortion of [decals](../../../objects/decals/index.md) projected onto water. |  |  |  |  |
| Soft Intersection | Soft intersection of water with the shoreline and surfaces of objects. |  |  |  |  |


### Caustics


![](caustics.png)


Parameters defining caustics:


| Caustics | Enables the effect of light rays refraction by the water surface. \| ![](caustics_0.png) \| ![](caustics_1.png) \| \|---\|---\| \| *Caustics disabled* \| *Caustics enabled* \| | ![](caustics_0.png) | ![](caustics_1.png) | *Caustics disabled* | *Caustics enabled* |
|---|---|---|---|---|---|
| ![](caustics_0.png) | ![](caustics_1.png) |  |  |  |  |
| *Caustics disabled* | *Caustics enabled* |  |  |  |  |
| Caustics Distortion | Removes pixelation and makes caustics look smoother. When smoothing is not required, you can disable this option to gain performance. \| ![](caustics_distortion_0.png) \| ![](caustics_distortion_1.png) \| \|---\|---\| \| *Caustics Distortion disabled* \| *Caustics Distortion enabled* \| | ![](caustics_distortion_0.png) | ![](caustics_distortion_1.png) | *Caustics Distortion disabled* | *Caustics Distortion enabled* |
| ![](caustics_distortion_0.png) | ![](caustics_distortion_1.png) |  |  |  |  |
| *Caustics Distortion disabled* | *Caustics Distortion enabled* |  |  |  |  |
| Texture | The 3D **Caustic** texture determines the pattern of light rays refracted by the water surface. The texture is 1-channeled: - *R* value defines the caustics pattern. |  |  |  |  |
| UV Transform | UV Transform coordinates for the [caustic texture](#caustics_texture). \| ![](caustics_uv_0.png) \| ![](caustics_uv_1.png) \| \|---\|---\| \| ![](caustics_uv_param_0.png) \| ![](caustics_uv_param_1.png) \| | ![](caustics_uv_0.png) | ![](caustics_uv_1.png) | ![](caustics_uv_param_0.png) | ![](caustics_uv_param_1.png) |
| ![](caustics_uv_0.png) | ![](caustics_uv_1.png) |  |  |  |  |
| ![](caustics_uv_param_0.png) | ![](caustics_uv_param_1.png) |  |  |  |  |
| Distance Fade | Distance from the water surface downwards, at which light shapes fade, in units. \| ![](caustics_distance_fade_0.png) \| ![](caustics_distance_fade_1.png) \| \|---\|---\| \| *Distance Fade: 20.0* \| *Distance Fade: 40.0* \| | ![](caustics_distance_fade_0.png) | ![](caustics_distance_fade_1.png) | *Distance Fade: 20.0* | *Distance Fade: 40.0* |
| ![](caustics_distance_fade_0.png) | ![](caustics_distance_fade_1.png) |  |  |  |  |
| *Distance Fade: 20.0* | *Distance Fade: 40.0* |  |  |  |  |
| Animation Speed | Movement speed of the light patterns. |  |  |  |  |
| Brightness | Brightness of the light shapes. |  |  |  |  |


### Field Height


![](field_height.png)


Parameters concerning [FieldHeight](../../../objects/effects/fields/field_height/index.md) object:


| Foam Contrast | Contrast of the foam generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in *Global Water*. |
|---|---|
| Foam Intensity | Intensity of the foam generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in *Global Water*. |
| Steepness | Sharpness of the crests for the waves generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in *Global Water*. |


### Field Shoreline


![](field_shoreline.png)


Parameters concerning [FieldShoreline](../../../objects/effects/fields/field_shoreline/index.md) object:


| High Precision | Enables improved interpolation between the adjacent pixels of the shoreline texture to reduce stepping artifacts. This can be noticed when looking at the waterline separating overwater and underwater. > **Notice:** This state should be used only when [geometry](#fieldshoreline_geometry) and/or [normal](#fieldshoreline_normal) options are enabled. You may also need to adjust the [quality of waterline calculation](../../../editor2/settings/render_settings/water_ssr/index.md#waterline_accuracy) in case of medium and high Beaufort values, or if the camera is to be submerged underwater (to see the waterline). \| ![](high_precision_0.png) \| ![](high_precision_1.png) \| \|---\|---\| \| *High Precision disabled* \| *High Precision enabled* \| | ![](high_precision_0.png) | ![](high_precision_1.png) | *High Precision disabled* | *High Precision enabled* |
|---|---|---|---|---|---|
| ![](high_precision_0.png) | ![](high_precision_1.png) |  |  |  |  |
| *High Precision disabled* | *High Precision enabled* |  |  |  |  |
| Normal | Enables calculation of normals for geometry of shoreline waves. This option significantly reduces performance and can be used in cases, when really large waves are required. Enabling just the [geometry](#fieldshoreline_geometry) option to simulate distortion of the water surface by a shoreline wave is enough in most cases. |  |  |  |  |
| Geometry | Enables rendering of wave geometry for shoreline waves. If disabled, the water surface remains flat. Disabling this option in cases where wave geometry is hardly noticeable (e.g. a flight simulator) gives a performance gain. \| ![](geometry_0.png) \| ![](geometry_1.png) \| \|---\|---\| \| *Geometry option disabled* \| *Geometry option enabled* \| | ![](geometry_0.png) | ![](geometry_1.png) | *Geometry option disabled* | *Geometry option enabled* |
| ![](geometry_0.png) | ![](geometry_1.png) |  |  |  |  |
| *Geometry option disabled* | *Geometry option enabled* |  |  |  |  |
| Foam | Enables rendering of foam for shoreline zones. \| ![](foam_0.png) \| ![](foam_1.png) \| \|---\|---\| \| *Foam option disabled* \| *Foam option enabled* \| | ![](foam_0.png) | ![](foam_1.png) | *Foam option disabled* | *Foam option enabled* |
| ![](foam_0.png) | ![](foam_1.png) |  |  |  |  |
| *Foam option disabled* | *Foam option enabled* |  |  |  |  |
| Lut | Path to the LUT texture used for shoreline wetness effect. |  |  |  |  |
| Wave Speed | Speed of tidal waves. |  |  |  |  |
| Wave Tiling | Frequency of tidal waves. |  |  |  |  |
| Wave Exponent | Nonlinearity of tidal waves frequency and movement speed. |  |  |  |  |
| Front Exponent | Semi-transparency of the foam at an angle to the wind direction. Allows making the foam visible only on the windward side. |  |  |  |  |
| Wave Height | Height of oncoming tidal waves. |  |  |  |  |
| Wave Falloff | Visibility gradient of waves coming from sea to the shore. |  |  |  |  |
| Mask Tiling | Size of the foam procedural pattern used to reduce the foam tiling effect when seen from above. |  |  |  |  |
| Beaufort Falloff | Beaufort falloff value that provides height control of main geometry waves near the shoreline. |  |  |  |  |
| Foam Stretching | Width of the [Shoreline LUT texture](#fieldshoreline_lut) that creates a tidal wave. |  |  |  |  |
| Foam Intensity | Degree of foam intensity along the shoreline. |  |  |  |  |
| Foam Exponent | Visibility of the foam texture pattern. |  |  |  |  |


### Shoreline Wetness


![](shoreline_wetness.png)


Parameters defining the effect of wetness near the shoreline:


| Intensity | Intensity of the wetness effect along the shoreline. |
|---|---|
| Distance | Spread of the wetness area along the shoreline. |
| Offset | Offset of the wetness area from the water. |


### Auxiliary


![](auxiliary.png)


Auxiliary rendering pass parameters:


| Auxiliary | Enables the [auxiliary rendering pass](../../../principles/render/sequence/index.md#auxiliary). It can be used for custom post-effects, such as thermal vision, night vision, etc. |
|---|---|
| Color | Color that goes into the auxiliary buffer. *Alpha* is the blend factor. |


## Intersections and Fetch Requests


The *Global Water* object supports [intersection detection](../../../api/library/objects/class.objectwaterglobal_cpp.md#intersections), that can be used, for example, to simulate a splash at a point of contact of a projectile with water surface, as well as for many other purposes.


You can also [obtain water level (height) and normal orientation at a certain point](../../../api/library/objects/class.objectwaterglobal_cpp.md#fetch), for example, to ensure proper placement and orientation of a ship relatively to the water surface without engaging physics.


The *Global Water* object offers you a set of parameters to control accuracy of these operations for performance optimization, as different number of iterations may be required to provide an acceptable result depending on wave steepness and height differences on the water surface (various Beaufort levels). All these parameters are available via API and described in the *[ObjectWaterGlobal](../../../api/library/objects/class.objectwaterglobal_cpp.md)* class article.


Check out the sample in **C++ Samples** and in **C# Component Samples** included in the SDK and demonstrating the influence of the *Steepness Quality, Amplitude Threshold*, and *Precision* parameters on the accuracy of fetch and intersection requests for the *Global Water* object at various Beaufort levels.
