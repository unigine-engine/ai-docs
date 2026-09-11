# VRHandController Component

**Inherits from:** HandController


VRHandController extends **[HandController](../../../../api/templates/template_vr_csharp/controllers/class.handcontroller.md)** to provide hand tracking and controller model rendering in VR mode. It loads the controller 3D model from the VR runtime (or uses a default fallback object) and updates its transform each frame. Supports separate transform offsets for OpenXR, OpenVR, and Varjo runtimes. Activates only when the current input configuration is set to VR input.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| OpenXR Default Controller Additional Translation | *vec3* | Additional positional offset for the default controller model when using OpenXR. |
| OpenXR Default Controller Additional Rotation | *vec3* | Additional rotational offset (Euler angles) for the default controller model when using OpenXR. |
| OpenVR Default Controller Additional Translation | *vec3* | Additional positional offset for the default controller model when using OpenVR. |
| OpenVR Default Controller Additional Rotation | *vec3* | Additional rotational offset (Euler angles) for the default controller model when using OpenVR. |
| Varjo Default Controller Additional Translation | *vec3* | Additional positional offset for the default controller model when using Varjo. |
| Varjo Default Controller Additional Rotation | *vec3* | Additional rotational offset (Euler angles) for the default controller model when using Varjo. |
| Default Controller Object | *Object* | Fallback controller object used when the VR runtime model is not available. |


### See Also


- **[HandController](../../../../api/templates/template_vr_csharp/controllers/class.handcontroller.md)**
- **[PCHandController](../../../../api/templates/template_vr_csharp/controllers/class.pchandcontroller.md)**


## VRHandController Class

---

## void SetOutline ( )

Enables or disables the auxiliary outline on all controller model surfaces.
### Arguments

## void VibrateController ( )

Triggers haptic feedback on the VR controller.
