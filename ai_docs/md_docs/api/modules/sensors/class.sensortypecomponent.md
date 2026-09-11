# SensorTypeComponent Component

**Inherits from:** ComponentBase


SensorTypeComponent defines a sensor type that can be instantiated by the SensorManager. Each type has a unique name and an associated post-process material that defines the visual effect applied when the sensor is active.


Add this component to nodes in your scene to register sensor types. The **[SensorManager](../../../api/modules/sensors/class.sensormanager.md)** will discover all SensorTypeComponent instances and make their types available for sensor creation.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Name | *String* | Unique identifier for this sensor type, used when creating sensors via **[SensorManager](../../../api/modules/sensors/class.sensormanager.md)**. |
| Material | *Material* | Post-process material applied to the viewport when this sensor type is active. |


### See Also


- **[SensorManager](../../../api/modules/sensors/class.sensormanager.md)**
