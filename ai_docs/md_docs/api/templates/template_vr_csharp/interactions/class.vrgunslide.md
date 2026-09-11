# VRGunSlide Component

**Inherits from:** Component


VRGunSlide provides a sliding animation for a gun component along a specified axis. Used by **[VRGun](../../../../api/templates/template_vr_csharp/interactions/class.vrgun.md)** to animate the bolt/slide cycling on each shot.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Axis | *MathLib.AXIS* | Axis along which the slide moves. |
| Range | *Float* | Distance the slide travels. |
| Backward Time | *Float* | Duration of the backward slide motion. |
| Forward Time | *Float* | Duration of the forward slide return motion. |


### See Also


- **[VRGun](../../../../api/templates/template_vr_csharp/interactions/class.vrgun.md)**


## VRGunSlide Class

---

## void Slide ( )

Triggers the slide animation cycle (backward then forward).
