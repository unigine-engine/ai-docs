# ObjHandle Component

**Inherits from:** ComponentBase, VRInteractable


ObjHandle creates a constrained handle that moves within defined position and rotation limits. When grabbed, the handle follows the hand but is clamped to the specified bounds.


Use this for sliders, throttles, joysticks, and other controls with limited range of motion. The component supports optional anchor-relative positioning and audio feedback during movement.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Sound Group |  |  |
| Use Sounds | *Toggle* | Enable sound feedback. |
| Sound Start | *File* | Sound when grab begins. |
| Sound Loop | *File* | Sound during movement. |
| Sound Stop | *File* | Sound when released. |
| Sound Min Dist | *Float* | Minimum audible distance for sounds. Default: *0.2*. |
| Sound Max Dist | *Float* | Maximum audible distance for sounds. Default: *1000.0*. |
| Movement Group |  |  |
| Change Pos | *Toggle* | Allow position movement. |
| Change Rot | *Toggle* | Allow rotation movement. |
| Use Anchor | *Toggle* | Use anchor node for relative positioning. |
| Anchor Param | *Node* | Anchor node reference. |
| Limits Group |  |  |
| Handle Min Pos | *Vec3* | Minimum position limit. Default: *(0, 0, 0)*. |
| Handle Max Pos | *Vec3* | Maximum position limit. Default: *(0, 0, 0)*. |
| Handle Min Rot | *Vec3* | Minimum rotation limit in degrees. Default: *(-180, -180, -180)*. |
| Handle Max Rot | *Vec3* | Maximum rotation limit in degrees. Default: *(180, 180, 180)*. |


### See Also


- **[VRInteractable](../../../../../api/modules/vr/components/class.vrinteractable.md)**
