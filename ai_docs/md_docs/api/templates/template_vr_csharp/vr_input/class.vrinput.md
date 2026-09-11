# VRInput Component

**Inherits from:** VRBaseInput


VRInput extends **[VRBaseInput](../../../../api/templates/template_vr_csharp/base/class.vrbaseinput.md)** to provide input handling in VR mode. Wraps VR controller button/axis queries, device transforms, and haptic feedback. Supports OpenXR, OpenVR, and Varjo runtimes with configurable velocity rotation offsets and axis press/release thresholds. Optionally supports hand tracking input presets.


### See Also


- **[VRBaseInput](../../../../api/templates/template_vr_csharp/base/class.vrbaseinput.md)**
- **[PCInput](../../../../api/templates/template_vr_csharp/vr_input/class.pcinput.md)**
- **[VRControllerInput](../../../../api/templates/template_vr_csharp/vr_input/class.vrcontrollerinput.md)**
- **[VRHandTrackingInput](../../../../api/templates/template_vr_csharp/vr_input/class.vrhandtrackinginput.md)**


## VRInput Class

---

## static IsButtonDown ( )

Returns whether the specified VR button was pressed this frame on the given hand.
### Arguments

### Return value

True if the button was pressed this frame.
## static IsButtonPress ( )

Returns whether the specified VR button is currently held on the given hand.
### Arguments

### Return value

True if the button is held.
## static IsButtonUp ( )

Returns whether the specified VR button was released this frame on the given hand.
### Arguments

### Return value

True if the button was released this frame.
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
## static void SetControllerVibration ( )

Triggers haptic feedback on the specified VR device.
### Arguments
