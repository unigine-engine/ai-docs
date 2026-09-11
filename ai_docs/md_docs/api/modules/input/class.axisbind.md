# InputModule::AxisBind Class

**Inherits from:** Bind


AxisBind binds an analog input source to an action. It provides continuous values with support for dead zones, inversion, clamping, and fake axes from digital inputs.


AxisBind supports hardware analog axes (joystick sticks, triggers), mouse movement axes, fake axes from key pairs (e.g., W/S keys for forward/back), and value clamping modes (full range, positive only, negative only).


For fake axes, sensitivity and gravity parameters control how quickly the value changes when keys are pressed/released.


### See Also


- **[Bind](../../../api/modules/input/class.bind.md)**
- **[JoystickAxisBind](../../../api/modules/input/class.joystickaxisbind.md)**
- **[AxisSettings](../../../api/modules/input/struct.axissettings.md)**


## InputModule::AxisBind Class

---

## AxisBind ( )

Constructs an axis binding for the specified device.
### Arguments

## void setSettings ( )

Configures the binding with the specified axis settings.
### Arguments

## getSettings ( )

Returns the current axis settings.
### Return value

Current axis settings.
## void update ( )

Updates the binding state from the device.
### Arguments

## getCurrentValue ( )

Returns the current axis value after applying all transformations.
### Return value

Current axis value.
## void setValueForce ( )

Forces the binding to a specific value, bypassing device input.
### Arguments
