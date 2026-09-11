# CameraBase Component

**Inherits from:** ComponentBase


CameraBase is the abstract base class for all camera components in the camera system. It provides a common interface for camera activation, transformation, and player management.


Derived classes (**[CameraSpectator](../../../api/modules/cameras/class.cameraspectator.md)** and **[CameraPivot](../../../api/modules/cameras/class.camerapivot.md)**) implement specific camera behaviors. All cameras register themselves with **[CameraManager](../../../api/modules/cameras/class.cameramanager.md)** automatically.


The camera system supports two types: CAMERA_SPECTATOR for free-flight cameras and CAMERA_PIVOT for orbit cameras around a target.


### See Also


- **[CameraSpectator](../../../api/modules/cameras/class.cameraspectator.md)**
- **[CameraPivot](../../../api/modules/cameras/class.camerapivot.md)**
- **[CameraManager](../../../api/modules/cameras/class.cameramanager.md)**


## CameraBase Class

---

## virtual getType ( )

Returns the type of this camera. Pure virtual method implemented by derived classes.
### Return value

Camera type (CAMERA_SPECTATOR or CAMERA_PIVOT).
## virtual isActive ( )

Returns whether this camera is currently the active camera.
### Return value

True if the camera is currently active.
## virtual void setActive ( )

Activates or deactivates this camera. When activated, this camera becomes the current view camera.
### Arguments

## getPlayer ( )

Returns the Unigine Player object used by this camera for rendering.
### Return value

The Unigine Player associated with this camera.
## virtual void setTransform ( )

Sets the camera's world transformation.
### Arguments

## getTransform ( )

Returns the camera's current world transformation.
### Return value

Current world transformation matrix.
## void setFov ( )

Sets the camera's field of view.
### Arguments

## getFov ( )

Returns the camera's current field of view.
### Return value

Field of view in degrees.
