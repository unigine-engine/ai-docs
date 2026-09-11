# VRPlayer Component

**Inherits from:** ComponentBase


VRPlayer is the base class for **VR** interaction systems, providing a unified interface for both **VR** headset and PC/desktop modes. It manages player positioning, hand tracking, object grabbing, and controller input across different hardware configurations.


The class uses a singleton pattern accessed via **get()**. Subclasses (**[VRPlayerVR](../../../../../api/modules/vr/components/players/class.vrplayervr.md)** and **[VRPlayerPC](../../../../../api/modules/vr/components/players/class.vrplayerpc.md)**) implement hardware-specific functionality while maintaining a consistent **API**. VRPlayer handles events for object interactions: grab, hold, use, and throw.


### See Also


- **[VRPlayerVR](../../../../../api/modules/vr/components/players/class.vrplayervr.md)**
- **[VRPlayerPC](../../../../../api/modules/vr/components/players/class.vrplayerpc.md)**
- **[VRController](../../../../../api/modules/vr/components/players/class.vrcontroller.md)**


## VRPlayer Class

---

## static get ( )

Returns the singleton instance of VRPlayer.
### Return value

Last created VRPlayer instance.
## static isVRLoaded ( )

Returns whether a VR system is loaded and available.
### Return value

Non-zero if VR is loaded.
## isVR ( )

Returns whether this player is using VR hardware.
### Return value

True if running in VR mode.
## getPlayer ( )

Returns the Unigine Player associated with this VRPlayer.
### Return value

Current player.
## void setPlayerPosition ( )

Sets the player's world position.
### Arguments

## void landPlayerTo ( )

Moves the player to a position and lands them on the ground, facing the specified direction.
### Arguments

## void teleportPlayerTo ( )

Teleports the player to a position facing the specified direction.
### Arguments

## getHead ( )

Returns the node representing the player's head.
### Return value

Head node.
## getNumHands ( )

Returns the number of tracked hands (0, 1, or 2).
### Return value

Number of tracked hands.
## getHandNode ( )

Returns the node representing a hand.
### Arguments

### Return value

Hand node.
## getHandState ( )

Returns the current state of a hand (FREE, GRAB, HOLD, THROW).
### Arguments

### Return value

Current hand state.
## getGrabNode ( )

Returns the node currently grabbed by the specified hand.
### Arguments

### Return value

Grabbed node or nullptr.
## isNodeGrabbed ( )

Returns whether the specified node is currently grabbed by either hand.
### Arguments

### Return value

True if grabbed.
## getHandLinearVelocity ( )

Returns the linear velocity of a hand.
### Arguments

### Return value

Linear velocity vector.
## getHandAngularVelocity ( )

Returns the angular velocity of a hand.
### Arguments

### Return value

Angular velocity vector.
## getControllerButtonPressed ( )

Returns whether a controller button is currently pressed.
### Arguments

### Return value

Non-zero if pressed.
## void vibrateController ( )

Triggers haptic feedback on a controller.
### Arguments

## getEventOnNodeGrab ( )

Returns the event triggered when a node is grabbed.
### Return value

Grab event.
## getEventOnNodeThrow ( )

Returns the event triggered when a node is thrown.
### Return value

Throw event.
## getEventOnNodeUse ( )

Returns the event triggered when a node is used.
### Return value

Use event.
## getEventOnNodeHold ( )

Returns the event triggered when a node is held.
### Return value

Hold event.
## void setRayIntersectionMask ( )

Sets the intersection mask for teleportation raycasting.
### Arguments

## void setTeleportationMask ( )

Sets the surface mask defining where the player can teleport.
### Arguments

## void setLock ( )

Locks or unlocks player movement.
### Arguments

## void setGrabMode ( )

Sets the grab detection mode (bounding box or ray intersection).
### Arguments

## getHandDegreesOfFreedom ( )

Returns the tracking degrees of freedom for a hand.
### Arguments

### Return value

Degrees of freedom (0-5 for PC, 6 for VR).
## getGrabComponents ( )

Returns the interactable components attached to the grabbed node.
### Arguments

### Return value

Vector of interactable components.
## getHandyPos ( )

Returns the default grip position offset for held objects.
### Arguments

### Return value

Local grip position offset.
## getHandyRot ( )

Returns the default grip rotation offset for held objects.
### Arguments

### Return value

Local grip rotation offset.
## void visualizeController ( )

Enables or disables controller model visualization.
### Arguments

## getControllerButtonDown ( )

Returns whether a controller button was pressed this frame.
### Arguments

### Return value

Non-zero if button was pressed this frame.
## getControllerButtonUp ( )

Returns whether a controller button was released this frame.
### Arguments

### Return value

Non-zero if button was released this frame.
## getControllerAxis ( )

Returns the value of a controller axis (trigger, thumbstick, etc.).
### Arguments

### Return value

Axis value.
## isEyetrackingValid ( )

Returns whether eye tracking data is valid this frame.
### Return value

True if eye tracking data is currently valid.
## isEyetrackingAvailable ( )

Returns whether eye tracking hardware is available on the headset.
### Return value

True if eye tracking hardware is available.
## getFocusWorldPosition ( )

Returns the world position where the user is looking (requires eye tracking).
### Return value

World position of gaze focus point.
