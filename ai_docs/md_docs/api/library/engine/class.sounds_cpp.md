# Unigine::Sounds Class (CPP)

**Header:** #include <UnigineSounds.h>

> **Notice:** This class is a singleton.


The *Sounds* class contains methods for handling the sound output source.


## Sounds Class

### Members

## void setCurrentDeviceName ( const char * name )

Sets a new current device name (changing the name changes the currently used device as well). Only names got by the *[getDeviceName()](#getDeviceName_int_cstr)* method are supported.
### Arguments

- *const char ** **name** - The name of the currently used device.

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

## const char * getDeviceName ( int num )

Returns the name of the device by its index.
### Arguments

- *int* **num** - The index of the device.

### Return value

The name of the device.
## void updateDeviceList ( )

Updates the list of available devices each 5 seconds.
## float getSampleWaveform ( const char * name , int num_bins , Vector <float> & OUT_out_peaks ) const

Builds a peak-amplitude waveform preview of a sound file without playing it. The file is decoded in streaming chunks, so long tracks do not need to fit into memory entirely.
### Arguments

- *const char ** **name** - Path to the sound sample file.
- *int* **num_bins** - Number of bins in the output waveform. If a non-positive value is passed, the bin count is chosen automatically as 100 bins per second of audio, clamped to the [256; 16384] range.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **OUT_out_peaks** - Output vector resized to the number of bins, where each element is the peak amplitude of the frames falling into that time slice, normalized to the [0; 1] range. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Duration of the sample in seconds, or 0.0 if the file cannot be loaded.
