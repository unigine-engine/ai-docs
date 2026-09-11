# PlayerMotor Class


PlayerMotor is a standalone (non-component) class that handles the physical simulation of the VR player character. It processes movement input, manages collision detection with the world, and handles jumping, crouching, and slope traversal.


### See Also


- **[VRMovementManager](../../../../api/templates/template_vr_csharp/movements/class.vrmovementmanager.md)**
- **[VRPlayer](../../../../api/templates/template_vr_csharp/class.vrplayer.md)**


## PlayerMotor Class

---

## static PlayerMotor ( )

Creates a new PlayerMotor with the specified parameters.
### Arguments

## void ProvideInput ( )

Provides movement input for the current frame.
### Arguments

## void SetHeadAndLegPosition ( )

Sets the head and leg positions for collision shape updates.
### Arguments

## void Update ( )

Updates the player motor simulation for the current frame.
## void UpdatePhysics ( )

Updates the physics simulation step for the player motor.
