# VRHandShapeInteraction Component

**Inherits from:** VRBaseInteraction


VRHandShapeInteraction extends **[VRBaseInteraction](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteraction.md)** to provide proximity-based interaction using a contact object (typically the hand mesh or a collision shape). Detects hover and grab by checking physical contact between the controller's object and interactable objects.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Show Interact Trigger | *Bool* | Whether to visualize the interaction trigger volume. |
| Use This Node As Object | *Bool* | Whether to use this component's node as the contact object. |
| Contact Object | *Object* | Custom contact object for proximity detection (available when Use This Node As Object is disabled). |


### See Also


- **[VRBaseInteraction](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteraction.md)**
- **[VRHandMenuInteraction](../../../../api/templates/template_vr_csharp/interactions/class.vrhandmenuinteraction.md)**


## VRHandShapeInteraction Class

---

## GetGrabbedObject ( )

Returns the object currently grabbed by this interaction.
### Return value

The currently grabbed object, or null.
