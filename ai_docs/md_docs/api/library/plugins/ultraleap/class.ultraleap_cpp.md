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

## void setBackgroundUpdate ( bool update )

Sets a new value indicating if the application is allowed to receive frames in the background. By default your UNIGINE application stops rendering frames and updating its main window, when its window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Arguments

- *bool* **update** - Set **true** to enable the application is allowed to receive frames in the background; **false** - to disable it.

## bool isBackgroundUpdate () const

Returns the current value indicating if the application is allowed to receive frames in the background. By default your UNIGINE application stops rendering frames and updating its main window, when its window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Return value

**true** if the application is allowed to receive frames in the background; otherwise **false**.
## void setStreamImages ( bool images )

Sets a new value indicating if streaming of images is currently enabled.
### Arguments

- *bool* **images** - Set **true** to enable streaming of images is currently enabled; **false** - to disable it.

## bool isStreamImages () const

Returns the current value indicating if streaming of images is currently enabled.
### Return value

**true** if streaming of images is currently enabled; otherwise **false**.
## void setPaused ( bool paused )

Sets a new value indicating if the Ultraleap service is currently paused.
### Arguments

- *bool* **paused** - Set **true** to enable the Ultraleap service is currently paused; **false** - to disable it.

## bool isPaused () const

Returns the current value indicating if the Ultraleap service is currently paused.
### Return value

**true** if the Ultraleap service is currently paused; otherwise **false**.
## void setAllowPauseResume ( bool resume )

Sets a new value indicating if the application is allowed to pause and unpause the Ultraleap service.
### Arguments

- *bool* **resume** - Set **true** to enable the application is allowed to pause and unpause the Ultraleap service; **false** - to disable it.

## bool isAllowPauseResume () const

Returns the current value indicating if the application is allowed to pause and unpause the Ultraleap service.
### Return value

**true** if the application is allowed to pause and unpause the Ultraleap service; otherwise **false**.
## void setOptimizeMode ( Ultraleap::OPTIMIZE_MODE mode )

Sets a new optimization mode set for tracking. One of the [OPTIMIZE_MODE_*](#OPTIMIZE_MODE_DISABLED) values. Some policies can be denied if the user has disabled the feature on their Ultraleap control panel.
### Arguments

- *[Ultraleap::OPTIMIZE_MODE](../../../../api/library/plugins/ultraleap/class.ultraleap_cpp.md#OPTIMIZE_MODE)* **mode** - The optimization mode set for tracking

## Ultraleap::OPTIMIZE_MODE getOptimizeMode () const

Returns the current optimization mode set for tracking. One of the [OPTIMIZE_MODE_*](#OPTIMIZE_MODE_DISABLED) values. Some policies can be denied if the user has disabled the feature on their Ultraleap control panel.
### Return value

Current optimization mode set for tracking
## void setTrackingMode ( Ultraleap::TRACKING_MODE mode )

Sets a new tracking mode. One of the [TRACKING_MODE_*](#TRACKING_MODE_DESKTOP) values.
### Arguments

- *[Ultraleap::TRACKING_MODE](../../../../api/library/plugins/ultraleap/class.ultraleap_cpp.md#TRACKING_MODE)* **mode** - The tracking mode

## Ultraleap::TRACKING_MODE getTrackingMode () const

Returns the current tracking mode. One of the [TRACKING_MODE_*](#TRACKING_MODE_DESKTOP) values.
### Return value

Current tracking mode
## void setTrackingInterpolation ( bool interpolation )

Sets a new value indicating if the tracking interpolation is enabled.
### Arguments

- *bool* **interpolation** - Set **true** to enable the tracking interpolation is enabled; **false** - to disable it.

## bool isTrackingInterpolation () const

Returns the current value indicating if the tracking interpolation is enabled.
### Return value

**true** if the tracking interpolation is enabled; otherwise **false**.
## Ultraleap::CONNECTION_STATUS getConnectionStatus () const

Returns the current status of connection to the Ultraleap daemon/service. One of the [CONNECTION_STATUS_*](#CONNECTION_STATUS_NOT_CONNECTED) values.
### Return value

Current status of connection to the Ultraleap daemon/service
## bool isStatusLowFPSDetected () const

Returns the current value indicating if the service cannot receive frames fast enough from the underlying hardware.
### Return value

**true** if the service cannot receive frames fast enough from the underlying hardware; otherwise **false**.
## bool isStatusPoorPerformancePause () const

Returns the current value indicating if the service has paused itself due to an insufficient frame rate from the hardware.
### Return value

**true** if the service has paused itself due to an insufficient frame rate from the hardware; otherwise **false**.
## bool isStatusTrackingErrorUnknown () const

Returns the current value indicating if the service has failed to start tracking due to unknown reasons.
### Return value

**true** if the service has failed to start tracking due to unknown reasons; otherwise **false**.
## void setTrackingOffsetDefault ( const Math:: Vec3 & default )

Sets a new virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md)&* **default** - The virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters

## Math:: Vec3 getTrackingOffsetDefault () const

Returns the current virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Return value

Current virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters
## void setTransformModeOffsetDefault ( UltraleapDevice::TRANSFORM_MODE default )

Sets a new default transform mode for the offset of a newly connected device.
One of the [TRANSFORM_MODE_*](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_HMD_VARJO) values. Setting it adjusts the offset to manually match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).


> **Notice:** If the [HMD VARJO](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_MANUAL).


### Arguments

- *[UltraleapDevice::TRANSFORM_MODE](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE)* **default** - The default transform mode for the offset of a newly connected device

## UltraleapDevice::TRANSFORM_MODE getTransformModeOffsetDefault () const

Returns the current default transform mode for the offset of a newly connected device.
One of the [TRANSFORM_MODE_*](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_HMD_VARJO) values. Setting it adjusts the offset to manually match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).


> **Notice:** If the [HMD VARJO](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE_MANUAL).


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
## long long getLeapNow () const

Returns the current universal clock value used by the system to timestamp image and tracking frames, in microseconds since an epoch time. The clock used for the counter itself is implementation-defined, but generally speaking, it is global, monotonic, and makes use of the most accurate high-performance counter available on the system.
### Return value

Current universal clock value, in microseconds since an unspecified epoch
---

## UltraleapDevice * getDevice ( int device_id ) const

Returns the Ultraleap controller device from the list of recognized devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## UltraleapDevice * getDeviceConnected ( int device_id ) const

Returns the Ultraleap controller device from the list of connected devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## void synchronize ( ) const

Synchronizes the internal Ultraleap clock rebaser with the current engine time. This keeps the Ultraleap tracking clock aligned with the engine timeline so that tracking frames are timestamped consistently (used, in particular, for tracking interpolation). In manual (non-VR) mode this is called automatically each frame on the begin render event.
