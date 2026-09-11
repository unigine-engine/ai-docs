# InputSystem Component

**Inherits from:** Component


InputSystem is the central input management component for the VR Template. It provides a unified static API for querying button states, axis values, device transforms, and controller vibration across all input modes (PC and VR). Manages input presets and delegates queries to the currently active **[VRBaseInput](../../../../api/templates/template_vr_csharp/base/class.vrbaseinput.md)** configuration.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Inputs | *List<VRBaseInput>* | List of input configurations (e.g., VRInput, PCInput). |


### See Also


- **[VRBaseInput](../../../../api/templates/template_vr_csharp/base/class.vrbaseinput.md)**
- **[VRInput](../../../../api/templates/template_vr_csharp/vr_input/class.vrinput.md)**
- **[PCInput](../../../../api/templates/template_vr_csharp/vr_input/class.pcinput.md)**


## InputSystem Class

---

## static IsLeftButtonDown ( )

Returns whether the specified left controller button was pressed this frame.
### Arguments

### Return value

True if the button was pressed this frame.
## static IsLeftButtonPress ( )

Returns whether the specified left controller button is currently held down.
### Arguments

### Return value

True if the button is held.
## static IsLeftButtonUp ( )

Returns whether the specified left controller button was released this frame.
### Arguments

### Return value

True if the button was released this frame.
## static GetLeftAxis ( )

Returns the value of the specified left controller axis.
### Arguments

### Return value

Axis value.
## static IsRightButtonDown ( )

Returns whether the specified right controller button was pressed this frame.
### Arguments

### Return value

True if the button was pressed this frame.
## static IsRightButtonPress ( )

Returns whether the specified right controller button is currently held down.
### Arguments

### Return value

True if the button is held.
## static IsRightButtonUp ( )

Returns whether the specified right controller button was released this frame.
### Arguments

### Return value

True if the button was released this frame.
## static GetRightAxis ( )

Returns the value of the specified right controller axis.
### Arguments

### Return value

Axis value.
## static IsGeneralButtonDown ( )

Returns whether the specified general button was pressed this frame.
### Arguments

### Return value

True if the button was pressed this frame.
## static IsGeneralButtonPress ( )

Returns whether the specified general button is currently held down.
### Arguments

### Return value

True if the button is held.
## static IsGeneralButtonUp ( )

Returns whether the specified general button was released this frame.
### Arguments

### Return value

True if the button was released this frame.
## static GetGeneralAxis ( )

Returns the value of the specified general axis.
### Arguments

### Return value

Axis value.
## static GetTransform ( )

Returns the local transform of the specified VR device.
### Arguments

### Return value

Local transformation matrix.
## static IsDeviceConnected ( )

Returns whether the specified VR device is connected.
### Arguments

### Return value

True if connected.
## static IsTransformValid ( )

Returns whether the specified VR device has a valid tracking transform.
### Arguments

### Return value

True if the transform is valid.
## static GetLinearVelocity ( )

Returns the linear velocity of the specified VR device.
### Arguments

### Return value

Linear velocity vector.
## static GetAngularVelocity ( )

Returns the angular velocity of the specified VR device.
### Arguments

### Return value

Angular velocity vector.
## static void SetControllerVibration ( )

Triggers haptic feedback on the specified VR device.
### Arguments

## static void SetPrefferedRotationType ( )

Sets the preferred rotation type for VR turning.
### Arguments

## static GetPrefferedRotationType ( )

Returns the current preferred rotation type for VR turning.
### Return value

Current rotation type.
