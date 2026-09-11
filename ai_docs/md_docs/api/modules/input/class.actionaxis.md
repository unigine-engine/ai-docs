# InputModule::ActionAxis Class

**Inherits from:** Action


ActionAxis represents an analog input action with continuous values, typically in the range -1 to 1 or 0 to 1. It's used for inputs like throttle, steering, camera look, and other continuous controls.


When multiple bindings are active, the action uses the binding with the largest absolute value (priority to strongest input).


Axis actions support hardware analog axes (joystick sticks, triggers), fake axes from digital inputs (WASD keys simulating an axis), and dead zones, inversion, and value clamping.


### See Also


- **[Action](../../../api/modules/input/class.action.md)**
- **[AxisBind](../../../api/modules/input/class.axisbind.md)**
- **[AxisSettings](../../../api/modules/input/struct.axissettings.md)**


## InputModule::ActionAxis Class

---

## ActionAxis ( )

Constructs an axis action with the specified name and ID.
### Arguments

## addBinding ( )

Adds a binding with specific axis settings.
### Arguments

### Return value

ID of the created binding.
## void setBindingSettings ( )

Updates the settings for an existing binding.
### Arguments

## getValue ( )

Returns the current axis value, aggregated from all bindings.
### Return value

Current axis value.
