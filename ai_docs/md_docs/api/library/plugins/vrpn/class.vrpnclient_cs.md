# Unigine::Plugins::VrpnClient Class (CS)

> **Notice:** This class is a singleton.


A class for the [VRPN Plugin](../../../../code/plugins/vrpn/index_cs.md) that allows managing different input devices.


### See Also


- Article on [VRPN Plugin](../../../../code/plugins/vrpn/index_cs.md)
- UnigineScript samples:

  -
  -


## VrpnClient Class

### Members

---

## VrpnAnalogDevice createAnalogDevice ( string name )

Creates an object that allows receiving data about input device sticks (for example, game-pad sticks).
### Arguments

- *string* **name** - Path to the device in the format device_name@server_address.

### Return value

Newly created VrpnAnalogDevice.
## void deleteAnalogDevice ( VrpnAnalogDevice [] OUT_device )

Deletes the VrpnAnalogDevice object.
### Arguments

- *[VrpnAnalogDevice](../../../../api/library/plugins/vrpn/vrpnanalogdevice.class_cs.md)[]* **OUT_device** - VrpnAnalogDevice to be deleted. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## VrpnButtonDevice createButtonDevice ( string name )

Creates an object that allows receiving data about states of input device buttons.
### Arguments

- *string* **name** - Path to the device in the format device_name@server_address.

### Return value

Newly created VrpnButtonDevice.
## void deleteButtonDevice ( VrpnButtonDevice [] OUT_device )

Deletes the VrpnButtonDevice object.
### Arguments

- *[VrpnButtonDevice](../../../../api/library/plugins/vrpn/vrpnbuttondevice.class_cs.md)[]* **OUT_device** - VrpnButtonDevice to be deleted. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## VrpnTrackerDevice createTrackerDevice ( string name )

Creates an object that allows receiving data about position, orientation, velocity and acceleration of tracked objects from 3D tracking sensors.
### Arguments

- *string* **name** - Path to the device in the format device_name@server_address.

### Return value

Newly created VrpnTrackerDevice.
## void deleteTrackerDevice ( VrpnTrackerDevice [] OUT_device )

Deletes the VrpnTrackerDevice object.
### Arguments

- *[VrpnTrackerDevice](../../../../api/library/plugins/vrpn/vrpntrackerdevice.class_cs.md)[]* **OUT_device** - VrpnTrackerDevice to be deleted. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
