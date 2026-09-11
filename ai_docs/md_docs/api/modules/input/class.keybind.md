# InputModule::KeyBind Class

**Inherits from:** Bind


KeyBind binds a digital input (key, button) to an action. It tracks the current state and provides down/pressed/up detection.


KeyBind supports various input sources including keyboard keys, mouse buttons, gamepad buttons, axis-as-button (trigger pressed past threshold), and POV hat directions (via **[JoystickKeyBind](../../../api/modules/input/class.joystickkeybind.md)**).


### See Also


- **[Bind](../../../api/modules/input/class.bind.md)**
- **[JoystickKeyBind](../../../api/modules/input/class.joystickkeybind.md)**
- **[KeySettings](../../../api/modules/input/struct.keysettings.md)**


## InputModule::KeyBind Class

---

## KeyBind ( )

Constructs a key binding for the specified device.
### Arguments

## void setSettings ( )

Configures the binding with the specified key settings.
### Arguments

## getSettings ( )

Returns the current key settings.
### Return value

Current key settings.
## void update ( )

Updates the binding state from the device.
## getCurrentValue ( )

Returns whether the key is currently pressed.
### Return value

True if pressed.
## isKeyDown ( )

Returns true on the frame when the key was first pressed.
### Return value

True on first press frame.
## isKeyPressed ( )

Returns true while the key is held down.
### Return value

True while held.
## isKeyUp ( )

Returns true on the frame when the key was released.
### Return value

True on release frame.
## void setValueForce ( )

Forces the binding to a specific value, bypassing device input.
### Arguments
