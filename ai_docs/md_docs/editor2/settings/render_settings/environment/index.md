# Environment


This section describes settings that control environment of the scene (scattering, haze, etc.). You can create some presets and smoothly combine them by specifying the intensity of a preset thus producing new environments.


![](environment.png)

*Environment Settings*


| Enabled | The value indicating if rendering of environment of the scene is enabled. **enabled** by default. `Console access:render_environment` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment)) |  |  |
|---|---|---|---|
| Correct Roughness | The GGX Mipmap quality mode for environment reflections on rough surfaces. Quality modes differ in the number of rays used to create a reflection on a rough surface. One of the following values: - *Low* - low quality (by default) - *Medium* - medium quality - *High* - high quality - *Ultra* - ultra quality `Console access:render_environment_ggx_mipmaps_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment_ggx_mipmaps_quality)) |  |  |
| Background Color | The [background color](../../../../editor2/settings/render_settings/environment/index.md#background_color) vector. The Alpha channel of this color sets background transparency: lower alpha channel values produce darker background color. This parameter allows creating colored transparent background instead of rendering an environment cubemap. However, if the environment cubemap is rendered, the background color will always be rendered over the environment. `Console access:render_background_color` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_background_color)) \| ![Black background color](../background0.jpg) *Default Background Color* \| ![Blue background color](../background1.jpg) *Blue Background* \| \|---\|---\| | ![Black background color](../background0.jpg) *Default Background Color* | ![Blue background color](../background1.jpg) *Blue Background* |
| ![Black background color](../background0.jpg) *Default Background Color* | ![Blue background color](../background1.jpg) *Blue Background* |  |  |


## Environment Presets


The environment cubemap is tweaked in the *Rendering* panel -> *Environment* tab. The scattering can have up to 3 separate settings presets that can be blended by the Preset intensity scroll bars.


![](preset_intensity.png)


Presets work as layers: the first preset will overlay the zero one, the second will overlay the first and the zero ones. For example, you can set the zero preset for the clean and clear sky, set the first preset for the cloudy sky and lerp them smoothly.


## Screen-Space Shadow Shafts Settings


This set of parameters is used to configure rendering of volumetric Screen-Space Shadow Shafts. Shadow shafts can be rendered for both the Sun and the Moon.


![](ssss_settings.png)


| Mode | The rendering mode for volumetric [screen-space shadow shafts](../../../../editor2/settings/render_settings/environment/index.md#ssss). Shadow shafts (aka light shafts) can be generated in screen space for the Sun and the Moon to simulate the real world effect of crepuscular rays, or atmospheric shadowing of atmospheric in-scattering. These rays add depth and realism to any scene. > **Notice:** - This effect works for opaque geometry only. > - It is recommended to use Screen-Space Shadow Shafts with relatively thick haze for visual consistency. > - Disable this effect for indoor scenes as only world light sources are supported. One of the following values: - Disabled - Sun shadow shafts (by default) - Moon shadow shafts - Sun and Moon shadow shafts `Console access:render_screen_space_shadow_shafts_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_screen_space_shadow_shafts_mode)) |
|---|---|
| Quality | The [quality](../../../../editor2/settings/render_settings/environment/index.md#ssss_quality) of screen-space shadow shafts. Defines the number of steps to be used when generating the texture for this effect. *Lower* quality values may result in noticeable banding effect especially in case of long shadow shafts. *Medium* quality is usually enough, but you can increase it if shafts are long enough and banding effect becomes noticeable. One of the following values: - *Low* - low quality - *Medium* - medium quality (by default) - *High* - high quality - *Ultra* - ultra quality `Console access:render_screen_space_shadow_shafts_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_screen_space_shadow_shafts_quality)) |
| Resolution | The [resolution of the texture](../../../../editor2/settings/render_settings/environment/index.md#ssss_resolution) to which screen-space shadows are rendered. One of the following values: - *Quarter* - quarter resolution - *Half* - half resolution (by default) - *Full* - full resolution `Console access:render_screen_space_shadow_shafts_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_screen_space_shadow_shafts_resolution)) |
| Shaft Length | The length of volumetric [screen-space shadow shafts](../../../../editor2/settings/render_settings/environment/index.md#ssss). Range of values: **[0.0f, 100.0f]**. The default value is : **3.0f**. `Console access:render_screen_space_shadow_shafts_length` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_screen_space_shadow_shafts_length)) |


## Scattering LUT Settings


All the presets settings are identical. The scattering versatility is achieved mostly because of the scattering LUT textures.


![](scattering_lut.jpg)


### Base


A [2D](../../../../editor2/assets_workflow/texture_import.md#image_type) texture defining the base color of the sky, clouds, and haze.


![Base LUT Texture](base.jpg)

*Base LUT Texture*


The texture consists of 6 columns, each for a specific reason:


1. Color of the sky on the side opposite to the light source (to provide a possibility of rendering a shadow cast by a planet, if required)
2. General sky color
3. Color of clouds on the side opposite to the light source (to provide a possibility of rendering a shadow cast by a planet, if required)
4. General clouds color
5. Color of haze on the side opposite to the light source (to provide a possibility of rendering a shadow cast by a planet, if required)
6. General haze color


The use of texture also depends on the *[Scattering](../../../../objects/lights/world/index.md#light_settings)* mode of the active *World* light source. For the *Sun* scattering mode, the left side of each column is used:


- Left to right: the position of the Sun above the surface (time of day).
- Top to bottom: the gradient of the Sun.


For the *Moon* scattering mode, the right side of each column is used.


![](lut_base.gif)

*Sampling the Base LUT texture for the general sky color based on the sun angle*


If the default LUT doesn't meet the visual requirements of your project, you can **customize it** using a third-party image editor to achieve the desired effect by selectively adjusting specific areas of the LUT texture. The image below illustrates how the base LUT texture was edited to produce a clearer and more saturated sky with reduced haze:


![](lut_customized.png)


In the upper sections of the texture, blue tones were intensified for a deeper sky color (columns 1 and 2) and less intense haze (columns 5 and 6). Mid-to-lower regions were shifted downward to reduce grayish haze near the horizon.


![](base_before.png) ![](base_after.png)


> **Warning:** We do not recommend repainting or restructuring the LUT texture since it can result in incorrect atmospheric rendering, visible seams, or unnatural transitions. Instead, focus on adjusting color balance, saturation, brightness, or contrast only.


**To Apply the Customized LUTs**


1. Extract the original `base.tif` LUT texture from your project. For example, you can do it the following way: in the *Environment -> Scattering LUT* settings window, click the magnifying glass icon next to the *Base* slot to locate the file and copy it to the `/data` folder of your project in the Asset Browser. ![](lut_base_edit.png)
2. Then using SDK Browser click *Open Folder* in your project's card and open the `base.tif` file in your preferred third-party image editor. Make the desired adjustments and save the file in the same `.tif` format. The file name can be different if needed.
3. Import the customized LUT texture file into your project via the Asset Browser.
4. Go to *Windows -> Settings -> Environment -> Scattering LUT* and assign the texture to the *Base* slot.


### Mie


A [2D](../../../../editor2/assets_workflow/texture_import.md#image_type) texture for setting the Mie light (the color of the light around the light source) to simulate interaction of light with water, dust and other particles in the atmosphere.


![Mie LUT Texture](mie.jpg)

*Mie LUT Texture*


The texture consists of 3 columns, each for a specific reason:


1. Color of the sky around the light source
2. Color of clouds around the light source
3. Color of haze around the light source


The top square of each column is for the *Sun*, the bottom one � for the *Moon* [scattering](../../../../objects/lights/world/index.md#light_settings) mode.


The texture (each column) is sampled vertically according to the time of day along the horizontal axis.


![](lut_mie.gif)

*Sampling the Mie LUT texture (sky color) based on the sun angle*


The Alpha channel stores the mask for the [celestial body texture](#celestial_bodies).


![Alpha Channel of Mie LUT Texture](mie_alpha.jpg)

*Alpha Channel of Mie LUT Texture*


To simulate dense cloudiness without a visible celestial body (the Sun or the Moon), paint the Alpha channel black.


![](lut_mie_alpha_0.png) ![](lut_mie_alpha_1.png)


*The result of using different masks in the Alpha channel*


### Light Color


A [2D](../../../../editor2/assets_workflow/texture_import.md#image_type) texture defining the color of *LightWorld* depending on the time of day.


![Light Color LUT Texture](light_color.jpg)

*Light Color LUT Texture*


The texture is split vertically (top for the *Sun* and bottom for the *Moon* [scattering](../../../../objects/lights/world/index.md#light_settings) mode) and consists of 4 columns, each for a specific reason:


1. Color to be used for objects in the world. The values in this column should differ only vertically, horizontally the value should be the same.
2. Color to be used for clouds on the side opposite to the light source (to provide a possibility of rendering a shadow cast by a planet, if required)
3. Color to be used for clouds
4. Color to be used for clouds around the light source


Sampling of the color for objects based on the sun angle (the black texture is used for the Base and Mie LUTs for clarity):


![](lut_lightcolor.gif)


## Environment Settings


Environment settings are required for creating environment by means of panorama (cubemap).


![](environment_settings.png)


| Texture | A [cube map](../../../../editor2/assets_workflow/texture_import.md#image_type) defining the environment image; for example, HDRI environment map or skydome. You can download suitable images from such websites as [polyhaven.com](https://polyhaven.com/). > **Notice:** We recommend using an *HDR* or uncompressed *EXR* image for better shading results. Note that lossy compression types **B44, B44A, PIX24**, which the *EXR* format may use, are **not supported**. |
|---|---|
| Color | The environment color multiplier, where alpha defines the visibility of a cubemap above scattering. This parameter is required when you need to display a sky with a photo texture and dynamic gradients at the same time. |
| Blur | A value defining blurring of the environment. |
| Rotation X | The rotation angle of the environment cubemap around the X axis. |
| Rotation Y | The rotation angle of the environment cubemap around the Y axis. |
| Rotation Z | The rotation angle of the environment cubemap around the Z axis. |
| Blend Mode | The blending mode for the environment cubemap. One of the following values: - alpha blend (by default) - additive blend - multiply - overlay `Console access:render_environment_cubemap_blend` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment_cubemap_blend)) |


## Haze Settings


![](pbhaze.png)

*Physically based haze*


This group of parameters set the atmosphere haze. It automatically uses the color from the scattering LUTs, so objects smoothly fade into the distance without any artifacts.


![](haze.png)

*Haze Settings*


> **Notice:** In some cases, the configuration of the default environment presets is not suitable for dense fog simulation and might require some [adjustment](../../../../editor2/lighting/environment.md#haze).


| Mode | The [mode](../../../../editor2/settings/render_settings/environment/index.md#haze) for the haze effect. - If **Disabled**, no haze is applied. - The **Solid** mode uses the solid color from the *[Color](../../../../editor2/settings/render_settings/environment/index.md#haze_color)* parameter. - The **Scattering** mode uses the color from the sky LUTs is blended with the *[Color](../../../../editor2/settings/render_settings/environment/index.md#haze_color)* parameter. This value is recommended for better realism: objects will smoothly fade into the distance. Option **#3** is selected by default (see above). `Console access:render_environment_haze` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment_haze)) \| ![](haze_disabled.jpg) ![](haze_solid.jpg) \| ![](haze_disabled.jpg) ![](haze_scattering.jpg) \| \|---\|---\| | ![](haze_disabled.jpg) ![](haze_solid.jpg) | ![](haze_disabled.jpg) ![](haze_scattering.jpg) |
|---|---|---|---|
| ![](haze_disabled.jpg) ![](haze_solid.jpg) | ![](haze_disabled.jpg) ![](haze_scattering.jpg) |  |  |
| Gradient Mode | The environment haze gradient mode. By using this option, you can make the haze look more realistic for a specific distance range. - Short Distance Range - better suitable for near-surface haze - Long Distance Range - better suitable for hazy mountains - Physically Based - for physically based haze simulation Option **#1** is selected by default (see above). `Console access:render_environment_haze_gradient` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment_haze_gradient)) |  |  |
| Color | The color of the haze. This value can be specified for both the *Solid* and *Scattering* haze modes: in the first case, the color will be used as is, in the second case, the color will be blended with the color from the sky LUTs. \| ![](haze_solid_color_0.jpg) ![](haze_solid_color_1.jpg) \| ![](haze_scattering_color_0.jpg) ![](haze_scattering_color_1.jpg) \| \|---\|---\| | ![](haze_solid_color_0.jpg) ![](haze_solid_color_1.jpg) | ![](haze_scattering_color_0.jpg) ![](haze_scattering_color_1.jpg) |
| ![](haze_solid_color_0.jpg) ![](haze_solid_color_1.jpg) | ![](haze_scattering_color_0.jpg) ![](haze_scattering_color_1.jpg) |  |  |
| Max Distance | The distance starting at which the haze becomes completely solid, so nothing will be seen behind. For large terrains it is recommended to set this parameter equal to your camera's *[Far](../../../../editor2/camera_settings/index.md#far)* parameter. This is required for distant objects to fade into the distance instead of being cut sharply. |  |  |
| Density | The density of the haze. |  |  |
| Mie Intensity | Minimum Mie intensity value for geometry-occluded areas. This value specifies the fraction of Mie intensity visible when the surface is viewed from straight on. Setting this value to 1 disables the Fresnel effect. You can use this parameter together with **[Mie Fresnel Intensity](#haze_mie_fresnel_intensity)** and **[Mie Fresnel Power](#haze_mie_fresnel_power)** to control light occlusion from *[World](../../../../objects/lights/world/index.md)* light sources. Works for both, opaque and transparent objects. |  |  |
| Mie Front Side Intensity | Falloff of the Fresnel effect for Mie intensity. This parameter enables you to control occlusion of light from a *[World](../../../../objects/lights/world/index.md)* light source by the geometry. |  |  |
| Mie Fresnel Power | The power of the Fresnel effect for Mie visibility. *Higher* values will tighten up the areas affected, while *lower* ones will allow more areas to be affected by the Fresnel effect. |  |  |


### Physically Based Haze Calculation Parameters


This group of parameters is used for physically based calculation of the haze gradient.


In most cases there is no need to adjust default haze settings here. However, if you want to change haze color (e.g., make it a bit more bluish) we recommend you doing it via the [**Color**](#haze_color) multiplier above instead of tweaking **Color Saturation** for sunlight and ambient lighting, as this may cause problems with colors at sunset.


![](haze_physically_based.png)

*Physically Based Haze Calculation Parameters*


| Half Visibility Distance | Distance at which the visibility comprises 50%. There is no zero-visibility in the real world, so the half-visibility boundary is used to adjust haze distance. |
|---|---|
| Half Faloff Height | Height of the haze density gradient. The *higher* the value, the *longer* the haze desity reduces as the height grows, making the transition between the clear sky and haze smoother. |
| Start Height | Reference height value for the two parameters above (**Half Visibility Distance** and **Half Faloff Height**). |
| Ambient Light Intensity | Intensity of the impact of ambient lighting on haze (how much ambient lighting affects the haze). |
| Ambient Color Saturation | Intensity of the ambient color's contribution to the haze (how much the haze color is affected). |
| Sun Light Intensity | Intensity of the impact of the sunlight on haze (how much the sunlight affects the haze). |
| Sun Color Saturation | Intensity of the sunlight color's contribution to the haze (how much the haze color is affected). > **Notice:** "Sunlight color" here does not simply mean the color multiplier of the *[WorldLight](../../../../objects/lights/world/index.md)* source, but rather the *[Light Color](#light_lut)* in the *Scattering LUT* section above. |


### Screen-Space Haze Global Illumination


Screen-Space Haze Global Illumination (SSHGI) is a screen-space effect ensuring consistency of haze color with the current color of Global Illumination. Available for *Physically Based* [haze gradient mode](#haze_gradient_mode) only.


![](sshgi.png)


| Screen-Space Haze Global Illumination | Toggles the value indicating if the Screen-Space Haze Global Illumination effect is enabled. |
|---|---|
| Colorization Threshold | The treshold value for scene depth used when setting haze color for the SSHGI effect in "information lost" areas on the screen. - 0 - haze color is defined only by surfaces currently visible on the screen. - 1 - haze color is defined by surfaces everywhere, even in "information lost" areas. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_environment_haze_colorization_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment_haze_colorization_threshold)) |
| Colorization Intensity | The colorization intensity value that defines haze color in "information lost" areas on the screen. - 0 - haze in "information lost" areas will have the initial color (same as it would be without SSHGI). - 1 - haze in "information lost" areas will have the less bright color among the two, initial color and haze color with SSHGI correction. This parameter is ignored when *[Colorization Threshold](#render_environment_haze_colorization_threshold)* is set to 1, as there will be no "information lost" areas not covered by SSHGI. Range of values: **[0.0f, 1.0f]**. The default value is : **0.95f**. `Console access:render_environment_haze_colorization_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment_haze_colorization_intensity)) |
| Distance Min | The minimum distance at which Screen Space Haze GI calculations start to take effect. Range of values: **[0.0f, inf]**. The default value is : **98000.0f**. `Console access:render_environment_haze_screen_space_global_illumination_distance_min` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment_haze_screen_space_global_illumination_distance_min)) |
| Distance Max | The maximum distance within which Screen Space Haze GI calculations are performed. Range of values: **[0.0f, inf]**. The default value is : **100000.0f**. `Console access:render_environment_haze_screen_space_global_illumination_distance_max` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment_haze_screen_space_global_illumination_distance_max)) |
| Temporal Filter | The value indicating if temporal filtering for the Screen-Space Haze Global Illumination effect is enabled. **enabled** by default. `Console access:render_environment_haze_temporal_filter` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_environment_haze_temporal_filter)) |


## Intensity Settings


> **Notice:** It is recommended to use the default values of the parameters below (if possible) to keep the image realistic.


![](intensity.png)

*Intensity Settings*


| Ambient | Intensity of the environment ambient lighting for the given preset. **0** value means no environment ambient lighting for the given preset. The higher the value, the more ambient lighting affects environment. The value can be greater than 1.0 (useful for some dark scenes). ![](env_intensity_ambient_0.png) ![](env_intensity_default.png) |
|---|---|
| Reflection | Intensity of the environment reflection for the given preset. **0** value means no environment reflection for the given preset. ![](env_intensity_reflection_0.png) ![](env_intensity_default.png) |
| Sky | Intensity of the environment sky for the given preset. **0** value means no environment sky for the given preset. If, for example, the sky looks too dark in contrast with lighting from it, you should check exposure and tone mapping settings before changing the environment intensity. ![](env_intensity_sky_0.png) ![](env_intensity_default.png) |


## Celestial Bodies Settings


This group of parameters allows setting up the notable celestial bodies: the ***Sun*** and the ***Moon***. By using these parameters, you can set the Sun and the Moon by using textures, adjust its intensity and color multipliers, specify the angular size of the celestial bodies. By default, values of the parameters are set for an observer on the Earth.


| Sun | A texture that sets the Sun in the sky. On the picture below, the *[Sun Size](#sun_size)* is increased to demonstrate how the textures are applied: ![](sun_texture_0.jpg) ![](sun_texture_1.jpg) The texture may also be used to imitate the extremely bright area around the light source. |  |  |  |  |
|---|---|---|---|---|---|
| Moon | A texture that sets the Moon in the sky. On the picture below, *[Moon Size](#moon_size)* and *[Moon Intensity](#moon_intensity)* are increased to demonstrate how the textures are applied: ![](moon_texture_0.jpg) ![](moon_texture_1.jpg) The texture may also be used to imitate the extremely bright area around the light source. |  |  |  |  |
| Sun Color | Color multiplier for the Sun texture in the RGBA format. By default, the color is white. \| ![](sun_color_0.jpg) \| ![](sun_color_1.jpg) \| \|---\|---\| \| ![](sun_green.jpg) \| ![](sun_red.jpg) \| | ![](sun_color_0.jpg) | ![](sun_color_1.jpg) | ![](sun_green.jpg) | ![](sun_red.jpg) |
| ![](sun_color_0.jpg) | ![](sun_color_1.jpg) |  |  |  |  |
| ![](sun_green.jpg) | ![](sun_red.jpg) |  |  |  |  |
| Moon Color | Color multiplier for the Moon texture in the RGBA format. By default, the color is white. \| ![](moon_color_0.jpg) \| ![](moon_color_1.jpg) \| \|---\|---\| \| ![](moon_yellow.jpg) \| ![](moon_blue.jpg) \| | ![](moon_color_0.jpg) | ![](moon_color_1.jpg) | ![](moon_yellow.jpg) | ![](moon_blue.jpg) |
| ![](moon_color_0.jpg) | ![](moon_color_1.jpg) |  |  |  |  |
| ![](moon_yellow.jpg) | ![](moon_blue.jpg) |  |  |  |  |
| Sun Size | Angular size of the Sun in degrees. The value is set for an observer on the Earth. By default, the size of the Sun is 0.5 degrees as seen from the Earth. |  |  |  |  |
| Moon Size | Angular size of the Moon in degrees. The value is set for an observer on the Earth. By default, the size of the Moon is 0.5 degrees as seen from the Earth. |  |  |  |  |
| Sun Intensity | Intensity multiplier for the Sun texture. It allows increasing/reducing brightness of the Sun. ![](sun_intensity_0.jpg) ![](sun_intensity_1.jpg) |  |  |  |  |
| Moon Intensity | Intensity multiplier for the Moon texture. It allows increasing/reducing brightness of the Moon. ![](moon_intensity_0.jpg) ![](moon_intensity_1.jpg) |  |  |  |  |
