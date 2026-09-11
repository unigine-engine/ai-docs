# VR & XR Development


UNIGINE handles stereo rendering, head tracking, controller input, and device management for you - you focus on building your application. The VR API is hardware-agnostic: the same code runs on *Quest, HTC Vive, Varjo*, and other headsets without changes. Advanced features like hand tracking, eye tracking, foveated rendering, and mixed reality are available where the hardware supports them.


This article gives an overview of UNIGINE's VR capabilities, supported backends, and devices. For a step-by-step setup guide, see [*Getting Started with VR*](../vr_development/vr_template/index.md).


> **Notice:** Development of AR applications is not currently supported. This includes optical see-through AR (overlaying virtual content onto semi-transparent optics such as glass or prisms) and mobile AR (ARKit/ARCore).


## What You Can Build


UNIGINE supports two types of XR applications:


- **Virtual Reality** (VR) - a fully synthetic immersive environment rendered stereoscopically. The user is entirely inside a virtual world and interacts with it through controllers, hand tracking, or gaze. Typical use cases: training simulators, engineering visualization, design review, virtual prototyping.
- **[Mixed Reality](#mixed_reality)** (MR)  - the virtual world is blended with a live camera feed from the headset, so the user sees both real and virtual objects at the same time. Useful when the user needs to stay aware of their physical surroundings - for example, operating real equipment while seeing virtual overlays, or collaborating with other people in the room. Requires a headset with passthrough cameras (Varjo XR, Quest 3, and others).


## Quick Start


To get a VR application running:


1. Connect your headset and install its runtime software (SteamVR, Quest PC app, Varjo Base - depending on the device).
2. Create or open a UNIGINE project. For new projects, start with the *[VR Template](../content/vr/index.md#vr_template)* (C++ or C#) available on the *Templates* tab in SDK Browser - it comes with preconfigured VR features, locomotion, and interaction mechanics that can serve as a base for any VR application.
3. Launch the application with *[-vr_app openxr](../code/command_line.md#vr_app)* (or *openvr / varjo*, depending on your [backend](#vr_backends)). Any UNIGINE project can run in VR this way.


The template's built-in mechanics are described in *Getting Started with the VR Template*.


## Backends and Runtimes


UNIGINE application communicates with VR headsets through two layers:


- **Backend** - the engine-side integration that sets up stereo rendering and passes frames to the runtime.
- **Runtime** - a background service on your PC (SteamVR, Horizon Link, Varjo Base, etc.) that manages the headset hardware: tracking, controllers, frame compositing.


![](vr_stack.png)


You write your application once using the [UNIGINE VR API](../vr_development/vr_api.md). The backend is chosen at launch time and depends on your target device. Features that are not available on a given backend or device can be queried at runtime, so your code does not need to branch per platform.


### Which Backend to Choose


UNIGINE supports three backends:


- **OpenXR** - the default choice for most projects. Works with the widest range of devices.
- **Varjo** - use this if you have a Varjo headset and need access to its full feature set (mixed reality, foveated rendering, motion prediction, Varjo Markers).
- **OpenVR** - provides access to features not yet available in OpenXR: trackers, render models, and base stations.


You select the backend at application start-up via the *[-vr_app](../code/command_line.md#vr_app)* command-line option:


- *-vr_app openxr*
- *-vr_app varjo*
- *-vr_app openvr*


Alternatively, you can set the default backend for all projects in SDK Browser under *Global Options → Default Video Options*:


![](global_options.png)


By default, VR is not initialized.


### OpenXR


![](openxr.png)


***OpenXR*** is an open, royalty-free standard by the Khronos Group. It is the recommended backend for new projects because it supports the widest range of devices through a single API.


The runtime depends on your headset: Quest devices work with the [Quest PC app](https://www.oculus.com/setup/) or [SteamVR](https://store.steampowered.com/about/); HTC Vive and other SteamVR-compatible devices use SteamVR; WMR headsets use the runtime built into Windows. Refer to your headset vendor's documentation for setup details.


### Varjo


![](varjo-logo.jpg)


The ***Varjo*** backend is a dedicated integration for Varjo industrial-grade headsets. Use it when you need the full Varjo feature set: eye tracking, mixed reality with camera control, foveated rendering, motion prediction, and Varjo Markers.


To get started, install *[Varjo Base](https://varjo.com/downloads/#varjo-base)* and *[SteamVR](https://store.steampowered.com/about/)* (required by the Varjo backend for controller and tracker input). Hand tracking is available via the *[Ultraleap plugin](../code/plugins/ultraleap/index_cpp.md)*.


> **Notice:** Varjo headsets also work with the OpenXR backend (via Varjo Base as the OpenXR runtime), but some Varjo-specific features will not be available. See the [Supported Features](#vr_features) table for details.


### OpenVR


![](openvr.png)


***OpenVR*** is a VR API by Valve. While OpenXR has become the industry standard, OpenVR remains the only backend that provides access to trackers, render models, and base stations. Choose it when your project depends on these features.


OpenVR works exclusively through the ***SteamVR*** runtime - [install it via Steam](https://store.steampowered.com/about/).


> **Warning:** **Reprojection** on Linux must be enabled manually.
>
>
> Add the following line in the *"steamvr"* section of the `~/.steam/steam/config/steamvr.vrsettings` file:
>
>
> ```xml
> "steamvr" : {
> 	"enableLinuxVulkanAsync" : true
> 	/.../
> }
>
> ```


## Supported Features


Not every feature is available on every backend. Some features also depend on the headset hardware - use the [VR API](../vr_development/vr_api.md) to check what is available at runtime.


| Feature | OpenXR | Varjo | OpenVR |
|---|---|---|---|
| **Eye Tracking** Gaze direction and eye state | ![Supported](yes.png) | ![Supported](yes.png) | ![Not supported](no.png) |
| **Hand Tracking** Skeletal finger tracking without controllers | ![Supported](yes.png) | ![Supported](yes.png) (via [Ultraleap plugin](../code/plugins/ultraleap/index_cpp.md)) | ![Not supported](no.png) |
| **Mixed Reality** Blending virtual content with a live camera feed | ![Supported](yes.png) | ![Supported](yes.png) | ![Not supported](no.png) |
| **Foveated Rendering** Full resolution only where the user is looking, reducing GPU load | ![Supported](yes.png) | ![Supported](yes.png) | ![Not supported](no.png) |
| **Motion Prediction** Extrapolating head pose to reduce perceived latency | ![Not supported](no.png) | ![Supported](yes.png) | ![Not supported](no.png) |
| **Object Markers** Anchoring virtual objects to tracked physical markers | ![Not supported](no.png) | ![Supported](yes.png) | ![Not supported](no.png) |
| **Trackers** Standalone tracked devices (e.g. Vive Trackers for body parts or props) | ![Not supported](no.png) | ![Not supported](no.png) | ![Supported](yes.png) |
| **Base Stations** Access to tracking reference points in the play area | ![Not supported](no.png) | ![Not supported](no.png) | ![Supported](yes.png) |
| **Render Models** 3D models of controllers provided by the runtime | ![Not supported](no.png) | ![Not supported](no.png) | ![Supported](yes.png) |


## Supported Devices


The following devices are regularly tested with UNIGINE:


- *Quest 2* / *Quest 3* / *Quest Pro* / *Rift* / *Rift S*
- *HTC Vive* / *Vive Pro* / *Vive Focus* / *Vive Cosmos* / *Vive XR Elite*
- *Varjo VR-1* / *VR-2* / *VR-3* / *XR-3* / *XR-4*
- *PICO 4*


Any other OpenXR- or OpenVR-compatible headset should work as well, though specific features may vary.


For performance profiling, use the tools provided by your runtime: [SteamVR Frame Timing](https://developer.valvesoftware.com/wiki/SteamVR/Frame_Timing) for SteamVR, [Oculus PerfHud](https://developer.oculus.com/documentation/native/pc/dg-hud/?locale=ru_RU) for Oculus devices. You can also use [XR Simulator](https://developer.oculus.com/documentation/unreal/xrsim-intro) as an OpenXR runtime for testing without a physical headset.


## Mixed Reality


In a pure VR application the user is fully immersed in a synthetic world. Mixed Reality adds the real world back in: front-facing cameras on the headset capture the physical environment, and the engine composites virtual objects on top of the camera feed. The user sees both at the same time.


This matters when users need to stay aware of their physical surroundings - operating real equipment with virtual overlays, collaborating with other people in the room, or navigating a real workspace. MR is supported via the **Varjo** backend (Varjo XR headsets) and the **OpenXR** backend (devices with passthrough cameras, such as *Quest 3*).


The Varjo backend also supports **object markers** - physical markers tracked by the headset cameras to anchor virtual objects to real-world positions (e.g., placing a virtual panel on a real desk).


Mixed Reality is managed via the *[VRMixedReality](../api/library/vr/class.vrmixedreality_cpp.md)* and *[VRMarkerObject](../api/library/vr/class.vrmarkerobject_cpp.md)* classes. Check out the **[C++ VR Template](../vr_development/vr_template/vr_template_mixed_reality/index.md)** to see MR features in action.


## VR Template


Rather than starting from scratch, you can use the *[VR Template](../content/vr/index.md#vr_template)* - a ready-made project with common VR interactions already implemented: grabbing and throwing objects, pressing buttons, opening and closing drawers, locomotion, and more.


The template is built on the [Component System](../principles/component_system/index.md), so you can extend it by adding your own components.


See [Getting Started with VR](../vr_development/vr_template/index.md) for a step-by-step guide on creating a project from the template.


## Next Steps


- [*Getting Started with VR*](../vr_development/vr_template/index.md) - create and run your first VR project.
- [*VR API Reference*](../api/library/vr/index.md) - the full class and method reference for managing VR via code.
