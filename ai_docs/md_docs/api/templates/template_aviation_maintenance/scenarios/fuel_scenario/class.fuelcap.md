# FuelCap Component

**Inherits from:** ComponentBase


FuelCap manages the aircraft fuel cap interaction. The cap can be rotated to unlock, then moved away from the fuel port. It tracks states (rotating, moving away, moving freely) and notifies **[FuelScenario](../../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelscenario.md)** when opened or closed.


The cap requires rotating past a threshold angle before it can be detached. Once detached, it can be placed in the player's inventory. The cap can be reset to its initial closed position.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Plane Fuel Cap Socket Node | *Node* | � | Socket node for the fuel cap attachment point. |
| Pivot Node | *Node* | � | Node used as rotation pivot for the cap. |
| Angle Threshold | *Float* | *90.0* | Rotation angle required to detach the cap. |
| Move Away Threshold | *Float* | *25.0* | Squared distance threshold to fully detach. |


### See Also


- **[FuelScenario](../../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelscenario.md)**
- **[ObjMovable](../../../../../api/modules/vr/components/objects/class.objmovable.md)**
- **[ObjectHandleRotatable](../../../../../api/modules/vr/components/objects/class.objecthandlerotatable.md)**


## FuelCap Class

---

## isClosed ( )

Returns whether the fuel cap is currently in the closed position.
### Return value

true if cap is closed.
## isInserted ( )

Returns whether the fuel cap is currently inserted in the fuel port (in rotating state).
### Return value

true if cap is inserted in the socket.
## void reset ( )

Resets the fuel cap to its initial closed state.
## void onPlaceInInventory ( )

Called when the fuel cap is placed into the player's inventory.
