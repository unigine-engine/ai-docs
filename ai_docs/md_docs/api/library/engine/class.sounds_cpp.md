# Unigine::Sounds Class (CPP)

**Header:** #include <UnigineSounds.h>

> **Notice:** This class is a singleton.


The *Sounds* class contains methods for handling the sound output source.


## Sounds Class

### Members

---

## void setCurrentDeviceName ( const char * name )

Changes the current device name thus changing the used current device. Only names got by the *[getDeviceName()](#getDeviceName_int_cstr)* method are supported.
### Arguments

- *const char ** **name** - The new name of the device.

## const char * getCurrentDeviceName ( )

Returns the name of the currently used device.
### Return value

Current device name.
## const char * getDefaultDeviceName ( )

Returns the name of the device set in its system by default.
### Return value

The default device name.
## int isDeviceConnected ( )

Returns the value indicating if the device is currently connected.
### Return value

true if device is connected; otherwise false.
## int isDeviceEnumerationSupported ( )

Returns the value indicating if the device enumeration is supported. If it is not, the further actions (for example, getting the device name) won't be possible.
## const char * getDeviceName ( int num )

Returns the name of the device by its index.
### Arguments

- *int* **num** - The index of the device.

### Return value

The name of the device.
## int getNumDevices ( )

Returns the total number of the available devices.
### Return value

Number of devices.
## void updateDeviceList ( )

Updates the list of available devices each 5 seconds.
