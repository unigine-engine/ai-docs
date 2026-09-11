# PCInput Component

**Inherits from:** VRBaseInput


PCInput extends **[VRBaseInput](../../../../api/templates/template_vr_csharp/base/class.vrbaseinput.md)** to provide input handling in PC (non-VR) mode. Wraps keyboard, mouse, and simulated controller queries. Provides static methods for direct key and mouse button access.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Throw Force | *Float* | Force applied when throwing grabbed objects. |


### See Also


- **[VRBaseInput](../../../../api/templates/template_vr_csharp/base/class.vrbaseinput.md)**
- **[VRInput](../../../../api/templates/template_vr_csharp/vr_input/class.vrinput.md)**
- **[PCGeneralInput](../../../../api/templates/template_vr_csharp/vr_input/class.pcgeneralinput.md)**


## PCInput Class

---

## static IsKeyDown ( )

Returns whether the specified keyboard key was pressed this frame.
### Arguments

### Return value

True if the key was pressed this frame.
## static IsKeyPress ( )

Returns whether the specified keyboard key is currently held down.
### Arguments

### Return value

True if the key is held.
## static IsKeyUp ( )

Returns whether the specified keyboard key was released this frame.
### Arguments

### Return value

True if the key was released this frame.
## static IsMouseButtonDown ( )

Returns whether the specified mouse button was pressed this frame.
### Arguments

### Return value

True if the button was pressed this frame.
## static IsMouseButtonPress ( )

Returns whether the specified mouse button is currently held down.
### Arguments

### Return value

True if the button is held.
## static IsMouseButtonUp ( )

Returns whether the specified mouse button was released this frame.
### Arguments

### Return value

True if the button was released this frame.
## static GetAxis ( )

Returns the value of the specified mouse wheel axis.
### Arguments

### Return value

Axis value.
