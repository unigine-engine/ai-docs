# ObjectHandleTranslatable Component

**Inherits from:** ComponentBase, VRInteractable


ObjectHandleTranslatable creates a translatable handle that can be grabbed and moved within defined position limits. When grabbed, the handle moves linearly while being clamped to min/max positions.


Use this for sliders, push buttons, drawers, and other linear controls. The component supports optional anchor-relative positioning, toggle animation, and audio feedback.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Sound Group |  |  |
| use_sounds | *Toggle* | Enable sound feedback. |
| sound_start | *File* | Sound when grab begins. |
| sound_loop | *File* | Sound during movement. |
| sound_stop | *File* | Sound when released. |
| sound_min_dist | *Float* | Minimum 3D sound distance. Default: 0.2. |
| sound_max_dist | *Float* | Maximum 3D sound distance. Default: 1000.0. |
| Anchor Group |  |  |
| use_anchor | *Toggle* | Use anchor node for relative positioning. |
| anchor_param | *Node* | Anchor node reference. |
| Position Limits |  |  |
| min_handle_position | *Vec3* | Minimum position limits. |
| max_handle_position | *Vec3* | Maximum position limits. |
| Toggle Animation |  |  |
| toggled | *Toggle* | Enable toggle animation mode. |
| animation_time | *Float* | Duration of toggle animation in seconds. Default: 1.0. |
| Physics |  |  |
| acceleration_factor | *Float* | Movement acceleration factor. Default: 3.0. |


### See Also


- **[VRInteractable](../../../../../api/modules/vr/components/class.vrinteractable.md)**
- **[ObjectHandleRotatable](../../../../../api/modules/vr/components/objects/class.objecthandlerotatable.md)**
- **[ObjHandle](../../../../../api/modules/vr/components/objects/class.objhandle.md)**


## ObjectHandleTranslatable Class

---

## void grabIt ( )

Called when the player grabs this handle.
### Arguments

## void holdIt ( )

Called every frame while the player holds and moves the handle.
### Arguments

## void throwIt ( )

Called when the player releases this handle.
### Arguments
