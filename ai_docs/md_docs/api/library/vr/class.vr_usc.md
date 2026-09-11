# Unigine.VR Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The base class for managing virtual reality in UNIGINE.


### VR Initialization


By default, VR is not initialized. To run the engine with VR, you need to specify the [*-vr_app*](../../../vr_development/index.md#which_backend) command-line option on the application start-up.


### Supported Graphics APIs


The following graphics APIs are supported out of the box:


- DirectX 12
- Vulkan


## VR Class

### Members

## void setRenderEnabled ( int enabled = 0 )

***Console*:**`vr_render_enabled`Sets a new value indicating if rendering into the head-mounted display is enabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **enabled** - The rendering into the HMD The default value is **false**.

## int isRenderEnabled () const

***Console*:**`vr_render_enabled`Returns the current value indicating if rendering into the head-mounted display is enabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current rendering into the HMD The default value is **false**.
## void setPeripheralRenderingModeEnabled ( int enabled = 0 )

***Console*:**`vr_peripheral_rendering_mode_enabled`Sets a new value indicating if the peripheral rendering mode is enabled. In this mode, the HMD has two context (peripheral) and two focus viewports. You can disable two additional viewports to improve performance. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **enabled** - The the peripheral rendering mode The default value is **false**.

## int isPeripheralRenderingModeEnabled () const

***Console*:**`vr_peripheral_rendering_mode_enabled`Returns the current value indicating if the peripheral rendering mode is enabled. In this mode, the HMD has two context (peripheral) and two focus viewports. You can disable two additional viewports to improve performance. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current the peripheral rendering mode The default value is **false**.
## void setPeripheralRenderingDebugEnabled ( bool enabled = 0 )

***Console*:**`vr_peripheral_rendering_debug_enabled`Sets a new value indicating if debug visualization for peripheral rendering is enabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *bool* **enabled** - Set **true** to enable debug visualization for peripheral rendering; **false** - to disable it. The default value is **false**.

## bool isPeripheralRenderingDebugEnabled () const

***Console*:**`vr_peripheral_rendering_debug_enabled`Returns the current value indicating if debug visualization for peripheral rendering is enabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

**true** if debug visualization for peripheral rendering is enabled ; otherwise **false**. The default value is **false**.
## void setPeripheralRenderingBorderWidth ( float width = 0.2f )

***Console*:**`vr_peripheral_rendering_border_width`Sets a new width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **width** - The width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible. Range of values: **[eps, 1.0f]**. The default value is : **0.2f**.

## float getPeripheralRenderingBorderWidth () const

***Console*:**`vr_peripheral_rendering_border_width`Returns the current width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible.
Range of values: **[eps, 1.0f]**. The default value is : **0.2f**.
## void setPeripheralRenderingFOVScale ( )

***Console*:**`vr_peripheral_rendering_fov_scale`Sets a new scale factor applied to the field of view used for focus viewports. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- **fovscale** - The scale factor applied to the field of view used for focus viewports. **[0; 1]** - available range. **(0.3f, 0.3f)** - default value.

## getPeripheralRenderingFOVScale () const

***Console*:**`vr_peripheral_rendering_fov_scale`Returns the current scale factor applied to the field of view used for focus viewports. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current scale factor applied to the field of view used for focus viewports.
**[0; 1]** - available range.
**(0.3f, 0.3f)** - default value.
## void setPeripheralRenderingFocusScale ( )

***Console*:**`vr_peripheral_rendering_focus_scale`Sets a new scale factor controlling the size of the foveal (focus) area. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- **scale** - The scale factor controlling the size of the foveal (focus) area. **[0; 1]** - available range. **(0.5f, 0.2f)** - default value.

## getPeripheralRenderingFocusScale () const

***Console*:**`vr_peripheral_rendering_focus_scale`Returns the current scale factor controlling the size of the foveal (focus) area. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current scale factor controlling the size of the foveal (focus) area.
**[0; 1]** - available range.
**(0.5f, 0.2f)** - default value.
## void setPeripheralRenderingFocusDeadzone ( float deadzone = 0.15f )

***Console*:**`vr_peripheral_rendering_focus_deadzone`Sets a new angular deadzone between the focus and context viewport transition.
> **Notice:** Available for OpenXR only.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **deadzone** - The angular deadzone between the focus and context viewport transition. Range of values: **[0.0f, 1.0f]**. The default value is : **0.15f**.

## float getPeripheralRenderingFocusDeadzone () const

***Console*:**`vr_peripheral_rendering_focus_deadzone`Returns the current angular deadzone between the focus and context viewport transition.
> **Notice:** Available for OpenXR only.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current angular deadzone between the focus and context viewport transition.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.15f**.
## void setMirrorMode ( int mode = 3 )

***Console*:**`vr_mirror_mode`Sets a new mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **mode** - The mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. One of the following values:

  - **0** - black screen (no image is displayed).
  - **1** - image rendered for the left eye.
  - **2** - image rendered for the right eye.
  - **3** - stereo image (both the left and right eyes). (by default)

## int getMirrorMode () const

***Console*:**`vr_mirror_mode`Returns the current mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. One of the following values:
- **0** - black screen (no image is displayed).
- **1** - image rendered for the left eye.
- **2** - image rendered for the right eye.
- **3** - stereo image (both the left and right eyes). (by default)

## void setWindowMode ( int mode = 1 )

***Console*:**`vr_window_mode`Sets a new window mode that defines which window will display the mirrored image (i.e. VR image). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **mode** - The window mode that defines which window will display the mirrored image (i.e. VR image). One of the following values:

  - **0** - mirroring is disabled.
  - **1** - main window displays the mirrored image. (by default)

## int getWindowMode () const

***Console*:**`vr_window_mode`Returns the current window mode that defines which window will display the mirrored image (i.e. VR image). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current window mode that defines which window will display the mirrored image (i.e. VR image). One of the following values:
- **0** - mirroring is disabled.
- **1** - main window displays the mirrored image. (by default)

## void setTrackingSpace ( int space = 1 )

***Console*:**`vr_tracking_space`Sets a new zero pose of the tracking origin. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **space** - The zero pose of the tracking origin. One of the following values:

  - **0** - poses are provided relative to the Local (Seated or Stationary in OpenVR) Tracking Space. The origin is based on the user's position at startup (or after reset). Suited for sitting/simulator experiences (e.g. cockpit VR), where the player is already placed at the desired position.
  - **1** - poses are provided relative to the Absolute (Standing in OpenVR) Tracking Space. The origin is fixed to the physical floor level (established by the tracking system, e.g. Base Stations or HMD SLAM Tracking). Suited for standing/room-scale experiences where the player is placed on the floor and the camera height comes from the HMD offset. (by default)

## int getTrackingSpace () const

***Console*:**`vr_tracking_space`Returns the current zero pose of the tracking origin. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current zero pose of the tracking origin. One of the following values:
- **0** - poses are provided relative to the Local (Seated or Stationary in OpenVR) Tracking Space. The origin is based on the user's position at startup (or after reset). Suited for sitting/simulator experiences (e.g. cockpit VR), where the player is already placed at the desired position.
- **1** - poses are provided relative to the Absolute (Standing in OpenVR) Tracking Space. The origin is fixed to the physical floor level (established by the tracking system, e.g. Base Stations or HMD SLAM Tracking). Suited for standing/room-scale experiences where the player is placed on the floor and the camera height comes from the HMD offset. (by default)

## void setMotionPrediction ( int prediction = 0 )

***Console*:**`vr_motion_prediction`Sets a new value indicating if motion prediction is enabled. When enabled, the engine submits the velocity value from the GBuffer to the VR compositor. Check [hasFeatureMotionPrediction()](#hasFeatureMotionPrediction_int) to verify availability. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **prediction** - The motion prediction The default value is **false**.

## int isMotionPrediction () const

***Console*:**`vr_motion_prediction`Returns the current value indicating if motion prediction is enabled. When enabled, the engine submits the velocity value from the GBuffer to the VR compositor. Check [hasFeatureMotionPrediction()](#hasFeatureMotionPrediction_int) to verify availability. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current motion prediction The default value is **false**.
## void setMotionPredictionVelocityPrecision ( float precision = 32.0f )

***Console*:**`vr_motion_prediction_velocity_precision`Sets a new factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint). Requires [motion prediction support](#hasFeatureMotionPrediction_int). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **precision** - The factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint). Range of values: **[eps, inf]**. The default value is : **32.0f**.

## float getMotionPredictionVelocityPrecision () const

***Console*:**`vr_motion_prediction_velocity_precision`Returns the current factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint). Requires [motion prediction support](#hasFeatureMotionPrediction_int). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint).
Range of values: **[eps, inf]**. The default value is : **32.0f**.
## void setMotionPredictionVelocityTimeDelta ( float delta = 1.0f / 60.0f )

***Console*:**`vr_motion_prediction_velocity_time_delta`Sets a new factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa. Requires [motion prediction support](#hasFeatureMotionPrediction_int). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **delta** - The factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa. Range of values: **[eps, inf]**. The default value is : **1.0f / 60.0f**.

## float getMotionPredictionVelocityTimeDelta () const

***Console*:**`vr_motion_prediction_velocity_time_delta`Returns the current factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa. Requires [motion prediction support](#hasFeatureMotionPrediction_int). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa.
Range of values: **[eps, inf]**. The default value is : **1.0f / 60.0f**.
## void setFoveatedRenderingEnabled ( int enabled = 1 )

***Console*:**`vr_foveated_rendering_enabled`Sets a new value indicating if foveated rendering is enabled. Foveated rendering uses eye tracking to improve performance by reducing the image quality in peripheral areas where the user is not looking, allowing applications to render fewer pixels. Check [hasFeatureFoveatedRendering()](#hasFeatureFoveatedRendering_int) to verify availability. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **enabled** - The foveated rendering The default value is **true**.

## int isFoveatedRenderingEnabled () const

***Console*:**`vr_foveated_rendering_enabled`Returns the current value indicating if foveated rendering is enabled. Foveated rendering uses eye tracking to improve performance by reducing the image quality in peripheral areas where the user is not looking, allowing applications to render fewer pixels. Check [hasFeatureFoveatedRendering()](#hasFeatureFoveatedRendering_int) to verify availability. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current foveated rendering The default value is **true**.
## void setFoveatedFixedEyeCenterBias ( float bias = 0.0f )

***Console*:**`vr_foveated_fixed_eye_center_bias`Sets a new value by which the high-resolution focus area is shifted toward the center of the display when eye tracking is not used. A value of 0 keeps the focus area at the eye's natural resting position, a value of 1 moves it to the exact center. Takes effect when [peripheral rendering](../../../vr_development/vr_console.md#vr_peripheral_rendering_mode_enabled) is enabled and eye-tracked [foveated rendering](../../../vr_development/vr_console.md#vr_foveated_rendering_enabled) is disabled or eye tracking is unavailable.
> **Notice:** Available for *OpenXR only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **bias** - The how much to shift the high-resolution focus area toward the center of the display when eye tracking is not used. Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.

## float getFoveatedFixedEyeCenterBias () const

***Console*:**`vr_foveated_fixed_eye_center_bias`Returns the current value by which the high-resolution focus area is shifted toward the center of the display when eye tracking is not used. A value of 0 keeps the focus area at the eye's natural resting position, a value of 1 moves it to the exact center. Takes effect when [peripheral rendering](../../../vr_development/vr_console.md#vr_peripheral_rendering_mode_enabled) is enabled and eye-tracked [foveated rendering](../../../vr_development/vr_console.md#vr_foveated_rendering_enabled) is disabled or eye tracking is unavailable.
> **Notice:** Available for *OpenXR only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current how much to shift the high-resolution focus area toward the center of the display when eye tracking is not used.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## const char * getApiName () const

Returns the current name of the VR API: *Null, OpenVR, OpenXR*, or *Varjo*.
### Return value

Current name of the VR API.
## int getApiType () const

Returns the current type of the VR API.
### Return value

Current type of the VR API.
## float getHMDRefreshRate () const

Returns the current refresh rate of the head-mounted display.
### Return value

Current refresh rate of the HMD.
## Vec3 getHandTrackingOffset () const

Returns the current hand tracking offset (for the Ultraleap device only).
### Return value

Current hand tracking offset.
## bool isHandTrackingOffsetSupported () const

Returns the current value indicating if the hand tracking offset is supported.
### Return value

**true** if the hand tracking offset is supported; otherwise **false**.
## int isPeripheralRenderingModeUsed () const

Returns the current value indicating if the peripheral rendering is used.
### Return value

Current the peripheral rendering is used
## int isHMDConnected () const

Returns the current value indicating if the head-mounted display is connected.
### Return value

Current the HMD is connected
## int isUsingFoveatedRendering () const

Returns the current value indicating if the foveated rendering is used.
### Return value

Current the foveated rendering is used
## Viewport getViewport () const

Returns the current viewport. It can be useful when implementing extra VR logic.
### Return value

Current viewport.
## getPlayerIModelview () const

Returns the current inverse model-view matrix of the camera that renders VR.
### Return value

Current inverse model-view matrix.
## getPlayerModelview () const

Returns the current model-view matrix of the camera that renders VR.
### Return value

Current model-view matrix.
## getPlayerWorldTransform () const

Returns the current world transformation of the camera that renders VR.
### Return value

Current world transformation matrix.
## getAbsoluteToLocalWorldTransform () const

Returns the current transformation matrix from absolute to local tracking space. Can be used to convert poses between tracking spaces.
### Return value

Current transformation matrix from absolute to local tracking space.
## static Event<bool> getEventRenderModelsVisibility () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventAudioSettingsChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event<int> getEventDeviceRenderModelChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## bool isSteamVRDashboardActive () const

Returns the current value indicating if the SteamVR dashboard is active. When the SteamVR dashboard is open, SteamVR renders its own controllers on top of the scene. You can use this to hide your application's controller models and avoid rendering both simultaneously.
### Return value

**true** if the SteamVR dashboard is active and SteamVR is drawing its own controllers is enabled ; otherwise **false**.
## getInputRuntimeType () const

Returns the current type of the VR input runtime.
### Return value

Current type of the VR input runtime.
## const char * getInputRuntimeName () const

Returns the current name of the VR input runtime.
### Return value

Current name of the VR input runtime.
## const char * getInputRuntimeVersion () const

Returns the current version of the VR input runtime.
### Return value

Current version of the VR input runtime.
## void setDebugMode ( )

Sets a new [debug mode](#DEBUG_MODE) for VR. If the debug mode is disabled, displaying of GAPI errors in VR runtime is also disabled.
### Arguments

- **mode** - The debug mode for VR.

## getDebugMode () const

Returns the current [debug mode](#DEBUG_MODE) for VR. If the debug mode is disabled, displaying of GAPI errors in VR runtime is also disabled.
### Return value

Current debug mode for VR.
## void setRenderWhileHMDIdle ( bool hmdidle = 1 )

***Console*:**`vr_render_while_hmd_idle`Sets a new value indicating if rendering is enabled while HMD is not worn. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *bool* **hmdidle** - Set **true** to enable rendering while HMD is not worn; **false** - to disable it. The default value is **true**.

## bool isRenderWhileHMDIdle () const

***Console*:**`vr_render_while_hmd_idle`Returns the current value indicating if rendering is enabled while HMD is not worn. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

**true** if rendering while HMD is not worn is enabled ; otherwise **false**. The default value is **true**.
## float getEyeNativeFOV () const

Returns the current device-native vertical field of view in radians (measured from the left eye).
### Return value

Current device-native vertical field of view in radians (measured from the left eye).
## void setEyeOverrideFOV ( float fov )

Sets a new vertical field of view override value (in degrees).
### Arguments

- *float* **fov** - The vertical field of view override value (in degrees). Range of values: **[0.00001f; 179.0f]**

## float getEyeOverrideFOV () const

Returns the current vertical field of view override value (in degrees).
### Return value

Current vertical field of view override value (in degrees). Range of values: **[0.00001f; 179.0f]**
## bool isEyeOverriddenFOV () const

Returns the current value indicating if the native vertical field of view value has been overridden (i.e., differs from the native field of view).
### Return value

**true** if the native vertical field of view value has been overridden (i.e., differs from the native field of view); otherwise **false**.
## void setEmulationMirrorCrop ( float crop = 1.0f )

***Console*:**`vr_emulation_mirror_crop`Sets a new crop factor defining how the image is zoomed in the target window when running in VR emulation. The value 1.0 means no crop (default), and 5.0 is the maximum. Used instead of the **[getMirrorCrop()()](../../...md#getMirrorCrop_float)** property when not rendering to an HMD. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **crop** - The crop (zoom) factor of the mirror image in VR emulation Range of values: **[1.0f, 5.0f]**. The default value is : **1.0f**.

## float getEmulationMirrorCrop () const

***Console*:**`vr_emulation_mirror_crop`Returns the current crop factor defining how the image is zoomed in the target window when running in VR emulation. The value 1.0 means no crop (default), and 5.0 is the maximum. Used instead of the **[getMirrorCrop()()](../../...md#getMirrorCrop_float)** property when not rendering to an HMD. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current crop (zoom) factor of the mirror image in VR emulation
Range of values: **[1.0f, 5.0f]**. The default value is : **1.0f**.
## void setEmulationMirrorCropOffset ( vec2 offset = vec2(0.5f, 0.5f) )

***Console*:**`vr_emulation_mirror_crop_offset`Sets a new offset of the cropped mirror image within the target window when running in VR emulation, as normalized coordinates. The value (0, 0) corresponds to the top-left corner, (0.5, 0.5) means no offset (default), (1, 1) is the bottom-right corner. Used instead of the **[getMirrorCropOffset()()](../../...md#getMirrorCropOffset_vec2)** property when not rendering to an HMD. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *vec2* **offset** - The offset of the cropped mirror image in VR emulation

## vec2 getEmulationMirrorCropOffset () const

***Console*:**`vr_emulation_mirror_crop_offset`Returns the current offset of the cropped mirror image within the target window when running in VR emulation, as normalized coordinates. The value (0, 0) corresponds to the top-left corner, (0.5, 0.5) means no offset (default), (1, 1) is the bottom-right corner. Used instead of the **[getMirrorCropOffset()()](../../...md#getMirrorCropOffset_vec2)** property when not rendering to an HMD. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current offset of the cropped mirror image in VR emulation

## void setEmulationMirrorMode ( int mode = 3 )

***Console*:**`vr_emulation_mirror_mode`Sets a new mirror mode used when running in VR emulation (without rendering to an HMD), one of the *MIRROR_MODE_** values: black screen, left eye, right eye, or stereo (default). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **mode** - The mirror mode used in VR emulation One of the following values:

## int getEmulationMirrorMode () const

***Console*:**`vr_emulation_mirror_mode`Returns the current mirror mode used when running in VR emulation (without rendering to an HMD), one of the *MIRROR_MODE_** values: black screen, left eye, right eye, or stereo (default). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current mirror mode used in VR emulation One of the following values:

## int getFoveatedMode () const

Returns the current effective foveated-rendering mode: *[DISABLED](#FOVEATED_MODE_DISABLED)* when foveated rendering is not used, *[FIXED](#FOVEATED_MODE_FIXED)* when the focus region is pinned, *[DYNAMIC](#FOVEATED_MODE_DYNAMIC)* when it follows the tracked gaze.
### Return value

Current effective foveated-rendering mode
## void setMirrorCrop ( float crop = 2.0f )

***Console*:**`vr_mirror_crop`Sets a new crop factor defining how the VR image is zoomed when mirrored to the target window. The value 1.0 means no crop, 2.0 means 2x zoom (default), and 5.0 is the maximum. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **crop** - The crop (zoom) factor of the VR mirror image Range of values: **[1.0f, 5.0f]**. The default value is : **2.0f**.

## float getMirrorCrop () const

***Console*:**`vr_mirror_crop`Returns the current crop factor defining how the VR image is zoomed when mirrored to the target window. The value 1.0 means no crop, 2.0 means 2x zoom (default), and 5.0 is the maximum. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current crop (zoom) factor of the VR mirror image
Range of values: **[1.0f, 5.0f]**. The default value is : **2.0f**.
## void setMirrorCropOffset ( vec2 offset = vec2(0.5f, 0.5f) )

***Console*:**`vr_mirror_crop_offset`Sets a new offset of the cropped VR mirror image within the target window, as normalized coordinates. The value (0, 0) corresponds to the top-left corner, (0.5, 0.5) means no offset (default), (1, 1) is the bottom-right corner. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *vec2* **offset** - The offset of the cropped VR mirror image

## vec2 getMirrorCropOffset () const

***Console*:**`vr_mirror_crop_offset`Returns the current offset of the cropped VR mirror image within the target window, as normalized coordinates. The value (0, 0) corresponds to the top-left corner, (0.5, 0.5) means no offset (default), (1, 1) is the bottom-right corner. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current offset of the cropped VR mirror image

## void setPeripheralRenderingDebugGazeOverrideCoord ( vec2 coord = vec2(0.5f, 0.5f) )

***Console*:**`vr_peripheral_rendering_debug_gaze_override_coord`Sets a new gaze position used when the debug override mode is set to *[COORD](#PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE_COORD)*, as normalized UV coordinates in texture space. The value (0, 0) is the top-left corner, (0.5, 0.5) is the center (default), (1, 1) is the bottom-right corner. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *vec2* **coord** - The gaze position for the coordinate-based debug override

## vec2 getPeripheralRenderingDebugGazeOverrideCoord () const

***Console*:**`vr_peripheral_rendering_debug_gaze_override_coord`Returns the current gaze position used when the debug override mode is set to *[COORD](#PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE_COORD)*, as normalized UV coordinates in texture space. The value (0, 0) is the top-left corner, (0.5, 0.5) is the center (default), (1, 1) is the bottom-right corner. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current gaze position for the coordinate-based debug override

## void setPeripheralRenderingDebugGazeOverrideMode ( int mode = 0 )

***Console*:**`vr_peripheral_rendering_debug_gaze_override_mode`Sets a new debug override mode for the gaze position used by peripheral (foveated) rendering, one of the *PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE_** values. Disabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **mode** - The debug gaze override mode for peripheral rendering One of the following values:

## int getPeripheralRenderingDebugGazeOverrideMode () const

***Console*:**`vr_peripheral_rendering_debug_gaze_override_mode`Returns the current debug override mode for the gaze position used by peripheral (foveated) rendering, one of the *PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE_** values. Disabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current debug gaze override mode for peripheral rendering One of the following values:

## void setProfilerBackgroundAlpha ( int alpha = 0.8f )

***Console*:**`vr_profiler_background_alpha`Sets a new opacity of the VR profiler overlay background. The value is in the [0.0; 1.0] range, 0.8 by default. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **alpha** - The opacity of the VR profiler background Range of values: **[0.0f, 1.0f]**. The default value is : **0.8f**.

## int getProfilerBackgroundAlpha () const

***Console*:**`vr_profiler_background_alpha`Returns the current opacity of the VR profiler overlay background. The value is in the [0.0; 1.0] range, 0.8 by default. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current opacity of the VR profiler background
Range of values: **[0.0f, 1.0f]**. The default value is : **0.8f**.
## void setProfilerPosition ( int position = 5 )

***Console*:**`vr_profiler_position`Sets a new position of the VR profiler overlay within the HMD view, one of the *PROFILER_POSITION_** values aligned with the numeric keypad layout. The default is the center of the view. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **position** - The position of the VR profiler overlay One of the following values:

## int getProfilerPosition () const

***Console*:**`vr_profiler_position`Returns the current position of the VR profiler overlay within the HMD view, one of the *PROFILER_POSITION_** values aligned with the numeric keypad layout. The default is the center of the view. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current position of the VR profiler overlay One of the following values:

## void setShowProfiler ( int profiler = 0 )

***Console*:**`vr_show_profiler`Sets a new display mode of the profiler overlay rendered inside the HMD view, one of the *SHOW_PROFILER_** values (disabled, basic, or advanced). Disabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **profiler** - The display mode of the VR profiler overlay One of the following values:

## int getShowProfiler () const

***Console*:**`vr_show_profiler`Returns the current display mode of the profiler overlay rendered inside the HMD view, one of the *SHOW_PROFILER_** values (disabled, basic, or advanced). Disabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current display mode of the VR profiler overlay One of the following values:

## void setShowProfilerMemory ( int memory = 1 )

***Console*:**`vr_show_profiler_memory`Sets a new value indicating if the memory info panel of the VR profiler overlay is displayed. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. Enabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **memory** - The the memory info panel of the VR profiler The default value is **true**.

## int isShowProfilerMemory () const

***Console*:**`vr_show_profiler_memory`Returns the current value indicating if the memory info panel of the VR profiler overlay is displayed. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. Enabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current the memory info panel of the VR profiler The default value is **true**.
## void setShowProfilerMisc ( int misc = 1 )

***Console*:**`vr_show_profiler_misc`Sets a new value indicating if the miscellaneous info panel of the VR profiler overlay is displayed. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. Enabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **misc** - The the miscellaneous info panel of the VR profiler The default value is **true**.

## int isShowProfilerMisc () const

***Console*:**`vr_show_profiler_misc`Returns the current value indicating if the miscellaneous info panel of the VR profiler overlay is displayed. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. Enabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current the miscellaneous info panel of the VR profiler The default value is **true**.
## void setShowProfilerPerformance ( int performance = 1 )

***Console*:**`vr_show_profiler_performance`Sets a new value indicating if the performance info panel of the VR profiler overlay is displayed. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. Enabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **performance** - The the performance info panel of the VR profiler The default value is **true**.

## int isShowProfilerPerformance () const

***Console*:**`vr_show_profiler_performance`Returns the current value indicating if the performance info panel of the VR profiler overlay is displayed. Effective only when the **[getShowProfiler()()](../../...md#getShowProfiler_int)** property is not set to disabled. Enabled by default. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current the performance info panel of the VR profiler The default value is **true**.
---

## ivec2 engine.vr. getHMDResolution ( int viewport_type = Enum.VR.VIEWPORT_TYPE.CONTEXT )

Returns the current resolution of the head-mounted display. For HMDs having context (peripheral) and focus displays, you should specify the viewport type.
### Arguments

- *int* **viewport_type** - Type of the viewport (for HMDs having context (peripheral) and focus displays).

### Return value

HMD resolution.
## int engine.vr. hasFeatureMixedReality ( )

Returns a value indicating if the mixed reality mode is available on the current device and VR backend. Mixed reality enables you to combine real-world view from front-facing cameras mounted on the headset with the VR image rendered.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureEyeTracking ( )

Returns a value indicating if eye tracking is available on the current device and VR backend.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureHandTracking ( )

Returns a value indicating if hand tracking is available. This feature is natively supported when using the **OpenXR** backend (via the *XR_EXT_hand_tracking* extension).
When using the **Varjo** backend, hand tracking is available via the **[Ultraleap plugin](../../../code/plugins/ultraleap/index_usc.md)**, but this method will return false � use the plugin's API to check the hand tracking status.


> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureMotionPrediction ( )

Returns a value indicating if motion prediction is available on the current device and VR backend. When enabled, the engine submits the velocity from the GBuffer to the VR compositor.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureFoveatedRendering ( )

Returns a value indicating if foveated rendering is available on the current device and VR backend. Foveated rendering enhances performance by using eye tracking to decrease the image quality in peripheral areas where the user is not looking, allowing applications to render fewer pixels and achieve a better VR experience.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureReportProximitySensor ( )

Returns a value indicating if proximity sensor reporting is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureSupportForTreadmill ( )

Returns a value indicating if the user treadmill support is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureSupportForBaseStations ( )

Returns a value indicating if the base stations support is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureSupportForTrackers ( )

Returns a value indicating if support for trackers is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureSupportForRenderModelComponents ( )

Returns a value indicating if support for render model components is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## static int engine.vr. resetZeroPose ( )

Sets the zero pose to the current tracker position.
### Return value

true if the pose is reset successfully; otherwise, false.
## int engine.vr. hasFeatureSupportForRenderModel ( )

Returns a value indicating if VR API can provide Render Models for the controllers.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureFadeToColor ( )

Returns a value indicating if the FadeToColor feature is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureFadeGrid ( )

Returns the value indicating if the FadeGrid feature is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## int engine.vr. hasFeatureGetAudioDevice ( )

Returns the value indicating if VR API can return Audio Device name (usually Oculus only).
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## void engine.vr. fadeToColor ( float seconds , vec4 color , int background )

Fades the engine render to the specified color over time.
### Arguments

- *float* **seconds** - Fade period, in seconds.
- *vec4* **color** - Target color.
- *int* **background**

## void engine.vr. fadeGrid ( float seconds , int fade_in )

Fades the engine render to/from the grid over the specified time.
### Arguments

- *float* **seconds** - Fade period, in seconds.
- *int* **fade_in** - true fades render to grid; false fades grid to render.

## void engine.vr. clearScriptableMaterials ( int eye )

Removes all [scriptable materials](../../../content/materials/scriptable.md) assigned to the target eye.
### Arguments

- *int* **eye** - Target eye.

## int engine.vr. getNumScriptableMaterials ( int eye )

Returns the number of [scriptable materials](../../../content/materials/scriptable.md) currently assigned to the specified eye.
### Arguments

- *int* **eye** - Target eye.

### Return value

Number of scriptable materials currently assigned to the specified eye.
## Material engine.vr. getScriptableMaterial ( int eye , int num )

Returns the [scriptable material](../../../content/materials/scriptable.md) assigned to the target eye by the number. The material's number determines the order in which the expressions assigned to it are executed.
### Arguments

- *int* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

### Return value

Scriptable material assigned to the target eye.
## void engine.vr. setScriptableMaterial ( int eye , int num , Material material )

Replaces the specified [scriptable material](../../../content/materials/scriptable.md) with a new scriptable material by its number for the target eye. The material's number determines the order in which the expressions assigned to it are executed.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *int* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).
- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - New scriptable material to replace the one with the specified number.

## void engine.vr. insertScriptableMaterial ( int eye , int num , Material material )

Inserts a new [scriptable material](../../../content/materials/scriptable.md) at the specified position for the target eye. The material's number determines the order in which the expressions assigned to it are executed. To apply a scriptable material globally, use the **[insertScriptableMaterial()()](../../../api/library/rendering/class.render_usc.md#insertScriptableMaterial_int_Material_void)** method of the Render class.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *int* **eye** - Target eye.
- *int* **num** - Position at which the new scriptable material is to be inserted.
- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Scriptable material to be inserted.

## int engine.vr. findScriptableMaterial ( int eye , Material material )

Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) for the target eye. The material's number determines the order in which the expressions assigned to it are executed.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *int* **eye** - Target eye.
- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Scriptable material for which the number is to be found.

### Return value

The number of the specified scriptable material for the target eye.
## void engine.vr. addScriptableMaterial ( int eye , Material material )

Adds the specified [scriptable material](../../../content/materials/scriptable.md) to the target eye's material list. The material's number determines the order in which the expressions assigned to it are executed. To apply a scriptable material globally, use the **[addScriptableMaterial()()](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void)** method of the Render class.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *int* **eye** - Target eye.
- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Scriptable material to add.

## void engine.vr. removeScriptableMaterial ( int eye , int num )

Removes the [scriptable material](../../../content/materials/scriptable.md) with the specified number from the target eye's material list.
### Arguments

- *int* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

## void engine.vr. swapScriptableMaterials ( int eye , int num_0 , int num_1 )

Swaps two [scriptable materials](../../../content/materials/scriptable.md) with the specified numbers in the target eye's material list. The material's number determines the order in which the expressions assigned to it are executed.
### Arguments

- *int* **eye** - Target eye.
- *int* **num_0** - Number of the first scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).
- *int* **num_1** - Number of the second scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

## void engine.vr. setScriptableMaterialEnabled ( int eye , int num , int enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number for the target eye. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).
- *int* **enabled** - true to enable the scriptable material with the specified number, false to disable it.

## int engine.vr. getScriptableMaterialEnabled ( int eye , int num )

Returns a value indicating if the [scriptable material](../../../content/materials/scriptable.md) with the specified number is enabled (active) for the target eye. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

### Return value

true if the scriptable material with the specified number is enabled; otherwise, **false**.
## void engine.vr. setEyeOffset ( int eye , mat4 offset )

Sets a custom transformation matrix to be applied to the target eye.
### Arguments

- *int* **eye** - Target eye.
- *mat4* **offset** - Transformation matrix to be applied to the target eye.

## mat4 engine.vr. getEyeOffset ( int eye )

Returns the current transformation matrix applied to the target eye.
### Arguments

- *int* **eye** - Target eye.

### Return value

Transformation matrix currently applied to the target eye.
## void engine.vr. resetEyeOffset ( int eye )

Resets the transformation offset of the target eye to the identity matrix.
### Arguments

- *int* **eye** - Target eye.

## void engine.vr. resetEyeOffset ( )

Resets the transformation offsets for both eyes to the identity matrix.
## void engine.vr. resetEyeOverrideFOV ( )

Resets the vertical field of view override to the native value.
