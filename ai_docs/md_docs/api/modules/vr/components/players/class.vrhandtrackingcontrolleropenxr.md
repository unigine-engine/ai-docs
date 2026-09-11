# VRHandTrackingControllerOpenXR Component

**Inherits from:** VRHandTracking


VRHandTrackingControllerOpenXR implements hand tracking using the OpenXR hand tracking extension. It extends **[VRHandTracking](../../../../../api/modules/vr/components/players/class.vrhandtracking.md)** to provide skeletal hand tracking with full finger articulation.


The component supports gesture detection, pinch and grab strength detection, and hand visualization through skinned mesh mapping.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| controller_left | *Node* | Reference to the left hand node. |
| controller_right | *Node* | Reference to the right hand node. |
| visualize_hands | *Toggle* | Enable or disable hand visualization. |
| node_hands | *Node* | Reference to the hands visualization node. |


### See Also


- **[VRHandTracking](../../../../../api/modules/vr/components/players/class.vrhandtracking.md)**
- **[VRHandTrackingControllerUltraleap](../../../../../api/modules/vr/components/players/class.vrhandtrackingcontrollerultraleap.md)**


## VRHandTrackingControllerOpenXR Class

---

## isControllerValid ( )

Returns whether the specified hand is currently being tracked.
### Arguments

### Return value

True if the hand is being tracked.
## isControllerActive ( )

Returns whether the specified hand is currently active.
### Arguments

### Return value

True if the hand is active.
## getControllerButtonPressed ( )

Returns whether a gesture-based virtual button is currently pressed.
### Arguments

### Return value

True if the gesture-based button is pressed.
## getControllerAxis ( )

Returns the value of a gesture-based virtual axis.
### Arguments

### Return value

Axis value.
## getHandyPos ( )

Returns the position of the specified hand.
### Arguments

### Return value

Hand position.
## getHandyRot ( )

Returns the rotation of the specified hand.
### Arguments

### Return value

Hand rotation.
## checkGesture ( )

Returns whether the specified gesture is currently detected.
### Arguments

### Return value

True if gesture is detected.
