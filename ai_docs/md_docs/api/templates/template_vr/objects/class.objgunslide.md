# ObjGunSlide Component

**Inherits from:** ComponentBase


ObjGunSlide animates a gun slide (bolt) movement when the gun is fired. The slide moves forward along the specified axis and then returns backward, simulating a recoil action.


This component is used together with **[ObjGun](../../../../api/templates/template_vr/objects/class.objgun.md)** and is triggered by calling the slide() method on each shot.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| axis | *Switch* | Slide movement axis: AXIS_X, AXIS_Y, AXIS_Z, AXIS_NX, AXIS_NY, AXIS_NZ. |
| range | *Float* | Distance the slide moves along the axis. |
| backward_time | *Float* | Duration in seconds for the backward (recoil) phase. |
| forward_time | *Float* | Duration in seconds for the forward (return) phase. |


### See Also


- **[ObjGun](../../../../api/templates/template_vr/objects/class.objgun.md)**


## ObjGunSlide Class

---

## void slide ( )

Triggers the slide animation. The slide moves forward and then returns to its initial position.
