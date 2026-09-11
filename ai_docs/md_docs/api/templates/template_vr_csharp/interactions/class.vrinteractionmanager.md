# VRInteractionManager Component

**Inherits from:** Component


VRInteractionManager is a central manager that tracks the interaction state of all **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)** objects. It provides static methods to query whether objects are hovered, grabbed, or used, and to force-grab or release objects programmatically.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Interaction Collision Mask | *Mask* | Collision mask used for interaction raycasts. |
| Grab Collision Mask | *Mask* | Collision mask used for grab detection. |


### See Also


- **[VRBaseInteractable](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteractable.md)**
- **[VRBaseInteraction](../../../../api/templates/template_vr_csharp/base/class.vrbaseinteraction.md)**


## VRInteractionManager Class

---

## static IsInteract ( )

Returns whether the specified object is currently being interacted with (hovered, grabbed, or used).
### Arguments

### Return value

True if the object is in any interaction state.
## static IsHovered ( )

Returns whether the specified object is currently hovered.
### Arguments

### Return value

True if the object is hovered.
## static IsGrabbed ( )

Returns whether the specified object is currently grabbed.
### Arguments

### Return value

True if the object is grabbed.
## static IsUsed ( )

Returns whether the specified object is currently being used.
### Arguments

### Return value

True if the object is being used.
## static GetGrabbedInteractables ( )

Returns a list of all currently grabbed interactable objects.
### Return value

List of currently grabbed interactable objects.
## static GetHoverInteraction ( )

Returns the interaction that is currently hovering the specified object.
### Arguments

### Return value

The interaction currently hovering the object, or null.
## static GetGrabInteraction ( )

Returns the interaction that is currently grabbing the specified object.
### Arguments

### Return value

The interaction currently grabbing the object, or null.
## static GetUseInteraction ( )

Returns the interaction that is currently using the specified object.
### Arguments

### Return value

The interaction currently using the object, or null.
## static void StopHover ( )

Stops hover state for the specified interaction.
### Arguments

## static void StopGrab ( )

Stops grab state for the specified interaction.
### Arguments

## static void StopUse ( )

Stops use state for the specified interaction.
### Arguments

## static ForceGrab ( )

Forces the specified interaction to grab the object.
### Arguments

### Return value

True if the grab was successful.
## static void ForceRelease ( )

Forces the specified interaction to release the object.
### Arguments
