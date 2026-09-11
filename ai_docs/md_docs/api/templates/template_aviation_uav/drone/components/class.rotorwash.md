# RotorWash Component

**Inherits from:** ComponentBase


RotorWash manages rotor wash particle effects for helicopters. The effect intensity changes based on the distance from the ground and the aircraft's velocity. Uses Kalman filtering for smooth velocity calculations.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Max Height | *Float* | 16 | Height from ground at which the effect disappears. |
| Min Height | *Float* | 4 | Height from ground at which the effect has maximum intensity. |
| Forward Offset | *Float* | 1.0 | Multiplier to move the effect forward relative to the helicopter. |
| Use Normal | *Toggle* | true | Use ground normal for effect orientation. |
| Static Only | *Node* | � | Root node for effects only displayed when helicopter is not moving. |
| Disable Static | *Toggle* | true | Disable static effects. |
| Max Velocity For Static | *Float* | 8 | Upper speed limit at which helicopter is considered static. |
| Terrain Intersection Mask | *Mask* | � | Collision mask for ground detection. |
| Velocity Filter Settings Group |  |  |  |
| Measurement Error | *Float* | 2.0 | Kalman filter measurement error. |
| Error Estimate | *Float* | 2.0 | Kalman filter error estimate. |
| Process Noise | *Float* | 0.1 | Kalman filter process noise. |


### See Also


- **[RotorWashController](../../../../../api/templates/template_aviation_uav/drone/components/class.rotorwashcontroller.md)**
- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**


## RotorWash Class

---

## void setDrone ( )

Sets the drone instance for velocity tracking.
### Arguments
