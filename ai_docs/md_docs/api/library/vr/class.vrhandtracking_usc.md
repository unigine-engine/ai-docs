# Unigine.VRHandTracking Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class manages the VR hand tracking feature. It allows visualizing the bones basis, velocity and size to check and configure the hands configuration.


> **Notice:** Hand tracking is natively supported only when using the OpenXR backend. This includes **any VR device that supports OpenXR hand tracking** (e.g., Quest, Varjo, Vive with appropriate runtimes). For *varjo* and *openvr* backends, hand tracking requires an additional **[Ultraleap Plugin](../../../code/plugins/ultraleap/index_usc.md)**.
>
>
> Refer to [this article](../../../vr_development/vr_hand_tracking.md) to properly configure hand tracking in your project and choose the right backend.


## VRHandTracking Class

### Members

## int isAvailable () const

Returns the current value indicating if hand tracking is available on the active VR device and is supported at runtime.
### Return value

Current hand tracking is available
## VRHand getHandLeft () const

Returns the current left hand.
### Return value

Current left hand.
## VRHand getHandRight () const

Returns the current right hand.
### Return value

Current right hand.
## void setVisualizerEnabled ( int enabled = 0 )

***Console*:**`vr_hand_tracking_visualizer_enabled`Sets a new  value indicating if the visualizer for hands is enabled. When set to 1, the engine will draw a simple debug skeleton of the hands, showing bones only. This option requires the [Visualizer](../../../code/console/index.md#show_visualizer) to be enabled.
![](../../../api/library/vr/ht_command_visualizer.png)

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **enabled** - The the visualizer for hands The default value is **false**.

## int isVisualizerEnabled () const

***Console*:**`vr_hand_tracking_visualizer_enabled`Returns the current  value indicating if the visualizer for hands is enabled. When set to 1, the engine will draw a simple debug skeleton of the hands, showing bones only. This option requires the [Visualizer](../../../code/console/index.md#show_visualizer) to be enabled.
![](../../../api/library/vr/ht_command_visualizer.png)

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current the visualizer for hands The default value is **false**.
## void setShowBasis ( int basis = 0 )

***Console*:**`vr_hand_tracking_show_basis`Sets a new  value indicating if the visualizer for the coordinate axes (basis) of each hand bone is enabled. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled.
![](../../../api/library/vr/ht_command_bone_basis.png)

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **basis** - The the visualizer for the basis of each hand bone The default value is **false**.

## int isShowBasis () const

***Console*:**`vr_hand_tracking_show_basis`Returns the current  value indicating if the visualizer for the coordinate axes (basis) of each hand bone is enabled. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled.
![](../../../api/library/vr/ht_command_bone_basis.png)

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current the visualizer for the basis of each hand bone The default value is **false**.
## void setShowVelocity ( int velocity = 0 )

***Console*:**`vr_hand_tracking_show_velocity`Sets a new  value indicating if the visualizer for the velocity vectors of each hand bone is enabled. Useful for debugging motion-based interactions like swipes or throws. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled.
![](../../../api/library/vr/ht_command_bone_velocity.png)

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **velocity** - The the visualizer for the velocity vectors of each hand bone The default value is **false**.

## int isShowVelocity () const

***Console*:**`vr_hand_tracking_show_velocity`Returns the current  value indicating if the visualizer for the velocity vectors of each hand bone is enabled. Useful for debugging motion-based interactions like swipes or throws. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled.
![](../../../api/library/vr/ht_command_bone_velocity.png)

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current the visualizer for the velocity vectors of each hand bone The default value is **false**.
## void setShowBoneSizes ( int sizes = 0 )

***Console*:**`vr_hand_tracking_show_bone_sizes`Sets a new  value indicating if the visualizer for the size of each hand bone is enabled. Displays red spheres representing the size (radius) of each bone, providing a visual reference for the physical dimensions of the tracked hand. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled.
![](../../../api/library/vr/ht_command_bone_sizes.png)

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Arguments

- *int* **sizes** - The the visualizer for the size of each hand bone The default value is **false**.

## int isShowBoneSizes () const

***Console*:**`vr_hand_tracking_show_bone_sizes`Returns the current  value indicating if the visualizer for the size of each hand bone is enabled. Displays red spheres representing the size (radius) of each bone, providing a visual reference for the physical dimensions of the tracked hand. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled.
![](../../../api/library/vr/ht_command_bone_sizes.png)

 This parameter is stored in the following configuration file: **[*.boot](../../../code/configuration_file_cpp.md#boot)**.
### Return value

Current the visualizer for the size of each hand bone The default value is **false**.
