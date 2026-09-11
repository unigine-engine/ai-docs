# TransparentHelper Component

**Inherits from:** ComponentBase


TransparentHelper manages smooth transparency transitions for objects and their shadow casters. When using transparent materials, shadows may not work correctly, so a separate invisible mesh with a shadow-only mask can be used. This helper synchronizes the transparency of both meshes.


The **[RotorBlade](../../../api/modules/ig_aviation/class.rotorblade.md)** component uses TransparentHelper to smoothly fade blades and disks during the RPM-based transition.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Shadow Object | *Node* | Optional separate mesh for shadow casting. |


### See Also


- **[RotorBlade](../../../api/modules/ig_aviation/class.rotorblade.md)**


## TransparentHelper Class

---

## void setAlbedoTransparent ( )

Sets the albedo alpha channel for both the main object and shadow object materials.
### Arguments

## getMaterialInherit ( )

Returns the inherited material of the main object.
### Return value

The inherited material.
