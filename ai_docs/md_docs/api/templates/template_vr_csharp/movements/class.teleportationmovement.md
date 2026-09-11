# TeleportationMovement Component

**Inherits from:** VRBaseMovement


TeleportationMovement extends **[VRBaseMovement](../../../../api/templates/template_vr_csharp/base/class.vrbasemovement.md)** to provide arc-based teleportation in VR mode. Displays a parabolic ray from the controller to the landing point with allowed/forbidden visual indicators. The teleport is triggered by the thumbstick.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Max Distance | *Float* | Maximum teleport distance. |
| Allowed Point | *Node* | Visual marker shown at valid landing points. |
| Forbidden Point | *Node* | Visual marker shown at invalid landing points. |
| Allowed Material | *Material* | Material for the ray when the landing point is valid. |
| Forbidden Material | *Material* | Material for the ray when the landing point is invalid. |
| Ray Width | *Float* | Width of the teleport arc ray. |
| Start Point | *vec3* | Local offset for the ray start position. |


### See Also


- **[VRBaseMovement](../../../../api/templates/template_vr_csharp/base/class.vrbasemovement.md)**
- **[VRHandTrackingTeleportMovement](../../../../api/templates/template_vr_csharp/movements/class.vrhandtrackingteleportmovement.md)**


## TeleportationMovement Class
