# AvionicsIndicatorsController Component

**Inherits from:** ComponentBase


When building a cockpit with multiple analog instruments, you need a way to feed flight data to all of them from a single source. AvionicsIndicatorsController solves this by acting as a central hub that distributes flight parameters to all indicator components.


Instead of connecting your flight model outputs to each indicator individually, you create a node hierarchy containing all your analog indicator meshes (**[Airspeed](../../../api/modules/avionics/class.airspeed.md)**, **[Altimeter](../../../api/modules/avionics/class.altimeter.md)**, **[Attitude](../../../api/modules/avionics/class.attitude.md)**, **[Compass](../../../api/modules/avionics/class.compass.md)**, **[Variometer](../../../api/modules/avionics/class.variometer.md)** components), add AvionicsIndicatorsController to a parent node, set Indicators Root to point to this hierarchy, and connect your flight model to the controller's runtime parameters.


The controller automatically finds all indicator components in children of the root node during initialization and updates them each frame with the appropriate values (speed to Airspeed, altitude to Altimeter, pitch/roll to Attitude, etc.).


This design simplifies cockpit setup and makes it easy to swap indicator implementations or add new instruments without modifying your flight model integration code.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Indicators Group |  |  |
| Indicators Root | *Node* | Root node containing indicator components. |
| Runtime Group |  |  |
| In Speed | *Float* | Input speed value. |
| In Altitude | *Float* | Input altitude value. |
| In Pitch | *Float* | Input pitch angle. |
| In Roll | *Float* | Input roll angle. |
| In Y Acceleration Fps | *Float* | Input lateral acceleration. |
| In Z Acceleration Fps | *Float* | Input vertical acceleration. |
| In Yaw | *Float* | Input yaw angle. |
| In Vertical Speed | *Float* | Input vertical speed. |


### See Also


- **[Airspeed](../../../api/modules/avionics/class.airspeed.md)**
- **[Altimeter](../../../api/modules/avionics/class.altimeter.md)**
- **[Attitude](../../../api/modules/avionics/class.attitude.md)**
- **[Compass](../../../api/modules/avionics/class.compass.md)**
- **[Variometer](../../../api/modules/avionics/class.variometer.md)**
