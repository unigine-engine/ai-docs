# InputModule::Device Class


Device is the abstract base class for all input devices in the input system. It provides a unified interface for querying keys/buttons and axes across different device types.


Device types include **[Keyboard](../../../api/modules/input/class.keyboard.md)** (standard keyboard with keys), **[Mouse](../../../api/modules/input/class.mouse.md)** (mouse buttons and movement axes), **[Gamepad](../../../api/modules/input/class.gamepad.md)** (console-style controllers with buttons, sticks, and triggers), and **[Joystick](../../../api/modules/input/class.joystick.md)** (flight sticks, **HOTAS**, wheels with buttons, axes, and POV hats).


Each device provides events for connection and disconnection, useful for hot-plugging support.


### See Also


- **[Keyboard](../../../api/modules/input/class.keyboard.md)**
- **[Mouse](../../../api/modules/input/class.mouse.md)**
- **[Gamepad](../../../api/modules/input/class.gamepad.md)**
- **[Joystick](../../../api/modules/input/class.joystick.md)**
- **[DeviceManager](../../../api/modules/input/class.devicemanager.md)**


## InputModule::Device Class

---

## isValid ( )

Returns whether the device is valid and ready for use.
### Return value

True if device is connected and available.
## getDeviceName ( )

Returns the human-readable name of the device.
### Return value

Device name.
## getDeviceNum ( )

Returns the device number for multiple devices of the same type.
### Return value

Device number.
## getNumKeys ( )

Returns the number of keys or buttons on this device.
### Return value

Number of keys/buttons.
## isKeyValid ( )

Checks if the specified key index is valid.
### Arguments

### Return value

True if valid.
## getKeyName ( )

Returns the name of the specified key.
### Arguments

### Return value

Key name.
## isKeyDown ( )

Returns true on the frame the key was first pressed.
### Arguments

### Return value

True on first press frame.
## isKeyPressed ( )

Returns true while the key is held down.
### Arguments

### Return value

True while held.
## isKeyUp ( )

Returns true on the frame the key was released.
### Arguments

### Return value

True on release frame.
## getNumAxes ( )

Returns the number of analog axes on this device.
### Return value

Number of axes.
## isAxisValid ( )

Checks if the specified axis index is valid.
### Arguments

### Return value

True if valid.
## getAxisName ( )

Returns the name of the specified axis.
### Arguments

### Return value

Axis name.
## getAxisValue ( )

Returns the current value of the specified axis.
### Arguments

### Return value

Axis value.
## getAxisDelta ( )

Returns the change in axis value since last frame.
### Arguments

### Return value

Axis delta.
## getType ( )

Returns the type of this device.
### Return value

Device type.
## getEventConnected ( )

Returns the event that fires when the device is connected.
### Return value

Reference to the connected event.
## getEventDisconnected ( )

Returns the event that fires when the device is disconnected.
### Return value

Reference to the disconnected event.
