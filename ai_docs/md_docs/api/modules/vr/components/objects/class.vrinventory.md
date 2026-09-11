# VRInventory Component

**Inherits from:** ComponentBase


VRInventory provides a grid-based inventory system that floats in front of the player. Items can be placed into cells and retrieved later. The inventory supports hover animations and scales items for display.


The inventory renders as a dynamic mesh grid attached to the player's head. When items are dropped near the inventory, they snap into available cells. Picking up items from cells returns them to their original scale.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Grid Group |  |  |
| Cell Amount | *IVec2* | Grid size (columns x rows). |
| Use Mesh Grid | *Toggle* | Render grid lines. |
| Cell Width | *Float* | Grid line thickness (*default: 0.01*). |
| Cell Size | *Float* | Cell dimensions (*default: 0.1*). |
| Grid Material | *Material* | Material for grid lines. |
| Background Group |  |  |
| Use Plane | *Toggle* | Render background plane. |
| Plane Material | *Material* | Background material. |
| Animation Group |  |  |
| Hover Scale Timer | *Float* | Duration of hover scale animation. |
| Take Scale Timer | *Float* | Duration of take scale animation. |
| Inventory Node Scale | *Vec3* | Scale of items in inventory. |
| Hover Node Scale | *Vec3* | Scale during hover. |


### See Also


- **[VRInventoryItem](../../../../../api/modules/vr/components/objects/class.vrinventoryitem.md)**


## VRInventory Class

---

## getEventOnNewInventoryItem ( )

Returns the event triggered when a new item is added to the inventory.
### Return value

New item event.
## isNodeInInventory ( )

Returns whether a node is currently in the inventory.
### Arguments

### Return value

True if in inventory.
## void removeItemFromInventory ( )

Removes an item from the inventory.
### Arguments
