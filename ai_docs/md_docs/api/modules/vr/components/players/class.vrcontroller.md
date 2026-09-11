# VRController Component

**Inherits from:** ComponentBase


VRController is the abstract base class for all VR hand controller implementations. It defines the unified interface for hand tracking, button input, haptic feedback, and object grabbing that all controller types must implement.


> **Notice:** This is an abstract base class. You do not add this component directly � instead, add its implementations to the controllers node specified in **[VRPlayerSpawner](../../../../../api/modules/vr/components/class.vrplayerspawner.md)** (**VR Controllers Node** parameter). In PC mode, **[VRPlayerPC](../../../../../api/modules/vr/components/players/class.vrplayerpc.md)** implements controller functionality directly without using this class.


### Architecture


The controller system uses the following class hierarchy:


- **VRController** � abstract base class defining the interface
- **[VRHandController](../../../../../api/modules/vr/components/players/class.vrhandcontroller.md)** � implementation for physical VR controllers (OpenVR, OpenXR, Varjo)
- **[VRHandTracking](../../../../../api/modules/vr/components/players/class.vrhandtracking.md)** � base for hand tracking implementations

  - **VRHandTrackingControllerOpenXR** � OpenXR hand tracking
  - **VRHandTrackingControllerUltraleap** � Ultraleap hand tracking


### Runtime Controller Selection


Multiple controller components can be added to the same controllers node (for example, **[VRHandController](../../../../../api/modules/vr/components/players/class.vrhandcontroller.md)**, **VRHandTrackingControllerOpenXR**, and **VRHandTrackingControllerUltraleap** together). At runtime, **[VRPlayerVR](../../../../../api/modules/vr/components/players/class.vrplayervr.md)** automatically selects which controller to use based on hardware availability:


- If hand tracking detects hands → uses **[VRHandTracking](../../../../../api/modules/vr/components/players/class.vrhandtracking.md)** implementation
- Otherwise if physical controllers are connected → uses **[VRHandController](../../../../../api/modules/vr/components/players/class.vrhandcontroller.md)**


This allows seamless switching between physical controllers and hand tracking during gameplay. Only the active controller processes input; others are disabled via

```text
setControllersEnabled(false)
```

.
### Creating Custom Controllers


To implement a custom controller (for example, for a new tracking system), inherit from VRController and implement all pure virtual methods:


- ```text getHandNode() ``` � return the node representing the hand
- ```text getHandDegreesOfFreedom() ``` � return tracking DOF (typically 6 for full tracking)
- ```text getHandLinearVelocity() ``` / ```text getHandAngularVelocity() ``` � return hand velocities for throwing physics
- ```text getHandState() ``` � return current grab state
- ```text getControllerTransform() ``` / ```text getControllerMeshTransform() ``` � return controller transforms
- ```text isControllerValid() ``` / ```text isControllerActive() ``` � return tracking status
- ```text getControllerButtonPressed() ``` / ```text getControllerButtonDown() ``` / ```text getControllerButtonUp() ``` � return button states
- ```text getControllerAxis() ``` � return analog axis values
- ```text vibrateController() ``` � trigger haptic feedback


See **[VRHandController](../../../../../api/modules/vr/components/players/class.vrhandcontroller.md)** for a reference implementation.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Controller Buffer Count | *Int* | Samples for linear regression velocity smoothing (*default: 4*). |
| Teleport Allowed Marker | *Node* | Valid teleport destination marker. |
| Teleport Forbidden Marker | *Node* | Invalid teleport destination marker. |
| Teleport Allowed Material | *Material* | Material for valid teleport ray. |
| Teleport Forbidden Material | *Material* | Material for invalid teleport ray. |


### See Also


- **[VRHandController](../../../../../api/modules/vr/components/players/class.vrhandcontroller.md)**
- **[VRHandTracking](../../../../../api/modules/vr/components/players/class.vrhandtracking.md)**


## VRController Class

---

## getHandNode ( )

Returns the node representing a controller hand.
### Arguments

### Return value

Hand node.
## getHandState ( )

Returns the current grab state of a hand.
### Arguments

### Return value

Current state.
## getControllerTransform ( )

Returns the world transform of a controller.
### Arguments

### Return value

World transform.
## isControllerValid ( )

Returns whether a controller is connected and tracked.
### Arguments

### Return value

True if valid.
## getControllerButtonPressed ( )

Returns whether a button is currently pressed.
### Arguments

### Return value

True if pressed.
## void vibrateController ( )

Triggers haptic feedback.
### Arguments

## void setControllersEnabled ( )

Enables or disables controller input processing.
### Arguments

## isControllersEnabled ( )

Returns whether controller input processing is enabled.
### Return value

True if controllers are enabled.
## void setGrabMode ( )

Sets the grab detection mode (bounding box or ray intersection).
### Arguments

## getNumHands ( )

Returns the number of tracked hands.
### Return value

Number of tracked hands (0-2).
## getHandDegreesOfFreedom ( )

Returns the tracking degrees of freedom for a hand.
### Arguments

### Return value

Degrees of freedom (0-5 for PC, 6 for VR).
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
## getGrabNode ( )

Returns the node currently grabbed by the specified hand.
### Arguments

### Return value

Grabbed node or nullptr.
## getGrabComponents ( )

Returns the interactable components attached to the grabbed node.
### Arguments

### Return value

Vector of interactable components.
## getControllerMeshTransform ( )

Returns the transformation matrix of the controller mesh.
### Arguments

### Return value

Controller mesh transform.
## void setControllerMeshTransform ( )

Sets a custom transformation for the controller mesh.
### Arguments

## void setControllerFakeTransform ( )

Sets a fake transform for the controller model (resets after one frame).
### Arguments

## getControllerFakeTransform ( )

Returns the current fake transform for the controller.
### Arguments

### Return value

Current fake transform.
## isControllerActive ( )

Returns whether the controller is currently active.
### Arguments

### Return value

True if active.
## getControllerButtonDown ( )

Returns whether a button was pressed this frame.
### Arguments

### Return value

True if pressed this frame.
## getControllerButtonUp ( )

Returns whether a button was released this frame.
### Arguments

### Return value

True if released this frame.
## getControllerAxis ( )

Returns the value of a controller axis.
### Arguments

### Return value

Axis value.
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
