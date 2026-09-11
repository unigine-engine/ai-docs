# VRInventory Component

**Inherits from:** Component


VRInventory implements a grid-based inventory system. Objects can be placed into cells and visually represented with a mesh grid and/or plane. Supports hover and take scale animations.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Cell Amount | *ivec2* | Number of cells in X and Y dimensions. |
| Use Mesh Grid | *Bool* | Whether to display a mesh grid overlay. |
| Cell Width | *Float* | Width of grid lines. |
| Cell Size | *Float* | Size of each cell. |
| Grid Material | *Material* | Material for the grid mesh. |
| Use Plane | *Bool* | Whether to display a background plane. |
| Plane Material | *Material* | Material for the background plane. |
| Hover Scale Timer | *Float* | Duration of the hover scale animation. |
| Take Scale Timer | *Float* | Duration of the take scale animation. |
| Inventory Node Scale | *vec3* | Scale applied to items in the inventory. |
| Hover Node Scale | *vec3* | Scale applied to items when hovered. |


### See Also


- **[VRInventoryItem](../../../../api/templates/template_vr_csharp/interactions/class.vrinventoryitem.md)**


## VRInventory Class

---

## GetEventOnNewInventoryItem ( )

Returns the event that fires when a new item is added to the inventory.
### Return value

Event triggered when a new item is added to the inventory.
## IsNodeInInventory ( )

Returns whether the specified node is currently in the inventory.
### Arguments

### Return value

True if the node is in the inventory.
## void RemoveItemFromInventory ( )

Removes the specified node from the inventory.
### Arguments
