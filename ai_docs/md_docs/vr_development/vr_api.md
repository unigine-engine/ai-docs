# VR API Reference


The following classes are used for VR management in UNIGINE:


| Class | Description |
|---|---|
| *[VR](../api/library/vr/class.vr_cpp.md)* | Central entry point for the VR subsystem: initialization, backend and device info, tracking space, and runtime feature queries. |
| *[VREyeTracking](../api/library/vr/class.vreyetracking_cpp.md)* | Access to eye tracking data: gaze direction, eye openness, pupil position, and IPD. |
| *[VRHandTracking](../api/library/vr/class.vrhandtracking_cpp.md)* | Controller-free hand tracking: retrieve per-hand skeleton data and tracking state. |
| *[VRMixedReality](../api/library/vr/class.vrmixedreality_cpp.md)* | Mixed reality pipeline control: camera feed, chroma key, depth testing, blend masking, and camera settings (exposure, white balance, ISO). |
| *[VRMarkerObject](../api/library/vr/class.vrmarkerobject_cpp.md)* | Represents a single tracked physical marker used to anchor virtual objects to real-world positions. |
| *[VRHand](../api/library/vr/class.vrhand_cpp.md)* | A tracked hand returned by *VRHandTracking*: per-finger bone hierarchy, confidence, and hand-level transforms. |
| *[VRBone](../api/library/vr/class.vrbone_cpp.md)* | An individual bone in a tracked hand skeleton: position, rotation, and radius. |


Classes for VR input - devices and events:


| Class | Description |
|---|---|
| *[InputVRDevice](../api/library/controls/class.inputvrdevice_cpp.md)* | Base class for all VR input devices: common properties like device type, pose, velocity, and connection state. |
| *[InputVRHead](../api/library/controls/class.inputvrhead_cpp.md)* | The headset as an input device: head pose and HMD-specific properties (display frequency, proximity sensor). |
| *[InputVRController](../api/library/controls/class.inputvrcontroller_cpp.md)* | A hand controller: buttons, axes (trigger, grip, thumbstick), haptic feedback, and controller-specific pose. |
| *[InputVRTracker](../api/library/controls/class.inputvrtracker_cpp.md)* | A standalone tracked object (e.g., Vive Tracker): pose and role assignment. OpenVR backend only. |
| *[InputVRBaseStation](../api/library/controls/class.inputvrbasestation_cpp.md)* | A tracking reference point (e.g., Lighthouse base station): position in the play area. OpenVR backend only. |


| Event Class | Description |
|---|---|
| *[InputEventVRButton](../api/library/controls/class.inputeventvrbutton_cpp.md)* | Fired when a controller button is pressed or released. |
| *[InputEventVRButtonTouch](../api/library/controls/class.inputeventvrbuttontouch_cpp.md)* | Fired when a controller button is touched or untouched (capacitive sensors). |
| *[InputEventVRAxisMotion](../api/library/controls/class.inputeventvraxismotion_cpp.md)* | Fired when a controller axis value changes (trigger pull, thumbstick movement). |
| *[InputEventVRDevice](../api/library/controls/class.inputeventvrdevice_cpp.md)* | Fired when a VR device is connected, disconnected, or changes its tracking state. |
