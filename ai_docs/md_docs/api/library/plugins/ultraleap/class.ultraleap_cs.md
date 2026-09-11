# Unigine::Plugins::Ultraleap Class (CS)

> **Notice:** This class is a singleton.


## Ultraleap Class

### Enums

## TRACKING_MODE

| Name | Description |
|---|---|
| **DESKTOP** = 0 | The tracking mode optimised for desktop devices. |
| **HMD** = 1 | The tracking mode optimised for head-mounted devices. |
| **SCREEN_TOP** = 2 | The tracking mode optimised for screen top-mounted devices. |
| **UNKNOWN** = 3 | Tracking mode is not known. |

## CONNECTION_STATUS

| Name | Description |
|---|---|
| **NOT_CONNECTED** = 0 | The connection is not open. |
| **CONNECTED** = 1 | The connection is open. |
| **HANDSHAKE_INCOMPLETE** = 2 | Opening the connection is underway, but not complete. |
| **NOT_RUNNING** = -1 | The connection could not be opened because the Ultraleap Tracking Service does not appear to be running. |

## OPTIMIZE_MODE

| Name | Description |
|---|---|
| **DISABLED** = 0 | Tracking optimization is disabled. |
| **AUTO** = 1 | Tracking optimization is set to automatic. |
| **HMD** = 2 | Tracking is optimized for head-mounted devices. The optimize HMD policy improves tracking in situations where the Ultraleap hardware is attached to a head-mounted display. This policy is not granted for devices that cannot be mounted to an HMD, such as Ultraleap controllers embedded in a laptop or keyboard. |
| **SCREEN_TOP** = 3 | Tracking is optimized for screen-top devices. |

### Properties

## bool BackgroundUpdate

The value indicating if the application is allowed to receive frames in the background. By default your UNIGINE application stops rendering frames and updating its main window, when its window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
## bool StreamImages

The value indicating if streaming of images is currently enabled.
## bool Paused

The value indicating if the Ultraleap service is currently paused.
## bool AllowPauseResume

The value indicating if the application is allowed to pause and unpause the Ultraleap service.
## Ultraleap.OPTIMIZE_MODE OptimizeMode

The optimization mode set for tracking. One of the [OPTIMIZE_MODE_*](#OPTIMIZE_MODE_DISABLED) values. Some policies can be denied if the user has disabled the feature on their Ultraleap control panel.
## Ultraleap.TRACKING_MODE TrackingMode

The tracking mode. One of the [TRACKING_MODE_*](#TRACKING_MODE_DESKTOP) values.
## bool TrackingInterpolation

The value indicating if the tracking interpolation is enabled.
## 🔒︎ Ultraleap.CONNECTION_STATUS ConnectionStatus

The status of connection to the Ultraleap daemon/service. One of the [CONNECTION_STATUS_*](#CONNECTION_STATUS_NOT_CONNECTED) values.
## 🔒︎ bool IsStatusLowFPSDetected

The value indicating if the service cannot receive frames fast enough from the underlying hardware.
## 🔒︎ bool IsStatusPoorPerformancePause

The value indicating if the service has paused itself due to an insufficient frame rate from the hardware.
## 🔒︎ bool IsStatusTrackingErrorUnknown

The value indicating if the service has failed to start tracking due to unknown reasons.
## vec3 TrackingOffsetDefault

The virtual offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
## UltraleapDevice.TRANSFORM_MODE TransformModeOffsetDefault

The default transform mode for the offset of a newly connected device.
One of the [TRANSFORM_MODE_*](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cs.md#TRANSFORM_MODE_HMD_VARJO) values. Setting it adjusts the offset to manually match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).


> **Notice:** If the [HMD VARJO](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cs.md#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cs.md#TRANSFORM_MODE_MANUAL).


## 🔒︎ int NumDevices

The total number of recognized devices.
## 🔒︎ int NumDevicesConnected

The number of connected Ultraleap controller devices.
## 🔒︎ long LeapNow

The universal clock value used by the system to timestamp image and tracking frames, in microseconds since an epoch time. The clock used for the counter itself is implementation-defined, but generally speaking, it is global, monotonic, and makes use of the most accurate high-performance counter available on the system.
### Members

---

## UltraleapDevice GetDevice ( int device_id )

Returns the Ultraleap controller device from the list of recognized devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## UltraleapDevice GetDeviceConnected ( int device_id )

Returns the Ultraleap controller device from the list of connected devices.
### Arguments

- *int* **device_id** - The ID of the Ultraleap controller device.

### Return value

The Ultraleap controller device.
## void Synchronize ( )

Synchronizes the internal Ultraleap clock rebaser with the current engine time. This keeps the Ultraleap tracking clock aligned with the engine timeline so that tracking frames are timestamped consistently (used, in particular, for tracking interpolation). In manual (non-VR) mode this is called automatically each frame on the begin render event.
