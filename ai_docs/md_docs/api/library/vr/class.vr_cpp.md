# Unigine.VR Class (CPP)

**Header:** #include <UnigineVR.h>

> **Notice:** This class is a singleton.


The base class for managing virtual reality in UNIGINE.


### VR Initialization


By default, VR is not initialized. To run the engine with VR, you need to specify the [*-vr_app*](../../../vr_development/index.md#vr_init) command-line option on the application start-up.


### Supported Graphics APIs


The following graphics APIs are supported out of the box:


- DirectX 12
- Vulkan


## VR Class

### Enums

## API

| Name | Description |
|---|---|
| **API_NULL** = 0 | VR API is not initialized. |
| **API_VARJO** = 1 | Varjo API. |
| **API_OPENVR** = 2 | OpenVR API. |
| **API_OPENXR** = 3 | OpenXR API. |

## VIEWPORT_TYPE

| Name | Description |
|---|---|
| **VIEWPORT_TYPE_CONTEXT** = 0 | Context (low-res) viewport. |
| **VIEWPORT_TYPE_FOCUS** = 1 | Focus (high-res) viewport. |
| **VIEWPORT_TYPE_NUM** = 2 | Number of viewport types. |

## EYE_TYPE

| Name | Description |
|---|---|
| **EYE_TYPE_LEFT** = 0 | Left eye. |
| **EYE_TYPE_RIGHT** = 1 | Right eye. |
| **EYE_TYPE_NUM** = 2 | Number of eye types. |

## MIRROR_MODE

| Name | Description |
|---|---|
| **MIRROR_MODE_BEGIN** = 0 | The first element to be used for iteration. |
| **MIRROR_MODE_BLACK_SCREEN** = 0 | No image (black screen). |
| **MIRROR_MODE_MONO_LEFT** = 1 | Mono image for the left eye. |
| **MIRROR_MODE_MONO_RIGHT** = 2 | Mono image for the right eye. |
| **MIRROR_MODE_STEREO** = 3 | Stereo image (left and right eyes). |
| **MIRROR_MODE_END** = 3 | The last element to be used for iteration. |

## WINDOW_MODE

| Name | Description |
|---|---|
| **WINDOW_MODE_BEGIN** = 0 | The first element to be used for iteration. |
| **WINDOW_MODE_DISABLED** = 0 | Showing the mirrored image is disabled. |
| **WINDOW_MODE_MAIN** = 1 | The main window shows the mirrored image. |
| **WINDOW_MODE_END** = 1 | The last element to be used for iteration. |

## TRACKING_SPACE

| Name | Description |
|---|---|
| **TRACKING_SPACE_BEGIN** = 0 | The first element to be used for iteration. |
| **TRACKING_SPACE_LOCAL** = 0 | Local tracking space. Poses are provided relative to the Local (Seated or Stationary in OpenVR) Tracking Space. The origin is based on the user's position at startup (or after reset). Suited for sitting/simulator experiences (e.g. cockpit VR), where the player is already placed at the desired position. |
| **TRACKING_SPACE_ABSOLUTE** = 1 | Absolute tracking space. Poses are provided relative to the Absolute (Standing in OpenVR) Tracking Space. The origin is fixed to the physical floor level (established by the tracking system, e.g. Base Stations or HMD SLAM Tracking). Suited for standing/room-scale experiences where the player is placed on the floor and the camera height comes from the HMD offset. |
| **TRACKING_SPACE_END** = 1 | The last element to be used for iteration. |

## DEBUG_MODE

| Name | Description |
|---|---|
| **DEBUG_MODE_DISABLED** = 0 | Debug VR context is disabled. |
| **DEBUG_MODE_ENABLED** = 1 | Debug VR context is enabled. |
| **DEBUG_MODE_ENABLED_BREAK_ON_ERROR** = 2 | Debug VR context with the break on error option is enabled (only on debug binaries). |

## RUNTIME_TYPE

| Name | Description |
|---|---|
| **RUNTIME_TYPE_UNKNOWN** = 0 | The runtime type is unknown. |
| **RUNTIME_TYPE_NULL** = 1 | The runtime is null. |
| **RUNTIME_TYPE_STEAMVR** = 2 | SteamVR runtime. |
| **RUNTIME_TYPE_OCULUS** = 3 | Oculus runtime. |
| **RUNTIME_TYPE_VARJO** = 4 | Varjo runtime. |
| **RUNTIME_TYPE_WMR** = 5 | Windows Mixed Reality OpenXR runtime. |

### Members

## void setRenderEnabled ( bool enabled = 0 )

***Console*:**`vr_render_enabled`Sets a new value indicating if rendering into the head-mounted display is enabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *bool* **enabled** - Set **true** to enable rendering into the HMD; **false** - to disable it. The default value is **false**.

## bool isRenderEnabled () const

***Console*:**`vr_render_enabled`Returns the current value indicating if rendering into the head-mounted display is enabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

**true** if rendering into the HMD is enabled; otherwise **false**. The default value is **false**.
## void setPeripheralRenderingModeEnabled ( bool enabled = 1 )

***Console*:**`vr_peripheral_rendering_mode_enabled`Sets a new value indicating if the peripheral rendering mode is enabled. In this mode, the HMD has two context (peripheral) and two focus viewports. You can disable two additional viewports to improve peformance. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *bool* **enabled** - Set **true** to enable the peripheral rendering mode; **false** - to disable it. The default value is **true**.

## bool isPeripheralRenderingModeEnabled () const

***Console*:**`vr_peripheral_rendering_mode_enabled`Returns the current value indicating if the peripheral rendering mode is enabled. In this mode, the HMD has two context (peripheral) and two focus viewports. You can disable two additional viewports to improve peformance. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

**true** if the peripheral rendering mode is enabled; otherwise **false**. The default value is **true**.
## void setPeripheralRenderingDebugEnabled ( bool enabled = 1 )

***Console*:**`vr_peripheral_rendering_debug_enabled`Sets a new value indicating if debug visualization for peripheral rendering is enabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *bool* **enabled** - Set **true** to enable debug visualization for peripheral rendering; **false** - to disable it. The default value is **true**.

## bool isPeripheralRenderingDebugEnabled () const

***Console*:**`vr_peripheral_rendering_debug_enabled`Returns the current value indicating if debug visualization for peripheral rendering is enabled. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

**true** if debug visualization for peripheral rendering is enabled; otherwise **false**. The default value is **true**.
## void setPeripheralRenderingBorderWidth ( float width = 0.2f )

***Console*:**`vr_peripheral_rendering_border_width`Sets a new width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **width** - The width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible. Range of values: **[eps, 1.0f]**. The default value is : **0.2f**.

## float getPeripheralRenderingBorderWidth () const

***Console*:**`vr_peripheral_rendering_border_width`Returns the current width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current width of the transition border between foveal (focus) and context rendering zones. A value of 1.0 means the entire viewport has a wide, smooth transition. A very small value (close to epsilon) means the transition will be extremely narrow and almost invisible.
Range of values: **[eps, 1.0f]**. The default value is : **0.2f**.
## void setPeripheralRenderingFOVScale ( const Math:: vec2 & fovscale )

***Console*:**`vr_peripheral_rendering_fov_scale`Sets a new scale factor applied to the field of view used for focus viewports. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **fovscale** - The scale factor applied to the field of view used for focus viewports. **[0; 1]** - available range. **(0.3f, 0.3f)** - default value.

## Math:: vec2 getPeripheralRenderingFOVScale () const

***Console*:**`vr_peripheral_rendering_fov_scale`Returns the current scale factor applied to the field of view used for focus viewports. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current scale factor applied to the field of view used for focus viewports.
**[0; 1]** - available range.
**(0.3f, 0.3f)** - default value.
## void setPeripheralRenderingFocusScale ( const Math:: vec2 & scale )

***Console*:**`vr_peripheral_rendering_focus_scale`Sets a new scale factor controlling the size of the foveal (focus) area. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md)&* **scale** - The scale factor controlling the size of the foveal (focus) area. **[0; 1]** - available range. **(0.5f, 0.2f)** - default value.

## Math:: vec2 getPeripheralRenderingFocusScale () const

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
## void setMirrorMode ( VR::MIRROR_MODE mode = 3 )

***Console*:**`vr_mirror_mode`Sets a new mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *[VR::MIRROR_MODE](../../../api/library/vr/class.vr_cpp.md#MIRROR_MODE)* **mode** - The mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. One of the following values:

  - **0** - black screen (no image is displayed).
  - **1** - image rendered for the left eye.
  - **2** - image rendered for the right eye.
  - **3** - stereo image (both the left and right eyes). (by default)

## VR::MIRROR_MODE getMirrorMode () const

***Console*:**`vr_mirror_mode`Returns the current mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current mirror mode that defines how the mirrored image (i.e. VR image) will be displayed in the target window. One of the following values:
- **0** - black screen (no image is displayed).
- **1** - image rendered for the left eye.
- **2** - image rendered for the right eye.
- **3** - stereo image (both the left and right eyes). (by default)

## void setWindowMode ( VR::WINDOW_MODE mode = 1 )

***Console*:**`vr_window_mode`Sets a new window mode that defines which window will display the mirrored image (i.e. VR image). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *[VR::WINDOW_MODE](../../../api/library/vr/class.vr_cpp.md#WINDOW_MODE)* **mode** - The window mode that defines which window will display the mirrored image (i.e. VR image). One of the following values:

  - **0** - mirroring is disabled.
  - **1** - main window displays the mirrored image. (by default)

## VR::WINDOW_MODE getWindowMode () const

***Console*:**`vr_window_mode`Returns the current window mode that defines which window will display the mirrored image (i.e. VR image). This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current window mode that defines which window will display the mirrored image (i.e. VR image). One of the following values:
- **0** - mirroring is disabled.
- **1** - main window displays the mirrored image. (by default)

## void setTrackingSpace ( VR::TRACKING_SPACE space = 1 )

***Console*:**`vr_tracking_space`Sets a new zero pose of the tracking origin. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *[VR::TRACKING_SPACE](../../../api/library/vr/class.vr_cpp.md#TRACKING_SPACE)* **space** - The zero pose of the tracking origin. One of the following values:

  - **0** - poses are provided relative to the Local (Seated or Stationary in OpenVR) Tracking Space. The origin is based on the user's position at startup (or after reset). Suited for sitting/simulator experiences (e.g. cockpit VR), where the player is already placed at the desired position.
  - **1** - poses are provided relative to the Absolute (Standing in OpenVR) Tracking Space. The origin is fixed to the physical floor level (established by the tracking system, e.g. Base Stations or HMD SLAM Tracking). Suited for standing/room-scale experiences where the player is placed on the floor and the camera height comes from the HMD offset. (by default)

## VR::TRACKING_SPACE getTrackingSpace () const

***Console*:**`vr_tracking_space`Returns the current zero pose of the tracking origin. This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current zero pose of the tracking origin. One of the following values:
- **0** - poses are provided relative to the Local (Seated or Stationary in OpenVR) Tracking Space. The origin is based on the user's position at startup (or after reset). Suited for sitting/simulator experiences (e.g. cockpit VR), where the player is already placed at the desired position.
- **1** - poses are provided relative to the Absolute (Standing in OpenVR) Tracking Space. The origin is fixed to the physical floor level (established by the tracking system, e.g. Base Stations or HMD SLAM Tracking). Suited for standing/room-scale experiences where the player is placed on the floor and the camera height comes from the HMD offset. (by default)

## void setMotionPrediction ( bool prediction = 0 )

***Console*:**`vr_motion_prediction`Sets a new value indicating if motion prediction in the Varjo headsets is enabled. When enabled, the engine submits the velocity value from the GBuffer to the Varjo Composer.
> **Notice:** This feature is available for the *Varjo devices only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *bool* **prediction** - Set **true** to enable motion prediction; **false** - to disable it. The default value is **false**.

## bool isMotionPrediction () const

***Console*:**`vr_motion_prediction`Returns the current value indicating if motion prediction in the Varjo headsets is enabled. When enabled, the engine submits the velocity value from the GBuffer to the Varjo Composer.
> **Notice:** This feature is available for the *Varjo devices only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

**true** if motion prediction is enabled; otherwise **false**. The default value is **false**.
## void setMotionPredictionVelocityPrecision ( float precision = 32.0f )

***Console*:**`vr_motion_prediction_velocity_precision`Sets a new factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint).
> **Notice:** This feature is available for the *Varjo devices only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **precision** - The factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint). Range of values: **[eps, inf]**. The default value is : **32.0f**.

## float getMotionPredictionVelocityPrecision () const

***Console*:**`vr_motion_prediction_velocity_precision`Returns the current factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint).
> **Notice:** This feature is available for the *Varjo devices only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current factor of velocity scale before packing a floating point value into a 2x8 bit unsigned integer (uint).
Range of values: **[eps, inf]**. The default value is : **32.0f**.
## void setMotionPredictionVelocityTimeDelta ( float delta = 1.0f / 60.0f )

***Console*:**`vr_motion_prediction_velocity_time_delta`Sets a new factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa.
> **Notice:** This feature is available for the *Varjo devices only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *float* **delta** - The factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa. Range of values: **[eps, inf]**. The default value is : **1.0f / 60.0f**.

## float getMotionPredictionVelocityTimeDelta () const

***Console*:**`vr_motion_prediction_velocity_time_delta`Returns the current factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa.
> **Notice:** This feature is available for the *Varjo devices only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current factor for optimizing between fast and slow-moving objects. A smaller number works better for fast-moving objects, and vice versa.
Range of values: **[eps, inf]**. The default value is : **1.0f / 60.0f**.
## void setFoveatedRenderingEnabled ( bool enabled = 1 )

***Console*:**`vr_foveated_rendering_enabled`Sets a new value indicating if foveated rendering is enabled. Foveated rendering makes use of the eye tracking functionality in the Varjo headsets to improve performance by reducing the image quality in peripheral areas where the user is not looking. Foveation allows applications to render fewer pixels and achieve a better VR experience.
> **Notice:** This feature is available for the *Varjo devices only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *bool* **enabled** - Set **true** to enable foveated rendering; **false** - to disable it. The default value is **true**.

## bool isFoveatedRenderingEnabled () const

***Console*:**`vr_foveated_rendering_enabled`Returns the current value indicating if foveated rendering is enabled. Foveated rendering makes use of the eye tracking functionality in the Varjo headsets to improve performance by reducing the image quality in peripheral areas where the user is not looking. Foveation allows applications to render fewer pixels and achieve a better VR experience.
> **Notice:** This feature is available for the *Varjo devices only*.

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

**true** if foveated rendering is enabled; otherwise **false**. The default value is **true**.
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
## VR::API getApiType () const

Returns the current type of the VR API.
### Return value

Current type of the VR API.
## float getHMDRefreshRate () const

Returns the current refresh rate of the head-mounted display.
### Return value

Current refresh rate of the HMD.
## Math:: Vec3 getHandTrackingOffset () const

Returns the current hand tracking offset (for the Ultraleap device only).
### Return value

Current hand tracking offset.
## bool isHandTrackingOffsetSupported () const

Returns the current value indicating if the hand tracking offset is supported.
### Return value

**true** if the hand tracking offset is supported; otherwise **false**.
## bool isPeripheralRenderingModeUsed () const

Returns the current value indicating if the peripheral rendering is used.
### Return value

**true** if the peripheral rendering is used; otherwise **false**.
## bool isHMDConnected () const

Returns the current value indicating if the head-mounted display is connected.
### Return value

**true** if the HMD is connected; otherwise **false**.
## bool isUsingFoveatedRendering () const

Returns the current value indicating if the foveated rendering is used.
### Return value

**true** if the foveated rendering is used; otherwise **false**.
## Ptr < Viewport > getViewport () const

Returns the current viewport. It can be useful when implementing extra VR logic.
### Return value

Current viewport.
## Math:: Mat4 getPlayerIModelview () const

Returns the current inverse model-view matrix of the camera that renders VR.
### Return value

Current inverse model-view matrix.
## Math:: Mat4 getPlayerModelview () const

Returns the current model-view matrix of the camera that renders VR.
### Return value

Current model-view matrix.
## Math:: Mat4 getPlayerWorldTransform () const

Returns the current world transformation of the camera that renders VR.
### Return value

Current world transformation matrix.
## Math:: Mat4 getAbsoluteToLocalWorldTransform () const

Returns the current transformation matrix from absolute to local tracking space. Can be used to convert poses between tracking spaces.
### Return value

Current transformation matrix from absolute to local tracking space.
## static Event<bool> getEventRenderModelsVisibility () const

Event triggered when the render models visibility is changed. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**visible**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the RenderModelsVisibility event handler
void rendermodelsvisibility_event_handler(visible)
{
	Log::message("\Handling RenderModelsVisibility event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections rendermodelsvisibility_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VR::getEventRenderModelsVisibility().connect(rendermodelsvisibility_event_connections, rendermodelsvisibility_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VR::getEventRenderModelsVisibility().connect(rendermodelsvisibility_event_connections, [](visible) {
		Log::message("\Handling RenderModelsVisibility event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
rendermodelsvisibility_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection rendermodelsvisibility_event_connection;

// subscribe to the RenderModelsVisibility event with a handler function keeping the connection
VR::getEventRenderModelsVisibility().connect(rendermodelsvisibility_event_connection, rendermodelsvisibility_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
rendermodelsvisibility_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
rendermodelsvisibility_event_connection.setEnabled(true);

// ...

// remove subscription to the RenderModelsVisibility event via the connection
rendermodelsvisibility_event_connection.disconnect();

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

	// A RenderModelsVisibility event handler implemented as a class member
	void event_handler(visible)
	{
		Log::message("\Handling RenderModelsVisibility event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VR::getEventRenderModelsVisibility().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId rendermodelsvisibility_handler_id;

// subscribe to the RenderModelsVisibility event with a lambda handler function and keeping connection ID
rendermodelsvisibility_handler_id = VR::getEventRenderModelsVisibility().connect(e_connections, [](visible) {
		Log::message("\Handling RenderModelsVisibility event (lambda).\n");
	}
);

// remove the subscription later using the ID
VR::getEventRenderModelsVisibility().disconnect(rendermodelsvisibility_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all RenderModelsVisibility events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VR::getEventRenderModelsVisibility().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VR::getEventRenderModelsVisibility().setEnabled(true);

```

</details>

### Return value

Event reference.
## static Event<> getEventAudioSettingsChanged () const

Event triggered when the audio settings changed. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the AudioSettingsChanged event handler
void audiosettingschanged_event_handler()
{
	Log::message("\Handling AudioSettingsChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections audiosettingschanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VR::getEventAudioSettingsChanged().connect(audiosettingschanged_event_connections, audiosettingschanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VR::getEventAudioSettingsChanged().connect(audiosettingschanged_event_connections, []() {
		Log::message("\Handling AudioSettingsChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
audiosettingschanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection audiosettingschanged_event_connection;

// subscribe to the AudioSettingsChanged event with a handler function keeping the connection
VR::getEventAudioSettingsChanged().connect(audiosettingschanged_event_connection, audiosettingschanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
audiosettingschanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
audiosettingschanged_event_connection.setEnabled(true);

// ...

// remove subscription to the AudioSettingsChanged event via the connection
audiosettingschanged_event_connection.disconnect();

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

	// A AudioSettingsChanged event handler implemented as a class member
	void event_handler()
	{
		Log::message("\Handling AudioSettingsChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VR::getEventAudioSettingsChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId audiosettingschanged_handler_id;

// subscribe to the AudioSettingsChanged event with a lambda handler function and keeping connection ID
audiosettingschanged_handler_id = VR::getEventAudioSettingsChanged().connect(e_connections, []() {
		Log::message("\Handling AudioSettingsChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
VR::getEventAudioSettingsChanged().disconnect(audiosettingschanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all AudioSettingsChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VR::getEventAudioSettingsChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VR::getEventAudioSettingsChanged().setEnabled(true);

```

</details>

### Return value

Event reference.
## static Event<int> getEventDeviceRenderModelChanged () const

Event triggered when the render model of the VR device is changed. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(**vr_device_number**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the DeviceRenderModelChanged event handler
void devicerendermodelchanged_event_handler(vr_device_number)
{
	Log::message("\Handling DeviceRenderModelChanged event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections devicerendermodelchanged_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
VR::getEventDeviceRenderModelChanged().connect(devicerendermodelchanged_event_connections, devicerendermodelchanged_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
VR::getEventDeviceRenderModelChanged().connect(devicerendermodelchanged_event_connections, [](vr_device_number) {
		Log::message("\Handling DeviceRenderModelChanged event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
devicerendermodelchanged_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection devicerendermodelchanged_event_connection;

// subscribe to the DeviceRenderModelChanged event with a handler function keeping the connection
VR::getEventDeviceRenderModelChanged().connect(devicerendermodelchanged_event_connection, devicerendermodelchanged_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
devicerendermodelchanged_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
devicerendermodelchanged_event_connection.setEnabled(true);

// ...

// remove subscription to the DeviceRenderModelChanged event via the connection
devicerendermodelchanged_event_connection.disconnect();

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

	// A DeviceRenderModelChanged event handler implemented as a class member
	void event_handler(vr_device_number)
	{
		Log::message("\Handling DeviceRenderModelChanged event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
VR::getEventDeviceRenderModelChanged().connect(sc->e_connections, sc, &SomeClass::event_handler);

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
EventConnectionId devicerendermodelchanged_handler_id;

// subscribe to the DeviceRenderModelChanged event with a lambda handler function and keeping connection ID
devicerendermodelchanged_handler_id = VR::getEventDeviceRenderModelChanged().connect(e_connections, [](vr_device_number) {
		Log::message("\Handling DeviceRenderModelChanged event (lambda).\n");
	}
);

// remove the subscription later using the ID
VR::getEventDeviceRenderModelChanged().disconnect(devicerendermodelchanged_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all DeviceRenderModelChanged events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
VR::getEventDeviceRenderModelChanged().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
VR::getEventDeviceRenderModelChanged().setEnabled(true);

```

</details>

### Return value

Event reference.
## bool isSteamVRDashboardActive () const

Returns the current value indicating if the SteamVR controllers are rendered. When you access the SteamVR menu during the application runtime, the SteamVR controllers start to be rendered along with the application controllers. You can use this function to check the state of the SteamVR controllers and disable the application controllers to avoid performance drops caused by the simultaneous rendering of both controllers.
### Return value

**true** if the SteamVR controllers are rendered is enabled; otherwise **false**.
## VR::RUNTIME_TYPE getInputRuntimeType () const

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
## void setDebugMode ( VR::DEBUG_MODE mode )

Sets a new [debug mode](#DEBUG_MODE) for VR. If the debug mode is disabled, displaying of GAPI errors in VR runtime is also disabled.
### Arguments

- *[VR::DEBUG_MODE](../../../api/library/vr/class.vr_cpp.md#DEBUG_MODE)* **mode** - The debug mode for VR.

## VR::DEBUG_MODE getDebugMode () const

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

**true** if rendering while HMD is not worn is enabled; otherwise **false**. The default value is **true**.
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
---

## Math:: ivec2 getHMDResolution ( VR::VIEWPORT_TYPE viewport_type = Enum.VR.VIEWPORT_TYPE.CONTEXT ) const

Returns the current resolution of the head-mounted display. For HMDs having context (peripheral) and focus displays, you should specify the viewport type.
### Arguments

- *[VR::VIEWPORT_TYPE](../../../api/library/vr/class.vr_cpp.md#VIEWPORT_TYPE)* **viewport_type** - Type of the viewport (for HMDs having context (peripheral) and focus displays).

### Return value

HMD resolution.
## bool hasFeatureMixedReality ( ) const

Returns a value indicating if the mixed reality mode is available. Mixed reality enables you to combine real-world view from front-facing cameras mounted on the headset with the VR image rendered. This feature is available for the *Varjo devices only*.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureEyeTracking ( ) const

Returns a value indicating if eye tracking is available. This feature is available for the *Varjo devices only*.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureHandTracking ( ) const

Returns a value indicating if hand tracking is available. This feature is available for the *Varjo devices only*.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureMotionPrediction ( ) const

Returns a value indicating if motion prediction is available. This feature is available for the *Varjo devices only*. It allows the engine to submit the velocity from the GBuffer to the Varjo Composer.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureFoveatedRendering ( ) const

Returns a value indicating if foveated rendering is available. This feature is available for the *Varjo devices only*. Foveated rendering enhances performance by using the eye tracking functionality in Varjo headsets: it decreases the image quality in the peripheral areas where the user is not looking. Foveation allows applications to render fewer pixels and achieve a better VR experience.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureReportProximitySensor ( ) const

Returns a value indicating if proximity sensor reporting is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureSupportForTreadmill ( ) const

Returns a value indicating if the user treadmill support is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureSupportForBaseStations ( ) const

Returns a value indicating if the base stations support is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureSupportForTrackers ( ) const

Returns a value indicating if support for trackers is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureSupportForRenderModelComponents ( ) const

Returns a value indicating if support for render model components is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## static bool resetZeroPose ( )

Sets the zero pose to the current tracker position.
### Return value

true if the pose is reset successfully; otherwise, false.
## bool hasFeatureSupportForRenderModel ( ) const

Returns a value indicating if VR API can provide Render Models for the controllers.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureFadeToColor ( ) const

Returns a value indicating if the FadeToColor feature is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureFadeGrid ( ) const

Returns the value indicating if the FadeGrid feature is available.
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## bool hasFeatureGetAudioDevice ( ) const

Returns the value indicating if VR API can return Audio Device name (usually Oculus only).
> **Notice:** If VR is not initialized, the function will return false.


### Return value

true if the feature is available; otherwise, false.
## void fadeToColor ( float seconds , const Math:: vec4 & color , bool background )

Fades the engine render to the specified color over time.
### Arguments

- *float* **seconds** - Fade period, in seconds.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Target color.
- *bool* **background**

## void fadeGrid ( float seconds , bool fade_in )

Fades the engine render to/from the grid over the specified time.
### Arguments

- *float* **seconds** - Fade period, in seconds.
- *bool* **fade_in** - true fades render to grid; false fades grid to render.

## void clearScriptableMaterials ( VR::EYE_TYPE eye )

Removes all [scriptable materials](../../../content/materials/scriptable.md) assigned to the target eye.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.

## int getNumScriptableMaterials ( VR::EYE_TYPE eye )

Returns the number of [scriptable materials](../../../content/materials/scriptable.md) currently assigned to the specified eye.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.

### Return value

Number of scriptable materials currently assigned to the specified eye.
## Ptr < Material > getScriptableMaterial ( VR::EYE_TYPE eye , int num ) const

Returns the [scriptable material](../../../content/materials/scriptable.md) assigned to the target eye by the number. The material's number determines the order in which the expressions assigned to it are executed.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

### Return value

Scriptable material assigned to the target eye.
## void setScriptableMaterial ( VR::EYE_TYPE eye , int num , const Ptr < Material > & material )

Replaces the specified [scriptable material](../../../content/materials/scriptable.md) with a new scriptable material by its number for the target eye. The material's number determines the order in which the expressions assigned to it are executed.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - New scriptable material to replace the one with the specified number.

## void insertScriptableMaterial ( VR::EYE_TYPE eye , int num , const Ptr < Material > & material )

Inserts a new [scriptable material](../../../content/materials/scriptable.md) at the specified position for the target eye. The material's number determines the order in which the expressions assigned to it are executed. To apply a scriptable material globally, use the **[insertScriptableMaterial()](../../../api/library/rendering/class.render_cpp.md#insertScriptableMaterial_int_Material_void)** method of the Render class.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Position at which the new scriptable material is to be inserted.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Scriptable material to be inserted.

## int findScriptableMaterial ( VR::EYE_TYPE eye , const Ptr < Material > & material ) const

Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) for the target eye. The material's number determines the order in which the expressions assigned to it are executed.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Scriptable material for which the number is to be found.

### Return value

The number of the specified scriptable material for the target eye.
## void addScriptableMaterial ( VR::EYE_TYPE eye , const Ptr < Material > & material )

Adds the specified [scriptable material](../../../content/materials/scriptable.md) to the target eye's material list. The material's number determines the order in which the expressions assigned to it are executed. To apply a scriptable material globally, use the **[addScriptableMaterial()](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_int_Material_void)** method of the Render class.
> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-eye.


### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Scriptable material to add.

## void removeScriptableMaterial ( VR::EYE_TYPE eye , int num )

Removes the [scriptable material](../../../content/materials/scriptable.md) with the specified number from the target eye's material list.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

## void swapScriptableMaterials ( VR::EYE_TYPE eye , int num_0 , int num_1 )

Swaps two [scriptable materials](../../../content/materials/scriptable.md) with the specified numbers in the target eye's material list. The material's number determines the order in which the expressions assigned to it are executed.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num_0** - Number of the first scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).
- *int* **num_1** - Number of the second scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

## void setScriptableMaterialEnabled ( VR::EYE_TYPE eye , int num , bool enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number for the target eye. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).
- *bool* **enabled** - true to enable the scriptable material with the specified number, false to disable it.

## bool getScriptableMaterialEnabled ( VR::EYE_TYPE eye , int num ) const

Returns a value indicating if the [scriptable material](../../../content/materials/scriptable.md) with the specified number is enabled (active) for the target eye. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int_int).

### Return value

true if the scriptable material with the specified number is enabled; otherwise, **false**.
## void setEyeOffset ( VR::EYE_TYPE eye , const Math:: mat4 & offset )

Sets a custom transformation matrix to be applied to the target eye.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **offset** - Transformation matrix to be applied to the target eye.

## Math:: mat4 getEyeOffset ( VR::EYE_TYPE eye ) const

Returns the current transformation matrix applied to the target eye.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.

### Return value

Transformation matrix currently applied to the target eye.
## void resetEyeOffset ( VR::EYE_TYPE eye )

Resets the transformation offset of the target eye to the identity matrix.
### Arguments

- *[VR::EYE_TYPE](../../../api/library/vr/class.vr_cpp.md#EYE_TYPE)* **eye** - Target eye.

## void resetEyeOffset ( )

Resets the transformation offsets for both eyes to the identity matrix.
## void resetEyeOverrideFOV ( )

Resets the vertical field of view override to the native value.
