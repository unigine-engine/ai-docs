# Unigine::Plugins::Ultraleap Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


## Ultraleap Class

### Members

---

## void setBackgroundUpdate ( int update )

Sets the value indicating whether the application is allowed to receive frames in the background. By default your UNIGINE application stops rendering frames and updating its main window, when it window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Arguments

- *int* **update** - The window update mode: **1** for constantly repeating update cycle (i.e. the application is updated even if the window is hidden or out of focus); otherwise, **0**.

## int isBackgroundUpdate ( )

Returns a value indicating whether the application is allowed to receive frames in the background.
### Return value

**1** if the update cycle is constantly repeated (i.e. the application is updated even if the window is hidden or out of focus); otherwise, **0**.
## void setStreamImages ( int images )

Enables or disables streaming of images.
### Arguments

- *int* **images** - **1** - to enable streaming of images; **0** - to disable it.

## int isStreamImages ( )

Returns a value indicating if streaming of images is currently enabled.
### Return value

**1** if streaming of images is currently enabled; otherwise, **0**.
## void setPaused ( int paused )

Pauses or resumes the Ultraleap service.
### Arguments

- *int* **paused** - **1** - to pause the Ultraleap service; **0** - to resume it.

## int isPaused ( )

Returns a value indicating if the Ultraleap service is currently paused.
### Return value

**1** if the Ultraleap service is currently paused; otherwise, **0**.
## void setAllowPauseResume ( int resume )

Allows the application to pause and unpause the Ultraleap service.
### Arguments

- *int* **resume** - **1** — to allow the application pause and unpause the Ultraleap service; otherwise, **0**.

## int isAllowPauseResume ( )

Returns a value indicating if the application is allowed to pause and unpause the Ultraleap service.
### Return value

**1** if the application is allowed to pause and unpause the Ultraleap service; otherwise, **0**.
## void setOptimizeMode ( int mode )

Sets an optimization mode for tracking. Some policies can be denied if the user has disabled the feature on their Ultraleap control panel.
### Arguments

- *int* **mode** - The optimization mode. One of the [ULTRALEAP_OPTIMIZE_MODE_*](#OPTIMIZE_MODE_DISABLED) values.

## int getOptimizeMode ( )

Returns the current optimization mode set for tracking.
### Return value

The optimization mode. One of the [ULTRALEAP_OPTIMIZE_MODE_*](#OPTIMIZE_MODE_DISABLED) values.
## void setTrackingMode ( int mode )

Sets the tracking mode.
### Arguments

- *int* **mode** - The tracking mode. One of the [ULTRALEAP_TRACKING_MODE_*](#TRACKING_MODE_DESKTOP) values.

## int getTrackingMode ( )

Returns the current tracking mode.
### Return value

The tracking mode. One of the [ULTRALEAP_TRACKING_MODE_*](#TRACKING_MODE_DESKTOP) values.
## void setTrackingInterpolation ( int interpolation )

Toggles the tracking interpolation on and off.
### Arguments

- *int* **interpolation** - **1** — to enable the tracking interpolation; otherwise, **0**.

## int isTrackingInterpolation ( )

Returns the value indicating if the tracking interpolation is enabled.
### Return value

**1** if the tracking interpolation is enabled; otherwise, **0**.
## int getConnectionStatus ( )

Retuns the status of connection to the Ultraleap daemon/service.
### Return value

The connection status. One of the [ULTRALEAP_CONNECTION_STATUS_*](#CONNECTION_STATUS_NOT_CONNECTED) values.
## int isStatusLowFPSDetected ( )

Returns the value indicating if the service cannot receive frames fast enough from the underlying hardware.
### Return value

**1** if the service cannot receive frames fast enough from the underlying hardware; otherwise, **0**.
## int isStatusPoorPerformancePause ( )

Returns the value indicating if the service has paused itself due to an insufficient frame rate from the hardware.
### Return value

**1** if the service has paused itself due to an insufficient frame rate from the hardware; otherwise, **0**.
## int isStatusTrackingErrorUnknown ( )

Returns the value indicating if the service has failed to start tracking due to unknown reasons.
### Return value

**1** if the service has failed to start tracking due to unknown reasons; otherwise, **0**.
## void setTrackingOffsetDefault ( Vec3 val )

Sets the default offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Arguments

- *Vec3* **val** - The the default offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).

## Vec3 getTrackingOffsetDefault ( )

Returns the current virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters.
### Return value

The default offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters.
## void setTransformModeOffsetDefault ( int val )

Sets the offset to manually adjust the specified transform mode. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
> **Notice:** If the [HMD VARJO](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_MANUAL).


### Arguments

- *int* **val** - Transform mode. One of the [ULTRALEAP_TRANSFORM_MODE_*](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_HMD_VARJO) values.

## int getTransformModeOffsetDefault ( )

Returns the default transform mode for the offset of a newly connected device.
### Return value

The transform mode. One of the [ULTRALEAP_TRANSFORM_MODE_*](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_usc.md#TRANSFORM_MODE_HMD_VARJO) values.
## int getNumDevices ( )

Returns the total number of recognized devices.
### Return value

The number of connected devices.
## UltraleapDevice getDevice ( int device_id )

Returns the Ultraleap controller device from the list of recognized devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## int getNumDevicesConnected ( )

Returns the number of connected Ultraleap controller devices.
### Return value

The number of connected Ultraleap controller devices.
## UltraleapDevice getDeviceConnected ( int device_id )

Returns the Ultraleap controller device from the list of connected devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## long getLeapNow ( )

Samples the universal clock used by the system to timestamp image and tracking frames. The returned counter value is given in microseconds since an epoch time. The clock used for the counter itself is implementation-defined, but generally speaking, it is global, monotonic, and makes use of the most accurate high-performance counter available on the system.
### Return value

The time, in microseconds since an unspecified epoch.
## void synchronize ( )
