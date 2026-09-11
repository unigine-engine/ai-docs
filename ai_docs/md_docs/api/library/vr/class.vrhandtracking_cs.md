# Unigine.VRHandTracking Class (CS)

> **Notice:** This class is a singleton.


This class manages the VR hand tracking feature. It allows visualizing the bones basis, velocity and size to check and configure the hands configuration.


> **Notice:** Hand tracking is natively supported only when using the OpenXR backend. This includes **any VR device that supports OpenXR hand tracking** (e.g., Quest, Varjo, Vive with appropriate runtimes). For *varjo* and *openvr* backends, hand tracking requires an additional **[Ultraleap Plugin](../../../code/plugins/ultraleap/index_cs.md)**.
>
>
> Refer to [this article](../../../vr_development/vr_hand_tracking.md) to properly configure hand tracking in your project and choose the right backend.


## VRHandTracking Class

### Properties

## 🔒︎ bool IsAvailable

The value indicating if hand tracking is available on the active VR device and is supported at runtime.
## 🔒︎ VRHand HandLeft

The left hand.
## 🔒︎ VRHand HandRight

The right hand.
## bool VisualizerEnabled

***Console*:**`vr_hand_tracking_visualizer_enabled`The  value indicating if the visualizer for hands is enabled. When set to 1, the engine will draw a simple debug skeleton of the hands, showing bones only. This option requires the [Visualizer](../../../code/console/index.md#show_visualizer) to be enabled.
![](../../../api/library/vr/ht_command_visualizer.png)

  The default value is **false**.
## bool ShowBasis

***Console*:**`vr_hand_tracking_show_basis`The  value indicating if the visualizer for the coordinate axes (basis) of each hand bone is enabled. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled.
![](../../../api/library/vr/ht_command_bone_basis.png)

  The default value is **false**.
## bool ShowVelocity

***Console*:**`vr_hand_tracking_show_velocity`The  value indicating if the visualizer for the velocity vectors of each hand bone is enabled. Useful for debugging motion-based interactions like swipes or throws. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled.
![](../../../api/library/vr/ht_command_bone_velocity.png)

  The default value is **false**.
## bool ShowBoneSizes

***Console*:**`vr_hand_tracking_show_bone_sizes`The  value indicating if the visualizer for the size of each hand bone is enabled. Displays red spheres representing the size (radius) of each bone, providing a visual reference for the physical dimensions of the tracked hand. This option requires the [Hand visualizer](#vr_hand_tracking_visualizer_enabled) to be enabled.
![](../../../api/library/vr/ht_command_bone_sizes.png)

  The default value is **false**.
