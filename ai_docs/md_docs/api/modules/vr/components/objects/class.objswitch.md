# ObjSwitch Component

**Inherits from:** ComponentBase, VRInteractable


ObjSwitch creates an interactive switch that toggles between on/off states when grabbed. The switch animates between two positions/rotations with optional sound feedback.


Use this for levers, buttons, toggles, and similar interactive controls. The component supports linear position animation, rotation animation, and ping-pong mode where the switch returns to its original position after activation.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Animation Group |  |  |
| Play Pingpong | *Toggle* | Return to starting position after reaching the end. |
| Use Quaternions | *Toggle* | Use quaternion interpolation for rotation instead of euler angles. |
| Animation Duration | *Float* | Time to animate between states in seconds (*default: 0.5*). |
| Position Group |  |  |
| Change Position | *Toggle* | Animate position. |
| Disable Position | *Vec3* | Position in the off state. |
| Enable Position | *Vec3* | Position in the on state. |
| Rotation Group |  |  |
| Change Rotation | *Toggle* | Animate rotation. |
| Disable Rotation Euler | *Vec3* | Rotation in the off state. Default: *(0, 0, 270)*. |
| Enable Rotation Euler | *Vec3* | Rotation in the on state. Default: *(0, 0, 360)*. |
| Sound Group |  |  |
| Switch Sound File | *File* | Sound played when toggled. |


### See Also


- **[VRInteractable](../../../../../api/modules/vr/components/class.vrinteractable.md)**
