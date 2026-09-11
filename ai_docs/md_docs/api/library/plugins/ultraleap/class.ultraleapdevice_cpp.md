# Unigine::Plugins::UltraleapDevice Class (CPP)

**Header:** #include <plugins/Unigine/Ultraleap/UnigineUltraleap.h>


## UltraleapDevice Class

### Enums

## HARDWARE_TYPE

| Name | Description |
|---|---|
| **HARDWARE_TYPE_UNKNOWN** = 0x0000 | An unknown device that is compatible with the tracking software. |
| **HARDWARE_TYPE_PERIPHERAL** = 0x0003 | The Leap Motion Controller (the first consumer peripheral). |
| **HARDWARE_TYPE_DRAGONFLY** = 0x1102 | Internal research product codename �Dragonfly�. |
| **HARDWARE_TYPE_NIGHTCRAWLER** = 0x1201 | Internal research product codename �Nightcrawler�. |
| **HARDWARE_TYPE_RIGEL** = 0x1202 | Research product codename �Rigel�. |
| **HARDWARE_TYPE_SIR170** = 0x1203 | he Ultraleap Stereo IR 170 (SIR170) hand tracking module. |
| **HARDWARE_TYPE__3DI** = 0x1204 | The Ultraleap 3Di hand tracking camera. |
| **HARDWARE_TYPE_INVALID** = -1 | An invalid device type. |

## TRANSFORM_MODE

| Name | Description |
|---|---|
| **TRANSFORM_MODE_HMD_VARJO** = 0 | HMD Pose from AppVarjo and the *[IModelView](../../../../api/library/rendering/class.camera_cpp.md#getIModelview_Mat4)* from *[Game::getPlayer()](../../../../api/library/engine/class.game_cpp.md#getPlayer_Player)* are used for transform. |
| **TRANSFORM_MODE_MANUAL** = 1 | The user manually [sets the transform matrix](#setTransform_Mat4_void) as described for the [Ultraleap Coordinate System](../../../../code/plugins/ultraleap/index_cpp.md#coordinate_system). |

### Members

## bool isStatusConnected () const

Returns the current value indicating if the *Ultraleap Controller* device is connected.
### Return value

**true** if the *Ultraleap Controller* device is connected; otherwise **false**.
## bool isStatusStreaming () const

Returns the current value indicating if the *Ultraleap Controller* device is sending out frames.
### Return value

**true** if the *Ultraleap Controller* device is sending out frames; otherwise **false**.
## bool isStatusPaused () const

Returns the current value indicating if the *Ultraleap Controller* device streaming has been paused.
### Return value

**true** if the *Ultraleap Controller* device streaming has been paused; otherwise **false**.
## bool isStatusRobust () const

Returns the current value indicating if the *Ultraleap Controller* device has transitioned to robust mode in order to compensate for known sources of infrared interference.
### Return value

**true** if the *Ultraleap Controller* device has transitioned to robust mode in order to compensate for known sources of infrared interference; otherwise **false**.
## bool isStatusSmudged () const

Returns the current value indicating if the *Ultraleap Controller* device�s window is smudged. If the device�s window is smudged, tracking may be degraded.
### Return value

**true** if the *Ultraleap Controller* device�s window is smudged; otherwise **false**.
## bool isStatusLowResource () const

Returns the current value indicating if the *Ultraleap Controller* device has entered low-resource mode.
### Return value

**true** if the *Ultraleap Controller* device has entered low-resource mode; otherwise **false**.
## bool isStatusUnknownFailure () const

Returns the current value indicating if the *Ultraleap Controller* device has failed, but the failure reason is not known.
### Return value

**true** if the *Ultraleap Controller* device has failed, but the failure reason is not known; otherwise **false**.
## bool isStatusBadCalibration () const

Returns the current value indicating if the *Ultraleap Controller* device has a bad calibration record and cannot send frames.
### Return value

**true** if the *Ultraleap Controller* device has a bad calibration record and cannot send frames; otherwise **false**.
## bool isStatusBadFirmware () const

Returns the current value indicating if the *Ultraleap Controller* device reports corrupt firmware or cannot install a required firmware update.
### Return value

**true** if the *Ultraleap Controller* device reports corrupt firmware or cannot install a required firmware update; otherwise **false**.
## bool isStatusBadTransport () const

Returns the current value indicating if the *Ultraleap Controller* device USB connection is faulty.
### Return value

**true** if the *Ultraleap Controller* device USB connection is faulty; otherwise **false**.
## bool isStatusBadControl () const

Returns the current value indicating if the *Ultraleap Controller* device USB control interfaces failed to initialize.
### Return value

**true** if the *Ultraleap Controller* device USB control interfaces failed to initialize; otherwise **false**.
## String getSerial () const

Returns the current device serial number.
### Return value

Current device serial number
## float getHFov () const

Returns the current horizontal field of view of this device in **radians**.
### Return value

Current horizontal field of view of this device in **radians**
## float getVFov () const

Returns the current vertical field of view of this device in **radians**.
### Return value

Current vertical field of view of this device in **radians**
## double getRange () const

Returns the current maximum range for this device, in **meters**.
### Return value

Current maximum range for this device, in **meters**
## double getDistanceBetweenCameras () const

Returns the current distance between the Ultraleap cameras, in meters.
### Return value

Current distance between the Ultraleap cameras, in meters
## UltraleapDevice::HARDWARE_TYPE getHardwareType () const

Returns the current recognized type of hardware. One of the [HARDWARE_TYPE_*](#HARDWARE_TYPE_UNKNOWN) values.
### Return value

Current recognized type of hardware
## unsigned int getLeapID () const

Returns the current ID of the current device.
### Return value

Current ID of the current device
## bool isSupportedColorImages () const

Returns the current value indicating if color images are supported for this device.
### Return value

**true** if color images are supported for this device; otherwise **false**.
## bool isSupportedAccelerometer () const

Returns the current value indicating if the accelerometer is supported for this device.
### Return value

**true** if the accelerometer is supported for this device; otherwise **false**.
## bool isSupportedGyroscope () const

Returns the current value indicating if the gyroscope is supported for this device.
### Return value

**true** if the gyroscope is supported for this device; otherwise **false**.
## bool isSupportedTemperature () const

Returns the current value indicating if temperature measuring is supported for this device.
### Return value

**true** if temperature measuring is supported for this device; otherwise **false**.
## Math:: vec3 getAccelerometer () const

Returns the current accelerometer measurements, in **m/s^2**.
### Return value

Current accelerometer measurements, **in m/s^2**
## Math:: vec3 getGyroscope () const

Returns the current gyroscope measurements, in **rad/s**.
### Return value

Current gyroscope measurements, in **rad/s**
## float getTemperature () const

Returns the current measured temperature, in **deg C**.
### Return value

Current measured temperature, in **deg C**
## void setTrackingOffset ( const Math:: Vec3 & offset )

Sets a new virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md)&* **offset** - The virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters

## Math:: Vec3 getTrackingOffset () const

Returns the current virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Return value

Current virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters
## float getTrackingFPS () const

Returns the current number of the tracking frames per second for this device.
### Return value

Current number of the tracking frames per second for this device
## void setTransform ( const Math:: Mat4 & transform )

Sets a new transformation matrix for this device.
### Arguments

- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md)&* **transform** - The transformation matrix for this device

## Math:: Mat4 getTransform () const

Returns the current transformation matrix for this device.
### Return value

Current transformation matrix for this device
## void setTransformMode ( UltraleapDevice::TRANSFORM_MODE mode )

Sets a new transform mode for this device.
> **Notice:** If the [HMD VARJO](#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](#TRANSFORM_MODE_MANUAL).


### Arguments

- *[UltraleapDevice::TRANSFORM_MODE](../../../../api/library/plugins/ultraleap/class.ultraleapdevice_cpp.md#TRANSFORM_MODE)* **mode** - The transform mode for this device

## UltraleapDevice::TRANSFORM_MODE getTransformMode () const

Returns the current transform mode for this device.
> **Notice:** If the [HMD VARJO](#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](#TRANSFORM_MODE_MANUAL).


### Return value

Current transform mode for this device
## UltraleapHand * getLeftHand () const

Returns the current object for the left hand.
### Return value

Current object for the left hand
## UltraleapHand * getRightHand () const

Returns the current object for the right hand.
### Return value

Current object for the right hand
## bool isLeftDistortionReceived () const

Returns the current value indicating if the distortion calibration map for the left-eye image has been received.
### Return value

**true** if the distortion calibration map for the left-eye image has been received; otherwise **false**.
## Ptr < Image > getLeftDistortionImage () const

Returns the current distortion calibration map for the left-eye image.
### Return value

Current distortion calibration map for the left-eye image
## bool isLeftColorReceived () const

Returns the current value indicating if the color image for the left eye image has been received.
### Return value

**true** if the color image for the left eye image has been received; otherwise **false**.
## Ptr < Image > getLeftColorImage () const

Returns the current color image for the left eye.
### Return value

Current color image for the left eye
## bool isRightDistortionReceived () const

Returns the current value indicating if the distortion calibration map for the right-eye image has been received.
### Return value

**true** if the distortion calibration map for the right-eye image has been received; otherwise **false**.
## Ptr < Image > getRightDistortionImage () const

Returns the current distortion calibration map for the right-eye image.
### Return value

Current distortion calibration map for the right-eye image
## bool isRightColorReceived () const

Returns the current value indicating if the color image for the right eye image has been received.
### Return value

**true** if the color image for the right eye image has been received; otherwise **false**.
## Ptr < Image > getRightColorImage () const

Returns the current color image for the right eye.
### Return value

Current color image for the right eye
