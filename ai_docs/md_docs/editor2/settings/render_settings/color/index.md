# Color Correction


This section describes settings for color correction of the scene.


![](scene_color.png)

*Scene Color Settings*


## Local Tonemapper


Local tone mapping uses a spatially varying mapping function determined by the neighborhood of a pixel, which allows an increase in the local contrast and the visibility of some details of an image. The local tonemapper enables the generation of a mask based on the entire image, providing more pleasing results because human vision is more sensitive to local contrast.


![](local_tonemapper_settings.png)

*Local Tonemapper Settings*


| Local Tonemapper | The value indicating if the local tonemapper is enabled. **disabled** by default. `Console access:render_local_tonemapper` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper)) |
|---|---|
| Debug | The value indicating whether the debug mode for the local tonemapper is enabled. **disabled** by default. `Console access:render_local_tonemapper_debug` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_debug)) |
| Blur Resolution | The resolution of the blur applied during the tone mapping process. > **Notice:** It is recommended to use the *Half* resolution in conjunction with the *[Blur Upscale](#LocalTonemapperBlurUpscale)* mode enabled. One of the following values: - *Quarter* - quarter resolution - *Half* - half resolution - *Full* - full resolution (by default) `Console access:render_local_tonemapper_blur_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_blur_resolution)) |
| Blur Upscale | The value indicating whether upscaling the blurred image from the *Quarter* or *Half* resolution to the *Full* one is enabled. **disabled** by default. `Console access:render_local_tonemapper_blur_upscale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_blur_upscale)) |
| Blur Upscale Kernel Size | The size of the kernel used for upscaling the blurred image. The higher the value the better the upscaling quality, but the lower the performance. It is recommended to set the kernel size as follows: - *3x3* for the *Half* resolution. - *5x5* for the *Quarter* resolution. Option **#1** is selected by default (see above). `Console access:render_local_tonemapper_blur_upscale_kernel_size` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_blur_upscale_kernel_size)) |
| Blur Iterations | The number of blur iterations applied to the screen texture, which is used to define bright and dark portions of the screen. A higher number of iterations increases the blur radius and reduces halo artifacts around objects, but may affect performance. Range of values: **[0, 10]**. The default value is : **5**. `Console access:render_local_tonemapper_num_blur_iterations` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_num_blur_iterations)) |
| Tonemapping Intensity | The intensity of the local tonemapping effect. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_local_tonemapper_tonemapping_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_tonemapping_intensity)) |
| Effect On Dark Areas | The extent of applying the local tonemapping effect on dark areas. Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**. `Console access:render_local_tonemapper_effect_on_dark_areas` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_effect_on_dark_areas)) |
| Effect On Dark Areas Gamma | The gamma correction value for dark areas. Specifying values greater than 1 decreases the local tone mapping effect in extremely dark areas. Range of values: **[0.0f, inf]**. The default value is : **5.0f**. `Console access:render_local_tonemapper_effect_on_dark_areas_gamma` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_effect_on_dark_areas_gamma)) |
| Target Middle Gray | The target middle gray value for tonemapping. Range of values: **[0.0f, 1.0f]**. The default value is : **0.4f**. `Console access:render_local_tonemapper_target_middle_gray` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_target_middle_gray)) |
| Luma Blurred Intensity | The intensity of blurring the luma values. It is recommended to keep the default value for this setting. With the value set to 0, a regular screen texture is used instead of a blurred screen texture. This might be required in a rare case of reducing the halo effect and increasing the tonemapping effect for small details. Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**. `Console access:render_local_tonemapper_luma_blurred_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_luma_blurred_intensity)) |
| Use Depth Difference | The value indicating whether considering of the depth difference between objects in the scene is enabled. Enabling this feature allows reducing halo artifacts around objects. However, we recommend using it only in exceptional cases, as it is a performance-costly operation. **disabled** by default. `Console access:render_local_tonemapper_depth_difference_enabled` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_depth_difference_enabled)) |
| Depth Threshold | The depth threshold value used to detect the areas affected by local tonemapping. A properly set value may help to reduce halo artifacts. Range of values: **[0.0f, 1.0f]**. The default value is : **0.9f**. `Console access:render_local_tonemapper_depth_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_depth_threshold)) |
| Use Color Difference | The value indicating whether considering of the image color rendered on the screen is enabled. Enabling this feature allows reducing halo artifacts on surfaces with sharp color transitions. For example, it can significantly improve the appearance of a distinct shadow from the sun on asphalt. **disabled** by default. `Console access:render_local_tonemapper_color_difference_enabled` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_color_difference_enabled)) |
| Color Difference Threshold | The threshold value that determines the extent to which color differences on the screen are considered. If you set the value to 1, the result will appear as if the [*Color Difference*](#LocalTonemapperColorDifferenceEnabled) feature is turned off. Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**. `Console access:render_local_tonemapper_color_difference_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_local_tonemapper_color_difference_threshold)) |


## Tonemapper


The tone mapping provides better image quality by remapping high dynamic range (HDR) colors into a range suitable for mediums with low dynamic range (LDR), like LCD or CRT screens. Its most common purpose is to make an image with a low dynamic range appear to have a higher range of colors providing a more dynamic and realistic effect. It lightens the darkest image regions and makes the lightest regions darker.


When using an HDR camera, always apply tonemapping, otherwise color intensity values exceeding 1 will be clamped at 1, altering the luminance balance of the scene.


![](filmic_settings.png)

*Tonemapper settings*


| Tonemapper | The value indicating if [tone mapping](../../../../editor2/settings/render_settings/color/index.md#tonemapper) is enabled. **enabled** by default. `Console access:render_tonemapper` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_tonemapper)) |
|---|---|
| Tonemapper Mode | The mode of [tone mapping](../../../../editor2/settings/render_settings/color/index.md#tonemapper). One of the following values: - Filmic - ACES (by default) - ACES with Reinhard - Reinhard - Reinhard Luma-Based `Console access:render_tonemapper_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_tonemapper_mode)) |


### Filmic


Parameters described below represent John Hable's artist-friendly tonemapping curve, which is constructed by using the following formula:


![](tonemapping_formula.gif)


- **A** � Shoulder Scale
- **B** � Linear Scale
- **C** � Linear Angle
- **D** � Toe Scale
- **E** � Toe Numerator
- **F** � Toe Denominator


![](tonemapping_curve.png)

*Tone Mapping Curve*


For more details about tone mapping curve construction see the article on [Filmic Tonemapping with Piecewise Power Curves](http://filmicworlds.com/blog/filmic-tonemapping-with-piecewise-power-curves/).


| Shoulder Scale | The [Shoulder Strength](../../../../editor2/settings/render_settings/color/index.md#shoulder_scale) tonemapping parameter value that is used to change bright values. Range of values: **[0.0f, 1.0f]**. The default value is : **0.2f**. `Console access:render_filmic_shoulder_scale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_filmic_shoulder_scale)) \| ![](shoulder_scale_0.png) *Shoulder Scale= 0.2 (by default)* \| ![](shoulder_scale_1.png) *Shoulder Scale= 1* \| \|---\|---\| | ![](shoulder_scale_0.png) *Shoulder Scale= 0.2 (by default)* | ![](shoulder_scale_1.png) *Shoulder Scale= 1* |
|---|---|---|---|
| ![](shoulder_scale_0.png) *Shoulder Scale= 0.2 (by default)* | ![](shoulder_scale_1.png) *Shoulder Scale= 1* |  |  |
| Linear Scale | The [Linear Strength](../../../../editor2/settings/render_settings/color/index.md#linear_scale) tone mapping parameter value that is used to change gray values. The Linear Scale controls the length of the [tone mapping curve](../../../../editor2/settings/render_settings/color/index.md#tonemapping_curve) linear part. Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_filmic_linear_scale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_filmic_linear_scale)) \| ![](linear_scale_0.png) *Linear Scale= 0.3 (by default)* \| ![](linear_scale_1.png) *Linear Scale= 1* \| \|---\|---\| | ![](linear_scale_0.png) *Linear Scale= 0.3 (by default)* | ![](linear_scale_1.png) *Linear Scale= 1* |
| ![](linear_scale_0.png) *Linear Scale= 0.3 (by default)* | ![](linear_scale_1.png) *Linear Scale= 1* |  |  |
| Linear Angle | The [Linear Angle](../../../../editor2/settings/render_settings/color/index.md#linear_angle) tone mapping parameter value. This parameter controls the slope of the linear part of the [tone mapping curve](../../../../editor2/settings/render_settings/color/index.md#tonemapping_curve). Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**. `Console access:render_filmic_linear_angle` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_filmic_linear_angle)) \| ![](linear_scale_0.png) *Linear Angle= 0.10 (by default)* \| ![](linear_angle_1.png) *Linear Angle= 1* \| \|---\|---\| | ![](linear_scale_0.png) *Linear Angle= 0.10 (by default)* | ![](linear_angle_1.png) *Linear Angle= 1* |
| ![](linear_scale_0.png) *Linear Angle= 0.10 (by default)* | ![](linear_angle_1.png) *Linear Angle= 1* |  |  |
| Toe Scale | The [Toe Scale](../../../../editor2/settings/render_settings/color/index.md#toe_scale) tonemapping parameter value that is used to change dark values. The Toe Scale controls the slope of the tone mapping curve toe (the area of underexposure). Range of values: **[0.0f, 1.0f]**. The default value is : **0.2f**. `Console access:render_filmic_toe_scale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_filmic_toe_scale)) \| ![](linear_scale_0.png) *Toe Scale= 0.20 (by default)* \| ![](toe_scale_1.png) *Toe Scale= 1* \| \|---\|---\| | ![](linear_scale_0.png) *Toe Scale= 0.20 (by default)* | ![](toe_scale_1.png) *Toe Scale= 1* |
| ![](linear_scale_0.png) *Toe Scale= 0.20 (by default)* | ![](toe_scale_1.png) *Toe Scale= 1* |  |  |
| Toe Numerator | The [Toe Numerator](../../../../editor2/settings/render_settings/color/index.md#toe_numerator) tonemapping parameter value. Range of values: **[0.0f, 1.0f]**. The default value is : **0.01f**. `Console access:render_filmic_toe_numerator` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_filmic_toe_numerator)) \| ![](linear_scale_0.png) *Toe Numerator= 0.01 (by default)* \| ![](toe_numerator_1.png) *Toe Numerator= 0.08* \| \|---\|---\| | ![](linear_scale_0.png) *Toe Numerator= 0.01 (by default)* | ![](toe_numerator_1.png) *Toe Numerator= 0.08* |
| ![](linear_scale_0.png) *Toe Numerator= 0.01 (by default)* | ![](toe_numerator_1.png) *Toe Numerator= 0.08* |  |  |
| Toe Denominator | The [Toe Denominator](../../../../editor2/settings/render_settings/color/index.md#toe_denominator) tonemapping parameter value. Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_filmic_toe_denominator` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_filmic_toe_denominator)) \| ![](linear_scale_0.png) *Toe Denominator= 0.3 (by default)* \| ![](toe_denominator_1.png) *Toe Denominator= 1* \| \|---\|---\| | ![](linear_scale_0.png) *Toe Denominator= 0.3 (by default)* | ![](toe_denominator_1.png) *Toe Denominator= 1* |
| ![](linear_scale_0.png) *Toe Denominator= 0.3 (by default)* | ![](toe_denominator_1.png) *Toe Denominator= 1* |  |  |
| White Level | The [Linear White Point](../../../../editor2/settings/render_settings/color/index.md#white_level) tonemapping parameter value, which is mapped as pure white in the resulting image. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_filmic_white_level` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_filmic_white_level)) \| ![](linear_scale_0.png) *White Level= 1.0 (by default)* \| ![](white_level_1.png) *White Level= 0.5* \| \|---\|---\| | ![](linear_scale_0.png) *White Level= 1.0 (by default)* | ![](white_level_1.png) *White Level= 0.5* |
| ![](linear_scale_0.png) *White Level= 1.0 (by default)* | ![](white_level_1.png) *White Level= 0.5* |  |  |
| Saturation Recovery | The [color saturation recovery](../../../../editor2/settings/render_settings/color/index.md#saturation_recovery) value for the filmic tonemapper. Filmic tonemapper desaturates image colors in bright areas making them look grayish. This parameter enables you to recover initial color saturation in such areas. Higher values make colors more saturated: - 0.0f - standard filmic tonemapping, no saturation recovery is performed. - 1.0f - color saturation is recovered to the full extent. > **Notice:** When the 1.0f value is set specular highlights appear too saturated, so the recommended value is 0.75f (default) Range of values: **[0.0f, 1.0f]**. The default value is : **0.75f**. `Console access:render_filmic_saturation_recovery` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_filmic_saturation_recovery)) \| ![](linear_scale_0.png) *White Level = 1.0 (by default)* \| ![](white_level_1.png) *White Level = 0.5* \| \|---\|---\| | ![](linear_scale_0.png) *White Level = 1.0 (by default)* | ![](white_level_1.png) *White Level = 0.5* |
| ![](linear_scale_0.png) *White Level = 1.0 (by default)* | ![](white_level_1.png) *White Level = 0.5* |  |  |


### ACES


| White Clip | The [white clip](../../../../editor2/settings/render_settings/color/index.md#white_clip) parameter for the ACES operator. Controls the cut-off point for white. Range of values: **[0.0f, 10.0f]**. The default value is : **2.51f**. `Console access:render_aces_white_clip` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_aces_white_clip)) |
|---|---|
| Toe | The [toe](../../../../editor2/settings/render_settings/color/index.md#toe) parameter for the ACES operator. Controls the dark color. Higher values result in darker colors. Range of values: **[0.0f, 10.0f]**. The default value is : **0.03f**. `Console access:render_aces_toe` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_aces_toe)) |
| Shoulder Angle | The [shoulder angle](../../../../editor2/settings/render_settings/color/index.md#shoulder_angle) parameter for the ACES operator. Controls how much overshoot should be added to the curve's shoulder. Range of values: **[0.0f, 10.0f]**. The default value is : **2.43f**. `Console access:render_aces_shoulder_angle` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_aces_shoulder_angle)) |
| Shoulder Strength | The [shoulder strength](../../../../editor2/settings/render_settings/color/index.md#shoulder_length) parameter for the ACES operator. Controls the strength of the transition between the curve's midsection and the curve's shoulder. Range of values: **[0.0f, 10.0f]**. The default value is : **0.59f**. `Console access:render_aces_shoulder_strength` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_aces_shoulder_strength)) |
| Shoulder Length | The [shoulder length](../../../../editor2/settings/render_settings/color/index.md#shoulder_length) parameter for the ACES operator. Controls the amount of f-stops to add to the dynamic range of the curve. Defines how much of the highlights the curve takes into account. Range of values: **[0.0f, 1.0f]**. The default value is : **0.59f**. `Console access:render_aces_shoulder_length` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_aces_shoulder_length)) |


### Mix ACES With Reinhard


| Mix With Reinhard | The [ACES with Reinhard tonemapping](../../../../editor2/settings/render_settings/color/index.md#mix_with_reinhard) operator contribution. If the value is closer to **0**, then ACES prevails. Otherwise, when the value is closer to **1**, the Reinhard has a grater impact. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_aces_with_reinhard_mix` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_aces_with_reinhard_mix)) |
|---|---|


### Reinhard


| Contribution | The [Reinhard tonemapping](../../../../editor2/settings/render_settings/color/index.md#contribution_r) operator contribution. The value is calculated according to the following formula: **C / (1 + C)** It controls the overall contribution that the Reinhard operator makes to the final color grading of the image. The higher values result in more tonemapping contribution to the final image. Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**. `Console access:render_reinhard_contribution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_reinhard_contribution)) |
|---|---|


### Reinhard Luma-Based


| Contribution | The [Reinhard Luma-Based tonemapping](../../../../editor2/settings/render_settings/color/index.md#contribution_l) operator contribution. Controls the overall contribution that the Reinhard operator makes to the final color grading of the image. Higher values result in more tonemapping contribution to the final image. Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**. `Console access:render_reinhard_luma_based_contribution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_reinhard_luma_based_contribution)) |
|---|---|


## Sharpness


![](sharpness.png)


| Sharpness | The value indicating if the sharpening post-processing effect is enabled. **disabled** by default. `Console access:render_sharpen` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sharpen)) |
|---|---|
| Sharpen Intensity | The intensity of the sharpening effect. To use this option, sharpening post-processing effect should be enabled*[Sharpen](#render_sharpen)*. Range of values: **[0.0f, inf]**. The default value is : **0.5f**. `Console access:render_sharpen_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sharpen_intensity)) |
| Blur Sigma | The smoothing applied to the Gaussian blur used in the [sharpening post-processing effect](#render_sharpen). Lower values result in a smoother, less noticeable blur. Such values are effective when the [blur radius](#render_sharpen_blur_radius) is greater than 1 pixel. If the blur radius is set to 1 pixel, a value of 1 is typically sufficient. Range of values: **[0.001f, inf]**. The default value is : **1.0f**. `Console access:render_sharpen_blur_sigma` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sharpen_blur_sigma)) |
| Blur Color Threshold | The brightness difference threshold between neighboring pixels to determine whether they should be blurred together when the [sharpening post-processing effect](#render_sharpen) is applied. If the brightness difference is below this threshold, the pixels will be blurred as a group. Lower values help avoid visual artifacts such as blooming around objects, harsh shadows, or thin details like wires against the sky. Range of values: **[0.001f, inf]**. The default value is : **0.2f**. `Console access:render_sharpen_blur_color_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sharpen_blur_color_threshold)) |
| Blur Dark Color Threshold Bias | The bias value applied to the sharpening blur in dark regions of the image. This value is used in the [sharpening post-processing effect](#render_sharpen) to reduce excessive noise that may occur when sharpening low-light areas during post-processing. Range of values: **[0.0f, 1.0f]**. The default value is : **0.05f**. `Console access:render_sharpen_blur_dark_color_threshold_bias` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sharpen_blur_dark_color_threshold_bias)) |
| Blur Radius | The radius of the blur applied in the [sharpening post-processing effect](#render_sharpen). A radius greater than 1-2 pixels may cause an undesirable blooming effect and negatively affect performance. Range of values: **[1, INT_MAX]**. The default value is : **1**. `Console access:render_sharpen_blur_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sharpen_blur_radius)) |
| Diagonal Samples | The value indicating diagonal neighboring pixels are included in the blur calculation, which is a part of the [sharpening post-processing effect](#render_sharpen). When enabled, all eight surrounding pixels affect the blur, resulting in a more rounded and consistent blur shape, but may affect performance. Disabling it limits the effect to only horizontal and vertical neighbors (left, right, top, bottom). **enabled** by default. `Console access:render_sharpen_diagonal_samples` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_sharpen_diagonal_samples)) |


## Color Grading


| Brightness | Correction of the overall scene brightness: - *Positive* values lighten the colors up to white. - *Negative* values darken the colors up to black. |
|---|---|
| Contrast | Correction of the overall scene contrast: - *Positive* values increase the contrast. - *Negative* values decrease the contrast. |
| Gamma | Correction of the overall scene gamma. |
| Fade Color | The fade color for the scene on the screen. By gradually changing this value it is possible to create "fade in" and "fade out" effects depending on the w component of the given vector. For example, when the following vectors are passed the result will be: - vec4(1,1,1,1) - a fully white screen. Positive w results in additive blending. - vec4(0.5,0.5,0.5,1) - light colors on the screen. - vec4(1,0,0,1) - R channel for all screen colors is to its maximum; G and B without changes. - vec4(0,0,0,0) - there is no fading (no color alterations are done to the screen). - vec4(1,1,1,-1) - a fully black screen. Negative w results in scene colors * (1 - RGB), where RGB is the first three components of the passed vector. - vec4(0.5,0.5,0.5,-1) - dark colors on the screen. **vec4_zero** - default value (white) `Console access:render_fade_color` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_fade_color)) |
| White Level | White level of the scene. |
| 3D LUT Texture | The loading, viewing, or clearing of the [Lookup Table texture](#color_lut) for color transformation. |


## Color Correction by Curves


| Color Correction | Tonal range and tone response of the final image. The horizontal input color values are mapped to the vertical output values based on [curves](../../../../editor2/curve_editor/index.md) for Red, Green and Blue channels. By adjusting all three channels at once, you control the luminance of the final image. ![](cc_curve.png) *Color correction curves* |
|---|---|
| Preserve Saturation | Preserve initial scene color saturation after applying color correction. |
| Saturation Correction | Correction [curve](../../../../editor2/curve_editor/index.md) of the overall scene saturation. The input luminance values are mapped to the vertical saturation values: - The *higher* the value, the more saturated and vibrant the colors are. - The *lower* the value, the duller and more colorless the colors are. ![](saturation_curve.png) *Saturation curve* Control the saturation of shadows by adjusting the values on the left, highlights - on the right. |


## Saturation and Hue


| Saturation per Color | Saturation fine-adjustment for 12 major colors of the spectre. ![](sat.gif) *Saturation adjustment* |
|---|---|
| Hue per Color | Hue (color shift) fine-adjustment for 12 major colors of the spectre. ![](hue.gif) *Hue adjustment* |


## Color Correction LUT


**Color Correction LUT** (Lookup Texture) is an optimized way of performing color grading in a post effect. Instead of tweaking individual color grading parameters, only a single texture is used to produce the corrected image. The lookup is performed by using the original image color as a vector to address the lookup texture.


One of the most common applications of lookup tables is to use them to see how images look in different media, such as TV/video or film, which have different color capabilities. Using a lookup table designed to mimic a certain display medium gives a much better idea what your current work will look like after it�s transferred to that medium.


**Advantages** of using a Color correction LUT include:


- **Better performance** � realtime computation is replaced by a simple array indexing operation.
- **More professional workflow opportunities**, where all color transforms can be defined using professional image editing software (such as Photoshop or GIMP), which provides a more precise result.


![](color_LUT1.png)

*Simple scene with neutral color correction applied.*


![](color_LUT2.png)

*Same scene using the lookup texture with shadows, highlights and vibrance applied.*


> **Notice:** Various visual effects can be created by changing the color correction LUT dynamically in realtime.


### Lookup Texture Requirements


The 2D texture representation must be laid out in a way that it represents an unwrapped volume texture (as an image sequence of "depth slices").


![](default_lut.png)

*A1024 x 32texture, representing a32x32x32color LUT.*


### Workflow Example


1. Generate a default lookup texture by clicking the ![](plus.png) button (*Save texture*) right to the LUT texture field and saving it as a **TGA** file (by selecting it in the *Type*field).
2. Take a screenshot of your scene.
3. Import your screenshot into a graphics editor (e.g., Photoshop or GIMP) and perform all necessary image correction operations (brightness, contrast, etc.) to achieve a desired look.
4. Import your generated default lookup texture into the graphics editor and perform the same operations as for the scene screenshot. Save the modified lookup texture as a new LUT.
5. In *Render Settings -> Color -> LUT texture*, select you new texture.


Now your scene in UnigineEditor looks exactly as in the graphics editor!
