# VR Input System


The VR input system allows managing user input from *VR controllers*, *head-mounted displays (HMDs)*, *base stations*, and *trackers*. It supports a wide range of VR devices, enabling you to utilize several devices from various vendors and process input from them.


The *[InputVRDevice](../api/library/controls/class.inputvrdevice_cpp.md)* class provides access to properties and settings common for all VR devices (for example, a device name).


## VR Controllers


Controllers serve as a primary interface for VR input. There are three types of VR controllers: *left-hand*, *right-hand controllers*, and a *treadmill*. You can get the controller's type and check whether it is a *hand controller* by using the corresponding methods of the *[InputVRController](../api/library/controls/class.inputvrcontroller_cpp.md)* class.


The VR input system supports a range of controller models compatible with *OpenVR, Varjo*, and *OpenXR* devices. In this article, we will consider the following:


- General approach to processing inputs on VR controllers.
- Examples of inputs on some models of OpenVR-compatible devices (*HTC Vive*, *Oculus Touch*, and *Valve Knuckles*).


UNIGINE API provides access to the VR controller inputs — ***axes*** and ***buttons***.


- ***Buttons*** are mapped to the controller's buttons that can be pressed, touched, or released.
- ***Axes*** detect 1-dimensional movement of the control and have more complex behavior. Depending on the type of the VR controller, the number of axes differs. UNIGINE supports several axes. But usually, a controller has *3* or *4*. In UNIGINE, an axis can be mapped to a control of one of the supported types, also referred to as an [*axis type*](../api/library/controls/class.inputvrcontroller_cpp.md#AXIS_TYPE). > **Notice:** You cannot know in advance which type of controller is connected, so UNIGINE API allows you to identify the [number of supported axes](../api/library/controls/class.inputvrcontroller_cpp.md#getNumAxes_int), check their [types](../api/library/controls/class.inputvrcontroller_cpp.md#getAxisType_int_int), find the axis index by its type via *[findAxisByType()](../api/library/controls/class.inputvrcontroller_cpp.md#findAxisByType_int_int)*, or get a state value for the axis via *[getAxisByType()](../api/library/controls/class.inputvrcontroller_cpp.md#getAxisByType_int_float)*.


### General Approach to VR Controller Inputs


Some VR controllers have unique button layouts. For example, *Vive Wand* has only one button, typically used as the Menu button. Others may have more buttons and may even include a trackpad in addition to a thumbstick.


To account for such differences, you can use *[InputVRController::getSupportedButtonMask()](../api/library/controls/class.inputvrcontroller_cpp.md)* and *[InputVRController::findAxisByType()](../api/library/controls/class.inputvrcontroller_cpp.md)* methods to determine which button to use for specific actions.


> **Notice:** It is the recommended approach to processing controller inputs. For OpenVR controllers, you can also refer to the tables below for [details on button mapping](#openvr_input).


For example, you can decide which button to use as the teleport button as follows:


> **Notice:** This example can be extended to other actions as well.


```cpp
bool isTeleportButtonPressed(InputVRControllerPtr device)
{
	if (!device || device->isAvailable() == false || device->isTransformValid() == false)
		return false;

	// check if there is the X button on the controller
	if (device->getSupportedButtonsMask() & (1ull << uint64_t(Input::VR_BUTTON_X)))
		// consider the X button as the teleport button and check if it is pressed
		return device->isButtonPressed(Input::VR_BUTTON_X);

	// if there is no X button on the controller, try to use the Trackpad, Trigger, or Grip button as the teleport button
	VectorStack<InputVRController::AXIS_TYPE> axis_types = { InputVRController::AXIS_TYPE_TRACKPAD_X, InputVRController::AXIS_TYPE_TRIGGER_VALUE, InputVRController::AXIS_TYPE_GRIP_VALUE };
	for (int i = 0; i < axis_types.size(); i++)
	{
		// find the axis index by the axis type
		int axis_index = device->findAxisByType(axis_types[i]);
		if (axis_index == -1)
			continue;

		Input::VR_BUTTON button = Input::VR_BUTTON(Input::VR_BUTTON_AXIS_0 + axis_index);
		if (device->getSupportedButtonsMask() & (1ull << uint64_t(button)))
			return device->isButtonPressed(button);
	}

	return false;
}

```


### Inputs for OpenVR Controllers


This chapter showcases examples of inputs on different types of **OpenVR-supported controllers** — *HTC Vive, Oculus Touch*, and *Valve Knuckles* controllers — and provides information on how these inputs are mapped to the buttons and axes within the UNIGINE input system.


> **Notice:** You can find the list of common OpenVR controller types [here](https://github.com/ValveSoftware/openvr/wiki/List-of-common-controller-types).


#### HTC Vive Controller Inputs


> **Notice:** This type of controller is supported by Varjo devices as well.


![](vive_controller.jpg)

*HTC Vive Controller Axes and Buttons (image sourced from vive.com, courtesy of vive.com)*


| Button/ Axis | Description | Interaction Type | UNIGINE Button/ Axis | UNIGINE Axis Number | Axis Range |
|---|---|---|---|---|---|
| 1 | Menu Button | Press | - *VR_BUTTON* |  |  |
| 2 | Trackpad | Press / Touch | - *VR_BUTTON_AXIS_0* |  |  |
| 2 | Trackpad | Horizontal / Vertical Movement |  | - 0 for the X axis - 1 for the Y axis | [-1;1] - When moving along the X axis: -1 for right-to-left movement, 1 for left-to-right movement - When moving along the Y axis: -1 for forward movement, 1 for backward movement |
| 3 | System button | Press | - *VR_BUTTON_SYSTEM* |  |  |
| 7 | Trigger | Press / Touch | - *VR_BUTTON_AXIS_1* |  |  |
| 7 | Trigger | Squeeze |  | 2 for the Trigger axis | [0;1] |
| 8 | Grip button | Press | - *VR_BUTTON_GRIP* |  |  |


#### Oculus Touch Controller Inputs


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


#### Valve Knuckles Controller Inputs


> **Notice:** This type of controller is supported by Varjo devices as well.


[![](knuckles_controller_sm.png)](knuckles_controller.png)

*Valve Knuckles controller axes and buttons (Image sourced from steamcommunity.com, courtesy of steamcommunity.com)*


> **Notice:** Currently, UNIGINE doesn't offer support for the *Force Sensor* and *Finger Tracking* inputs.


| Button/ Axis | Interaction Type | UNIGINE Button/ Axis | UNIGINE Axis Number | Axis Range |
|---|---|---|---|---|
| A Button | Press | - *VR_BUTTON_GRIP* |  |  |
| B Button | Press | - *VR_BUTTON_X* |  |  |
| System Button | Press | - *VR_BUTTON_SYSTEM* |  |  |
| Trigger | Press / Touch | - *VR_BUTTON_AXIS_1* |  |  |
| Trigger | Squeeze |  | 2 for the Trigger axis | [0;1] |
| Track Button (Trackpad) | Press / Touch | - *VR_BUTTON_AXIS_0* |  |  |
| Track Button (Trackpad) | Horizontal / Vertical Movement |  | - 0 for the X axis - 1 for the Y axis | [-1;1] - When moving along the X axis: -1 for right-to-left movement, 1 for left-to-right movement - When moving along the Y axis: -1 for forward movement, 1 for backward movement |
| Thumbstick | Press / Touch | - *VR_BUTTON_AXIS_0* |  |  |
| Thumbstick | Horizontal / Vertical Movement |  | - 0 for the X axis - 1 for the Y axis | [-1;1] - When moving along the X axis: -1 for right-to-left movement, 1 for left-to-right movement - When moving along the Y axis: -1 for forward movement, 1 for backward movement |
| Grip | Press / Touch | - *VR_BUTTON_GRIP* |  |  |


## Head-Mounted Displays


The VR system allows you to process input from *head-mounted displays* (*HMDs*) via the *[InputVRHead](../api/library/controls/class.inputvrhead_cpp.md)* class.


> **Notice:** The *[InputVRDevice](../api/library/controls/class.inputvrdevice_cpp.md)* class is also used for managing HMD input.


## Base Stations


A *VR base station* helps the HMD and controllers to track their exact positions, enhancing the immersion of room-scale virtual reality experience.


The *[InputVRDevice](../api/library/controls/class.inputvrdevice_cpp.md)* and *[InputVRBaseStation](../api/library/controls/class.inputvrbasestation_cpp.md)* classes is used to handle base station input.


> **Notice:** UNIGINE supports base stations that are compatible with OpenVR and Varjo devices only.


## VR Trackers


A *VR tracker* allows embedding real-world objects into the VR environment. You can attach it to a real thing that needs to be tracked. In Mixed Reality, you can install the VR tracker on a camera or player to track its position in the virtual world.


The *[InputVRDevice](../api/library/controls/class.inputvrdevice_cpp.md)* and *[InputVRTracker](../api/library/controls/class.inputvrtracker_cpp.md)* classes is used to manage tracker input.


> **Notice:** UNIGINE supports VR trackers that are compatible with OpenVR and Varjo devices only.
