# Unigine.VREyeTracking Class (CPP)

**Header:** #include <UnigineVREyeTracking.h>

> **Notice:** This class is a singleton.


The class is used for eye tracking management in Varjo devices.


## VREyeTracking Class

### Enums

## STATUS

| Name | Description |
|---|---|
| **STATUS_INVALID** = 0 | Data is not available, user is not wearing the device or eyes cannot be found. |
| **STATUS_ADJUST** = 1 | User is wearing the device, but gaze tracking is being calibrated. |
| **STATUS_VALID** = 2 | Data is valid. |

## EYE_STATUS

| Name | Description |
|---|---|
| **EYE_STATUS_INVALID** = 0 | Eye is not tracked and not visible (for example, eye is shut). |
| **EYE_STATUS_VISIBLE** = 1 | Eye is visible but not reliably tracked (for example, saccade or blink). |
| **EYE_STATUS_COMPENSATED** = 2 | Eye is tracked but quality compromised (for example, headset has moved after calibration). |
| **EYE_STATUS_TRACKED** = 3 | Eye is tracked. |

### Members

## bool isAvailable () const

Returns the current value indicating if eye tracking is available on the active VR device and is supported at runtime.
### Return value

**true** if eye tracking is available; otherwise **false**.
## bool isValid () const

Returns the current value indicating if eye tracking is valid.
### Return value

**true** if eye tracking is valid; otherwise **false**.
## Math:: Vec3 getFocusWorldPosition () const

Returns the current position of the eye focus point in world coordinates.
### Return value

Current world position of the eye focus point.
## Math:: vec3 getGazeWorldDirection () const

Returns the current gaze direction vector, which is a combined value for both eyes, in world coordinates.
### Return value

Current direction vector for both eyes
## Math:: Vec3 getLeftEyeWorldPosition () const

Returns the current position of the left eye in world coordinates.
### Return value

Current world position of the left eye.
## Math:: vec3 getLeftEyeWorldDirection () const

Returns the current direction vector of the left eye in world coordinates.
### Return value

Current direction vector of the left eye.
## float getLeftPupilDiameter () const

Returns the current estimated diameter of the left pupil. The function returns 0.0f if the pupil is not tracked or the estimate is unavailable.
### Return value

Current diameter of the left pupil, in millimeters.
## getLeftPupilIrisDiameterRatio () const

Returns the current ratio between the left pupil diameter estimate and the estimated diameter of the left iris. If either estimate is unavailable, preventing the calculation of the ratio, the function returns 0.0f.
### Return value

Current ratio of the left pupil diameter estimate to the estimated left iris diameter.
## float getLeftIrisDiameter () const

Returns the current an estimated diameter of the left iris. The function returns 0.0f if the estimate is unavailable.
### Return value

Current diameter of the left iris, in millimeters.
## float getLeftOpenness () const

Returns the current estimated openness ratio of the left eye. 1.0f corresponds to a fully open eye, 0.0f to a fully closed eye.
### Return value

Current estimated openness ratio of the left eye in range [0.0f;1.0f].
## VREyeTracking::EYE_STATUS getLeftStatus () const

Returns the current status of the left eye.
### Return value

Current status of the left eye.
## float getRightPupilDiameter () const

Returns the current estimated diameter of the right pupil. The function returns 0.0f if the pupil is not tracked or the estimate is unavailable.
### Return value

Current diameter of the right pupil, in millimeters.
## float getRightPupilIrisDiameterRatio () const

Returns the current ratio between the right pupil diameter estimate and the estimated diameter of the left iris. If either estimate is unavailable, preventing the calculation of the ratio, the function returns 0.0f.
### Return value

Current ratio of the right pupil diameter estimate to the estimated left iris diameter.
## float getRightIrisDiameter () const

Returns the current an estimated diameter of the right iris. The function returns 0.0f if the estimate is unavailable.
### Return value

Current diameter of the right iris, in millimeters.
## float getRightOpenness () const

Returns the current estimated openness ratio of the right eye. 1.0f corresponds to a fully open eye, 0.0f to a fully closed eye.
### Return value

Current estimated openness ratio of the right eye in range [0.0f;1.0f].
## Math:: Vec3 getRightEyeWorldPosition () const

Returns the current position of the right eye in world coordinates.
### Return value

Current world position of the right eye.
## Math:: vec3 getRightEyeWorldDirection () const

Returns the current direction vector of the right eye in world coordinates.
### Return value

Current direction vector of the right eye.
## VREyeTracking::EYE_STATUS getRightStatus () const

Returns the current status of the right eye.
### Return value

Current status of the right eye.
## float getIPD () const

Returns the current interpupillary distance (IPD).
### Return value

Current interpupillary distance.
## long long getCaptureTime () const

Returns the current timestamp of when the data was recorded, in nanoseconds.
### Return value

Current timestamp of when the data was recorded, in nanoseconds.
## double getFocusDistance () const

Returns the current distance between the eye and the focus point. It is a value between 0 and 2> meters.
### Return value

Current distance between the eye and the focus point.
## double getStability () const

Returns the current value specifying the stability of the user's focus. 0.0 means not stable and 1.0 means stable.
### Return value

Current stability of the user's focus in range [0.0;1.0].
## VREyeTracking::STATUS getStatus () const

Returns the current value representing the status of eye tracking in the Varjo headsets.
### Return value

Current value representing the status of eye tracking.
## long long getRawFrame () const

Returns the current unique identifier of the frame when the data was recorded.
### Return value

Current unique identifier of the frame when the data was recorded.
## void setVisualizerEnabled ( bool enabled )

Sets a new value indicating if the visualizer is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable the visualizer; **false** - to disable it.

## bool isVisualizerEnabled () const

Returns the current value indicating if the visualizer is enabled.
### Return value

**true** if the visualizer is enabled ; otherwise **false**.
---

## bool hasFeatureRequestCalibration ( ) const

Returns a value indicating if eye tracking calibration can be requested via the API.
### Return value

true if eye tracking calibration can be requested via the API; otherwise, false.
## bool hasFeaturePupilDiameter ( ) const

Returns a value indicating if pupil diameter data is available.
### Return value

true if pupil diameter data is available; otherwise, false.
## bool hasFeatureIrisDiameter ( ) const

Returns a value indicating if iris diameter data is available.
### Return value

true if iris diameter data is available; otherwise, false.
## bool hasFeaturePupilIrisDiameterRatio ( ) const

Returns a value indicating if the ratio between pupil and iris diameters is available.
### Return value

true if the ratio between pupil and iris diameters is available; otherwise, false.
## bool hasFeatureOpenness ( ) const

Returns a value indicating if eye openness data (e.g., blink state or squinting) is available.
### Return value

true if eye openness data is available; otherwise, false.
## void requestCalibration ( )

Triggers the gaze calibration sequence, if gaze tracking has been enabled in Varjo settings and the Varjo system is in a state where it can bring up the calibration UI.
