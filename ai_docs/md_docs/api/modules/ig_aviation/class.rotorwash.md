# RotorWash Component

**Inherits from:** ComponentBase


RotorWash controls the visual effects of rotor downwash - dust, snow, grass displacement, and other particles that appear when a helicopter hovers near the ground. The effect intensity varies based on altitude and can be positioned beneath the aircraft.


The component manages **[ParameterModifier](../../../api/modules/ig_aviation/class.parametermodifier.md)** objects to control effect intensity based on altitude (effect is strongest at min_height, fades at max_height), intensity parameter (external control from rotor RPM or collective), and movement (static-only effects can be disabled when the helicopter is moving).


A forward offset feature moves the effect forward based on velocity, keeping it visible from the cockpit view when the helicopter is moving.


The velocity calculation uses a **Kalman** filter for smooth, noise-resistant speed estimation.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Effect Group |  |  |
| Intensity | *Float* | Effect visibility intensity 0-1 (*default: 1.0*). |
| Max Height | *Float* | Height at which effect disappears (*default: 16*). |
| Min Height | *Float* | Height of maximum effect intensity (*default: 4*). |
| Forward Offset | *Float* | Speed-based forward offset multiplier (*default: 1.0*). |
| Use Normal | *Toggle* | Align effect to terrain normal. |
| Static Effects Group |  |  |
| Static Only | *Node* | Root node for static-only effects. |
| Disable Static | *Toggle* | Disable static effects when moving. |
| Max Velocity For Static | *Float* | Speed threshold for static effects (*default: 8*). |
| Velocity Filter Group |  |  |
| Measurement Error | *Float* | Kalman filter measurement error. |
| Error Estimate | *Float* | Kalman filter error estimate. |
| Process Noise | *Float* | Kalman filter process noise. |


### See Also


- **[RotorWashController](../../../api/modules/ig_aviation/class.rotorwashcontroller.md)**
- **[ParameterModifier](../../../api/modules/ig_aviation/class.parametermodifier.md)**


## RotorWash Class

---

## void setParent ( )

Sets the parent node that the rotor wash effect will follow.
### Arguments
