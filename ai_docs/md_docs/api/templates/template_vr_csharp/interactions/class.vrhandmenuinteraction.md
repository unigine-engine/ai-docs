# VRHandMenuInteraction Component

**Inherits from:** VRBaseInteraction


VRHandMenuInteraction extends **[VRBaseInteraction](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteraction.md)** to provide ray-based interaction from the VR hand controller. Casts a ray from the controller and interacts with GUI objects and interactables within the maximum distance. Renders a visible ray using a procedural mesh.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Max Distance | *Float* | Maximum ray distance for interaction. |
| Ray Material | *Material* | Material applied to the visible ray mesh. |
| Ray Width | *Float* | Width of the visible ray. |
| Exclude Nodes | *Node[]* | Nodes excluded from ray interaction. |


### See Also


- **[VRBaseInteraction](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteraction.md)**
- **[VRHandTrackingMenuInteraction](../../../../api/templates/template_vr_csharp/interactions/class.vrhandtrackingmenuinteraction.md)**
