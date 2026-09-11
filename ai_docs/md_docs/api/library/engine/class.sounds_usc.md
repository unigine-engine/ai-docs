# Unigine::Sounds Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


The *Sounds* class contains methods for handling the sound output source.


## Sounds Class

### Members

## void setCurrentDeviceName ( string name )

Sets a new current device name (changing the name changes the currently used device as well). Only names got by the *[getDeviceName()](#getDeviceName_int_cstr)* method are supported.
### Arguments

- *string* **name** - The name of the currently used device.

## const char * getCurrentDeviceName () const

Returns the current current device name (changing the name changes the currently used device as well). Only names got by the *[getDeviceName()](#getDeviceName_int_cstr)* method are supported.
### Return value

Current name of the currently used device.
## const char * getDefaultDeviceName () const

Returns the current name of the device set in its system by default.
### Return value

Current default device name.
## int getNumDevices () const

Returns the current total number of the available devices.
### Return value

Current number of devices.
## int isDeviceEnumerationSupported () const

Returns the current The value indicating if the device enumeration is supported. if it is not, the further actions (for example, getting the device name) won't be possible.
### Return value

Current device enumeration is supported
## int isDeviceConnected () const

Returns the current value indicating if the device is currently connected.
### Return value

Current device is currently connected
---

## string engine.sounds. getDeviceName ( int num )

Returns the name of the device by its index.
### Arguments

- *int* **num** - The index of the device.

### Return value

The name of the device.
## void engine.sounds. updateDeviceList ( )

Updates the list of available devices each 5 seconds.
