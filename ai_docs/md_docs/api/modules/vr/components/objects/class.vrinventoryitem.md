# VRInventoryItem Component

**Inherits from:** ComponentBase


VRInventoryItem marks an object as storable in the VR inventory system. The component defines how the object should be positioned and rotated when placed in the inventory.


Attach this component to objects that can be picked up and stored in the **[VRInventory](../../../../../api/modules/vr/components/objects/class.vrinventory.md)**.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| inventory_position_param | *Vec3* | Position offset when displayed in inventory. |
| inventory_rotation_euler_param | *Vec3* | Rotation (Euler angles) when displayed in inventory. |


### See Also


- **[VRInventory](../../../../../api/modules/vr/components/objects/class.vrinventory.md)**


## VRInventoryItem Class

---

## getInventoryTransform ( )

Returns the transformation matrix for displaying the item in the inventory.
### Return value

Inventory display transformation.
