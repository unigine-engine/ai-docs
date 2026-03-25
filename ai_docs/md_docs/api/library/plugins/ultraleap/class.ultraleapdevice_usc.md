# Unigine::Plugins::UltraleapDevice Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## UltraleapDevice Class

### Members

---

## int isStatusConnected ( )

Returns a value indicating if the Ultraleap Controller device is connected.
### Return value

**1** if the device is connected; otherwise, **0**.
## int isStatusStreaming ( )

Returns a value indicating if the Ultraleap Controller device is sending out frames.
### Return value

**1** if the device is sending out frames; otherwise, **0**.
## int isStatusPaused ( )

Returns a value indicating if the Ultraleap Controller device streaming has been paused.
### Return value

**1** if the device streaming has been paused; otherwise, **0**.
## int isStatusRobust ( )

Returns a value indicating if the Ultraleap Controller device has transitioned to robust mode in order to compensate for known sources of infrared interference.
### Return value

**1** if the device has transitioned to robust mode in order to compensate; otherwise, **0**.
## int isStatusSmudged ( )

Returns a value indicating if the Ultraleap Controller device’s window is smudged. If the device’s window is smudged, tracking may be degraded.
### Return value

**1** if the device’s window is smudged; otherwise, **0**.
## int isStatusLowResource ( )

Returns a value indicating if the Ultraleap Controller device has entered low-resource mode.
### Return value

**1** if the device has entered low-resource mode; otherwise, **0**.
## int isStatusUnknownFailure ( )

Returns a value indicating if the Ultraleap Controller device has failed, but the failure reason is not known.
### Return value

**1** if the device has failed, but the failure reason is not known; otherwise, **0**.
## int isStatusBadCalibration ( )

Returns a value indicating if the Ultraleap Controller device has a bad calibration record and cannot send frames.
### Return value

**1** if the device has a bad calibration record and cannot send frames; otherwise, **0**.
## int isStatusBadFirmware ( )

Returns a value indicating if the Ultraleap Controller device reports corrupt firmware or cannot install a required firmware update.
### Return value

**1** if the device reports corrupt firmware or cannot install a required firmware update; otherwise, **0**.
## int isStatusBadTransport ( )

Returns a value indicating if the Ultraleap Controller device USB connection is faulty.
### Return value

**1** if the device USB connection is faulty; otherwise, **0**.
## int isStatusBadControl ( )

Returns a value indicating if the Ultraleap Controller device USB control interfaces failed to initialize.
### Return value

**1** if the device USB control interfaces failed to initialize; otherwise, **0**.
## String getSerial ( )

Returns the device serial number.
### Return value

The device serial number.
## float getHFov ( )

Returns the horizontal field of view of this device in **radians**.
### Return value

The horizontal field of view of this device in **radians**.
## float getVFov ( )

Returns the vertical field of view of this device in **radians**.
### Return value

The vertical field of view of this device in **radians**.
## double getRange ( )

Returns the maximum range for this device, in **meters**.
### Return value

The maximum range for this device, in **meters**.
## double getDistanceBetweenCameras ( )

Returns the distance between the Ultraleap cameras, in meters.
### Return value

The distance between the Ultraleap cameras, in meters.
## int getHardwareType ( )

Returns the recognized type of hardware.
### Return value

The hardware type. One of the [ULTRALEAP_HARDWARE_TYPE_*](#HARDWARE_TYPE_UNKNOWN) values.
## unsigned int getLeapID ( )

Returns the ID of the current device.
### Return value

The device ID.
## int isSupportedColorImages ( )

Returns the value indicating if color images are supported for this device.
### Return value

**1** if color images are supported for this device; otherwise, **0**.
## int isSupportedAccelerometer ( )

Returns the value indicating if the accelerometer is supported for this device.
### Return value

**1** if the accelerometer is supported for this device; otherwise, **0**.
## int isSupportedGyroscope ( )

Returns the value indicating if the gyroscope is supported for this device.
### Return value

**1** if the gyroscope is supported for this device; otherwise, **0**.
## int isSupportedTemperature ( )

Returns the value indicating if temperature measuring is supported for this device.
### Return value

**1** if temperature measuring is supported for this device; otherwise, **0**.
## vec3 getAccelerometer ( )

Returns the accelerometer measurements, in **in m/s^2**.
### Return value

The accelerometer measurements, **in m/s^2**.
## vec3 getGyroscope ( )

Returns the gyroscope measurements, in **rad/s**.
### Return value

The gyroscope measurements, in **rad/s**.
## float getTemperature ( )

Returns the measured temperature, in **deg C**.
### Return value

The measured temperature, in **deg C**.
## void setTrackingOffset ( Vec3 offset )

Sets the default offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters. The X value should be set to 0. These settings can be used to match the physical position and orientation of the Tracking Hardware on a tracked device it is mounted on (such as a VR headset).
### Arguments

- *Vec3* **offset** - The default offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters. The X value should be set to 0.

## Vec3 getTrackingOffset ( )

Returns the current virtual offset of the tracking device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters.
### Return value

The default offset for the newly connected device. The Y value specifies the offset from the eyes to the frontal camera plane, in meters, and the Z value — the offset from the eye level up to the camera level, in meters. The X value should be set to 0.
## float getTrackingFPS ( )

Returns the number of the tracking frames per second for this device.
### Return value

The tracking FPS value.
## void setTransform ( Mat4 transform )

Sets the transformation matrix for this device.
### Arguments

- *Mat4* **transform** - The transformation matrix.

## Mat4 getTransform ( )

Returns the current transformation matrix for this device.
### Return value

The transformation matrix.
## void setTransformMode ( int mode )

Sets the transform mode for this device.
> **Notice:** If the [HMD VARJO](#TRANSFORM_MODE_HMD_VARJO) transform mode has been set, but AppVarjo hasn't been found, the transform mode is switched to [MANUAL](#TRANSFORM_MODE_MANUAL).


### Arguments

- *int* **mode** - The transform mode. One of the [ULTRALEAP_TRANSFORM_MODE_*](#TRANSFORM_MODE_HMD_VARJO) values.

## int getTransformMode ( )

Returns the current transform mode for this device.
### Return value

The transform mode. One of the [ULTRALEAP_TRANSFORM_MODE_*](#TRANSFORM_MODE_HMD_VARJO) values.
## UltraleapHand getLeftHand ( )

Returns the object for the left hand.
### Return value

The object for the left hand.
## UltraleapHand getRightHand ( )

Returns the object for the right hand.
### Return value

The object for the right hand.
## int isLeftDistortionReceived ( )

Returns a value indicating if the distortion calibration map for the left-eye image has been received.
### Return value

**1** if the distortion calibration map for the left-eye image has been received; otherwise, **0**.
## Image getLeftDistortionImage ( )

Returns the distortion calibration map for the left-eye image.
### Return value

The distortion calibration map for the left-eye image.
## int isLeftColorReceived ( )

Returns a value indicating if the color image for the left eye image has been received.
### Return value

**1** if the color image for the left eye image has been received; otherwise, **0**.
## Image getLeftColorImage ( )

Returns the color image for the left eye.
### Return value

The color image for the left eye.
## int isRightDistortionReceived ( )

Returns a value indicating if the distortion calibration map for the right-eye image has been received.
### Return value

**1** if the distortion calibration map for the right-eye image has been received; otherwise, **0**.
## Image getRightDistortionImage ( )

Returns the distortion calibration map for the right-eye image.
### Return value

The distortion calibration map for the right-eye image.
## int isRightColorReceived ( )

Returns a value indicating if the color image for the right eye image has been received.
### Return value

**1** if the color image for the right eye image has been received; otherwise, **0**.
## Image getRightColorImage ( )

Returns the color image for the right eye.
### Return value

The color image for the right eye.
