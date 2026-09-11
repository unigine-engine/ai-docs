# VRKinematicMovableObject Component

**Inherits from:** VRBaseInteractable


VRKinematicMovableObject extends **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** to implement a grabbable object that follows the hand using kinematic body movement. On release, it applies velocity to the physics body based on the hand's movement. Supports per-hand position and rotation offsets for precise grip alignment.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Linear Velocity Factor | *Float* | Multiplier for the throw linear velocity. |
| Angular Velocity Factor | *Float* | Multiplier for the throw angular velocity. |
| Use Handy Transform | *Bool* | Whether to use custom per-hand grip offsets. |
| Left Hand Position | *vec3* | Grip position offset for the left hand (available when Use Handy Transform is enabled). |
| Left Hand Rotation | *vec3* | Grip rotation offset for the left hand. |
| Right Hand Position | *vec3* | Grip position offset for the right hand. |
| Right Hand Rotation | *vec3* | Grip rotation offset for the right hand. |
| PC Hand Position | *vec3* | Grip position offset for PC mode. |
| PC Hand Rotation | *vec3* | Grip rotation offset for PC mode. |


### See Also


- **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)**
- **[VRPhysicMovableObject](../../../../api/templates/template_vr_csharp/interactions/class.vrphysicmovableobject.md)**
- **[VRTransformMovableObject](../../../../api/templates/template_vr_csharp/interactions/class.vrtransformmovableobject.md)**
