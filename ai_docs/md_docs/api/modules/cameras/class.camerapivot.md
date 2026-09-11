# CameraPivot Component

**Inherits from:** CameraBase


CameraPivot is an orbit camera that rotates around a pivot point. It provides smooth third-person camera behavior with configurable distance, FOV, and angle limits. The camera can also function as a first-person view when distance factor is set to -1.


The camera supports collision detection to prevent clipping through objects, smooth interpolation for following moving targets, and customizable rotation constraints.


Input is handled through the **InputModule** system for rotation, distance, and FOV adjustments.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Pivot Group |  |  |
| Pivot Node | *Node* | The pivot node around which the camera will rotate. Leave empty to use the parent node. |
| Pivot Offset | *Vec3* | Local offset for the pivot node. |
| Intersection Group |  |  |
| Intersection Mask | *Mask* | Intersection mask for checking camera collision. Set to 0 to disable (*default: 1*). |
| Intersection Exclude | *Node* | Node hierarchy excluded from intersection checks. |
| Intersection Margin | *Float* | Margin from collision point (*default: 0.5*). |
| Limits Group |  |  |
| FOV Distance Scale | *Curve2d* | Curve mapping FOV to render distance scale. |
| FOV Range | *Vec2* | Allowed FOV range (*default: 20-60*). |
| Distance Factor | *Float* | Camera distance multiplier. Set to -1 for first-person view (*default: 1*). |
| Distance Range | *Vec2* | Allowed distance range from pivot (*default: 2-6*). |
| Pitch Range | *Vec2* | Allowed pitch angle range. |
| Yaw Range | *Vec2* | Allowed yaw angle range. |
| Use Pivot Axes | *Vec3* | Rotation axes used for pivot transform in ZXY order (*default: 1,1,1*). |
| Rates Group |  |  |
| Rotation Change Increment | *Float* | Mouse sensitivity for rotation in deg/dpi (*default: 0.1*). |
| Distance Change Increment | *Float* | Mouse scroll sensitivity for distance (*default: 0.5*). |
| Rotation Change Rate | *Float* | Rotation speed in deg/sec (*default: 90*). |
| Distance Change Rate | *Float* | Distance change speed in units/sec (*default: 1*). |
| FOV Change Rate | *Float* | FOV change speed in deg/sec (*default: 10*). |
| Pivot Follow Rate | *Float* | Speed of following pivot transform changes (*default: 5*). |
| Distance Follow Rate | *Float* | Speed of following target distance changes (*default: 10*). |


### See Also


- **[CameraBase](../../../api/modules/cameras/class.camerabase.md)**
- **[CameraSpectator](../../../api/modules/cameras/class.cameraspectator.md)**
- **[CameraManager](../../../api/modules/cameras/class.cameramanager.md)**


## CameraPivot Class

---

## virtual getType ( )

Returns the camera type identifier.
### Return value

Always returns CAMERA_PIVOT.
