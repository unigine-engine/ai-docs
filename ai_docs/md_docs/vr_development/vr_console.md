# VR Console Commands and Variables


After [VR initialization](../vr_development/index.md#which_backend), a set of VR-related console commands will become available.


## General


| vr_info |  |
|---|---|
| **Description:** - **Command.** Prints the information on the current VR API and the connected VR devices � HMD, controllers, and others. For the controllers, it also displays the battery level (if available). |  |
| vr_debug_mode | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current debug mode for VR API. - **Command.** � Sets the debug mode for VR API. > **Notice:** When the debug mode is enabled, a severe slowdown may occur. > > > Required to be set to 1 when using the **Varjo Base Simulator** (also make sure that *"Simulate"* is active in **Varjo Base**). | **Arguments:** **0** - release VR context (no debug) (by default) **1** - debug VR context **2** - debug VR context with break on error (only on debug binaries) |
| vr_reset_zero_pose |  |
| **Description:** - **Command.** Sets the zero pose to the current tracker position. |  |
| vr_show_profiler | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** display mode of the profiler overlay rendered inside the HMD view, one of the *SHOW_PROFILER_** values (disabled, basic, or advanced). Disabled by default. |  |
| vr_show_profiler_memory | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if the memory info panel of the VR profiler overlay is displayed. Effective only when the  property is not set to disabled. Enabled by default. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| vr_show_profiler_misc | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if the miscellaneous info panel of the VR profiler overlay is displayed. Effective only when the  property is not set to disabled. Enabled by default. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| vr_show_profiler_performance | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if the performance info panel of the VR profiler overlay is displayed. Effective only when the  property is not set to disabled. Enabled by default. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| vr_profiler_background_alpha | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current opacity of the VR profiler overlay background. The value is in the [0.0; 1.0] range, 0.8 by default. Effective only when the  property is not set to disabled. - **Command.** � Sets the opacity of the VR profiler overlay background. The value is in the [0.0; 1.0] range, 0.8 by default. Effective only when the  property is not set to disabled. | **Arguments:** **[0.0f; 1.0f]** - available range **0.8f** - by default |
| vr_profiler_position | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** position of the VR profiler overlay within the HMD view, one of the *PROFILER_POSITION_** values aligned with the numeric keypad layout. The default is the center of the view. Effective only when the  property is not set to disabled. |  |
| vr_render_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if rendering into the head-mounted display is enabled. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_render_while_hmd_idle | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if rendering is enabled while HMD is not worn. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| vr_service_init_timeout | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current VR initialization timeout in number of attempts. The engine attempts to run VR Service and has to wait for its initialization. - **Command.** � Sets the VR initialization timeout in number of attempts. The engine attempts to run VR Service and has to wait for its initialization. | **Arguments:** **[0; 200]** - available range **60** - by default |
| vr_mirror_crop | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current crop factor defining how the VR image is zoomed when mirrored to the target window. The value 1.0 means no crop, 2.0 means 2x zoom (default), and 5.0 is the maximum. - **Command.** � Sets the crop factor defining how the VR image is zoomed when mirrored to the target window. The value 1.0 means no crop, 2.0 means 2x zoom (default), and 5.0 is the maximum. | **Arguments:** **[1.0f; 5.0f]** - available range **2.0f** - by default |
| vr_mirror_crop_offset | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** offset of the cropped VR mirror image within the target window, as normalized coordinates. The value (0, 0) corresponds to the top-left corner, (0.5, 0.5) means no offset (default), (1, 1) is the bottom-right corner. |  |
| vr_emulation_mirror_crop | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current crop factor defining how the image is zoomed in the target window when running in VR emulation. The value 1.0 means no crop (default), and 5.0 is the maximum. Used instead of the  property when not rendering to an HMD. - **Command.** � Sets the crop factor defining how the image is zoomed in the target window when running in VR emulation. The value 1.0 means no crop (default), and 5.0 is the maximum. Used instead of the  property when not rendering to an HMD. | **Arguments:** **[1.0f; 5.0f]** - available range **1.0f** - by default |
| vr_emulation_mirror_crop_offset | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** offset of the cropped mirror image within the target window when running in VR emulation, as normalized coordinates. The value (0, 0) corresponds to the top-left corner, (0.5, 0.5) means no offset (default), (1, 1) is the bottom-right corner. Used instead of the  property when not rendering to an HMD. |  |
| vr_emulation_mirror_mode | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** mirror mode used when running in VR emulation (without rendering to an HMD), one of the *MIRROR_MODE_** values: black screen, left eye, right eye, or stereo (default). |  |
| vr_mirror_mode | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. - **Command.** � Sets the mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. | **Arguments:** **0** - black screen (no image is displayed). **1** - image rendered for the left eye. **2** - image rendered for the right eye. **3** - stereo image (both the left and right eyes). (by default) |
| vr_window_mode | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current window mode that defines which window will display the mirrored image (i.e. VR image). - **Command.** � Sets the window mode that defines which window will display the mirrored image (i.e. VR image). | **Arguments:** **0** - mirroring is disabled. **1** - main window displays the mirrored image. (by default) |


## Tracking


| vr_tracking_space | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** - **Variable.** � Prints the current zero pose of the tracking origin. - **Command.** � Sets the zero pose of the tracking origin. | **Arguments:** **0** - poses are provided relative to the Local (Seated or Stationary in OpenVR) Tracking Space. The origin is based on the user's position at startup (or after reset). Suited for sitting/simulator experiences (e.g. cockpit VR), where the player is already placed at the desired position. **1** - poses are provided relative to the Absolute (Standing in OpenVR) Tracking Space. The origin is fixed to the physical floor level (established by the tracking system, e.g. Base Stations or HMD SLAM Tracking). Suited for standing/room-scale experiences where the player is placed on the floor and the camera height comes from the HMD offset. (by default) |
| vr_head_tracking_position_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if the head position is locked. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| vr_head_tracking_rotation_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if the head rotation is locked. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| vr_motion_prediction | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if motion prediction is enabled. When enabled, the engine submits the velocity value from the GBuffer to the VR compositor. Check [hasFeatureMotionPrediction()](#hasFeatureMotionPrediction_int) to verify availability. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_motion_prediction_velocity_precision | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint). Requires [motion prediction support](#hasFeatureMotionPrediction_int). - **Command.** � Sets the factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint). Requires [motion prediction support](#hasFeatureMotionPrediction_int). | **Arguments:** **[eps; inf]** - available range **32.0f** - by default |
| vr_motion_prediction_velocity_time_delta | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa. Requires [motion prediction support](#hasFeatureMotionPrediction_int). - **Command.** � Sets the factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa. Requires [motion prediction support](#hasFeatureMotionPrediction_int). | **Arguments:** **[eps; inf]** - available range **1.0f / 60.0f** - by default |


## Peripheral Rendering


| vr_peripheral_rendering_mode_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if the peripheral rendering mode is enabled. In this mode, the HMD has two context (peripheral) and two focus viewports. You can disable two additional viewports to improve performance. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_peripheral_rendering_debug_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if debug visualization for peripheral rendering is enabled. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_peripheral_rendering_debug_gaze_override_coord | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** gaze position used when the debug override mode is set to *[COORD](#PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE_COORD)*, as normalized UV coordinates in texture space. The value (0, 0) is the top-left corner, (0.5, 0.5) is the center (default), (1, 1) is the bottom-right corner. |  |
| vr_peripheral_rendering_debug_gaze_override_mode | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** debug override mode for the gaze position used by peripheral (foveated) rendering, one of the *PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE_** values. Disabled by default. |  |
| vr_peripheral_rendering_border_width | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible. - **Command.** � Sets the width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible. | **Arguments:** **[eps; 1.0f]** - available range **0.2f** - by default |
| vr_peripheral_rendering_fov_scale | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current scale factor applied to the field of view used for focus viewports. - **Command.** � Sets the scale factor applied to the field of view used for focus viewports. | **Arguments:** **[0; 1]** - available range. **(0.3f, 0.3f)** - default value. |
| vr_peripheral_rendering_focus_scale | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current scale factor controlling the size of the foveal (focus) area. - **Command.** � Sets the scale factor controlling the size of the foveal (focus) area. | **Arguments:** **[0; 1]** - available range. **(0.5f, 0.2f)** - default value. |
| vr_peripheral_rendering_focus_deadzone | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current angular deadzone between the focus and context viewport transition. > **Notice:** Available for OpenXR only. - **Command.** � Sets the angular deadzone between the focus and context viewport transition. > **Notice:** Available for OpenXR only. | **Arguments:** **[0.0f; 1.0f]** - available range **0.15f** - by default |


## Foveated Rendering


| vr_foveated_rendering_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if foveated rendering is enabled. Foveated rendering uses eye tracking to improve performance by reducing the image quality in peripheral areas where the user is not looking, allowing applications to render fewer pixels. Check [hasFeatureFoveatedRendering()](#hasFeatureFoveatedRendering_int) to verify availability. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| vr_foveated_fixed_eye_center_bias | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current value by which the high-resolution focus area is shifted toward the center of the display when eye tracking is not used. A value of 0 keeps the focus area at the eye's natural resting position, a value of 1 moves it to the exact center. Takes effect when [peripheral rendering](../vr_development/vr_console.md#vr_peripheral_rendering_mode_enabled) is enabled and eye-tracked [foveated rendering](../vr_development/vr_console.md#vr_foveated_rendering_enabled) is disabled or eye tracking is unavailable. > **Notice:** Available for *OpenXR only*. - **Command.** � Sets the value by which the high-resolution focus area is shifted toward the center of the display when eye tracking is not used. A value of 0 keeps the focus area at the eye's natural resting position, a value of 1 moves it to the exact center. Takes effect when [peripheral rendering](../vr_development/vr_console.md#vr_peripheral_rendering_mode_enabled) is enabled and eye-tracked [foveated rendering](../vr_development/vr_console.md#vr_foveated_rendering_enabled) is disabled or eye tracking is unavailable. > **Notice:** Available for *OpenXR only*. | **Arguments:** **[0.0f; 1.0f]** - available range **0.0f** - by default |


## Stereo Rendering


| render_stereo_hidden_area_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Enables stereo hidden area support in shaders. This optimization masks pixels that are not visible through the headset lenses, reducing GPU work. | **Arguments:** **0** - disabled **1** - enabled (by default) |
| render_stereo_hidden_area |  |
| **Description:** - **Variable.** � Prints the current culling mode for pixels that are not visible in VR mode. - **Command.** � Sets the culling mode for pixels that are not visible in VR mode. One of the following values:  This parameter is used for performance optimization. - 0 - hidden area culling is disabled (by default). - 1 - **OpenVR-based culling mode**. Culling is performed using meshes returned by OpenVR. > **Notice:** Culling result depends on HMD used. - **2** - **Custom culling mode**. Culling is performed using meshes returned by OpenVR and an oval or circular mesh determined by custom adjustable parameters. | **Arguments:** **0** - disabled (by default) **1** - OpenVR-based culling mode **2** - Custom culling mode |
| render_stereo_hidden_area_transform |  |
| **Description:** - **Variable.** � Prints the current size and offset parameters for a new oval or circular mesh to be used for culling pixels, that are not visible in VR mode. - **Command.** � Sets the size and offset parameters for a new oval or circular mesh to be used for culling pixels, that are not visible in VR mode. A four-component vector (X, Y, Z, W), that determines an area to be used for exposure calculation, when culling of pixels, that are not visible in VR mode, is enabled:  All components are specified within the **[0.0f, 1.0f]** range - First two components **(X, Y)** - sizes along the X and Y axes respectively. - Second two components **(Z, W)** - offset values along the X and Y axes respectively. > **Notice:** These components can be used only when the hidden area culling mode is set to 2. | **Arguments:** **(1.0f, 1.0f, 0.0f, 0.0f)** - default value |
| render_stereo_hidden_area_exposure_transform |  |
| **Description:** - **Variable.** � Prints the current area to be used for exposure calculation, when culling of pixels that are not visible in VR mode is enabled. - **Command.** � Sets the area to be used for exposure calculation, when culling of pixels that are not visible in VR mode is enabled. Correction of this area is used to avoid visual artefacts when clipped pixels affect exposure in visible areas. A four-component vector (X, Y, Z, W):  All components are specified within the **[0.0f, 1.0f]** range. - First two components **(X, Y)** - sizes along the X and Y axes respectively. - Second two components **(Z, W)** - offset values along the X and Y axes respectively. > **Notice:** These components can be used only when the hidden area culling mode is set to 1 or 2. | **Arguments:** **(0.6f, 0.6f, 0.0f, 0.0f)** - default value |
| render_stereo_focus_supersampling |  |
| **Description:** - **Variable.** � Prints the current supersampling factor for focus viewports in the stereo video mode (number of samples per pixel used for adjusting supersampling for focus displays). The main supersampling factor  for focus viewports is multiplied by this value. - **Command.** � Sets the supersampling factor for focus viewports in the stereo video mode (number of samples per pixel used for adjusting supersampling for focus displays). The main supersampling factor  for focus viewports is multiplied by this value. | **Arguments:** **[1e-6f; 2.0f]** - available range **1.0f** - by default |
| render_stereo_distance | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current Focal distance for stereo convergence, in units. Determines the distance at which the left and right eye images converge. Objects at this distance appear at the screen plane; closer objects appear in front of it, farther objects behind it. - **Command.** � Sets the Focal distance for stereo convergence, in units. Determines the distance at which the left and right eye images converge. Objects at this distance appear at the screen plane; closer objects appear in front of it, farther objects behind it. | **Arguments:** **[0; inf]** - available range **4.0** - by default |
| render_stereo_radius | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current Half of the interpupillary distance (IPD), in units. Defines the offset of each eye from the head center. The default value of 0.032 corresponds to an IPD of 64 mm. In VR mode, this value is typically overridden by the headset's hardware IPD setting. - **Command.** � Sets the Half of the interpupillary distance (IPD), in units. Defines the offset of each eye from the head center. The default value of 0.032 corresponds to an IPD of 64 mm. In VR mode, this value is typically overridden by the headset's hardware IPD setting. | **Arguments:** **[0; inf]** - available range **0.032** - by default |
| render_stereo_offset | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current Additional horizontal offset applied to both eye cameras, in units. Can be used to fine-tune stereo separation on top of the base IPD radius. - **Command.** � Sets the Additional horizontal offset applied to both eye cameras, in units. Can be used to fine-tune stereo separation on top of the base IPD radius. | **Arguments:** **[0; inf]** - available range **0.0** - by default |
| render_stereo_planar_reflections_per_eye | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Renders planar reflections separately for each eye camera instead of once from the midpoint between both eyes. Produces more accurate reflections in VR at the cost of significantly reduced performance. | **Arguments:** **0** - disabled (by default) **1** - enabled |


## Mixed Reality Settings


| vr_mixed_reality_chroma_key_enabled |  |
|---|---|
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if chroma keying is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_mixed_reality_depth_test_enabled |  |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if depth buffer submission is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_mixed_reality_alpha_blend_enabled |  |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if alpha blending is enabled. This option is used for blending VR and AR images using the alpha channel. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled and the [screen precision](../api/library/rendering/class.render_cpp.md#isScreenPrecision_int) must be 1. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_mixed_reality_video_enabled |  |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if the video signal from the real-world view from the front-facing HMD-mounted cameras is enabled. The real-world view is used for combining virtual and real-world elements to create an immersive experience in mixed reality. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_mixed_reality_depth_test_range_enabled |  |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if the depth test range usage is enabled. Use the [depth test range](#getDepthTestRange_vec2) (*Depth Test Near Z*, *Depth Test Far Z*) to control the range for which the depth test is evaluated. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_mixed_reality_depth_test_range |  |
| **Description:** - **Variable.** � Prints the current depth test range as a two-component vector (the near and far planes). The [depth test range usage](#isDepthTestRangeEnabled_int) must be enabled. - **Command.** � Sets the depth test range as a two-component vector (the near and far planes). The [depth test range usage](#isDepthTestRangeEnabled_int) must be enabled. | **Arguments:** **vec2(0.0f, 1.0f)** - default value |
| vr_mixed_reality_camera_exposure_time | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current exposure time value that is valid for the connected device. - **Command.** � Sets the exposure time value that is valid for the connected device. | **Arguments:** - **1** - exposure time value equal to 91 ms - **2** - exposure time value equal to 125 ms (default) - **3** - exposure time value equal to 250 ms - **4** - exposure time value equal to 500 ms - **5** - exposure time value equal to 1000 ms - **6** - exposure time value equal to 2000 ms - **7** - exposure time value equal to 4000 ms - **8** - exposure time value equal to 8000 ms |
| vr_mixed_reality_camera_exposure_time_mode |  |
| **Description:** - **Variable.** � Prints the current exposure adjustment mode for the camera. - **Command.** � Sets the exposure adjustment mode for the camera. | **Arguments:** **0** - exposure adjustment is disabled **1** - automatic exposure adjustment (by default) **2** - manual exposure adjustment |
| vr_mixed_reality_camera_white_balance | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current white balance correction value that is valid for the connected device. - **Command.** � Sets the white balance correction value that is valid for the connected device. | **Arguments:** - **1** - white balance value equal to 2000 K - **2** - white balance value equal to 3000 K - **3** - white balance value equal to 3500 K - **4** - white balance value equal to 4200 K - **5** - white balance value equal to 5000 K - **6** - white balance value equal to 5400 K - **7** - white balance value equal to 6500 K (default) - **8** - white balance value equal to 8000 K - **9** - white balance value equal to 12000 K |
| vr_mixed_reality_camera_white_balance_mode |  |
| **Description:** - **Variable.** � Prints the current white balance adjustment mode for the camera. - **Command.** � Sets the white balance adjustment mode for the camera. | **Arguments:** **0** - white balance adjustment is disabled **1** - automatic white balance adjustment (by default) **2** - manual white balance adjustment |
| vr_mixed_reality_camera_iso | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints the current ISO value for the camera. - **Command.** � Sets the ISO value for the camera. | **Arguments:** - **1** - ISO value equal to 100 - **2** - ISO value equal to 200 - **3** - ISO value equal to 400 - **4** - ISO value equal to 800 (default) - **5** - ISO value equal to 1600 - **6** - ISO value equal to 3200 - **7** - ISO value equal to 6400 |
| vr_mixed_reality_camera_iso_mode |  |
| **Description:** - **Variable.** � Prints the current ISO adjustment mode for the camera. - **Command.** � Sets the ISO adjustment mode for the camera. | **Arguments:** **0** - ISO adjustment is disabled **1** - automatic ISO adjustment (by default) **2** - manual ISO adjustment |
| vr_mixed_reality_camera_flicker_compensation |  |
| **Description:** flicker compensation value for the camera. This is useful when using the HMD indoors with mostly artificial light bulbs, which flicker at the frequency of 50Hz or 60Hz and can cause visual flicker artifacts on the video see through image. The correct setting depends on the underlying power grid's frequency. For example, in most parts of Africa/Asia/Australia/Europe the frequency is 50 Hz and in most parts of North and South America 60 Hz. |  |
| vr_mixed_reality_camera_sharpness |  |
| **Description:** - **Variable.** � Prints the current sharpness filter power value for the camera. - **Command.** � Sets the sharpness filter power value for the camera. | **Arguments:** **[0; 10]** - available range **0** - by default |
| vr_mixed_reality_view_offset |  |
| **Description:** - **Variable.** � Prints the current eyes [view offset](https://developer.varjo.com/docs/apidocs/_varjo__mr_8h.html#a0aa1772b02020977c3c5b1c974848f75) (where eye camera should be positioned when using Mixed Reality): - **0** for physical eye position - **1** for VST camera position - **Command.** � Sets the eyes [view offset](https://developer.varjo.com/docs/apidocs/_varjo__mr_8h.html#a0aa1772b02020977c3c5b1c974848f75) (where eye camera should be positioned when using Mixed Reality): - **0** for physical eye position - **1** for VST camera position | **Arguments:** **[0.0; 1.0]** - available range **0.0** - by default |
| vr_mixed_reality_marker_tracking_enabled |  |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if marker tracking is enabled. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_mixed_reality_marker_visualizer_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating the marker visualizer is enabled. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_mixed_reality_blend_masking_mode |  |
| **Description:** - **Variable.** � Prints the current mode of the *Blend Control Mask* that can be used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth. - **Command.** � Sets the mode of the *Blend Control Mask* that can be used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth. | **Arguments:** **0** - Disabled (masking mode is disabled). (by default) **1** - Restrict Video to Mask (show the video pass-through image (VST) in the mask; can be used with chroma key) **2** - Restrict VR to Mask (show VR in the mask; can be used with chroma key) **3** - Restrict VR to Chromakey reduced by Mask (show VR in the mask and chroma elsewhere; requires chroma key) |
| vr_mixed_reality_blend_masking_debug_enabled |  |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the value indicating if blend masking debug visualization is enabled. The [blend masking mode](#getBlendMaskingMode_int) must be enabled. | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_mixed_reality_cubemap_mode |  |
| **Description:** - **Variable.** � Prints the current mode defining the way the AR texture is set for the environment. - **Command.** � Sets the mode defining the way the AR texture is set for the environment. | **Arguments:** **0** - cubemap streaming from AR cameras is disabled. **1** - environment texture substitutes the sky. **2** - the first environment preset defines the way the AR texture is set for the environment. (by default) **3** - the second environment preset defines the way the AR texture is set for the environment. **4** - the third environment preset defines the way the AR texture is set for the environment. |
| vr_mixed_reality_cubemap_ggx_quality |  |
| **Description:** - **Variable.** � Prints the current quality of the generated GGX mips for the AR cubemap. - **Command.** � Sets the quality of the generated GGX mips for the AR cubemap. | **Arguments:** **0** - low **1** - medium (by default) **2** - high **3** - ultra |
| vr_mixed_reality_override_color_correction_mode |  |
| **Description:** - **Variable.** � Prints the current color correction mode for the stream from the AR cameras. - **Command.** � Sets the color correction mode for the stream from the AR cameras. | **Arguments:** **0** - correction is disabled. (by default) **1** - exposure correction for the stream from the AR cameras. **2** - exposure and white balance correction for the stream. |
| vr_mixed_reality_camera_vst_reprojection_mode |  |
| **Description:** - **Variable.** � Prints the current reprojection mode of VST. - **Command.** � Sets the reprojection mode of VST. | **Arguments:** **0** - reprojection of VST is disabled (default). (by default) **1** - automatic reprojection mode of VST (the Depth buffer is used for reprojection) **2** - manual reprojections mode of VST |
| vr_mixed_reality_camera_vst_reprojection_distance |  |
| **Description:** - **Variable.** � Prints the current static distance in meters used to shift the whole image. Is configured only if the [VST reprojection mode](#CameraVSTReprojectionMode) is set to [Manual](#CAMERA_PROPERTY_MODE_MANUAL). - **Command.** � Sets the static distance in meters used to shift the whole image. Is configured only if the [VST reprojection mode](#CameraVSTReprojectionMode) is set to [Manual](#CAMERA_PROPERTY_MODE_MANUAL). | **Arguments:** **[0.0f; 1000.0f]** - available range **0.0f** - by default |
| vr_mixed_reality_apply_settings |  |
| **Description:** - **Command.** Updates mixed reality settings based on current settings. |  |


## Hand Tracking Settings


| vr_hand_tracking_visualizer_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the  value indicating if the visualizer for hands is enabled. When set to 1, the engine will draw a simple debug skeleton of the hands, showing bones only. This option requires the [Visualizer](../code/console/index.md#show_visualizer) to be enabled. ![](../api/library/vr/ht_command_visualizer.png) | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_hand_tracking_show_basis | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the  value indicating if the visualizer for the coordinate axes (basis) of each hand bone is enabled. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled. ![](../api/library/vr/ht_command_bone_basis.png) | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_hand_tracking_show_bone_sizes | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the  value indicating if the visualizer for the size of each hand bone is enabled. Displays red spheres representing the size (radius) of each bone, providing a visual reference for the physical dimensions of the tracked hand. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled. ![](../api/library/vr/ht_command_bone_sizes.png) | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_hand_tracking_show_velocity | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the  value indicating if the visualizer for the velocity vectors of each hand bone is enabled. Useful for debugging motion-based interactions like swipes or throws. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled. ![](../api/library/vr/ht_command_bone_velocity.png) | **Arguments:** **0** - disabled (by default) **1** - enabled |
