# VRBaseMovement Component

**Inherits from:** Component


VRBaseMovement is the base class for all movement components (teleportation, walking, turning, crouching). Each movement component contributes to the player's input by modifying the PlayerInput struct each frame.


Movement components are managed by the **[VRMovementManager](../../../../api/templates/template_vr_csharp/movements/class.vrmovementmanager.md)**, which iterates over all registered movements and combines their contributions.


### See Also


- **[VRMovementManager](../../../../api/templates/template_vr_csharp/movements/class.vrmovementmanager.md)**
- **[PlayerMotor](../../../../api/templates/template_vr_csharp/movements/class.playermotor.md)**
- **[VRPlayer](../../../../api/templates/template_vr_csharp/class.vrplayer.md)**


## VRBaseMovement Class

---

## void ContributeInput ( )

Called each frame to contribute movement input. Derived classes override this to add their specific movement logic.
### Arguments

## void InitMovement ( )

Called once during movement system initialization.
### Arguments
