# IgSensor Component

**Inherits from:** ComponentBase


IgSensor is a component that automatically creates a sensor and binds it to a specific **IG** view. This is useful in multi-channel **IG** setups where different displays need different sensor effects.


The component creates the sensor on initialization, binds it to the specified view index, and cleans up on shutdown. Only available when **SENSORS_USE_IG** is defined.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| View | *Int* | **IG** view index to bind the sensor to. |
| Type | *String* | Name of the sensor type to create. |
| Enabled | *Toggle* | Initial enabled state of the sensor. |


### See Also


- **[SensorManager](../../../api/modules/sensors/class.sensormanager.md)**
- **[Sensor](../../../api/modules/sensors/class.sensor.md)**


## IgSensor Class

---

## getSensor ( )

Returns the ID of the sensor managed by this component.
### Return value

Managed sensor ID, or -1 if not created.
