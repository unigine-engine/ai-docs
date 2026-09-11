# EyetrackingPointer Component

**Inherits from:** ComponentBase


EyetrackingPointer is a component that visualizes the user's eye gaze direction using an intersection pointer. It performs a ray intersection from the eye tracking data each frame and highlights the object being looked at.


This component requires a VR headset with eye tracking support (e.g., Varjo). When eye tracking data is available, the component casts a ray into the scene and can be used to identify and interact with objects the user is looking at.


### See Also


- **[VRPlayerVR](../../../../api/modules/vr/components/players/class.vrplayervr.md)**
