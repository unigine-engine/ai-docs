# PCHandController Component

**Inherits from:** HandController


PCHandController extends **[HandController](../../../../api/templates/template_vr_csharp/controllers/class.handcontroller.md)** to simulate hand control in PC (non-VR) mode. The hand is positioned along the camera's forward direction based on world intersection, within a configurable maximum reach distance. Activates only when the current input configuration is set to PC input.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Hand Length | *Float* | Maximum reach distance for the simulated hand. |


### See Also


- **[HandController](../../../../api/templates/template_vr_csharp/controllers/class.handcontroller.md)**
- **[VRHandController](../../../../api/templates/template_vr_csharp/controllers/class.vrhandcontroller.md)**


## PCHandController Class

---

## void SetGrabDistanceToMax ( )

Sets the hand distance to the maximum reach value and refreshes the hand transform.
