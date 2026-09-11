# CameraSpectator Component

**Inherits from:** CameraBase


CameraSpectator is a free-flight camera that allows unrestricted movement in 3D space. It provides smooth acceleration-based movement with configurable speed ranges and mouse-based rotation.


The camera supports multiple speed modes with shift-key acceleration and smooth interpolation for natural camera movement. Roll is automatically restored to horizontal over time.


Input is handled through the **InputModule** system, allowing customizable key bindings for movement and rotation.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Speed Group |  |  |
| Speed | *Float* | Base movement speed in units per second (*default: 5*). |
| Speed Rate | *Float* | Acceleration rate for reaching target speed (*default: 10*). |
| Speed Increment | *Float* | Speed change per scroll step (*default: 1*). |
| Speed Shift Increment | *Float* | Speed change per scroll step when shift is held (*default: 3*). |
| Speed Shift Multiplier | *Float* | Speed multiplier when shift key is held (*default: 2*). |
| Speed Range | *Vec2* | Minimum and maximum allowed speed (*default: 1-20*). |
| Rotation Group |  |  |
| Turn Sensitivity | *Float* | Mouse sensitivity for rotation in degrees per pixel (*default: 0.1*). |
| Turn Rate | *Float* | Keyboard rotation rate in degrees per second (*default: 90*). |
| Restore Roll Rate | *Float* | Rate at which roll returns to horizontal (*default: 5*). |


### See Also


- **[CameraBase](../../../api/modules/cameras/class.camerabase.md)**
- **[CameraPivot](../../../api/modules/cameras/class.camerapivot.md)**
- **[CameraManager](../../../api/modules/cameras/class.cameramanager.md)**


## CameraSpectator Class

---

## virtual getType ( )

Returns the camera type identifier.
### Return value

Always returns CAMERA_SPECTATOR.
## virtual void setTransform ( )

Sets the camera's world transformation and updates internal position/rotation state.
### Arguments
