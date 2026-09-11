# VR Input System (CPP)


VR input is different from regular keyboard-and-mouse input: VR devices exist in 3D space - they have position, orientation, and velocity, and are tracked as the user moves. The Engine gives you access to **where** each device is, **what buttons** are pressed, **how far** analog controls are pushed, and lets you send **haptic feedback** (vibration) back to the user. The input API is the same regardless of the backend (OpenXR, OpenVR, Varjo).


> **Notice:** The **[VR Template](../vr_development/vr_template/index.md)** already handles controller input for you - grabbing objects, teleportation, laser pointers, and haptic feedback are all implemented and ready to use. We recommend starting from the Template rather than writing input code from scratch. This article explains the underlying API for when you need to customize or extend that behavior.


## Device Types


The Engine recognizes four types of VR devices:


| Type | Class | What It Is | Data |
|---|---|---|---|
| HMD | *[InputVRHead](../api/library/controls/class.inputvrhead_cpp.md)* | The headset. | Transform, display refresh rate (*[InputVRHead::getRefreshRate](../api/library/controls/class.inputvrhead_cpp.md#)*), tracking enable/disable, optional buttons. |
| Controller | *[InputVRController](../api/library/controls/class.inputvrcontroller_cpp.md)* | A hand-held controller. | Transform, buttons, touch sensors, analog axes (joystick, trigger, grip, trackpad), haptic feedback (*[InputVRController::applyHaptic](../api/library/controls/class.inputvrcontroller_cpp.md#)*). |
| Tracker | *[InputVRTracker](../api/library/controls/class.inputvrtracker_cpp.md)* | An external tracking puck (e.g., SteamVR Tracker). **OpenVR only.** | Transform only. |
| Base Station | *[InputVRBaseStation](../api/library/controls/class.inputvrbasestation_cpp.md)* | A Lighthouse tracking reference. **OpenVR only.** | Transform only. |


All devices are accessed through the *[Input](../api/library/controls/class.input_cpp.md)* class and share a common base - *[InputVRDevice](../api/library/controls/class.inputvrdevice_cpp.md)*. Before reading any data, check *[InputVRDevice::isAvailable](../api/library/controls/class.inputvrdevice_cpp.md#)* - the device may be turned off or out of tracking range. Every device also reports:


- Name and model - *[InputVRDevice::getName](../api/library/controls/class.inputvrdevice_cpp.md#)*, *[InputVRDevice::getDeviceModelName](../api/library/controls/class.inputvrdevice_cpp.md#)*
- Hardware identifiers - *[InputVRDevice::getSerialNumber](../api/library/controls/class.inputvrdevice_cpp.md#)*, *[InputVRDevice::getManufacturerName](../api/library/controls/class.inputvrdevice_cpp.md#)*
- Battery level and charging state - *[InputVRDevice::getBatteryValue](../api/library/controls/class.inputvrdevice_cpp.md#)*, *[InputVRDevice::isCharging](../api/library/controls/class.inputvrdevice_cpp.md#)*


> **Notice:** Hand tracking is a separate subsystem with its own API - see *[VRHandTracking](../api/library/vr/class.vrhandtracking_cpp.md)*, *[VRHand](../api/library/vr/class.vrhand_cpp.md)*, and *[VRBone](../api/library/vr/class.vrbone_cpp.md)*. It provides a full 26-joint bone hierarchy per hand and is available on devices that support it (OpenXR and Varjo backends).


## Accessing VR Devices


All VR devices are accessed through static methods of the *[Input](../api/library/controls/class.input_cpp.md)* class. Controllers are split into left and right:


```cpp
// Get the headset
InputVRHeadPtr head = Input::getVRHead();

// Get hand controllers
InputVRControllerPtr left  = Input::getVRControllerLeft();
InputVRControllerPtr right = Input::getVRControllerRight();

```


Always check *[InputVRDevice::isAvailable](../api/library/controls/class.inputvrdevice_cpp.md#)* before reading data - the device may be turned off, out of range, or simply not present:


```cpp
InputVRControllerPtr right = Input::getVRControllerRight();
if (right && right->isAvailable())
{
	// safe to read buttons, axes, transforms
}

```


You can also check the controller hand assignment at runtime via *[InputVRController::getControllerType](../api/library/controls/class.inputvrcontroller_cpp.md#)*, which returns *CONTROLLER_TYPE_HAND_LEFT* or *CONTROLLER_TYPE_HAND_RIGHT*.


## Transforms


Every VR device has a position and orientation in 3D space - its **transform**. A single device can provide several transforms depending on how you want to use it. The type is specified via *[InputVRDevice::TRANSFORM_TYPE](../api/library/controls/class.inputvrdevice_cpp.md#TRANSFORM_TYPE)*:


| Transform Type | Device | Backend | What You Get |
|---|---|---|---|
| *TRANSFORM_TYPE_AIM* | Controller | OpenXR | Pointing direction of the controller. Use for raycasts, laser pointers, aiming. **Default** when no type is specified. |
| *TRANSFORM_TYPE_GRIP* | Controller, HMD | OpenXR, OpenVR, Varjo | Where the user's hand grips the controller (or head position for HMD). Use for attaching virtual objects to the hand - a sword, a tool, a grabbed item. |
| *TRANSFORM_TYPE_MESH* | Controller | OpenXR | Origin point for the controller's 3D model. Use when rendering controller geometry. |
| *TRANSFORM_TYPE_PINCH* | Controller (hand tracking) | OpenXR | Point between thumb and index finger tips. Use for picking up small objects, precision manipulation. |
| *TRANSFORM_TYPE_POKE* | Controller (hand tracking) | OpenXR | Tip of the index finger. Use for pressing virtual buttons, touching UI elements. |
| *TRANSFORM_TYPE_GAZE* | HMD (eye tracking) | OpenXR | Direction the user is looking at. Origin is between the eyes, forward axis follows gaze. Use for gaze-based selection, foveated rendering hints. |


To get a transform in code, call *[InputVRDevice::getWorldTransform](../api/library/controls/class.inputvrdevice_cpp.md#)* with the desired type. If no type is specified, *TRANSFORM_TYPE_AIM* is used by default:


```cpp
InputVRControllerPtr right = Input::getVRControllerRight();

// Pointing direction - use for raycasts / laser pointers
Mat4 aim = right->getWorldTransform(InputVRDevice::TRANSFORM_TYPE_AIM);

// Hand grip position - use for attaching objects to the hand
Mat4 grip = right->getWorldTransform(InputVRDevice::TRANSFORM_TYPE_GRIP);

// You can also read velocity (useful for throwing objects)
vec3 velocity = right->getLinearVelocity(InputVRDevice::TRANSFORM_TYPE_GRIP);

```


Before reading a specific transform type, you can check if the current device supports it via *[InputVRDevice::isTransformTypeSupported](../api/library/controls/class.inputvrdevice_cpp.md#)*. For example, *TRANSFORM_TYPE_PINCH* and *TRANSFORM_TYPE_POKE* are only available with hand tracking.


## Head-Mounted Display


The HMD (*[InputVRHead](../api/library/controls/class.inputvrhead_cpp.md)*) is the primary tracking device. Its main job is to tell the Engine where the user's head is and which way it faces.


### Tracking Space


All coordinates that come from the headset are measured relative to a **tracking space** - a coordinate system managed by the VR runtime (SteamVR, Quest app, Varjo Base). The Engine supports two modes (*[VR::TRACKING_SPACE](../api/library/vr/class.vr_cpp.md#TRACKING_SPACE)*):


| Mode | Origin | When to Use |
|---|---|---|
| *TRACKING_SPACE_LOCAL* | Where the headset was when the application started. | Seated or stationary applications - the user stays in one place (cockpit, desk, control panel). |
| *TRACKING_SPACE_ABSOLUTE* | On the floor of the play area. | Room-scale applications - the user walks around, and coordinates reflect their real position in the room. |


> **Notice:** In ABSOLUTE mode the floor level is determined by the VR runtime, not by the Engine. If the runtime does not provide floor data, the Engine falls back to an estimated height of 1.5 m.


### Tracking Origin


The active Player node acts as the tracking origin - the zero point for all VR tracking. The headset's position is applied as an offset on top of it each frame.


The Player node's position in the scene defines where the user "stands". Physical movement (leaning, stepping) shifts the camera relative to that point. Moving the Player node via code relocates the user entirely.


Position and rotation tracking can be toggled independently via *[InputVRHead::setTrackingPositionEnabled](../api/library/controls/class.inputvrhead_cpp.md#)* and *[InputVRHead::setTrackingRotationEnabled](../api/library/controls/class.inputvrhead_cpp.md#)*. Disabling position tracking locks the camera to the Player node's position - only rotation follows the headset. This is useful for cutscenes or fixed-viewpoint experiences.


To recenter tracking to the user's current position and facing direction, call *[VR::resetZeroPose](../api/library/vr/class.vr_cpp.md#)*.


## Buttons and Axes


VR controllers have physical buttons (face buttons, triggers, grips, system buttons) and analog axes (joystick position, trigger squeeze amount, grip pressure). The Engine maps all of them to unified enums - *[Input::VR_BUTTON](../api/library/controls/class.input_cpp.md#VR_BUTTON)* for buttons and *[InputVRController::AXIS_TYPE](../api/library/controls/class.inputvrcontroller_cpp.md#AXIS_TYPE)* for axes - so the same code works across all backends and controller models. Some controllers also distinguish between a physical **press** and a **touch** (finger resting on the button without pressing).


Not every controller has every button or axis. The available set depends on the hardware. For exact mappings per controller, see the [Controller Reference](#controller_reference) at the end of this article.


### Checking Buttons


Each button has three states you can check:


- *[InputVRController::isButtonDown](../api/library/controls/class.inputvrcontroller_cpp.md#)* - *true* on the frame when the button is first pressed
- *[InputVRController::isButtonPressed](../api/library/controls/class.inputvrcontroller_cpp.md#)* - *true* every frame while the button is held down
- *[InputVRController::isButtonUp](../api/library/controls/class.inputvrcontroller_cpp.md#)* - *true* on the frame when the button is released


Some controllers also detect whether a finger is **touching** a button without pressing it (capacitive sensing). Use the corresponding touch methods: *[InputVRController::isButtonTouchDown](../api/library/controls/class.inputvrcontroller_cpp.md#)*, *[InputVRController::isButtonTouchPressed](../api/library/controls/class.inputvrcontroller_cpp.md#)*, *[InputVRController::isButtonTouchUp](../api/library/controls/class.inputvrcontroller_cpp.md#)*.


```cpp
InputVRControllerPtr right = Input::getVRControllerRight();
if (right && right->isAvailable())
{
	// Button just pressed this frame
	if (right->isButtonDown(Input::VR_BUTTON_X))
		Log::message("A/X button pressed!\n");

	// Trigger held down
	if (right->isButtonPressed(Input::VR_BUTTON_AXIS_0))
		Log::message("Trigger is held\n");

	// Finger touching the thumbstick (not pressing)
	if (right->isButtonTouchPressed(Input::VR_BUTTON_AXIS_0))
		Log::message("Finger on thumbstick\n");
}

```


### Reading Axes


Analog values (how far a trigger is squeezed, where the thumbstick is tilted) are read via *[InputVRController::getAxisByType](../api/library/controls/class.inputvrcontroller_cpp.md#)*:


```cpp
InputVRControllerPtr right = Input::getVRControllerRight();
if (right && right->isAvailable())
{
	// Trigger squeeze: 0.0 (released) to 1.0 (fully pulled)
	float trigger = right->getAxisByType(InputVRController::AXIS_TYPE_TRIGGER_VALUE);

	// Thumbstick tilt: -1.0 to 1.0 on each axis
	float stick_x = right->getAxisByType(InputVRController::AXIS_TYPE_JOYSTICK_X);
	float stick_y = right->getAxisByType(InputVRController::AXIS_TYPE_JOYSTICK_Y);

	// Grip pressure: 0.0 to 1.0
	float grip = right->getAxisByType(InputVRController::AXIS_TYPE_GRIP_VALUE);
}

```


## Haptic Feedback


Controllers can vibrate to give the user physical feedback - for example, when picking up an object, colliding with something, or pressing a virtual button. Call *[InputVRController::applyHaptic](../api/library/controls/class.inputvrcontroller_cpp.md#)* with three parameters:


- **amplitude** (0.0 - 1.0) - vibration intensity. Higher values = stronger vibration.
- **duration** (milliseconds) - how long the vibration lasts.
- **frequency** (Hz) - vibration frequency. Not all hardware supports custom frequencies; pass -1 to use the device default.


```cpp
InputVRControllerPtr right = Input::getVRControllerRight();

// Short, light tap - good for UI button feedback
right->applyHaptic(0.3f, 50, -1);

// Strong, longer pulse - good for picking up / hitting something
right->applyHaptic(1.0f, 200, -1);

```


To stop an ongoing vibration immediately, call *[InputVRController::stopHaptic](../api/library/controls/class.inputvrcontroller_cpp.md#)*.


## Input Events


Besides polling device state every frame, you can subscribe to events on the *[Input](../api/library/controls/class.input_cpp.md)* class to react to input changes as they happen. The available VR events are:


- *[Input::getEventVrDeviceConnected](../api/library/controls/class.input_cpp.md#)* / *[Input::getEventVrDeviceDisconnected](../api/library/controls/class.input_cpp.md#)* - a device was connected or disconnected. Callback receives the device connection ID.
- *[Input::getEventVrDeviceButtonDown](../api/library/controls/class.input_cpp.md#)* / *[Input::getEventVrDeviceButtonUp](../api/library/controls/class.input_cpp.md#)* - a button was pressed or released. Callback receives the connection ID and the *VR_BUTTON*.
- *[Input::getEventVrDeviceButtonTouchDown](../api/library/controls/class.input_cpp.md#)* / *[Input::getEventVrDeviceButtonTouchUp](../api/library/controls/class.input_cpp.md#)* - a button touch started or ended.
- *[Input::getEventVrDeviceAxisMotion](../api/library/controls/class.input_cpp.md#)* - an axis value changed. Callback receives the connection ID and axis index.


```cpp
// Subscribe to button press events
Input::getEventVrDeviceButtonDown().connect([](int connection_id, Input::VR_BUTTON button)
{
	Log::message("VR button %d pressed on device %d\n", button, connection_id);
});

```


## Controller Reference


The tables below show how physical controller inputs map to UNIGINE enums. The mapping depends on the backend.


### OpenXR Mapping


With the **OpenXR** backend, the Engine loads controller profiles from `<SDK>/data/core/openxr/device_profiles.xml` (auto-generated from the [OpenXR specification](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html)). At startup, bindings for all known profiles are registered with the runtime. When the user connects a controller, the runtime selects the matching profile automatically.


#### Button Mapping


The table shows how OpenXR component subpaths map to *[Input::VR_BUTTON](../api/library/controls/class.input_cpp.md#VR_BUTTON)*:


| VR_BUTTON | Meaning | OpenXR component |
|---|---|---|
| *VR_BUTTON_X* | Primary face button (A on right hand, X on left hand) | */input/a/click*, */input/x/click* |
| *VR_BUTTON_Y* | Secondary face button (B on right hand, Y on left hand) | */input/b/click*, */input/y/click* |
| *VR_BUTTON_GRIP* | Grip / squeeze as a button (binary press) | */input/squeeze/click* |
| *VR_BUTTON_SYSTEM* | System button (may be intercepted by the runtime) | */input/system/click* |
| *VR_BUTTON_APPLICATION* | Application / menu button | */input/menu/click* |
| *VR_BUTTON_SELECT* | Select (on simple controllers) | */input/select/click* |
| *VR_BUTTON_SHOULDER* | Shoulder button (gamepad-style controllers) | */input/shoulder_*/click* |
| *VR_BUTTON_DPAD_UP/DOWN/LEFT/RIGHT* | D-pad directions (physical or emulated from trackpad/thumbstick) | */input/dpad_*/click*, */input/thumbstick/dpad_**, */input/trackpad/dpad_** |
| *VR_BUTTON_AXIS_0 .. AXIS_15* | Analog control pressed as a button (e.g., trigger pulled fully, trackpad clicked) | */input/trigger/click*, */input/trackpad/click*, */input/thumbstick/click* |
| *VR_BUTTON_THUMBREST* | Thumb resting surface (capacitive sensor) | */input/thumbrest/touch* |
| *VR_BUTTON_PROXIMITY_SENSOR* | Headset proximity sensor (detects if the HMD is on the user's face) | - |
| *VR_BUTTON_HOME*, *VR_BUTTON_START*, *VR_BUTTON_END*, *VR_BUTTON_BACK*, *VR_BUTTON_VIEW* | Additional system/navigation buttons (availability varies by controller) | */input/home/click*, */input/start/click*, etc. |
| *VR_BUTTON_VOLUME_UP*, *VR_BUTTON_VOLUME_DOWN*, *VR_BUTTON_MUTE_MIC*, *VR_BUTTON_PLAY_PAUSE* | Media controls (typically on HMDs like HTC Vive Pro) | */input/volume_up/click*, etc. |


#### Axis Mapping


The table shows how OpenXR component subpaths map to *[InputVRController::AXIS_TYPE](../api/library/controls/class.inputvrcontroller_cpp.md#AXIS_TYPE)*:


| AXIS_TYPE | Range | OpenXR component |
|---|---|---|
| *AXIS_TYPE_TRACKPAD_X* / *_Y* | -1 .. 1 | */input/trackpad/x*, */input/trackpad/y* |
| *AXIS_TYPE_TRACKPAD_FORCE* | 0 .. 1 | */input/trackpad/force* |
| *AXIS_TYPE_JOYSTICK_X* / *_Y* | -1 .. 1 | */input/thumbstick/x*, */input/thumbstick/y* |
| *AXIS_TYPE_JOYSTICK_FORCE* | 0 .. 1 | */input/thumbstick/force* |
| *AXIS_TYPE_TRIGGER_VALUE* / *_FORCE* | 0 .. 1 | */input/trigger/value*, */input/trigger/force* |
| *AXIS_TYPE_TRIGGER_CURL_VALUE* / *_FORCE* | 0 .. 1 | */input/trigger_curl/value*, */input/trigger_curl/force* |
| *AXIS_TYPE_TRIGGER_SLIDE_VALUE* / *_FORCE* | 0 .. 1 | */input/trigger_slide/value*, */input/trigger_slide/force* |
| *AXIS_TYPE_GRIP_VALUE* / *_FORCE* | 0 .. 1 | */input/squeeze/value*, */input/squeeze/force* |
| *AXIS_TYPE_PINCH_VALUE* | 0 .. 1 | */input/pinch/value* |
| *AXIS_TYPE_GRASP_VALUE* | 0 .. 1 | */input/grasp/value* |
| *AXIS_TYPE_AIM_ACTIVATE_VALUE* | 0 .. 1 | */input/aim_activate/value* |


#### Device Profiles


To see exactly which buttons and axes a specific controller has, open `device_profiles.xml` in your SDK installation. For example, the Oculus Touch Controller profile:


```xml
<device_profile name="/interaction_profiles/oculus/touch_controller"
                title="Oculus Touch Controller">
    <component user_path="/user/hand/left" subpath="/input/x/click" ... />
    <component user_path="/user/hand/left" subpath="/input/y/click" ... />
    <component user_path="/user/hand/right" subpath="/input/a/click" ... />
    <component user_path="/user/hand/right" subpath="/input/b/click" ... />
    <component subpath="/input/squeeze/value" ... />
    <component subpath="/input/trigger/value" ... />
    <component subpath="/input/thumbstick/x" ... />
    <component subpath="/input/thumbstick/y" ... />
    ...
</device_profile>

```


If a new controller is released and is not yet included in the SDK, you can add support for it yourself - see [*Adding New Controller Interactions*](../vr_development/troubleshooting/adding_controller_interactions.md).


### OpenVR / Varjo Mapping


With the **OpenVR** or **Varjo** backend, button and axis mapping is hardcoded in the Engine. The tables below show the exact mapping for each supported controller model.


> **Notice:** The tables below use **axis numbers** (0, 1, 2, ...) - these are the raw indices used by the OpenVR API. To read an axis value in your code, use *[InputVRController::getAxis](../api/library/controls/class.inputvrcontroller_cpp.md#)* with the axis number, or use *[InputVRController::getAxisByType](../api/library/controls/class.inputvrcontroller_cpp.md#)* with an *AXIS_TYPE* enum for a more readable approach. You can check what type a raw axis corresponds to via *[InputVRController::getAxisType](../api/library/controls/class.inputvrcontroller_cpp.md#)*.


#### HTC Vive Controller


> **Notice:** This type of controller is supported by Varjo devices as well.


![](vive_controller.jpg)

*HTC Vive Controller Axes and Buttons (image sourced from vive.com, courtesy of vive.com)*


| Button/ Axis | Description | Interaction Type | UNIGINE Button/ Axis | UNIGINE Axis Number | Axis Range |
|---|---|---|---|---|---|
| 1 | Menu Button | Press | - *VR_BUTTON_Y* |  |  |
| 2 | Trackpad | Press / Touch | - *VR_BUTTON_AXIS_0* |  |  |
| 2 | Trackpad | Horizontal / Vertical Movement |  | - 0 for the X axis - 1 for the Y axis | [-1;1] - When moving along the X axis: -1 for right-to-left movement, 1 for left-to-right movement - When moving along the Y axis: -1 for forward movement, 1 for backward movement |
| 3 | System button | Press | - *VR_BUTTON_SYSTEM* |  |  |
| 7 | Trigger | Press / Touch | - *VR_BUTTON_AXIS_1* |  |  |
| 7 | Trigger | Squeeze |  | 2 for the Trigger axis | [0;1] |
| 8 | Grip button | Press | - *VR_BUTTON_GRIP* |  |  |


#### Oculus Touch Controller


> **Notice:** This type of controller works via OpenVR and is compatible with Oculus HMDs only.


[![](oculus_touch_controller.png)](oculus_touch_controller.png)

*Oculus Touch Controller Axes and Buttons (image courtesy of developer.oculus.com)*


| Button/ Axis | Interaction Type | UNIGINE Button/ Axis | UNIGINE Axis Number | Axis Range |
|---|---|---|---|---|
| - Button.One - Button.Three | Press | - *VR_BUTTON_X* |  |  |
| - Button.Two - Button.Four | Press | - *VR_BUTTON_Y* |  |  |
| - Button.PrimaryThumbstick - Button.SecondaryThumbstick | Press / Touch | - *VR_BUTTON_AXIS_0* |  |  |
| - Axis2D.PrimaryThumbstick - Axis2D.SecondaryThumbstick | Horizontal / Vertical Movement |  | - 0 for the X axis - 1 for the Y axis | [-1;1] - When moving along the X axis: -1 for right-to-left movement, 1 for left-to-right movement - When moving along the Y axis: -1 for forward movement, 1 for backward movement |
| - Axis1D.PrimaryIndexTrigger - Axis1D.SecondaryIndexTrigger | Press / Touch | - *VR_BUTTON_AXIS_1* |  |  |
| - Axis1D.PrimaryIndexTrigger - Axis1D.SecondaryIndexTrigger | Squeeze |  | 2 for the Trigger axis | [0;1] |
| - Axis1D.PrimaryHandTrigger - Axis1D.SecondaryHandTrigger | Squeeze | - *VR_BUTTON_GRIP* |  |  |


#### Valve Knuckles Controller


> **Notice:** This type of controller is supported by Varjo devices as well.


[![](knuckles_controller_sm.png)](knuckles_controller.png)

*Valve Knuckles controller axes and buttons (Image sourced from steamcommunity.com, courtesy of steamcommunity.com)*


| Button/ Axis | Interaction Type | UNIGINE Button/ Axis | UNIGINE Axis Number | Axis Range |
|---|---|---|---|---|
| A Button | Press | - *VR_BUTTON_GRIP* |  |  |
| B Button | Press | - *VR_BUTTON_X* |  |  |
| System Button | Press | - *VR_BUTTON_SYSTEM* |  |  |
| Trigger | Press / Touch | - *VR_BUTTON_AXIS_2* |  |  |
| Trigger | Squeeze |  | 4 for the Trigger axis | [0;1] |
| Track Button (Trackpad) | Press / Touch | - *VR_BUTTON_AXIS_0* |  |  |
| Track Button (Trackpad) | Horizontal / Vertical Movement |  | - 0 for the X axis - 1 for the Y axis | [-1;1] - When moving along the X axis: -1 for right-to-left movement, 1 for left-to-right movement - When moving along the Y axis: -1 for forward movement, 1 for backward movement |
| Thumbstick | Press / Touch | - *VR_BUTTON_AXIS_1* |  |  |
| Thumbstick | Horizontal / Vertical Movement |  | - 2 for the X axis - 3 for the Y axis | [-1;1] - When moving along the X axis: -1 for right-to-left movement, 1 for left-to-right movement - When moving along the Y axis: -1 for forward movement, 1 for backward movement |
| Grip | Press / Touch | - *VR_BUTTON_GRIP* |  |  |
