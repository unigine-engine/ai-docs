# ObjLaserPointer Component

**Inherits from:** ComponentBase, VRInteractable


ObjLaserPointer is a grabbable laser pointer that can be picked up, aimed, and activated by the player. When held, pressing the use button toggles the laser beam on and off. The laser ray is cast from the pointer and a hit marker is displayed at the intersection point. The component also shows the name of the pointed object via **[ObjectLabeling](../../../../api/templates/template_vr/global/class.objectlabeling.md)**.


The component implements the **[VRInteractable](../../../../api/modules/vr/components/class.vrinteractable.md)** interface for grab/throw/use interaction.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| laser | *Node* | Laser emitter node (origin of the ray). |
| laser_ray | *Node* | Node representing the visible laser beam. Scaled to match the ray length. |
| laser_hit | *Node* | Node placed at the laser hit point. |


### See Also


- **[VRInteractable](../../../../api/modules/vr/components/class.vrinteractable.md)**
- **[ObjectLabeling](../../../../api/templates/template_vr/global/class.objectlabeling.md)**


## ObjLaserPointer Class

---

## void useIt ( )

Called when the player presses the use button. Toggles the laser on or off.
### Arguments

## void grabIt ( )

Called when the player grabs the laser pointer.
### Arguments

## void throwIt ( )

Called when the player releases the laser pointer. Turns off the laser.
### Arguments
