# CameraManager Component

**Inherits from:** ComponentBase


CameraManager is a singleton component that manages all cameras in the scene. It tracks registered cameras, handles camera switching, and provides access to the currently active camera.


Cameras automatically register with the manager when initialized and unregister when destroyed. The manager ensures only one camera is active at a time.


Access the singleton via **CameraManager::get()**.


### See Also


- **[CameraBase](../../../api/modules/cameras/class.camerabase.md)**
- **[CameraSpectator](../../../api/modules/cameras/class.cameraspectator.md)**
- **[CameraPivot](../../../api/modules/cameras/class.camerapivot.md)**


## CameraManager Class

---

## static get ( )

Returns the singleton instance of CameraManager.
### Return value

The singleton instance.
## getNumCameras ( )

Returns the total number of cameras registered with the manager.
### Return value

Number of registered cameras.
## getCameraIndex ( )

Returns the index of the specified camera in the manager's list.
### Arguments

### Return value

Index of the camera, or -1 if not found.
## getCamera ( )

Returns the camera at the specified index.
### Arguments

### Return value

Camera at the specified index.
## getActiveCamera ( )

Returns the currently active camera.
### Return value

Currently active camera, or nullptr if none.
## getSpectator ( )

Returns the first CameraSpectator found in the registered cameras.
### Return value

Spectator camera, or nullptr if not found.
## void setActiveCamera ( )

Sets the specified camera as the active camera. Deactivates the previously active camera.
### Arguments
