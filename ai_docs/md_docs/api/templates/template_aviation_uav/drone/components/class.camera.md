# drone::Camera Component

**Inherits from:** Drone::Component


drone::Camera manages multiple cameras attached to a drone. It handles camera switching, freezing, and activation based on drone state.


### See Also


- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**
- **[CameraBase](../../../../../api/modules/cameras/class.camerabase.md)**
- **[CameraManager](../../../../../api/modules/cameras/class.cameramanager.md)**


## drone::Camera Class

---

## getCameras ( )

Returns the vector of all cameras attached to this drone.
## getSelectedCamera ( )

Returns the currently selected camera, or nullptr if none.
## getSelectedCameraIdx ( )

Returns the index of the currently selected camera.
## getNumCameras ( )

Returns the total number of cameras.
