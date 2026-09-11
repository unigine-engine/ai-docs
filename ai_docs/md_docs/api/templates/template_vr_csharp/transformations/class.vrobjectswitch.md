# VRObjectSwitch Component

**Inherits from:** VRBaseInteractable


VRObjectSwitch extends **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** to implement a toggle switch that animates between two position and/or rotation states when grabbed. Supports ping-pong animation and quaternion-based rotation interpolation.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Play Ping Pong | *Bool* | Whether the animation plays back and forth continuously. |
| Use Quaternions | *Bool* | Whether to use quaternion interpolation for rotation. |
| Animation Duration | *Float* | Duration of the switch animation. |
| Change Position | *Bool* | Whether the switch changes position. |
| Disabled Position | *Vec3* | Position in the disabled (off) state. |
| Enabled Position | *Vec3* | Position in the enabled (on) state. |
| Change Rotation | *Bool* | Whether the switch changes rotation. |
| Disabled Rotation | *Vec3* | Rotation (Euler angles) in the disabled state. |
| Enabled Rotation | *Vec3* | Rotation (Euler angles) in the enabled state. |
