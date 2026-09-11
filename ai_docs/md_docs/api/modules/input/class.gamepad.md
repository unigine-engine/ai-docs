# InputModule::Gamepad Class

**Inherits from:** Device


Gamepad provides access to console-style game controllers (Xbox, PlayStation, etc.). Gamepads have standardized buttons and axes, making them easier to support than generic joysticks.


Gamepads support hot-plugging - they can be connected and disconnected at runtime. Use the connected/disconnected events to handle this.


### See Also


- **[Device](../../../api/modules/input/class.device.md)**
- **[DeviceManager](../../../api/modules/input/class.devicemanager.md)**


## InputModule::Gamepad Class

---

## Gamepad ( )

Default constructor.
## Gamepad ( )

Constructs a gamepad wrapper for the specified Unigine gamepad.
### Arguments

## Gamepad ( )

Constructs a gamepad for the device at the specified index.
### Arguments

## setGamepad ( )

Sets the underlying Unigine gamepad.
### Arguments

### Return value

True if successful.
## setGamepad ( )

Sets the gamepad by index.
### Arguments

### Return value

True if successful.
## getGamepad ( )

Returns the underlying Unigine gamepad pointer.
### Return value

The underlying Unigine gamepad.
## getGamepadNumber ( )

Returns the gamepad's device number.
### Return value

Gamepad number.
