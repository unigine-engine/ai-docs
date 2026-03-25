# VR & XR Development


**XR** (extended reality), is a general term for any enhanced technology combining the real and digital worlds to create new kinds of interactivity and perception. Essentially, this term is an umbrella under which the following types of applications:


- **Virtual Reality** (VR): is an immersive self-contained environment that makes the user feel inside a virtual or digitally reproduced real 3D world.
- **[Mixed Reality](#mixed_reality)** (MR): user's real-world environment combined with the application's virtual environment with an ability to interact with each other.
- **Augmented Reality** (AR): application's virtual content is projected onto physical glass or a display over a view of the real world. > **Notice:** Development of AR applications for mobile platforms is not currently supported.


These technologies provide new ways to train, educate, entertain, and collaborate.


UNIGINE offers built-in functionality for development of Virtual Reality and [Mixed Reality](#mixed_reality) applications. It enables you to implement logic for various VR devices through a [single API interface](../api/library/vr/index.md) without using additional plugins.


> **Warning:** **Reprojection** on Linux is to be enabled manually.
>
>
> Add the following line in the *"steamvr"* section of the `~/.steam/steam/config/steamvr.vrsettings` file:
>
>
> ```xml
> 	"steamvr" : {
> 		"enableLinuxVulkanAsync" : true
>
> 		/.../
> 	}
>
> ```


### See Also


- The article on [*Getting Started with VR*](../start/vr/index_cpp.md) to start developing VR projects in UNIGINE.
- The section on [*Developing VR Applications*](https://learn.unigine.com/mod/page/view.php?id=112) of the [Basic Introductory Course on UNIGINE real-time 3D engine](https://learn.unigine.com/?redirect=0).
- [*VR API Reference*](../start/vr/index_cpp.md) for details on managing VR via code.


## VR System in UNIGINE


The built-in VR system provides integration of ***OpenVR***, ***Varjo***, and ***OpenXR***.


### OpenVR Integration


![](openvr.png)


***OpenVR*** is a comprehensive VR SDK (API and runtime) that allows access to VR hardware from various vendors without requiring that applications have specific knowledge of the hardware they are targeting.


So, thanks to OpenVR integration, UNIGINE supports VR development for a wide range of VR devices, including the *Oculus Rift, HTC Vive*, and other OpenVR-compatible devices. The full list of supported devices is given [below](#vr_devices).


### Varjo Integration and Supported Features


![](varjo_xr-3_sm.jpg)

*Image Courtesy of Varjo.*


***Varjo's*** industrial-grade headsets with **eye-tracking** and **[mixed reality](#mixed_reality)** capabilities allow you to create VR and MR applications. With Mixed Reality, you can combine the real-world view from front-facing cameras mounted on the headset with the VR image.


Moreover, there is **hand-tracking** in VR available for Varjo VR and XR headsets through the *[Ultraleap](../code/plugins/ultraleap/index_cpp.md)* integration plugin. It provides finger fidelity, two-hand performance, higher tracking robustness, and a lot of other improvements.


Additionally, Varjo headsets **running with the OpenXR** runtime support native hand tracking without the need for extra plugins, offering a more streamlined and unified experience. Refer to [this article](../vr_development/vr_hand_tracking.md) to properly configure hand tracking with Varjo devices and choose the best setup for your project.


The following table lists *Varjo* *native features* that are supported by UNIGINE VR system:


| Varjo Features | VR System |
|---|---|
| Supported graphics APIs | DX12, Vulkan |
| Human-eye resolution | ![Supported](yes.png) |
| Eye tracking | ![Supported](yes.png) |
| Eye tracking parameters | ![Supported](yes.png) |
| Eye camera datastream | ![Not supported](no.png) |
| Mixed reality (MR) | ![Supported](yes.png) |
| MR environment reflections | ![Supported](yes.png) |
| MR post-process shaders | ![Not supported](no.png) |
| MR datastream | ![Supported](yes.png) |
| Chroma keying | ![Supported](yes.png) |
| Varjo Markers | ![Supported](yes.png) |
| Depth buffer submission | ![Supported](yes.png) |
| Velocity buffer submission | ![Supported](yes.png) |
| Multi-app support | ![Not supported](no.png) |
| Support for multiple layers | ![Supported](yes.png) |
| Occlusion mask | ![Supported](yes.png) |
| Instanced rendering | ![Not supported](no.png) |
| Foveated rendering | ![Supported](yes.png) |
| SLI-compatible | ![Not supported](no.png) |


### OpenXR Integration


![](openxr.png)


***OpenXR*** is an open standard aimed at unifying the AR/VR/MR software development for broader hardware reach, reducing the effort for porting or re-writing code, providing seamless integration across diverse platforms and devices.


The current implementation is a baseline for supporting VR via OpenXR API, which includes support for *DX11*, *DX12*, and *Vulkan* graphics APIs on Windows.


## VR Development


UNIGINE enables the development of VR applications for different VR platforms, including the ones that have released *OpenXR runtimes*.


### Working with OpenVR


To utilize ***OpenVR***, you need to install the *SteamVR* platform. OpenVR is not tied to a particular hardware, allowing projects to be used with *any VR device that supports SteamVR*.


When developing for SteamVR, you should first [download and install Steam](https://store.steampowered.com/about/) and then launch SteamVR.


> **Notice:** If you install one of the [HTC Vive HMDs](https://www.vive.com/us/setup/), SteamVR will be set automatically on the HMD's installation.


For performance profiling, you can use the *[SteamVR Frame Timing](https://developer.valvesoftware.com/wiki/SteamVR/Frame_Timing)* tool.


*[VR Template](../content/vr/index.md#vr_template)* provides the models of the following SteamVR-compatible controllers: *HTC Vive, HTC Vive Pro*, and *HTC Vive Cosmos*.


### Working with OpenXR


***OpenXR*** integration allows you to develop applications for OpenXR-compatible devices. It doesn't require SteamVR — you only need to choose the correct runtime depending on the device.


For example, with Oculus HMDs, you need to install [Oculus Rift PC Runtime](https://www.oculus.com/setup/), launch the Oculus PC application, and enable OpenXR runtime (*Settings → General → OpenXR Runtime → Set Oculus as active*). It allows the engine to connect to the Oculus HMD through OpenXR, utilizing Oculus runtime. Such an approach simplifies development by using a single API instead of separate, hardware-specific APIs.


> **Notice:** Alternatively, you can enable OpenXR runtime in SteamVR, and the engine will connect to the Oculus HMD *through OpenXR using SteamVR*. Moreover, some standalone headsets (like *Meta Quest* devices) have the option to install *Steam Link* allowing them to connect to a PC using SteamVR.


> **Notice:** There is also an option to use *[XR Simulator](https://developer.oculus.com/documentation/unreal/xrsim-intro)* as an XR runtime for Quest headsets.


For performance profiling, you can use the [Oculus PerfHud](https://developer.oculus.com/documentation/native/pc/dg-hud/?locale=ru_RU) tool. It displays a performance summary, including the frame rate of the application and the unused hardware performance available, latency timing, application render timing, information about the HMD version, and others. To use Oculus PerfHud with UNIGINE, follow the instructions in [Oculus documentation](https://developer.oculus.com/documentation/native/pc/dg-performance-indicator/).


*[VR Template](../content/vr/index.md#vr_template)* provides the models of the *Oculus Touch* and *Oculus Quest* controllers that are compatible with Oculus HMDs only.


## Supported Devices


The following VR device models are supported:


- *Oculus Rift* / *Rift S* / *Quest* / *Quest 2* / *Quest 3* / *Quest Pro* (with Oculus Link cable / Oculus Link wireless / SteamLink)
- *HTC Vive* / *Vive Pro* / *Focus* / *Cosmos*
- *Varjo VR-1* / *VR-2* / *VR-3* / *XR-3* (with extended mixed reality support)
- *PICO 4*
- Windows Mixed Reality (WMR)-compatible
- OpenVR-compatible
- OpenXR-compatible


> **Notice:** The list above includes devices that we test on a regular basis, so the range of supported devices may be wider.


## Mixed Reality Development


Thanks to ***Varjo*** integration, you can implement *Mixed Reality* applications to be run with Varjo HMDs.


UNIGINE supports **Varjo SDK 3.10.0** with chroma keying, so you can change environments quickly, along with depth testing enabling you to composite and sort real and virtual worlds together by utilizing the depth-sensing capabilities of *XR-3* and *XR-1*. Tracking of static or dynamic real-world objects using the video pass-through cameras via markers is also available now. With Alpha Blend capabilities you can blend your virtual environment with the real world enabling efficient collaboration in both.


You can also use **object markers** to track static or dynamic objects in the user environment in both XR and VR applications. VR apps without video pass-through rendering can use these markers to align virtual objects in the scene with physical objects in the real world.


Check out the **[C++ VR Sample](...md)** showcasing *Mixed Reality* features.


To develop an application, you need to install *[Varjo Base](https://varjo.com/downloads/#varjo-base)* and *[SteamVR](https://store.steampowered.com/about/)*.


Mixed Reality management is performed via the *[VRMixedReality](../api/library/vr/class.vrmixedreality_cpp.md)* and *[VRMarkerObject](../api/library/vr/class.vrmarkerobject_cpp.md)* classes of UNIGINE API.


## Supported Graphics APIs


The following graphics APIs are supported out of the box:


- DirectX 12
- Vulkan


## Initialization


By default, VR is not initialized. To run the engine with VR, you need to specify the *[-vr_app](../code/command_line.md#vr_app)* command-line option on the application start-up.


- For OpenVR: ```bash -vr_app openvr ```
- For Varjo: ```bash -vr_app varjo ```
- For OpenXR: ```bash -vr_app openxr ```


## VR Input


UNIGINE VR input system provides access to a wide range of VR devices: you can manage input from *VR controllers*, *head-mounted displays (HMDs)*, *base stations*, and *trackers*.


For more details on types of VR devices and their examples, check the article on *[VR Input System](../vr_development/vr_input.md)*.


## VR Template


UNIGINE provides a *[VR Template](../content/vr/index.md#vr_template)* that is used to facilitate the creation of a custom application for VR. It contains a set of 3D models of popular VR controllers and the implementation of basic mechanics such as grabbing and throwing objects, pressing buttons, opening/closing drawers, and a lot more.


The template is created using the [Component System](../principles/component_system/index.md), so you can easily extend its functionality.


Refer to the *[Getting Started with VR](../start/vr/index_cpp.md)* section to learn how to use the template for *C++/C# VR* project development.


## Basic Workflow on Using VR


Unlike other 3D applications, developing a **VR** application is more complex: you should set up a VR environment, add interactive elements, process user input from various VR devices, and so on.


The general workflow of the VR application development in UNIGINE is the following:


1. Set up your UNIGINE project for VR development:

  1. Set up a VR device (check the instructions provided by the vendor, if necessary).
  2. Configure the project to use the appropriate VR mode. You can perform it via SDK Browser for *C++/C#* projects or in UnigineEditor for C# projects, depending on your preferred method of running your application.
  3. [Initialize VR](#vr_init).
2. Create the VR environment:

  - Create a 3D environment for your VR project by using 3rd-party 3D modeling and level design tools and UnigineEditor.
  - Extend the VR environment with animations, sounds, videos, and other interactive elements.
3. Make the VR environment more interactive:

  - Implement components to extend the functionality of objects in the environment and process [user input](../vr_development/vr_input.md).
  - Use [UNIGINE's VR Template](../start/vr/index_cpp.md) (available for C++ and C# APIs) that offers a basic set of VR components and allows users to move around and interact with objects in the environment.
4. Debug and profile your VR application. Use the VR platform-specific and UNIGINE built-in profiling tools to improve performance.
5. Build and deploy your VR application.
