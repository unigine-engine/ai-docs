# FuelScenario Component

**Inherits from:** ComponentBase


FuelScenario manages a complete aircraft fueling training scenario in VR. It tracks the user through a multi-step procedure: grounding the aircraft, opening the fuel cap, connecting the fuel pistol, pumping fuel, disconnecting, closing the cap, removing grounding, and taking a fuel sample.


The scenario supports both training mode with tooltips/hints and exam mode where the user must complete steps without guidance. It integrates with **[Tablet](../../../../../api/templates/template_aviation_maintenance/missions/class.tablet.md)** for task display, **[Tooltip](../../../../../api/modules/vr/components/objects/tooltip/class.tooltip.md)** for contextual hints, and various VR interaction components.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Fuel Pistol Node | *Node* | � | Node with **[FuelPistol](../../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelpistol.md)** component. |
| Grounding Clamp Node | *Node* | � | Grounding clamp object node. |
| Fuel Syringe Node | *Node* | � | Fuel sample syringe object node. |
| Fuel Hose Node | *Node* | � | Node with **[FuelHose](../../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelhose.md)** component. |
| Required Fuel Amount | *Float* | *3.0* | Amount of fuel required to complete fueling. |
| Fuel Per Second Amount | *Float* | *1.0* | Fueling rate per second. |
| Tooltip Z Offset | *Float* | *5* | Vertical offset for tooltip positioning. |
| Is Exam | *Toggle* | *false* | Enable exam mode without hints. |
| Sockets |  |  |  |
| Plane Fuel Cap Socket Node | *Node* | � | Socket for the fuel cap on the aircraft. |
| Plane Fuel Sample Socket Node | *Node* | � | Socket for fuel sample syringe on aircraft. |
| Plane Grounding Hook Socket Node | *Node* | � | Socket for grounding clamp on aircraft. |
| Plane Fuel Pistol Socket Node | *Node* | � | Socket for fuel pistol on aircraft. |
| Fuel Station Pistol Socket Node | *Node* | � | Socket for pistol at fuel station. |
| Fuel Station Syringe Socket Node | *Node* | � | Socket for syringe at fuel station. |
| Fuel Station Clamp Socket Node | *Node* | � | Socket for grounding clamp at fuel station. |
| Tooltips |  |  |  |
| Open Tablet Tooltip Node | *Node* | � | Tooltip for opening the tablet. |
| Take Clamp Tooltip Node | *Node* | � | Tooltip for grabbing the grounding clamp. |
| Plug Clamp Tooltip Node | *Node* | � | Tooltip for connecting the grounding clamp. |
| Open Fuel Cap Tooltip Node | *Node* | � | Tooltip for opening the fuel cap. |
| Take Fuel Cap Node | *Node* | � | Tooltip for taking the fuel cap. |
| Put Cap In Inventory Tooltip Node | *Node* | � | Tooltip for storing the cap in inventory. |
| Take Fuel Pistol Tooltip Node | *Node* | � | Tooltip for grabbing the fuel pistol. |
| Insert Fuel Pistol Tooltip Node | *Node* | � | Tooltip for inserting the fuel pistol. |
| Remove Fuel Pistol Tooltip Node | *Node* | � | Tooltip for removing the fuel pistol. |
| Close Fuel Cap Tooltip Node | *Node* | � | Tooltip for closing the fuel cap. |
| Disconnect Clamp Tooltip Node | *Node* | � | Tooltip for disconnecting grounding. |
| Take Syringe Tooltip Node | *Node* | � | Tooltip for grabbing the syringe. |
| Attach Syringe Tooltip Node | *Node* | � | Tooltip for attaching the syringe. |
| Grab Pistol Hint Tooltip Node | *Node* | � | Hint for grabbing the pistol. |
| Use Pistol Hint Tooltip Node | *Node* | � | Hint for using the pistol trigger. |


### See Also


- **[Tablet](../../../../../api/templates/template_aviation_maintenance/missions/class.tablet.md)**
- **[FuelCap](../../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelcap.md)**
- **[FuelPistol](../../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelpistol.md)**
- **[FuelHose](../../../../../api/templates/template_aviation_maintenance/scenarios/fuel_scenario/class.fuelhose.md)**
- **[VRPluggable](../../../../../api/modules/vr/components/objects/class.vrpluggable.md)**
- **[VRSocketObject](../../../../../api/modules/vr/components/objects/class.vrsocketobject.md)**


## FuelScenario Class

---

## void fuelingTick ( )

Called each frame while fueling is active to update fuel amount.
## void onFuelCupClosed ( )

Called when the fuel cap is closed.
## void onFuelCupOpenned ( )

Called when the fuel cap is opened.
## void onFuelPistolUnplugged ( )

Called when the fuel pistol is disconnected from the aircraft.
## void onFuelPistolPlugged ( )

Called when the fuel pistol is connected to the aircraft.
## void setExamEnabled ( )

Enables or disables exam mode (no hints shown).
### Arguments

## getEventScenarioTimeInSeconds ( )

Returns the elapsed time since the scenario started in seconds.
### Return value

Elapsed scenario time.
## isPlaneFull ( )

Returns whether the aircraft has received the required amount of fuel.
### Return value

true if fueling is complete.
## isFuelPistolConnectedToPlane ( )

Returns whether the fuel pistol is currently connected to the aircraft.
### Return value

true if connected.
