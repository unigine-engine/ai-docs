# EffectAircraftController Component

**Inherits from:** NetworkComponentBase


EffectAircraftController is a central controller for managing multiple aircraft effects (fires, smoke, contrails). Instead of controlling each effect individually, you control them through this single component using toggle parameters.


The controller automatically discovers all **[EffectAircraft](../../../api/modules/ig_aviation/class.effectaircraft.md)** components in child nodes during initialization and provides a unified interface to enable/disable them by type. This simplifies integration with flight models and damage systems.


Use cases include simulating engine fires when engines are damaged, showing landing gear fires during hard landings, enabling contrails at high altitude, and displaying smoke trails during combat damage.


The component supports network synchronization, ensuring effect states are consistent across distributed displays.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Engine Fires Group |  |  |
| Fire Engine 1 | *Toggle* | Enable/disable engine 1 fire effect. |
| Fire Engine 2 | *Toggle* | Enable/disable engine 2 fire effect. |
| Fire Engine 3 | *Toggle* | Enable/disable engine 3 fire effect. |
| Fire Engine 4 | *Toggle* | Enable/disable engine 4 fire effect. |
| Other Effects Group |  |  |
| Fire Landing Front | *Toggle* | Enable/disable front landing gear fire. |
| Fire Landing Back | *Toggle* | Enable/disable rear landing gear fire. |
| Fire Tail | *Toggle* | Enable/disable tail fire effect. |
| Smoke | *Toggle* | Enable/disable smoke trail. |
| Contrail | *Toggle* | Enable/disable condensation trail. |
| Burning | *Toggle* | Enable/disable general burning effect. |


### See Also


- **[EffectAircraft](../../../api/modules/ig_aviation/class.effectaircraft.md)**


## EffectAircraftController Class

---

## void setEnable ( )

Enables or disables a specific effect type.
### Arguments
