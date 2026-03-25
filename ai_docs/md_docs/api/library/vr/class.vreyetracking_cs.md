# Unigine.VREyeTracking Class (CS)

> **Notice:** This class is a singleton.


The class is used for eye tracking management in Varjo devices.


## VREyeTracking Class

### Enums

## STATUS

| Name | Description |
|---|---|
| **INVALID** = 0 | Data is not available, user is not wearing the device or eyes cannot be found. |
| **ADJUST** = 1 | User is wearing the device, but gaze tracking is being calibrated. |
| **VALID** = 2 | Data is valid. |

## EYE_STATUS

| Name | Description |
|---|---|
| **INVALID** = 0 | Eye is not tracked and not visible (for example, eye is shut). |
| **VISIBLE** = 1 | Eye is visible but not reliably tracked (for example, saccade or blink). |
| **COMPENSATED** = 2 | Eye is tracked but quality compromised (for example, headset has moved after calibration). |
| **TRACKED** = 3 | Eye is tracked. |

### Properties

## 🔒︎ bool IsAvailable

The value indicating if eye tracking is available on the active VR device and is supported at runtime.
## 🔒︎ bool IsValid

The value indicating if eye tracking is valid.
## 🔒︎ vec3 FocusWorldPosition

The position of the eye focus point in world coordinates.
## 🔒︎ vec3 GazeWorldDirection

The gaze direction vector, which is a combined value for both eyes, in world coordinates.
## 🔒︎ vec3 LeftEyeWorldPosition

The position of the left eye in world coordinates.
## 🔒︎ vec3 LeftEyeWorldDirection

The direction vector of the left eye in world coordinates.
## 🔒︎ float LeftPupilDiameter

The estimated diameter of the left pupil. The function returns 0.0f if the pupil is not tracked or the estimate is unavailable.
## 🔒︎ float LeftPupilIrisDiameterRatio

The ratio between the left pupil diameter estimate and the estimated diameter of the left iris. If either estimate is unavailable, preventing the calculation of the ratio, the function returns 0.0f.
## 🔒︎ float LeftIrisDiameter

The an estimated diameter of the left iris. The function returns 0.0f if the estimate is unavailable.
## 🔒︎ float LeftOpenness

The estimated openness ratio of the left eye. 1.0f corresponds to a fully open eye, 0.0f to a fully closed eye.
## 🔒︎ VREyeTracking.EYE_STATUS LeftStatus

The status of the left eye.
## 🔒︎ float RightPupilDiameter

The estimated diameter of the right pupil. The function returns 0.0f if the pupil is not tracked or the estimate is unavailable.
## 🔒︎ float RightPupilIrisDiameterRatio

The ratio between the right pupil diameter estimate and the estimated diameter of the left iris. If either estimate is unavailable, preventing the calculation of the ratio, the function returns 0.0f.
## 🔒︎ float RightIrisDiameter

The an estimated diameter of the right iris. The function returns 0.0f if the estimate is unavailable.
## 🔒︎ float RightOpenness

The estimated openness ratio of the right eye. 1.0f corresponds to a fully open eye, 0.0f to a fully closed eye.
## 🔒︎ vec3 RightEyeWorldPosition

The position of the right eye in world coordinates.
## 🔒︎ vec3 RightEyeWorldDirection

The direction vector of the right eye in world coordinates.
## 🔒︎ VREyeTracking.EYE_STATUS RightStatus

The status of the right eye.
## 🔒︎ float IPD

The interpupillary distance (IPD).
## 🔒︎ long CaptureTime

The timestamp of when the data was recorded, in nanoseconds.
## 🔒︎ double FocusDistance

The distance between the eye and the focus point. It is a value between 0 and 2> meters.
## 🔒︎ double Stability

The value specifying the stability of the user's focus. 0.0 means not stable and 1.0 means stable.
## 🔒︎ VREyeTracking.STATUS Status

The value representing the status of eye tracking in the Varjo headsets.
## 🔒︎ long RawFrame

The unique identifier of the frame when the data was recorded.
## bool VisualizerEnabled

The value indicating if the visualizer is enabled.
### Members

---

## bool HasFeatureRequestCalibration ( )

Returns a value indicating if eye tracking calibration can be requested via the API.
### Return value

true if eye tracking calibration can be requested via the API; otherwise, false.
## bool HasFeaturePupilDiameter ( )

Returns a value indicating if pupil diameter data is available.
### Return value

true if pupil diameter data is available; otherwise, false.
## bool HasFeatureIrisDiameter ( )

Returns a value indicating if iris diameter data is available.
### Return value

true if iris diameter data is available; otherwise, false.
## bool HasFeaturePupilIrisDiameterRatio ( )

Returns a value indicating if the ratio between pupil and iris diameters is available.
### Return value

true if the ratio between pupil and iris diameters is available; otherwise, false.
## bool HasFeatureOpenness ( )

Returns a value indicating if eye openness data (e.g., blink state or squinting) is available.
### Return value

true if eye openness data is available; otherwise, false.
## void RequestCalibration ( )

Triggers the gaze calibration sequence, if gaze tracking has been enabled in Varjo settings and the Varjo system is in a state where it can bring up the calibration UI.
