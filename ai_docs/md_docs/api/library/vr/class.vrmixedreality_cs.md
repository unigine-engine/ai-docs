# Unigine.VRMixedReality Class (CS)

> **Notice:** This class is a singleton.


The class is used for mixed reality management on compatible head-mounted displays (HMDs) that support mixed reality and operate on **Varjo** or **OpenXR** backends.


When using the **Varjo** backend, all features of this class are available. Under **OpenXR**, mixed reality support is limited. Use the *[HasFeature...()](../../...md#hasFeatureAlphaBlend_int)* methods to check which features and corresponding methods of this class are supported specifically for your device and backend configuration.


## VRMixedReality Class

### Enums

## BLEND_MASKING_MODE

| Name | Description |
|---|---|
| **BEGIN** = 0 | The first element to be used for iteration. |
| **DISABLED** = 0 | Masking mode is disabled. |
| **RESTRICT_VIDEO_TO_MASK** = 1 | Show the video pass-through image (VST) in the mask. Can be used with chroma key. |
| **RESTRICT_VR_TO_MASK** = 2 | Show VR in the mask. Can be used with chroma key. |
| **RESTRICT_VR_TO_CHROMAKEY_REDUCED_BY_MASK** = 3 | Show VR in the mask and chroma elsewhere. Requires chroma key. |
| **END** = 3 | The last element to be used for iteration. |

## CAMERA_PROPERTY_MODE

| Name | Description |
|---|---|
| **DISABLED** = 0 | The camera property adjustment is disabled. |
| **AUTO** = 1 | Automatic property adjustment for the camera. |
| **MANUAL** = 2 | Manual property adjustment for the camera. In this mode you can set the desired property value (exposure time correction, white balance correction, ISO) manually via the corresponding methods. |

## CAMERA_EXPOSURE_TIME

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | The camera exposure time is not specified. |
| **BEGIN** = 1 | The first element to be used for iteration. |
| **VALUE_91_MS** = 1 | The camera exposure time value equal to 91 K. |
| **VALUE_125_MS** = 2 | The camera exposure time value equal to 125 K. |
| **VALUE_250_MS** = 3 | The camera exposure time value equal to 250 K. |
| **VALUE_500_MS** = 4 | The camera exposure time value equal to 500 K. |
| **VALUE_1000_MS** = 5 | The camera exposure time value equal to 1000 K. |
| **VALUE_2000_MS** = 6 | The camera exposure time value equal to 2000 K. |
| **VALUE_4000_MS** = 7 | The camera exposure time value equal to 4000 K. |
| **VALUE_8000_MS** = 8 | The camera exposure time value equal to 8000 K. |
| **END** = 8 | The last element to be used for iteration. |

## CAMERA_WHITE_BALANCE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | The camera white balance value is not specified. |
| **BEGIN** = 1 | The first element to be used for iteration. |
| **VALUE_2000_K** = 1 | The camera white balance value equal to 2000 K. |
| **VALUE_3000_K** = 2 | The camera white balance value equal to 3000 K. |
| **VALUE_3500_K** = 3 | The camera white balance value equal to 3500 K. |
| **VALUE_4200_K** = 4 | The camera white balance value equal to 4200 K. |
| **VALUE_5000_K** = 5 | The camera white balance value equal to 5000 K. |
| **VALUE_5400_K** = 6 | The camera white balance value equal to 5400 K. |
| **VALUE_6500_K** = 7 | The camera white balance value equal to 6500 K. |
| **VALUE_8000_K** = 8 | The camera white balance value equal to 8000 K. |
| **VALUE_12000_K** = 9 | The camera white balance value equal to 12000 K. |
| **END** = 9 | The last element to be used for iteration. |

## CAMERA_ISO

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | The camera ISO value is not specified. |
| **BEGIN** = 1 | The first element to be used for iteration. |
| **GAIN_100** = 1 | The camera ISO value equal to 100. |
| **GAIN_200** = 2 | The camera ISO value equal to 200. |
| **GAIN_400** = 3 | The camera ISO value equal to 400. |
| **GAIN_800** = 4 | The camera ISO value equal to 800. |
| **GAIN_1600** = 5 | The camera ISO value equal to 1600. |
| **GAIN_3200** = 6 | The camera ISO value equal to 3200. |
| **GAIN_6400** = 7 | The camera ISO value equal to 6400. |
| **END** = 7 | The last element to be used for iteration. |

## CAMERA_FLICKER_COMPENSATION

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | The camera flicker compensation value is not specified. |
| **BEGIN** = 1 | The first element to be used for iteration. |
| **FREQ_50_HZ** = 1 | The camera flicker compensation value equal to 50 Hz. |
| **FREQ_60_HZ** = 2 | The camera flicker compensation value equal to 60 Hz. |
| **END** = 2 | The last element to be used for iteration. |

## CUBEMAP_MODE

| Name | Description |
|---|---|
| **BEGIN** = 0 | The first element to be used for iteration. |
| **DISABLED** = 0 | The cubemap streaming from AR cameras is disabled. |
| **ENVIRONMENT_OVERLAP** = 1 | The environment texture substitutes the sky. |
| **ENVIRONMENT_PRESET_0** = 2 | The first [environment preset](../../../editor2/settings/render_settings/environment/index.md#presets) defines the way the AR texture is set for the environment. |
| **ENVIRONMENT_PRESET_1** = 3 | The second [environment preset](../../../editor2/settings/render_settings/environment/index.md#presets) defines the way the AR texture is set for the environment. |
| **ENVIRONMENT_PRESET_2** = 4 | The third [environment preset](../../../editor2/settings/render_settings/environment/index.md#presets) defines the way the AR texture is set for the environment. |
| **END** = 4 | The last element to be used for iteration. |

## OVERRIDE_COLOR_CORRECTION_MODE

| Name | Description |
|---|---|
| **BEGIN** = 0 | The first element to be used for iteration. |
| **DISABLED** = 0 | The color correction is disabled. |
| **EXPOSURE** = 1 | Exposure correction for the stream from the AR cameras. |
| **EXPOSURE_WHITE_BALANCE** = 2 | Exposure and white balance correction for the stream. |
| **END** = 2 | The last element to be used for iteration. |

### Properties

## 🔒︎ bool IsAvailable

The value indicating if mixed reality is available on the active VR device, and is supported at runtime.
## bool ChromaKeyEnabled

***Console*:**`vr_mixed_reality_chroma_key_enabled`The value indicating if chroma keying is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled. The default value is **false**.
## bool DepthTestEnabled

***Console*:**`vr_mixed_reality_depth_test_enabled`The value indicating if depth buffer submission is enabled. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled. The default value is **false**.
## bool AlphaBlendEnabled

***Console*:**`vr_mixed_reality_alpha_blend_enabled`The value indicating if alpha blending is enabled. This option is used for blending VR and AR images using the alpha channel. [VST capturing](#isVideoEnabled_int) from HMD cameras must be enabled and the [screen precision](../../../api/library/rendering/class.render_cs.md#isScreenPrecision_int) must be 1. The default value is **false**.
## bool VideoEnabled

***Console*:**`vr_mixed_reality_video_enabled`The value indicating if the video signal from the real-world view from the front-facing HMD-mounted cameras is enabled. The real-world view is used for combining virtual and real-world elements to create an immersive experience in mixed reality. The default value is **false**.
## bool DepthTestRangeEnabled

***Console*:**`vr_mixed_reality_depth_test_range_enabled`The value indicating if the depth test range usage is enabled. Use the [depth test range](#getDepthTestRange_vec2) (*Depth Test Near Z*, *Depth Test Far Z*) to control the range for which the depth test is evaluated. The default value is **false**.
## vec2 DepthTestRange

***Console*:**`vr_mixed_reality_depth_test_range`The depth test range as a two-component vector (the near and far planes). The [depth test range usage](#isDepthTestRangeEnabled_int) must be enabled.
**vec2(0.0f, 1.0f)** - default value
## 🔒︎ int ChromaKeyConfigNum

The number of chroma key config indices supported. The maximum index will be count-1.
## VRMixedReality.BLEND_MASKING_MODE BlendMaskingMode

***Console*:**`vr_mixed_reality_blend_masking_mode`The mode of the *Blend Control Mask* that can be used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth. One of the following values:
- **0** - Disabled (masking mode is disabled). (by default)
- **1** - Restrict Video to Mask (show the video pass-through image (VST) in the mask; can be used with chroma key)
- **2** - Restrict VR to Mask (show VR in the mask; can be used with chroma key)
- **3** - Restrict VR to Chromakey reduced by Mask (show VR in the mask and chroma elsewhere; requires chroma key)

## bool BlendMaskingDebugEnabled

***Console*:**`vr_mixed_reality_blend_masking_debug_enabled`The value indicating if blend masking debug visualization is enabled. The [blend masking mode](#getBlendMaskingMode_int) must be enabled. The default value is **false**.
## 🔒︎ bool IsBlendMaskingUsed

The value indicating if the *Blend Control Mask* is used to extend or restrict the chroma key mask or to control the depth testing against the estimated video depth.
## 🔒︎ Texture CurrentBlendMaskColorBuffer

The image representing the current color buffer of the *Blend Control Mask*.
## double CameraExposureTimeRaw

The exposure time value for the camera.
## VRMixedReality.CAMERA_EXPOSURE_TIME CameraExposureTime

***Console*:**`vr_mixed_reality_camera_exposure_time`The exposure time value that is valid for the connected device.

## VRMixedReality.CAMERA_PROPERTY_MODE CameraExposureTimeMode

***Console*:**`vr_mixed_reality_camera_exposure_time_mode`The exposure adjustment mode for the camera. One of the following values:
- **0** - exposure adjustment is disabled
- **1** - automatic exposure adjustment (by default)
- **2** - manual exposure adjustment

## int CameraWhiteBalanceRaw

The white balance correction value that is valid for the connected device.
## VRMixedReality.CAMERA_WHITE_BALANCE CameraWhiteBalance

***Console*:**`vr_mixed_reality_camera_white_balance`The white balance correction value that is valid for the connected device.

## VRMixedReality.CAMERA_PROPERTY_MODE CameraWhiteBalanceMode

***Console*:**`vr_mixed_reality_camera_white_balance_mode`The white balance adjustment mode for the camera. One of the following values:
- **0** - white balance adjustment is disabled
- **1** - automatic white balance adjustment (by default)
- **2** - manual white balance adjustment

## int CameraISORaw

The ISO value that is valid for the connected device.
## VRMixedReality.CAMERA_ISO CameraISO

***Console*:**`vr_mixed_reality_camera_iso`The ISO value for the camera.

## VRMixedReality.CAMERA_PROPERTY_MODE CameraISOMode

***Console*:**`vr_mixed_reality_camera_iso_mode`The ISO adjustment mode for the camera. One of the following values:
- **0** - ISO adjustment is disabled
- **1** - automatic ISO adjustment (by default)
- **2** - manual ISO adjustment

## int CameraFlickerCompensationRaw

The flicker compensation value for the camera. This is useful when using the HMD indoors with mostly artificial light bulbs, which flicker at the frequency of 50Hz or 60Hz and can cause visual flicker artifacts on the video see through image. The correct setting depends on the underlying power grid's frequency. For example, in most parts of Africa/Asia/Australia/Europe the frequency is 50 Hz and in most parts of North and South America 60 Hz.
## VRMixedReality.CAMERA_FLICKER_COMPENSATION CameraFlickerCompensation

***Console*:**`vr_mixed_reality_camera_flicker_compensation`The flicker compensation value for the camera. This is useful when using the HMD indoors with mostly artificial light bulbs, which flicker at the frequency of 50Hz or 60Hz and can cause visual flicker artifacts on the video see through image. The correct setting depends on the underlying power grid's frequency. For example, in most parts of Africa/Asia/Australia/Europe the frequency is 50 Hz and in most parts of North and South America 60 Hz.

## 🔒︎ int CameraMinSharpness

The minimum possible value for the [camera sharpness](#CameraSharpness).
## 🔒︎ int CameraMaxSharpness

The maximum possible value for the [camera sharpness](#CameraSharpness).
## int CameraSharpness

***Console*:**`vr_mixed_reality_camera_sharpness`The sharpness filter power value for the camera.
Range of values: **[0, 10]**. The default value is : **0**.
## float ViewOffset

***Console*:**`vr_mixed_reality_view_offset`The eyes [view offset](https://developer.varjo.com/docs/apidocs/_varjo__mr_8h.html#a0aa1772b02020977c3c5b1c974848f75) (where eye camera should be positioned when using Mixed Reality):
- **0** for physical eye position
- **1** for VST camera position


Range of values: **[0.0, 1.0]**. The default value is : **0.0**.
## bool MarkerTrackingEnabled

***Console*:**`vr_mixed_reality_marker_tracking_enabled`The value indicating if marker tracking is enabled. The default value is **false**.
## 🔒︎ short NumMarkerObjectVisible

The number of visible marker objects.
## VRMixedReality.CUBEMAP_MODE CubemapMode

***Console*:**`vr_mixed_reality_cubemap_mode`The mode defining the way the AR texture is set for the environment. One of the following values:
- **0** - cubemap streaming from AR cameras is disabled.
- **1** - environment texture substitutes the sky.
- **2** - the first environment preset defines the way the AR texture is set for the environment. (by default)
- **3** - the second environment preset defines the way the AR texture is set for the environment.
- **4** - the third environment preset defines the way the AR texture is set for the environment.

## Render.GGX_MIPMAPS_QUALITY CubemapGGXQuality

***Console*:**`vr_mixed_reality_cubemap_ggx_quality`The quality of the generated GGX mips for the AR cubemap. One of the following values:
- **0** - low
- **1** - medium (by default)
- **2** - high
- **3** - ultra

## VRMixedReality.OVERRIDE_COLOR_CORRECTION_MODE OverrideColorCorrectionMode

***Console*:**`vr_mixed_reality_override_color_correction_mode`The color correction mode for the stream from the AR cameras. One of the following values:
- **0** - correction is disabled. (by default)
- **1** - exposure correction for the stream from the AR cameras.
- **2** - exposure and white balance correction for the stream.

## 🔒︎ Event EventCameraPropertyUpdateSharpness

The Event triggered when the sharpness value is changed in Varjo Base. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CameraPropertyUpdateSharpness event handler
void camerapropertyupdatesharpness_event_handler()
{
	Log.Message("\Handling CameraPropertyUpdateSharpness event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdatesharpness_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality.EventCameraPropertyUpdateSharpness.Connect(camerapropertyupdatesharpness_event_connections, camerapropertyupdatesharpness_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality.EventCameraPropertyUpdateSharpness.Connect(camerapropertyupdatesharpness_event_connections, () => {
		Log.Message("Handling CameraPropertyUpdateSharpness event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdatesharpness_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CameraPropertyUpdateSharpness event with a handler function
VRMixedReality.EventCameraPropertyUpdateSharpness.Connect(camerapropertyupdatesharpness_event_handler);

// remove subscription to the CameraPropertyUpdateSharpness event later by the handler function
VRMixedReality.EventCameraPropertyUpdateSharpness.Disconnect(camerapropertyupdatesharpness_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection camerapropertyupdatesharpness_event_connection;

// subscribe to the CameraPropertyUpdateSharpness event with a lambda handler function and keeping the connection
camerapropertyupdatesharpness_event_connection = VRMixedReality.EventCameraPropertyUpdateSharpness.Connect(() => {
		Log.Message("Handling CameraPropertyUpdateSharpness event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
camerapropertyupdatesharpness_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
camerapropertyupdatesharpness_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
camerapropertyupdatesharpness_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CameraPropertyUpdateSharpness events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality.EventCameraPropertyUpdateSharpness.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VRMixedReality.EventCameraPropertyUpdateSharpness.Enabled = true;

```

</details>

## 🔒︎ Event EventCameraPropertyUpdateFlickerCompensation

The Event triggered when the flicker compensation value of the camera is changed in Varjo Base. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CameraPropertyUpdateFlickerCompensation event handler
void camerapropertyupdateflickercompensation_event_handler()
{
	Log.Message("\Handling CameraPropertyUpdateFlickerCompensation event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdateflickercompensation_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality.EventCameraPropertyUpdateFlickerCompensation.Connect(camerapropertyupdateflickercompensation_event_connections, camerapropertyupdateflickercompensation_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality.EventCameraPropertyUpdateFlickerCompensation.Connect(camerapropertyupdateflickercompensation_event_connections, () => {
		Log.Message("Handling CameraPropertyUpdateFlickerCompensation event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdateflickercompensation_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CameraPropertyUpdateFlickerCompensation event with a handler function
VRMixedReality.EventCameraPropertyUpdateFlickerCompensation.Connect(camerapropertyupdateflickercompensation_event_handler);

// remove subscription to the CameraPropertyUpdateFlickerCompensation event later by the handler function
VRMixedReality.EventCameraPropertyUpdateFlickerCompensation.Disconnect(camerapropertyupdateflickercompensation_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection camerapropertyupdateflickercompensation_event_connection;

// subscribe to the CameraPropertyUpdateFlickerCompensation event with a lambda handler function and keeping the connection
camerapropertyupdateflickercompensation_event_connection = VRMixedReality.EventCameraPropertyUpdateFlickerCompensation.Connect(() => {
		Log.Message("Handling CameraPropertyUpdateFlickerCompensation event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
camerapropertyupdateflickercompensation_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
camerapropertyupdateflickercompensation_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
camerapropertyupdateflickercompensation_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CameraPropertyUpdateFlickerCompensation events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality.EventCameraPropertyUpdateFlickerCompensation.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VRMixedReality.EventCameraPropertyUpdateFlickerCompensation.Enabled = true;

```

</details>

## 🔒︎ Event EventCameraPropertyUpdateISO

The Event triggered when the camera ISO value and/or the ISO adjustment mode are changed in Varjo Base. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CameraPropertyUpdateISO event handler
void camerapropertyupdateiso_event_handler()
{
	Log.Message("\Handling CameraPropertyUpdateISO event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdateiso_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality.EventCameraPropertyUpdateISO.Connect(camerapropertyupdateiso_event_connections, camerapropertyupdateiso_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality.EventCameraPropertyUpdateISO.Connect(camerapropertyupdateiso_event_connections, () => {
		Log.Message("Handling CameraPropertyUpdateISO event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdateiso_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CameraPropertyUpdateISO event with a handler function
VRMixedReality.EventCameraPropertyUpdateISO.Connect(camerapropertyupdateiso_event_handler);

// remove subscription to the CameraPropertyUpdateISO event later by the handler function
VRMixedReality.EventCameraPropertyUpdateISO.Disconnect(camerapropertyupdateiso_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection camerapropertyupdateiso_event_connection;

// subscribe to the CameraPropertyUpdateISO event with a lambda handler function and keeping the connection
camerapropertyupdateiso_event_connection = VRMixedReality.EventCameraPropertyUpdateISO.Connect(() => {
		Log.Message("Handling CameraPropertyUpdateISO event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
camerapropertyupdateiso_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
camerapropertyupdateiso_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
camerapropertyupdateiso_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CameraPropertyUpdateISO events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality.EventCameraPropertyUpdateISO.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VRMixedReality.EventCameraPropertyUpdateISO.Enabled = true;

```

</details>

## 🔒︎ Event EventCameraPropertyUpdateWhiteBalance

The Event triggered when the white balance correction value of the camera and/or the white balance adjustment mode are changed in Varjo Base. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CameraPropertyUpdateWhiteBalance event handler
void camerapropertyupdatewhitebalance_event_handler()
{
	Log.Message("\Handling CameraPropertyUpdateWhiteBalance event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdatewhitebalance_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality.EventCameraPropertyUpdateWhiteBalance.Connect(camerapropertyupdatewhitebalance_event_connections, camerapropertyupdatewhitebalance_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality.EventCameraPropertyUpdateWhiteBalance.Connect(camerapropertyupdatewhitebalance_event_connections, () => {
		Log.Message("Handling CameraPropertyUpdateWhiteBalance event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdatewhitebalance_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CameraPropertyUpdateWhiteBalance event with a handler function
VRMixedReality.EventCameraPropertyUpdateWhiteBalance.Connect(camerapropertyupdatewhitebalance_event_handler);

// remove subscription to the CameraPropertyUpdateWhiteBalance event later by the handler function
VRMixedReality.EventCameraPropertyUpdateWhiteBalance.Disconnect(camerapropertyupdatewhitebalance_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection camerapropertyupdatewhitebalance_event_connection;

// subscribe to the CameraPropertyUpdateWhiteBalance event with a lambda handler function and keeping the connection
camerapropertyupdatewhitebalance_event_connection = VRMixedReality.EventCameraPropertyUpdateWhiteBalance.Connect(() => {
		Log.Message("Handling CameraPropertyUpdateWhiteBalance event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
camerapropertyupdatewhitebalance_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
camerapropertyupdatewhitebalance_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
camerapropertyupdatewhitebalance_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CameraPropertyUpdateWhiteBalance events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality.EventCameraPropertyUpdateWhiteBalance.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VRMixedReality.EventCameraPropertyUpdateWhiteBalance.Enabled = true;

```

</details>

## 🔒︎ Event EventCameraPropertyUpdateExposureTime

The Event triggered when the exposure time value of the camera and/or the exposure adjustment mode are changed in Varjo Base. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CameraPropertyUpdateExposureTime event handler
void camerapropertyupdateexposuretime_event_handler()
{
	Log.Message("\Handling CameraPropertyUpdateExposureTime event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdateexposuretime_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality.EventCameraPropertyUpdateExposureTime.Connect(camerapropertyupdateexposuretime_event_connections, camerapropertyupdateexposuretime_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality.EventCameraPropertyUpdateExposureTime.Connect(camerapropertyupdateexposuretime_event_connections, () => {
		Log.Message("Handling CameraPropertyUpdateExposureTime event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdateexposuretime_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CameraPropertyUpdateExposureTime event with a handler function
VRMixedReality.EventCameraPropertyUpdateExposureTime.Connect(camerapropertyupdateexposuretime_event_handler);

// remove subscription to the CameraPropertyUpdateExposureTime event later by the handler function
VRMixedReality.EventCameraPropertyUpdateExposureTime.Disconnect(camerapropertyupdateexposuretime_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection camerapropertyupdateexposuretime_event_connection;

// subscribe to the CameraPropertyUpdateExposureTime event with a lambda handler function and keeping the connection
camerapropertyupdateexposuretime_event_connection = VRMixedReality.EventCameraPropertyUpdateExposureTime.Connect(() => {
		Log.Message("Handling CameraPropertyUpdateExposureTime event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
camerapropertyupdateexposuretime_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
camerapropertyupdateexposuretime_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
camerapropertyupdateexposuretime_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CameraPropertyUpdateExposureTime events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality.EventCameraPropertyUpdateExposureTime.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VRMixedReality.EventCameraPropertyUpdateExposureTime.Enabled = true;

```

</details>

## 🔒︎ Event EventChromakeyUpdate

The Event triggered when the chroma keying settings are changed in Varjo Base. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ChromakeyUpdate event handler
void chromakeyupdate_event_handler()
{
	Log.Message("\Handling ChromakeyUpdate event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections chromakeyupdate_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality.EventChromakeyUpdate.Connect(chromakeyupdate_event_connections, chromakeyupdate_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality.EventChromakeyUpdate.Connect(chromakeyupdate_event_connections, () => {
		Log.Message("Handling ChromakeyUpdate event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
chromakeyupdate_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ChromakeyUpdate event with a handler function
VRMixedReality.EventChromakeyUpdate.Connect(chromakeyupdate_event_handler);

// remove subscription to the ChromakeyUpdate event later by the handler function
VRMixedReality.EventChromakeyUpdate.Disconnect(chromakeyupdate_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection chromakeyupdate_event_connection;

// subscribe to the ChromakeyUpdate event with a lambda handler function and keeping the connection
chromakeyupdate_event_connection = VRMixedReality.EventChromakeyUpdate.Connect(() => {
		Log.Message("Handling ChromakeyUpdate event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
chromakeyupdate_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
chromakeyupdate_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
chromakeyupdate_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ChromakeyUpdate events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality.EventChromakeyUpdate.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VRMixedReality.EventChromakeyUpdate.Enabled = true;

```

</details>

## 🔒︎ Event EventDeviceDisconnected

The Event triggered when the Varjo device is disconnected. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the DeviceDisconnected event handler
void devicedisconnected_event_handler()
{
	Log.Message("\Handling DeviceDisconnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections devicedisconnected_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality.EventDeviceDisconnected.Connect(devicedisconnected_event_connections, devicedisconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality.EventDeviceDisconnected.Connect(devicedisconnected_event_connections, () => {
		Log.Message("Handling DeviceDisconnected event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
devicedisconnected_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the DeviceDisconnected event with a handler function
VRMixedReality.EventDeviceDisconnected.Connect(devicedisconnected_event_handler);

// remove subscription to the DeviceDisconnected event later by the handler function
VRMixedReality.EventDeviceDisconnected.Disconnect(devicedisconnected_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection devicedisconnected_event_connection;

// subscribe to the DeviceDisconnected event with a lambda handler function and keeping the connection
devicedisconnected_event_connection = VRMixedReality.EventDeviceDisconnected.Connect(() => {
		Log.Message("Handling DeviceDisconnected event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
devicedisconnected_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
devicedisconnected_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
devicedisconnected_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring DeviceDisconnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality.EventDeviceDisconnected.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VRMixedReality.EventDeviceDisconnected.Enabled = true;

```

</details>

## 🔒︎ Event EventDeviceConnected

The Event triggered when the Varjo device is connected. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the DeviceConnected event handler
void deviceconnected_event_handler()
{
	Log.Message("\Handling DeviceConnected event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections deviceconnected_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality.EventDeviceConnected.Connect(deviceconnected_event_connections, deviceconnected_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality.EventDeviceConnected.Connect(deviceconnected_event_connections, () => {
		Log.Message("Handling DeviceConnected event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
deviceconnected_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the DeviceConnected event with a handler function
VRMixedReality.EventDeviceConnected.Connect(deviceconnected_event_handler);

// remove subscription to the DeviceConnected event later by the handler function
VRMixedReality.EventDeviceConnected.Disconnect(deviceconnected_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection deviceconnected_event_connection;

// subscribe to the DeviceConnected event with a lambda handler function and keeping the connection
deviceconnected_event_connection = VRMixedReality.EventDeviceConnected.Connect(() => {
		Log.Message("Handling DeviceConnected event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
deviceconnected_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
deviceconnected_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
deviceconnected_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring DeviceConnected events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality.EventDeviceConnected.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VRMixedReality.EventDeviceConnected.Enabled = true;

```

</details>

## 🔒︎ Event EventCameraPropertyUpdateVSTReprojection

The Event triggered when the camera VST reprojection property is updated. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CameraPropertyUpdateVSTReprojection event handler
void camerapropertyupdatevstreprojection_event_handler()
{
	Log.Message("\Handling CameraPropertyUpdateVSTReprojection event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections camerapropertyupdatevstreprojection_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VRMixedReality.EventCameraPropertyUpdateVSTReprojection.Connect(camerapropertyupdatevstreprojection_event_connections, camerapropertyupdatevstreprojection_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VRMixedReality.EventCameraPropertyUpdateVSTReprojection.Connect(camerapropertyupdatevstreprojection_event_connections, () => {
		Log.Message("Handling CameraPropertyUpdateVSTReprojection event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
camerapropertyupdatevstreprojection_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CameraPropertyUpdateVSTReprojection event with a handler function
VRMixedReality.EventCameraPropertyUpdateVSTReprojection.Connect(camerapropertyupdatevstreprojection_event_handler);

// remove subscription to the CameraPropertyUpdateVSTReprojection event later by the handler function
VRMixedReality.EventCameraPropertyUpdateVSTReprojection.Disconnect(camerapropertyupdatevstreprojection_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection camerapropertyupdatevstreprojection_event_connection;

// subscribe to the CameraPropertyUpdateVSTReprojection event with a lambda handler function and keeping the connection
camerapropertyupdatevstreprojection_event_connection = VRMixedReality.EventCameraPropertyUpdateVSTReprojection.Connect(() => {
		Log.Message("Handling CameraPropertyUpdateVSTReprojection event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
camerapropertyupdatevstreprojection_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
camerapropertyupdatevstreprojection_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
camerapropertyupdatevstreprojection_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CameraPropertyUpdateVSTReprojection events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VRMixedReality.EventCameraPropertyUpdateVSTReprojection.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VRMixedReality.EventCameraPropertyUpdateVSTReprojection.Enabled = true;

```

</details>

## VRMixedReality.CAMERA_PROPERTY_MODE CameraVSTReprojectionMode

***Console*:**`vr_mixed_reality_camera_vst_reprojection_mode`The reprojection mode of VST. One of the following values:
- **0** - reprojection of VST is disabled (default). (by default)
- **1** - automatic reprojection mode of VST (the Depth buffer is used for reprojection)
- **2** - manual reprojections mode of VST

## float CameraVSTReprojectionDistance

***Console*:**`vr_mixed_reality_camera_vst_reprojection_distance`The static distance in meters used to shift the whole image. Is configured only if the [VST reprojection mode](#CameraVSTReprojectionMode) is set to [Manual](#CAMERA_PROPERTY_MODE_MANUAL).
Range of values: **[0.0f, 1000.0f]**. The default value is : **0.0f**.
### Members

---

## void ApplySettings ( )

Updates the mixed reality settings to the current settings.
## bool IsChromaKeyConfigEnabled ( int index )

Returns the current value indicating if the chroma key configuration with the specified index is enabled.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

1 the chroma key configuration is enabled; otherwise, 0.
## void SetChromaKeyConfigEnabled ( int index , bool enabled )

Sets a new value indicating if the chroma key configuration with the specified index is enabled.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *bool* **enabled** - 1 to enable the chroma key configuration; 0 to disable it.

## vec3 GetChromaKeyConfigFalloff ( int index )

Returns the current tolerance falloff values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

Current tolerance falloff values for HSV components of the chroma key target color. The range for each component is [0.0; 1.0].
## void SetChromaKeyConfigFalloff ( int index , vec3 falloff )

Sets new tolerance falloff values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *vec3* **falloff** - New tolerance falloff values to be set for HSV components of the chroma key target color. The range for each component is [0.0; 1.0].

## vec3 GetChromaKeyConfigTargetColor ( int index )

Returns the current chroma key target color in HSV color model.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

Current chroma key target color in HSV color model. The range for each component is [0.0; 1.0].
## void SetChromaKeyConfigTargetColor ( int index , vec3 target_color )

Sets a new chroma key target color in HSV color model.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *vec3* **target_color** - New chroma key target color to be set in HSV color model. The range for each component is [0.0; 1.0].

## vec3 GetChromaKeyConfigTolerance ( int index )

Returns the current tolerance values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

### Return value

Current tolerance values for HSV components of the chroma key target color. The range for each component is [0.0; 1.0].
## void SetChromaKeyConfigTolerance ( int index , vec3 tolerance )

Sets new tolerance values for HSV components of the chroma key target color.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.
- *vec3* **tolerance** - New tolerance values for HSV components of the chroma key target color to be set. The range for each component is [0.0; 1.0].

## void ApplyChromaKeySettings ( int index )

Updates the settings of the chroma key configuration with the specified index to the current settings.
### Arguments

- *int* **index** - Chroma key config index in the range from 0 to [config count](#ChromaKeyConfigNum) - 1.

## GetCameraSupportedRawISO ( )

Returns a vector containing the ISO values that are set as valid for the connected device.
### Return value

The vector containing the ISO values.
## VRMarkerObject GetMarkerObject ( short index )

Returns the marker object with the specified index.
### Arguments

- *short* **index** - Marker object index.

### Return value

Marker object.
## VRMarkerObject GetMarkerObjectByID ( short marker_id )

Returns the marker object with the specified ID.
### Arguments

- *short* **marker_id** - Marker object ID.

### Return value

Marker object.
## bool CameraConfigLock ( )

Returns the value indicating whether the attempt to lock the camera config is successful.
### Return value

**true** if the camera config is locked successfully or it was already locked; otherwise, **false**.
## void CameraConfigUnlock ( )

Unlocks the previously locked camera config.
## bool HasFeatureChromakey ( )

Returns a value indicating if chroma key blending is available for mixed reality composition.
### Return value

true if chroma key blending is available; otherwise, false.
## bool HasFeatureAlphaBlend ( )

Returns a value indicating if alpha blending is supported for mixing real and virtual images.
### Return value

true if alpha blending is supported; otherwise, false.
## bool HasFeatureDepthTest ( )

Returns a value indicating if depth testing is available for mixing of real and virtual content based on depth occlusion.
### Return value

true if depth testing is available; otherwise, false.
## bool HasFeatureDepthTestRange ( )

Returns a value indicating if configurable depth testing range is supported.
### Return value

true if configurable depth testing range is supported; otherwise, false.
## bool HasFeatureBlendmasking ( )

Returns a value indicating if blend masking is supported in mixed reality.
### Return value

true if blend masking is supported; otherwise, false.
## bool HasFeatureCameraProperties ( )

Returns a value indicating if access to real-world camera properties is supported (e.g., white balance, ISO, shutter speed, etc.).
### Return value

true if access to real-world camera properties is supported; otherwise, false.
## bool HasFeatureMarkerTracking ( )

Returns a value indicating if marker-based spatial tracking is supported.
### Return value

true if marker-based spatial tracking is supported; otherwise, false.
## bool HasFeatureViewOffset ( )

Returns a value indicating if per-eye view offset is supported for manual aligning virtual content with passthrough imagery.
### Return value

true if per-eye view offset is supported; otherwise, false.
## bool HasFeatureColorCorrection ( )

Returns a value indicating if color correction feature is supported.
### Return value

true if color correction feature is supported; otherwise, false.
## bool HasFeatureEnvironmentCubemap ( )

Returns a value indicating if the environment cubemap feature is supported.
### Return value

true if the environment cubemap feature is supported; otherwise, false.
