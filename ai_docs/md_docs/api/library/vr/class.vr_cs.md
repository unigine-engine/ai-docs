# Unigine.VR Class (CS)

> **Notice:** This class is a singleton.


The base class for managing virtual reality in UNIGINE.


### VR Initialization


By default, VR is not initialized. To run the engine with VR, you need to specify the [*-vr_app*](../../../vr_development/index.md#which_backend) command-line option on the application start-up.


### Supported Graphics APIs


The following graphics APIs are supported out of the box:


- DirectX 12
- Vulkan


## VR Class

### Enums

## API

| Name | Description |
|---|---|
| **NULL** = 0 | VR API is not initialized. |
| **VARJO** = 1 | Varjo API. |
| **OPENVR** = 2 | OpenVR API. |
| **OPENXR** = 3 | OpenXR API. |

## VIEWPORT_TYPE

| Name | Description |
|---|---|
| **CONTEXT** = 0 | Context (low-res) viewport. |
| **FOCUS** = 1 | Focus (high-res) viewport. |
| **NUM** = 2 | Number of viewport types. |

## EYE_TYPE

| Name | Description |
|---|---|
| **LEFT** = 0 | Left eye. |
| **RIGHT** = 1 | Right eye. |
| **NUM** = 2 | Number of eye types. |

## MIRROR_MODE

| Name | Description |
|---|---|
| **BEGIN** = 0 | The first element to be used for iteration. |
| **BLACK_SCREEN** = 0 | No image (black screen). |
| **MONO_LEFT** = 1 | Mono image for the left eye. |
| **MONO_RIGHT** = 2 | Mono image for the right eye. |
| **STEREO** = 3 | Stereo image (left and right eyes). |
| **END** = 3 | The last element to be used for iteration. |

## WINDOW_MODE

| Name | Description |
|---|---|
| **BEGIN** = 0 | The first element to be used for iteration. |
| **DISABLED** = 0 | Showing the mirrored image is disabled. |
| **MAIN** = 1 | The main window shows the mirrored image. |
| **END** = 1 | The last element to be used for iteration. |

## TRACKING_SPACE

| Name | Description |
|---|---|
| **BEGIN** = 0 | The first element to be used for iteration. |
| **LOCAL** = 0 | Local tracking space. Poses are provided relative to the Local (Seated or Stationary in OpenVR) Tracking Space. The origin is based on the user's position at startup (or after reset). Suited for sitting/simulator experiences (e.g. cockpit VR), where the player is already placed at the desired position. |
| **ABSOLUTE** = 1 | Absolute tracking space. Poses are provided relative to the Absolute (Standing in OpenVR) Tracking Space. The origin is fixed to the physical floor level (established by the tracking system, e.g. Base Stations or HMD SLAM Tracking). Suited for standing/room-scale experiences where the player is placed on the floor and the camera height comes from the HMD offset. |
| **END** = 1 | The last element to be used for iteration. |

## DEBUG_MODE

| Name | Description |
|---|---|
| **DISABLED** = 0 | Debug VR context is disabled. |
| **ENABLED** = 1 | Debug VR context is enabled. |
| **ENABLED_BREAK_ON_ERROR** = 2 | Debug VR context with the break on error option is enabled (only on debug binaries). |

## RUNTIME_TYPE

| Name | Description |
|---|---|
| **UNKNOWN** = 0 | The runtime type is unknown. |
| **NULL** = 1 | The runtime is null. |
| **STEAMVR** = 2 | SteamVR runtime. |
| **OCULUS** = 3 | Oculus runtime. |
| **VARJO** = 4 | Varjo runtime. |
| **WMR** = 5 | Windows Mixed Reality OpenXR runtime. |

## FOVEATED_MODE

Effective foveated-rendering state derived at runtime from the peripheral rendering settings, the debug gaze override, and the eye-tracking state.
| Name | Description |
|---|---|
| **DISABLED** = 0 | Foveated (peripheral) rendering is not currently used. |
| **FIXED** = 1 | Foveated rendering is active, but the high-detail (focus) region does not track the eyes: the gaze is pinned by a debug override or rests at a fixed pose because eye-tracking data is unavailable or invalid. |
| **DYNAMIC** = 2 | Foveated rendering is active and the high-detail (focus) region follows the gaze, based on valid eye-tracking data (or the mouse-based debug override). |

## PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE

Debug override source for the gaze position used by peripheral (foveated) rendering.
| Name | Description |
|---|---|
| **DISABLED** = 0 | No gaze override, the real gaze direction is used (default). |
| **FIXED** = 1 | Freezes the current gaze direction. |
| **MOUSE** = 2 | Uses the mouse position over the mirrored view as the current gaze direction. |
| **COORD** = 3 | Uses fixed normalized UV coordinates in texture space as the current gaze direction (set via the **[PeripheralRenderingDebugGazeOverrideCoord](../../...md#getPeripheralRenderingDebugGazeOverrideCoord_vec2)** property). |

## PROFILER_POSITION

Placement of the VR profiler overlay within the HMD view. The values are aligned with the numeric keypad layout, from 1 (bottom-left) to 9 (top-right).
| Name | Description |
|---|---|
| **BOTTOM_LEFT** = 1 | The profiler overlay is placed in the bottom-left corner of the view. |
| **BOTTOM_CENTER** = 2 | The profiler overlay is placed at the bottom center of the view. |
| **BOTTOM_RIGHT** = 3 | The profiler overlay is placed in the bottom-right corner of the view. |
| **CENTER_LEFT** = 4 | The profiler overlay is placed at the center-left of the view. |
| **CENTER_CENTER** = 5 | The profiler overlay is placed at the center of the view (default). |
| **CENTER_RIGHT** = 6 | The profiler overlay is placed at the center-right of the view. |
| **TOP_LEFT** = 7 | The profiler overlay is placed in the top-left corner of the view. |
| **TOP_CENTER** = 8 | The profiler overlay is placed at the top center of the view. |
| **TOP_RIGHT** = 9 | The profiler overlay is placed in the top-right corner of the view. |

## SHOW_PROFILER

Display mode of the VR profiler overlay shown inside the HMD view.
| Name | Description |
|---|---|
| **DISABLED** = 0 | The VR profiler overlay is not shown in the HMD view (default). |
| **BASIC** = 1 | Basic VR profiler overlay is shown in the HMD view. |
| **ADVANCED** = 2 | Advanced VR profiler overlay is shown in the HMD view. |

### Properties

## bool RenderEnabled

***Console*:**`vr_render_enabled`The value indicating if rendering into the head-mounted display is enabled. The default value is **false**.
## bool PeripheralRenderingModeEnabled

***Console*:**`vr_peripheral_rendering_mode_enabled`The value indicating if the peripheral rendering mode is enabled. In this mode, the HMD has two context (peripheral) and two focus viewports. You can disable two additional viewports to improve performance. The default value is **false**.
## bool PeripheralRenderingDebugEnabled

***Console*:**`vr_peripheral_rendering_debug_enabled`The value indicating if debug visualization for peripheral rendering is enabled. The default value is **false**.
## float PeripheralRenderingBorderWidth

***Console*:**`vr_peripheral_rendering_border_width`The width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible.
Range of values: **[eps, 1.0f]**. The default value is : **0.2f**.
## vec2 PeripheralRenderingFOVScale

***Console*:**`vr_peripheral_rendering_fov_scale`The scale factor applied to the field of view used for focus viewports.
**[0; 1]** - available range.
**(0.3f, 0.3f)** - default value.
## vec2 PeripheralRenderingFocusScale

***Console*:**`vr_peripheral_rendering_focus_scale`The scale factor controlling the size of the foveal (focus) area.
**[0; 1]** - available range.
**(0.5f, 0.2f)** - default value.
## float PeripheralRenderingFocusDeadzone

***Console*:**`vr_peripheral_rendering_focus_deadzone`The angular deadzone between the focus and context viewport transition.
> **Notice:** Available for OpenXR only.

Range of values: **[0.0f, 1.0f]**. The default value is : **0.15f**.
## VR.MIRROR_MODE MirrorMode

***Console*:**`vr_mirror_mode`The mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. One of the following values:
- **0** - black screen (no image is displayed).
- **1** - image rendered for the left eye.
- **2** - image rendered for the right eye.
- **3** - stereo image (both the left and right eyes). (by default)

## VR.WINDOW_MODE WindowMode

***Console*:**`vr_window_mode`The window mode that defines which window will display the mirrored image (i.e. VR image). One of the following values:
- **0** - mirroring is disabled.
- **1** - main window displays the mirrored image. (by default)

## VR.TRACKING_SPACE TrackingSpace

***Console*:**`vr_tracking_space`The zero pose of the tracking origin. One of the following values:
- **0** - poses are provided relative to the Local (Seated or Stationary in OpenVR) Tracking Space. The origin is based on the user's position at startup (or after reset). Suited for sitting/simulator experiences (e.g. cockpit VR), where the player is already placed at the desired position.
- **1** - poses are provided relative to the Absolute (Standing in OpenVR) Tracking Space. The origin is fixed to the physical floor level (established by the tracking system, e.g. Base Stations or HMD SLAM Tracking). Suited for standing/room-scale experiences where the player is placed on the floor and the camera height comes from the HMD offset. (by default)

## bool MotionPrediction

***Console*:**`vr_motion_prediction`The value indicating if motion prediction is enabled. When enabled, the engine submits the velocity value from the GBuffer to the VR compositor. Check [hasFeatureMotionPrediction()](#hasFeatureMotionPrediction_int) to verify availability. The default value is **false**.
## float MotionPredictionVelocityPrecision

***Console*:**`vr_motion_prediction_velocity_precision`The factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint). Requires [motion prediction support](#hasFeatureMotionPrediction_int).
Range of values: **[eps, inf]**. The default value is : **32.0f**.
## float MotionPredictionVelocityTimeDelta

***Console*:**`vr_motion_prediction_velocity_time_delta`The factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa. Requires [motion prediction support](#hasFeatureMotionPrediction_int).
Range of values: **[eps, inf]**. The default value is : **1.0f / 60.0f**.
## bool FoveatedRenderingEnabled

***Console*:**`vr_foveated_rendering_enabled`The value indicating if foveated rendering is enabled. Foveated rendering uses eye tracking to improve performance by reducing the image quality in peripheral areas where the user is not looking, allowing applications to render fewer pixels. Check [hasFeatureFoveatedRendering()](#hasFeatureFoveatedRendering_int) to verify availability.  The default value is **true**.
## float FoveatedFixedEyeCenterBias

***Console*:**`vr_foveated_fixed_eye_center_bias`The value by which the high-resolution focus area is shifted toward the center of the display when eye tracking is not used. A value of 0 keeps the focus area at the eye's natural resting position, a value of 1 moves it to the exact center. Takes effect when [peripheral rendering](../../../vr_development/vr_console.md#vr_peripheral_rendering_mode_enabled) is enabled and eye-tracked [foveated rendering](../../../vr_development/vr_console.md#vr_foveated_rendering_enabled) is disabled or eye tracking is unavailable.
> **Notice:** Available for *OpenXR only*.


Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## 🔒︎ string ApiName

The name of the VR API: *Null, OpenVR, OpenXR*, or *Varjo*.
## 🔒︎ VR.API ApiType

The type of the VR API.
## 🔒︎ float HMDRefreshRate

The refresh rate of the head-mounted display.
## 🔒︎ vec3 HandTrackingOffset

The hand tracking offset (for the Ultraleap device only).
## 🔒︎ bool IsHandTrackingOffsetSupported

The value indicating if the hand tracking offset is supported.
## 🔒︎ bool IsPeripheralRenderingModeUsed

The value indicating if the peripheral rendering is used.
## 🔒︎ bool IsHMDConnected

The value indicating if the head-mounted display is connected.
## 🔒︎ bool IsUsingFoveatedRendering

The value indicating if the foveated rendering is used.
## 🔒︎ Viewport Viewport

The viewport. It can be useful when implementing extra VR logic.
## 🔒︎ mat4 PlayerIModelview

The inverse model-view matrix of the camera that renders VR.
## 🔒︎ mat4 PlayerModelview

The model-view matrix of the camera that renders VR.
## 🔒︎ mat4 PlayerWorldTransform

The world transformation of the camera that renders VR.
## 🔒︎ mat4 AbsoluteToLocalWorldTransform

The transformation matrix from absolute to local tracking space. Can be used to convert poses between tracking spaces.
## 🔒︎ Event<bool> EventRenderModelsVisibility

The Event triggered when the render models visibility is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(bool **visible**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the RenderModelsVisibility event handler
void rendermodelsvisibility_event_handler(bool visible)
{
	Log.Message("\Handling RenderModelsVisibility event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections rendermodelsvisibility_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VR.EventRenderModelsVisibility.Connect(rendermodelsvisibility_event_connections, rendermodelsvisibility_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VR.EventRenderModelsVisibility.Connect(rendermodelsvisibility_event_connections, (bool visible) => {
		Log.Message("Handling RenderModelsVisibility event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
rendermodelsvisibility_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the RenderModelsVisibility event with a handler function
VR.EventRenderModelsVisibility.Connect(rendermodelsvisibility_event_handler);

// remove subscription to the RenderModelsVisibility event later by the handler function
VR.EventRenderModelsVisibility.Disconnect(rendermodelsvisibility_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection rendermodelsvisibility_event_connection;

// subscribe to the RenderModelsVisibility event with a lambda handler function and keeping the connection
rendermodelsvisibility_event_connection = VR.EventRenderModelsVisibility.Connect((bool visible) => {
		Log.Message("Handling RenderModelsVisibility event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
rendermodelsvisibility_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
rendermodelsvisibility_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
rendermodelsvisibility_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring RenderModelsVisibility events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VR.EventRenderModelsVisibility.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VR.EventRenderModelsVisibility.Enabled = true;

```

</details>

## 🔒︎ Event EventAudioSettingsChanged

The Event triggered when the audio settings changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the AudioSettingsChanged event handler
void audiosettingschanged_event_handler()
{
	Log.Message("\Handling AudioSettingsChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections audiosettingschanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VR.EventAudioSettingsChanged.Connect(audiosettingschanged_event_connections, audiosettingschanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VR.EventAudioSettingsChanged.Connect(audiosettingschanged_event_connections, () => {
		Log.Message("Handling AudioSettingsChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
audiosettingschanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the AudioSettingsChanged event with a handler function
VR.EventAudioSettingsChanged.Connect(audiosettingschanged_event_handler);

// remove subscription to the AudioSettingsChanged event later by the handler function
VR.EventAudioSettingsChanged.Disconnect(audiosettingschanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection audiosettingschanged_event_connection;

// subscribe to the AudioSettingsChanged event with a lambda handler function and keeping the connection
audiosettingschanged_event_connection = VR.EventAudioSettingsChanged.Connect(() => {
		Log.Message("Handling AudioSettingsChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
audiosettingschanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
audiosettingschanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
audiosettingschanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring AudioSettingsChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VR.EventAudioSettingsChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VR.EventAudioSettingsChanged.Enabled = true;

```

</details>

## 🔒︎ Event<int> EventDeviceRenderModelChanged

The Event triggered when the render model of the VR device is changed. You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(int **vr_device_number**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the DeviceRenderModelChanged event handler
void devicerendermodelchanged_event_handler(int vr_device_number)
{
	Log.Message("\Handling DeviceRenderModelChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections devicerendermodelchanged_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
VR.EventDeviceRenderModelChanged.Connect(devicerendermodelchanged_event_connections, devicerendermodelchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VR.EventDeviceRenderModelChanged.Connect(devicerendermodelchanged_event_connections, (int vr_device_number) => {
		Log.Message("Handling DeviceRenderModelChanged event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
devicerendermodelchanged_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the DeviceRenderModelChanged event with a handler function
VR.EventDeviceRenderModelChanged.Connect(devicerendermodelchanged_event_handler);

// remove subscription to the DeviceRenderModelChanged event later by the handler function
VR.EventDeviceRenderModelChanged.Disconnect(devicerendermodelchanged_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection devicerendermodelchanged_event_connection;

// subscribe to the DeviceRenderModelChanged event with a lambda handler function and keeping the connection
devicerendermodelchanged_event_connection = VR.EventDeviceRenderModelChanged.Connect((int vr_device_number) => {
		Log.Message("Handling DeviceRenderModelChanged event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
devicerendermodelchanged_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
devicerendermodelchanged_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
devicerendermodelchanged_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring DeviceRenderModelChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VR.EventDeviceRenderModelChanged.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
VR.EventDeviceRenderModelChanged.Enabled = true;

```

</details>

## 🔒︎ bool IsSteamVRDashboardActive

The value indicating if the SteamVR dashboard is active. When the SteamVR dashboard is open, SteamVR renders its own controllers on top of the scene. You can use this to hide your application's controller models and avoid rendering both simultaneously.
## 🔒︎ VR.RUNTIME_TYPE InputRuntimeType

The type of the VR input runtime.
## 🔒︎ string InputRuntimeName

The name of the VR input runtime.
## 🔒︎ string InputRuntimeVersion

The version of the VR input runtime.
## VR.DEBUG_MODE DebugMode

The [debug mode](#DEBUG_MODE) for VR. If the debug mode is disabled, displaying of GAPI errors in VR runtime is also disabled.
## bool RenderWhileHMDIdle

***Console*:**`vr_render_while_hmd_idle`The value indicating if rendering is enabled while HMD is not worn. The default value is **true**.
## 🔒︎ float EyeNativeFOV

The device-native vertical field of view in radians (measured from the left eye).
## float EyeOverrideFOV

The vertical field of view override value (in degrees).
## 🔒︎ bool IsEyeOverriddenFOV

The value indicating if the native vertical field of view value has been overridden (i.e., differs from the native field of view).
## float EmulationMirrorCrop

***Console*:**`vr_emulation_mirror_crop`The crop factor defining how the image is zoomed in the target window when running in VR emulation. The value 1.0 means no crop (default), and 5.0 is the maximum. Used instead of the **[MirrorCrop](../../...md#getMirrorCrop_float)** property when not rendering to an HMD.
Range of values: **[1.0f, 5.0f]**. The default value is : **1.0f**.
## vec2 EmulationMirrorCropOffset

***Console*:**`vr_emulation_mirror_crop_offset`The offset of the cropped mirror image within the target window when running in VR emulation, as normalized coordinates. The value (0, 0) corresponds to the top-left corner, (0.5, 0.5) means no offset (default), (1, 1) is the bottom-right corner. Used instead of the **[MirrorCropOffset](../../...md#getMirrorCropOffset_vec2)** property when not rendering to an HMD.

## int EmulationMirrorMode

***Console*:**`vr_emulation_mirror_mode`The mirror mode used when running in VR emulation (without rendering to an HMD), one of the *MIRROR_MODE_** values: black screen, left eye, right eye, or stereo (default). One of the following values:

## 🔒︎ VR.FOVEATED_MODE FoveatedMode

The effective foveated-rendering mode: *[DISABLED](#FOVEATED_MODE_DISABLED)* when foveated rendering is not used, *[FIXED](#FOVEATED_MODE_FIXED)* when the focus region is pinned, *[DYNAMIC](#FOVEATED_MODE_DYNAMIC)* when it follows the tracked gaze.
## float MirrorCrop

***Console*:**`vr_mirror_crop`The crop factor defining how the VR image is zoomed when mirrored to the target window. The value 1.0 means no crop, 2.0 means 2x zoom (default), and 5.0 is the maximum.
Range of values: **[1.0f, 5.0f]**. The default value is : **2.0f**.
## vec2 MirrorCropOffset

***Console*:**`vr_mirror_crop_offset`The offset of the cropped VR mirror image within the target window, as normalized coordinates. The value (0, 0) corresponds to the top-left corner, (0.5, 0.5) means no offset (default), (1, 1) is the bottom-right corner.

## vec2 PeripheralRenderingDebugGazeOverrideCoord

***Console*:**`vr_peripheral_rendering_debug_gaze_override_coord`The gaze position used when the debug override mode is set to *[COORD](#PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE_COORD)*, as normalized UV coordinates in texture space. The value (0, 0) is the top-left corner, (0.5, 0.5) is the center (default), (1, 1) is the bottom-right corner.

## int PeripheralRenderingDebugGazeOverrideMode

***Console*:**`vr_peripheral_rendering_debug_gaze_override_mode`The debug override mode for the gaze position used by peripheral (foveated) rendering, one of the *PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE_** values. Disabled by default. One of the following values:

## float ProfilerBackgroundAlpha

***Console*:**`vr_profiler_background_alpha`The opacity of the VR profiler overlay background. The value is in the [0.0; 1.0] range, 0.8 by default. Effective only when the **[ShowProfiler](../../...md#getShowProfiler_int)** property is not set to disabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.8f**.
## int ProfilerPosition

***Console*:**`vr_profiler_position`The position of the VR profiler overlay within the HMD view, one of the *PROFILER_POSITION_** values aligned with the numeric keypad layout. The default is the center of the view. Effective only when the **[ShowProfiler](../../...md#getShowProfiler_int)** property is not set to disabled. One of the following values:

## int ShowProfiler

***Console*:**`vr_show_profiler`The display mode of the profiler overlay rendered inside the HMD view, one of the *SHOW_PROFILER_** values (disabled, basic, or advanced). Disabled by default. One of the following values:

## bool ShowProfilerMemory

***Console*:**`vr_show_profiler_memory`The value indicating if the memory info panel of the VR profiler overlay is displayed. Effective only when the **[ShowProfiler](../../...md#getShowProfiler_int)** property is not set to disabled. Enabled by default. The default value is **true**.
## bool ShowProfilerMisc

***Console*:**`vr_show_profiler_misc`The value indicating if the miscellaneous info panel of the VR profiler overlay is displayed. Effective only when the **[ShowProfiler](../../...md#getShowProfiler_int)** property is not set to disabled. Enabled by default. The default value is **true**.
## bool ShowProfilerPerformance

***Console*:**`vr_show_profiler_performance`The value indicating if the performance info panel of the VR profiler overlay is displayed. Effective only when the **[ShowProfiler](../../...md#getShowProfiler_int)** property is not set to disabled. Enabled by default. The default value is **true**.
### Members

---

## ivec2 GetHMDResolution ( VR.VIEWPORT_TYPE viewport_type = Enum.VR.VIEWPORT_TYPE.CONTEXT )

Returns the current resolution of the head-mounted display. For HMDs having context (peripheral) and focus displays, you should specify the viewport type.
### Arguments

- *[VR.VIEWPORT_TYPE](../../../api/library/vr/class.vr_cs.md#VIEWPORT_TYPE)* **viewport_type** - Type of the viewport (for HMDs having context (peripheral) and focus displays).

### Return value

HMD resolution.
## bool HasFeatureMixedReality ( )

Returns a value indicating if the mixed reality mode is available on the current device and VR backend. Mixed reality enables you to combine real-world view from front-facing cameras mounted on the headset with the VR image rendered.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureEyeTracking ( )

Returns a value indicating if eye tracking is available on the current device and VR backend.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureHandTracking ( )

Returns a value indicating if hand tracking is available. This feature is natively supported when using the **OpenXR** backend (via the *XR_EXT_hand_tracking* extension).
When using the **Varjo** backend, hand tracking is available via the **[Ultraleap plugin](../../../code/plugins/ultraleap/index_cs.md)**, but this method will return false � use the plugin's API to check the hand tracking status.


> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureMotionPrediction ( )

Returns a value indicating if motion prediction is available on the current device and VR backend. When enabled, the engine submits the velocity from the GBuffer to the VR compositor.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureFoveatedRendering ( )

Returns a value indicating if foveated rendering is available on the current device and VR backend. Foveated rendering enhances performance by using eye tracking to decrease the image quality in peripheral areas where the user is not looking, allowing applications to render fewer pixels and achieve a better VR experience.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureReportProximitySensor ( )

Returns a value indicating if proximity sensor reporting is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureSupportForTreadmill ( )

Returns a value indicating if the user treadmill support is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureSupportForBaseStations ( )

Returns a value indicating if the base stations support is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureSupportForTrackers ( )

Returns a value indicating if support for trackers is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureSupportForRenderModelComponents ( )

Returns a value indicating if support for render model components is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## static bool ResetZeroPose ( )

Sets the zero pose to the current tracker position.
### Return value

true if the pose is reset successfully; otherwise, false.
## bool HasFeatureSupportForRenderModel ( )

Returns a value indicating if VR API can provide Render Models for the controllers.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureFadeToColor ( )

Returns a value indicating if the FadeToColor feature is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureFadeGrid ( )

Returns the value indicating if the FadeGrid feature is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool HasFeatureGetAudioDevice ( )

Returns the value indicating if VR API can return Audio Device name (usually Oculus only).
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## void FadeToColor ( float seconds , vec4 color , bool background )

Fades the engine render to the specified color over time.
### Arguments

- *float* **seconds** - Fade period, in seconds.
- *vec4* **color** - Target color.
- *bool* **background**

## void FadeGrid ( float seconds , bool fade_in )

Fades the engine render to/from the grid over the specified time.
### Arguments

- *float* **seconds** - Fade period, in seconds.
- *bool* **fade_in** - true fades render to grid; false fades grid to render.

## void ClearScriptableMaterials ( VR.EYE_TYPE eye )

Removes all [scriptable materials](../../../content/materials/scriptable.md) assigned to the target eye.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.

## int GetNumScriptableMaterials ( VR.EYE_TYPE eye )

Returns the number of [scriptable materials](../../../content/materials/scriptable.md) currently assigned to the specified eye.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.

### Return value

Number of scriptable materials currently assigned to the specified eye.
## Material GetScriptableMaterial ( VR.EYE_TYPE eye , int num )

Returns the [scriptable material](../../../content/materials/scriptable.md) assigned to the target eye by the number. The material's number determines the order in which the expressions assigned to it are executed.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

### Return value

Scriptable material assigned to the target eye.
## void SetScriptableMaterial ( VR.EYE_TYPE eye , int num , Material material )

Replaces the specified [scriptable material](../../../content/materials/scriptable.md) with a new scriptable material by its number for the target eye. The material's number determines the order in which the expressions assigned to it are executed.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - New scriptable material to replace the one with the specified number.

## void InsertScriptableMaterial ( VR.EYE_TYPE eye , int num , Material material )

Inserts a new [scriptable material](../../../content/materials/scriptable.md) at the specified position for the target eye. The material's number determines the order in which the expressions assigned to it are executed. To apply a scriptable material globally, use the **[InsertScriptableMaterial()](../../../api/library/rendering/class.render_cs.md#insertScriptableMaterial_int_Material_void)** method of the Render class.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Position at which the new scriptable material is to be inserted.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material to be inserted.

## int FindScriptableMaterial ( VR.EYE_TYPE eye , Material material )

Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) for the target eye. The material's number determines the order in which the expressions assigned to it are executed.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material for which the number is to be found.

### Return value

The number of the specified scriptable material for the target eye.
## void AddScriptableMaterial ( VR.EYE_TYPE eye , Material material )

Adds the specified [scriptable material](../../../content/materials/scriptable.md) to the target eye's material list. The material's number determines the order in which the expressions assigned to it are executed. To apply a scriptable material globally, use the **[AddScriptableMaterial()](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void)** method of the Render class.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material to add.

## void RemoveScriptableMaterial ( VR.EYE_TYPE eye , int num )

Removes the [scriptable material](../../../content/materials/scriptable.md) with the specified number from the target eye's material list.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

## void SwapScriptableMaterials ( VR.EYE_TYPE eye , int num_0 , int num_1 )

Swaps two [scriptable materials](../../../content/materials/scriptable.md) with the specified numbers in the target eye's material list. The material's number determines the order in which the expressions assigned to it are executed.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num_0** - Number of the first scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).
- *int* **num_1** - Number of the second scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

## void SetScriptableMaterialEnabled ( VR.EYE_TYPE eye , int num , bool enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number for the target eye. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).
- *bool* **enabled** - true to enable the scriptable material with the specified number, false to disable it.

## bool GetScriptableMaterialEnabled ( VR.EYE_TYPE eye , int num )

Returns a value indicating if the [scriptable material](../../../content/materials/scriptable.md) with the specified number is enabled (active) for the target eye. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

### Return value

true if the scriptable material with the specified number is enabled; otherwise, **false**.
## void SetEyeOffset ( VR.EYE_TYPE eye , mat4 offset )

Sets a custom transformation matrix to be applied to the target eye.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.
- *mat4* **offset** - Transformation matrix to be applied to the target eye.

## mat4 GetEyeOffset ( VR.EYE_TYPE eye )

Returns the current transformation matrix applied to the target eye.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.

### Return value

Transformation matrix currently applied to the target eye.
## void ResetEyeOffset ( VR.EYE_TYPE eye )

Resets the transformation offset of the target eye to the identity matrix.
### Arguments

- *[VR.EYE_TYPE](../../../api/library/vr/class.vr_cs.md#EYE_TYPE)* **eye** - Target eye.

## void ResetEyeOffset ( )

Resets the transformation offsets for both eyes to the identity matrix.
## void ResetEyeOverrideFOV ( )

Resets the vertical field of view override to the native value.
