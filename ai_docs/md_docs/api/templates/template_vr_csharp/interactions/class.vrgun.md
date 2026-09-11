# VRGun Component

**Inherits from:** VRBaseInteractable


VRGun extends **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** to implement a grabbable firearm. Supports automatic and semi-automatic firing modes, muzzle flash, hit decals, sound effects, and optional slide animation via **[VRGunSlide](../../../../api/templates/template_vr_csharp/interactions/class.vrgunslide.md)**.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Muzzle | *Node* | Node representing the muzzle position and direction. |
| Automatic | *Bool* | Whether the gun fires automatically while the trigger is held. |
| Cooldown | *Float* | Minimum time between shots. |
| Shoot Range | *Float* | Maximum range of the shot raycast. |
| Shoot Sound File | *File* | Path to the gunshot sound file. |
| Shoot Impulse | *Float* | Physical impulse applied to hit objects. |
| Hit Decal File | *File* | Path to the hit decal material file. |
| Flash Decal File | *File* | Path to the muzzle flash decal material file. |
| Use Slide | *Bool* | Whether to trigger a slide animation on each shot. |
| Slide Node | *VRGunSlide* | Gun slide component for the cycling animation (available when Use Slide is enabled). |


### See Also


- **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)**
- **[VRGunSlide](../../../../api/templates/template_vr_csharp/interactions/class.vrgunslide.md)**
