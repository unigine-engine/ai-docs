# VRPlayer Component

**Inherits from:** Component


VRPlayer is the main player component for the VR Template. It manages the player's position, rotation, camera, and references to hand/head controllers. Provides methods for teleportation, turning, crouching, and position manipulation.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Player Standing Height | *Float* | Standing height of the player capsule. |
| Player Crouch Height | *Float* | Crouched height of the player capsule. |
| Selection Outline Material | *Material* | Material used for the selection outline effect on interactable objects. |


### See Also


- **[InputSystem](../../../api/templates/template_vr_csharp/vr_input/class.inputsystem.md)**
- **[VRMovementManager](../../../api/templates/template_vr_csharp/movements/class.vrmovementmanager.md)**
- **[HandController](../../../api/templates/template_vr_csharp/controllers/class.handcontroller.md)**
- **[HeadController](../../../api/templates/template_vr_csharp/controllers/class.headcontroller.md)**


## VRPlayer Class

---

## void SetWorldPosition ( )

Sets the player's world position.
### Arguments

## void SetViewDirection ( )

Sets the player's view direction.
### Arguments

## void LandTo ( )

Teleports the player to the specified position.
### Arguments

## void SetRotation ( )

Sets the player's rotation.
### Arguments

## void Rotate ( )

Applies an additional rotation to the player.
### Arguments

## void Turn ( )

Turns the player by the specified angle around the vertical axis.
### Arguments

## void OnCrouchBegin ( )

Initiates the crouch transition.
## void OnCrouchEnd ( )

Ends the crouch transition and returns to standing.
