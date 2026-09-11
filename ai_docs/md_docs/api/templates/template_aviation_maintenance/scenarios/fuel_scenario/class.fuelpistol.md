# FuelPistol Component

**Inherits from:** VRPluggable


FuelPistol extends **[VRPluggable](../../../../../api/modules/vr/components/objects/class.vrpluggable.md)** to create a fuel dispensing nozzle that can be grabbed and connected simultaneously. Unlike standard pluggable objects, the pistol remains grabbable while connected to the aircraft fuel port.


The pistol can connect to either the fuel station (storage) or the aircraft. When connected to the aircraft and the trigger is used, it pumps fuel through **[FuelScenario](../../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelscenario.md)**.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Plane Fuel Pistol Socket Node | *Node* | � | Socket node on the aircraft for pistol connection. |


### See Also


- **[FuelScenario](../../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelscenario.md)**
- **[VRPluggable](../../../../../api/modules/vr/components/objects/class.vrpluggable.md)**
- **[ObjMovable](../../../../../api/modules/vr/components/objects/class.objmovable.md)**


## FuelPistol Class

---

## isConnectedToFuelStation ( )

Returns whether the pistol is currently connected to the fuel station socket.
### Return value

true if connected to station.
## isConnectedToPlane ( )

Returns whether the pistol is currently connected to the aircraft fuel port.
### Return value

true if connected to aircraft.
## void reset ( )

Resets the pistol to its initial state at the fuel station.
