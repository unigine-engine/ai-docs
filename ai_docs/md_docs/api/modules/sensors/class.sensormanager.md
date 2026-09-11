# SensorManager Component

**Inherits from:** ComponentBase


SensorManager is a singleton component that manages sensor instances and their bindings to render targets. Sensors apply post-process materials to specific viewports, enabling effects like thermal imaging, night vision, or other image processing filters.


The manager handles sensor lifecycle (creation, removal), binding sensors to Players or **IG** views, and synchronization across networked instances when **Syncker** is enabled. Each sensor has an associated material that defines its visual effect, and can be independently enabled or set to active state.


### See Also


- **[Sensor](../../../api/modules/sensors/class.sensor.md)**
- **[IgSensor](../../../api/modules/sensors/class.igsensor.md)**
- **[SensorTypeComponent](../../../api/modules/sensors/class.sensortypecomponent.md)**


## SensorManager Class

---

## static get ( )

Returns the singleton instance of the sensor manager.
### Return value

Singleton instance.
## isSensorExists ( )

Checks whether a sensor with the given ID exists.
### Arguments

### Return value

True if sensor exists.
## isSensorTypeExists ( )

Checks whether a sensor type with the given name is registered.
### Arguments

### Return value

True if type is registered.
## createSensor ( )

Creates a new sensor of the specified type with a target binding.
### Arguments

### Return value

New sensor ID.
## createSensor ( )

Creates a new sensor of the specified type without binding.
### Arguments

### Return value

New sensor ID.
## void removeSensor ( )

Removes a sensor by ID.
### Arguments

## isSensorEnabled ( )

Returns whether the sensor is enabled.
### Arguments

### Return value

True if enabled.
## void setSensorEnabled ( )

Sets whether the sensor is enabled.
### Arguments

## isSensorActive ( )

Returns whether the sensor is currently active.
### Arguments

### Return value

True if active.
## void setSensorActive ( )

Sets whether the sensor is active.
### Arguments

## getSensorBinding ( )

Returns the current target binding for a sensor.
### Arguments

### Return value

Current binding or nullptr.
## void setSensorBinding ( )

Sets the target binding for a sensor.
### Arguments

## getSensors ( )

Returns all registered sensor IDs.
### Return value

Vector of all sensor IDs.
## getSensors ( )

Returns sensor IDs of the specified type.
### Arguments

### Return value

Vector of matching sensor IDs.
## getSensors ( )

Returns sensor IDs bound to the specified target.
### Arguments

### Return value

Vector of matching sensor IDs.
## getSensorTypes ( )

Returns all registered sensor type names.
### Return value

Vector of type names.
## getSensorType ( )

Returns the type name of a sensor.
### Arguments

### Return value

Sensor type name.
## getSensorMaterial ( )

Returns the material instance for a sensor.
### Arguments

### Return value

Sensor material instance.
## getSensorTypeMaterial ( )

Returns the base material for a sensor type.
### Arguments

### Return value

Base material for the type.
## getSensorEventRender ( )

Returns the render event for a sensor, triggered when render state changes.
### Arguments

### Return value

Render event invoker.
## getSensorEventActive ( )

Returns the active event for a sensor, triggered when active state changes.
### Arguments

### Return value

Active event invoker.
## getEventSensorCreated ( )

Returns the event triggered when a new sensor is created. Callback receives the sensor ID.
### Return value

Sensor created event.
## getEventSensorRemoved ( )

Returns the event triggered when a sensor is removed. Callback receives the sensor ID.
### Return value

Sensor removed event.
