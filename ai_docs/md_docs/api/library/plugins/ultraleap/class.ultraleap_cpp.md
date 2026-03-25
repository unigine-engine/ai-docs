# Unigine::Plugins::Ultraleap Class (CPP)

**Header:** #include <plugins/Unigine/Ultraleap/UnigineUltraleap.h>

> **Notice:** This class is a singleton.


## Ultraleap Class

### Enums

## TRACKING_MODE

| Name | Description |
|---|---|
| **TRACKING_MODE_DESKTOP** = 0 | The tracking mode optimised for desktop devices. |
| **TRACKING_MODE_HMD** = 1 | The tracking mode optimised for head-mounted devices. |
| **TRACKING_MODE_SCREEN_TOP** = 2 | The tracking mode optimised for screen top-mounted devices. |
| **TRACKING_MODE_UNKNOWN** = 3 | Tracking mode is not known. |

## CONNECTION_STATUS

| Name | Description |
|---|---|
| **CONNECTION_STATUS_NOT_CONNECTED** = 0 | The connection is not open. |
| **CONNECTION_STATUS_CONNECTED** = 1 | The connection is open. |
| **CONNECTION_STATUS_HANDSHAKE_INCOMPLETE** = 2 | Opening the connection is underway, but not complete. |
| **CONNECTION_STATUS_NOT_RUNNING** = -1 | The connection could not be opened because the Ultraleap Tracking Service does not appear to be running. |

## OPTIMIZE_MODE

| Name | Description |
|---|---|
| **OPTIMIZE_MODE_DISABLED** = 0 | Tracking optimization is disabled. |
| **OPTIMIZE_MODE_AUTO** = 1 | Tracking optimization is set to automatic. |
| **OPTIMIZE_MODE_HMD** = 2 | Tracking is optimized for head-mounted devices. The optimize HMD policy improves tracking in situations where the Ultraleap hardware is attached to a head-mounted display. This policy is not granted for devices that cannot be mounted to an HMD, such as Ultraleap controllers embedded in a laptop or keyboard. |
| **OPTIMIZE_MODE_SCREEN_TOP** = 3 | Tracking is optimized for screen-top devices. |

### Members

---

## void setBackgroundUpdate ( bool update )

Sets the value indicating whether the application is allowed to receive frames in the background. By default your UNIGINE application stops rendering frames and updating its main window, when it window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Arguments

- *bool* **update** - The window update mode: true for constantly repeating update cycle (i.e. the application is updated even if the window is hidden or out of focus); otherwise, false.

## bool isBackgroundUpdate ( ) const

Returns a value indicating whether the application is allowed to receive frames in the background.
### Return value

**true** if the update cycle is constantly repeated (i.e. the application is updated even if the window is hidden or out of focus); otherwise, **false**.
## void setStreamImages ( bool images )

Enables or disables streaming of images.
### Arguments

- *bool* **images** - true - to enable streaming of images; false - to disable it.

## bool isStreamImages ( ) const

Returns a value indicating if streaming of images is currently enabled.
### Return value

true if streaming of images is currently enabled; otherwise, false.
## void setPaused ( bool paused )

Pauses or resumes the Ultraleap service.
### Arguments

- *bool* **paused** - true - to pause the Ultraleap service; false - to resume it.

## bool isPaused ( ) const

Returns a value indicating if the Ultraleap service is currently paused.
### Return value

true if the Ultraleap service is currently paused; otherwise, false.
## void setAllowPauseResume ( bool resume )

Allows the application to pause and unpause the Ultraleap service.
### Arguments

- *bool* **resume** - true — to allow the application pause and unpause the Ultraleap service; otherwise, false.

## bool isAllowPauseResume ( ) const

Returns a value indicating if the application is allowed to pause and unpause the Ultraleap service.
### Return value

true if the application is allowed to pause and unpause the Ultraleap service; otherwise, false.
## void setOptimizeMode ( Ultraleap::OPTIMIZE_MODE mode )

Sets an optimization mode for tracking. Some policies can be denied if the user has disabled the feature on their Ultraleap control panel.
### Arguments

- *[Ultraleap::OPTIMIZE_MODE](../../../../api/library/plugins/ultraleap/class.ultraleap_cpp.md#OPTIMIZE_MODE)* **mode** - The optimization mode. One of the [UltraleapFinger::OPTIMIZE_MODE_*](#OPTIMIZE_MODE_DISABLED) values.

## Ultraleap::OPTIMIZE_MODE getOptimizeMode ( ) const

Returns the current optimization mode set for tracking.
### Return value

The optimization mode. One of the [OPTIMIZE_MODE_*](#OPTIMIZE_MODE_DISABLED) values.
## void setTrackingMode ( Ultraleap::TRACKING_MODE mode )

Sets the tracking mode.
### Arguments

- *[Ultraleap::TRACKING_MODE](../../../../api/library/plugins/ultraleap/class.ultraleap_cpp.md#TRACKING_MODE)* **mode** - The tracking mode. One of the [TRACKING_MODE_*](#TRACKING_MODE_DESKTOP) values.

## Ultraleap::TRACKING_MODE getTrackingMode ( ) const

Returns the current tracking mode.
### Return value

The tracking mode. One of the [TRACKING_MODE_*](#TRACKING_MODE_DESKTOP) values.
## void setTrackingInterpolation ( bool interpolation )

Toggles the tracking interpolation on and off.
### Arguments

- *bool* **interpolation** - true — to enable the tracking interpolation; otherwise, false.

## bool isTrackingInterpolation ( ) const

Returns the value indicating if the tracking interpolation is enabled.
### Return value

true if the tracking interpolation is enabled; otherwise, false.
## Ultraleap::CONNECTION_STATUS getConnectionStatus ( ) const

Retuns the status of connection to the Ultraleap daemon/service.
### Return value

The connection status. One of the [CONNECTION_STATUS_*](#CONNECTION_STATUS_NOT_CONNECTED) values.
## bool isStatusLowFPSDetected ( ) const

Returns the value indicating if the service cannot receive frames fast enough from the underlying hardware.
### Return value

true if the service cannot receive frames fast enough from the underlying hardware; otherwise, false.
## bool isStatusPoorPerformancePause ( ) const

Returns the value indicating if the service has paused itself due to an insufficient frame rate from the hardware.
### Return value

true if the service has paused itself due to an insufficient frame rate from the hardware; otherwise, false.
## bool isStatusTrackingErrorUnknown ( ) const

Returns the value indicating if the service has failed to start tracking due to unknown reasons.
### Return value

true if the service has failed to start tracking due to unknown reasons; otherwise, false.
## void setTrackingOffsetDefault ( const Math::Vec3& val )

Sets the default offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Arguments

- *const  Math::Vec3&* **val** - The the default offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).

## Math:: Vec3 getTrackingOffsetDefault ( ) const

Returns the current virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters.
### Return value

The default offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters.
## void setTransformModeOffsetDefault ( UltraleapDevice::TRANSFORM_MODE val )

Sets the offset to manually adjust the specified transform mode. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
> **Notice:** If the [HMD VARJO](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_MANUAL).


### Arguments

- *[UltraleapDevice::TRANSFORM_MODE](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE)* **val** - Transform mode. One of the [TRANSFORM_MODE*](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_HMD_VARJO) values.

## UltraleapDevice::TRANSFORM_MODE getTransformModeOffsetDefault ( ) const

Returns the default transform mode for the offset of a newly connected device.
### Return value

The transform mode. One of the [TRANSFORM_MODE*](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_HMD_VARJO) values.
## int getNumDevices ( ) const

Returns the total number of recognized devices.
### Return value

The number of connected devices.
## UltraleapDevice * getDevice ( int device_id ) const

Returns the Ultraleap controller device from the list of recognized devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## int getNumDevicesConnected ( ) const

Returns the number of connected Ultraleap controller devices.
### Return value

The number of connected Ultraleap controller devices.
## UltraleapDevice * getDeviceConnected ( int device_id ) const

Returns the Ultraleap controller device from the list of connected devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## long long getLeapNow ( ) const

Samples the universal clock used by the system to timestamp image and tracking frames. The returned counter value is given in microseconds since an epoch time. The clock used for the counter itself is implementation-defined, but generally speaking, it is global, monotonic, and makes use of the most accurate high-performance counter available on the system.
### Return value

The time, in microseconds since an unspecified epoch.
## void synchronize ( ) const
