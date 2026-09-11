# Unigine::Plugins::UltraleapDevice Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## UltraleapDevice Class

### Members

## int isStatusConnected () const

Returns the current value indicating if the *Ultraleap Controller* device is connected.
### Return value

Current the *Ultraleap Controller* device is connected
## int isStatusStreaming () const

Returns the current value indicating if the *Ultraleap Controller* device is sending out frames.
### Return value

Current the *Ultraleap Controller* device is sending out frames
## int isStatusPaused () const

Returns the current value indicating if the *Ultraleap Controller* device streaming has been paused.
### Return value

Current the *Ultraleap Controller* device streaming has been paused
## int isStatusRobust () const

Returns the current value indicating if the *Ultraleap Controller* device has transitioned to robust mode in order to compensate for known sources of infrared interference.
### Return value

Current the *Ultraleap Controller* device has transitioned to robust mode in order to compensate for known sources of infrared interference
## int isStatusSmudged () const

Returns the current value indicating if the *Ultraleap Controller* device�s window is smudged. If the device�s window is smudged, tracking may be degraded.
### Return value

Current the *Ultraleap Controller* device�s window is smudged
## int isStatusLowResource () const

Returns the current value indicating if the *Ultraleap Controller* device has entered low-resource mode.
### Return value

Current the *Ultraleap Controller* device has entered low-resource mode
## int isStatusUnknownFailure () const

Returns the current value indicating if the *Ultraleap Controller* device has failed, but the failure reason is not known.
### Return value

Current the *Ultraleap Controller* device has failed, but the failure reason is not known
## int isStatusBadCalibration () const

Returns the current value indicating if the *Ultraleap Controller* device has a bad calibration record and cannot send frames.
### Return value

Current the *Ultraleap Controller* device has a bad calibration record and cannot send frames
## int isStatusBadFirmware () const

Returns the current value indicating if the *Ultraleap Controller* device reports corrupt firmware or cannot install a required firmware update.
### Return value

Current the *Ultraleap Controller* device reports corrupt firmware or cannot install a required firmware update
## int isStatusBadTransport () const

Returns the current value indicating if the *Ultraleap Controller* device USB connection is faulty.
### Return value

Current the *Ultraleap Controller* device USB connection is faulty
## int isStatusBadControl () const

Returns the current value indicating if the *Ultraleap Controller* device USB control interfaces failed to initialize.
### Return value

Current the *Ultraleap Controller* device USB control interfaces failed to initialize
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
## int getHardwareType () const

Returns the current recognized type of hardware. One of the [HARDWARE_TYPE_*](#HARDWARE_TYPE_UNKNOWN) values.
### Return value

Current recognized type of hardware
## unsigned int getLeapID () const

Returns the current ID of the current device.
### Return value

Current ID of the current device
## int isSupportedColorImages () const

Returns the current value indicating if color images are supported for this device.
### Return value

Current color images are supported for this device
## int isSupportedAccelerometer () const

Returns the current value indicating if the accelerometer is supported for this device.
### Return value

Current the accelerometer is supported for this device
## int isSupportedGyroscope () const

Returns the current value indicating if the gyroscope is supported for this device.
### Return value

Current the gyroscope is supported for this device
## int isSupportedTemperature () const

Returns the current value indicating if temperature measuring is supported for this device.
### Return value

Current temperature measuring is supported for this device
## vec3 getAccelerometer () const

Returns the current accelerometer measurements, in **m/s^2**.
### Return value

Current accelerometer measurements, **in m/s^2**
## vec3 getGyroscope () const

Returns the current gyroscope measurements, in **rad/s**.
### Return value

Current gyroscope measurements, in **rad/s**
## float getTemperature () const

Returns the current measured temperature, in **deg C**.
### Return value

Current measured temperature, in **deg C**
## void setTrackingOffset ( Vec3 offset )

Sets a new virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Arguments

- *Vec3* **offset** - The virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters

## Vec3 getTrackingOffset () const

Returns the current virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Return value

Current virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value � the offset from the eye level up to the camera level, in meters
## float getTrackingFPS () const

Returns the current number of the tracking frames per second for this device.
### Return value

Current number of the tracking frames per second for this device
## void setTransform ( )

Sets a new transformation matrix for this device.
### Arguments

- **transform** - The transformation matrix for this device

## getTransform () const

Returns the current transformation matrix for this device.
### Return value

Current transformation matrix for this device
## void setTransformMode ( int mode )

Sets a new transform mode for this device.
> **Notice:** If the [HMD VARJO](#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](#TRANSFORM_MODE_MANUAL).


### Arguments

- *int* **mode** - The transform mode for this device

## int getTransformMode () const

Returns the current transform mode for this device.
> **Notice:** If the [HMD VARJO](#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](#TRANSFORM_MODE_MANUAL).


### Return value

Current transform mode for this device
## UltraleapHand getLeftHand () const

Returns the current object for the left hand.
### Return value

Current object for the left hand
## UltraleapHand getRightHand () const

Returns the current object for the right hand.
### Return value

Current object for the right hand
## int isLeftDistortionReceived () const

Returns the current value indicating if the distortion calibration map for the left-eye image has been received.
### Return value

Current the distortion calibration map for the left-eye image has been received
## Image getLeftDistortionImage () const

Returns the current distortion calibration map for the left-eye image.
### Return value

Current distortion calibration map for the left-eye image
## int isLeftColorReceived () const

Returns the current value indicating if the color image for the left eye image has been received.
### Return value

Current the color image for the left eye image has been received
## Image getLeftColorImage () const

Returns the current color image for the left eye.
### Return value

Current color image for the left eye
## int isRightDistortionReceived () const

Returns the current value indicating if the distortion calibration map for the right-eye image has been received.
### Return value

Current the distortion calibration map for the right-eye image has been received
## Image getRightDistortionImage () const

Returns the current distortion calibration map for the right-eye image.
### Return value

Current distortion calibration map for the right-eye image
## int isRightColorReceived () const

Returns the current value indicating if the color image for the right eye image has been received.
### Return value

Current the color image for the right eye image has been received
## Image getRightColorImage () const

Returns the current color image for the right eye.
### Return value

Current color image for the right eye
