# VRBaseInteractable Component

**Inherits from:** Component


VRBaseInteractable is the base class for all interactable objects in the C# VR Template. It defines the interaction lifecycle with virtual methods for hover, grab, and use events that derived classes can override.


Interactable objects are managed by the **[VRInteractionManager](../../../../api/templates/template_vr_csharp/interactions/class.vrinteractionmanager.md)**, which detects collisions and triggers the appropriate interaction callbacks.


### See Also


- **[VRBaseInteraction](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteraction.md)**
- **[VRInteractionManager](../../../../api/templates/template_vr_csharp/interactions/class.vrinteractionmanager.md)**
- **[VRBaseController](../../../../api/templates/template_vr_csharp/base/class.vrbasecontroller.md)**


## VRBaseInteractable Class

---

## void OnHoverBegin ( )

Called when the object begins being hovered over.
### Arguments

## void OnHoverEnd ( )

Called when the object stops being hovered over.
### Arguments

## void OnGrabBegin ( )

Called when the object is grabbed.
### Arguments

## void OnGrabEnd ( )

Called when the object is released from grab.
### Arguments

## void OnUseBegin ( )

Called when the object begins being used.
### Arguments

## void OnUseEnd ( )

Called when the object stops being used.
### Arguments
