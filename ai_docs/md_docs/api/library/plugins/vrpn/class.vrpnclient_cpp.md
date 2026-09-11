# Unigine::Plugins::VrpnClient Class (CPP)

**Header:** #include <plugins/Unigine/VrpnClient/UnigineVrpnClient.h>

> **Notice:** This class is a singleton.


A class for the [VRPN Plugin](../../../../code/plugins/vrpn/index_cpp.md) that allows managing different input devices.


### See Also


- Article on [VRPN Plugin](../../../../code/plugins/vrpn/index_cpp.md)
- UnigineScript samples:

  -
  -


## VrpnClient Class

---

## VrpnAnalogDeviceInterface * createAnalogDevice ( const char * name )

Creates an object that allows receiving data about input device sticks (for example, game-pad sticks).
### Arguments

- *const char ** **name** - Path to the device in the format device_name@server_address.

### Return value

Newly created VrpnAnalogDevice.
## void deleteAnalogDevice ( VrpnAnalogDeviceInterface * OUT_device )

Deletes the VrpnAnalogDevice object.
### Arguments

- *VrpnAnalogDeviceInterface ** **OUT_device** - VrpnAnalogDevice to be deleted. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## VrpnButtonDeviceInterface * createButtonDevice ( const char * name )

Creates an object that allows receiving data about states of input device buttons.
### Arguments

- *const char ** **name** - Path to the device in the format device_name@server_address.

### Return value

Newly created VrpnButtonDevice.
## void deleteButtonDevice ( VrpnButtonDeviceInterface * OUT_device )

Deletes the VrpnButtonDevice object.
### Arguments

- *VrpnButtonDeviceInterface ** **OUT_device** - VrpnButtonDevice to be deleted. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## VrpnTrackerDeviceInterface * createTrackerDevice ( const char * name )

Creates an object that allows receiving data about position, orientation, velocity and acceleration of tracked objects from 3D tracking sensors.
### Arguments

- *const char ** **name** - Path to the device in the format device_name@server_address.

### Return value

Newly created VrpnTrackerDevice.
## void deleteTrackerDevice ( VrpnTrackerDeviceInterface * OUT_device )

Deletes the VrpnTrackerDevice object.
### Arguments

- *VrpnTrackerDeviceInterface ** **OUT_device** - VrpnTrackerDevice to be deleted. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
