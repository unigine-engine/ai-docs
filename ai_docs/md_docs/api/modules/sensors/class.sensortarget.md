# SensorTarget Namespace

**Inherits from:** SensorTarget::BaseSensorTarget::BaseSensorTarget::Base


SensorTarget namespace contains structures for specifying render targets that sensors can bind to. A sensor binding determines which viewport receives the sensor's post-process effect.


Three target types are available: None (unbound), Player (binds to a Player's viewport), and IgView (binds to an **IG** channel view). Use these when creating sensors via **SensorManager::createSensor()** or when changing bindings at runtime.


### See Also


- **[SensorManager](../../../api/modules/sensors/class.sensormanager.md)**


## SensorTarget::Base Class

---

## getType ( )

Returns the type of this target binding.
### Return value

Target type enum value.
## SensorTarget::None Class

---

## None ( )

Constructs an unbound target. Sensors with this binding will not render.
## SensorTarget::Player Class

---

## Player ( )

Constructs a player target from a player ID.
### Arguments

## Player ( )

Constructs a player target from a Player pointer.
### Arguments


## SensorTarget::IgView Class

---

## IgView ( )

Constructs an IG view target for the specified view index.
### Arguments
