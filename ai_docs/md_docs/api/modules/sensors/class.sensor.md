# Sensor Component

**Inherits from:** ComponentBase


Sensor is a component that automatically creates and manages a sensor instance through the SensorManager. When initialized, it creates a sensor of the specified type and removes it on shutdown.


Use this component when you want to define sensors declaratively in the scene rather than creating them programmatically.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Type | *String* | Name of the sensor type to create (must match a registered **[SensorTypeComponent](../../../api/modules/sensors/class.sensortypecomponent.md)** name). |
| Enabled | *Toggle* | Initial enabled state of the sensor. |


### See Also


- **[SensorManager](../../../api/modules/sensors/class.sensormanager.md)**
- **[SensorTypeComponent](../../../api/modules/sensors/class.sensortypecomponent.md)**


## Sensor Class

---

## getSensor ( )

Returns the ID of the sensor managed by this component.
### Return value

Managed sensor ID, or -1 if not created.
