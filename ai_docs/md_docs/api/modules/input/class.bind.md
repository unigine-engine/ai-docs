# InputModule::Bind Class


Bind is the abstract base class for input bindings that connect physical device inputs to actions. Each binding is associated with a specific device and tracks whether it's enabled and valid.


Concrete binding types include **[KeyBind](../../../api/modules/input/class.keybind.md)** for keyboard keys or mouse/gamepad buttons, **[AxisBind](../../../api/modules/input/class.axisbind.md)** for analog axes, **[JoystickKeyBind](../../../api/modules/input/class.joystickkeybind.md)** for joystick buttons with POV support, and **[JoystickAxisBind](../../../api/modules/input/class.joystickaxisbind.md)** for joystick axes with advanced features.


Bindings can be serialized to **XML** for saving user control preferences.


### See Also


- **[KeyBind](../../../api/modules/input/class.keybind.md)**
- **[AxisBind](../../../api/modules/input/class.axisbind.md)**
- **[Action](../../../api/modules/input/class.action.md)**


## InputModule::Bind Class

---

## void setDevice ( )

Sets the input device for this binding.
### Arguments

## getDevice ( )

Returns the device associated with this binding.
### Return value

The bound device.
## getDeviceType ( )

Returns the type of device this binding is associated with.
### Return value

The device type.
## isEnabled ( )

Returns whether this binding is enabled.
### Return value

True if enabled.
## void setEnabled ( )

Enables or disables this binding.
### Arguments

## isValid ( )

Returns whether this binding is properly configured and ready to use.
### Return value

True if valid.
## getID ( )

Returns the unique ID of this binding.
### Return value

The binding ID.
## void setID ( )

Sets the binding ID.
### Arguments

## void clearState ( )

Resets the binding state to default values.
## getControlsName ( )

Returns a user-friendly name for the bound input (e.g., "Space", "Left Stick X").
### Return value

Human-readable name of the bound control.
