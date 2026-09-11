# VRBaseGeneralInput Component

**Inherits from:** Component


VRBaseGeneralInput is the base class for general (non-side-specific) input presets. It defines virtual methods for querying button states, axis values, and which hand side a button or axis is associated with.


### See Also


- **[VRBaseInput](../../../../api/templates/template_vr_csharp/base/class.vrbaseinput.md)**
- **[VRBaseControllerInput](../../../../api/templates/template_vr_csharp/base/class.vrbasecontrollerinput.md)**


## VRBaseGeneralInput Class

---

## IsButtonDown ( )

Returns whether the specified general button was pressed this frame.
### Arguments

### Return value

True if the button was pressed this frame.
## IsButtonPress ( )

Returns whether the specified general button is currently held down.
### Arguments

### Return value

True if the button is currently held.
## IsButtonUp ( )

Returns whether the specified general button was released this frame.
### Arguments

### Return value

True if the button was released this frame.
## GetButtonSide ( )

Returns which hand side a general button is associated with.
### Arguments

### Return value

Hand side associated with the button.
## GetAxisSide ( )

Returns which hand side a general axis is associated with.
### Arguments

### Return value

Hand side associated with the axis.
## GetAxis ( )

Returns the value of the specified general axis.
### Arguments

### Return value

Axis value.
