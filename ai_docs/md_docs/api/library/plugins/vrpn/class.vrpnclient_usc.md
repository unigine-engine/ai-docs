# Unigine::Plugins::VrpnClient Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


A class for the [VRPN Plugin](../../../../code/plugins/vrpn/index_usc.md) that allows managing different input devices.


### See Also


- Article on [VRPN Plugin](../../../../code/plugins/vrpn/index_usc.md)
- UnigineScript samples:

  -
  -


## VrpnClient Class

---

## VrpnAnalogDevice createAnalogDevice ( string name )

Creates an object that allows receiving data about input device sticks (for example, game-pad sticks).
### Arguments

- *string* **name** - Path to the device in the format device_name@server_address.

### Return value

Newly created VrpnAnalogDevice.
## void deleteAnalogDevice ( VrpnAnalogDevice * OUT_device )

Deletes the VrpnAnalogDevice object.
### Arguments

- *[VrpnAnalogDevice](../../../../api/library/plugins/vrpn/vrpnanalogdevice.class_usc.md) ** **OUT_device** - VrpnAnalogDevice to be deleted. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## VrpnButtonDevice createButtonDevice ( string name )

Creates an object that allows receiving data about states of input device buttons.
### Arguments

- *string* **name** - Path to the device in the format device_name@server_address.

### Return value

Newly created VrpnButtonDevice.
## void deleteButtonDevice ( VrpnButtonDevice * OUT_device )

Deletes the VrpnButtonDevice object.
### Arguments

- *[VrpnButtonDevice](../../../../api/library/plugins/vrpn/vrpnbuttondevice.class_usc.md) ** **OUT_device** - VrpnButtonDevice to be deleted. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## VrpnTrackerDevice createTrackerDevice ( string name )

Creates an object that allows receiving data about position, orientation, velocity and acceleration of tracked objects from 3D tracking sensors.
### Arguments

- *string* **name** - Path to the device in the format device_name@server_address.

### Return value

Newly created VrpnTrackerDevice.
## void deleteTrackerDevice ( VrpnTrackerDevice * OUT_device )

Deletes the VrpnTrackerDevice object.
### Arguments

- *[VrpnTrackerDevice](../../../../api/library/plugins/vrpn/vrpntrackerdevice.class_usc.md) ** **OUT_device** - VrpnTrackerDevice to be deleted. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
