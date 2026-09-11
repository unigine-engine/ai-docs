# InputModule::Joystick Class

**Inherits from:** Device


Joystick provides access to flight sticks, **HOTAS** systems, racing wheels, and other specialized controllers. Unlike gamepads, joysticks have variable numbers of buttons, axes, and POV hats depending on the hardware.


**POV** (Point of View) hats are directional switches commonly found on flight sticks for camera control or quick menu navigation.


Joysticks support hot-plugging - use the connected/disconnected events to handle devices being added or removed at runtime.


### See Also


- **[Device](../../../api/modules/input/class.device.md)**
- **[DeviceManager](../../../api/modules/input/class.devicemanager.md)**
- **[JoystickKeyBind](../../../api/modules/input/class.joystickkeybind.md)**
- **[JoystickAxisBind](../../../api/modules/input/class.joystickaxisbind.md)**


## InputModule::Joystick Class

---

## Joystick ( )

Default constructor.
## Joystick ( )

Constructs a joystick wrapper for the specified Unigine joystick.
### Arguments

## Joystick ( )

Constructs a joystick for the device at the specified index.
### Arguments

## setJoystick ( )

Sets the underlying Unigine joystick.
### Arguments

### Return value

True if successful.
## setJoystick ( )

Sets the joystick by index.
### Arguments

### Return value

True if successful.
## getJoystick ( )

Returns the underlying Unigine joystick pointer.
### Return value

The underlying Unigine joystick.
## getJoystickNumber ( )

Returns the joystick's device number.
### Return value

Joystick number.
## getNumPovs ( )

Returns the number of POV hats on this joystick.
### Return value

Number of POV hats.
## isPovValid ( )

Checks if the specified POV index is valid.
### Arguments

### Return value

True if valid.
## getPovValue ( )

Returns the current direction value of the specified POV hat.
### Arguments

### Return value

POV direction value.
## getPovName ( )

Returns the name of the specified POV hat.
### Arguments

### Return value

POV name.
