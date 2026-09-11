# VRTransformMovableObject Component

**Inherits from:** VRBaseInteractable


VRTransformMovableObject extends **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** to implement a grabbable object that follows the hand using direct transform manipulation (no physics). On release, it applies velocity to the physics body if present. Supports per-hand grip offsets.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Linear Velocity Factor | *Float* | Multiplier for the throw linear velocity. |
| Angular Velocity Factor | *Float* | Multiplier for the throw angular velocity. |
| Use Handy Transform | *Bool* | Whether to use custom per-hand grip offsets. |
| Left Hand Position | *vec3* | Grip position offset for the left hand. |
| Left Hand Rotation | *vec3* | Grip rotation offset for the left hand. |
| Right Hand Position | *vec3* | Grip position offset for the right hand. |
| Right Hand Rotation | *vec3* | Grip rotation offset for the right hand. |
| PC Hand Position | *vec3* | Grip position offset for PC mode. |
| PC Hand Rotation | *vec3* | Grip rotation offset for PC mode. |


### See Also


- **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)**
- **[VRKinematicMovableObject](../../../../api/templates/template_vr_csharp/interactions/class.vrkinematicmovableobject.md)**
- **[VRPhysicMovableObject](../../../../api/templates/template_vr_csharp/interactions/class.vrphysicmovableobject.md)**
