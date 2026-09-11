# Unigine::Plugins::UltraleapDevice Class (CS)


## UltraleapDevice Class

### Enums

## HARDWARE_TYPE

| Name | Description |
|---|---|
| **UNKNOWN** = 0x0000 | An unknown device that is compatible with the tracking software. |
| **PERIPHERAL** = 0x0003 | The Leap Motion Controller (the first consumer peripheral). |
| **DRAGONFLY** = 0x1102 | Internal research product codename �Dragonfly�. |
| **NIGHTCRAWLER** = 0x1201 | Internal research product codename �Nightcrawler�. |
| **RIGEL** = 0x1202 | Research product codename �Rigel�. |
| **SIR170** = 0x1203 | he Ultraleap Stereo IR 170 (SIR170) hand tracking module. |
| **_3DI** = 0x1204 | The Ultraleap 3Di hand tracking camera. |
| **INVALID** = -1 | An invalid device type. |

## TRANSFORM_MODE

| Name | Description |
|---|---|
| **HMD_VARJO** = 0 | HMD Pose from AppVarjo and the *[IModelView](../../../../api/library/rendering/class.camera_cs.md#getIModelview_Mat4)* from *[Game::getPlayer()](../../../../api/library/engine/class.game_cs.md#getPlayer_Player)* are used for transform. |
| **MANUAL** = 1 | The user manually [sets the transform matrix](#setTransform_Mat4_void) as described for the [Ultraleap Coordinate System](../../../../code/plugins/ultraleap/index_cs.md#coordinate_system). |

### Properties

## 🔒︎ bool IsStatusConnected

The value indicating if the *Ultraleap Controller* device is connected.
## 🔒︎ bool IsStatusStreaming

The value indicating if the *Ultraleap Controller* device is sending out frames.
## 🔒︎ bool IsStatusPaused

The value indicating if the *Ultraleap Controller* device streaming has been paused.
## 🔒︎ bool IsStatusRobust

The value indicating if the *Ultraleap Controller* device has transitioned to robust mode in order to compensate for known sources of infrared interference.
## 🔒︎ bool IsStatusSmudged

The value indicating if the *Ultraleap Controller* device�s window is smudged. If the device�s window is smudged, tracking may be degraded.
## 🔒︎ bool IsStatusLowResource

The value indicating if the *Ultraleap Controller* device has entered low-resource mode.
## 🔒︎ bool IsStatusUnknownFailure

The value indicating if the *Ultraleap Controller* device has failed, but the failure reason is not known.
## 🔒︎ bool IsStatusBadCalibration

The value indicating if the *Ultraleap Controller* device has a bad calibration record and cannot send frames.
## 🔒︎ bool IsStatusBadFirmware

The value indicating if the *Ultraleap Controller* device reports corrupt firmware or cannot install a required firmware update.
## 🔒︎ bool IsStatusBadTransport

The value indicating if the *Ultraleap Controller* device USB connection is faulty.
## 🔒︎ bool IsStatusBadControl

The value indicating if the *Ultraleap Controller* device USB control interfaces failed to initialize.
## 🔒︎ string Serial

The device serial number.
## 🔒︎ float HFov

The horizontal field of view of this device in **radians**.
## 🔒︎ float VFov

The vertical field of view of this device in **radians**.
## 🔒︎ double Range

The maximum range for this device, in **meters**.
## 🔒︎ double DistanceBetweenCameras

The distance between the Ultraleap cameras, in meters.
## 🔒︎ UltraleapDevice.HARDWARE_TYPE HardwareType

The recognized type of hardware. One of the [HARDWARE_TYPE_*](#HARDWARE_TYPE_UNKNOWN) values.
## 🔒︎ uint LeapID

The ID of the current device.
## 🔒︎ bool IsSupportedColorImages

The value indicating if color images are supported for this device.
## 🔒︎ bool IsSupportedAccelerometer

The value indicating if the accelerometer is supported for this device.
## 🔒︎ bool IsSupportedGyroscope

The value indicating if the gyroscope is supported for this device.
## 🔒︎ bool IsSupportedTemperature

The value indicating if temperature measuring is supported for this device.
## 🔒︎ vec3 Accelerometer

The accelerometer measurements, in **m/s^2**.
## 🔒︎ vec3 Gyroscope

The gyroscope measurements, in **rad/s**.
## 🔒︎ float Temperature

The measured temperature, in **deg C**.
## vec3 TrackingOffset

The virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
## 🔒︎ float TrackingFPS

The number of the tracking frames per second for this device.
## mat4 Transform

The transformation matrix for this device.
## UltraleapDevice.TRANSFORM_MODE TransformMode

The transform mode for this device.
> **Notice:** If the [HMD VARJO](#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](#TRANSFORM_MODE_MANUAL).


## 🔒︎ UltraleapHand LeftHand

The object for the left hand.
## 🔒︎ UltraleapHand RightHand

The object for the right hand.
## 🔒︎ bool IsLeftDistortionReceived

The value indicating if the distortion calibration map for the left-eye image has been received.
## 🔒︎ Image LeftDistortionImage

The distortion calibration map for the left-eye image.
## 🔒︎ bool IsLeftColorReceived

The value indicating if the color image for the left eye image has been received.
## 🔒︎ Image LeftColorImage

The color image for the left eye.
## 🔒︎ bool IsRightDistortionReceived

The value indicating if the distortion calibration map for the right-eye image has been received.
## 🔒︎ Image RightDistortionImage

The distortion calibration map for the right-eye image.
## 🔒︎ bool IsRightColorReceived

The value indicating if the color image for the right eye image has been received.
## 🔒︎ Image RightColorImage

The color image for the right eye.
