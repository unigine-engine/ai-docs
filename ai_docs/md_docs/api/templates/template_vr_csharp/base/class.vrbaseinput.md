# VRBaseInput Component

**Inherits from:** Component


VRBaseInput is the base class for the input abstraction layer. It manages input presets for left and right controllers as well as general (non-side-specific) input, delegating button and axis queries to the currently active **[VRBaseControllerInput](../../../../api/templates/template_vr_csharp/base/class.vrbasecontrollerinput.md)** and **[VRBaseGeneralInput](../../../../api/templates/template_vr_csharp/base/class.vrbasegeneralinput.md)** preset components.


Derived classes (e.g., VRInput, PCInput) override device-related methods to provide actual VR headset/controller transforms and connection status.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Input Name | *String* | Identifier for this input configuration. |
| Left Controller Presets | *List<VRBaseControllerInput>* | List of input preset components for the left controller. |
| Right Controller Presets | *List<VRBaseControllerInput>* | List of input preset components for the right controller. |
| General Presets | *List<VRBaseGeneralInput>* | List of general input preset components (non-side-specific buttons and axes). |


### See Also


- **[VRBaseControllerInput](../../../../api/templates/template_vr_csharp/base/class.vrbasecontrollerinput.md)**
- **[VRBaseGeneralInput](../../../../api/templates/template_vr_csharp/base/class.vrbasegeneralinput.md)**
- **[InputSystem](../../../../api/templates/template_vr_csharp/vr_input/class.inputsystem.md)**


## VRBaseInput Class

---

## IsLeftButtonDown ( )

Returns whether the specified button on the left controller was pressed this frame.
### Arguments

### Return value

True if the button was pressed this frame.
## IsLeftButtonPress ( )

Returns whether the specified button on the left controller is currently held down.
### Arguments

### Return value

True if the button is currently held.
## IsLeftButtonUp ( )

Returns whether the specified button on the left controller was released this frame.
### Arguments

### Return value

True if the button was released this frame.
## GetLeftAxis ( )

Returns the value of the specified axis on the left controller.
### Arguments

### Return value

Axis value.
## IsRightButtonDown ( )

Returns whether the specified button on the right controller was pressed this frame.
### Arguments

### Return value

True if the button was pressed this frame.
## IsRightButtonPress ( )

Returns whether the specified button on the right controller is currently held down.
### Arguments

### Return value

True if the button is currently held.
## IsRightButtonUp ( )

Returns whether the specified button on the right controller was released this frame.
### Arguments

### Return value

True if the button was released this frame.
## GetRightAxis ( )

Returns the value of the specified axis on the right controller.
### Arguments

### Return value

Axis value.
## IsGeneralButtonDown ( )

Returns whether the specified general button was pressed this frame.
### Arguments

### Return value

True if the button was pressed this frame.
## IsGeneralButtonPress ( )

Returns whether the specified general button is currently held down.
### Arguments

### Return value

True if the button is currently held.
## IsGeneralButtonUp ( )

Returns whether the specified general button was released this frame.
### Arguments

### Return value

True if the button was released this frame.
## GetGeneralButtonSide ( )

Returns which hand side a general button is associated with.
### Arguments

### Return value

Hand side associated with the button.
## GetGeneralAxisSide ( )

Returns which hand side a general axis is associated with.
### Arguments

### Return value

Hand side associated with the axis.
## GetGeneralAxis ( )

Returns the value of the specified general axis.
### Arguments

### Return value

Axis value.
## GetTransformInterface ( )

Returns the local transformation of the specified VR device.
### Arguments

### Return value

Local transformation matrix of the device.
## IsDeviceConnectedInterface ( )

Returns whether the specified VR device is connected.
### Arguments

### Return value

True if the device is connected.
## IsTransformValidInterface ( )

Returns whether the specified VR device has a valid tracking transform.
### Arguments

### Return value

True if the transform is valid.
## GetLinearVelocityInterface ( )

Returns the linear velocity of the specified VR device.
### Arguments

### Return value

Linear velocity vector.
## GetAngularVelocityInterface ( )

Returns the angular velocity of the specified VR device.
### Arguments

### Return value

Angular velocity vector.
## void SetControllerVibrationInterface ( )

Triggers haptic feedback on the specified VR device.
### Arguments
