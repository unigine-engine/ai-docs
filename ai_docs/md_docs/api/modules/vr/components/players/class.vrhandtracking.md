# VRHandTracking Class

**Inherits from:** VRController


VRHandTracking is an abstract base class for hand tracking controllers that detect hand poses without physical controllers. It extends **[VRController](../../../../../api/modules/vr/components/players/class.vrcontroller.md)** to provide gesture-based input and hand tracking functionality.


This class serves as the base for specific hand tracking implementations such as **[VRHandTrackingControllerOpenXR](../../../../../api/modules/vr/components/players/class.vrhandtrackingcontrolleropenxr.md)** and **[VRHandTrackingControllerUltraleap](../../../../../api/modules/vr/components/players/class.vrhandtrackingcontrollerultraleap.md)**. It handles gesture detection (e.g., wrist holding) and provides teleportation through the integrated **[PlayerHandTrackingTeleporter](../../../../../api/modules/vr/components/players/class.playerhandtrackingteleporter.md)**.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| button_hand_radius | *Float* | Radius for button gesture detection on hands. |
| hold_wrist_delay_max | *Float* | Maximum delay for wrist hold gesture detection. |
| hand_force_multiplier | *Float* | Force multiplier for hand interactions. |


### See Also


- **[VRController](../../../../../api/modules/vr/components/players/class.vrcontroller.md)**
- **[VRHandController](../../../../../api/modules/vr/components/players/class.vrhandcontroller.md)**
- **[VRHandTrackingControllerOpenXR](../../../../../api/modules/vr/components/players/class.vrhandtrackingcontrolleropenxr.md)**
- **[VRHandTrackingControllerUltraleap](../../../../../api/modules/vr/components/players/class.vrhandtrackingcontrollerultraleap.md)**


## VRHandTracking Class

---

## getHandNode ( )

Returns the node representing the specified hand.
### Arguments

### Return value

Hand node.
## getHandDegreesOfFreedom ( )

Returns the degrees of freedom for the specified hand.
### Arguments

### Return value

Degrees of freedom.
## getHandLinearVelocity ( )

Returns the linear velocity of the specified hand.
### Arguments

### Return value

Linear velocity vector.
## getHandAngularVelocity ( )

Returns the angular velocity of the specified hand.
### Arguments

### Return value

Angular velocity vector.
## getHandState ( )

Returns the current state of the specified hand (FREE, GRAB, HOLD, THROW).
### Arguments

### Return value

Current hand state.
## getGrabNode ( )

Returns the node currently grabbed by the specified hand.
### Arguments

### Return value

Grabbed node or nullptr.
## getControllerTransform ( )

Returns the world transformation of the specified hand.
### Arguments

### Return value

Hand transformation.
## void setRayIntersectionMask ( )

Sets the ray intersection mask for hand tracking interactions.
### Arguments

## void setTeleportationMask ( )

Sets the mask for surfaces that allow teleportation.
### Arguments

## getGrabComponents ( )

Returns the interactable components attached to the grabbed node.
### Arguments

### Return value

Vector of interactable components.
## void setControllerMeshTransform ( )

Sets a custom transformation for the hand mesh.
### Arguments

## getControllerMeshTransform ( )

Returns the transformation matrix of the hand mesh.
### Arguments

### Return value

Hand mesh transform.
## getControllerButtonDown ( )

Returns whether a button gesture was detected this frame.
### Arguments

### Return value

True if gesture was detected this frame.
## getControllerButtonUp ( )

Returns whether a button gesture ended this frame.
### Arguments

### Return value

True if gesture ended this frame.
## void vibrateController ( )

No-op for hand tracking (no haptic feedback available).
### Arguments
