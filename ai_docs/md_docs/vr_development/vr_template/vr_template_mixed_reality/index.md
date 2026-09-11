# Mixed Reality

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


Want to see the real world while wearing a headset? Mixed reality (MR) blends the camera feed from your device with the virtual scene - so you can walk around your room, interact with physical objects, or overlay virtual content on top of reality.


> **Notice:** *Mixed Reality* functionality is supported through both the [OpenXR](../../../vr_development/index.md#backend_openxr) and [Varjo](../../../vr_development/index.md#backend_varjo) backends. The Varjo backend provides a richer set of MR features including chromakey, camera controls, and color correction.


## Mixed Reality Menu


MR functionality is accessed through the [Head Menu](../../../vr_development/vr_template/vr_template_gui/index_cpp.md#head_menu_cpp) - a panel that stays fixed relative to the player's view. The menu is implemented by the *[MixedRealityMenuGui](../../../api/templates/template_vr/gui/class.mixedrealitymenugui.md)* property and provides the following controls:


- **Video Passthrough** - toggle the real-world camera feed on or off, with an option for motion prediction to reduce artifacts in dynamic scenes.
- **Camera Settings** - adjust white balance, exposure time, and ISO sensitivity. Each parameter supports multiple presets as well as an automatic mode.
- **Blend Masking** - control how the real and virtual images are composited. Available modes include restricting the video feed to a mask, restricting VR content to a mask, or using a chromakey-based separation.
- **Chromakey** - HSV-based color keying with configurable hue, saturation, and value thresholds plus per-channel tolerance falloff. A live color preview is displayed in the menu.
- **Depth Test** - enable depth testing between the real and virtual worlds, with configurable near/far range limits.
- **Color Correction** - match the virtual scene's lighting to the real camera feed using exposure and white balance correction modes.


The available settings depend on the capabilities of the active VR backend - some features (chromakey, depth test, blend masking) may not be available on all devices.


To manage mixed reality programmatically, use the [VRMixedReality](../../../api/library/vr/class.vrmixedreality_cpp.md) class of UNIGINE API.


Built with: [AttachToHead](../../../api/modules/vr/components/objects/class.attachtohead.md), [MixedRealityMenuGui](../../../api/templates/template_vr/gui/class.mixedrealitymenugui.md)
