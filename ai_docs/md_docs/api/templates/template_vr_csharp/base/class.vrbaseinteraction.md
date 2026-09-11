# VRBaseInteraction Component

**Inherits from:** Component


VRBaseInteraction is the base class for interaction handlers. An interaction defines how a controller detects and interacts with **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** objects � through raycasting, shape casting, or other means.


Derived classes override virtual methods to implement specific interaction logic (e.g., hand shape interaction, ray-based menu interaction). The **[VRInteractionManager](../../../../api/templates/template_vr_csharp/interactions/class.vrinteractionmanager.md)** calls these methods each frame.


### See Also


- **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)**
- **[VRInteractionManager](../../../../api/templates/template_vr_csharp/interactions/class.vrinteractionmanager.md)**


## VRBaseInteraction Class

---

## void Interact ( )

Called each frame to perform interaction logic (detect hover, grab, use).
### Arguments

## void StopHover ( )

Forces the current hover interaction to stop.
### Arguments

## void StopGrab ( )

Forces the current grab interaction to stop.
### Arguments

## void StopUse ( )

Forces the current use interaction to stop.
### Arguments

## void ForceGrab ( )

Forces the interaction to grab a specific interactable object.
### Arguments

## void ForceUse ( )

Forces the interaction to use a specific interactable object.
### Arguments

## void ForceHover ( )

Forces the interaction to hover over a specific interactable object.
### Arguments
