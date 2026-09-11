# VRHandController Component

**Inherits from:** VRController


VRHandController is a component that handles VR controller input and hand tracking for standard VR controllers. It extends **[VRController](../../../../../api/modules/vr/components/players/class.vrcontroller.md)** to provide controller-specific functionality including button input, haptic feedback, and controller visualization.


The component manages left and right controllers, tracking their positions, rotations, and input states. It also handles teleportation through the integrated **[PlayerHandControllerTeleporter](../../../../../api/modules/vr/components/players/class.playerhandcontrollerteleporter.md)**.


### Controller Model Loading


VRHandController attempts to load controller models from the VR runtime. The loading process works as follows:

 On initialization, the component requests controller models from the VR runtime via getCombinedModelMesh() or getModelMesh() If the runtime provides models (mesh and texture), they are loaded and displayed with the material specified in *controller_material* If the runtime does not provide models within 2 seconds, the fallback models from *default_controller_left* and *default_controller_right* are used
> **Notice:** Automatic controller model loading from the VR runtime is only available for **OpenVR (SteamVR)**. When running on **OpenXR** or **Varjo**, the runtime does not provide controller models, so the fallback models specified in *default_controller_left* and *default_controller_right* parameters will always be used. Make sure to configure these parameters with appropriate controller or hand models for your application.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Controller References |  |  |
| default_controller_left | *Node* | Fallback model for the left controller. Used when the VR runtime does not provide controller models (OpenXR, Varjo) or when loading times out. Should be a NodeReference pointing to an ObjectMeshSkinned. |
| default_controller_right | *Node* | Fallback model for the right controller. Used when the VR runtime does not provide controller models (OpenXR, Varjo) or when loading times out. Should be a NodeReference pointing to an ObjectMeshSkinned. |
| Controller Position Adjustments |  |  |
| Left Controller Adjustment | *Struct* | Position and rotation adjustment for the left controller. Contains rotation (Vec3) and translation (Vec3) fields. |
| Right Controller Adjustment | *Struct* | Position and rotation adjustment for the right controller. Contains rotation (Vec3) and translation (Vec3) fields. |
| Visuals |  |  |
| Controller Material Path | *File* | Material applied to controller models loaded from the VR runtime (OpenVR only). The runtime-provided texture is assigned to the albedo slot. Not used for fallback models. Default: *modules/vr/vr_template/shaders/vr_controller.mgraph*. |


### See Also


- **[VRController](../../../../../api/modules/vr/components/players/class.vrcontroller.md)**
- **[VRHandTracking](../../../../../api/modules/vr/components/players/class.vrhandtracking.md)**
- **[VRPlayerVR](../../../../../api/modules/vr/components/players/class.vrplayervr.md)**


## VRHandController Class

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
## getGrabComponents ( )

Returns the interactable components attached to the grabbed node.
### Arguments

### Return value

Vector of interactable components on the grabbed node.
## void setControllerMeshTransform ( )

Sets a custom transformation for the controller mesh.
### Arguments

## getControllerMeshTransform ( )

Returns the transformation matrix of the controller mesh.
### Arguments

### Return value

Controller mesh transformation.
## getControllerTransform ( )

Returns the world transformation of the controller.
### Arguments

### Return value

Controller transformation.
## isControllerValid ( )

Returns whether the specified controller is valid and connected.
### Arguments

### Return value

True if the controller is valid.
## isControllerActive ( )

Returns whether the specified controller is currently active.
### Arguments

### Return value

True if the controller is active.
## void visualizeController ( )

Enables or disables controller visualization.
### Arguments

## getControllerButtonPressed ( )

Returns whether the specified button is currently pressed.
### Arguments

### Return value

True if pressed.
## getControllerButtonDown ( )

Returns whether the specified button was pressed this frame.
### Arguments

### Return value

True if button was pressed this frame.
## getControllerButtonUp ( )

Returns whether the specified button was released this frame.
### Arguments

### Return value

True if button was released this frame.
## getControllerAxis ( )

Returns the value of the specified controller axis.
### Arguments

### Return value

Axis value.
## void vibrateController ( )

Triggers haptic feedback on the specified controller.
### Arguments

## getRawController ( )

Returns the raw InputVRController for direct access to controller data.
### Arguments

### Return value

Raw VR controller.
