# Unigine::Plugins::Ultraleap Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


## Ultraleap Class

### Members

## void setBackgroundUpdate ( int update )

Sets a new value indicating if the application is allowed to receive frames in the background. By default your UNIGINE application stops rendering frames and updating its main window, when its window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Arguments

- *int* **update** - The the application is allowed to receive frames in the background

## int isBackgroundUpdate () const

Returns the current value indicating if the application is allowed to receive frames in the background. By default your UNIGINE application stops rendering frames and updating its main window, when its window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Return value

Current the application is allowed to receive frames in the background
## void setStreamImages ( int images )

Sets a new value indicating if streaming of images is currently enabled.
### Arguments

- *int* **images** - The streaming of images is currently enabled

## int isStreamImages () const

Returns the current value indicating if streaming of images is currently enabled.
### Return value

Current streaming of images is currently enabled
## void setPaused ( int paused )

Sets a new value indicating if the Ultraleap service is currently paused.
### Arguments

- *int* **paused** - The the Ultraleap service is currently paused

## int isPaused () const

Returns the current value indicating if the Ultraleap service is currently paused.
### Return value

Current the Ultraleap service is currently paused
## void setAllowPauseResume ( int resume )

Sets a new value indicating if the application is allowed to pause and unpause the Ultraleap service.
### Arguments

- *int* **resume** - The the application is allowed to pause and unpause the Ultraleap service

## int isAllowPauseResume () const

Returns the current value indicating if the application is allowed to pause and unpause the Ultraleap service.
### Return value

Current the application is allowed to pause and unpause the Ultraleap service
## void setOptimizeMode ( int mode )

Sets a new optimization mode set for tracking. One of the [OPTIMIZE_MODE_*](#OPTIMIZE_MODE_DISABLED) values. Some policies can be denied if the user has disabled the feature on their Ultraleap control panel.
### Arguments

- *int* **mode** - The optimization mode set for tracking

## int getOptimizeMode () const

Returns the current optimization mode set for tracking. One of the [OPTIMIZE_MODE_*](#OPTIMIZE_MODE_DISABLED) values. Some policies can be denied if the user has disabled the feature on their Ultraleap control panel.
### Return value

Current optimization mode set for tracking
## void setTrackingMode ( )

Sets a new tracking mode. One of the [TRACKING_MODE_*](#TRACKING_MODE_DESKTOP) values.
### Arguments

- **mode** - The tracking mode

## getTrackingMode () const

Returns the current tracking mode. One of the [TRACKING_MODE_*](#TRACKING_MODE_DESKTOP) values.
### Return value

Current tracking mode
## void setTrackingInterpolation ( int interpolation )

Sets a new value indicating if the tracking interpolation is enabled.
### Arguments

- *int* **interpolation** - The the tracking interpolation is enabled

## int isTrackingInterpolation () const

Returns the current value indicating if the tracking interpolation is enabled.
### Return value

Current the tracking interpolation is enabled
## int getConnectionStatus () const

Returns the current status of connection to the Ultraleap daemon/service. One of the [CONNECTION_STATUS_*](#CONNECTION_STATUS_NOT_CONNECTED) values.
### Return value

Current status of connection to the Ultraleap daemon/service
## int isStatusLowFPSDetected () const

Returns the current value indicating if the service cannot receive frames fast enough from the underlying hardware.
### Return value

Current the service cannot receive frames fast enough from the underlying hardware
## int isStatusPoorPerformancePause () const

Returns the current value indicating if the service has paused itself due to an insufficient frame rate from the hardware.
### Return value

Current the service has paused itself due to an insufficient frame rate from the hardware
## int isStatusTrackingErrorUnknown () const

Returns the current value indicating if the service has failed to start tracking due to unknown reasons.
### Return value

Current the service has failed to start tracking due to unknown reasons
## void setTrackingOffsetDefault ( Vec3 default )

Sets a new virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Arguments

- *Vec3* **default** - The virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters

## Vec3 getTrackingOffsetDefault () const

Returns the current virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Return value

Current virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters
## void setTransformModeOffsetDefault ( int default )

Sets a new default transform mode for the offset of a newly connected device.
One of the [TRANSFORM_MODE_*](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_HMD_VARJO) values. Setting it adjusts the offset to manually match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).


> **Notice:** If the [HMD VARJO](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_MANUAL).


### Arguments

- *int* **default** - The default transform mode for the offset of a newly connected device

## int getTransformModeOffsetDefault () const

Returns the current default transform mode for the offset of a newly connected device.
One of the [TRANSFORM_MODE_*](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_HMD_VARJO) values. Setting it adjusts the offset to manually match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).


> **Notice:** If the [HMD VARJO](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_MANUAL).


### Return value

Current default transform mode for the offset of a newly connected device
## int getNumDevices () const

Returns the current total number of recognized devices.
### Return value

Current total number of recognized devices
## int getNumDevicesConnected () const

Returns the current number of connected Ultraleap controller devices.
### Return value

Current number of connected Ultraleap controller devices
## long getLeapNow () const

Returns the current universal clock value used by the system to timestamp image and tracking frames, in microseconds since an epoch time. The clock used for the counter itself is implementation-defined, but generally speaking, it is global, monotonic, and makes use of the most accurate high-performance counter available on the system.
### Return value

Current universal clock value, in microseconds since an unspecified epoch
---

## UltraleapDevice getDevice ( int device_id )

Returns the Ultraleap controller device from the list of recognized devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## UltraleapDevice getDeviceConnected ( int device_id )

Returns the Ultraleap controller device from the list of connected devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## synchronize ( )

Synchronizes the internal Ultraleap clock rebaser with the current engine time. This keeps the Ultraleap tracking clock aligned with the engine timeline so that tracking frames are timestamped consistently (used, in particular, for tracking interpolation). In manual (non-VR) mode this is called automatically each frame on the begin render event.
