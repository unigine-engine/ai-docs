# VRHandTrackingControllerUltraleap Component

**Inherits from:** VRHandTracking


VRHandTrackingControllerUltraleap implements hand tracking using Ultraleap (Leap Motion) devices. It extends **[VRHandTracking](../../../../../api/modules/vr/components/players/class.vrhandtracking.md)** to provide hand tracking with finger articulation via Ultraleap sensors.


The component supports gesture detection, pinch and grab strength detection, and hand visualization through skinned mesh mapping.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| controller_0 | *Node* | Reference to the left hand node. |
| controller_1 | *Node* | Reference to the right hand node. |
| visualize_hands | *Toggle* | Enable or disable hand visualization. |
| noderef_hands_skinned_mesh | *Node* | Reference to the skinned mesh for hand visualization. |


### See Also


- **[VRHandTracking](../../../../../api/modules/vr/components/players/class.vrhandtracking.md)**
- **[VRHandTrackingControllerOpenXR](../../../../../api/modules/vr/components/players/class.vrhandtrackingcontrolleropenxr.md)**


## VRHandTrackingControllerUltraleap Class

---

## isControllerValid ( )

Returns whether the specified hand is currently being tracked by the Ultraleap device.
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
