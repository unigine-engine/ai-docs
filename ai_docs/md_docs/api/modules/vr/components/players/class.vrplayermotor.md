# VRPlayerMotor Class


VRPlayerMotor is a physics-based character controller for VR players. It handles player movement, collision detection, jumping, crouching, and stair climbing. The motor uses a capsule shape for collision and supports various movement modes.


The class provides configurable parameters for movement speeds, physics interactions, and collision settings. It processes player input and updates the player position while handling ground detection, ceiling collisions, and slope navigation.


> **Notice:** This class is created internally by **[VRPlayerVR](../../../../../api/modules/vr/components/players/class.vrplayervr.md)** and is not configurable through the editor. To customize movement parameters such as walk speed, jump power, or capsule dimensions, modify the values in **VRPlayerMotor.h**.


### See Also


- **[VRPlayerVR](../../../../../api/modules/vr/components/players/class.vrplayervr.md)**


## VRPlayerMotor Class

---

## void provideInput ( )

Provides input data for the motor to process during the next update.
### Arguments

## void setHeadAndLegPositions ( )

Sets the head and leg positions for collision shape adjustment.
### Arguments

## isInitialized ( )

Returns whether the motor has been initialized.
### Return value

True if initialized.
## isGround ( )

Returns whether the player is currently on the ground.
### Return value

True if on ground.
## isCeiling ( )

Returns whether the player is touching a ceiling.
### Return value

True if touching ceiling.
## isCrouch ( )

Returns whether the player is currently crouching.
### Return value

True if crouching.
## isHorizontalFrozen ( )

Returns whether horizontal movement is currently frozen.
### Return value

True if horizontal movement is frozen.
## getSlopeNormal ( )

Returns the normal vector of the current slope surface.
### Return value

Slope normal vector.
## getSlopeAxisX ( )

Returns the X axis of the current slope basis.
### Return value

Slope X axis.
## getSlopeAxisY ( )

Returns the Y axis of the current slope basis.
### Return value

Slope Y axis.
## getHorizontalVelocity ( )

Returns the current horizontal velocity in slope basis.
### Return value

Horizontal velocity vector.
## getVerticalVelocity ( )

Returns the current vertical velocity.
### Return value

Vertical velocity.
## void setWorldTransform ( )

Sets the world transformation of the player.
### Arguments

## void update ( )

Updates the motor state. Should be called every frame.
## void updatePhysics ( )

Updates physics calculations. Should be called during physics update.
