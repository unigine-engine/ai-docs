# VRBaseControllerInput Component

**Inherits from:** Component


VRBaseControllerInput is the base class for side-specific controller input presets. It defines virtual methods for querying button states and axis values that derived classes override to map actual hardware input.


### See Also


- **[VRBaseInput](../../../../api/templates/template_vr_csharp/base/class.vrbaseinput.md)**
- **[VRBaseGeneralInput](../../../../api/templates/template_vr_csharp/base/class.vrbasegeneralinput.md)**


## VRBaseControllerInput Class

---

## IsButtonDown ( )

Returns whether the specified button was pressed this frame.
### Arguments

### Return value

True if the button was pressed this frame.
## IsButtonPress ( )

Returns whether the specified button is currently held down.
### Arguments

### Return value

True if the button is currently held.
## IsButtonUp ( )

Returns whether the specified button was released this frame.
### Arguments

### Return value

True if the button was released this frame.
## GetAxis ( )

Returns the value of the specified axis.
### Arguments

### Return value

Axis value.
