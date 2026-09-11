# Unigine.VRMixedReality Class (CPP)

**Header:** #include <UnigineVRMixedReality.h>

> **Notice:** This class is a singleton.


The class is used for mixed reality management on compatible head-mounted displays (HMDs) that support mixed reality and operate on **Varjo** or **OpenXR** backends.


When using the **Varjo** backend, all features of this class are available. Under **OpenXR**, mixed reality support is limited. Use the *[hasFeature...()](../../...md#hasFeatureAlphaBlend_int)* methods to check which features and corresponding methods of this class are supported specifically for your device and backend configuration.


## VRMixedReality Class

### Enums

## BLEND_MASKING_MODE

| Name | Description |
|---|---|
| **BLEND_MASKING_MODE_BEGIN** = 0 | The first element to be used for iteration. |
| **BLEND_MASKING_MODE_DISABLED** = 0 | Masking mode is disabled. |
| **BLEND_MASKING_MODE_RESTRICT_VIDEO_TO_MASK** = 1 | Show the video pass-through image (VST) in the mask. Can be used with chroma key. |
| **BLEND_MASKING_MODE_RESTRICT_VR_TO_MASK** = 2 | Show VR in the mask. Can be used with chroma key. |
| **BLEND_MASKING_MODE_RESTRICT_VR_TO_CHROMAKEY_REDUCED_BY_MASK** = 3 | Show VR in the mask and chroma elsewhere. Requires chroma key. |
| **BLEND_MASKING_MODE_END** = 3 | The last element to be used for iteration. |

## CAMERA_PROPERTY_MODE

| Name | Description |
|---|---|
| **CAMERA_PROPERTY_MODE_DISABLED** = 0 | The camera property adjustment is disabled. |
| **CAMERA_PROPERTY_MODE_AUTO** = 1 | Automatic property adjustment for the camera. |
| **CAMERA_PROPERTY_MODE_MANUAL** = 2 | Manual property adjustment for the camera. In this mode you can set the desired property value (exposure time correction, white balance correction, ISO) manually via the corresponding methods. |

## CAMERA_EXPOSURE_TIME

| Name | Description |
|---|---|
| **CAMERA_EXPOSURE_TIME_UNKNOWN** = 0 | The camera exposure time is not specified. |
| **CAMERA_EXPOSURE_TIME_BEGIN** = 1 | The first element to be used for iteration. |
| **CAMERA_EXPOSURE_TIME_VALUE_91_MS** = 1 | The camera exposure time value equal to 91 K. |
| **CAMERA_EXPOSURE_TIME_VALUE_125_MS** = 2 | The camera exposure time value equal to 125 K. |
| **CAMERA_EXPOSURE_TIME_VALUE_250_MS** = 3 | The camera exposure time value equal to 250 K. |
| **CAMERA_EXPOSURE_TIME_VALUE_500_MS** = 4 | The camera exposure time value equal to 500 K. |
| **CAMERA_EXPOSURE_TIME_VALUE_1000_MS** = 5 | The camera exposure time value equal to 1000 K. |
| **CAMERA_EXPOSURE_TIME_VALUE_2000_MS** = 6 | The camera exposure time value equal to 2000 K. |
| **CAMERA_EXPOSURE_TIME_VALUE_4000_MS** = 7 | The camera exposure time value equal to 4000 K. |
| **CAMERA_EXPOSURE_TIME_VALUE_8000_MS** = 8 | The camera exposure time value equal to 8000 K. |
| **CAMERA_EXPOSURE_TIME_END** = 8 | The last element to be used for iteration. |

## CAMERA_WHITE_BALANCE

| Name | Description |
|---|---|
| **CAMERA_WHITE_BALANCE_UNKNOWN** = 0 | The camera white balance value is not specified. |
| **CAMERA_WHITE_BALANCE_BEGIN** = 1 | The first element to be used for iteration. |
| **CAMERA_WHITE_BALANCE_VALUE_2000_K** = 1 | The camera white balance value equal to 2000 K. |
| **CAMERA_WHITE_BALANCE_VALUE_3000_K** = 2 | The camera white balance value equal to 3000 K. |
| **CAMERA_WHITE_BALANCE_VALUE_3500_K** = 3 | The camera white balance value equal to 3500 K. |
| **CAMERA_WHITE_BALANCE_VALUE_4200_K** = 4 | The camera white balance value equal to 4200 K. |
| **CAMERA_WHITE_BALANCE_VALUE_5000_K** = 5 | The camera white balance value equal to 5000 K. |
| **CAMERA_WHITE_BALANCE_VALUE_5400_K** = 6 | The camera white balance value equal to 5400 K. |
| **CAMERA_WHITE_BALANCE_VALUE_6500_K** = 7 | The camera white balance value equal to 6500 K. |
| **CAMERA_WHITE_BALANCE_VALUE_8000_K** = 8 | The camera white balance value equal to 8000 K. |
| **CAMERA_WHITE_BALANCE_VALUE_12000_K** = 9 | The camera white balance value equal to 12000 K. |
| **CAMERA_WHITE_BALANCE_END** = 9 | The last element to be used for iteration. |

## CAMERA_ISO

| Name | Description |
|---|---|
| **CAMERA_ISO_UNKNOWN** = 0 | The camera ISO value is not specified. |
| **CAMERA_ISO_BEGIN** = 1 | The first element to be used for iteration. |
| **CAMERA_ISO_GAIN_100** = 1 | The camera ISO value equal to 100. |
| **CAMERA_ISO_GAIN_200** = 2 | The camera ISO value equal to 200. |
| **CAMERA_ISO_GAIN_400** = 3 | The camera ISO value equal to 400. |
| **CAMERA_ISO_GAIN_800** = 4 | The camera ISO value equal to 800. |
| **CAMERA_ISO_GAIN_1600** = 5 | The camera ISO value equal to 1600. |
| **CAMERA_ISO_GAIN_3200** = 6 | The camera ISO value equal to 3200. |
| **CAMERA_ISO_GAIN_6400** = 7 | The camera ISO value equal to 6400. |
| **CAMERA_ISO_END** = 7 | The last element to be used for iteration. |

## CAMERA_FLICKER_COMPENSATION

| Name | Description |
|---|---|
| **CAMERA_FLICKER_COMPENSATION_UNKNOWN** = 0 | The camera flicker compensation value is not specified. |
| **CAMERA_FLICKER_COMPENSATION_BEGIN** = 1 | The first element to be used for iteration. |
| **CAMERA_FLICKER_COMPENSATION_FREQ_50_HZ** = 1 | The camera flicker compensation value equal to 50 Hz. |
| **CAMERA_FLICKER_COMPENSATION_FREQ_60_HZ** = 2 | The camera flicker compensation value equal to 60 Hz. |
| **CAMERA_FLICKER_COMPENSATION_END** = 2 | The last element to be used for iteration. |

## CUBEMAP_MODE

| Name | Description |
|---|---|
| **CUBEMAP_MODE_BEGIN** = 0 | The first element to be used for iteration. |
| **CUBEMAP_MODE_DISABLED** = 0 | The cubemap streaming from AR cameras is disabled. |
| **CUBEMAP_MODE_ENVIRONMENT_OVERLAP** = 1 | The environment texture substitutes the sky. |
| **CUBEMAP_MODE_ENVIRONMENT_PRESET_0** = 2 | The first [environment preset](../../../editor2/settings/render_settings/environment/index.md#presets) defines the way the AR texture is set for the environment. |
| **CUBEMAP_MODE_ENVIRONMENT_PRESET_1** = 3 | The second [environment preset](../../../editor2/settings/render_settings/environment/index.md#presets) defines the way the AR texture is set for the environment. |
| **CUBEMAP_MODE_ENVIRONMENT_PRESET_2** = 4 | The third [environment preset](../../../editor2/settings/render_settings/environment/index.md#presets) defines the way the AR texture is set for the environment. |
| **CUBEMAP_MODE_END** = 4 | The last element to be used for iteration. |

## OVERRIDE_COLOR_CORRECTION_MODE

| Name | Description |
|---|---|
| **OVERRIDE_COLOR_CORRECTION_MODE_BEGIN** = 0 | The first element to be used for iteration. |
| **OVERRIDE_COLOR_CORRECTION_MODE_DISABLED** = 0 | The color correction is disabled. |
| **OVERRIDE_COLOR_CORRECTION_MODE_EXPOSURE** = 1 | Exposure correction for the stream from the AR cameras. |
| **OVERRIDE_COLOR_CORRECTION_MODE_EXPOSURE_WHITE_BALANCE** = 2 | Exposure and white balance correction for the stream. |
| **OVERRIDE_COLOR_CORRECTION_MODE_END** = 2 | The last element to be used for iteration. |

### Members

## bool isAvailable () const

Returns the current value indicating if mixed reality is available on the active VR device, and is supported at runtime.
### Return value

**true** if mixed reality is available; otherwise **false**.
## void setChromaKeyEnabled ( bool enabled = 0 )

***Console*:**`vr_mixed_reality_chroma_key_enabled`Sets a new value indicating if chroma keying is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable chroma keying; **false** - to disable it. The default value is **false**.

## bool isChromaKeyEnabled () const

***Console*:**`vr_mixed_reality_chroma_key_enabled`Returns the current value indicating if chroma keying is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled.
### Return value

**true** if chroma keying is enabled ; otherwise **false**. The default value is **false**.
## void setDepthTestEnabled ( bool enabled = 0 )

***Console*:**`vr_mixed_reality_depth_test_enabled`Sets a new value indicating if depth buffer submission is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable depth testing; **false** - to disable it. The default value is **false**.

## bool isDepthTestEnabled () const

***Console*:**`vr_mixed_reality_depth_test_enabled`Returns the current value indicating if depth buffer submission is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled.
### Return value

**true** if depth testing is enabled ; otherwise **false**. The default value is **false**.
## void setAlphaBlendEnabled ( bool enabled = 0 )

***Console*:**`vr_mixed_reality_alpha_blend_enabled`Sets a new value indicating if alpha blending is enabled. This option is used for blending VR and AR images using the alpha channel. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled and the [screen precision](../../../api/library/rendering/class.render_cpp.md#isScreenPrecision_int) must be 1.
### Arguments

- *bool* **enabled** - Set **true** to enable alpha blending; **false** - to disable it. The default value is **false**.

## bool isAlphaBlendEnabled () const

***Console*:**`vr_mixed_reality_alpha_blend_enabled`Returns the current value indicating if alpha blending is enabled. This option is used for blending VR and AR images using the alpha channel. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled and the [screen precision](../../../api/library/rendering/class.render_cpp.md#isScreenPrecision_int) must be 1.
### Return value

**true** if alpha blending is enabled ; otherwise **false**. The default value is **false**.
## void setVideoEnabled ( bool enabled = 0 )

***Console*:**`vr_mixed_reality_video_enabled`Sets a new value indicating if the video signal from the real-world view from the front-facing HMD-mounted cameras is enabled. The real-world view is used for combining virtual and real-world elements to create an immersive experience in mixed reality.
### Arguments

- *bool* **enabled** - Set **true** to enable the real-world view from the front-facing HMD-mounted cameras; **false** - to disable it. The default value is **false**.

## bool isVideoEnabled () const

***Console*:**`vr_mixed_reality_video_enabled`Returns the current value indicating if the video signal from the real-world view from the front-facing HMD-mounted cameras is enabled. The real-world view is used for combining virtual and real-world elements to create an immersive experience in mixed reality.
### Return value

**true** if the real-world view from the front-facing HMD-mounted cameras is enabled ; otherwise **false**. The default value is **false**.
## void setDepthTestRangeEnabled ( bool enabled = 0 )

***Console*:**`vr_mixed_reality_depth_test_range_enabled`Sets a new value indicating if the depth test range usage is enabled. Use the [depth test range](#getDepthTestRange_vec2) (*Depth Test Near Z*, *Depth Test Far Z*) to control the range for which the depth test is evaluated.
### Arguments

- *bool* **enabled** - Set **true** to enable the depth test range; **false** - to disable it. The default value is **false**.

## bool isDepthTestRangeEnabled () const

***Console*:**`vr_mixed_reality_depth_test_range_enabled`Returns the current value indicating if the depth test range usage is enabled. Use the [depth test range](#getDepthTestRange_vec2) (*Depth Test Near Z*, *Depth Test Far Z*) to control the range for which the depth test is evaluated.
### Return value

**true** if the depth test range is enabled ; otherwise **false**. The default value is **false**.
## void setDepthTestRange ( const Math:: vec2 & range )

***Console*:**`vr_mixed_reality_depth_test_range`Sets a new depth test range as a two-component vector (the near and far planes). The [depth test range usage](#isDepthTestRangeEnabled_int) must be enabled.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **range** - The depth test range. **vec2(0.0f, 1.0f)** - default value

## Math:: vec2 getDepthTestRange () const

***Console*:**`vr_mixed_reality_depth_test_range`Returns the current depth test range as a two-component vector (the near and far planes). The [depth test range usage](#isDepthTestRangeEnabled_int) must be enabled.
### Return value

Current depth test range.
**vec2(0.0f, 1.0f)** - default value
## int getChromaKeyConfigNum () const

Returns the current number of chroma key config indices supported. The maximum index will be count-1.
### Return value

Current number of chroma key config indices.
## void setBlendMaskingMode ( VRMixedReality::BLEND_MASKING_MODE mode = 0 )

***Console*:**`vr_mixed_reality_blend_masking_mode`Sets a new mode of the *Blend Control Mask* that can be used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth.
### Arguments

- *[VRMixedReality::BLEND_MASKING_MODE](../../../api/library/vr/class.vrmixedreality_cpp.md#BLEND_MASKING_MODE)* **mode** - The masking mode. One of the following values:

  - **0** - Disabled (masking mode is disabled). (by default)
  - **1** - Restrict Video to Mask (show the video pass-through image (VST) in the mask; can be used with chroma key)
  - **2** - Restrict VR to Mask (show VR in the mask; can be used with chroma key)
  - **3** - Restrict VR to Chromakey reduced by Mask (show VR in the mask and chroma elsewhere; requires chroma key)

## VRMixedReality::BLEND_MASKING_MODE getBlendMaskingMode () const

***Console*:**`vr_mixed_reality_blend_masking_mode`Returns the current mode of the *Blend Control Mask* that can be used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth.
### Return value

Current masking mode. One of the following values:
- **0** - Disabled (masking mode is disabled). (by default)
- **1** - Restrict Video to Mask (show the video pass-through image (VST) in the mask; can be used with chroma key)
- **2** - Restrict VR to Mask (show VR in the mask; can be used with chroma key)
- **3** - Restrict VR to Chromakey reduced by Mask (show VR in the mask and chroma elsewhere; requires chroma key)

## void setBlendMaskingDebugEnabled ( bool enabled = 0 )

***Console*:**`vr_mixed_reality_blend_masking_debug_enabled`Sets a new value indicating if blend masking debug visualization is enabled. The [blend masking mode](#getBlendMaskingMode_int) must be enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable blend masking debug visualization; **false** - to disable it. The default value is **false**.

## bool isBlendMaskingDebugEnabled () const

***Console*:**`vr_mixed_reality_blend_masking_debug_enabled`Returns the current value indicating if blend masking debug visualization is enabled. The [blend masking mode](#getBlendMaskingMode_int) must be enabled.
### Return value

**true** if blend masking debug visualization is enabled ; otherwise **false**. The default value is **false**.
## bool isBlendMaskingUsed () const

Returns the current value indicating if the *Blend Control Mask* is used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth.
### Return value

**true** if the blend mask is used; otherwise **false**.
## Ptr < Texture > getCurrentBlendMaskColorBuffer () const

Returns the current image representing the current color buffer of the *Blend Control Mask*.
### Return value

Current color buffer.
## void setCameraExposureTimeRaw ( double raw )

Sets a new exposure time value for the camera.
### Arguments

- *double* **raw** - The exposure time, in frames per second (e.g. 90.0 -> ~11ms).

## double getCameraExposureTimeRaw () const

Returns the current exposure time value for the camera.
### Return value

Current exposure time, in frames per second (e.g. 90.0 -> ~11ms).
## void setCameraExposureTime ( VRMixedReality::CAMERA_EXPOSURE_TIME time )

***Console*:**`vr_mixed_reality_camera_exposure_time`Sets a new exposure time value that is valid for the connected device.
### Arguments

- *[VRMixedReality::CAMERA_EXPOSURE_TIME](../../../api/library/vr/class.vrmixedreality_cpp.md#CAMERA_EXPOSURE_TIME)* **time** - The valid exposure time value for the connected device.

## VRMixedReality::CAMERA_EXPOSURE_TIME getCameraExposureTime () const

***Console*:**`vr_mixed_reality_camera_exposure_time`Returns the current exposure time value that is valid for the connected device.
### Return value

Current valid exposure time value for the connected device.

## void setCameraExposureTimeMode ( VRMixedReality::CAMERA_PROPERTY_MODE mode = 1 )

***Console*:**`vr_mixed_reality_camera_exposure_time_mode`Sets a new exposure adjustment mode for the camera.
### Arguments

- *[VRMixedReality::CAMERA_PROPERTY_MODE](../../../api/library/vr/class.vrmixedreality_cpp.md#CAMERA_PROPERTY_MODE)* **mode** - The exposure adjustment mode. One of the following values:

  - **0** - exposure adjustment is disabled
  - **1** - automatic exposure adjustment (by default)
  - **2** - manual exposure adjustment

## VRMixedReality::CAMERA_PROPERTY_MODE getCameraExposureTimeMode () const

***Console*:**`vr_mixed_reality_camera_exposure_time_mode`Returns the current exposure adjustment mode for the camera.
### Return value

Current exposure adjustment mode. One of the following values:
- **0** - exposure adjustment is disabled
- **1** - automatic exposure adjustment (by default)
- **2** - manual exposure adjustment

## void setCameraWhiteBalanceRaw ( int raw )

Sets a new white balance correction value that is valid for the connected device.
### Arguments

- *int* **raw** - The color temperature value.

## int getCameraWhiteBalanceRaw () const

Returns the current white balance correction value that is valid for the connected device.
### Return value

Current color temperature value.
## void setCameraWhiteBalance ( VRMixedReality::CAMERA_WHITE_BALANCE balance )

***Console*:**`vr_mixed_reality_camera_white_balance`Sets a new white balance correction value that is valid for the connected device.
### Arguments

- *[VRMixedReality::CAMERA_WHITE_BALANCE](../../../api/library/vr/class.vrmixedreality_cpp.md#CAMERA_WHITE_BALANCE)* **balance** - The color temperature value.

## VRMixedReality::CAMERA_WHITE_BALANCE getCameraWhiteBalance () const

***Console*:**`vr_mixed_reality_camera_white_balance`Returns the current white balance correction value that is valid for the connected device.
### Return value

Current color temperature value.

## void setCameraWhiteBalanceMode ( VRMixedReality::CAMERA_PROPERTY_MODE mode = 1 )

***Console*:**`vr_mixed_reality_camera_white_balance_mode`Sets a new white balance adjustment mode for the camera.
### Arguments

- *[VRMixedReality::CAMERA_PROPERTY_MODE](../../../api/library/vr/class.vrmixedreality_cpp.md#CAMERA_PROPERTY_MODE)* **mode** - The white balance adjustment mode. One of the following values:

  - **0** - white balance adjustment is disabled
  - **1** - automatic white balance adjustment (by default)
  - **2** - manual white balance adjustment

## VRMixedReality::CAMERA_PROPERTY_MODE getCameraWhiteBalanceMode () const

***Console*:**`vr_mixed_reality_camera_white_balance_mode`Returns the current white balance adjustment mode for the camera.
### Return value

Current white balance adjustment mode. One of the following values:
- **0** - white balance adjustment is disabled
- **1** - automatic white balance adjustment (by default)
- **2** - manual white balance adjustment

## void setCameraISORaw ( int isoraw )

Sets a new ISO value that is valid for the connected device.
### Arguments

- *int* **isoraw** - The ISO value (e.g., "200" -> ISO200).

## int getCameraISORaw () const

Returns the current ISO value that is valid for the connected device.
### Return value

Current ISO value (e.g., "200" -> ISO200).
## void setCameraISO ( VRMixedReality::CAMERA_ISO iso )

***Console*:**`vr_mixed_reality_camera_iso`Sets a new ISO value for the camera.
### Arguments

- *[VRMixedReality::CAMERA_ISO](../../../api/library/vr/class.vrmixedreality_cpp.md#CAMERA_ISO)* **iso** - The ISO value.

## VRMixedReality::CAMERA_ISO getCameraISO () const

***Console*:**`vr_mixed_reality_camera_iso`Returns the current ISO value for the camera.
### Return value

Current ISO value.

## void setCameraISOMode ( VRMixedReality::CAMERA_PROPERTY_MODE isomode = 1 )

***Console*:**`vr_mixed_reality_camera_iso_mode`Sets a new ISO adjustment mode for the camera.
### Arguments

- *[VRMixedReality::CAMERA_PROPERTY_MODE](../../../api/library/vr/class.vrmixedreality_cpp.md#CAMERA_PROPERTY_MODE)* **isomode** - The ISO adjustment mode. One of the following values:

  - **0** - ISO adjustment is disabled
  - **1** - automatic ISO adjustment (by default)
  - **2** - manual ISO adjustment

## VRMixedReality::CAMERA_PROPERTY_MODE getCameraISOMode () const

***Console*:**`vr_mixed_reality_camera_iso_mode`Returns the current ISO adjustment mode for the camera.
### Return value

Current ISO adjustment mode. One of the following values:
- **0** - ISO adjustment is disabled
- **1** - automatic ISO adjustment (by default)
- **2** - manual ISO adjustment

## void setCameraFlickerCompensationRaw ( int raw )

Sets a new flicker compensation value for the camera. This is useful when using the HMD indoors with mostly artificial light bulbs, which flicker at the frequency of 50Hz or 60Hz and can cause visual flicker artifacts on the video see through image. The correct setting depends on the underlying power grid's frequency. For example, in most parts of Africa/Asia/Australia/Europe the frequency is 50 Hz and in most parts of North and South America 60 Hz.
### Arguments

- *int* **raw** - The flicker compensation, in Hz.

## int getCameraFlickerCompensationRaw () const

Returns the current flicker compensation value for the camera. This is useful when using the HMD indoors with mostly artificial light bulbs, which flicker at the frequency of 50Hz or 60Hz and can cause visual flicker artifacts on the video see through image. The correct setting depends on the underlying power grid's frequency. For example, in most parts of Africa/Asia/Australia/Europe the frequency is 50 Hz and in most parts of North and South America 60 Hz.
### Return value

Current flicker compensation, in Hz.
## void setCameraFlickerCompensation ( VRMixedReality::CAMERA_FLICKER_COMPENSATION compensation )

***Console*:**`vr_mixed_reality_camera_flicker_compensation`Sets a new flicker compensation value for the camera. This is useful when using the HMD indoors with mostly artificial light bulbs, which flicker at the frequency of 50Hz or 60Hz and can cause visual flicker artifacts on the video see through image. The correct setting depends on the underlying power grid's frequency. For example, in most parts of Africa/Asia/Australia/Europe the frequency is 50 Hz and in most parts of North and South America 60 Hz.
### Arguments

- *[VRMixedReality::CAMERA_FLICKER_COMPENSATION](../../../api/library/vr/class.vrmixedreality_cpp.md#CAMERA_FLICKER_COMPENSATION)* **compensation** - The flicker compensation.

## VRMixedReality::CAMERA_FLICKER_COMPENSATION getCameraFlickerCompensation () const

***Console*:**`vr_mixed_reality_camera_flicker_compensation`Returns the current flicker compensation value for the camera. This is useful when using the HMD indoors with mostly artificial light bulbs, which flicker at the frequency of 50Hz or 60Hz and can cause visual flicker artifacts on the video see through image. The correct setting depends on the underlying power grid's frequency. For example, in most parts of Africa/Asia/Australia/Europe the frequency is 50 Hz and in most parts of North and South America 60 Hz.
### Return value

Current flicker compensation.

## int getCameraMinSharpness () const

Returns the current minimum possible value for the [camera sharpness](#CameraSharpness).
### Return value

Current minimum possible value for the camera sharpness.
## int getCameraMaxSharpness () const

Returns the current maximum possible value for the [camera sharpness](#CameraSharpness).
### Return value

Current maximum possible value for the camera sharpness.
## void setCameraSharpness ( int sharpness = 0 )

***Console*:**`vr_mixed_reality_camera_sharpness`Sets a new sharpness filter power value for the camera.
### Arguments

- *int* **sharpness** - The sharpness filter power value: lowest value corresponds to small amount of filtering and the highest value corresponds to the largest amount of filtering. Range of values: **[0, 10]**. The default value is : **0**.

## int getCameraSharpness () const

***Console*:**`vr_mixed_reality_camera_sharpness`Returns the current sharpness filter power value for the camera.
### Return value

Current sharpness filter power value: lowest value corresponds to small amount of filtering and the highest value corresponds to the largest amount of filtering.
Range of values: **[0, 10]**. The default value is : **0**.
## void setViewOffset ( float offset = 0.0 )

***Console*:**`vr_mixed_reality_view_offset`Sets a new eyes [view offset](https://developer.varjo.com/docs/apidocs/_varjo__mr_8h.html#a0aa1772b02020977c3c5b1c974848f75) (where eye camera should be positioned when using Mixed Reality):
- **0** for physical eye position
- **1** for VST camera position


### Arguments

- *float* **offset** - The view offset. Range of values: **[0.0, 1.0]**. The default value is : **0.0**.

## float getViewOffset () const

***Console*:**`vr_mixed_reality_view_offset`Returns the current eyes [view offset](https://developer.varjo.com/docs/apidocs/_varjo__mr_8h.html#a0aa1772b02020977c3c5b1c974848f75) (where eye camera should be positioned when using Mixed Reality):
- **0** for physical eye position
- **1** for VST camera position


### Return value

Current view offset.
Range of values: **[0.0, 1.0]**. The default value is : **0.0**.
## void setMarkerTrackingEnabled ( bool enabled = 0 )

***Console*:**`vr_mixed_reality_marker_tracking_enabled`Sets a new value indicating if marker tracking is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable marker tracking; **false** - to disable it. The default value is **false**.

## bool isMarkerTrackingEnabled () const

***Console*:**`vr_mixed_reality_marker_tracking_enabled`Returns the current value indicating if marker tracking is enabled.
### Return value

**true** if marker tracking is enabled ; otherwise **false**. The default value is **false**.
## short getNumMarkerObjectVisible () const

Returns the current number of visible marker objects.
### Return value

Current number of visible marker objects.
## void setCubemapMode ( VRMixedReality::CUBEMAP_MODE mode = 2 )

***Console*:**`vr_mixed_reality_cubemap_mode`Sets a new mode defining the way the AR texture is set for the environment.
### Arguments

- *[VRMixedReality::CUBEMAP_MODE](../../../api/library/vr/class.vrmixedreality_cpp.md#CUBEMAP_MODE)* **mode** - The cubemap mode. One of the following values:

  - **0** - cubemap streaming from AR cameras is disabled.
  - **1** - environment texture substitutes the sky.
  - **2** - the first environment preset defines the way the AR texture is set for the environment. (by default)
  - **3** - the second environment preset defines the way the AR texture is set for the environment.
  - **4** - the third environment preset defines the way the AR texture is set for the environment.

## VRMixedReality::CUBEMAP_MODE getCubemapMode () const

***Console*:**`vr_mixed_reality_cubemap_mode`Returns the current mode defining the way the AR texture is set for the environment.
### Return value

Current cubemap mode. One of the following values:
- **0** - cubemap streaming from AR cameras is disabled.
- **1** - environment texture substitutes the sky.
- **2** - the first environment preset defines the way the AR texture is set for the environment. (by default)
- **3** - the second environment preset defines the way the AR texture is set for the environment.
- **4** - the third environment preset defines the way the AR texture is set for the environment.

## void setCubemapGGXQuality ( Render::GGX_MIPMAPS_QUALITY ggxquality = 1 )

***Console*:**`vr_mixed_reality_cubemap_ggx_quality`Sets a new quality of the generated GGX mips for the AR cubemap.
### Arguments

- *[Render::GGX_MIPMAPS_QUALITY](../../../api/library/rendering/class.render_cpp.md#GGX_MIPMAPS_QUALITY)* **ggxquality** - The quality of the GGX mipmaps. One of the following values:

  - **0** - low
  - **1** - medium (by default)
  - **2** - high
  - **3** - ultra

## Render::GGX_MIPMAPS_QUALITY getCubemapGGXQuality () const

***Console*:**`vr_mixed_reality_cubemap_ggx_quality`Returns the current quality of the generated GGX mips for the AR cubemap.
### Return value

Current quality of the GGX mipmaps. One of the following values:
- **0** - low
- **1** - medium (by default)
- **2** - high
- **3** - ultra

## void setOverrideColorCorrectionMode ( VRMixedReality::OVERRIDE_COLOR_CORRECTION_MODE mode = 0 )

***Console*:**`vr_mixed_reality_override_color_correction_mode`Sets a new color correction mode for the stream from the AR cameras.
### Arguments

- *[VRMixedReality::OVERRIDE_COLOR_CORRECTION_MODE](../../../api/library/vr/class.vrmixedreality_cpp.md#OVERRIDE_COLOR_CORRECTION_MODE)* **mode** - The color correction mode. One of the following values:

  - **0** - correction is disabled. (by default)
  - **1** - exposure correction for the stream from the AR cameras.
  - **2** - exposure and white balance correction for the stream.

## VRMixedReality::OVERRIDE_COLOR_CORRECTION_MODE getOverrideColorCorrectionMode () const

***Console*:**`vr_mixed_reality_override_color_correction_mode`Returns the current color correction mode for the stream from the AR cameras.
### Return value

Current color correction mode. One of the following values:
- **0** - correction is disabled. (by default)
- **1** - exposure correction for the stream from the AR cameras.
- **2** - exposure and white balance correction for the stream.

## static Event<> getEventCameraPropertyUpdateSharpness () const

Event triggered when the sharpness value of the camera is changed in Varjo Base. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CameraPropertyUpdateSharpness event handler
void camerapropertyupdatesharpness_event_handler()
{
	Log::message("\Handling CameraPropertyUpdateSharpness event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdatesharpness_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality::getEventCameraPropertyUpdateSharpness().connect(camerapropertyupdatesharpness_event_connections, camerapropertyupdatesharpness_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality::getEventCameraPropertyUpdateSharpness().connect(camerapropertyupdatesharpness_event_connections, []() {
		Log::message("\Handling CameraPropertyUpdateSharpness event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdatesharpness_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection camerapropertyupdatesharpness_event_connection;

// subscribe to the CameraPropertyUpdateSharpness event with a handler function keeping the connection
VRMixedReality::getEventCameraPropertyUpdateSharpness().connect(camerapropertyupdatesharpness_event_connection, camerapropertyupdatesharpness_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
camerapropertyupdatesharpness_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
camerapropertyupdatesharpness_event_connection.setEnabled(true);

// ...

// remove subscription to the CameraPropertyUpdateSharpness event via the connection
camerapropertyupdatesharpness_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A CameraPropertyUpdateSharpness event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling CameraPropertyUpdateSharpness event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VRMixedReality::getEventCameraPropertyUpdateSharpness().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId camerapropertyupdatesharpness_handler_id;

// subscribe to the CameraPropertyUpdateSharpness event with a lambda handler function and keeping connection ID
camerapropertyupdatesharpness_handler_id = VRMixedReality::getEventCameraPropertyUpdateSharpness().connect(e_connections, []() {
		Log::message("\Handling CameraPropertyUpdateSharpness event (lambda).\n");
	}
);

// remove the subscription later using the ID
VRMixedReality::getEventCameraPropertyUpdateSharpness().disconnect(camerapropertyupdatesharpness_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CameraPropertyUpdateSharpness events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality::getEventCameraPropertyUpdateSharpness().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VRMixedReality::getEventCameraPropertyUpdateSharpness().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventCameraPropertyUpdateFlickerCompensation () const

Event triggered when the flicker compensation value of the camera is changed in Varjo Base. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CameraPropertyUpdateFlickerCompensation event handler
void camerapropertyupdateflickercompensation_event_handler()
{
	Log::message("\Handling CameraPropertyUpdateFlickerCompensation event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdateflickercompensation_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality::getEventCameraPropertyUpdateFlickerCompensation().connect(camerapropertyupdateflickercompensation_event_connections, camerapropertyupdateflickercompensation_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality::getEventCameraPropertyUpdateFlickerCompensation().connect(camerapropertyupdateflickercompensation_event_connections, []() {
		Log::message("\Handling CameraPropertyUpdateFlickerCompensation event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdateflickercompensation_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection camerapropertyupdateflickercompensation_event_connection;

// subscribe to the CameraPropertyUpdateFlickerCompensation event with a handler function keeping the connection
VRMixedReality::getEventCameraPropertyUpdateFlickerCompensation().connect(camerapropertyupdateflickercompensation_event_connection, camerapropertyupdateflickercompensation_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
camerapropertyupdateflickercompensation_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
camerapropertyupdateflickercompensation_event_connection.setEnabled(true);

// ...

// remove subscription to the CameraPropertyUpdateFlickerCompensation event via the connection
camerapropertyupdateflickercompensation_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A CameraPropertyUpdateFlickerCompensation event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling CameraPropertyUpdateFlickerCompensation event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VRMixedReality::getEventCameraPropertyUpdateFlickerCompensation().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId camerapropertyupdateflickercompensation_handler_id;

// subscribe to the CameraPropertyUpdateFlickerCompensation event with a lambda handler function and keeping connection ID
camerapropertyupdateflickercompensation_handler_id = VRMixedReality::getEventCameraPropertyUpdateFlickerCompensation().connect(e_connections, []() {
		Log::message("\Handling CameraPropertyUpdateFlickerCompensation event (lambda).\n");
	}
);

// remove the subscription later using the ID
VRMixedReality::getEventCameraPropertyUpdateFlickerCompensation().disconnect(camerapropertyupdateflickercompensation_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CameraPropertyUpdateFlickerCompensation events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality::getEventCameraPropertyUpdateFlickerCompensation().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VRMixedReality::getEventCameraPropertyUpdateFlickerCompensation().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventCameraPropertyUpdateISO () const

Event triggered when the camera ISO value and/or the ISO adjustment mode are changed in Varjo Base. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CameraPropertyUpdateISO event handler
void camerapropertyupdateiso_event_handler()
{
	Log::message("\Handling CameraPropertyUpdateISO event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdateiso_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality::getEventCameraPropertyUpdateISO().connect(camerapropertyupdateiso_event_connections, camerapropertyupdateiso_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality::getEventCameraPropertyUpdateISO().connect(camerapropertyupdateiso_event_connections, []() {
		Log::message("\Handling CameraPropertyUpdateISO event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdateiso_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection camerapropertyupdateiso_event_connection;

// subscribe to the CameraPropertyUpdateISO event with a handler function keeping the connection
VRMixedReality::getEventCameraPropertyUpdateISO().connect(camerapropertyupdateiso_event_connection, camerapropertyupdateiso_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
camerapropertyupdateiso_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
camerapropertyupdateiso_event_connection.setEnabled(true);

// ...

// remove subscription to the CameraPropertyUpdateISO event via the connection
camerapropertyupdateiso_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A CameraPropertyUpdateISO event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling CameraPropertyUpdateISO event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VRMixedReality::getEventCameraPropertyUpdateISO().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId camerapropertyupdateiso_handler_id;

// subscribe to the CameraPropertyUpdateISO event with a lambda handler function and keeping connection ID
camerapropertyupdateiso_handler_id = VRMixedReality::getEventCameraPropertyUpdateISO().connect(e_connections, []() {
		Log::message("\Handling CameraPropertyUpdateISO event (lambda).\n");
	}
);

// remove the subscription later using the ID
VRMixedReality::getEventCameraPropertyUpdateISO().disconnect(camerapropertyupdateiso_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CameraPropertyUpdateISO events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality::getEventCameraPropertyUpdateISO().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VRMixedReality::getEventCameraPropertyUpdateISO().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventCameraPropertyUpdateWhiteBalance () const

Event triggered when the white balance correction value of the camera and/or the white balance adjustment mode are changed in Varjo Base. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CameraPropertyUpdateWhiteBalance event handler
void camerapropertyupdatewhitebalance_event_handler()
{
	Log::message("\Handling CameraPropertyUpdateWhiteBalance event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdatewhitebalance_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality::getEventCameraPropertyUpdateWhiteBalance().connect(camerapropertyupdatewhitebalance_event_connections, camerapropertyupdatewhitebalance_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality::getEventCameraPropertyUpdateWhiteBalance().connect(camerapropertyupdatewhitebalance_event_connections, []() {
		Log::message("\Handling CameraPropertyUpdateWhiteBalance event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdatewhitebalance_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection camerapropertyupdatewhitebalance_event_connection;

// subscribe to the CameraPropertyUpdateWhiteBalance event with a handler function keeping the connection
VRMixedReality::getEventCameraPropertyUpdateWhiteBalance().connect(camerapropertyupdatewhitebalance_event_connection, camerapropertyupdatewhitebalance_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
camerapropertyupdatewhitebalance_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
camerapropertyupdatewhitebalance_event_connection.setEnabled(true);

// ...

// remove subscription to the CameraPropertyUpdateWhiteBalance event via the connection
camerapropertyupdatewhitebalance_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A CameraPropertyUpdateWhiteBalance event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling CameraPropertyUpdateWhiteBalance event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VRMixedReality::getEventCameraPropertyUpdateWhiteBalance().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId camerapropertyupdatewhitebalance_handler_id;

// subscribe to the CameraPropertyUpdateWhiteBalance event with a lambda handler function and keeping connection ID
camerapropertyupdatewhitebalance_handler_id = VRMixedReality::getEventCameraPropertyUpdateWhiteBalance().connect(e_connections, []() {
		Log::message("\Handling CameraPropertyUpdateWhiteBalance event (lambda).\n");
	}
);

// remove the subscription later using the ID
VRMixedReality::getEventCameraPropertyUpdateWhiteBalance().disconnect(camerapropertyupdatewhitebalance_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CameraPropertyUpdateWhiteBalance events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality::getEventCameraPropertyUpdateWhiteBalance().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VRMixedReality::getEventCameraPropertyUpdateWhiteBalance().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventCameraPropertyUpdateExposureTime () const

Event triggered when the exposure time value of the camera and/or the exposure adjustment mode are changed in Varjo Base. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CameraPropertyUpdateExposureTime event handler
void camerapropertyupdateexposuretime_event_handler()
{
	Log::message("\Handling CameraPropertyUpdateExposureTime event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdateexposuretime_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality::getEventCameraPropertyUpdateExposureTime().connect(camerapropertyupdateexposuretime_event_connections, camerapropertyupdateexposuretime_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality::getEventCameraPropertyUpdateExposureTime().connect(camerapropertyupdateexposuretime_event_connections, []() {
		Log::message("\Handling CameraPropertyUpdateExposureTime event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdateexposuretime_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection camerapropertyupdateexposuretime_event_connection;

// subscribe to the CameraPropertyUpdateExposureTime event with a handler function keeping the connection
VRMixedReality::getEventCameraPropertyUpdateExposureTime().connect(camerapropertyupdateexposuretime_event_connection, camerapropertyupdateexposuretime_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
camerapropertyupdateexposuretime_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
camerapropertyupdateexposuretime_event_connection.setEnabled(true);

// ...

// remove subscription to the CameraPropertyUpdateExposureTime event via the connection
camerapropertyupdateexposuretime_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A CameraPropertyUpdateExposureTime event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling CameraPropertyUpdateExposureTime event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VRMixedReality::getEventCameraPropertyUpdateExposureTime().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId camerapropertyupdateexposuretime_handler_id;

// subscribe to the CameraPropertyUpdateExposureTime event with a lambda handler function and keeping connection ID
camerapropertyupdateexposuretime_handler_id = VRMixedReality::getEventCameraPropertyUpdateExposureTime().connect(e_connections, []() {
		Log::message("\Handling CameraPropertyUpdateExposureTime event (lambda).\n");
	}
);

// remove the subscription later using the ID
VRMixedReality::getEventCameraPropertyUpdateExposureTime().disconnect(camerapropertyupdateexposuretime_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CameraPropertyUpdateExposureTime events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality::getEventCameraPropertyUpdateExposureTime().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VRMixedReality::getEventCameraPropertyUpdateExposureTime().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventChromakeyUpdate () const

Event triggered when the chroma keying settings are changed in Varjo Base. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ChromakeyUpdate event handler
void chromakeyupdate_event_handler()
{
	Log::message("\Handling ChromakeyUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections chromakeyupdate_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality::getEventChromakeyUpdate().connect(chromakeyupdate_event_connections, chromakeyupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality::getEventChromakeyUpdate().connect(chromakeyupdate_event_connections, []() {
		Log::message("\Handling ChromakeyUpdate event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
chromakeyupdate_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection chromakeyupdate_event_connection;

// subscribe to the ChromakeyUpdate event with a handler function keeping the connection
VRMixedReality::getEventChromakeyUpdate().connect(chromakeyupdate_event_connection, chromakeyupdate_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
chromakeyupdate_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
chromakeyupdate_event_connection.setEnabled(true);

// ...

// remove subscription to the ChromakeyUpdate event via the connection
chromakeyupdate_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A ChromakeyUpdate event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling ChromakeyUpdate event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VRMixedReality::getEventChromakeyUpdate().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId chromakeyupdate_handler_id;

// subscribe to the ChromakeyUpdate event with a lambda handler function and keeping connection ID
chromakeyupdate_handler_id = VRMixedReality::getEventChromakeyUpdate().connect(e_connections, []() {
		Log::message("\Handling ChromakeyUpdate event (lambda).\n");
	}
);

// remove the subscription later using the ID
VRMixedReality::getEventChromakeyUpdate().disconnect(chromakeyupdate_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ChromakeyUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality::getEventChromakeyUpdate().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VRMixedReality::getEventChromakeyUpdate().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventDeviceDisconnected () const

Event triggered when the Varjo device is disconnected. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the DeviceDisconnected event handler
void devicedisconnected_event_handler()
{
	Log::message("\Handling DeviceDisconnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections devicedisconnected_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality::getEventDeviceDisconnected().connect(devicedisconnected_event_connections, devicedisconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality::getEventDeviceDisconnected().connect(devicedisconnected_event_connections, []() {
		Log::message("\Handling DeviceDisconnected event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
devicedisconnected_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection devicedisconnected_event_connection;

// subscribe to the DeviceDisconnected event with a handler function keeping the connection
VRMixedReality::getEventDeviceDisconnected().connect(devicedisconnected_event_connection, devicedisconnected_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
devicedisconnected_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
devicedisconnected_event_connection.setEnabled(true);

// ...

// remove subscription to the DeviceDisconnected event via the connection
devicedisconnected_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A DeviceDisconnected event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling DeviceDisconnected event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VRMixedReality::getEventDeviceDisconnected().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId devicedisconnected_handler_id;

// subscribe to the DeviceDisconnected event with a lambda handler function and keeping connection ID
devicedisconnected_handler_id = VRMixedReality::getEventDeviceDisconnected().connect(e_connections, []() {
		Log::message("\Handling DeviceDisconnected event (lambda).\n");
	}
);

// remove the subscription later using the ID
VRMixedReality::getEventDeviceDisconnected().disconnect(devicedisconnected_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all DeviceDisconnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality::getEventDeviceDisconnected().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VRMixedReality::getEventDeviceDisconnected().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventDeviceConnected () const

Event triggered when the Varjo device is connected. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the DeviceConnected event handler
void deviceconnected_event_handler()
{
	Log::message("\Handling DeviceConnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections deviceconnected_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality::getEventDeviceConnected().connect(deviceconnected_event_connections, deviceconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality::getEventDeviceConnected().connect(deviceconnected_event_connections, []() {
		Log::message("\Handling DeviceConnected event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
deviceconnected_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection deviceconnected_event_connection;

// subscribe to the DeviceConnected event with a handler function keeping the connection
VRMixedReality::getEventDeviceConnected().connect(deviceconnected_event_connection, deviceconnected_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
deviceconnected_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
deviceconnected_event_connection.setEnabled(true);

// ...

// remove subscription to the DeviceConnected event via the connection
deviceconnected_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A DeviceConnected event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling DeviceConnected event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VRMixedReality::getEventDeviceConnected().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId deviceconnected_handler_id;

// subscribe to the DeviceConnected event with a lambda handler function and keeping connection ID
deviceconnected_handler_id = VRMixedReality::getEventDeviceConnected().connect(e_connections, []() {
		Log::message("\Handling DeviceConnected event (lambda).\n");
	}
);

// remove the subscription later using the ID
VRMixedReality::getEventDeviceConnected().disconnect(deviceconnected_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all DeviceConnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality::getEventDeviceConnected().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VRMixedReality::getEventDeviceConnected().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<> getEventCameraPropertyUpdateVSTReprojection () const

Event triggered when the camera VST reprojection property is updated. You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CameraPropertyUpdateVSTReprojection event handler
void camerapropertyupdatevstreprojection_event_handler()
{
	Log::message("\Handling CameraPropertyUpdateVSTReprojection event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdatevstreprojection_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality::getEventCameraPropertyUpdateVSTReprojection().connect(camerapropertyupdatevstreprojection_event_connections, camerapropertyupdatevstreprojection_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality::getEventCameraPropertyUpdateVSTReprojection().connect(camerapropertyupdatevstreprojection_event_connections, []() {
		Log::message("\Handling CameraPropertyUpdateVSTReprojection event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdatevstreprojection_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection camerapropertyupdatevstreprojection_event_connection;

// subscribe to the CameraPropertyUpdateVSTReprojection event with a handler function keeping the connection
VRMixedReality::getEventCameraPropertyUpdateVSTReprojection().connect(camerapropertyupdatevstreprojection_event_connection, camerapropertyupdatevstreprojection_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
camerapropertyupdatevstreprojection_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
camerapropertyupdatevstreprojection_event_connection.setEnabled(true);

// ...

// remove subscription to the CameraPropertyUpdateVSTReprojection event via the connection
camerapropertyupdatevstreprojection_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A CameraPropertyUpdateVSTReprojection event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling CameraPropertyUpdateVSTReprojection event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VRMixedReality::getEventCameraPropertyUpdateVSTReprojection().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId camerapropertyupdatevstreprojection_handler_id;

// subscribe to the CameraPropertyUpdateVSTReprojection event with a lambda handler function and keeping connection ID
camerapropertyupdatevstreprojection_handler_id = VRMixedReality::getEventCameraPropertyUpdateVSTReprojection().connect(e_connections, []() {
		Log::message("\Handling CameraPropertyUpdateVSTReprojection event (lambda).\n");
	}
);

// remove the subscription later using the ID
VRMixedReality::getEventCameraPropertyUpdateVSTReprojection().disconnect(camerapropertyupdatevstreprojection_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CameraPropertyUpdateVSTReprojection events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality::getEventCameraPropertyUpdateVSTReprojection().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VRMixedReality::getEventCameraPropertyUpdateVSTReprojection().setEnabled(true);

```

</details>

### Return value

Event instance.
## void setCameraVSTReprojectionMode ( VRMixedReality::CAMERA_PROPERTY_MODE mode = 0 )

***Console*:**`vr_mixed_reality_camera_vst_reprojection_mode`Sets a new reprojection mode of VST.
### Arguments

- *[VRMixedReality::CAMERA_PROPERTY_MODE](../../../api/library/vr/class.vrmixedreality_cpp.md#CAMERA_PROPERTY_MODE)* **mode** - The reprojection mode of VST. One of the following values:

  - **0** - reprojection of VST is disabled (default). (by default)
  - **1** - automatic reprojection mode of VST (the Depth buffer is used for reprojection)
  - **2** - manual reprojections mode of VST

## VRMixedReality::CAMERA_PROPERTY_MODE getCameraVSTReprojectionMode () const

***Console*:**`vr_mixed_reality_camera_vst_reprojection_mode`Returns the current reprojection mode of VST.
### Return value

Current reprojection mode of VST. One of the following values:
- **0** - reprojection of VST is disabled (default). (by default)
- **1** - automatic reprojection mode of VST (the Depth buffer is used for reprojection)
- **2** - manual reprojections mode of VST

## void setCameraVSTReprojectionDistance ( float distance = 0.0f )

***Console*:**`vr_mixed_reality_camera_vst_reprojection_distance`Sets a new static distance in meters used to shift the whole image. Is configured only if the [VST reprojection mode](#CameraVSTReprojectionMode) is set to [Manual](#CAMERA_PROPERTY_MODE_MANUAL).
### Arguments

- *float* **distance** - The static distance in meters used to control VST reprojection. Range of values: **[0.0f, 1000.0f]**. The default value is : **0.0f**.

## float getCameraVSTReprojectionDistance () const

***Console*:**`vr_mixed_reality_camera_vst_reprojection_distance`Returns the current static distance in meters used to shift the whole image. Is configured only if the [VST reprojection mode](#CameraVSTReprojectionMode) is set to [Manual](#CAMERA_PROPERTY_MODE_MANUAL).
### Return value

Current static distance in meters used to control VST reprojection.
Range of values: **[0.0f, 1000.0f]**. The default value is : **0.0f**.
---

## void applySettings ( )

Updates the mixed reality settings to the current settings.
## bool isChromaKeyConfigEnabled ( int index ) const

Returns the current value indicating if the chroma key configuration with the specified index is enabled.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

1 the chroma key configuration is enabled; otherwise, 0.
## void setChromaKeyConfigEnabled ( int index , bool enabled )

Sets a new value indicating if the chroma key configuration with the specified index is enabled.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *bool* **enabled** - 1 to enable the chroma key configuration; 0 to disable it.

## Math:: vec3 getChromaKeyConfigFalloff ( int index ) const

Returns the current tolerance falloff values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

Current tolerance falloff values for HSV components of the chroma key target color. The range for each component is [0.0; 1.0].
## void setChromaKeyConfigFalloff ( int index , const Math:: vec3 & falloff )

Sets new tolerance falloff values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **falloff** - New tolerance falloff values to be set for HSV components of the chroma key target color. The range for each component is [0.0; 1.0].

## Math:: vec3 getChromaKeyConfigTargetColor ( int index ) const

Returns the current chroma key target color in HSV color model.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

Current chroma key target color in HSV color model. The range for each component is [0.0; 1.0].
## void setChromaKeyConfigTargetColor ( int index , const Math:: vec3 & target_color )

Sets a new chroma key target color in HSV color model.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **target_color** - New chroma key target color to be set in HSV color model. The range for each component is [0.0; 1.0].

## Math:: vec3 getChromaKeyConfigTolerance ( int index ) const

Returns the current tolerance values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

Current tolerance values for HSV components of the chroma key target color. The range for each component is [0.0; 1.0].
## void setChromaKeyConfigTolerance ( int index , const Math:: vec3 & tolerance )

Sets new tolerance values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **tolerance** - New tolerance values for HSV components of the chroma key target color to be set. The range for each component is [0.0; 1.0].

## void applyChromaKeySettings ( int index ) const

Updates the settings of the chroma key configuration with the specified index to the current settings.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

## Vector <double> getCameraSupportedRawExposureTimes ( ) const

Returns a vector containing the exposure time values that are set as valid for the connected device.
### Return value

The vector containing the exposure time values.
## Vector <int> getCameraSupportedRawWhiteBalances ( ) const

Returns a vector containing the white balance values that are set as valid for the connected device.
### Return value

The vector containing the white balance values.
## Vector <int> getCameraSupportedRawISO ( ) const

Returns a vector containing the ISO values that are set as valid for the connected device.
### Return value

The vector containing the ISO values.
## Vector <int> getCameraSupportedRawFlickerCompensations ( ) const

Returns a vector containing the flicker compensation values that are set as valid for the connected device.
### Return value

The vector containing the flicker compensation values.
## Ptr < VRMarkerObject > getMarkerObject ( short index ) const

Returns the marker object with the specified index.
### Arguments

- *short* **index** - Marker object index.

### Return value

Marker object.
## Ptr < VRMarkerObject > getMarkerObjectByID ( short marker_id ) const

Returns the marker object with the specified ID.
### Arguments

- *short* **marker_id** - Marker object ID.

### Return value

Marker object.
## bool cameraConfigLock ( ) const

Returns the value indicating whether the attempt to lock the camera config is successful.
### Return value

**true** if the camera config is locked successfully or it was already locked; otherwise, **false**.
## void cameraConfigUnlock ( ) const

Unlocks the previously locked camera config.
## bool hasFeatureChromakey ( ) const

Returns a value indicating if chroma key blending is available for mixed reality composition.
### Return value

true if chroma key blending is available; otherwise, false.
## bool hasFeatureAlphaBlend ( ) const

Returns a value indicating if alpha blending is supported for mixing real and virtual images.
### Return value

true if alpha blending is supported; otherwise, false.
## bool hasFeatureDepthTest ( ) const

Returns a value indicating if depth testing is available for mixing of real and virtual content based on depth occlusion.
### Return value

true if depth testing is available; otherwise, false.
## bool hasFeatureDepthTestRange ( ) const

Returns a value indicating if configurable depth testing range is supported.
### Return value

true if configurable depth testing range is supported; otherwise, false.
## bool hasFeatureBlendmasking ( ) const

Returns a value indicating if blend masking is supported in mixed reality.
### Return value

true if blend masking is supported; otherwise, false.
## bool hasFeatureCameraProperties ( ) const

Returns a value indicating if access to real-world camera properties is supported (e.g., white balance, ISO, shutter speed, etc.).
### Return value

true if access to real-world camera properties is supported; otherwise, false.
## bool hasFeatureMarkerTracking ( ) const

Returns a value indicating if marker-based spatial tracking is supported.
### Return value

true if marker-based spatial tracking is supported; otherwise, false.
## bool hasFeatureViewOffset ( ) const

Returns a value indicating if per-eye view offset is supported for manual aligning virtual content with passthrough imagery.
### Return value

true if per-eye view offset is supported; otherwise, false.
## bool hasFeatureColorCorrection ( ) const

Returns a value indicating if color correction feature is supported.
### Return value

true if color correction feature is supported; otherwise, false.
## bool hasFeatureEnvironmentCubemap ( ) const

Returns a value indicating if the environment cubemap feature is supported.
### Return value

true if the environment cubemap feature is supported; otherwise, false.
