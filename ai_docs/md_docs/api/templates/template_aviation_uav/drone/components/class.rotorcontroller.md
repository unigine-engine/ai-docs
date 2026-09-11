# RotorController

**Inherits from:** Drone::Component


RotorController animates drone rotor blades with motion blur effects. It manages the transition between visible rotor blades at low speed and transparent blur disk at high speed.


### Component Parameters


| Input Group |  |  |  |
|---|---|---|---|
| Name | Type | Default | Description |
| Speed | *Float* | 0.0 | Rotor speed input. |
| Rotor Group |  |  |  |
| Rotation Direction | *Switch* | CW | Rotation direction: *CW* (clockwise) or *CCW* (counter-clockwise). |
| Rotor Node | *Node* | � | The visible rotor blade mesh. |
| Disk Node | *Node* | � | The blur disk mesh for high-speed visualization. |
| Rotor Group |  |  |  |
| Rotation Axis | *Vec3* | up | Rotation axis vector. |
| Blurring Group |  |  |  |
| Threshold Rotor Speed | *Float* | 50.0 | Speed at which rotor starts fading. |
| Threshold Disk Speed | *Float* | 150.0 | Speed at which disk becomes fully visible. |
| Alpha Rotor | *Curve2d* | � | Curve controlling rotor transparency vs speed. |
| Alpha Disk | *Curve2d* | � | Curve controlling disk transparency vs speed. |


### See Also


- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**
- **[Propeller](../../../../../api/templates/template_aviation_uav/drone/components/class.propeller.md)**
- **[PropellerAnimation](../../../../../api/templates/template_aviation_uav/drone/components/class.propelleranimation.md)**
