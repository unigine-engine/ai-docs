# HandController Component

**Inherits from:** VRBaseController


HandController extends **[VRBaseController](../../../../api/templates/template_vr_csharp/base/class.vrbasecontroller.md)** to provide hand-specific tracking and transform management. It maintains an offset transform node representing the hand position and orientation relative to the controller, and exposes properties for querying the hand's world-space transform, position, and axes.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Hand Position Offset | *vec3* | Positional offset of the hand relative to the controller. |
| Hand Rotation Offset | *vec3* | Rotational offset (Euler angles) of the hand relative to the controller. |
| Show Hand Transform | *Bool* | Whether to visualize the hand transform axes using the Visualizer. |


### See Also


- **[VRBaseController](../../../../api/templates/template_vr_csharp/base/class.vrbasecontroller.md)**
- **[PCHandController](../../../../api/templates/template_vr_csharp/controllers/class.pchandcontroller.md)**
- **[VRHandController](../../../../api/templates/template_vr_csharp/controllers/class.vrhandcontroller.md)**
- **[VRHandTracking](../../../../api/templates/template_vr_csharp/controllers/class.vrhandtracking.md)**


## HandController Class

---

## void RefreshHandTransform ( )

Recalculates the hand node's world transform based on the current controller transform and hand offset.
