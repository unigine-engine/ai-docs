# Unigine.VRMixedReality Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The class is used for mixed reality management on compatible head-mounted displays (HMDs) that support mixed reality and operate on **Varjo** or **OpenXR** backends.


When using the **Varjo** backend, all features of this class are available. Under **OpenXR**, mixed reality support is limited. Use the *[hasFeature...()()](../../...md#hasFeatureAlphaBlend_int)* methods to check which features and corresponding methods of this class are supported specifically for your device and backend configuration.


## VRMixedReality Class

### Members

## int isAvailable () const

Returns the current value indicating if mixed reality is available on the active VR device, and is supported at runtime.
### Return value

Current mixed reality is available
## void setChromaKeyEnabled ( int enabled = 0 )

***Console*:**`vr_mixed_reality_chroma_key_enabled`Sets a new value indicating if chroma keying is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled.
### Arguments

- *int* **enabled** - The chroma keying The default value is **false**.

## int isChromaKeyEnabled () const

***Console*:**`vr_mixed_reality_chroma_key_enabled`Returns the current value indicating if chroma keying is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled.
### Return value

Current chroma keying The default value is **false**.
## void setDepthTestEnabled ( int enabled = 0 )

***Console*:**`vr_mixed_reality_depth_test_enabled`Sets a new value indicating if depth buffer submission is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled.
### Arguments

- *int* **enabled** - The depth testing The default value is **false**.

## int isDepthTestEnabled () const

***Console*:**`vr_mixed_reality_depth_test_enabled`Returns the current value indicating if depth buffer submission is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled.
### Return value

Current depth testing The default value is **false**.
## void setAlphaBlendEnabled ( int enabled = 0 )

***Console*:**`vr_mixed_reality_alpha_blend_enabled`Sets a new value indicating if alpha blending is enabled. This option is used for blending VR and AR images using the alpha channel. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled and the [screen precision](../../../api/library/rendering/class.render_usc.md#isScreenPrecision_int) must be 1.
### Arguments

- *int* **enabled** - The alpha blending The default value is **false**.

## int isAlphaBlendEnabled () const

***Console*:**`vr_mixed_reality_alpha_blend_enabled`Returns the current value indicating if alpha blending is enabled. This option is used for blending VR and AR images using the alpha channel. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled and the [screen precision](../../../api/library/rendering/class.render_usc.md#isScreenPrecision_int) must be 1.
### Return value

Current alpha blending The default value is **false**.
## void setVideoEnabled ( int enabled = 0 )

***Console*:**`vr_mixed_reality_video_enabled`Sets a new value indicating if the video signal from the real-world view from the front-facing HMD-mounted cameras is enabled. The real-world view is used for combining virtual and real-world elements to create an immersive experience in mixed reality.
### Arguments

- *int* **enabled** - The the real-world view from the front-facing HMD-mounted cameras The default value is **false**.

## int isVideoEnabled () const

***Console*:**`vr_mixed_reality_video_enabled`Returns the current value indicating if the video signal from the real-world view from the front-facing HMD-mounted cameras is enabled. The real-world view is used for combining virtual and real-world elements to create an immersive experience in mixed reality.
### Return value

Current the real-world view from the front-facing HMD-mounted cameras The default value is **false**.
## void setDepthTestRangeEnabled ( int enabled = 0 )

***Console*:**`vr_mixed_reality_depth_test_range_enabled`Sets a new value indicating if the depth test range usage is enabled. Use the [depth test range](#getDepthTestRange_vec2) (*Depth Test Near Z*, *Depth Test Far Z*) to control the range for which the depth test is evaluated.
### Arguments

- *int* **enabled** - The the depth test range The default value is **false**.

## int isDepthTestRangeEnabled () const

***Console*:**`vr_mixed_reality_depth_test_range_enabled`Returns the current value indicating if the depth test range usage is enabled. Use the [depth test range](#getDepthTestRange_vec2) (*Depth Test Near Z*, *Depth Test Far Z*) to control the range for which the depth test is evaluated.
### Return value

Current the depth test range The default value is **false**.
## void setDepthTestRange ( vec2 range )

***Console*:**`vr_mixed_reality_depth_test_range`Sets a new depth test range as a two-component vector (the near and far planes). The [depth test range usage](#isDepthTestRangeEnabled_int) must be enabled.
### Arguments

- *vec2* **range** - The depth test range. **vec2(0.0f, 1.0f)** - default value

## vec2 getDepthTestRange () const

***Console*:**`vr_mixed_reality_depth_test_range`Returns the current depth test range as a two-component vector (the near and far planes). The [depth test range usage](#isDepthTestRangeEnabled_int) must be enabled.
### Return value

Current depth test range.
**vec2(0.0f, 1.0f)** - default value
## int getChromaKeyConfigNum () const

Returns the current number of chroma key config indices supported. The maximum index will be count-1.
### Return value

Current number of chroma key config indices.
## void setBlendMaskingMode ( int mode = 0 )

***Console*:**`vr_mixed_reality_blend_masking_mode`Sets a new mode of the *Blend Control Mask* that can be used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth.
### Arguments

- *int* **mode** - The masking mode. One of the following values:

  - **0** - Disabled (masking mode is disabled). (by default)
  - **1** - Restrict Video to Mask (show the video pass-through image (VST) in the mask; can be used with chroma key)
  - **2** - Restrict VR to Mask (show VR in the mask; can be used with chroma key)
  - **3** - Restrict VR to Chromakey reduced by Mask (show VR in the mask and chroma elsewhere; requires chroma key)

## int getBlendMaskingMode () const

***Console*:**`vr_mixed_reality_blend_masking_mode`Returns the current mode of the *Blend Control Mask* that can be used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth.
### Return value

Current masking mode. One of the following values:
- **0** - Disabled (masking mode is disabled). (by default)
- **1** - Restrict Video to Mask (show the video pass-through image (VST) in the mask; can be used with chroma key)
- **2** - Restrict VR to Mask (show VR in the mask; can be used with chroma key)
- **3** - Restrict VR to Chromakey reduced by Mask (show VR in the mask and chroma elsewhere; requires chroma key)

## void setBlendMaskingDebugEnabled ( int enabled = 0 )

***Console*:**`vr_mixed_reality_blend_masking_debug_enabled`Sets a new value indicating if blend masking debug visualization is enabled. The [blend masking mode](#getBlendMaskingMode_int) must be enabled.
### Arguments

- *int* **enabled** - The blend masking debug visualization The default value is **false**.

## int isBlendMaskingDebugEnabled () const

***Console*:**`vr_mixed_reality_blend_masking_debug_enabled`Returns the current value indicating if blend masking debug visualization is enabled. The [blend masking mode](#getBlendMaskingMode_int) must be enabled.
### Return value

Current blend masking debug visualization The default value is **false**.
## int isBlendMaskingUsed () const

Returns the current value indicating if the *Blend Control Mask* is used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth.
### Return value

Current the blend mask is used
## Texture getCurrentBlendMaskColorBuffer () const

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
## void setCameraExposureTime ( int time )

***Console*:**`vr_mixed_reality_camera_exposure_time`Sets a new exposure time value that is valid for the connected device.
### Arguments

- *int* **time** - The valid exposure time value for the connected device.

## int getCameraExposureTime () const

***Console*:**`vr_mixed_reality_camera_exposure_time`Returns the current exposure time value that is valid for the connected device.
### Return value

Current valid exposure time value for the connected device.

## void setCameraExposureTimeMode ( int mode = 1 )

***Console*:**`vr_mixed_reality_camera_exposure_time_mode`Sets a new exposure adjustment mode for the camera.
### Arguments

- *int* **mode** - The exposure adjustment mode. One of the following values:

  - **0** - exposure adjustment is disabled
  - **1** - automatic exposure adjustment (by default)
  - **2** - manual exposure adjustment

## int getCameraExposureTimeMode () const

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
## void setCameraWhiteBalance ( int balance )

***Console*:**`vr_mixed_reality_camera_white_balance`Sets a new white balance correction value that is valid for the connected device.
### Arguments

- *int* **balance** - The color temperature value.

## int getCameraWhiteBalance () const

***Console*:**`vr_mixed_reality_camera_white_balance`Returns the current white balance correction value that is valid for the connected device.
### Return value

Current color temperature value.

## void setCameraWhiteBalanceMode ( int mode = 1 )

***Console*:**`vr_mixed_reality_camera_white_balance_mode`Sets a new white balance adjustment mode for the camera.
### Arguments

- *int* **mode** - The white balance adjustment mode. One of the following values:

  - **0** - white balance adjustment is disabled
  - **1** - automatic white balance adjustment (by default)
  - **2** - manual white balance adjustment

## int getCameraWhiteBalanceMode () const

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
## void setCameraISO ( int iso )

***Console*:**`vr_mixed_reality_camera_iso`Sets a new ISO value for the camera.
### Arguments

- *int* **iso** - The ISO value.

## int getCameraISO () const

***Console*:**`vr_mixed_reality_camera_iso`Returns the current ISO value for the camera.
### Return value

Current ISO value.

## void setCameraISOMode ( int isomode = 1 )

***Console*:**`vr_mixed_reality_camera_iso_mode`Sets a new ISO adjustment mode for the camera.
### Arguments

- *int* **isomode** - The ISO adjustment mode. One of the following values:

  - **0** - ISO adjustment is disabled
  - **1** - automatic ISO adjustment (by default)
  - **2** - manual ISO adjustment

## int getCameraISOMode () const

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
## void setCameraFlickerCompensation ( int compensation )

***Console*:**`vr_mixed_reality_camera_flicker_compensation`Sets a new flicker compensation value for the camera. This is useful when using the HMD indoors with mostly artificial light bulbs, which flicker at the frequency of 50Hz or 60Hz and can cause visual flicker artifacts on the video see through image. The correct setting depends on the underlying power grid's frequency. For example, in most parts of Africa/Asia/Australia/Europe the frequency is 50 Hz and in most parts of North and South America 60 Hz.
### Arguments

- *int* **compensation** - The flicker compensation.

## int getCameraFlickerCompensation () const

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
## void setMarkerTrackingEnabled ( int enabled = 0 )

***Console*:**`vr_mixed_reality_marker_tracking_enabled`Sets a new value indicating if marker tracking is enabled.
### Arguments

- *int* **enabled** - The marker tracking The default value is **false**.

## int isMarkerTrackingEnabled () const

***Console*:**`vr_mixed_reality_marker_tracking_enabled`Returns the current value indicating if marker tracking is enabled.
### Return value

Current marker tracking The default value is **false**.
## short getNumMarkerObjectVisible () const

Returns the current number of visible marker objects.
### Return value

Current number of visible marker objects.
## void setCubemapMode ( int mode = 2 )

***Console*:**`vr_mixed_reality_cubemap_mode`Sets a new mode defining the way the AR texture is set for the environment.
### Arguments

- *int* **mode** - The cubemap mode. One of the following values:

  - **0** - cubemap streaming from AR cameras is disabled.
  - **1** - environment texture substitutes the sky.
  - **2** - the first environment preset defines the way the AR texture is set for the environment. (by default)
  - **3** - the second environment preset defines the way the AR texture is set for the environment.
  - **4** - the third environment preset defines the way the AR texture is set for the environment.

## int getCubemapMode () const

***Console*:**`vr_mixed_reality_cubemap_mode`Returns the current mode defining the way the AR texture is set for the environment.
### Return value

Current cubemap mode. One of the following values:
- **0** - cubemap streaming from AR cameras is disabled.
- **1** - environment texture substitutes the sky.
- **2** - the first environment preset defines the way the AR texture is set for the environment. (by default)
- **3** - the second environment preset defines the way the AR texture is set for the environment.
- **4** - the third environment preset defines the way the AR texture is set for the environment.

## void setCubemapGGXQuality ( int ggxquality = 1 )

***Console*:**`vr_mixed_reality_cubemap_ggx_quality`Sets a new quality of the generated GGX mips for the AR cubemap.
### Arguments

- *int* **ggxquality** - The quality of the GGX mipmaps. One of the following values:

  - **0** - low
  - **1** - medium (by default)
  - **2** - high
  - **3** - ultra

## int getCubemapGGXQuality () const

***Console*:**`vr_mixed_reality_cubemap_ggx_quality`Returns the current quality of the generated GGX mips for the AR cubemap.
### Return value

Current quality of the GGX mipmaps. One of the following values:
- **0** - low
- **1** - medium (by default)
- **2** - high
- **3** - ultra

## void setOverrideColorCorrectionMode ( int mode = 0 )

***Console*:**`vr_mixed_reality_override_color_correction_mode`Sets a new color correction mode for the stream from the AR cameras.
### Arguments

- *int* **mode** - The color correction mode. One of the following values:

  - **0** - correction is disabled. (by default)
  - **1** - exposure correction for the stream from the AR cameras.
  - **2** - exposure and white balance correction for the stream.

## int getOverrideColorCorrectionMode () const

***Console*:**`vr_mixed_reality_override_color_correction_mode`Returns the current color correction mode for the stream from the AR cameras.
### Return value

Current color correction mode. One of the following values:
- **0** - correction is disabled. (by default)
- **1** - exposure correction for the stream from the AR cameras.
- **2** - exposure and white balance correction for the stream.

## static getEventCameraPropertyUpdateSharpness () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventCameraPropertyUpdateFlickerCompensation () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventCameraPropertyUpdateISO () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventCameraPropertyUpdateWhiteBalance () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventCameraPropertyUpdateExposureTime () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventChromakeyUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventDeviceDisconnected () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventDeviceConnected () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventCameraPropertyUpdateVSTReprojection () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## void setCameraVSTReprojectionMode ( )

***Console*:**`vr_mixed_reality_camera_vst_reprojection_mode`Sets a new reprojection mode of VST.
### Arguments

- **mode** - The reprojection mode of VST. One of the following values:

  - **0** - reprojection of VST is disabled (default). (by default)
  - **1** - automatic reprojection mode of VST (the Depth buffer is used for reprojection)
  - **2** - manual reprojections mode of VST

## getCameraVSTReprojectionMode () const

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

## void engine.vr_mixed_reality. applySettings ( )

Updates the mixed reality settings to the current settings.
## int engine.vr_mixed_reality. isChromaKeyConfigEnabled ( int index )

Returns the current value indicating if the chroma key configuration with the specified index is enabled.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

1 the chroma key configuration is enabled; otherwise, 0.
## void engine.vr_mixed_reality. setChromaKeyConfigEnabled ( int index , int enabled )

Sets a new value indicating if the chroma key configuration with the specified index is enabled.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *int* **enabled** - 1 to enable the chroma key configuration; 0 to disable it.

## vec3 engine.vr_mixed_reality. getChromaKeyConfigFalloff ( int index )

Returns the current tolerance falloff values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

Current tolerance falloff values for HSV components of the chroma key target color. The range for each component is [0.0; 1.0].
## void engine.vr_mixed_reality. setChromaKeyConfigFalloff ( int index , const vec3 & falloff )

Sets new tolerance falloff values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *const vec3 &* **falloff** - New tolerance falloff values to be set for HSV components of the chroma key target color. The range for each component is [0.0; 1.0].

## vec3 engine.vr_mixed_reality. getChromaKeyConfigTargetColor ( int index )

Returns the current chroma key target color in HSV color model.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

Current chroma key target color in HSV color model. The range for each component is [0.0; 1.0].
## void engine.vr_mixed_reality. setChromaKeyConfigTargetColor ( int index , const vec3 & target_color )

Sets a new chroma key target color in HSV color model.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *const vec3 &* **target_color** - New chroma key target color to be set in HSV color model. The range for each component is [0.0; 1.0].

## vec3 engine.vr_mixed_reality. getChromaKeyConfigTolerance ( int index )

Returns the current tolerance values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

Current tolerance values for HSV components of the chroma key target color. The range for each component is [0.0; 1.0].
## void engine.vr_mixed_reality. setChromaKeyConfigTolerance ( int index , const vec3 & tolerance )

Sets new tolerance values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *const vec3 &* **tolerance** - New tolerance values for HSV components of the chroma key target color to be set. The range for each component is [0.0; 1.0].

## void engine.vr_mixed_reality. applyChromaKeySettings ( int index )

Updates the settings of the chroma key configuration with the specified index to the current settings.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

## engine.vr_mixed_reality. getCameraSupportedRawISO ( )

Returns a vector containing the ISO values that are set as valid for the connected device.
### Return value

The vector containing the ISO values.
## VRMarkerObject engine.vr_mixed_reality. getMarkerObject ( short index )

Returns the marker object with the specified index.
### Arguments

- *short* **index** - Marker object index.

### Return value

Marker object.
## VRMarkerObject engine.vr_mixed_reality. getMarkerObjectByID ( short marker_id )

Returns the marker object with the specified ID.
### Arguments

- *short* **marker_id** - Marker object ID.

### Return value

Marker object.
## bool engine.vr_mixed_reality. cameraConfigLock ( )

Returns the value indicating whether the attempt to lock the camera config is successful.
### Return value

**true** if the camera config is locked successfully or it was already locked; otherwise, **false**.
## void engine.vr_mixed_reality. cameraConfigUnlock ( )

Unlocks the previously locked camera config.
## int engine.vr_mixed_reality. hasFeatureChromakey ( )

Returns a value indicating if chroma key blending is available for mixed reality composition.
### Return value

true if chroma key blending is available; otherwise, false.
## int engine.vr_mixed_reality. hasFeatureAlphaBlend ( )

Returns a value indicating if alpha blending is supported for mixing real and virtual images.
### Return value

true if alpha blending is supported; otherwise, false.
## int engine.vr_mixed_reality. hasFeatureDepthTest ( )

Returns a value indicating if depth testing is available for mixing of real and virtual content based on depth occlusion.
### Return value

true if depth testing is available; otherwise, false.
## int engine.vr_mixed_reality. hasFeatureDepthTestRange ( )

Returns a value indicating if configurable depth testing range is supported.
### Return value

true if configurable depth testing range is supported; otherwise, false.
## int engine.vr_mixed_reality. hasFeatureBlendmasking ( )

Returns a value indicating if blend masking is supported in mixed reality.
### Return value

true if blend masking is supported; otherwise, false.
## int engine.vr_mixed_reality. hasFeatureCameraProperties ( )

Returns a value indicating if access to real-world camera properties is supported (e.g., white balance, ISO, shutter speed, etc.).
### Return value

true if access to real-world camera properties is supported; otherwise, false.
## int engine.vr_mixed_reality. hasFeatureMarkerTracking ( )

Returns a value indicating if marker-based spatial tracking is supported.
### Return value

true if marker-based spatial tracking is supported; otherwise, false.
## int engine.vr_mixed_reality. hasFeatureViewOffset ( )

Returns a value indicating if per-eye view offset is supported for manual aligning virtual content with passthrough imagery.
### Return value

true if per-eye view offset is supported; otherwise, false.
## int engine.vr_mixed_reality. hasFeatureColorCorrection ( )

Returns a value indicating if color correction feature is supported.
### Return value

true if color correction feature is supported; otherwise, false.
## int engine.vr_mixed_reality. hasFeatureEnvironmentCubemap ( )

Returns a value indicating if the environment cubemap feature is supported.
### Return value

true if the environment cubemap feature is supported; otherwise, false.
