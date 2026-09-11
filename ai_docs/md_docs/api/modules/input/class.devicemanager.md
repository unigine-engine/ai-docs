# InputModule::DeviceManager Class


DeviceManager is a singleton that provides access to all input devices in the system. It manages keyboard, mouse, gamepads, and joysticks, creating device wrappers as needed.


The manager handles device enumeration and provides lazy instantiation for gamepads and joysticks - device objects are created when first requested.


### See Also


- **[Device](../../../api/modules/input/class.device.md)**
- **[Keyboard](../../../api/modules/input/class.keyboard.md)**
- **[Mouse](../../../api/modules/input/class.mouse.md)**
- **[Gamepad](../../../api/modules/input/class.gamepad.md)**
- **[Joystick](../../../api/modules/input/class.joystick.md)**


## InputModule::DeviceManager Class

---

## static get ( )

Returns the singleton instance of DeviceManager.
### Return value

The singleton instance.
## getDevice ( )

Returns a device by type and number.
### Arguments

### Return value

The device, or nullptr if not found.
## getKeyboard ( )

Returns the keyboard device.
### Return value

The keyboard device.
## getMouse ( )

Returns the mouse device.
### Return value

The mouse device.
## getGamepad ( )

Returns a gamepad by index, creating it if necessary.
### Arguments

### Return value

The gamepad device.
## getJoystick ( )

Returns a joystick by index, creating it if necessary.
### Arguments

### Return value

The joystick device.
## getNumGamepads ( )

Returns the number of registered gamepad devices.
### Return value

Number of gamepads.
## getNumJoysticks ( )

Returns the number of registered joystick devices.
### Return value

Number of joysticks.
