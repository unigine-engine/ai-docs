# TurnMovement Component

**Inherits from:** VRBaseMovement


TurnMovement extends **[VRBaseMovement](../../../../api/templates/template_vr_csharp/base/class.vrbasemovement.md)** to provide thumbstick-based snap or smooth turning in VR mode. Supports two modes: button click (snap turn) and button press (continuous turn with delay).


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Turn Step | *Float* | Rotation angle per snap turn step (degrees). |
| Turn Mode | *TURN_MODE* | Turn input mode (snap or continuous). |
| Turn Delay | *Float* | Delay between repeated turns in press mode. |
| Smooth Rotation Speed | *Float* | Speed of smooth rotation interpolation. |


## TurnMovement Class
