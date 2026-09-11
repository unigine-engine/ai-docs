# Hand Tracking


Hand tracking is a technology that allows mixed reality (MR) systems to accurately detect and track the user's hand movements and finger positions in real time. By using depth sensors and computer vision algorithms, MR devices can identify the position, orientation, and articulation of each hand.


With hand tracking, users interact with virtual environments using natural gestures, such as pointing, pinching, or grabbing, mirroring how they would manipulate objects in the real world. This allows for a more intuitive and immersive user experience, reducing the learning curve and increasing the sense of presence.


The system continuously captures and interprets hand poses and movements in real time, providing a detailed model of the user's hand. Hand tracking supports a wide range of use cases, including user interface navigation, direct manipulation of virtual objects, and execution of gesture-based commands.


## Hand Tracking in UNIGINE


UNIGINE provides built-in, native support for hand tracking based on the [OpenXR Standard](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_tracking). This allows VR applications created with UNIGINE to track user's hands and fingers in real time. The native hand tracking system supports the following [OpenXR Extensions](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#extension-appendices-list):


- *[XR_EXT_hand_tracking](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_tracking)* - core extension for tracking hand joints and providing their positions and orientations.
- *[XR_EXT_hand_interaction](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_interaction)* - enhances the basic tracking by providing interaction-specific hand data.
- *[XR_EXT_hand_joints_motion_range](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_joints_motion_range)* - offers additional control over the reported range of motion for joints, useful for improved realism and precision.
- *[XR_EXT_hand_tracking_data_source](https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_hand_tracking_data_source)* - provides information about the source or method used for hand tracking data.


This feature is integrated into the engine's VR system (no extra plugin needed) and supports any OpenXR - compatible device that offers hand tracking capabilities.


When a UNIGINE VR-based application with OpenXR backend starts, the engine checks for an available OpenXR runtime provided by the user's VR device or a platform. Then the engine automatically initializes native hand tracking and retrieves all the hand related data via the OpenXR API.


To use hand tracking, make sure to launch the engine with the OpenXR backend:


```bash
-vr_app openxr
```


Native hand tracking is only available in this mode. Other VR backends (such as OpenVR or *Varjo Native SDK*) **do not support it** and require external plugins to function. In this cases, hand tracking can still be enabled through the **[Ultraleap plugin](#plugins)**, but only if the necessary hardware is connected.


Note that some **Varjo headsets** (*Varjo XR-3, VR-3, VR-2 Pro*) include built-in Ultraleap sensors, but to access them, either the OpenXR runtime must be used or the Ultraleap plugin must be manually enabled in the application.

 Best Practice
To confirm that the required OpenXR extensions have been recognized, check the engine's startup logs or console. The following entries indicate that hand tracking and its related extensions are properly detected and initialized:


```text
OpenXRExt::init(): Extension "XR_EXT_hand_tracking" found
OpenXRExt::init(): Extension "XR_EXT_hand_interaction" found
OpenXRExt::init(): Extension "XR_EXT_hand_joints_motion_range" found
OpenXRExt::init(): Extension "XR_EXT_hand_tracking_data_source" found

```


If none of these extensions are listed, hand tracking won't be available as its support depends on the selected OpenXR runtime. If one or more extensions are missing, certain functionality may be limited or unavailable. In such cases, the engine will try its best to emulate the missing behavior.


## Hand Hierarchy


All hand tracking data is spatially relative to the main camera (i.e. the player's HMD - head-mounted display). This means that hand positions follow the headset, when the user moves or rotates their head, the hands move accordingly in the same local tracking space. They are not positioned in world space independently of the HMD.


> **Notice:** In the OpenXR Specification, tracked hand elements are referred to as joints. In UNIGINE, these elements are called bones, consistent with the **VRBone** class used in API. Conceptually, each bone corresponds to a tracked joint defined by *XR_EXT_hand_tracking*.


Each hand's skeletal model consists of 26 bones organized in a hierarchy under a single root. The bones include the **Wrist**, **Palm**, and **Finger** bones for all five fingers (thumb, index, middle, ring, little). The finger bones, except the tips, are named after the corresponding bone at the further end of the bone from the fingertips.


The **Wrist** is considered as the root of the hierarchy for the hand - it's the point where the hand would connect to the forearm. Under the **Wrist**, all finger bones are arranged.


The **Palm** bone is located at the center of the middle finger's metacarpal bone, representing a convenient central point (the middle of the palm area), which can be useful for certain calculations or attaching objects to the user's hand.


![](ht_bones_structure.png)


Unlike the other fingers, the thumb lacks an intermediate phalanx, resulting in one less bone - just like in a real human hand.


> **Notice:** The bone structure in the native OpenXR system differs from that used in the [Ultraleap plugin](../code/plugins/ultraleap/index_cpp.md).


## Coordinate System Orientation


All the hand tracking data is given in UNIGINE�s native coordinate system, which is a right-handed Cartesian coordinate system: X and Y form a horizontal plane, Z axis points up. When looking at a hand from the back (palm facing downward), the axes of each bone are aligned as follows:


- **X**-axis points to the left
- **Y**-axis points backwards, along the wrist
- **Z**-axis points upward, out of the back of the hand


![](ht_hands_basis.png)


This consistent basis orientation applies to all bones in the hand.


## Hand Tracking API


Hand tracking feature is accessible through a set of specialized classes in the engine's **[VR API](../vr_development/vr_api.md)**. These classes provide a structured way to get hand and finger bone information, and to control debug visualization. The main classes involved are:


- **[VRHandTracking](../api/library/vr/class.vrhandtracking_cpp.md)** - The manager class for the hand tracking system. Through **VRHandTracking** you can access the two tracked hands and configure global settings related to hand tracking visualization.
- **[VRHand](../api/library/vr/class.vrhand_cpp.md)** - This class represents a single hand (either left or right) being tracked. Each **VRHand** contains the set of bones (as **VRBone** objects) for that hand. The class also provides access to state information such as whether the hand is holding a controller or whether the controller is active. It also includes methods for querying individual bones and rendering a debug visualizer.
- **[VRBone](../api/library/vr/class.vrbone_cpp.md)** - This class represents a single bone in the hand�s skeletal model. Each **VRBone** provides the position and orientation of itself and additional information like its radius (approximate thickness) and velocity. It also includes a method for rendering a debug visualizer for the specific bone.


The system updates the **VRBone** transforms every frame in sync with the VR loop, so at any time you can query these classes to get the latest hand pose.


## Debugging and Visualization Tools


The following console commands control the hand tracking debug visualizer. They can be entered into the [Console](../code/console/index.md) (or set in [configuration files](../code/configuration_file_cpp.md) or called via the [API](../api/library/vr/class.vrhandtracking_cpp.md#vr_hand_tracking_visualizer_enabled)).


| vr_hand_tracking_visualizer_enabled | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
|---|---|
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the  value indicating if the visualizer for hands is enabled. When set to 1, the engine will draw a simple debug skeleton of the hands, showing bones only. This option requires the [Visualizer](../code/console/index.md#show_visualizer) to be enabled. ![](../api/library/vr/ht_command_visualizer.png) | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_hand_tracking_show_basis | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the  value indicating if the visualizer for the coordinate axes (basis) of each hand bone is enabled. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled. ![](../api/library/vr/ht_command_bone_basis.png) | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_hand_tracking_show_bone_sizes | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the  value indicating if the visualizer for the size of each hand bone is enabled. Displays red spheres representing the size (radius) of each bone, providing a visual reference for the physical dimensions of the tracked hand. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled. ![](../api/library/vr/ht_command_bone_sizes.png) | **Arguments:** **0** - disabled (by default) **1** - enabled |
| vr_hand_tracking_show_velocity | Config file: [*.boot](../code/configuration_file_cpp.md#boot) |
| **Description:** - **Variable.** � Prints a value indicating if the option controlled by the command below is enabled. - **Command.** � Toggles the  value indicating if the visualizer for the velocity vectors of each hand bone is enabled. Useful for debugging motion-based interactions like swipes or throws. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled. ![](../api/library/vr/ht_command_bone_velocity.png) | **Arguments:** **0** - disabled (by default) **1** - enabled |


## Alternative Hand Tracking Plugins


With the introduction of native OpenXR hand tracking, UNIGINE supports a unified and preffered approach for hand and finger tracking. However, the **[Ultraleap](../code/plugins/ultraleap/index_cpp.md)** plugin is available and functional for cases where OpenXR is not an option or specific hardware configurations (such as *Varjo Native SDK* or *OpenVR*) require them.


### Ultraleap Plugin (for Specific Use Cases)


To support newer *Ultraleap* devices, UNIGINE includes a separate Ultraleap plugin. While OpenXR is the preferred method for hand tracking, the *Ultraleap* plugin remains relevant for certain configurations and use cases, especially when using *Varjo Native SDK* or when OpenXR-based hand tracking is not available.


This plugin uses Ultraleap's tracking software and provides hand data via an API similar to the older Leap Motion interface.


> **Notice:** While these plugins are deprecated in favor of **native OpenXR hand tracking**, they are still functional and can be used with specific runtimes such as **Varjo Native SDK** and **OpenVR**.
>
>
> Additionally, if you need to use a *Leap Motion* or *Ultraleap* device with OpenXR, but your current runtime does not support the ***XR_EXT_hand_tracking*** extension (or lacks full compatibility), you can [configure Ultraleap's OpenXR API Layer](https://docs.ultraleap.com/openxr/installation/index.html). This layer injects or overrides the required hand tracking extensions and takes priority during runtime initialization.
