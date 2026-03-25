# Camera Effects


The camera effects list contains features specific to the usual SLR camera. To tweak, use *Rendering* panel -> *Camera Effects*.


[![](index.png)](index.jpg)

*Camera effects applied to viewport*


![](camera_effects.png)

*Camera Effects*


## Exposure And White Balance


### Exposure


![](exposure_settings.png)

*Exposure settings*


| Camera Mode | The camera mode, which determines the way the exposure is set. Either of the following: - **Physically-Based** - the real-world values are used to set up lighting and camera exposure: ISO*[ISO](#render_iso)*, shutter speed*[ShutterSpeed](#render_shutter_speed)*, F-stop*[FStop](#render_f_stop)*. With the default values of these parameters, the static exposure value is near 1. > **Notice:** For the physically-based mode, the exposure mode*[ExposureMode](#render_exposure_mode)* should be set to *Static* to avoid exposure issues. - **Classic** - the exposure is set by the Exposure value*[Exposure](#render_exposure)*. Option **#1** is selected by default (see above). `Console access:render_camera_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_camera_mode)) |
|---|---|
| Exposure Mode | The [mode of the adaptive exposure effect](../../../../editor2/settings/render_settings/camera_effects/index.md#mode). - **Static** - a static exposure. The amount of luminance is determined by the Exposure*[Exposure](#render_exposure)* depending on the Camera Mode*[CameraMode](#render_camera_mode)* parameter. - **Logarithmic** - adaptive logarithmic mapping technique. - **Quadratic** - adaptive quadratic mapping technique. - **Curve based** - adaptive curve based mapping technique. Option **#1** is selected by default (see above). `Console access:render_exposure_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_exposure_mode)) |
| Exposure | The camera [exposure](../../../../editor2/settings/render_settings/camera_effects/index.md#exposure) (a multiplier of the scene luminance and brightness). It determines the resulting amount of luminance: - By the minimum value of 0.0f, the image is rendered black. - The *higher* the value, the more luminance and the brighter the scene lit. Available only when the Camera Mode*[CameraMode](#render_camera_mode)* is set to Classic. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_exposure` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_exposure)) |


#### Classic Camera Model Settings


| Exposure | The camera [exposure](../../../../editor2/settings/render_settings/camera_effects/index.md#exposure) (a multiplier of the scene luminance and brightness). It determines the resulting amount of luminance: - By the minimum value of 0.0f, the image is rendered black. - The *higher* the value, the more luminance and the brighter the scene lit. Available only when the Camera Mode*[CameraMode](#render_camera_mode)* is set to Classic. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_exposure` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_exposure)) \| ![](exposure_0.png) *Exposure= 0.2* \| ![](exposure_1.png) *Exposure= 1* \| \|---\|---\| | ![](exposure_0.png) *Exposure= 0.2* | ![](exposure_1.png) *Exposure= 1* |
|---|---|---|---|
| ![](exposure_0.png) *Exposure= 0.2* | ![](exposure_1.png) *Exposure= 1* |  |  |


#### Physically Based Camera Model Settings


| ISO | The ISO value used for static exposure calculation. This value is available for the physically-based camera*[CameraMode](#render_camera_mode)* and represents the sensitivity of the camera sensor. The *higher* the ISO number, the more light is collected and the brighter the image is. Range of values: **[0, inf]**. The default value is : **100**. `Console access:render_iso` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_iso)) |
|---|---|
| Shutter Speed 1/ | The shutter speed used for static exposure calculation. This setting is available for the physically-based camera*[CameraMode](#render_camera_mode)* and indicates how long the sensor of the camera is actively collecting light. *Higher* values make the shutter speed faster and the image - darker. Range of values: **[0, inf]**. The default value is : **250**. `Console access:render_shutter_speed` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_shutter_speed)) |
| F-Stop | The f-stop value used for static exposure calculation. This setting is available for the physically-based camera*[CameraMode](#render_camera_mode)* and represents the ratio of the focal length (f) and the diameter of the lens opening (D): **f / D**. It is the reciprocal of the relative aperture. The *higher* the value, the darker the image is. Range of values: **[0, inf]**. The default value is : **11**. `Console access:render_f_stop` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_f_stop)) |


#### Logarithmic or Quadratic Adaptive Settings


| Adaptation | The time for the camera to adjust exposure, in seconds. 0.0f - means instant adaptation. If a too small or even negative value is provided, **1E-6** will be used instead. Range of values: **[eps, inf]**. The default value is : **1.0f**. `Console access:render_exposure_adaptation` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_exposure_adaptation)) |  |  |
|---|---|---|---|
| Min Luminance | The minimum luminance offset relative to the default luminance of the scene used for rendering of the adaptive exposure effect. The value range is **[-10.0f; 10.0f]**. The *higher* the value, the *darker* the adapted image is. The parameter can take on negative values. > **Notice:** If the specified value is greater than the current maximum luminance, the maximum luminance value will be changed to the specified minimum luminance so that they are equal. \| ![](min_luminance_0.png) *Min Luminance= -1* \| ![](min_luminance_1.png) *Min Luminance= 2* \| \|---\|---\| | ![](min_luminance_0.png) *Min Luminance= -1* | ![](min_luminance_1.png) *Min Luminance= 2* |
| ![](min_luminance_0.png) *Min Luminance= -1* | ![](min_luminance_1.png) *Min Luminance= 2* |  |  |
| Max Luminance | The maximum luminance offset relative to the default luminance of the scene used for rendering of adaptive exposure effect. The value range is **[-10.0f; 10.0f]**. The *lower* the value, the *brighter* the adapted image is. The parameter can take on negative values. > **Notice:** If the specified value is less than the current minimum luminance, the minimum luminance value is changed to the specified maximum luminance so that they are equal. |  |  |


#### Curve Based Adaptive Settings


| Adaptation | The time for the camera to adjust exposure, in seconds. 0.0f - means instant adaptation. If a too small or even negative value is provided, **1E-6** will be used instead. Range of values: **[eps, inf]**. The default value is : **1.0f**. `Console access:render_exposure_adaptation` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_exposure_adaptation)) |
|---|---|
| Auto Exposure Curve | Correction curve for the overall scene saturation. The input luminance values are mapped to the vertical saturation values. Higher values make colors more saturated and vibrant, lower values make colors duller and less saturated. |


### Auto White Balance


White balance correction eliminates the discoloration in the final image due to certain colors in the scene having more intensity and/or a higher or lower color temperature. Adaptive automatic white balance correction ensures realistic coloration of your scenes in real-time mode.


> **Notice:** To ensure the most natural look of your scene, adjust colors of light sources by setting [color temperatures](../../../../objects/lights/parameters/index.md#color_mode). In case of heavy high-contrast discoloration (e.g., too warm and too cold lights in a dark room), the final image may look unnatural.


![](w_balance_settings.png)

*White balance settings*


| White Balance | The value indicating if [automatic white balance correction](../../../../editor2/settings/render_settings/camera_effects/index.md#white_balance) is enabled. **enabled** by default. `Console access:render_white_balance` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_white_balance)) ![](white_balance_0.png) ![](white_balance_1.png) |
|---|---|
| Intensity | The value of [white balance correction intensity](../../../../editor2/settings/render_settings/camera_effects/index.md#white_balance_intensity). - 0.0f - no white balance correction is performed. - *higher* values result in stronger correction. > **Notice:** Do not set too high values for night-time and dimly lit scenes, as it may lead to heavy color distortion making the scene look totally unnatural. Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_white_balance_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_white_balance_intensity)) |
| Adaptation Time | The time period set for the camera to adjust white balance. During this time white balance correction is performed (0.0f - instant correction is to be used). > **Notice:** It is recommended to use lower values, when possible, to make correction process unnoticeable, otherwise it'll be slow and will catch user's eye. However, setting too low values may result in abrupt switching of colors as the camera moves. So, adjust this parameter carefully to make transition smoooth. You can set it equal to the Exposure Adaptation value*[ExposureAdaptation](#render_exposure_adaptation)*. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_white_balance_adaptation_time` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_white_balance_adaptation_time)) |


### Use Metering Mask


![](metering_mask.png)


| Use Metering Mask | The value indicating if metering mask for exposure and white balance correction is enabled. This option gives you an additional texture slot*[MeteringMaskTexture](#MeteringMaskTexture)* to control the effect of auto exposure and white balance correction on the whole screen, where each pixel is weighted in importance in accordance with the specified texture mask. **disabled** by default. `Console access:render_metering_mask_enabled` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_metering_mask_enabled)) |
|---|---|


| Metering Mask | The Metering Mask texture used to control the influence of auto exposure and white balance correction for the whole screen, where each pixel is weighted in importance in accordance with the specified texture mask. Giving importance to pixels toward the center of the screen rather than along the edges helps stabilize auto exposure. `Console access:MeteringMaskTexture` ([API control](../../../../api/library/rendering/class.render_cpp.md#MeteringMaskTexture)) |
|---|---|


## Motion Blur


![](motion_blur_preset.png)


| Motion Blur | The value indicating if the motion blur effect is enabled. **enabled** by default. `Console access:render_motion_blur` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur)) |
|---|---|
| Preset | The Motion Blur preset. To customize the Motion Blur effect options at run time you should activate the **Custom** preset: One of the following values: - Low (by default) - Medium - High - Ultra - Custom `Console access:render_motion_blur_preset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_preset)) > **Notice:** Presets override user-defined custom settings. When any preset other than Custom is active, modification of the parameters via [API](../../../../api/library/rendering/class.render_cpp.md) has no effect. The parameter value set via the last API call shall be used only when the Custom preset is active. When checking the current parameter value via API you'll get the corresponding setting stored in the active preset (default or custom one). |


### Customizable Settings


The following settings are available when the *[Custom](#motion_blur_preset)* preset is selected.


![Motion Blur custom settings](motion_blur.png)

*Motion Blur Settings*


| Velocity | The [scale value](../../../../editor2/settings/render_settings/camera_effects/index.md#velocity) of bodies' linear and angular velocities used for the motion blur. The *higher* the value, the more blurred the objects will appear when moving. To use this option, rendering of the motion blur effect*[MotionBlur](#render_motion_blur)* should be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_motion_blur_velocity_scale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_velocity_scale)) |
|---|---|
| Maximum Velocity | The [maximum possible amount](../../../../editor2/settings/render_settings/camera_effects/index.md#max_velocity) of [motion blur](../../../../principles/render/sequence/index.md#motion_blur) for moving physical objects. When their body velocity exceeds the set value, they will be blurred as if they have the maximum velocity set by the parameter. This parameter should be used: - To avoid excessive blurring of fast moving objects. - To save performance, as increasing the object's velocity leads increasing the radius of the motion blur effect that drops performance at too high values. To use this option, rendering of the motion blur effect*[MotionBlur](#render_motion_blur)* should be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_motion_blur_max_velocity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_max_velocity)) |
| Num Steps | The number of steps used in the [motion blur](../../../../principles/render/sequence/index.md#motion_blur). The higher the value, the more correct the motion blur effect is. At low values, moving objects may look doubled, however, performance will increase. To use this option, rendering of the motion blur effect*[MotionBlur](#render_motion_blur)* should be enabled. Range of values: **[2, 64]**. The default value is : **8**. `Console access:render_motion_blur_num_steps` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_num_steps)) |
| Noise Intensity | The intensity of the noise used in the [motion blur](../../../../principles/render/sequence/index.md#motion_blur). To use this option, rendering of the motion blur effect*[MotionBlur](#render_motion_blur)* should be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_motion_blur_noise_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_noise_intensity)) |
| Velocity Blur Samples | The number of iterations performed to blur the border between moving and static objects. Higher values ensure a higher quality of blurring, but affect the performance. To use this option, rendering of the motion blur effect*[MotionBlur](#render_motion_blur)* should be enabled. > **Notice:** Disabled in VR mode by default. Range of values: **[0, 512]**. The default value is : **32**. `Console access:render_motion_blur_velocity_blur_samples` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_velocity_blur_samples)) |
| Velocity Blur Radius | The radius of the [motion blur](../../../../principles/render/sequence/index.md#motion_blur) effect for the boundary between moving and static objects. Range of values: **[0.0f, inf]**. The default value is : **0.5f**. `Console access:render_motion_blur_velocity_blur_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_velocity_blur_radius)) |
| Depth Threshold Near | The value defining if the blur effect is applied to the foreground object. If the distance between the foreground object and the background object is less than this threshold value, the motion blur effect won't be applied to the foreground object. To use this option, rendering of the motion blur effect*[MotionBlur](#render_motion_blur)* should be enabled. > **Notice:** Disabled in VR mode by default. Range of values: **[0.0f, inf]**. The default value is : **0.2f**. `Console access:render_motion_blur_depth_threshold_near` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_depth_threshold_near)) |
| Depth Threshold Far | The value defining if the blur effect is applied to the background object. If the distance between the foreground object and the background object is less than this threshold value, the motion blur effect won't be applied to the background object. To use this option, rendering of the motion blur effect*[MotionBlur](#render_motion_blur)* should be enabled. > **Notice:** Disabled in VR mode by default. Range of values: **[0.0f, inf]**. The default value is : **0.5f**. `Console access:render_motion_blur_depth_threshold_far` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_depth_threshold_far)) |
| Camera Velocity | The value indicating if camera velocity contributes to the [motion blur](../../../../principles/render/sequence/index.md#motion_blur) effect (false to take into account velocities of objects only). To use this option, rendering of the motion blur effect*[MotionBlur](#render_motion_blur)* should be enabled. > **Notice:** Disabled in VR mode by default. **enabled** by default. `Console access:render_motion_blur_camera_velocity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_motion_blur_camera_velocity)) |


## Depth Of Field


![](dof_preset.png)


| Depth Of Field | The value indicating if the [DOF](../../../../editor2/settings/render_settings/camera_effects/index.md) (Depth Of Field) effect is enabled. **disabled** by default. `Console access:render_dof` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof)) |
|---|---|
| Preset | The DoF effect quality preset. To customize the DoF effect options at run time you should activate the **Custom** preset: One of the following values: - Very Low (by default) - Low - Medium - High - Ultra - Extreme - Custom `Console access:render_dof_preset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_preset)) > **Notice:** Presets override user-defined custom settings. When any preset other than Custom is active, modification of the parameters via [API](../../../../api/library/rendering/class.render_cpp.md) has no effect. The parameter value set via the last API call shall be used only when the Custom preset is active. When checking the current parameter value via API, you'll get the corresponding setting stored in the active preset (default or custom one). |
| Focal Distance | The [focal distance](../../../../editor2/settings/render_settings/camera_effects/index.md#focal_distance) of the camera, i.e. a point where objects are in-focus and visible clearly. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_dof_focal_distance` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_focal_distance)) ![](focal_distance_0.jpg) ![](focal_distance_1.jpg) |
| Blur | The intensity of [blur](../../../../editor2/settings/render_settings/camera_effects/index.md#blur) for the DOF (Depth Of Field) effect. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_dof_blur` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_blur)) ![](dof_blur_0.jpg) ![](dof_blur_1.jpg) |
| Chromatic Aberration | The intensity of [chromatic aberration](../../../../editor2/settings/render_settings/camera_effects/index.md#chromatic_aberration) for the DOF (Depth Of Field) effect. Range of values: **[0.0f, inf]**. The default value is : **0.0f**. `Console access:render_dof_chromatic_aberration` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_chromatic_aberration)) ![](dof_blur_0.jpg) ![](chromatic_aberration_1.jpg) |


### Near


| Distance | The [near DOF limit](../../../../editor2/settings/render_settings/camera_effects/index.md#near_distance) of the camera: the distance between the camera and the first element that is considered to be acceptably sharp. Black zone on the DOF mask means in-focus zone. Range of values: **[0.0f, inf]**. The default value is : **10.0f**. `Console access:render_dof_near_distance` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_near_distance)) \| ![Near Distance = 10](dof_normal.png) *Near Distance = 10* \| ![Near Distance = 1.5](dof_near.png) *Near Distance = 1.5* \| \|---\|---\| The black zone on the DoF mask means in-focus zone. | ![Near Distance = 10](dof_normal.png) *Near Distance = 10* | ![Near Distance = 1.5](dof_near.png) *Near Distance = 1.5* |
|---|---|---|---|
| ![Near Distance = 10](dof_normal.png) *Near Distance = 10* | ![Near Distance = 1.5](dof_near.png) *Near Distance = 1.5* |  |  |
| Focal offset | The [offset](../../../../editor2/settings/render_settings/camera_effects/index.md#near_focal_offset) from the focal to the nearest blurred zone. In other words, the distance when foreground (near) is in focus. Range of values: **[0.0f, inf]**. The default value is : **0.0f**. `Console access:render_dof_near_focal_offset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_near_focal_offset)) |  |  |


### Far


| Distance | The [far DOF limit](../../../../editor2/settings/render_settings/camera_effects/index.md#far_distance) of the camera: the distance between the camera and the furthest element that is considered to be acceptably sharp. Black zone on the DOF mask means in-focus zone. Range of values: **[0.0f, inf]**. The default value is : **10.0f**. `Console access:render_dof_far_distance` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_far_distance)) \| ![Far Distance = 10](dof_normal.png) *Far Distance = 10* \| ![Far Distance = 1.5](dof_far.png) *Far Distance = 1.5* \| \|---\|---\| The black zone on the DoF mask means in-focus zone. | ![Far Distance = 10](dof_normal.png) *Far Distance = 10* | ![Far Distance = 1.5](dof_far.png) *Far Distance = 1.5* |
|---|---|---|---|
| ![Far Distance = 10](dof_normal.png) *Far Distance = 10* | ![Far Distance = 1.5](dof_far.png) *Far Distance = 1.5* |  |  |
| Focal offset | The Sets the [offset](../../../../editor2/settings/render_settings/camera_effects/index.md#far_focal_offset) from the focal to the farthest blurred zone for the DOF effect. In other words, the distance when background (far) is in focus. Range of values: **[0.0f, inf]**. The default value is : **0.0f**. `Console access:render_dof_far_focal_offset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_far_focal_offset)) |  |  |


### Bokeh


| Shape | The shape of the [Bokeh](../../../../editor2/settings/render_settings/camera_effects/index.md#bokeh_shape) for the DOF effect. This parameter determines the way the lens renders out-of-focus points of light. > **Notice:** For the DOF effect, the Bokeh effect is enabled by default. One of the following values: - ring (by default) - circle `Console access:render_dof_bokeh_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_bokeh_mode)) ![](bokeh_shape_ring.jpg) ![](bokeh_shape_circle.jpg) |
|---|---|


### Customizable Settings


The following settings are available when the *[Custom](#dof_preset)* preset is selected.


![DOF custom settings](dof.png)

*DOF Settings*


| Quality | The [quality](../../../../editor2/settings/render_settings/camera_effects/index.md#quality) of the DOF (Depth Of Field) effect. One of the following values: - *Low* - low quality - *Medium* - medium quality (by default) - *High* - high quality - *Ultra* - ultra quality `Console access:render_dof_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_quality)) |
|---|---|
| Resolution | The [resolution](../../../../editor2/settings/render_settings/camera_effects/index.md#resolution) of the DOF (Depth Of Field) effect. One of the following values: - quarter - half - full (by default) `Console access:render_dof_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_resolution)) |
| Increased Accuracy | The value indicating if the [increased accuracy](../../../../editor2/settings/render_settings/camera_effects/index.md#increased_accuracy) option is enabled for the DOF (Depth Of Field) effect. When enabled, focusing calculation is performed with increased accuracy. **disabled** by default. `Console access:render_dof_increased_accuracy` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_increased_accuracy)) ![](increased_accuracy_off.jpg) ![](increased_accuracy_on.jpg) |
| Focus Improvement | The value indicating if the [focus improvement](../../../../editor2/settings/render_settings/camera_effects/index.md#focus_improvement) option is enabled for the DOF (Depth Of Field) effect. When enabled, transitions between the focused and unfocused parts of the scene become more accurate. **disabled** by default. `Console access:render_dof_focus_improvement` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dof_focus_improvement)) ![](focus_improvement_off.jpg) ![](increased_accuracy_on.jpg) |


## Glare Effects


| Threshold | The brightness threshold, which is used to detect if an object should be blurred in the HDR mode. By the minimum value of 0, the bright areas can become overexposed. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_camera_effects_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_camera_effects_threshold)) \| ![](threshold_0.png) *Threshold= 0.6* \| ![](threshold_1.png) *Threshold= 1.2* \| \|---\|---\| | ![](threshold_0.png) *Threshold= 0.6* | ![](threshold_1.png) *Threshold= 1.2* |
|---|---|---|---|
| ![](threshold_0.png) *Threshold= 0.6* | ![](threshold_1.png) *Threshold= 1.2* |  |  |
| Dirt Scale | The intensity of lens dirt effect modulating the pattern of lens flares defined by the [Dirt Texture](../../../../editor2/settings/render_settings/camera_effects/index.md#lens_dirt). For example, it can be used to create an effect of unclean optics when the camera looks at the sun. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_dirt_scale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_dirt_scale)) |  |  |
| Dirt | A texture that creates an effect of dirty camera lens. For example, it can be used to create an effect of light reflections or unclean optics when the camera looks at the sun. [![](dirt_texture_sm.png)](dirt_texture.png) *Example of dirt texture* \| [![](dirt_texture_default_sm.png)](dirt_texture_default.png) *No dirt texture* \| [![](dirt_texture_custom_sm.png)](dirt_texture_custom.png) *Custom dirt texture* \| \|---\|---\| > **Notice:** If you can't see any effect of the *Dirt* texture, try tweaking the *[Threshold](#threshold)* parameter. | [![](dirt_texture_default_sm.png)](dirt_texture_default.png) *No dirt texture* | [![](dirt_texture_custom_sm.png)](dirt_texture_custom.png) *Custom dirt texture* |
| [![](dirt_texture_default_sm.png)](dirt_texture_default.png) *No dirt texture* | [![](dirt_texture_custom_sm.png)](dirt_texture_custom.png) *Custom dirt texture* |  |  |
| Temporal Filtering | The value indicating if temporal filtering for camera effects is enabled. Temporal filtering reduces flickering of the bloom effect on the small bright objects (such flickering may appear when the camera moves). For example, it can be used in scenes with industrial pipes. **disabled** by default. `Console access:render_camera_effects_temporal_filtering` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_camera_effects_temporal_filtering)) |  |  |
| Color Clamping Intensity | The intensity of TAA color clamping for the Bloom effect. *Lower* values result in more accumulated frames combined, which reduces noise flickering, but increases ghosting effect. To reduce ghosting in this case you can use Min Velocity Clamping*[CameraEffectsTemporalFilteringMinVelocityClamping](#render_camera_effects_temporal_filtering_min_velocity_clamping)* and Max Velocity Clamping*[CameraEffectsTemporalFilteringMaxVelocityClamping](#render_camera_effects_temporal_filtering_max_velocity_clamping)*, while *higher* values reduce ghosting effect, but increase flickering. > **Notice:** This option is available only when the temporal filtering*[CameraEffectsTemporalFiltering](#render_camera_effects_temporal_filtering)* is enabled. Range of values: **[1.0f, inf]**. The default value is : **3.0f**. `Console access:render_camera_effects_temporal_filtering_color_clamping_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_camera_effects_temporal_filtering_color_clamping_intensity)) |  |  |
| Min Velocity Clamping | The sensitivity of TAA color clamping for the Bloom effect for static objects. This parameter is used to reduce ghosting effect for lower Color Clamping Intensity*[CameraEffectsTemporalFilteringColorClampingIntensity](#render_camera_effects_temporal_filtering_color_clamping_intensity)* values: higher values reduce ghosting, but at the same time reduce the temporal filter effect. > **Notice:** This option is available only when the temporal filtering*[CameraEffectsTemporalFiltering](#render_camera_effects_temporal_filtering)* is enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.05f**. `Console access:render_camera_effects_temporal_filtering_min_velocity_clamping` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_camera_effects_temporal_filtering_min_velocity_clamping)) |  |  |
| Max Velocity Clamping | The sensitivity of TAA color clamping for the Bloom effect for moving objects. This parameter is used to reduce ghosting effect for lower Color Clamping Intensity*[CameraEffectsTemporalFilteringColorClampingIntensity](#render_camera_effects_temporal_filtering_color_clamping_intensity)* values: higher values reduce ghosting, but at the same time reduce the temporal filter effect. > **Notice:** This option is available only when the temporal filtering*[CameraEffectsTemporalFiltering](#render_camera_effects_temporal_filtering)* is enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**. `Console access:render_camera_effects_temporal_filtering_max_velocity_clamping` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_camera_effects_temporal_filtering_max_velocity_clamping)) |  |  |


### Bloom


![](bloom_settings.png)

*Bloom settings*


| Enabled | The value indicating if the Bloom effect is enabled. **disabled** by default. `Console access:render_bloom` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_bloom)) |
|---|---|
| Resolution | The resolution of the Bloom effect. One of the following values: - quarter - half - full (by default) `Console access:render_bloom_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_bloom_resolution)) |
| Scale | The scale of the Bloom effect. Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_bloom_scale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_bloom_scale)) |
| Power | The power of the Bloom effect. - 0.0f (min) - the Bloom effect is blurred. - 1.0f (max) - the Bloom effect is more contrast. Range of values: **[0.0f, 1.0f]**. The default value is : **0.7f**. `Console access:render_bloom_power` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_bloom_power)) |
| Passes | The number of passes for the bloom effect. During the pass a Bloom texture is generating. Up to 8 Bloom textures can be generated: each texture has lower resolution (original size, original size /2, original size /4, so forth) with Bloom effect. After that, all these Bloom textures with the different resolution form the final Bloom texture. > **Notice:** The higher the value, the smoother the effect is. However, this option significantly affects performance. Range of values: **[2, 8]**. The default value is : **6**. `Console access:render_bloom_passes` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_bloom_passes)) |


### Cross


![](cross_settings.png)

*Cross Settings*


| Enabled | The value indicating if [cross flares](../../../../editor2/settings/render_settings/camera_effects/index.md#cross) are enabled. **disabled** by default. `Console access:render_cross` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_cross)) |  |  |  |  |
|---|---|---|---|---|---|
| Color | The [color](../../../../editor2/settings/render_settings/camera_effects/index.md#cross_color) of the cross flares. To use this option, rendering of cross flares*[Cross](#render_cross)* should be enabled. **vec4_one** - default value (white) `Console access:render_cross_color` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_cross_color)) \| ![](cross_color_0.png) \| ![](cross_color_1.png) \| \|---\|---\| \| ![](cross_color_white.png) \| ![](cross_color_red.png) \| | ![](cross_color_0.png) | ![](cross_color_1.png) | ![](cross_color_white.png) | ![](cross_color_red.png) |
| ![](cross_color_0.png) | ![](cross_color_1.png) |  |  |  |  |
| ![](cross_color_white.png) | ![](cross_color_red.png) |  |  |  |  |
| Scale | The color multiplier.[cross color scale](../../../../editor2/settings/render_settings/camera_effects/index.md#cross_scale) - a multiplier for the [color](#setCrossColor_vec4_void) of cross flares. *Higher* values produce *more pronounced* flares. To use this option, rendering of cross flares*[Cross](#render_cross)* should be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_cross_scale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_cross_scale)) \| ![](cross_color_1.png) *Scale = 0.4 (by default)* \| ![](cross_scale_1.png) *Scale = 0.7* \| \|---\|---\| | ![](cross_color_1.png) *Scale = 0.4 (by default)* | ![](cross_scale_1.png) *Scale = 0.7* |  |  |
| ![](cross_color_1.png) *Scale = 0.4 (by default)* | ![](cross_scale_1.png) *Scale = 0.7* |  |  |  |  |
| Shafts | The number of [shafts](../../../../editor2/settings/render_settings/camera_effects/index.md#cross_shafts) in a cross flare. High number of flares can cause a FPS drop on low-performance hardware. To use this option, rendering of cross flares*[Cross](#render_cross)* should be enabled. Range of values: **[2, 32]**. The default value is : **4**. `Console access:render_cross_shafts` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_cross_shafts)) \| ![](cross_shafts_0.png) *Shafts = 2 (minimum)* \| ![](cross_shafts_1.png) *Shafts = 6 (by default)* \| ![](cross_shafts_2.png) *Shafts = 32 (maximum)* \| \|---\|---\|---\| | ![](cross_shafts_0.png) *Shafts = 2 (minimum)* | ![](cross_shafts_1.png) *Shafts = 6 (by default)* | ![](cross_shafts_2.png) *Shafts = 32 (maximum)* |  |
| ![](cross_shafts_0.png) *Shafts = 2 (minimum)* | ![](cross_shafts_1.png) *Shafts = 6 (by default)* | ![](cross_shafts_2.png) *Shafts = 32 (maximum)* |  |  |  |
| Length | The [length](../../../../editor2/settings/render_settings/camera_effects/index.md#cross_length) of a cross flare relative to the screen width. *Increasing* this value also leads to fading of the shafts across their length. To use this option, rendering of cross flares*[Cross](#render_cross)* should be enabled. Range of values: **[0.0f, 2.0f]**. The default value is : **0.2f**. `Console access:render_cross_length` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_cross_length)) \| ![](cross_length_0.png) *Length = 0.2 (by default)* \| ![](cross_length_1.png) *Length = 0.4* \| \|---\|---\| | ![](cross_length_0.png) *Length = 0.2 (by default)* | ![](cross_length_1.png) *Length = 0.4* |  |  |
| ![](cross_length_0.png) *Length = 0.2 (by default)* | ![](cross_length_1.png) *Length = 0.4* |  |  |  |  |
| Angle | The cross flares orientation [angle](../../../../editor2/settings/render_settings/camera_effects/index.md#cross_angle). To use this option, rendering of cross flares*[Cross](#render_cross)* should be enabled. Range of values: **[-inf, inf]**. The default value is : **45.0f**. `Console access:render_cross_angle` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_cross_angle)) \| ![](cross_angle_0.png) *Angle = 45 (by default)* \| ![](cross_angle_1.png) *Angle = 90* \| \|---\|---\| | ![](cross_angle_0.png) *Angle = 45 (by default)* | ![](cross_angle_1.png) *Angle = 90* |  |  |
| ![](cross_angle_0.png) *Angle = 45 (by default)* | ![](cross_angle_1.png) *Angle = 90* |  |  |  |  |
| Threshold | The brightness [threshold](../../../../editor2/settings/render_settings/camera_effects/index.md#cross_threshold) for areas to produce flare. The *higher* the threshold value, the brighter the area should be to produce a flare. To use this option, rendering of cross flares*[Cross](#render_cross)* should be enabled. Range of values: **[0.0f, inf]**. The default value is : **0.0f**. `Console access:render_cross_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_cross_threshold)) |  |  |  |  |


### Lens


![](lens_settings.png)

*Lens settings*


| Enabled | The value indicating if lens flares are enabled. **disabled** by default. `Console access:render_lens` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lens)) |  |  |  |  |
|---|---|---|---|---|---|
| Color | The color of HDR lens flares. To use this option, rendering of lens flares*[Lens](#render_lens)* should be enabled. **vec4_one** - default value (white) `Console access:render_lens_color` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lens_color)) \| ![](lens_color_0.png) \| ![](lens_color_1.png) \| \|---\|---\| \| ![](cross_color_white.png) \| ![](cross_color_red.png) \| | ![](lens_color_0.png) | ![](lens_color_1.png) | ![](cross_color_white.png) | ![](cross_color_red.png) |
| ![](lens_color_0.png) | ![](lens_color_1.png) |  |  |  |  |
| ![](cross_color_white.png) | ![](cross_color_red.png) |  |  |  |  |
| Scale | The multiplier for color*[LensColor](#render_lens_color)* of HDR lens flares. To use this option, rendering of lens flares*[Lens](#render_lens)* should be enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_lens_scale` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lens_scale)) \| ![](lens_color_1.png) *Scale = 0.25* \| ![](lens_scale_1.png) *Scale = 0.5* \| \|---\|---\| | ![](lens_color_1.png) *Scale = 0.25* | ![](lens_scale_1.png) *Scale = 0.5* |  |  |
| ![](lens_color_1.png) *Scale = 0.25* | ![](lens_scale_1.png) *Scale = 0.5* |  |  |  |  |
| Length | The length of the radial lens flare indicating if the whole radial lens flare is rendered on the screen or only a part of it. This option controls how lens flares pattern is distributed. To use this option, rendering of lens flares *[Lens](#render_lens)* should be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_lens_length` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lens_length)) |  |  |  |  |
| Radius | The radius of the spherical lens flares on the screen. **1.0f** corresponds to a screen-wide radius (a lens flare is not visible). To use this option, rendering of lens flares*[Lens](#render_lens)* should be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_lens_radius` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lens_radius)) \| ![](lens_radius_0.png) *Radius = 0.07* \| ![](lens_radius_1.png) *Radius = 0.1* \| \|---\|---\| | ![](lens_radius_0.png) *Radius = 0.07* | ![](lens_radius_1.png) *Radius = 0.1* |  |  |
| ![](lens_radius_0.png) *Radius = 0.07* | ![](lens_radius_1.png) *Radius = 0.1* |  |  |  |  |
| Threshold | The value of the brightness threshold for areas to produce lens flares. The *higher* the threshold value, *the brighter* the area should be to produce flares. To use this option, rendering of lens flares*[Lens](#render_lens)* should be enabled. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_lens_threshold` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_lens_threshold)) |  |  |  |  |
| Red | Color displacement for the red channel of lens flares. \| ![](lens_red_0.png) *Red = 0.9* \| ![](lens_red_1.png) *Red = 1* \| ![](lens_red_2.png) *Red = 1.1* \| \|---\|---\|---\| | ![](lens_red_0.png) *Red = 0.9* | ![](lens_red_1.png) *Red = 1* | ![](lens_red_2.png) *Red = 1.1* |  |
| ![](lens_red_0.png) *Red = 0.9* | ![](lens_red_1.png) *Red = 1* | ![](lens_red_2.png) *Red = 1.1* |  |  |  |
| Green | Color displacement for the green channel of lens flares. \| ![](lens_green_0.png) *Green = 0.9* \| ![](lens_red_1.png) *Green = 1* \| ![](lens_green_2.png) *Green = 1.1* \| \|---\|---\|---\| | ![](lens_green_0.png) *Green = 0.9* | ![](lens_red_1.png) *Green = 1* | ![](lens_green_2.png) *Green = 1.1* |  |
| ![](lens_green_0.png) *Green = 0.9* | ![](lens_red_1.png) *Green = 1* | ![](lens_green_2.png) *Green = 1.1* |  |  |  |
| Blue | Color displacement for the blue channel of lens flares. \| ![](lens_blue_0.png) *Blue = 0.9* \| ![](lens_red_1.png) *Blue = 1* \| ![](lens_blue_2.png) *Blue = 1.1* \| \|---\|---\|---\| | ![](lens_blue_0.png) *Blue = 0.9* | ![](lens_red_1.png) *Blue = 1* | ![](lens_blue_2.png) *Blue = 1.1* |  |
| ![](lens_blue_0.png) *Blue = 0.9* | ![](lens_red_1.png) *Blue = 1* | ![](lens_blue_2.png) *Blue = 1.1* |  |  |  |


## Chromatic Aberration


![](chromatic_aberration_settings.png)


| Chromatic Aberration | The value indicating if rendering of the *[Chromatic Aberration](../../../../editor2/settings/render_settings/camera_effects/index.md#post_chromatic_aberration)* post-effect is enabled. This effect simulates color shifts in real-world camera lenses due to light rays entering a lens at different points causing separation of RGB colors. **disabled** by default. `Console access:render_chromatic_aberration` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_chromatic_aberration)) |
|---|---|
| Intensity | The intensity (strength) of the *[Chromatic Aberration](../../../../editor2/settings/render_settings/camera_effects/index.md#post_chromatic_aberration)* post-effect. Controls how much color shifting occurs. Range of values: **[0.0f, inf]**. The default value is : **0.5f**. `Console access:render_chromatic_aberration_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_chromatic_aberration_intensity)) |
| Noise Intensity | The intensity of noise applied for the *[Chromatic Aberration](../../../../editor2/settings/render_settings/camera_effects/index.md#post_chromatic_aberration)* post-effect. Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**. `Console access:render_chromatic_aberration_noise_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_chromatic_aberration_noise_intensity)) |
| Samples | The number of samples used for calculation of the *[Chromatic Aberration](../../../../editor2/settings/render_settings/camera_effects/index.md#post_chromatic_aberration)* post-effect. *Higher* values reduce banding making the effect look smoother. Range of values: **[1, 32]**. The default value is : **1**. `Console access:render_chromatic_aberration_samples` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_chromatic_aberration_samples)) |


## Noise


![](noise_settings.png)


| Noise | The value indicating if rendering of the *[Noise](../../../../editor2/settings/render_settings/camera_effects/index.md#post_noise)* post-effect is enabled. **disabled** by default. `Console access:render_noise` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_noise)) |
|---|---|
| Intensity | The intensity of the *[Noise](../../../../editor2/settings/render_settings/camera_effects/index.md#post_noise)* post-effect. *Higher* values result in more noise applied to the image. Range of values: **[0.0f, inf]**. The default value is : **0.03f**. `Console access:render_noise_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_noise_intensity)) |


## Vignette Mask


![](vignette_mask_settings.png)


| Vignette Mask | The value indicating if rendering of the *[Vignette Mask](../../../../editor2/settings/render_settings/camera_effects/index.md#post_vignette)* post-effect is enabled. The effect applies darkening towards the edges of an image compared to the center usually caused by thick or stacked filters, secondary lenses, and lens hoods. It can be used for an artistic effect, to draw focus to the center of the image. **disabled** by default. `Console access:render_vignette_mask` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_vignette_mask)) |
|---|---|
| Mask | Custom texture to be used as a vignette mask. |
| Mask Intensity | The intensity of the *[Vignette Mask](../../../../editor2/settings/render_settings/camera_effects/index.md#post_vignette)*. Defines the amount of vignetting on the screen: *higher* values moke the vignette wider. Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**. `Console access:render_vignette_mask_intensity` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_vignette_mask_intensity)) |
| Mask Power | The Power value that controls mask opacity for the *[Vignette Mask](../../../../editor2/settings/render_settings/camera_effects/index.md#post_vignette)* post-effect. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_vignette_mask_power` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_vignette_mask_power)) |
