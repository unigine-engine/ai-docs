# ObjectHandleRotatable Component

**Inherits from:** ComponentBase, VRInteractable, EventSignal


ObjectHandleRotatable creates a rotatable handle that can be grabbed and rotated within defined angle limits. When grabbed, the handle rotates around a specified axis while being clamped to min/max angles.


Use this for dials, knobs, valves, levers, and other rotary controls. The component supports optional anchor-relative rotation, toggle animation, and audio feedback.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Sound Group |  |  |
| use_sounds | *Toggle* | Enable sound feedback. |
| sound_start | *File* | Sound when grab begins. |
| sound_loop | *File* | Sound during rotation. |
| sound_stop | *File* | Sound when released. |
| sound_min_dist | *Float* | Minimum 3D sound distance. Default: 0.2. |
| sound_max_dist | *Float* | Maximum 3D sound distance. Default: 1000.0. |
| Anchor Group |  |  |
| use_anchor | *Toggle* | Use anchor node for relative rotation. |
| anchor_param | *Node* | Anchor node reference. |
| Toggle Animation |  |  |
| toggled | *Toggle* | Enable toggle animation mode. |
| animation_time | *Float* | Duration of toggle animation in seconds. Default: 1.0. |
| Rotation Settings |  |  |
| rotation_axis | *Switch* | Rotation axis: AXIS_X, AXIS_Y, AXIS_Z, AXIS_NX, AXIS_NY, AXIS_NZ. |
| min_angle | *Float* | Minimum rotation angle in degrees. |
| max_angle | *Float* | Maximum rotation angle in degrees. |
| acceleration_factor | *Float* | Rotation acceleration factor. Default: 3.0. |


### See Also


- **[VRInteractable](../../../../../api/modules/vr/components/class.vrinteractable.md)**
- **[ObjectHandleTranslatable](../../../../../api/modules/vr/components/objects/class.objecthandletranslatable.md)**
- **[ObjHandle](../../../../../api/modules/vr/components/objects/class.objhandle.md)**


## ObjectHandleRotatable Class

---

## void grabIt ( )

Called when the player grabs this handle.
### Arguments

## void holdIt ( )

Called every frame while the player holds and rotates the handle.
### Arguments

## void throwIt ( )

Called when the player releases this handle.
### Arguments

## void reset ( )

Resets the handle to its initial rotation.
