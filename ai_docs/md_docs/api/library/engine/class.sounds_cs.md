# Unigine::Sounds Class (CS)

> **Notice:** This class is a singleton.


The *Sounds* class contains methods for handling the sound output source.


## Sounds Class

### Properties

## string CurrentDeviceName

The current device name (changing the name changes the currently used device as well). Only names got by the *[getDeviceName()](#getDeviceName_int_cstr)* method are supported.
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
## float GetSampleWaveform ( string name , int num_bins , float[] OUT_out_peaks )

Builds a peak-amplitude waveform preview of a sound file without playing it. The file is decoded in streaming chunks, so long tracks do not need to fit into memory entirely.
### Arguments

- *string* **name** - Path to the sound sample file.
- *int* **num_bins** - Number of bins in the output waveform. If a non-positive value is passed, the bin count is chosen automatically as 100 bins per second of audio, clamped to the [256; 16384] range.
- *float[]* **OUT_out_peaks** - Output vector resized to the number of bins, where each element is the peak amplitude of the frames falling into that time slice, normalized to the [0; 1] range. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Duration of the sample in seconds, or 0.0 if the file cannot be loaded.
