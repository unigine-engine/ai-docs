# Unigine::Sounds Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The *Sounds* class contains methods for handling the sound output source.


## Sounds Class

### Members

---

## void engine.sounds. setCurrentDeviceName ( string name )

Changes the current device name thus changing the used current device. Only names got by the *[getDeviceName()](#getDeviceName_int_cstr)* method are supported.
### Arguments

- *string* **name** - The new name of the device.

## string engine.sounds. getCurrentDeviceName ( )

Returns the name of the currently used device.
### Return value

Current device name.
## string engine.sounds. getDefaultDeviceName ( )

Returns the name of the device set in its system by default.
### Return value

The default device name.
## int engine.sounds. isDeviceConnected ( )

Returns the value indicating if the device is currently connected.
### Return value

**1** if device is connected; otherwise **0**.
## int engine.sounds. isDeviceEnumerationSupported ( )

Returns the value indicating if the device enumeration is supported. If it is not, the further actions (for example, getting the device name) won't be possible.
## string engine.sounds. getDeviceName ( int num )

Returns the name of the device by its index.
### Arguments

- *int* **num** - The index of the device.

### Return value

The name of the device.
## int engine.sounds. getNumDevices ( )

Returns the total number of the available devices.
### Return value

Number of devices.
## void engine.sounds. updateDeviceList ( )

Updates the list of available devices each 5 seconds.
