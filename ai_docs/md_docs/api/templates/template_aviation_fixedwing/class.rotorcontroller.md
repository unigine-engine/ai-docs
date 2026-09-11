# RotorController Component

**Inherits from:** ComponentBase


RotorController manages propeller or rotor animation with motion blur effects. It smoothly transitions between a detailed rotor mesh at low speeds and a blurred disk mesh at high speeds, creating realistic visual representation of spinning rotors.


The component uses **[TransparentHelper](../../../api/modules/ig_aviation/class.transparenthelper.md)** to control the albedo transparency of both the rotor and disk meshes. As rotation speed increases past the rotor threshold, the rotor fades out while the disk fades in, with customizable alpha curves for fine control over the transition.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Input |  |  |  |
| Speed | *Float* | *0.0* | Rotation speed in RPM. |
| Rotor |  |  |  |
| Rotation Direction | *Switch* | *CW* | Rotation direction: *CW* (clockwise) or *CCW* (counter-clockwise). |
| Rotor Node | *Node* | � | Detailed rotor mesh visible at low speeds. |
| Disk Node | *Node* | � | Blurred disk mesh visible at high speeds. |
| Rotation Axis | *Vec3* | *(0, 0, 1)* | Axis of rotation. |
| Blurring |  |  |  |
| Threshold Rotor Speed | *Float* | *50.0* | Speed at which rotor begins fading out. |
| Threshold Disk Speed | *Float* | *150.0* | Speed at which disk is fully visible. |
| Alpha Rotor | *Curve2d* | � | Curve controlling rotor transparency during transition. |
| Alpha Disk | *Curve2d* | � | Curve controlling disk transparency during transition. |


### See Also


- **[TransparentHelper](../../../api/modules/ig_aviation/class.transparenthelper.md)**
- **[FlightLogic](../../../api/templates/template_aviation_fixedwing/class.flightlogic.md)**
