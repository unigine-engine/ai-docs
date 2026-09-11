# VRPlayerVR Component

**Inherits from:** VRPlayer


VRPlayerVR implements **[VRPlayer](../../../../../api/modules/vr/components/players/class.vrplayer.md)** for **VR** headset hardware. It handles **HMD** tracking, **VR** controller input, room-scale movement with collision detection, and teleportation.


The component integrates with **OpenVR**, **OpenXR**, and **Varjo** systems, automatically detecting available hardware. It supports multiple controller types including hand tracking when available.


> **Notice:** This component is created automatically at runtime by **[VRPlayerSpawner](../../../../../api/modules/vr/components/class.vrplayerspawner.md)** when a VR headset is detected. You should not add this component manually in the editor. All component parameters are configured through VRPlayerSpawner properties.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Obstacles | *Node* | Container with collision triggers for room boundary detection. |
| Controllers Node | *Node* | Parent node containing VR controller components. |
| Rotation Type | *Switch* | Player rotation mode: Discrete Step or Smooth. Default: *Smooth*. |
| Angle Per Step | *Float* | Rotation angle per discrete step in degrees. Visible when Rotation Type is set to Discrete Step. Default: *75.0*. |
| Smooth Rotation Speed | *Float* | Rotation speed in degrees per second for smooth rotation mode. Visible when Rotation Type is set to Smooth. Default: *60.0*. |


### See Also


- **[VRPlayer](../../../../../api/modules/vr/components/players/class.vrplayer.md)**
- **[VRHandController](../../../../../api/modules/vr/components/players/class.vrhandcontroller.md)**


## VRPlayerVR Class

---

## getHMD ( )

Returns the VR head-mounted display device.
### Return value

VR head device.
## isEyetrackingAvailable ( )

Returns whether eye tracking is available on the current headset.
### Return value

True if eye tracking hardware is present.
## isEyetrackingValid ( )

Returns whether eye tracking data is currently valid.
### Return value

True if current eye tracking data is valid.
## getFocusWorldPosition ( )

Returns the world position where the user is looking (requires eye tracking).
### Return value

World position of gaze focus.
## void setJoystickMoveEnabled ( )

Enables or disables joystick-based locomotion.
### Arguments

## void setTeleportEnabled ( )

Enables or disables teleport locomotion.
### Arguments

## isTeleportEnabled ( )

Returns whether teleport locomotion is enabled.
### Return value

True if teleport is enabled.
## isJoystickMoveEnabled ( )

Returns whether joystick-based locomotion is enabled.
### Return value

True if joystick move is enabled.
## isControllerValid ( )

Returns whether the specified controller is connected and valid.
### Arguments

### Return value

Non-zero if controller is valid.
## getControllerTransform ( )

Returns the world transformation matrix of the specified controller.
### Arguments

### Return value

Controller world transform.
## void setControllerEnabled ( )

Enables or disables controller input processing.
### Arguments

## getHeadOffset ( )

Returns the head position offset from the player origin.
### Return value

Head position offset.
## void setDynamicHandTracking ( )

Switches to dynamic hand tracking mode, where the system automatically selects between controllers and hand tracking based on hardware availability.
## void setStaticModeController ( )

Switches to static mode with physical controllers as the active input.
## void setStaticModeHandTracking ( )

Switches to static mode with hand tracking as the active input.
