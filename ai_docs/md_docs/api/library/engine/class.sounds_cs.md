# Unigine::Sounds Class (CS)

> **Notice:** This class is a singleton.


The *Sounds* class contains methods for handling the sound output source.


## Sounds Class

### Properties

## string CurrentDeviceName

The name of the currently used device.
## 🔒︎ string DefaultDeviceName

The name of the device set in its system by default.
## 🔒︎ int NumDevices

The total number of the available devices.
## 🔒︎ bool IsDeviceEnumerationSupported

The value indicating if the device enumeration is supported. if it is not, the further actions (for example, getting the device name) won't be possible.
## 🔒︎ bool IsDeviceConnected

The value indicating if the device is currently connected.
### Members

---

## string GetDeviceName ( int num )

Returns the name of the device by its index.
### Arguments

- *int* **num** - The index of the device.

### Return value

The name of the device.
## void UpdateDeviceList ( )

Updates the list of available devices each 5 seconds.
