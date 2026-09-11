# ObjGun Component

**Inherits from:** ComponentBase, VRInteractable


ObjGun is a grabbable gun object that can be picked up and fired by the player. When held, pressing the trigger fires a ray from the muzzle, applying an impulse to hit objects and spawning visual effects (decals for hits and muzzle flash).


The component implements the **[VRInteractable](../../../../api/modules/vr/components/class.vrinteractable.md)** interface for grab/throw interaction and supports both single-shot and automatic firing modes.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Shooting |  |  |
| muzzle | *Node* | Node at the gun muzzle position. Defines the origin and direction of shots. |
| automatic | *Toggle* | Enable automatic fire mode (continuous shooting while trigger is held). |
| cooldown | *Float* | Minimum time in seconds between shots. |
| shoot_range | *Float* | Maximum range of the shot ray intersection. |
| shoot_sound_file | *File* | Sound file played on each shot. |
| shoot_impulse | *Float* | Physics impulse applied to the hit object. |
| Visual Effects |  |  |
| hit_decal_file | *File* | Decal node file spawned at the hit point. |
| flash_decal_file | *File* | Decal node file spawned at the muzzle for flash effect. |
| Slide |  |  |
| use_slide | *Toggle* | Enable slide animation on the gun when firing. |
| slide_node | *Node* | Node with an **[ObjGunSlide](../../../../api/templates/template_vr/objects/class.objgunslide.md)** component for slide animation. Only available when *use_slide* is enabled. |


### See Also


- **[VRInteractable](../../../../api/modules/vr/components/class.vrinteractable.md)**
- **[ObjGunSlide](../../../../api/templates/template_vr/objects/class.objgunslide.md)**
- **[MaskHolder](../../../../api/modules/vr/components/class.maskholder.md)**
