# VRBaseController Component

**Inherits from:** Component


VRBaseController is the base class for all controller components (hand controllers, head controller, basestations). It provides device connection status, world-space transforms, and velocity tracking with regression smoothing.


Derived classes override ControllerInit() to perform device-specific initialization. When initialization succeeds, the static onInit event is fired.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Device | *InputSystem.VRDevice* | VR device type this controller represents. |
| Velocity Smoothing Samples | *Int* | Number of frames used for velocity smoothing via linear regression. Range: [1, 20]. Default: 4. |


### See Also


- **[HandController](../../../../api/templates/template_vr_csharp/controllers/class.handcontroller.md)**
- **[HeadController](../../../../api/templates/template_vr_csharp/controllers/class.headcontroller.md)**
- **[BasestationController](../../../../api/templates/template_vr_csharp/controllers/class.basestationcontroller.md)**


## VRBaseController Class
