# VRPCHeadMenuInteraction Component

**Inherits from:** VRBaseInteraction


VRPCHeadMenuInteraction extends **[VRBaseInteraction](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteraction.md)** to provide gaze-based interaction in PC (non-VR) mode. Casts a ray from the head controller and interacts with GUI objects and interactables. Renders a visible sphere cursor at the interaction point.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Max Distance | *Float* | Maximum ray distance for interaction. |
| Sphere Material | *Material* | Material applied to the cursor sphere. |
| Sphere Radius | *Float* | Radius of the cursor sphere. |
| Exclude Nodes | *Node[]* | Nodes excluded from ray interaction. |


### See Also


- **[VRBaseInteraction](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteraction.md)**
- **[VRHandMenuInteraction](../../../../api/templates/template_vr_csharp/interactions/class.vrhandmenuinteraction.md)**
