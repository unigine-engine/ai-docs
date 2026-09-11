# TransparentHelper Component

**Inherits from:** ComponentBase


TransparentHelper provides material transparency control for objects. It modifies the albedo color alpha channel to fade objects in and out, useful for visual effects like motion blur on spinning rotors.


The component caches the material's albedo color parameter on initialization and provides a method to update only the alpha component. It can optionally control a separate shadow object's transparency in sync with the main object.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Shadow Object | *Node* | Optional shadow mesh to synchronize transparency with the main object. |


### See Also


- **[RotorController](../../../api/templates/template_aviation_fixedwing/class.rotorcontroller.md)**


## TransparentHelper Class

---

## void setAlbedoTransparent ( )

Sets the alpha component of the albedo color for both the main object and shadow object (if assigned).
### Arguments
