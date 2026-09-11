# MaskHolder Component

**Inherits from:** ComponentBase


MaskHolder is a component that stores various intersection and collision masks used by the VR system. It provides centralized configuration for ray intersection, teleportation, physics collision, and other mask-based filtering operations.


This component allows fine-tuning of which objects are considered for different types of interactions in the VR environment.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Intersection Masks |  |  |
| Ray Intersection Mask | *Mask* | Mask for ray intersection tests. |
| Teleport Allowed Mask | *Mask* | Mask defining surfaces where teleportation is allowed. |
| Gun Intersection Mask | *Mask* | Mask for gun/weapon ray intersection tests. |
| Player Physics Masks |  |  |
| Player Physics Intersection Mask | *Mask* | Mask for player physics intersection tests. |
| Player Physics Collision Mask | *Mask* | Mask for player physics collision detection. |
| Player Exclusion Mask | *Mask* | Mask for excluding objects from player physics. |
| Player Check Move Mask | *Mask* | Mask for player movement checking. |
| Player Stair Detection Mask | *Mask* | Mask for stair detection during player movement. |


### See Also


- **[VRPlayerVR](../../../../api/modules/vr/components/players/class.vrplayervr.md)**
- **[VRPlayerMotor](../../../../api/modules/vr/components/players/class.vrplayermotor.md)**


## MaskHolder Class

---

## getRayIntersectionMask ( )

Returns the mask used for ray intersection tests.
### Return value

Ray intersection mask value.
## getTeleportationMask ( )

Returns the mask defining surfaces where teleportation is allowed.
### Return value

Teleportation mask value.
## getPlayerPhysicsIntersectionMask ( )

Returns the mask used for player physics intersection tests.
### Return value

Player physics intersection mask value.
## getPlayerPhysicsCollisionMask ( )

Returns the mask used for player physics collision detection.
### Return value

Player physics collision mask value.
## getPlayerExclusionMask ( )

Returns the mask for excluding objects from player physics.
### Return value

Player exclusion mask value.
## getPlayerCheckMoveMask ( )

Returns the mask used for player movement checking.
### Return value

Player check move mask value.
## getPlayerStairDetectionMask ( )

Returns the mask used for stair detection during player movement.
### Return value

Stair detection mask value.
## getGunIntersectionMask ( )

Returns the mask used for gun/weapon ray intersection tests.
### Return value

Gun intersection mask value.
